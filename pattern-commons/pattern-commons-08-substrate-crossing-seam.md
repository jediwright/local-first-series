⚑ STAMP: SINGLE-CONTEXT — NOT PANELED
All claims produced across producer (v0.1) and Counter-Pass iterations 1–3
(2026-08-17). Counter-Pass program complete — three iterations; all six
resolutions survive narrowed; no design verdict overturned at any iteration.
Four mechanical residuals from iteration 3 applied as v0.1.3. Landscape Position section added
as v0.1.4 (2026-08-18). Form C
cluster PROPOSED per UFO Lexicon v1.8. All new vocabulary PROPOSED pending
promotion. CONTEXTUAL register throughout. NI-5 in effect throughout.
v0.2 (2026-08-30): Phase 3 as-implemented terms absorbed; rebased onto v0.1.4.

---

# Pattern Commons #8 — The Substrate-Crossing Seam

**Status:** Draft v0.2.1 — Phase 3 as-implemented terms absorbed (UFO Lexicon v2.5). Phase 3 closed and verified at `fb05ea1`. Some sections still describe the prototype as pending; a post-prototype revision (v0.3) is queued — see Changelog.  
**Date:** August 30, 2026 (v0.2) · August 18, 2026 (v0.1.4)  
**Author:** J. Wright (UX Minds, LLC) · AI-assisted  
**Derived from:** Substrate-crossing seam speculative design sketch,  
2026-08-17 (`substrate-crossing-seam-design-sketch_2026-08-17.md`);  
OQ-5 operator decision, 2026-08-17; fact-base corrections web-verified  
2026-08-17.  
**Series:** Local-first prototype series — Pattern Commons  
**Parent pattern:** Pattern Commons #0 — The Governed Crossing (v0.1.1)  
**Companion entries:** #1 checkout seam · #2 high-stakes seam ·  
#3 profile map as local CRM · #4 attachArrayObserver (infrastructure) ·  
#5 distributed seam · #6 CRDT as trust graph · #7 employment seam  
**Governing architecture:** Artifact B — Form C Standalone Framework  
Manifesto-Spec (r2.4). This entry does not amend Artifact B and makes  
no claim on its behalf.  
**Base shape:** `seam:CrossingRecord`  
(`https://jediwright.github.io/seam-stack/vocab/crossing-record/0.1#`)  
**Stamps:** ⚑ SINGLE-CONTEXT — NOT PANELED. All confidence ~ unless  
otherwise marked. Ledger: SL-0105 (issuance); SL-0106 (Lexicon v1.8);  
SL-0107 (CP iter 1); SL-0108–SL-0109 (CP iter 2); SL-0110–SL-0112  
(CP iter 3 / program close); SL-0122 (v0.1.4 Landscape Position);  
SL-0190 / SL-0191 validation events fire at v0.2 (Lexicon v2.5 L4  
absorption; reconciliation routed lines).  

---

## What This Entry Is — and Is Not

This is the second Pattern Commons entry authored as a domain
instantiation of the governed crossing after the pattern was named
(PC#0), and the first authored **before its prototype exists**. The
employment seam (#7) earned its spec through five prototype builds and
a reference implementation; this entry is issued as **design intent**,
on the worked precedent that #7 itself began as a Pattern Commons entry
before it became a Form C demonstration.

The entry therefore names its own epistemic position:

- **Every design resolution in this entry is speculative** (~,
  single-context). Counter-Pass program complete — three iterations;
  all design verdicts survive (narrowed where noted). No resolution
  is prototype-verified.
- **NI-5 is in force throughout:** the architecture is local-first
  specific on current evidence. This entry advances **zero generality
  claims**. It is the speculative second domain, named as such.
- **Artifact B is untouched by this entry.** The Form C manifesto-spec
  neither cites nor anticipates this seam. If a prototype produces
  evidence, Artifact B may be amended later by that evidence — the
  sequencing the habitable finding established — not by this document.
- The Known Limits section (KL-1–KL-12) is not an appendix. It is the
  honest core of the entry: the inventory of everything the design
  cannot resolve speculatively, each item paired with the class of
  evidence that would close it.

Per PC#0's conformance requirements for new entries, this document
(1) cites PC#0 as the parent pattern, (2) specifies only what diverges
from the four constitutive properties and the Seam Stack, (3) names
the seam trigger explicitly, and (4) adopts `seam:CrossingRecord` as
the base shape for all governed-event records.

---

## The Pattern in One Sentence

The substrate-crossing seam is the boundary event that fires when a
record governed on a local-first substrate is published into a target
substrate with different epistemic properties — different regimes for
revocation, exposure, and record integrity — and the architectural
argument is that the crossing must be granted, gated, and recorded
**before it fires**, with the record honestly declaring that the
emitting architecture's enforcement terminates at the crossing and
that no upper bound on subsequent exposure can be asserted.

---

## The Problem It Solves

When a person publishes content from a local-first substrate (CRDT,
no coordinator, partition-tolerant, capability-governed) into AT
Protocol (PDS-hosted, DID-anchored, relay-distributed, globally
indexed), the epistemic properties of the record change irreversibly
at the crossing:

- **Revocation semantics change.** On the local-first side, revocation
  closes a capability stream — an enforcement. On the AT Protocol
  side, deletion is broadcast as a first-class firehose event and the
  Sync specification requires mirrors to respect it in a timely
  manner — but retention by third-party subscribers is unpreventable.
  Post-crossing revocation is a **propagated request, not an
  enforcement**.
- **The existing vocabulary has no value for this condition.** The
  crossing-record `boundType` vocabulary's floor value,
  `exposure-upper-bound`, still implies that a bound can be asserted.
  After a substrate crossing into a globally indexed regime, it
  cannot. The vocabulary needs a value for the exposure claim that
  claims nothing beyond the crossing.
- **The grant must carry the regime change.** A grant that authorizes
  a substrate crossing without explicit, person-authored
  acknowledgment of the enforcement termination at firing time is a
  grant that hides its most consequential property.
- **P9 applies reflexively.** The architecture cannot claim
  post-crossing control it does not enforce — including inside its
  own spec language.
- **P14 supplies the frame.** P14 names relay boundaries as governed
  crossings. Prior worked crossings governed boundaries between
  **institutional parties** on comparable substrates. The design work
  here is applying P14 where the two sides of the crossing have
  **different substrate properties** — different epistemic regimes —
  not merely different parties.

Every prior seam in this series fails cleanly: the cart is preserved,
the bundle is preserved, local state is intact, the worker retains the
knowledge graph. What is genuinely new at #8 is not irreversibility per
se — every crossing that hands data to a counterparty is already
irreversible in the copy sense, which is why `exposure-upper-bound` is
the standing floor. What is new is **bound-assertability**: prior seams
could honestly assert an upper bound (a named counterparty, an enumerable
peer set); #8 crosses into a regime where no bound at all is assertable.
All governance weight therefore shifts to the pre-crossing side of the
boundary — which is exactly where the governed-crossing pattern puts it.

---

## The Seam Trigger

Per PC#0, the trigger is named explicitly:

**The seam fires when a publish operation is invoked that will move a
record — or an export the architecture mediates — across a declared
substrate boundary into a target regime with different epistemic
properties for revocation, exposure, or record integrity.**

Note: content *derived* from governed records (paraphrase, screenshot,
re-publication outside the governed stack) crosses no boundary the gate
can see. That surface is an out-of-reach limit named here rather than a
scope the gate claims — see KL-11.

The reference target regime for this entry is AT Protocol (publish to
a PDS, with relay distribution and global indexing downstream). The
trigger is the publish invocation itself, not PDS acceptance and not
relay ingestion — those are post-crossing events the gate cannot see
(see the gate section below).

State changes that do **not** fire this seam: local edits, sync among
capability-governed peers on the same substrate, and crossings between
parties on substrates with equivalent epistemic properties (those are
governed by the existing seam types, #1–#7).

---

## Carry-In: What This Entry Inherits Unchanged

The four constitutive properties of the governed crossing (PC#0) —
declared scope, grant, gate, record — are invariant and carry in full,
with one qualification stated at design-session open and preserved
here:

**Gate qualification (temporal jurisdiction).** The gate's enforcement
jurisdiction ends at the crossing moment. "Checks current state at act
time" and "fails closed" are unchanged. Post-crossing gate behavior
neither exists nor is implied by any field in this design.

Also carried unchanged:

- **The finality-arbiter-free constraint.** No field or mechanism in
  this entry requires a coordinating party at record-emission time.
- **The Q6 lock** (trust-the-author-with-named-boundary):
  `lineageAnchorType: author-declared` is the only available anchor
  value; signed variants remain locked pending infrastructure.
- **The `seam:CrossingRecord` base shape** (Form C Item 2): identity
  group, provenance linkage group, lineage anchoring group, evidence
  scope group — all inherited, not repeated here.
- **Boundary principles in scope:** P8 (explicit, minimal, designed);
  P9 (exposure claims are upper bounds); P10 (data shapes carry
  lineage and horizons); P11 (agents are governed parties); P12
  (longevity commitments have terms); P13 (governance composes beyond
  the individual); P14 (relay boundaries are governed crossings).
  All PROPOSED per UFO Lexicon v1.7.

---

## Substrate Fact Base

The design rests on three substrate facts, web-verified 2026-08-17
(~, single-context verification):

**1. AT Protocol deletion is a propagated request.** Deletion is
broadcast as a first-class firehose event; the Sync spec requires
mirrors to respect record deletions in a timely manner. What the
protocol lacks is enforcement: retention by third-party subscribers is
unpreventable. The honest characterization — and the one this entry's
vocabulary encodes — is that post-crossing revocation is a propagated
request, not an enforcement. The flat claim "post-relay recall is not
possible" is rejected as imprecise in both directions; the epistemic
conclusion (no upper bound on post-crossing exposure is assertable)
survives.

**2. Firehose data is self-certifying.** Repository data synchronized
over the AT Protocol firehose carries verifiable signatures; consuming
services can verify it without contacting the PDS. This gives
cross-substrate references a content-addressed, signature-verifiable
integrity anchor (CID) requiring **no cooperation from the target
regime** — the load-bearing fact for the record-chaining design below.

**3. AT Protocol identity is default provider-custodied.** By default
the PDS holds both the signing key (signs every repo commit) and the
rotation key (controls the identity). A PDS operator can act as the
user in a way that is cryptographically indistinguishable from the
user's real activity. Sovereignty is opt-in recoverable: a user can
enroll a higher-priority rotation key, and unwanted PLC operations are
revertible within 72 hours. The PLC directory — the resolution root
for nearly all AT Protocol accounts — is centralized under Bluesky
Social PBC regardless. Summary: default provider-custodied;
conditionally mixed-custody; centralized resolution root in all cases.

**Reference note — iroh.** The iroh/n0 stack (connection-level P2P,
end-to-end encryption, relay fallback where relays see node
identifiers, not content) served as a second reference point in
design. An iroh-gossip topic crossing keeps content encrypted to topic
members and produces no global index — it sits closer to the
local-first side epistemically. It confirms the **axis** the new
vocabulary value names without populating the far end of it. It is not
an AT Protocol analog, and its own crossing classification is
deferred (KL-6).

---

## The Vocabulary Extension — Two Slots, Not One

The design question was where the substrate crossing enters the
crossing-record vocabulary. Three candidate values circulated in
pre-design work; the resolution splits the concept across two existing
slots rather than forcing it into one, because the candidates were
naming two different things — an **event class** and an **exposure
claim** — and the vocabulary's internal grammar keeps those apart
(`governanceEvent` is the governance-semantics discriminant;
`boundType` is the exposure claim the record makes).

**New `governanceEvent` value** *(PROPOSED)*:

| Value | Definition |
|---|---|
| `substrate-crossing` | A governed crossing whose two sides have different substrate properties — different epistemic regimes for revocation, exposure, and record integrity. The event-class discriminant for substrate-crossing seam records. Pairs with `boundType: exposure-unbounded`. |

**New `boundType` value** *(PROPOSED)*:

| Value | Definition | Used by |
|---|---|---|
| `exposure-unbounded` | The record claims that, at emission, the emitting architecture's enforcement terminated at a declared crossing into a regime where no upper bound on subsequent exposure can be asserted. Post-crossing revocation, where the target substrate provides it, is a propagated request, not an enforcement; the record asserts neither its delivery nor its honoring. The P9-reflexive floor value: the exposure claim that claims nothing beyond the crossing. | Substrate-crossing seam records (pre-crossing intent and completion instances). |

`exposure-unbounded` sits **below** `exposure-upper-bound` in a scale
that orders *admissible claim strength* — not a single epistemic
quantity (the scale spans bound-assertability at the lower end and
review-strength at the upper end). The ordering rule, amended to
accommodate the new floor value: **the asserted `boundType` must match
the architecture's actual enforcement capacity; both overclaiming and
underclaiming are substitution errors; overclaiming is inadmissible per
P9.** An architecture that can assert a named-counterparty bound must
not substitute `exposure-unbounded`; an architecture whose enforcement
terminates at a globally indexed regime must not substitute
`exposure-upper-bound`. (CP-F1 / CP-F3 — ordering note rewrite.)

**Companion field** *(PROPOSED — conditional, substrate-facing)*:

| Field | Vocabulary | Purpose |
|---|---|---|
| `recallSemantics` | `enforced-stream-close` / `propagated-request` / `none` | Declares what revocation means in the target regime. AT Protocol: `propagated-request`. Keeps `boundType` clean while preserving the substrate fact in-record. |

---

## The Grant Model — Acknowledged Regime Change, No Waiver

The grant is the legal-responsibility anchor (constitutive property
2). For this seam, the grant must additionally carry the person's
explicit acknowledgment of the regime change — fixed at grant time,
before the act, so the epistemic claim cannot be retrofitted.

**Mechanism:** a `crossingType` discriminant on the grant, whose value
`substrate-crossing` **structurally requires** a conditional field
group. This matches the schema's existing conditional-requirement
pattern (`provenanceStatusBasis` required when status ≠ `asserted`;
`chainDepth` required when `chainReference` is present).

**Conditional field group** *(PROPOSED — required when `crossingType:
substrate-crossing`)*:

| Field | Purpose |
|---|---|
| `regimeAcknowledgment` | Declared acknowledgment, at grant time, that enforcement terminates at the crossing and that post-crossing revocation is (per `recallSemantics`) a request, not an enforcement. Author-declared; Q6 lock applies. The gate checks *presence*, not authorship — under Q6 the field is a declared-acknowledgment ceiling, not a verified-acknowledgment guarantee; prefilled boilerplate is not architecturally distinguishable from person-authored text. Juridical effect (whether this field constitutes a waiver or consent in any legal forum) is a question for the legal substrate, not the schema. Form, authorship-verifiability, and effect review: see KL-7. |
| `declaredBoundType` | The `boundType` the crossing record will carry — `exposure-unbounded`, named at grant time so the epistemic claim is fixed before the act. |
| `recallSemantics` | Controlled vocabulary as defined above; declared per target substrate at grant time. Note: target-substrate semantics can change between grant time and publish time (protocol revisions, PDS policy changes); a standing grant could span such a change, making the declared value stale at act time. The gate re-asserts the declared value but cannot verify substrate currency. See KL-12. |

**Deliberate exclusion: no `waiver` field.** "Waiver" is
legal-register language implying the architecture extracts a rights
disposition. That overclaims the grant's juridical function (P9) and
drifts toward the platform authoring legal meaning rather than
recording acknowledgment. The `regimeAcknowledgment` field carries the
epistemic content; whether the acknowledgment has waiver effect is a
question for the legal substrate, not the schema. This exclusion is a
design decision of the entry, not an open question.

---

## The Gate — Fire Once, Jurisdiction-Complete

The gate honestly enforces, pre-crossing and at crossing moment only:

1. **Grant current at act time** (`assertCapabilityCurrent()`,
   unchanged from the pattern).
2. **Conditional group present and bound.** The
   `crossingType: substrate-crossing` conditional field group is
   present and bound to this grant. SHACL-enforceable at the
   Governance layer.
3. **Record-before-crossing ordering.** The pre-crossing intent
   record (`boundType: exposure-unbounded`, gate result) is minted
   **before** the publish call fires. At every other seam, a
   late-minted record is sloppy; here it is structurally
   unrecoverable — there is no post-act position from which the
   pre-act state can be honestly attested. This ordering is a required
   discipline of the seam, anchored `author-declared` (Q6 lock)
   until `timestamp-signed` infrastructure unlocks. The locked
   `timestamp-signed` value is precisely the infrastructure that would
   convert this discipline into a structurally enforced invariant.
   See KL-9. (CP-F8.)
4. **The gate fires exactly once.** Its role completes at the
   crossing moment. No post-crossing gate behavior exists, is
   claimed, or is implied by any field.

The gate fails closed, as always: unconfirmed grant state blocks;
silence blocks; a missing conditional group blocks.

**TOCTOU note (CP-F9).** The gate checks grant currency, then the
publish fires; a revocation landing in that window is checked-then-
crossed. This race cannot be eliminated under the finality-arbiter-free
constraint. The gate's check is honest to check-time, not to fire-time;
the intent record's `emittedAt` bounds the window in-evidence. See KL-10.

---

## The Two-Record Pattern — Intent and Completion

The gate cannot verify that the publish succeeded: PDS acceptance is
not relay ingestion, and neither is visible from the emitting side at
act time. The design therefore splits the record:

**Pre-crossing intent record.** Gate-governed, mandatory, minted
before the publish call. `recordType: crossing-intent` /
`governanceEvent: substrate-crossing` / `boundType: exposure-unbounded`.
Also carries the gate result, the identity binding block (below), and
an `authorizedContentDigest`
(PROPOSED — a CID or hash of the content being authorized to cross,
computable locally before the publish fires). The digest is the binding
between what was authorized and what the completion record later
attests; without it, a deferred party can verify the published record's
integrity via CID but cannot verify it is the content the grant
authorized. This is the last record the architecture can fully stand
behind, and it says exactly that. (CP-F11.)

**Completion record.** Post-hoc. `recordType: crossing-completion` /
`governanceEvent: substrate-crossing` / `boundType: exposure-unbounded`.
References the intent record via the chain (`chainReference` to the
intent record's `recordId`; `chainDepth` increments;
`lineageAnchorType: author-declared` — Q6 lock in force). Carries the
crossing-target fields (below).

**Failure states (sketch — population by KL-1 prototype; PC#0 conformance requires naming the state space now):**

| State | Condition | Chain posture |
|---|---|---|
| `crossing-intent-pending` | Intent record emitted; publish not yet attempted | Intent record present; no completion |
| `crossing-intent-failed` | Publish attempt failed before completion record minted | Intent record present; no completion; retry semantics: open — see KL-8; interim discipline: new gate pass |
| `crossing-complete` | Completion record minted; `crossingTargetCID` matches `authorizedContentDigest` content | Chain closed |
| `crossing-complete-digest-mismatch` | Completion record minted but CID does not match the authorized digest | Legible mismatch; not a valid completion; chain remains open |
| `crossing-unconfirmed` | Intent present; no completion record; `crossingTimeoutHorizon` elapsed | Fail-closed legible state: "crossing not confirmed complete" |
| `completion-mint-failed` | Publish succeeded per PDS acknowledgment; completion record minting failed | Worst-case state — crossing happened; chain reads unconfirmed forever unless completion is retroactively minted (author-declared; KL-8) |

Retry semantics, multi-intent ambiguity, and empirical failure-mode population: KL-8. (CP-F7.)

**Fail-closed legibility.** An intent record with no completion record
reads as **"crossing not confirmed complete."** The absence is
legible — which is the correct fail-closed posture for a gate that
cannot see past the boundary. A deferred party assembling the chain
does not need the target substrate's cooperation to know that a
crossing was attempted and never confirmed.

---

## Record Chaining Across the Boundary — The Asymmetric Bridge

**The chain of evidence crosses; the chain of governance terminates at
the crossing. Declared, not hidden.**

**Completion-record fields** *(PROPOSED — conditional)*:

| Field | Purpose |
|---|---|
| `crossingTargetURI` | The `at://` URI of the published record. |
| `crossingTargetCID` | The commit/record CID. Per substrate fact 2, the CID is a content-addressed, signature-verifiable anchor requiring no trust in the PDS — the strongest cross-substrate integrity claim available that requires no cooperation from the target regime. Note: verification requires the content to be retrievable; post-deletion or post-PDS-death, the anchor anchors nothing retrievable. The `evidenceDecay` field (base shape, optional) should be set on completion records to surface this horizon. See KL-2 (extended). (CP-F12.) |

**No symmetric back-reference is required.** A custom AT Protocol
lexicon *could* carry a `seamCrossingRef` back-pointer from the
published record to the intent record, and a prototype should attempt
it — but **requiring** it would place a governance obligation on a
substrate this architecture does not govern, a P9 violation committed
from inside the spec. The back-pointer is optional if the target app
schema supports it, and never load-bearing.

The design is a precise composite of the options considered: not a
bare URI pointer (which would cross the evidence without declaring the
governance boundary), and not a fully closed chain (which would
discard the CID integrity anchor). **Evidentially continued via
URI + CID; governance-terminated by declaration.** The completion
record is the last governed record in the chain, and says so.

C4 (resolvable chain) is satisfied up to the declared termination.
P10 is satisfied by carrying the horizon in-record rather than
implying continuity that does not exist.

---

## The Identity Model — Bind, Don't Merge

The two sides of the crossing have different identity custody models,
and the record must bind them without asserting equivalence.

**Identity binding block** *(PROPOSED — conditional, on the intent
record, required when `crossingType: substrate-crossing`)*:

| Field | Purpose |
|---|---|
| `grantorDID` | Seam-side DID — self-sovereign, person-held keys (the employment seam's Class A discipline). |
| `targetDID` | AT Protocol DID (`did:plc` or `did:web`). |
| `identityCustodyClass` | Controlled vocabulary *(PROPOSED)*: `self-custodied` / `mixed-custody` / `provider-custodied`. AT Protocol default: `provider-custodied`. With a user-enrolled higher-priority rotation key: `mixed-custody`. |

**Attribution strength cap.** The claim "post-crossing activity under
`targetDID` is attributable to the grantor" enters the intent record's
`provenanceStatus` at `asserted`. The cap by custody class:

- `provider-custodied`: capped at `asserted`. The architecture cannot
  distinguish the person's signature from the PDS's (substrate fact 3);
  KL-3 is the open question on this class.
- `mixed-custody`: also capped at `asserted` pending KL-3's closing
  evidence. The 72-hour revert window means an adversarial PDS's act
  stands if unnoticed; on current evidence `mixed-custody` does not
  justify any upgrade over `provider-custodied`. The upgrade path
  opens only when KL-3's verification arrives. (CP-F13.)
- `self-custodied`: may reach `confirmed` via the existing
  `provenanceStatusBasis` mechanism if the declaration is
  independently verifiable.

The cap binds the intent record's `provenanceStatus` as a whole — the
attribution claim lives on the intent record; there is no per-claim
status field in the base shape and none is introduced here. (CP-F15.)

This reuses the existing `provenanceStatus` vocabulary; no new
epistemic apparatus is introduced. It is P9 applied to attribution:
the custody class caps the bound.

**Ceremony.** The gate checks that the binding block is present and
the custody class is declared. It does **not** verify the custody
class — no adversarial-PDS test is available at act time. The
declaration is author-declared; the Q6 lock applies. Deferred
verifiability: did:plc custody state is publicly resolvable, so a
misdeclared custody class is checkable by a deferred party against the
DID document even though the gate cannot verify it at act time. A
misdeclaration is therefore legible after the fact — a meaningful
strengthening of the ceremony beyond a pure honor-system posture.
(CP-F14.)

**Structural asymmetry, noted and deferred.** Even a
`self-custodied`-adjacent AT Protocol identity carries a centralized
PLC resolution dependency that the seam-side identity does not. The
custody vocabulary may eventually need a fourth axis for resolution
custody as distinct from key custody. Deferred; not resolved by this
entry.

P11 note: the PDS is a governed-party-shaped actor on the far side of
the crossing. The record must not silently treat it as the person.
This entry does not extend the participant-class model to the target
regime — it only refuses to conflate the PDS with the grantor in the
attribution claim.

---

## How It Sits in the Series

| | #1–#6 (built prototypes) | #7 employment seam | #8 substrate-crossing seam |
|---|---|---|---|
| Seam fires | Per transaction / intake / connection | Per relationship state change | Per publish across a declared substrate boundary |
| Far side of seam | Server or peer on comparable substrate | Receiving party + legal record | A different epistemic regime (reference: AT Protocol) |
| Failure posture | Local state preserved; retry | Nine-state taxonomy; worker's copy is source of truth | Intent-without-completion is legible; local state preserved |
| **Exposure posture** | Bounded-set — named counterparty or enumerable peer set; `exposure-upper-bound` assertable | Bounded-set — receiving party + legal record; `exposure-upper-bound` assertable | **Unbounded — no bound assertable after crossing; `exposure-unbounded` is the P9-honest value** |
| Governance weight | At the seam | At the seam, both sides | **Entirely pre-crossing; terminates at the boundary, by declaration** |
| Evidence status | Built | Built + reference implementation | **Design intent — prototype-pending** |

What this entry inherits from the prior seams: the write-before-fire
discipline of #2 (radicalized into the record-before-crossing
discipline), the relay-exits posture of #5, and the evidentiary
discipline of #7. What is new is the exposure topology: prior seams
could assert a bound — a named counterparty, an enumerable peer set.
This seam crosses into a regime where no bound is assertable. The
architecture's honest response is to govern everything it can reach
and to declare, in-record, the exact point past which it reaches
nothing. The vocabulary work encodes this precisely:
`exposure-upper-bound` → `exposure-unbounded` is not a degree
difference but a topological one. (CP-F16.)

---

### Landscape Position

The category claim this entry makes — and the four criteria that define it —
requires explicit differentiation from three adjacent systems. The collision
check conducted 2026-08-18 (six sweeps; ADJACENT verdict; not an occupied
category) identified these as the three flanks requiring rhetoric narrowing
before any publication-track use of the claim.

**The claim, narrowed:**

There is an unoccupied category: substrate-neutral governed-crossing
middleware. The four defining criteria are:

**(i) Substrate-neutral via published conformance contract.** The framework
rides on pluggable local-first/decentralized substrates via a published
conformance contract — permitting substitution of any conformant substrate
(Automerge, SQLite+CRDTs, AT Protocol repos, or equivalent) without modifying
the crossing-governance layer itself — rather than targeting a specific
substrate or managed cloud service.

**(ii) Crossing as governed object with middleware-enforced write-before-fire
ordering.** The framework treats the authorized boundary crossing as a
first-class governed object. The durable crossing record is produced by the
middleware as a precondition of the crossing — not as a logging side-effect
placed on the application deployer to provide separately — and is distinct
from systems that govern *unauthorized* crossings by preventing sync to
unauthorized replicas, or systems that require the deployer to externally
build and maintain the event log the policy engine then consumes.

**(iii) No external finality arbiter in the crossing path.** The framework
requires no external finality arbiter — specifically, no managed cloud
service, no blockchain consensus, and no central authority that must be
reachable for the crossing record to be produced or validated — distinguishing
it from gateway-enforced systems where the policy evaluation service is itself
a centralized dependency.

**(iv) Tamper-evident post-hoc evidence envelope.** The framework ships a
tamper-evident evidence envelope — a cryptographically bound, self-contained
artifact per crossing event — legible to parties who arrive after the fact
without requiring access to the middleware's internal log store or a live
connection to any arbiter, and distinct from the authorization tokens (UCANs,
Biscuits) that authorize the crossing but do not record that it occurred.

---

**Primary adjacency — AWS Dogwood (released August 6, 2026):**

Dogwood is the most dangerous adjacency and requires front-loaded explicit
differentiation. It introduces temporal conditions on sequences of prior
tool-call events, requires a durable event log, and runs at a gateway that
intercepts before effects fire. The surface-level description — "governed
sequences of crossing events with a durable record required" — applies to
both Dogwood and this entry. The differences are architectural and specific:

- **(i) Substrate-locked.** Dogwood/Cedar is tied to Amazon Bedrock
  AgentCore Gateway. The "substrate" is AWS infrastructure and MCP. There is
  no published conformance contract for substituting Automerge, AT Protocol,
  SQLite, or other local-first substrates.

- **(ii) Log-consuming, not log-producing.** Dogwood is a policy language
  that *consumes* a durable event log the deployer must supply. It explicitly
  warns that "timestamps have to be trusted and events authenticated" and
  "traces need durable storage" — requirements *placed on the deployer*, not
  properties the framework guarantees. This entry's middleware *produces* the
  crossing record as a precondition of the crossing; the write-before-fire
  ordering is enforced by the middleware, not delegated to the deployer's
  infrastructure.

- **(iii) Managed arbiter required.** AgentCore Gateway is the centralized
  arbiter. The reference interpreter is not production-ready; the only
  production path runs through AWS infrastructure.

- **(iv) No evidence envelope.** Dogwood specifies policy evaluation logic.
  It makes no claim about cryptographic binding of crossing records or
  post-hoc legibility for parties who arrive after the fact.

The rhetoric narrowing on (ii) and (iii) must be explicit and prominent in
any publication-track artifact that makes this claim. The substrate-lock on
(i) is the current most visible differentiator but has the shortest shelf
life: Dogwood's published roadmap includes planned work on additional temporal
operators, and a third-party implementation against a different substrate is
possible. The (ii) and (iii) distinctions are architectural and survive a
future Dogwood substrate extension.

**Empirical note (as of 2026-08-18):** KL-1 and KL-2 have converted from
prototype-pending to closing evidence (PC#8 Phase 2 joint conversion event,
SL-0121). The claim is no longer spec-vs-spec against Dogwood; it is
prototype-evidence vs. spec. Dogwood has no published prototype evidence of
middleware-enforced write-before-fire ordering. This asymmetry is real and
should be maintained in any comparative framing.

---

**Secondary adjacency — Keyhive/Beelay (Ink & Switch):**

Keyhive is the local-first community's most serious access-control work and
shares criterion (iii) (coordination-free, arbiter-free). The distinction is
architectural and precise: Keyhive governs *who may cross* by preventing
unauthorized synchronization; this entry governs *authorized crossings* as
first-class objects with pre-committed evidence. In Keyhive, an unauthorized
crossing is prevented; an authorized crossing fires without a pre-committed
record of the crossing event, a declared exposure position, or an evidence
envelope for parties who arrive after the fact. The distinction in one
sentence: **Keyhive gate-on-sync; this entry govern-the-crossing.**

Jake Lazaroff's LFC Berlin 2026 talk ("Building More Resilient Local-First
Software with atproto," Day 1) names the gap this entry addresses. His
implementation crosses from Automerge-style CRDTs into AT Protocol using the
Jetstream for real-time sync. He explicitly defers the data-exposure problem:
all data is public, private data "floating out there in the PDS" is
acknowledged as uneasy, and the proper solution is to "wait for atproto to
support private and shared private data." The crossing fires without a
pre-committed record, a declared exposure position, or a governed
acknowledgment of the regime change. This is the gap; his own characterization
of it is citable.

---

**Tertiary adjacency — Denis et al. 2024 (DIFC for distributed systems):**

Denis, Arnaud, and colleagues (Computers & Security 144, 2024,
DOI 10.1016/j.cose.2024.103975) propose a decentralized information-flow
control mechanism for distributed systems using events as the unit of IFC,
without a central authority. This is the closest academic precedent in the
IFC line. A skeptical reviewer with an IFC background will cite it; the
distinguishability argument must appear explicitly.

The distinction: Denis et al. present a theoretical model for label-propagation
IFC at the event level in a decentralized system. This entry addresses
*explicitly authorized* boundary crossings — intentional, governed acts where
one party moves a record across a declared substrate boundary with the
acknowledgment of the epistemic-regime change — with a durable pre-committed
evidence envelope legible to parties who arrive after the fact. Denis et al.
govern *implicit* information-flow confidentiality and integrity within a
unified computation model; this entry governs *explicit* authorized crossings
with an audit trail for third parties. Denis et al. is a deployed-nowhere
theoretical model; this entry has prototype evidence on a live stack (PC#8
Phase 2 joint conversion, SL-0121).

---

**The IFC tradition as a class:**

The broader IFC tradition (Jif/Myers, LIO/Russo, FlowCaml, Troupe, Cocoon,
Carapace) is distinguishable as a class: it enforces label-propagation
noninterference at compile time or within a single runtime, rather than
governing explicitly authorized boundary crossings with durable
pre-committed evidence artifacts. The compile-time/label-propagation vs.
runtime/crossing-record distinction is the load-bearing differentiator. Jif
prevents *accidental* flow violations at compile time; this entry governs
*intentional* authorized crossings at runtime with auditability for parties
who arrive after the fact.

---

**TCP/TLS analogy (hygiene note):**

The framing "Keyhive is to this framework what TCP is to TLS" — used in the
crossing-layer framework design sketch (2026-08-18, speculative register) —
does not appear to be claimed in the target domain as of August 2026. The
collision check's Sweep 6 found no competing use of the TCP/TLS layering
analogy for a middleware category claim in the authorization/local-first/
decentralized space. Risk is assessed as LOW but not ZERO: Local-First Conf
Berlin 2026 content has now been swept in full (this session, 2026-08-18),
and no competing claim was found across the complete schedule (Day 1, Day 2,
Lab Day). The analogy may be used in speculative-register drafting; it
requires a final collision check before any publication-track use.

---

**LFC Berlin 2026 sweep status (residual risk: CLOSED):**

The collision check's single largest unresolved residual risk — Local-First
Conf 2026 talk content not yet indexed — has been closed by direct schedule
fetch and targeted talk reads (this session, 2026-08-18). Full three-day
schedule retrieved (Day 1: July 12; Day 2: July 13; Lab Day: July 14). No
talk across any day claims substrate-neutral governed-crossing middleware,
write-before-fire ordering, or tamper-evident crossing evidence envelopes.
Jake Lazaroff's Day 1 talk (full text read) names the gap and defers it.
Paul Frazee's Day 2 talk ("Solving for Scale in Open Networks") addresses
atproto's authenticated-transfer scaling architecture — upstream
infrastructure, not crossing governance. The data-ownership panel (Day 1)
produced no competing middleware claim. Residual risk assessed CLOSED.

---

## Known Limits — KL-1 through KL-12

This is the entry's core section. Each limit names what cannot be
resolved speculatively and the class of evidence that would close it.
None is papered over; several are load-bearing for whether the design
survives contact.

| # | Cannot be resolved speculatively | Closing evidence |
|---|---|---|
| **KL-1** | Publish-completion failure modes: the real behavior of the PDS-accept vs. relay-ingest gap, and whether intent-without-completion is in practice legible to deferred parties as designed | Prototype: instrumented crossing against a live PDS, with relay observation |
| **KL-2** | Whether a custom-lexicon `seamCrossingRef` back-pointer survives real AppView/consumer handling; CID-anchor stability under PDS migration | Prototype + ecosystem observation |
| **KL-3** | Attribution strength of `mixed-custody` under an adversarial PDS — the 72-hour nullification mechanics, and whether that window justifies any upgrade over `provider-custodied` | Technical verification against the did:plc specification + adversarial test |
| **KL-4** | The empirical meaning of `propagated-request` recall: delete-event propagation latency and third-party compliance in practice | Observation study; cannot be designed into existence |
| **KL-5** | Generality of `exposure-unbounded` to a third target regime (ActivityPub, plain public web, iroh-gossip with bounded topic membership) | A third worked crossing; NI-5 discipline holds until then |
| **KL-6** | iroh-gossip crossing classification: is topic membership a valid exposure upper bound, making that crossing `exposure-upper-bound` rather than `exposure-unbounded`? | Deferred; iroh served as an axis-confirming reference only |
| **KL-7** | The form, authorship-verifiability, and juridical effect of `regimeAcknowledgment`: free text vs. structured assertion vs. standard-text reference is the form question; whether the gate-unverified declaration constitutes verified consent (authorship question) and whether it carries waiver or consent effect in any legal forum (effect question) are independent and deeper | Prototype with human participants; legal-legibility review; effect: legal substrate assessment |
| **KL-8** | Retry and multi-intent-record semantics: after `crossing-intent-failed`, does retry require a new gate pass and a new intent record, or can the original intent record anchor a retry? *Interim discipline: new gate pass required — conservative, fail-closed, consistent with the gate's act-time-current posture; displacing evidence required to relax.* Multi-intent-with-no-completion posture and `completion-mint-failed` recovery path also open. | State space designable now (spec amendment session); empirical population by KL-1 prototype |
| **KL-9** | Enforceability of the record-before-crossing ordering under Q6: the discipline is `author-declared` until `timestamp-signed` infrastructure unlocks; nothing structurally prevents backdating an intent record | Signed-timestamp infrastructure (already named as locked in the crossing-record vocabulary); `timestamp-signed` anchor type is the converting event |
| **KL-10** | The check-to-fire window (TOCTOU): a revocation landing between gate check and publish fires is checked-then-crossed at an irreversible boundary; the window cannot be eliminated under the finality-arbiter-free constraint | Prototype instrumentation of the window duration; cannot be closed, only bounded in-evidence; `emittedAt` on the intent record bounds it for deferred parties |
| **KL-11** | Gate reach over derived content: content derived from governed records (paraphrase, screenshot, re-publication outside the governed stack) crosses no boundary the gate can detect; the trigger is narrowed to architecture-mediated records and exports, but the residual surface is a permanent limit | None fully — P8 honesty requires naming this as permanently out-of-reach; the narrow trigger is the correct posture |
| **KL-12** | `recallSemantics` staleness: target-substrate deletion semantics can change between grant time and act time (protocol revisions, PDS policy); a standing grant could declare `propagated-request` and have that become inaccurate before the publish fires | Design candidate: gate re-asserts declared value at act time; a grant-side validity-horizon field **`grantAuthorityHorizon`** (PROPOSED; renamed at Lexicon v2.5 L2 — formerly the `crossingGrantHorizon` candidate) declares the horizon after which the grant's authority to initiate a crossing *lapses* (a not-after on authority scope; not `evidenceDecay`, a `seam:CrossingRecord` base-shape field not applicable to the grant object — V2-F5). **Host object (corrected v2.5, F-3.2-3):** the grant, where the grant object carries fields; on the current stack Keyhive `Access` is field-less, so the intent record is the only available host — a stack question, not settled by the lexicon. **Not to be confused with the registered `crossingGrantHorizon`** (not-before horizon on the intent record, D-2 — see Phase 3 As-Implemented Terms). **Status at v0.2:** NOT closed — Runs 7–8 exercised a seam-hosted not-before gate and a no-horizon control; grant-authority lapse was not exercised (Lexicon v2.5 L1). Closing evidence: a governed run in which grant authority lapses and the gate refuses on that ground |

---

## What This Entry Does Not Solve

- It does not govern the target regime. Nothing in this design
  constrains, verifies, or makes claims about post-crossing behavior
  beyond what the target substrate's own specifications state.
- It does not make the crossing safe. It makes the crossing **honest**:
  granted with acknowledgment, gated before the act, recorded before
  the act, and declared unbounded past the boundary.
- It does not resolve the PLC centralization asymmetry, the
  adversarial-PDS attribution question, or the acknowledgment form —
  those are KL items with named closing evidence.
- It does not advance the NI-5 closure motion. A second domain
  becomes evidence when a prototype exists, not when a spec is
  written. That attachment is earned by the prototype, not declared
  by this entry.

---

## Phase 3 As-Implemented Terms — PROPOSED (one registered field)

*Added v0.2 (2026-08-30). Source: UFO Lexicon v2.5 (rulings L2–L4, SL-0190); decision records D-2, D-3, D-5, D-7; CONVENTIONS v0.4 at `fb05ea1`; reconciliation record 2026-08-30 (routed lines 6, 18b; SL-0191). The **Vocabulary Queue below predates the Lexicon v2.3 promotion of this entry's original cluster and is known-stale; see F-B2 / v0.3.** Nothing in this section amends the Grant Model, Gate, Two-Record Pattern, or Landscape Position prose above, which remains as issued at v0.1.4; promotion of any term here into that prose is v0.3 work.*

These terms name what the Phase 3 build (Items 3.1–3.3, Runs 6–8) implemented. They are recorded here because this entry is the register home the Lexicon names for them; their promotion in the Lexicon (v2.6) is gated on this absorption being read against v2.5, not on this session alone.

**`crossingGrantHorizon`** *(REGISTERED — Lexicon v2.5 L2; the only registered term in this section)* — an optional *not-before* horizon hosted on the `crossing-intent` record beside `crossingTimeoutHorizon`; the gate checks it from the system clock at mint, fresh on every attempt, never cached; a pre-horizon attempt mints no record (D-2). Seam-level, not grant-level. Sense of "grant" in the name (L3): the earliest-effective time of the authorization, not the host object — the two intent-record horizons differ in meaning (earliest-authorized vs latest-before-unconfirmed), not in host. Consistency rule (D-7): `crossingGrantHorizon ≥ crossingTimeoutHorizon` never mints and is refused explicitly (`horizon-inconsistent`, both values logged), never clamped or reordered. Registered on build-validation grounds (Runs 7–8). **It is not KL-12 closing evidence** and not the `grantAuthorityHorizon` lapse candidate (KL-12 row). AppView note (L5): horizon compliance is legible only from the intent record; an AppView may display a record pre-embargo.

**assembly document** *(PROPOSED — D-5)* — the single seam-owned Automerge document a crossing actor assembles from granted input documents, in a fixed aggregation order; the object every crossing goes through, single-source included (one code path in `initiateCrossing()`). Hosts the `crossingRecords` and `completionRecords` arrays; `sourceDocumentURI` / `sourceDocumentCID` name it (CID = its heads at mint); `sourceLineage` lists the granted inputs; `authorizedContentDigest` (D-3) is computed over its content object. Runs 1–5 evidence was minted under the singular shape and is never retrofitted.

**payload-provenance rule** *(PROPOSED — F-3.3-1)* — the published record's content object is built from the assembled content the seam hash-checked at mint, never from an independent fixture or a separately constructed object. From `fb05ea1` this is enforced by the fire wrapper (fire-time re-verification, Item 3.3) and asserted by the e2e test on the bytes actually published. Origin: an Item 1.2-era fixture published a payload divergent from its authorized content, masked until fire-time verification existed (fixture-only; no live record affected). Candidate general seam principle: *a seam publishes only what its own intent record describes.* General-principle home if promoted: Pattern Commons #00 amendment.

**block-vs-fault principle** *(PROPOSED — Item 3.3 ruling Q2)* — a *block* is a gate outcome on an external condition detected (the document changed under the seam; an expired or not-yet-reached horizon; a digest mismatch at mint): a loggable event, nothing written or nothing fired, the evidence posture preserved (`crossing-unconfirmed` derivable). A *seam fault* is the seam breaking its own invariant on bytes it just wrote (the step-4 recompute inequality): thrown, not logged as a gate outcome. Fire-time re-verification Surface A is a block (`fire-verification-blocked`); Surface B is a fault. Candidate general seam principle; general-principle home if promoted: Pattern Commons #00 amendment.

**Candidate text — routed from the Phase 3 spec r2 reconciliation** *(PROPOSED; absorbed here as candidate text only — promotion into design prose deferred to v0.3)*. Both are D-1 r2 consequences carrying Run 6 evidence:

- *Subset confinement* (reconciliation line 6): subset confinement on this stack is a capability-layer property achieved by document decomposition; the seam's digest binds the assembled output. (Consequence: no acceptance criterion at the seam claims to confine a subset; the Grant Model's "two slots" prose is untouched pending v0.3.)
- *Never partly authorized* (reconciliation line 18b): a document is never partly authorized; sections with different authorizations are separate documents. (General principle stated in D-1 r2; the assembly document is its structural expression.)

---

## Vocabulary Queue — PROPOSED

All of the following are PROPOSED pending a UFO Lexicon v1.8 amendment
session. None governs output until promoted. Nearest home: v1.8
amendment, bundled with this spec's issuance.

**New controlled-vocabulary values:**
- `governanceEvent`: `substrate-crossing`
- `boundType`: `exposure-unbounded` (ordering: below
  `exposure-upper-bound`)

**New conditional fields on the grant** (required when `crossingType:
substrate-crossing`): `crossingType` (discriminant);
`regimeAcknowledgment`; `declaredBoundType`; `recallSemantics`

**New conditional fields on the completion record:**
`crossingTargetURI`; `crossingTargetCID`

**New conditional field group on the intent record:** identity binding
block (`grantorDID`; `targetDID`; `identityCustodyClass`)

**New controlled vocabulary:** `identityCustodyClass`
(`self-custodied` / `mixed-custody` / `provider-custodied`)

**New controlled vocabulary:** `recallSemantics`
(`enforced-stream-close` / `propagated-request` / `none`)

**New `recordType` values** (CP-F2): `crossing-intent` (pre-crossing
intent record) and `crossing-completion` (post-hoc completion record).
Both pair with `governanceEvent: substrate-crossing`.

**New field on intent record** (CP-F11): `authorizedContentDigest` —
a CID or hash of the content being authorized to cross, computable
locally before the publish fires.

**New field — intent record or grant** (V2-F4 / V3-F2):
`crossingTimeoutHorizon` — an ISO 8601 date/datetime after which an
unconfirmed crossing transitions from `crossing-intent-pending` to
`crossing-unconfirmed`. Host object (intent-record vs. grant) and
value source (protocol-defined vs. user-declared) are part of
KL-8's designable-now scope.

**Ordering note amendment** (CP-F1/CP-F3): the `boundType` ordering
rule should be rewritten at promotion time from the absolute
"substituting weaker for stronger is never permitted" formulation to
the symmetric principle: the asserted value must match the
architecture's actual enforcement capacity; both overclaiming and
underclaiming are substitution errors; overclaiming inadmissible per
P9. The scale orders *admissible claim strength* (not a single
epistemic quantity).

**Lexicon v1.8 divergence note (V2-F6 — pending v1.9 or
promotion-time amendment).** The v1.8 PROPOSED-queue cluster was
registered from v0.1; v0.1.2 diverges in five places: (a)
`exposure-unbounded` entry carries the pre-CP-F1 asymmetric ordering
rule and "epistemic-strength ordering" label — v0.1.2 uses the
symmetric rule and "admissible claim strength"; (b)
`identityCustodyClass` cap text covers provider-custodied only —
v0.1.2 extends the cap to `mixed-custody` (CP-F13); (c)
`regimeAcknowledgment` queue text says "person-authored
acknowledgment" — v0.1.2 denies authorship verifiability ("presence,
not authorship"; "declared-acknowledgment ceiling"); this is the
substantive divergence: the queue entry overclaims relative to its
source spec, a P9-reflexive inaccuracy requiring correction before
promotion; (d) cluster cites the v0.1 filename — should reference
v0.1.2; (e) cluster omits `authorizedContentDigest` (CP-F11), the two
`recordType` values (CP-F2), and `crossingTimeoutHorizon` (V2-F4 /
V3-F2) — three omissions. None of (a)–(e) affects CV-table
registration (out of scope); all five require a v1.9 amendment
session before promotion.

---

## What Comes Next

1. **UFO Lexicon v1.9 amendment session** — correct the five
   divergences from the V2-F6 note (V2-F6c `regimeAcknowledgment`
   "person-authored" overclaim is the substantive item; (e) now
   covers three omissions including `crossingTimeoutHorizon`).
2. ~~**Prototype** — instrumented crossing against a live PDS; closing
   evidence for KL-1 and KL-2; gates CV-table promotion and any
   NI-5 motion.~~
3. ~~**Prototype.** An instrumented crossing against a live PDS —
   the closing evidence for KL-1 and KL-2, and the event that would
   make this entry's design claims testable rather than declared.~~
4. **Only after prototype evidence:** any Artifact B amendment, any
   NI-5 motion, any generality language. The employment-seam
   sequencing precedent governs.

---

## Changelog

**v0.2.1 (2026-08-30).** Header only; no content change. Status line reduced to reader-facing text — the revision inventory it carried now lives solely in the v0.2 changelog entry below, where a v0.3 revision reads it. Stamp-block v0.2 sentence shortened. Hard line breaks (trailing spaces) added to the header metadata lines so Status, Date, Author, and the rest render as separate lines rather than one paragraph (whitespace-only; affects v0.1.4-era lines). Series-wide question of governance metadata in public headers deferred to v0.3 / PC#00.

**v0.2 (2026-08-30).** Narrow post-Phase-3 absorption under manifest r7 (Mode 1, single context, no Counter-Pass). **Rebased onto v0.1.4 (F-B3); Landscape Position section carried unchanged.** (1) New section *Phase 3 As-Implemented Terms* absorbing the UFO Lexicon v2.5 L4 PROPOSED cluster — assembly document (D-5), payload-provenance rule (F-3.3-1), block-vs-fault principle (Q2) — and recording **`crossingGrantHorizon` as REGISTERED (v2.5 L2), not PROPOSED**: it enters this entry with registered status, the only such term in the new section. (2) KL-12 row: candidate field renamed `grantAuthorityHorizon` (v2.5 L2; rename recorded as a divergence from build-plan §KL-8c naming), host-object line corrected (F-3.2-3), disambiguated from the registered not-before field, status marked NOT closed (L1). (3) Reconciliation lines 6 and 18b absorbed as candidate text, PROPOSED — promotion to design-prose register deferred to v0.3 (a narrowing; SL-0191 → SURVIVED, narrowed). (4) SL-0190 validation event (a) fires: L4 cluster absorbed; Lexicon v2.6 promotion remains gated on this entry being read against v2.5. Status line supersedes v0.1.4's "Phases 0–2 complete; 27/27" with the Phase 3 close at `fb05ea1`. **Scoping correction (F-B1):** the r6.1-era phrase "correct Item 3.2 bullet 2 per D-2" named a Phase 3 *spec* §3 item, discharged in spec r2 and not present in this entry; the D-2 consequence for this entry is the `crossingGrantHorizon` registration above. **Deliberately not revised (F-B2, inventory corrected against v0.1.4):** KL-1/KL-2/KL-8/KL-10 rows (Landscape Position cites SL-0121 as KL-1/KL-2 closing evidence; the rows do not), Vocabulary Queue ("pending v1.8"; `crossingTimeoutHorizon` host listed open — resolved KL-8c/SL-0114), What Comes Next items 1 and 4, header references to Artifact B r2.4 and NI-5 "in effect", How It Sits in the Series table PC#8 evidence-status cell ("Design intent — prototype-pending"); repo-side: root README.md "Design intent, prototype-pending" line — all known-stale, queued for v0.3 with ledger + observation log attached. No design verdict modified.

**v0.1.4 (2026-08-18).** Landscape Position section added (new §, inserted
after "How It Sits in the Series"). Source: collision check
`collision_check_substrate_neutral_governed_crossing.md` (2026-08-18, six
sweeps, ADJACENT verdict) and LFC Berlin 2026 full schedule sweep (this
date). Content: four criteria narrowed with explicit Dogwood, Keyhive, and
Denis et al. differentiation language; Lazaroff gap-naming cited; LFC
residual risk closed. No vocabulary modified. No Known Limits opened or
closed. No existing text modified. Ledger: SL-0122.

**v0.1.3 (2026-08-17).** Counter-Pass program closed at iteration-3
ceiling. Mechanical residuals applied: V3-F1 (epistemic-position
bullet updated to program-complete); V3-F2 (`crossingTimeoutHorizon`
landed in vocabulary queue and failure table — was not present in
v0.1.2 despite changelog claim; divergence note (e) extended to
three omissions); V3-F3 (stamp block updated to program-complete);
V3-F4 (What Comes Next updated). V3-F5 (divergence-note accuracy)
resolved by critic — no amendment required. No design verdict modified.

**v0.1.2 (2026-08-17).** Counter-Pass iteration 2 amendments applied.
V2-F1 (KL header corrected to KL-1–KL-12). V2-F2 (epistemic-position
bullet updated: iters 1 and 2 complete, convergence at iter 3).
V2-F3 (failure-table retry cell softened; KL-8 records interim
discipline). V2-F4 (`crossingTimeoutHorizon` added to vocabulary
queue; named in failure table). V2-F5 (KL-12 candidate corrected:
grant-side validity-horizon field, not `evidenceDecay`). V2-F6
(Lexicon v1.8 divergence note added — five divergences, V2-F6c
`regimeAcknowledgment` overclaim is substantive). V2-F7 (typo
corrected; ledger line extended). V2-F8 (`recordType` bindings added
to both record definitions).

**v0.1.1 (2026-08-17).** Counter-Pass iteration 1 amendments applied.
16/16 findings accepted (zero rebuttals). Promotion-blocking items
resolved: ordering rule rewritten symmetric (CP-F1/F3); custody-cap
default narrowed — both `provider-custodied` and `mixed-custody` capped
at `asserted` pending KL-3 (CP-F13). `authorizedContentDigest` field
added to intent record (CP-F11 — most consequential gap). Failure-state
taxonomy sketched (CP-F7, six states). Record-before-crossing discipline
re-anchored as `author-declared` (CP-F8). Seam trigger narrowed to
architecture-mediated records and exports; derived content named as
out-of-reach limit (CP-F10). Series framing revised from
irreversibility to bound-assertability (CP-F16). KL-7 widened (form +
authorship + juridical effect; CP-F4/F5). KL-8–KL-12 added (CP-F6/7/9/
10/11). Two new `recordType` values added to vocabulary queue (CP-F2).
TOCTOU named in gate section (CP-F9). CID decay and `evidenceDecay`
noted on completion records (CP-F12). Deferred-verifiability of custody
declaration noted (CP-F14). `provenanceStatus` cap granularity resolved
to intent-record level (CP-F15).

**v0.1 (2026-08-17).** Initial draft from the speculative design
sketch of 2026-08-17. OQ-5 (home) settled by operator decision:
Pattern Commons entry, not Form C insertion. OQ-1–OQ-4 and OQ-6
candidate resolutions adopted as design basis (all ~,
single-context). KL-1–KL-7 inventory carried as the Known Limits
section. All vocabulary PROPOSED.


---

*This document is part of the Pattern Commons, the architectural-pattern
documentation series produced alongside the local-first prototype work.
It is published under the same methodology disclosure as the rest of
Systems of Thought: AI-collaborative drafting, human authorial
responsibility, intellectual direction held by the named author.*

*⚑ SINGLE-CONTEXT — NOT PANELED. Form C cluster PROPOSED per UFO
Lexicon v1.8. All new vocabulary PROPOSED pending promotion. NI-5: local-first
specific on current evidence — zero generality claims in this entry.*
*v0.2: Phase 3 as-implemented terms PROPOSED per UFO Lexicon v2.5 L4;
`crossingGrantHorizon` REGISTERED (v2.5 L2). Rebased onto v0.1.4 (F-B3).
Prototype-status prose known-stale, queued for v0.3 (F-B2, manifest r7).
Ledger: SL-0122 carried; SL-0190 / SL-0191 validation events.*
*Delivery-not-application enforced. Canonical files on operator's machine.*

*UX Minds, LLC · J. Wright · August 18, 2026 · v0.2 / v0.2.1 August 30, 2026*
