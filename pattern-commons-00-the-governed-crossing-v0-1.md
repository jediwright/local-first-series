# Pattern Commons #0 — The Governed Crossing

**Status:** Draft v0.1
**Date:** August 10, 2026
**Author:** J. Wright (UX Minds, LLC) · AI-assisted
**Series:** Local-first prototype series — Pattern Commons
**Companion entries:** #1 checkout seam · #2 high-stakes seam · #3 profile map as local CRM · #4 attachArrayObserver · #5 distributed seam · #6 CRDT as trust graph · #7 employment seam
**Governing architecture:** Artifact B — Form C Standalone Framework Manifesto-Spec (r2)
**Stamps:** ⚑ SINGLE-CONTEXT — NOT PANELED. CONTEXTUAL register. Form C cluster PROPOSED per UFO Lexicon v1.5. NI-5 in effect throughout.

---

## The Pattern in One Sentence

A governed crossing is the boundary event at which a party with contextual knowledge crosses into or out of a structured relationship under a capability grant — and the architectural argument is that every such crossing must be explicit, gated, and recorded before it fires, with the platform facilitating the event and exiting rather than accumulating the relationship.

---

## What This Document Is

Pattern Commons #0 is the root entry in the Pattern Commons series. It does not describe a new domain. It names and formalizes the pattern that all prior entries have been instantiating.

The series has demonstrated the governed crossing across commerce (one seam per transaction), healthcare (one seam per intake), social networking (a seam per connection, distributed), and employment (a seam at every state change in a working relationship). Each domain generated its own spec. None of them named the abstract pattern they were demonstrating.

This document does that.

The employment seam (Pattern Commons #7) is the entry where the pattern became fully visible — where all four Seam Stack layers became necessary at once, where the legal and evidentiary stakes forced the architecture into explicit view, and where the generalization became unavoidable. Pattern Commons #0 is not a retroactive reframe of #7. It is the document #7 implied and that the architecture had been building toward.

---

## The Pattern

### What a governed crossing is

A governed crossing is a boundary event with four constitutive properties. A crossing that is missing any one of them is not a governed crossing — it is an ungoverned exposure with a name attached.

**1. A declared scope.**
The crossing is explicit and minimal. The surface at which interior state meets an external party is named; its scope is the minimum required for the purpose; its failure states are enumerated. There is no ambient exfiltration. What crosses is declared; what does not cross is also declared.

**2. A grant.**
Authority to cross is issued by an eligible grantor party to an eligible crossing party. The grant is the legal-responsibility anchor: the crossing is attributable to the grant, and the grant is attributable to the grantor. No crossing without a grant; no grant without an issuer who can be held accountable.

**3. A gate.**
Every crossing attempt is checked at act time against the current capability state of the relevant grant. The gate fails closed: an unconfirmed revocation blocks; silence blocks. The gate does not read from a cached token or a TTL. It checks the current state at the moment of invocation.

**4. A record.**
Every gate-check invocation — pass or block — emits an evidence artifact. The record is a first-class output of the crossing, not an audit log appended afterward. The record names the grant, the party, the capability checked, the timestamp, and the result. A crossing with no record is not a governed crossing; it is an undeclared event the architecture cannot account for.

A crossing is valid if and only if all four properties are satisfied at crossing time.

---

### The inversion

Conventional platform architectures sit in the middle of relationships and own them. The platform holds the social graph, the employment history, the transaction record, the patient file. Parties interact through the platform, and the platform accumulates what they produce.

The governed crossing inverts this. The platform facilitates the boundary event and exits. The record lives on the party's substrate, not the platform's database. The platform is a relay, not an owner. The relationship lives on the parties' sides and in the legal record. The platform's role ends when the crossing completes.

This inversion is the load-bearing architectural commitment. Everything downstream — the grant structure, the gate discipline, the evidence plane — is a consequence of taking the inversion seriously.

---

### What fires a governed crossing

A governed crossing fires whenever the legal, evidentiary, or relational status of a structured relationship changes state. Not only at termination. The crossing fires:

- When a party enters a relationship (hire, engagement start, onboarding, connection accepted, transaction initiated)
- When a party's status within a relationship changes (role change, classification change, capability grant amended, access tier shifted)
- When a party exits a relationship (separation, contract close, transaction complete, connection severed, engagement ended)
- When a relay party enters or exits a chain (a sub-contractor onboarding to a project, an agent receiving a delegated capability grant, a new party joining an existing governed relationship)

The triggering condition is state change, not termination. This is the distinction the prior entries in the series made implicitly. Pattern Commons #0 makes it explicit.

---

## The Seam Stack

The governed crossing is specified against a four-layer architecture — the Seam Stack — that supplies what the crossing requires and nothing more. Each layer answers a question the others do not.

| Layer | Question it answers |
|---|---|
| **Substrate** | Where does the data live, who owns it, who can access it? |
| **Governance** | How is meaning structured, classified, made machine-legible, and constrained? |
| **Boundary** | What happens at the transition where relationship status changes state? |
| **Evidence** | What makes the record contemporaneous, tamper-evident, and legible to deferred parties without platform mediation? |

None of the four layers is novel in isolation. The synthesis claim — that all four are required, that they compose into a coherent architecture for any system where boundary events carry legal or evidentiary weight, and that missing any one of them is a structural failure — is what the Pattern Commons series demonstrates.

The employment seam is the entry where all four layers became necessary at once. Prior entries demonstrated aspects of the stack; #7 required the complete composition. Pattern Commons #0 names the composition as the pattern.

---

## The Crossing Record

The `seam:CrossingRecord` is the evidentiary unit of every governed crossing. It is the unified base shape that all governed-event records instantiate: gate-check records, lineage records, AI-provenance records, code-change verification records, and multi-party governance records all extend it.

The base shape carries four required field groups:

- **Identity group** — record ID, record type, emission timestamp, emitting party DID
- **Provenance linkage group** — epistemic status of the record's claims, basis when non-asserted, supersession reference when applicable
- **Lineage anchoring group** — chain reference, chain depth, and anchor type for relay-seam records
- **Evidence scope group** — governance event class, bound type, optional evidence decay date

The crossing record is not an audit log. It is a first-class architectural output — the artifact that makes the crossing legible to any deferred party without requiring platform mediation to interpret. A governed crossing that produces no crossing record is not governed; it is an event that occurred and left no evidence of its terms.

IRI namespace: `https://jediwright.github.io/seam-stack/vocab/crossing-record/0.1#`

---

## The Domain Instances

The prior Pattern Commons entries are instantiations of the governed crossing. They differ from each other in domain, legal substrate, participant model, and failure taxonomy. They share the four constitutive properties, the inversion, and the Seam Stack.

| Entry | Domain | Seam trigger | Stakes |
|---|---|---|---|
| #1 — Checkout seam | Commerce | Transaction initiation and completion | Financial; one seam per transaction |
| #2 — High-stakes seam | Healthcare | Patient intake and record handoff | Clinical; one seam per intake; regulatory weight |
| #3 — Profile map as local CRM | Social | Connection formation | Relational; seam per connection |
| #4 — attachArrayObserver | Infrastructure | CRDT state synchronization | Technical; pattern, not domain |
| #5 — Distributed seam | Social networking | Peer handshake; relay exits after sync | Distributed; relay-exits posture demonstrated |
| #6 — CRDT as trust graph | Social | Trust assignment at connection | Graph-structural; trust as local-first state |
| #7 — Employment seam | Labor / legal | Any state change in a working relationship | Legal and evidentiary; all four Seam Stack layers required; full participant model |

The employment seam (#7) is the most demanding instantiation — the one where the failure taxonomy is deepest, the participant model is most complex, and the legal substrate is part of the architecture rather than a wrapper around it. It is not the definition of the class. It is the proof that the class exists and that the architecture is sufficient to handle the hardest case.

---

## What the Pattern Generalizes To

The governed crossing applies to any structured relationship where:

- One party holds contextual knowledge or capability
- Another party holds access control or formal authority
- The relationship changes state in ways that carry legal, evidentiary, or relational consequences
- Neither party should be able to strand the other at the boundary

The employment seam is the highest-stakes instantiation identified to date, but it is not the only one. The pattern applies equally to:

**Platform-worker relationships** — gig economy, platform-mediated labor, algorithmic assignment and de-assignment. The seam fires per engagement. The platform is structurally the relay, not the owner of the relationship.

**Client-agency relationships** — a designer, strategist, or embedded consultant entering and exiting a client engagement. Knowledge artifacts produced during the engagement should write to a substrate the practitioner owns. The seam fires at kickoff, at handoff, and at contract close.

**Research and academic affiliations** — a postdoc, visiting researcher, or lab contractor. The data, code, and institutional context produced during the affiliation is exactly what gets stranded at exit under conventional architectures. The governed crossing disciplines that handoff.

**AI agent delegation** — an agent is granted a capability scoped to a context, acts on behalf of a principal, and the grant expires or revokes. The seam fires per delegation scope. The gate checks capability state at invocation. The crossing record names the agent DID, the grant reference, and the result. This is Pattern Commons #7's Class G instantiated at the pattern level.

**Creative and IP relationships** — a producer attached to a project, a writer under contract, a collaborator under a work-for-hire clause. The IP boundary event at project close is a governed crossing. The record is the legal anchor.

**Care relationships** — a home health aide, personal assistant, or support worker. Informal, rarely documented, high-stakes at transition. The governed crossing provides the architecture for contemporaneous, tamper-evident records where no formal process currently exists.

**Volunteer and civic roles** — board members, committee chairs, open-source maintainers. The knowledge transfer problem is structurally identical to employment. The formal process is thinner or absent. The governed crossing is the architectural response regardless of whether the relationship is compensated.

What these share is not a domain. They share a structural condition: a party with contextual knowledge or capability, a boundary event where that knowledge or capability is at risk of being stranded, and no architecture currently governing what happens at the crossing. The governed crossing is the architecture that applies.

---

## What Varies Across Instantiations

The four constitutive properties — declared scope, grant, gate, record — are invariant. Everything else varies by domain and is specified in the domain entry:

- **Participant model** — who the eligible grantors and crossing parties are; what credential infrastructure they use; what authority each class holds
- **Failure taxonomy** — what states the crossing can enter when properties are not satisfied; how each is recorded; what the recovery path is
- **Legal substrate** — whether the record is an evidentiary artifact in a legal proceeding; what regulatory regimes apply; what jurisdictional reconciliation is required
- **Bundle schema** — what knowledge artifacts cross at the seam; how they are structured; what the receiving party's ingestion format is
- **Identity verification ceremony** — how parties establish cryptographic identity before the crossing fires; what assurance level each class requires

Pattern Commons #0 specifies none of these. They are the work of the domain entries. This entry specifies only what is common to all of them.

---

## Boundary Principles

The governed crossing is the architectural expression of a set of boundary principles derived from the local-first series and formalized in Artifact B (Form C). The principles are PROPOSED per UFO Lexicon v1.5 and carry the Form C cluster stamp.

**P8 — Every boundary crossing is explicit, minimal, and designed.**
No ambient exfiltration. The crossing surface is scoped, its failure states enumerated. The local side loses nothing on failure.

**P9 — Exposure claims are upper bounds.**
The architecture never claims more control than it enforces. Revocation closes streams; it does not guarantee that no copy has escaped. The crossing record's `boundType: exposure-upper-bound` is the vocabulary expression of this principle.

**P11 — Agents are governed parties, never authors of record.**
Any non-human actor touching the data floor is a contact class with its own capability lifecycle, action context, and revocation semantics — checked at act time, not grant time. The employment seam's Class G is the only current worked example of P11 at the data floor.

**P14 — Relay boundaries are governed crossings.**
A relay party holding a crossing with one party while bridging to another does not collapse the governance surface. Each seam in a chain has its own grant, gate, and record. Composition rules CR-1 through CR-5 govern what is required for a composed crossing to be valid.

The full boundary principles set is specified in Artifact B. This entry names those most directly expressed by the governed crossing pattern.

---

## Prior Instantiations as Evidence

The Pattern Commons series does not claim that governed crossings are universal. It claims that the pattern applies wherever the structural condition — contextual knowledge at a boundary, legal or relational stakes at state change, no current architecture governing the event — is present.

The series demonstrates the claim across four built domains and one highly specified domain (employment). It does not prove the claim for all domains. It provides sufficient evidence that the pattern is real, that the architecture is sufficient, and that the four constitutive properties hold across materially different contexts.

NI-5 applies: these claims are local-first-specific on current evidence. No substrate-generality claim is made beyond what the built prototypes demonstrate.

---

## Known Limits

**Post-crossing revocation propagation.** The gate checks capability state at act time. Revocation of a grant does not propagate backward through chains — a crossing that occurred before revocation was issued is not retroactively invalidated. This is a structural limit of the current architecture, not a design failure. It is named and bounded in the crossing record's `boundType: exposure-upper-bound` vocabulary.

**Multi-party governance at scale.** The P13 frontier — governance that composes beyond the individual party — is specified as a Known Limit in Artifact B. The P13 evidence plane (SeamTermAmendmentRecord, ObjectionRecord, ConsentRecord, ResolutionRecord) is the first built machinery addressing this frontier. It is the beginning of a design, not a complete solution.

**Witness quorum and signed-timestamp anchoring.** The `lineageAnchorType: witness-signed` and `timestamp-signed` values are defined in the crossing-record vocabulary but locked pending infrastructure. Author-declared lineage is the current v0 default. This limit is named in the vocabulary and is not papered over.

**Domain-specific failure taxonomies.** Pattern Commons #0 does not specify failure states. Each domain instantiation carries its own failure taxonomy. A general failure taxonomy for the governed crossing class is a future derivation item, not a current known limit — it has not been attempted.

---

## How This Sits in the Series

The Pattern Commons series has been building toward this document without naming it. Each entry demonstrated a governed crossing in a domain-specific context. The employment seam forced all four Seam Stack layers into view simultaneously and made the generalization unavoidable.

Pattern Commons #0 is not the most important entry in the series. Pattern Commons #7 is — because it is the entry where the stakes are highest, the architecture is most fully specified, and the political argument of Full Personhood is demonstrated at the data floor.

Pattern Commons #0 is the entry that makes the series legible as a series. It is the abstract pattern that the domain entries instantiate, the root that the tree was already growing from, named at last.

---

## What Comes Next

Future Pattern Commons entries that instantiate the governed crossing should:

1. Cite Pattern Commons #0 as the parent pattern
2. Specify only what diverges from the four constitutive properties and the Seam Stack — participant model, failure taxonomy, legal substrate, bundle schema, identity ceremony
3. Name the seam trigger (what state change fires the crossing) explicitly
4. Adopt `seam:CrossingRecord` as the base shape for all governed-event records

Open items for future sessions:

- **General failure taxonomy** — a domain-agnostic taxonomy of failure states for governed crossings, derived from the union of existing domain taxonomies
- **Grantor eligibility model** — a general participant model specifying which classes are eligible grantors and which are eligible crossing parties across domains, from which domain entries derive their specific participant models
- **PC#0 Counter-Pass** — this draft is SINGLE-CONTEXT and not paneled; a Counter-Pass in a fresh context is available before any publication-track use

---

*This document is part of the Pattern Commons, the architectural-pattern documentation series produced alongside the local-first prototype work. It is published under the same methodology disclosure as the rest of Systems of Thought: AI-collaborative drafting, human authorial responsibility, intellectual direction held by the named author.*

*The governed crossing pattern and the Seam Stack are documented at [seamstack.org](https://seamstack.org). The governing manifesto-spec is Artifact B — Form C (r2), available in the local-first-series repository.*

*UX Minds, LLC · J. Wright · August 10, 2026*
