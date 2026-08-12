# Local-First Prototype Series

A series of working prototypes demonstrating local-first architecture applied across domains: governance monitoring, commerce, healthcare, and social networking. Plus a published architectural specification — with a built reference implementation — that extends the same argument into the employment relationship.

The central argument: local-first works when something irreducibly server-dependent has to happen. The question is not whether to touch a server — sometimes you must. The question is how to design that boundary deliberately, minimize it, and ensure the client loses nothing when it fails.

The name for that boundary is **the seam**.

---

## The Seam Stack

The series demonstrates a four-layer architecture for local-first systems where boundary events carry weight. I call it the **Seam Stack**, documented at [seamstack.org](https://seamstack.org) and in the [seam-stack](https://github.com/jediwright/seam-stack) repository.

| Layer | Question it answers | Technology in this series |
|---|---|---|
| **Substrate** | Where does the data live, who owns it, who can access it? | Y.js + IndexedDB (prototypes #1–#4); Automerge + Keyhive (employment seam — built reference implementation) |
| **Governance** | How is meaning structured, classified, and made machine-legible? | [The Tiered Content Framework (TCF)](https://www.jediwright.com/content-strategy-framework) — six tiers with three cross-cutting governance dimensions |
| **Boundary** | What happens at the transition where the relationship between client and server changes state? | The Pattern Commons seam discipline — the seam as architectural object |
| **Evidence** | What makes the record contemporaneous, tamper-evident, and legible to deferred parties without platform mediation? | W3C Verifiable Credentials Data Model 2.0 + RFC 3161 trusted timestamping + OpenTimestamps + bilateral cryptographic signatures (employment seam); `seam:CrossingRecord` base shape (all seam types) |

The synthesis claim: all four layers are required when boundary events carry legal and evidentiary weight, and they compose into a coherent architecture for local-first systems in those domains. None of the four layers is novel in isolation; the synthesis is the architectural composition.

---

## The Prototypes

| # | Prototype | Seam | Live | Repo |
|---|---|---|---|---|
| 1 | Governance Window Tracker | None — browser is the application | [infinitydrive.net](https://infinitydrive.net) | [governance-tracker](https://github.com/jediwright/governance-tracker) |
| 2 | checkout-seam | One seam per transaction (Stripe) | [checkout-seam.vercel.app](https://checkout-seam.vercel.app) | [checkout-seam](https://github.com/jediwright/checkout-seam) |
| 3 | fhir-seam | One seam per intake submission (FHIR R4) | [fhir-seam.vercel.app](https://fhir-seam.vercel.app) | [fhir-seam](https://github.com/jediwright/fhir-seam) |
| 4 | Local-First Social | One seam per new connection (WebSocket relay) | [localfirst.social](https://localfirst.social) | [local-first-social-network](https://github.com/jediwright/local-first-social-network) |
| 5 | employment-seam | One seam per transition (entry, exit, stage change, re-engagement) | Reference implementation — Automerge + Keyhive | [employment-seam](https://github.com/jediwright/employment-seam) |

Each prototype introduces a harder version of the seam problem. The Tracker has no seam at all. checkout-seam has one seam per transaction. fhir-seam has one seam per intake submission, with a richer failure taxonomy and higher stakes. Local-First Social has a seam that fires on every new connection — the social graph itself is a distributed seam. The employment seam fires on every transition in the employer–worker relationship, with nine failure states, multi-perspective preservation in contested cases, and a legal record format designed for evidentiary use across jurisdictions.

The fifth entry is the first in the series where the specification preceded the reference implementation. The spec and reference implementation (Automerge + Keyhive substrate, v0.5 build plan) are both at [employment-seam](https://github.com/jediwright/employment-seam).

---

## Pattern Commons

A root abstract pattern plus seven domain instantiations documented across the series. Each is designed as a reusable template — domain-agnostic, extractable, applicable beyond the prototype that first demonstrated it.

**#0 — The governed crossing.** The abstract pattern that all prior entries have been instantiating. A governed crossing is the boundary event at which a party with contextual knowledge crosses into or out of a structured relationship under a capability grant. Four constitutive properties — declared scope, grant, gate, record — are invariant across all domain instantiations. The architectural argument: every such crossing must be explicit, gated, and recorded before it fires, with the platform facilitating the event and exiting rather than accumulating the relationship. Spec at [pattern-commons-00](./pattern-commons/pattern-commons-00-the-governed-crossing-v0-1-1.md).

**#1 — The checkout seam.** Minimum server-dependent surface for a payment operation. Client preserves state on failure; writes the result record on success. Server is stateless and never consulted again after confirmation. Applies to: payment processing, identity verification, legal record creation, compliance logging.

**#2 — The high-stakes seam.** Write-before-POST discipline for operations where data loss is clinically or legally consequential. Richer failure taxonomy (accepted / validation error / transient error / permanent failure). Format translation at the seam boundary, not inside either system. Applies to: healthcare intake, government benefit submissions, regulatory filings.

**#3 — The profile map as local CRM.** Y.js document as the user's full relationship with a service — address, order history, intake history, trust graph — all local, sync-capable as an opt-in enhancement. No server-side session required.

**#4 — The `attachArrayObserver()` pattern.** How to correctly observe a Y.Array nested inside a Y.Map when the document hydrates from IndexedDB. Prevents the stale-reference bug. Must be applied from the start — not discovered during debugging. Applies to any hook in this stack.

**#5 — The distributed seam.** Where the server-dependent operation is a peer handshake rather than a server transaction. The relay facilitates connection and exits. The social graph is built from the accumulation of distributed seams, each of which fires once. Applies to any peer-to-peer application where a minimal relay facilitates connection without accumulating relationship data.

**#6 — CRDT as trust graph.** Trust tier assignments, connection history, and sync status stored as local-first Y.js state, synchronized via the distributed seam. No server owns the relationships.

**#7 — The employment seam.** The boundary event when a person enters or exits an employer–worker relationship. Worker owns the knowledge graph; the platform facilitates the handoff and exits. Bundle schema (SHACL over RDF, JSON-LD canonical), legal record format (W3C Verifiable Credentials 2.0 + RFC 3161 + OpenTimestamps), nine-state failure taxonomy, multi-perspective record in contested cases, seven-class participant model including AI agents (Class G). Generalizes WARN Act, EU European Works Council Directive, EU Collective Redundancies Directive, and contractor classification regimes. The first Pattern Commons entry where all four Seam Stack layers become necessary at once. Spec at [pattern-commons-07](./pattern-commons/pattern-commons-07-employment-seam-v0-5_2026-08-08.md). Reference implementation at [employment-seam](https://github.com/jediwright/employment-seam).

---

## Shared Specifications

These files govern the prototypes. They are series artifacts, not prototype-specific artifacts.

**`DESIGN.md`** — Design tokens and rationale for the series. The seam state palette (`seam-none`, `seam-connecting`, `seam-established`, `seam-error`) is the load-bearing design decision — it makes the architectural argument visible in the UI.

**`STATE_CONVENTIONS.md`** — Authoritative conventions for Y.js state across prototypes #1–#4 (Y.js + IndexedDB stack). Does not apply to employment-seam, which runs Automerge + Keyhive — see the employment-seam README for its state conventions. Every build session on #1–#4 reads this before writing any code that touches Y.js state.

**Vocabulary and schemas** — The base crossing-record vocabulary and employment-seam vocabulary are served from the [seam-stack](https://github.com/jediwright/seam-stack) repository via GitHub Pages:

| Namespace | IRI |
|---|---|
| Crossing record (base shape) | [https://jediwright.github.io/seam-stack/vocab/crossing-record/0.1/](https://jediwright.github.io/seam-stack/vocab/crossing-record/0.1/) |
| Employment seam | [https://jediwright.github.io/seam-stack/vocab/employment-seam/0.5/](https://jediwright.github.io/seam-stack/vocab/employment-seam/0.5/) |
| Canonical assurance scale | [https://jediwright.github.io/seam-stack/vocab/assurance/](https://jediwright.github.io/seam-stack/vocab/assurance/) |

---

## Governance

The failures that produced this governance framework are documented honestly in the [companion article](https://www.systemsofthought.com/) at Systems of Thought.

The core principle is that boundary events with legal and evidentiary weight can't be governed after the fact. The spec has to exist before the code. The failure taxonomy has to be named before the seam is implemented. The record has to be a first-class output of the crossing, not an audit log appended afterward. This is not a software-quality argument — it's an architectural one. A boundary you haven't declared is a boundary you can't govern.

That principle produces a small set of rules that govern every build session in this series:

- Specification exists and is read before any implementation begins
- State conventions document exists and is read before any Y.js code is written
- Acceptance criteria written as testable conditions before code generation begins
- Failure taxonomy named before the seam implementation
- Hypothesis written before a fix is generated when a bug appears
- External user testing required before any phase involving network behavior is closed

The governance framework itself is documented at [governed-pr-framework](https://github.com/jediwright/governed-pr-framework).

---

## Related Work

The theoretical frame for this series — why local-first systems need a theory of the boundary, and what worker-side governance infrastructure for AI agents at employment boundaries requires — is developed in [Full Personhood: The Governance Model AI Requires and Capitalism Never Built](https://www.systemsofthought.com/full-personhood-the-governance-model-ai-requires-and-capitalism-never-built/).

| Repo | What it is |
|---|---|
| [seam-stack](https://github.com/jediwright/seam-stack) | Architecture documentation, vocabulary namespaces, GitHub Pages IRI resolution |
| [employment-seam](https://github.com/jediwright/employment-seam) | Pattern Commons #7 spec + Automerge + Keyhive reference implementation |
| [governed-pr-framework](https://github.com/jediwright/governed-pr-framework) | Governed PR Framework (GPRF) — blast-radius classification and epistemic-status tagging for pull requests |

---

MIT License · Built with AI-collaborative methods · Intellectual direction and authorial responsibility: Jedi Wright · [Systems of Thought](https://www.systemsofthought.com/) · UX Minds, LLC
