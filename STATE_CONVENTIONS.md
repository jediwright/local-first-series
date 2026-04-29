# State Conventions

Authoritative conventions for Y.js state across all four prototypes in the
local-first series. Every build session reads this document before writing any
code that touches Y.js state. These conventions exist because the single most
damaging class of bugs in this codebase — stale references, key format
inconsistencies, observer failures — all trace back to sessions that didn't
have an authoritative spec to check against.

These are not preferences. They are requirements.

---

## The Y.js Document

All state lives in a single Y.js document per prototype, persisted to IndexedDB
via `y-indexeddb`. The document is initialized once at module load. All maps are
accessed via getter functions — never via module-level cached constants.

```typescript
import * as Y from 'yjs'
import { IndexeddbPersistence } from 'y-indexeddb'

export const doc = new Y.Doc()
export const provider = new IndexeddbPersistence('app-state', doc)
```

---

## Map Names

| Prototype | Map name | Value type | Notes |
|-----------|----------|------------|-------|
| All | `profile` | Nested Y.Maps | Identity, preferences, trust graph, history |
| checkout-seam | `cart` | Y.Map | Cart items keyed by productId |
| checkout-seam | `orders` | Y.Map | Order records keyed by orderId |
| checkout-seam | `catalog` | Y.Map | Product catalog keyed by productId |
| checkout-seam | `customer` | Y.Map | Customer profile fields |
| fhir-seam | `intake` | Y.Map | Form field values keyed by field name |
| fhir-seam | `submissions` | Y.Map | Submission records keyed by submissionId |
| Local-First Social | `pings` | Y.Map | Ephemeral ping state keyed by channel |
| Local-First Social | `threads` | Y.Map | Thread history keyed by canonical thread key |
| Local-First Social | `channels` | Y.Map | Interest channel memberships |
| Local-First Social | `assets` | Y.Map | Thread asset library keyed by assetId |

---

## The profile Map — Nested Structure

The `profile` map is shared across all prototypes as the pattern for local
identity and relationship state. In Local-First Social it carries the full social graph.

```typescript
// Access pattern — always via doc, never via cached reference
const profileMap = doc.getMap('profile')

// Keys within profile
profileMap.get('identity')     // plain object: { displayName, handle, ... }
profileMap.get('preferences')  // plain object: { defaultPingType, ... }

// Nested Y.Maps — must be accessed via getOrCreate, never cached at module level
profileMap.get('trust_graph')         // Y.Map<TrustEntry>
profileMap.get('ping_history')        // Y.Array<PingEntry>
profileMap.get('channel_memberships') // Y.Array<ChannelMembership>
```

**Critical:** Nested Y.Maps and Y.Arrays inside `profile` must be accessed via
a getter function that reads fresh from the document on each call. Do not export
them as module-level constants. See the stale reference rule below.

---

## Key Formats

Consistent key formats are required. Inconsistent key formats produce silent bugs
where data written in one session cannot be found in another.

### Handle format

User handles are stored and transmitted with the `@` prefix.

```typescript
// Correct
profile.set('handle', '@jediwright')
trustGraph.set('@jediwright', entry)
relay.emit('ping', { to: '@jediwright' })

// Wrong — bare handle without prefix
profile.set('handle', 'jediwright')        // ✗
trustGraph.set('jediwright', entry)        // ✗
```

The `@` prefix is the canonical format everywhere in the codebase. The relay,
the trust graph, the thread keys, and the profile map all use `@handle`.
Strip the prefix only at the display layer if needed for presentation.

### Thread key format

Thread keys are canonical and symmetric — the same key regardless of which
user initiates.

```typescript
// Canonical thread key: always alphabetical order, always with @ prefix
function threadKey(handleA: string, handleB: string): string {
  const a = handleA.startsWith('@') ? handleA : `@${handleA}`
  const b = handleB.startsWith('@') ? handleB : `@${handleB}`
  return [a, b].sort().join(':')
}

// Example
threadKey('@alice', '@bob')     // '@alice:@bob'
threadKey('@bob', '@alice')     // '@alice:@bob' — same result
```

This format is used in `threads` map keys and in relay routing. Do not
use bare handles in thread keys.

### Order / submission IDs

```typescript
// Timestamp-based IDs — milliseconds since epoch, stringified
const orderId = `order_${Date.now()}`
const submissionId = `submission_${Date.now()}`
```

### Asset IDs

```typescript
const assetId = `asset_${Date.now()}_${Math.random().toString(36).slice(2, 7)}`
```

---

## The Stale Reference Rule

**Never export nested Y.Maps or Y.Arrays as module-level constants.**

This is the most important rule in this document. The stale reference bug has
appeared in two prototypes (checkout-seam cart badge, Local-First Social trust graph)
and costs significant debugging time each time.

The failure mode: a Y.Map or Y.Array nested inside another Y.Map is captured
as a module-level export at import time, before `y-indexeddb` has loaded
persisted state from IndexedDB. When the persistence provider loads, it applies
updates to `doc` — but the cached reference points to the original empty object,
not the hydrated state.

```typescript
// Wrong — stale reference captured at module init
export const trustGraphMap = profileMap.get('trust_graph') as Y.Map<TrustEntry>

// Correct — getter reads fresh from document on each call
export function getTrustGraphMap(): Y.Map<TrustEntry> {
  return doc.getMap('profile').get('trust_graph') as Y.Map<TrustEntry>
}
```

This applies to all nested Y.Maps and Y.Arrays regardless of depth. If a
Y.Map is accessed via another Y.Map, it must be fetched fresh on each access,
not cached.

---

## The `attachArrayObserver()` Rule

Every hook that observes a Y.Array nested inside a Y.Map must use the
`attachArrayObserver()` pattern. No exceptions.

The failure mode without this pattern: the observer attaches to the initial
Y.Array reference. After `y-indexeddb` loads persisted state, it may replace
the nested array — the observer is now attached to a stale reference and the
hook reads empty state.

```typescript
function attachArrayObserver(
  map: Y.Map<unknown>,
  key: string,
  setState: (items: unknown[]) => void
) {
  const attach = () => {
    const arr = map.get(key) as Y.Array<unknown>
    if (arr) {
      arr.observe(() => setState(arr.toArray()))
      setState(arr.toArray())
    }
  }
  map.observe((event) => {
    if (event.keysChanged.has(key)) attach()
  })
  attach()
}
```

Apply `attachArrayObserver()` to all Y.Arrays at hook initialization — not
after discovering a bug. This pattern must be in the session kickoff prompt
so it is applied from the first hook written.

---

## Transactions

Mutations that update multiple keys atomically must use `doc.transact()`.

```typescript
// Correct — atomic update
doc.transact(() => {
  cartMap.set(productId, { quantity, price, name })
  profileMap.set('cartUpdatedAt', Date.now())
})

// Wrong — two separate mutations, observable intermediate state
cartMap.set(productId, { quantity, price, name })
profileMap.set('cartUpdatedAt', Date.now())
```

Use `doc.transact()` for: cart mutations with metadata updates, order writes,
intake form submissions, trust tier changes with history updates, ping sends
with streak updates.

Single-key mutations that stand alone do not require a transaction.

---

## Relay-Routing Keys vs. Local-Graph Keys

In Local-First Social, two key namespaces must not be mixed:

**Relay-routing keys** — used to address messages through the WebSocket relay.
These are the `@handle` strings registered with the relay at connection time.
The relay uses these to route handshake signals. They are ephemeral — the
relay's handle registry is rebuilt from reconnecting clients on restart.

**Local-graph keys** — used to key entries in the trust graph, thread map,
and ping history. These are also `@handle` strings but they are persistent —
stored in IndexedDB and survive relay restarts.

The formats are identical, which is intentional — it makes lookup straightforward.
The distinction matters for understanding what is server-state vs. client-state:
relay-routing keys exist only while the relay is running; local-graph keys
persist indefinitely on the client.

Do not store relay-routing state in the Y.js document. The relay connection
state (`established`, `connecting`, `disconnected`) is React component state,
not Y.js state.

---

## Seam Write Discipline

### Write-before-POST (fhir-seam, and any high-stakes seam)

Local state must be written to IndexedDB before the network request fires.
The user must not lose data to a failed POST.

```typescript
// Correct order
await ydocPersistence.whenSynced  // confirm local write
const response = await fetch(fhirEndpoint, { method: 'POST', body: bundle })
if (response.ok) {
  submissionsMap.set(submissionId, { status: 'accepted', submittedAt: Date.now() })
}
```

### Write-on-success (checkout-seam)

The order record is written to local state only on confirmed server success.
The cart is preserved on failure — never cleared until success is confirmed.

```typescript
const response = await fetch('/api/checkout', { method: 'POST', body: cart })
if (response.ok) {
  doc.transact(() => {
    ordersMap.set(orderId, { items, total, confirmedAt: Date.now() })
    cartMap.clear()
  })
}
// On failure: do nothing to cart — user can retry
```

---

## Environment Variables

Serverless functions (Vercel API routes) require environment variables set in
the deployment target, not just `.env.local`. This has caused a production
failure once (Stripe key missing in Vercel environment).

Pre-deploy checklist item: verify all environment variables used by API routes
are set in the Vercel project settings before deploying.

Variables by prototype:

| Prototype | Variable | Where used |
|-----------|----------|------------|
| checkout-seam | `STRIPE_SECRET_KEY` | `/api/checkout.js` |
| checkout-seam | `STRIPE_PUBLISHABLE_KEY` | Client bundle |
| fhir-seam | `FHIR_ENDPOINT` | `/api/submit.js` |
| Local-First Social | `RELAY_URL` | `src/lib/relay.js` |
| Local-First Social | `VITE_RELAY_URL` | Client bundle (Vite env prefix required) |

---

## Codespace Terminal Constraints (Local-First Social)

The GitHub Codespace terminal auto-converts dot-notation identifiers (`Y.Map`,
`WebSocket.OPEN`, etc.) into markdown hyperlinks when writing files via heredoc.
This corrupts TypeScript type annotations silently.

Rules for terminal work in Local-First Social:
- Write Python patch scripts to `/tmp/scriptname.py` using `cat >` heredoc, then run with `python3`
- For any file containing `Y.Map` TypeScript types: use the Codespace editor, not the terminal
- For git commit messages: `echo 'message' > /tmp/commitmsg.txt && git commit -F /tmp/commitmsg.txt`
- Build and deploy commands are safe to run in terminal — the constraint applies only to file writes

---

## Session Kickoff Checklist

Every build session that touches Y.js state must confirm these before writing code:

- [ ] This document has been read in full
- [ ] `DESIGN.md` has been read
- [ ] No new Y.Map or Y.Array is being exported as a module-level constant
- [ ] All new hooks that observe nested Y.Arrays use `attachArrayObserver()`
- [ ] All new handle strings use `@handle` format
- [ ] All new thread keys use the canonical sort → join format
- [ ] Multi-key mutations use `doc.transact()`
- [ ] Acceptance criteria for this session are written before code generation begins

---

*Part of the [Systems of Thought local-first series](https://github.com/jediwright/local-first-series)*
*MIT License · Last updated April 29, 2026*
