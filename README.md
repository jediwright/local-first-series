# Local-First Prototype Series

A series of working prototypes demonstrating local-first architecture applied to several domains: governance monitoring, commerce, healthcare, and social networking. Plus a seventh entry — a published architectural specification, not yet built — that extends the same argument into the employment relationship.

The central argument: local-first works when something irreducibly server-dependent has to happen. The question is not whether to touch a server — sometimes you must. The question is how to design that boundary deliberately, minimize it, and ensure the client loses nothing when it fails.

The name for that boundary is **the seam**.

## The Seam Stack

The series demonstrates a four-layer architecture for local-first systems where boundary events carry weight. I call it the **Seam Stack**, and it will be more heavily documented soon at seamstack.org.

| Layer | Question it answers | Technology in this series |
|---|---|---|
| **Substrate** | Where does the data live, who owns it, who can access it? | Y.js + IndexedDB (per-user, local); Solid Pods (employment seam, spec-only) |
| **Governance** | How is meaning structured, classified, and made machine-legible? | [The Tiered Content Framework (TCF)](https://www.jediwright.com/content-strategy-framework) — six tiers with three cross-cutting governance dimensions |
| **Boundary** | What happens at the transition where the relationship between client and server changes state? | The Pattern Commons seam discipline — the seam-as-architectural-object |
| **Evidence** | What makes the record contemporaneous, tamper-evident, and legible to deferred parties without platform mediation? | W3C Verifiable Credentials Data Model 2.0 + RFC 3161 trusted timestamping + OpenTimestamps + bilateral cryptographic signatures (employment seam, spec-only) |

The synthesis claim is that all four layers are required when boundary events carry legal and evidentiary weight, and that they compose into a coherent architecture for local-first systems in those domains. The series demonstrates the layers across domains, with the employment seam as the entry where all four become necessary at once. None of the four layers is novel in isolation; the synthesis is the architectural composition.

The Seam Stack is documented at [seamstack.org](https://seamstack.org). This repo is its working home.

## The Prototypes

| # | Prototype | Seam | Live | Repo |
|---|---|---|---|---|
| 1 | Governance Window Tracker | None — browser is the application | [infinitydrive.net](https://infinitydrive.net) | [governance-tracker](https://github.com/jediwright/governance-tracker) |
| 2 | checkout-seam | One seam per transaction (Stripe) | [checkout-seam.vercel.app](https://checkout-seam.vercel.app) | [checkout-seam](https://github.com/jediwright/checkout-seam) |
| 3 | fhir-seam | One seam per intake submission (FHIR R4) | [fhir-seam.vercel.app](https://fhir-seam.vercel.app) | [fhir-seam](https://github.com/jediwright/fhir-seam) |
| 4 | Local-First Social | One seam per new connection (WebSocket relay) | [localfirst.social](https://localfirst.social) | [local-first-social-network](https://github.com/jediwright/local-first-social-network) |
| 5 | employment-seam | One seam per transition (entry, exit, stage change, re-engagement) | Spec-only — not built | [employment-seam](https://github.com/jediwright/employment-seam) |

Each prototype introduces a harder version of the seam problem. The Tracker has no seam at all. checkout-seam has one seam per transaction. fhir-seam has one seam per intake submission, with a richer failure taxonomy and higher stakes. Local-First Social has a seam that fires on every new connection — the social graph itself is a distributed seam. The employment seam fires on every transition in the employer–worker relationship, with nine failure states, multi-perspective preservation in contested cases, and a legal record format designed for evidentiary use across jurisdictions.

The fifth entry is the first in the series specified without a reference implementation. Whether it becomes a built prototype, a published specification adopted by another builder, or remains a documented pattern that informs future work is an open question — and an open invitation. The spec is at [employment-seam](https://github.com/jediwright/employment-seam).

## Shared Specifications

These files govern the prototypes. They are series artifacts, not prototype-specific artifacts. Every build session reads them before writing code.

### `DESIGN.md`

Design tokens and rationale for the series. YAML front matter contains normative values for colors, typography, spacing, and component tokens. The seam state palette (`seam-none`, `seam-connecting`, `seam-established`, `seam-error`) is the load-bearing design decision — it makes the architectural argument visible in the UI. Validated with `@google/design.md`.

```bash
npx @google/design.md lint DESIGN.md
```

### `STATE_CONVENTIONS.md`

Authoritative conventions for Y.js state across all prototypes: map names and value types, key formats (including `@handle` prefix conventions), which mutations require `doc.transact()`, which hooks require `attachArrayObserver()`, and which keys are relay-routing keys vs. local-graph keys. Every session agent reads this before writing any code that touches Y.js state.

### `/vocab/` and `/schemas/`

Vocabulary and schema artifacts the Seam Stack depends on. The vocabulary at `seamstack.org/vocab/employment-seam/0.4.1#` and `seamstack.org/vocab/assurance/` resolves to files served from this directory via GitHub Pages. The SHACL shapes, JSON-LD context, and JSON Schema fallback validator for the employment seam bundle live alongside the vocabulary.

These artifacts are referenced by the employment seam spec and are intended to be reusable beyond it.

## Pattern Commons

Seven patterns documented across the series. Each is designed as a reusable template — domain-agnostic, extractable, applicable beyond the prototype that first demonstrated it.

**1. The checkout seam.** Minimum server-dependent surface for a payment operation. Client preserves state on failure; writes the result record on success. Server is stateless and never consulted again after confirmation. Applies to: payment processing, identity verification, legal record creation, compliance logging.

**2. The high-stakes seam.** Write-before-POST discipline for operations where data loss is clinically or legally consequential. Richer failure taxonomy (accepted / validation error / transient error / permanent failure). Format translation at the seam boundary, not inside either system. Applies to: healthcare intake, government benefit submissions, regulatory filings.

**3. The profile map as local CRM.** Y.js document as the user's full relationship with a service — address, order history, intake history, trust graph — all local, sync-capable as an opt-in enhancement. No server-side session required.

**4. The `attachArrayObserver()` pattern.** How to correctly observe a Y.Array nested inside a Y.Map when the document hydrates from IndexedDB. Prevents the stale-reference bug. Must be applied from the start — not discovered during debugging. Applies to any hook in this stack.

**5. The distributed seam.** Where the server-dependent operation is a peer handshake rather than a server transaction. The relay facilitates connection and exits. The social graph is built from the accumulation of distributed seams, each of which fires once. Applies to any peer-to-peer application where a minimal relay facilitates connection without accumulating relationship data.

**6. CRDT as trust graph.** Trust tier assignments, connection history, and sync status stored as local-first Y.Map state, synchronized via the distributed seam. No server owns the relationships.

**7. The employment seam.** *Spec-only, published as Pattern Commons #7.* The boundary event when a person enters or exits an employer–worker relationship. Worker owns the knowledge graph; the platform facilitates the handoff and exits. Bundle schema (SHACL over RDF, JSON-LD canonical), legal record format (W3C Verifiable Credentials 2.0 + RFC 3161 + OpenTimestamps), nine-state failure taxonomy, multi-perspective record in contested cases, seven-class participant model. Generalizes WARN Act, EU European Works Council Directive, EU Collective Redundancies Directive, and contractor classification regimes. The first Pattern Commons entry where all four Seam Stack layers become necessary at once. Spec at [employment-seam](https://github.com/jediwright/employment-seam).

## Governance Framework

The failures that produced this framework are documented honestly in the [companion article](https://www.systemsofthought.com/). The framework governs every build session in the series.

**Core principle:** Write the specification before writing the code. At every level — the data convention document before the first hook, the acceptance criteria before the first build session, the failure taxonomy before the seam implementation.

**The rules:**

- State conventions document exists and is read before any Y.js code is written
- `attachArrayObserver()` applied to all nested Y.Arrays from session start
- Acceptance criteria written as testable conditions before code generation begins
- Hypothesis written before fix is generated when a bug appears
- Pre-deploy checklist: dependencies in `dependencies` not `devDependencies`, environment variables verified, serverless endpoints tested via `curl`
- External user testing required before any phase involving network behavior is closed — two local browsers is not the same test

## Read More

The full account: what was built, what broke, what the AI wrote that shouldn't have shipped, and what the governance framework is — published at [Systems of Thought](https://www.systemsofthought.com/).

The Seam Stack as an architectural composition is documented at [seamstack.org](https://seamstack.org). The seventh Pattern Commons entry — the employment seam — is the spec where the four-layer synthesis is demonstrated end-to-end. The companion entries (#1–#6) demonstrate components of the synthesis across the prior built prototypes.

---

MIT License · Built with AI-collaborative methods · Intellectual direction and authorial responsibility: Jedi Wright | [Systems of Thought](https://www.systemsofthought.com/) | UX Minds, LLC
