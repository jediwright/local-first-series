# Pattern Commons #7 — The Employment Seam

**Status:** Draft v0.5
**Date:** August 8, 2026
**Author:** J. Wright (UX Minds, LLC) · AI-assisted
**Derived from:** onoff.work concept board (Miro); v0.1 spec refinement session, April 29, 2026; v0.2 framing session, April 30, 2026 (AM); v0.3 technical specification session, April 30, 2026 (PM); v0.4 secondary-question resolution sessions, April 30, 2026 (PM, continued) and May 1, 2026; v0.4.1 quality-pass tightenings, May 1, 2026; v0.5 agent-as-governed-party authoring session, August 8, 2026 (applying the Panel Pass-reconciled candidate entry of August 7–8, 2026).
**Series:** Local-first prototype series — Pattern Commons
**Companion entries:** #1 checkout seam · #2 high-stakes seam · #3 profile map as local CRM · #4 attachArrayObserver · #5 distributed seam · #6 CRDT as trust graph

---

## The Pattern in One Sentence

The employment seam is the boundary event that fires when a person enters or exits an employer–worker relationship, and the architectural argument is that knowledge artifacts should be written to a durable substrate the worker owns *before* the seam fires, with the platform facilitating the handoff and exiting the relationship rather than accumulating it.

---

## The Problem It Solves

The modern tech employment relationship persists in a thousand places the formal record does not capture: Slack DMs, half-finished docs, the SME's head, the contractor's local files, the sub-contractor's institutional memory, the half-written wiki page that never made it past draft. When the relationship terminates — through layoff, resignation, contract end, project handoff, or a stage transition from pitch to scope to kickoff — the formal exit process severs access to systems but does nothing to capture what the person actually knew.

The cost is paid in three currencies:

- **Time and money.** Wasted hours searching chat, email, and file history to chase down what someone already knew. Recruitment and re-onboarding cycles. Equipment retrieval friction. Re-training the replacement on the same context the predecessor had already built.
- **Velocity and morale.** Lost momentum on in-flight work. Team disruption. The cultural cost of treating workers as interchangeable when the cost of replacement says otherwise.
- **Reputation.** How the worker was treated on the way out is a company's most durable employer-brand signal. Word of mouth, alumni networks, and the willingness of former workers to refer or return all sit downstream of how the seam was handled.

Existing categories — applicant tracking systems, HRIS platforms, knowledge management tools, exit interview software — optimize either side of the seam in isolation. They optimize the front door (recruiting, onboarding) or the back door (offboarding, exit interview). The seam itself — the *transition* as a first-class object — is unowned. The under-served-ness is most pronounced in the contractor and sub-contractor case, where formal off-boarding processes are thinner or absent altogether and the worker's exposure to classification disputes, payment disputes, and IP claims is highest precisely when the documentary record is weakest.

---

## The Architectural Claim

> The worker owns the knowledge graph. The platform facilitates the handoff and exits.

This is the same claim the local-first series has been making across commerce, healthcare, and social networking, applied to the employment relationship.

In a local-first employment seam:

- The worker's knowledge artifacts — project context, decision history, contact map, work-in-flight, stakeholder relationships — are written to a durable substrate the worker owns and carries with them.
- The platform facilitates the handoff: it translates the worker's native artifact format into something the receiving party (employer, successor, client, sub-contractor) can consume, mediates the legal and identity-verification surface, and exits.
- The platform does not accumulate the relationship. It does not own the social graph. The alumni network is a byproduct of accumulated seams, not a database the platform sits on top of.

This is the architectural inversion. Conventional HR tech sits in the middle and owns the relationship. The employment seam treats the platform as a relay — the relationship lives on the worker's side, the receiving party's side, and the legal record. The platform facilitates the boundary event and gets out of the way.

This inversion is the spec's foundational positive commitment. Everything that follows — the bundle schema, the legal record format, the identity ceremony, the failure taxonomy, the regulatory durability discussion — is downstream of it. It is named explicitly as Principle 0 in the design principles section below.

---

## The Seam Stack

The employment seam is specified against an architectural composition we will call **the Seam Stack** — a four-layer architecture that supplies the technical substrate, governance vocabulary, boundary discipline, and evidentiary envelope the pattern requires. Each layer answers a question the others do not.

| Layer | Question it answers | Technology |
|---|---|---|
| **Substrate** | Where does the data live, who owns it, who can access it? | Solid (W3C Solid Project — Pods, WebID, Solid-OIDC, Web Access Control / Access Control Policy) |
| **Governance** | How is meaning structured, classified, made machine-legible, and constrained when AI-generated? | The Tiered Content Framework (TCF) — six tiers with three cross-cutting governance dimensions |
| **Boundary** | What happens at the transition where the relationship between worker and employer changes state? | The Pattern Commons seam discipline — the seam-as-architectural-object, applied to employment |
| **Evidence** | What makes the record contemporaneous, tamper-evident, and legible to deferred parties without platform mediation? | W3C Verifiable Credentials Data Model 2.0 + RFC 3161 trusted timestamping + OpenTimestamps + bilateral cryptographic signatures |

None of the four layers is novel in isolation. The synthesis claim — that all four are required, and that they compose into a coherent architecture for local-first systems where boundary events carry legal and evidentiary weight — is original to this work. The Seam Stack is the architectural frame within which the employment seam pattern is implementable; it is also the frame within which the prior Pattern Commons entries can be re-read.

The Seam Stack is documented separately at `seamstack.org`. This spec uses it as the reference architecture; the spec earns the right to cite it because the employment seam is the entry where the legal-substrate-as-architecture claim forces all four layers into view at once.

---

## How It Sits in the Series

| | checkout-seam | fhir-seam | localfirst.social | employment-seam |
|---|---|---|---|---|
| Seam fires | Once per purchase | Once per intake | On every new connection | Once per transition (entry, exit, stage change, re-engagement) |
| Far side of seam | Stripe (server) | Mock EHR (server) | Another user's local client | Receiving party (employer, successor, client) + legal record |
| Relay role | Payment processor | FHIR endpoint | WebSocket handshake facilitator | Identity verification + escrowed handoff delivery |
| Relay stores | Nothing | Nothing | Nothing | Nothing — only the verification proof and delivery confirmation |
| Data format translation | None | Local → FHIR R4 | Local → CRDT merge protocol | Local → standardized handoff bundle |
| Error state | Cart preserved | Bundle preserved | Connection fails cleanly, local state intact | Knowledge graph preserved on worker's side; receiving party gets explicit failure signal |
| Multi-party | No | No | Yes (peer-to-peer) | Yes (worker, employer, optional successor, layered participants) |
| Stakes when seam fails | Try again | Clinical record not received | Connection retry | Knowledge severed, livelihood disrupted, reputation damaged |

The employment seam combines properties of the prior four patterns:

- **From checkout-seam:** the discipline of a single, scoped, server-dependent transition with explicit success and failure states.
- **From fhir-seam:** write-before-POST discipline (the worker's knowledge graph must be durable before the seam fires) and richer failure taxonomy (what happens when the handoff is partial, contested, or the receiving party is non-responsive).
- **From localfirst.social:** the platform-as-relay posture, where the durable relationships (alumni network, professional graph) are byproducts of accumulated seams rather than central databases.
- **New to this pattern:** legal-substrate translation. The handoff bundle must speak the language of the receiving party's legal and HR systems, not just transfer files.

---

## The Minimum Server-Dependent Surface

For an employment seam, the minimum server-dependent surface is:

1. **Identity verification.** Confirming that the departing worker is who they say they are, and that the receiving party is authorized to receive the handoff.
2. **Escrowed delivery of the handoff bundle.** The bundle is held briefly, verified, and delivered. The platform does not retain a long-term copy.
3. **Legal record creation.** A timestamped, signed proof that the handoff occurred, with what was transferred and to whom. This is the audit artifact for both sides.

Everything else is local. The worker's knowledge graph, the format of artifacts, the contact map, the project history, the wiki entries, the asset library — all of it lives on the worker's substrate and travels with them.

---

## The Failure Taxonomy

The checkout seam has two states: success and try again. The fhir seam has four. The employment seam has nine, each with different operational meaning:

| State | What happened | Recovery posture |
|---|---|---|
| **Handoff complete** | Bundle delivered, receiving party confirmed receipt | Legal record created. Worker retains local copy. |
| **Handoff pending** | Bundle in escrow, receiving party not yet confirmed | Worker's local state intact. Escrow timeout policy applies. |
| **Handoff disputed** | Receiving party contests bundle contents | Mediation surface. Worker's local copy is the source of truth pending resolution. |
| **Handoff partial** | Some artifacts transferred, others blocked (NDA, IP claim, account lockout) — potentially by multiple blocking parties in layered-employer cases | Explicit list of what transferred and what didn't, with each blocking reason and each blocking party's signature. Worker retains full local copy regardless. |
| **Handoff refused** | Receiving party declines to receive | Worker retains full local copy. Legal record notes refusal. |
| **Worker unavailable** | Departing person cannot or will not produce the bundle | Receiving party gets explicit signal. No fabrication, no inference. |
| **Account pre-empted** | A party with IT authority locked accounts before the handoff completed | Worker's local substrate preserves what was already captured. The lockout is recorded as the failure cause, not as the worker's failure to deliver. The bundle records *which party's* IT lockout fired — in contractor cases, this can be the operational counterparty, the worker's own corporate entity acting as primary employer, or both. |
| **Reclassification pending** | Classification of the relationship is contested between worker and counterparty (1099 vs W-2 status, ABC test reclassification, EU Platform Work Directive presumption challenge, etc.) | Bundle finalized with `seam:RelationshipStructure` cluster recording all parties' classification claims and attestations. From the seam's perspective, the seam fires successfully; the relationship's classification is what's contested, and adjudication happens in the relevant forum (state agency, court, EU labor authority). |
| **Prior-bundle-unverifiable** | Re-engagement seam references a prior bundle that fails verification (signature broken, vocabulary version unsupported, IRI no longer resolves) | Worker's local Pod copy is consulted; if also unverifiable, the re-engagement proceeds as a new seam without prior-bundle reference; the unverifiability is recorded as part of the new bundle. |

The *account pre-empted* state is the one current HR practice handles worst. When a party with IT authority locks accounts before the worker has had time to produce a handoff, the knowledge transfer fails — and the conventional record blames the worker. A local-first employment seam preserves the worker's pre-lockout substrate and makes the lockout itself the recorded failure cause. This is where contemporaneity does its most consequential work: because the record was being written before the lockout occurred, its evidentiary weight cannot be challenged on the grounds that the worker constructed it after the fact. The sequence is in the record. The lockout timestamp is in the record. Neither party can revise them.

The cryptographic mechanism that makes this concrete is the temporal precedence anchored by RFC 3161 timestamps and OpenTimestamps proofs in the legal record format (specified below). The locking party's IT log, signed by that party's IT role, contains the lockout timestamp; the worker's pre-lockout substrate, signed by the worker, contains the assembly window timestamp. The cryptographic envelope can prove the lockout preceded the assembly window. This is what makes the worker's pre-lockout substrate evidentially load-bearing rather than a post-hoc claim. In layered-employer cases (contractor arrangements where the worker has both a primary employer and an operational counterparty, each with potential IT authority over different systems), the lockout signature is by whichever party's IT role fired the lockout — the bundle records this explicitly so the deferred party reading the record knows which party severed access first.

The *reclassification pending* state is new in v0.4 and reflects the recognition (from the contractor-case work) that classification of the relationship can itself be contested independently of the seam firing. The seam still fires; the bundle still completes; the classification dispute is preserved in the record for the forum that will adjudicate it. This is a structurally important separation: a worker who is reclassified after the fact (a 1099 contractor reclassified as a W-2 employee under an ABC test, with all the back-pay and benefits implications that follow) needs the contemporaneous record of what the parties claimed at the time, not an after-the-fact reconstruction.

The *prior-bundle-unverifiable* state, also new in v0.4, addresses re-engagement. When a worker returns to an employer they previously left — increasingly common, with ADP's March 2025 data showing 35% of all new hires are returning employees and roughly two-thirds of new hires in the information sector — the new seam may reference the prior bundle to establish continuity of the employment relationship. If that prior-bundle reference fails verification, the ceremony does not abort silently; it records the unverifiability and proceeds as a new seam without prior-bundle reference (with both parties' consent) or aborts (if either party requires verifiable continuity).

---

## The Format Translation Problem

The worker's native format is whatever they actually use to think and work: notes apps, scratch documents, a kanban board, a personal wiki, a contact list, a photo of a whiteboard, a recorded voice memo. The receiving party's format is whatever their organization expects: a structured handoff document, a project status template, an HRIS field map, a contractor onboarding packet.

The translation happens at the seam boundary, not inside either system. The pattern requires:

- A canonical handoff bundle schema — extensible, versioned, human-readable.
- A translator from the worker's native format(s) to the bundle.
- A translator from the bundle to the receiving party's expected ingestion format.
- A retained copy of the bundle on both sides, in canonical form, regardless of what either side does with it locally.

The bundle is the artifact that survives. If the platform disappears, the bundle is still readable. If the receiving party never opens it, the worker still has their copy. If the worker loses their device, the bundle has been delivered and is recoverable from the receiving party. The pattern is robust to the disappearance of any single party.

---

## The Platform's Accountability

The prior three seams each raise the buyer/user question implicitly: who commissions the relay, and whose interests does it serve? In the checkout seam, the merchant. In the fhir seam, the clinical institution. In localfirst.social, neither — the relay is symmetric by design, serving both parties to the connection equally.

The employment seam makes the same choice localfirst.social made, but for a harder reason. The handoff bundle can be initiated worker-side or employer-side, and a given implementation may be purchased by either. But the legal record — the component that makes the handoff evidentiary — cannot be produced by one party alone. It requires bilateral participation: worker and employer confirm the same facts, sign the same artifact, and each receive a copy. The platform's only irreducible role is producing that bilateral artifact. Everything else it does is facilitation it could decline to do; the legal record is the thing it structurally cannot produce by favoring one side.

That structural necessity is the basis for the pattern's accountability claim: the platform is accountable to the integrity of the record, not to either primary party. This is not a neutrality claim in the arbitration sense — the platform does not adjudicate disputes — it is a recorder claim. What happened is recorded. What should have happened is decided elsewhere.

Four architectural conditions follow from this:

- **Contemporaneity.** The record must be written as the seam fires, not reconstructed afterward. Post-hoc record construction is indistinguishable from post-hoc record fabrication. The platform's value is that the record was written when neither party knew how contested the separation would become.
- **Tamper-evidence.** Both parties receive cryptographically signed copies. The platform cannot alter the record after delivery without both copies diverging — the divergence is the evidence of tampering.
- **Multi-perspective in contested cases.** When the parties disagree on the facts of a separation, the platform does not collapse their accounts into a single narrative. It preserves three views: worker-submitted, employer-submitted, and the escrow log that records what was actually delivered when. The disagreement is part of the record.
- **Funding neutrality.** A platform funded primarily by employers has a structural incentive to produce records that favor employer-interpretable facts. A platform funded primarily by workers has the inverse incentive. The funding model must be designed to preserve the recorder posture — transaction fees split by formula, institutional funding from parties with no stake in individual outcomes (professional associations, state workforce infrastructure, benefits brokers), or a combination.

The architecture is implementer-agnostic by design, not by accident. The pattern can be implemented as a worker-primary product surface (a service the worker subscribes to, sold through professional associations, freelancer platforms, or unions), an employer-primary product surface (a service the employer purchases, sold alongside HRIS or compliance tooling), or a pattern-only reference implementation that no one commissions and that exists as a public-good demonstration. All three are consistent with the four conditions above. The architecture earns its accountability from structure — bilateral signatures, two independent timestamping authorities, a recorder rather than adjudicator posture, hash-only retention beyond the escrow window — not from sponsorship. A reader evaluating any specific implementation should look at whether the four conditions are satisfied, not at which side commissioned the build.

What this means for product strategy is a question the spec deliberately leaves open. The pattern is agnostic to which surface gets built — and available to whoever builds it.

---

## The Six Design Principles

The architectural conditions above name what the spec must produce. The design principles below name how the spec navigates choices when those conditions could be operationalized multiple ways. They emerged from the v0.4 work resolving secondary questions about contractor classification, re-engagement, cross-border identity, Pod provider operational models, collective bargaining, and mass events. Each principle did real work in those resolutions; surfacing them here makes the spec's authorial posture explicit. Principle 6 emerged from the v0.5 work formalizing agent-as-governed-party; like the others, it did its work — in the attribution model ruling and the grant-reference requirement — before it was named.

The principles divide into one foundational positive commitment, four constraints on what the spec doesn't do, one operative choice when the constraints could be operationalized multiple ways, and — as of v0.5 — one participant-scope commitment governing non-human participants.

### Principle 0 — The worker owns the knowledge graph.

This is the architectural inversion stated as a commitment. Everything else follows: the bundle is assembled in the worker's Pod and signed with the worker's key; the platform escrows briefly and exits; the alumni network is a byproduct of accumulated seams rather than a database the platform owns; cross-seam continuity in re-engagement is established through bundles the worker holds, not through platform-side memory of who used to work where. When the four constraints below appear to permit multiple paths, this principle is the tiebreaker.

### Principle 1 — Per-Particle, per-indicium optionality.

Optionality is structured at the smallest meaningful unit, not at field or bundle level. Each fact stands or falls separately. The spec does not offer "include this whole cluster or omit it" as a choice; it offers "include this Particle" or "omit this Particle" with the granularity of consent and disclosure attached to the Particle itself.

This bites hardest in contractor classification. The three-tier `classificationAttestation` (Tier 1 declared classification, Tier 2 controlling-test acknowledgment, Tier 3 indicia) places Tier 3 indicia at per-Particle opt-in, independently attested per party. Each indicium — degree of control, integration into the business, opportunity for profit or loss, investment in equipment, permanency, skill required — is a separate Particle that each party can include or omit independently. A worker may attest to a controlling test acknowledgment without committing to specific indicia. A counterparty may decline to attest to indicia the worker attests to. The bundle records the asymmetry rather than forcing the parties to either agree on a complete picture or produce no record at all.

### Principle 2 — Cryptographic reference, not platform persistence.

Continuity across seams is established by hash-and-IRI links between bundles held by the parties, not by platform-side memory. The platform retains nothing across seam-firings beyond the hash-only transparency log required for after-the-fact challenges to escrow log authenticity. When a worker re-engages with a former employer, the new seam references the prior bundle by content hash and IRI; the prior bundle is verified against the parties' retained copies, not against a platform-side record of "this worker used to work here."

This principle also bites in cross-border cases: trust list state at the moment of signing is captured by hash-and-snapshot in the bundle, not by reference to a platform-maintained registry of trust list state over time. The bundle is self-contained; the platform's role is brief, structural, and not architecturally load-bearing for any cross-time reasoning.

### Principle 3 — Regime fragmentation accommodated structurally, not papered over.

The spec records heterogeneity rather than pretending unification. Different jurisdictions have different identity assurance frameworks, different evidentiary standards, different timestamping authorities, different revocation mechanisms; the spec's response is to record what each party brought and what the regime context was at signing time, not to map everything to a fictional unified standard.

The 1–5 canonical assurance scale published at `seamstack.org/vocab/assurance/` is named honestly as a useful fiction rather than a binding determination: it gives deferred parties a comparable scale across regimes, but the bundle also records each party's native regime assurance level, the regime identifier, and the jurisdiction, so a deferred party who needs to do regime-specific reasoning has the underlying material. The canonical scale is for triage; the underlying material is for adjudication. The spec does not pretend the scales are commensurable; it provides a useful approximation alongside the underlying heterogeneity.

### Principle 4 — Records, doesn't certify or endorse.

The spec records what the parties committed to and what was true at signing time. It does not certify the truth of those commitments and does not endorse the parties' attestations. Classification attestations record claims; trust-list snapshots record state; provider attestations record commitments; signatures record what each party signed at what time. Evidentiary value comes from contemporaneous recording, not from authoritative endorsement.

This principle is what allows the spec to handle disputes faithfully without appearing to adjudicate them. A bundle that records two divergent classification attestations is not making a claim about which classification is correct; it is recording that the parties disagree, with each party's signed claim preserved separately. The forum that will adjudicate (state agency, court, EU labor authority) has the material it needs — including the disagreement itself as a primary fact — without the spec having pre-judged it.

### Principle 5 — Worker-side evidentiary protection over employer-side operational convenience when the two are in tension.

This is the spec's positive operative commitment. The first four constraints describe what the spec doesn't do; this one describes what the spec affirmatively chooses when forced to choose.

Concrete instances:

- **Worker-side review is unbatchable.** Even in declared mass events with employer-side `seam:contributionMode` set to *batched* or *delegated*, the worker side of each seam fires independently. A worker in a 10,000-person reduction in force gets the same per-seam review window as a worker in a single termination. The spec accommodates the operational reality of mass events by extending the escrow window (72h to 168h) and by allowing employer-side batching, but it does not extend that batching to the worker side.
- **Class-action aggregation is consent-gated.** The `seam:classActionAggregationConsent` attribute is independent — separate from the worker's general consent to the bundle's existence — and each worker-party retains the choice to decline aggregation even when other affected workers consent. The architecture supports class-action discovery (a plaintiff's counsel investigating a pattern can request aggregated bundles where workers have consented) but does not assume it.
- **Account pre-empted state preserves temporal precedence cryptographically.** When the locking party fires the lockout before the worker can produce the bundle, the bundle records the locking party's lockout timestamp (signed by that party's IT role) alongside the worker's pre-lockout substrate (signed by the worker), and the RFC 3161 timestamps with OpenTimestamps anchoring make the temporal precedence externally verifiable. The worker is not blamed for the failure to deliver; the lockout is recorded as the failure cause.

This principle is honest about its asymmetry. The spec's adoption pattern follows from this asymmetry: the architecture is more attractive to plaintiff-side firms, worker-side unions, gig-worker advocacy organizations, and labor-side regulators first; employer adoption follows from regulatory pressure rather than from the architecture's appeal to operational convenience. The asymmetry is not accidental; it is a design choice the spec makes explicitly.

### Principle 6 — Agents are governed parties, never authors of record.

This is the spec's participant-scope commitment, added in v0.5. Non-human participants act only under a human-issued, revocable capability grant checked at invocation time; they hold no record-authorship authority of any kind; and legal responsibility for every agent-performed action is resolvable from the record itself to a juridical person.

The three clauses each do structural work:

- **Governed, at invocation time.** An agent's authority does not flow from a credential of its own; it flows from a capability grant issued by a human operating party, and the grant is checked at every invocation by the `assertCapabilityCurrent()` gate. The grant/revoke/gate lifecycle is the governance surface — operational and logged, not descriptive. Revocation takes effect against the gate, not against a policy document.
- **Never authors of record.** An agent-class participant cannot attest, contribute a worker-submitted or employer-side account, hold or exercise any Class A sub-role authority, self-declare separation cause, submit a contest on any party's behalf, or sign any legal record component. This prohibition is SHACL-enforced at the schema level (per the Class G shape in the bundle schema), not a UI-layer default.
- **Resolvable to a juridical person.** Attribution to the agent is operational — gate, audit, and revocation run against the agent's identity — but legal responsibility rests structurally with the granting party. Every `seam:gateCheckRecord` carries a required grant reference so the responsible juridical person is derivable from the record itself, with no external DID-document lookup. Where the grantor is a Class C representative, the chain-of-authority condition extends this resolution one link further, through the representative's worker-issued authorization VC, back to the worker.

The commitment is symmetric across granting parties: a worker-granted agent and an employer-granted agent are governed identically. This is deliberately distinct from Principle 5's asymmetry — Principle 5 chooses the worker's side when evidentiary protection and operational convenience conflict; Principle 6 constrains what any party's agent may be, regardless of side.

The commitment also disciplines future versions. An agent with substantive record-authorship — one that could attest, contribute accounts, or sign — is outside this principle's boundary, and admitting one would require explicitly amending a named principle rather than quietly extending Class G. That is the spec's no-silent-breakage discipline applied to its own commitments.

---

## Regulatory Durability

The legal record is only as useful as its legibility to the parties who will consult it. Those parties operate under different regulatory regimes, on different timelines, with different evidentiary standards. The pattern is designed for the most demanding combination currently in force — not the most permissive.

The major regimes the record must satisfy:

**EU AI Act — labor provisions.** The EU AI Act classifies certain employment-related AI systems as high-risk, requiring transparency, human oversight, and auditability. A handoff bundle that includes AI-assisted summaries, performance assessments, or role-fit evaluations may itself be subject to these requirements. The record must be auditable at the artifact level: which components were AI-assisted, what inputs produced them, and whether human review occurred before the seam fired. The schema's AI-provenance attributes (specified below) make this auditable at the schema layer, not by application logic.

**US anti-discrimination regimes.** Title VII of the Civil Rights Act, the Americans with Disabilities Act (ADA), and the Age Discrimination in Employment Act (ADEA) each create potential evidentiary claims against the separation record. The contemporaneous, tamper-evident, multi-perspective record the pattern produces is the artifact a plaintiff's counsel or an EEOC investigator would want to see. The architecture is designed for this use case, not merely compatible with it.

**Contractor classification regimes.** The Fair Labor Standards Act (US federal) sets the baseline for employee-versus-contractor distinction; state ABC tests in California (AB5), Massachusetts, New Jersey, and a growing list of other jurisdictions impose stricter presumptions of employee status. The EU Platform Work Directive establishes a presumption of employment in algorithmically-managed work that contractor classification must rebut affirmatively. The `seam:RelationshipStructure` cluster's three-tier classification attestation (specified in the bundle schema) maps to the evidentiary requirements of each regime: Tier 1 records each party's declared classification, Tier 2 records each party's acknowledgment of which controlling test applies in the relevant jurisdiction, Tier 3 records per-indicium attestations the relevant test treats as probative. The cited cases anchoring this (Lyft New Jersey, Uber/Lyft Massachusetts, *Manoli*, Amity, Microsoft, FedEx Ground — discussed in the participant-model section below) demonstrate that classification disputes routinely produce settlements and judgments in the tens to hundreds of millions of dollars; the record's evidentiary weight is correspondingly load-bearing.

**Collective bargaining regimes.** The National Labor Relations Act governs private-sector US labor relations; 5 U.S.C. § 7114 governs federal-sector equivalents. *NLRB v. J. Weingarten, Inc.*, 420 U.S. 251 (1975), establishes the worker's right to representation in investigatory interviews that may result in discipline, with the federal-sector equivalent at 5 U.S.C. § 7114(a)(2)(B). *Troy Grove* (NLRB, 2023) extends Weingarten rights to strike replacement workers. The `seam:CollectiveBargainingContext` and `seam:GrievanceProcedure` clusters map to evidentiary requirements for unfair labor practice charges, grievance filings, and arbitration proceedings. Standard CBA grievance procedure timing windows (typically 30 days for filing, 5 for first-step response, 20 for second-step, 30 for arbitration demand) are accommodated by the schema's deadline fields. The schema overlays the CBA, not the reverse: the CBA's procedural rules govern, and the schema records compliance with those rules contemporaneously.

**Mass-event regimes.** The Worker Adjustment and Retraining Notification Act (WARN, US federal) requires 60 days' notice for plant closings and mass layoffs above specified thresholds; state mini-WARN statutes in New York, California, and other jurisdictions impose stricter requirements. The EU European Works Council Directive (2009/38/EC) and EU Collective Redundancies Directive (98/59/EC) impose parallel notification and consultation requirements at the European level. Bankruptcy-driven mass layoffs and acquisition-driven mass separations are scope variants the regimes accommodate. The `seam:massEventContext` cluster's notice-date and legal-regime fields map directly to the regulatory triggers; the extended escrow window (168h) accommodates the operational reality of large-scale notification while preserving per-worker review windows.

**Immigration timelines.** For workers on employer-sponsored visas — H-1B, L-1, O-1, TN — the separation event triggers a legally bounded clock. The legal record must capture the exact date and terms of separation with enough precision to support status maintenance, transfer, or grace-period calculation. Imprecision here is not a minor inconvenience; it is a deportation risk.

**Unemployment insurance.** State unemployment agencies adjudicate separation cause — resignation versus layoff versus termination for cause — using whatever record exists. The pattern's multi-perspective record in contested cases is directly relevant: if the employer and worker disagree on separation cause, both accounts are preserved separately rather than collapsed into a single employer-authored narrative. The state agency sees the disagreement, not a resolved version of it.

**COBRA and benefits continuation.** The date the employment relationship ends determines COBRA eligibility windows, benefits continuation rights, and HSA contribution cutoffs. The legal record's timestamp is the authoritative source for these calculations. Imprecision or post-hoc reconstruction introduces liability on both sides.

**Professional licensing and certification.** In regulated professions — healthcare, law, finance, engineering, education — the employment record may be required for license maintenance, renewal, or disciplinary proceedings. The bundle's canonical form must be legible to licensing boards without platform mediation.

**GDPR and CCPA.** The worker's personal data — including the knowledge graph, the contact map, the project history — is subject to data subject rights under GDPR (EU) and CCPA (California) regardless of which jurisdiction the employer operates in, if the worker is covered. The pattern's local-first architecture is structurally compatible with these regimes: the worker already owns the substrate. But the legal record itself, held briefly in escrow and then delivered to both parties, must have a defined retention policy, a deletion pathway, and documented consent at the point of seam firing.

**Whistleblower and protected-disclosure regimes.** Sarbanes-Oxley, Dodd-Frank, the EU Whistleblower Directive, and state-level protected-disclosure statutes each create heightened evidentiary requirements when the worker has made or is making protected disclosures. The schema accommodates this through `seam:regulatoryRegimeFlags` Particles (specified below) that mark the seam-firing context as triggering specific regulatory regimes, unlocking additional schema validations and additional deferred-party access.

**Cross-border identity infrastructure.** When the worker and employer operate under different national identity infrastructures, the credential reconciliation across jurisdictions is itself a regulatory regime. eIDAS 2.0 (Regulation (EU) 2024/1183, in force May 2024) establishes the European Digital Identity Framework, with EUDI Wallets demonstrated at the December 2025 Brussels Launchpad showing cross-border interoperability. The UK Digital Identity and Attributes Trust Framework (DIATF) achieved statutory status in December 2025 with 48 certified providers. US credential infrastructure (PIV, CAC, NIST 800-63 assurance levels) operates on different vocabulary. The `seam:credentialContext`, `seam:trustListReference`, and `seam:legalRecognitionDeclaration` fields map to the evidentiary requirements of each regime, recording each party's native assurance level, the regime context, and trust-list state at signing — without forcing a fictional unified standard. The 1–5 canonical assurance scale at `seamstack.org/vocab/assurance/` is published as a useful fiction (per Principle 3) for triage; the underlying regime material supports adjudication.

The empirical anchor for re-engagement: ADP's March 2025 data shows 35% of all new hires are returning employees, with the information sector running roughly two-thirds returnee rate. The pattern's `seam:SeamFiringContext` cluster, `seam:carriedForward` per-Particle attribute, and `seam:reEngagementPosture` declaration address what is now the dominant pattern of new-hire onboarding, not an edge case.

The pattern does not resolve conflicts between these regimes — jurisdictional conflicts in cross-border separations are a legal problem, not an architectural one. What the pattern provides is a record that is legible, contemporaneous, and tamper-evident across all of them. A record that satisfies the most demanding regime is not over-engineered. It is the only version worth building.

---

## The Layered Participant Model

The prior seams involve two parties at the boundary event: buyer and seller, patient and institution, peer and peer. The employment seam arrives with more participants structurally present, each with a legitimate interest in the record.

This spec organizes participants into eight identity classes, each with its own credential infrastructure and verification ceremony (specified in the Identity Verification Ceremony section below). The classes are:

- **Class A: Individual legal personalities** — the worker, in their various juridical capacities
- **Class B: Employer-issued roles** — HR, direct manager, IT, employer-side legal counsel, bargaining-unit liaison
- **Class B′: Client-party roles** — operational counterparty roles in contractor and vendor arrangements (engagement manager, project sponsor, vendor-management-office contact)
- **Class C: Third-party-verified professional representatives** — worker-side legal counsel, immigration counsel, tax preparer, benefits administrator
- **Class D: Institutional actors** — union representatives (with sub-classes D1–D4), state agencies, courts, future employers (consent-gated)
- **Class E: Self-asserted witnesses** — colleagues, family members, designated witnesses without formal credentials
- **Class F: Worker-adjacent individuals** — dependents, beneficiaries, emergency contacts
- **Class G: Agent-class participants** — non-human actors (AI models or automated systems) operating under a revocable capability grant from a human operating party; structurally grantee-only [v0.5]

Each class has structurally different identity verification needs because each draws on different credential infrastructure. The worker is self-sovereign (Class A); the HR professional is employer-credentialed (Class B); the engagement manager at the operational counterparty is also employer-credentialed but not by the worker's primary employer (Class B′); the worker's attorney is bar-credentialed (Class C); the union steward is institution-credentialed by the bargaining unit (Class D); the personal witness has no formal credential at all (Class E); the worker's spouse exercising COBRA continuation rights has their own self-sovereign identity but is structurally distinct from the worker (Class F); the AI agent assisting with bundle processing holds a DID issued and scoped by its human operating party, with authority flowing from the capability grant rather than from any credential of its own (Class G).

The full layered participant inventory follows the class structure:

**On the worker side (Class A — Individual legal personalities):**

The worker is one individual, but operates in multiple legal personalities simultaneously, each potentially relevant at different points in the seam-firing ceremony or in deferred-party consultations of the record. Sub-classes A1 through A6 are defined in the Identity Verification Ceremony section below.

**On the employer side (Class B — Employer-issued roles):**

- **HR.** The administrative party. Manages the employer-side bundle contribution and the employer's copy of the legal record.
- **Direct manager.** Subject-matter witness to the work being handed off. May contribute to the bundle directly.
- **Legal.** Employer-side counsel in contested separations. Role-conditioned access to the record parallel to worker-side legal.
- **IT.** Manages the account access timeline — the sequence of what was locked when. In account pre-emption cases, IT's log is part of the evidentiary record whether IT intends it to be or not. The pattern makes that explicit.
- **Bargaining unit liaison.** Where a union exists, the employer-side liaison to the bargaining unit has a corresponding witnessing role.

**On the client-party side (Class B′ — Client-party roles):**

In contractor and vendor arrangements, the worker's primary employer (typically the worker's own corporate entity, for B2B contractor relationships) is structurally distinct from the entity directing the work. Class B′ covers operational-counterparty roles that exist *because* the relationship is contractor rather than W-2:

- **Engagement manager / project sponsor at the client.** The party at the operational counterparty who directs the work, sets deliverables, and witnesses what was handed off. Role-conditioned access parallel to a direct manager in Class B, but credentialed by the operational counterparty rather than by the worker's primary employer.
- **Vendor-management-office (VMO) contact.** The administrative party at the operational counterparty managing the contractor relationship. Often the party who signs the master service agreement and statement of work; in classification disputes, the VMO's contemporaneous record of how the relationship was structured is a primary fact.
- **Client-side IT.** In contractor arrangements, account lockout authority can rest with the operational counterparty, the worker's primary employer, or both. The bundle's *account pre-empted* failure state records which party's IT lockout fired; Class B′ IT's signature attaches when the operational counterparty is the locking party.
- **Client-side legal.** Counsel for the operational counterparty in contested separations involving the contractor relationship. Role-conditioned access parallel to employer-side legal in Class B.

The cited cases anchoring Class B′ and the relationship-structure cluster demonstrate why the contractor case is structurally distinct rather than a marginal variant of the W-2 case. *Lyft v. Platkin* (New Jersey, September 2025) settled at $19.4 million for unemployment insurance contributions on misclassified drivers — a state-level enforcement action with a specific evidentiary pattern around how the relationship was structured and recorded. *Massachusetts v. Uber/Lyft* (June 2024) settled at $175 million, the largest worker-misclassification settlement in Massachusetts history, illustrating multi-jurisdictional pattern across ride-share platforms. *Manoli v. Practically Perfect Vacations* (Mass. Super. Ct., February 2025) shows judicial application of the state's ABC test outside the platform-economy context. *Amity In-Home Care* (California, $2.3 million, February 2025) demonstrates sectoral exposure beyond ride-share — home-care, construction, last-mile delivery, and creative production all face the same classification dynamics. The historic anchors (*Microsoft* at $97 million in 2000, *FedEx Ground* at $228 million across multiple states by 2015) show the pattern is durable rather than novel to the gig economy. In each case, the contemporaneous record of how the relationship was structured — what each party attested to at the time — is the load-bearing evidence. The architecture's design for these cases is not retrofitted; it is the contractor case taken seriously from the start.

**Worker-side professional representatives (Class C):**

- **Worker-side legal counsel.** Worker-side attorney or advocate, particularly in contested separations, wrongful termination claims, discrimination cases. Their access to the record is role-conditioned: they see what their client authorizes, plus the escrow log.
- **Downstream professional parties.** Immigration counsel (if visa status is affected), tax preparer (1099/W-2 classification, contractor status), benefits administrator. Each needs a structured slice of the record, not the full bundle.

**Institutional actors (Class D):**

- **Union or collective bargaining representative.** Where a bargaining unit exists, the representative has a legitimate interest in the record — terms of separation, compliance with the collective agreement, documentation of the separation cause. v0.4 refines Class D union representatives into four operational sub-classes:
    - **D1: Steward.** The bargaining-unit representative present at the workplace. Typically the first union representative to witness an investigatory interview, file a grievance, or sign a witnessing-party attestation. Stewards are credentialed by the union local.
    - **D2: Business representative.** The professional union staffer who manages grievances at second-step and arbitration demand. Credentialed by the union local or the international.
    - **D3: Legal counsel.** Union-side attorney or in-house counsel. Role-conditioned access parallel to worker-side legal counsel in Class C, but representing the bargaining unit's institutional interest as well as the individual worker's. Credentialed by the bar plus the union.
    - **D4: Investigator.** Union-side investigator in contested cases — workplace investigations, harassment cases, grievance fact-finding. May not be a steward or attorney; credentialed by the union for the specific investigation.
    
    The CBA's procedural rules govern; the schema overlays the CBA, not the reverse. The four sub-classes correspond to the witnessing roles standard CBA grievance procedures recognize, not to a categorization the spec invents.

- **State agencies.** Unemployment insurance adjudication, WARN Act compliance, tax withholding confirmation, anti-discrimination enforcement. The state is a deferred third party that may consult the legal record as a primary source. The record's format must be legible to these agencies without platform mediation.
- **Future employers.** With worker consent, a future employer or client may request verification of the prior relationship — employment dates, role, project scope, departure cause. The pattern supports consent-gated disclosure; the worker controls what future parties can see.
- **Courts and administrative tribunals.** In wrongful termination, discrimination, wage theft, classification, or immigration proceedings, the legal record may become evidence. Contemporaneity and tamper-evidence are what give it evidentiary weight.

**Self-asserted witnesses (Class E):**

Some seam-firings involve a witness who has no formal identity credential — a colleague present at a layoff conversation, a family member at a high-stakes resignation, a friend serving as the worker's chosen witness in a hostile separation. The pattern accommodates this by allowing the witness to sign with a self-asserted WebID at seam-firing and to have their signed account included in the bundle as a witnessing-party Cluster.

**Worker-adjacent individuals (Class F):**

Individuals on the worker side whose interests are affected by the seam but who are not the worker themselves. Each has their own self-sovereign DID. Role-conditioned access is typically narrow and consent-gated by the worker. Sub-classes within F:

- **F1: Dependent receiving benefits continuation** — COBRA spouses, dependent children, domestic partners on shared health plans.
- **F2: Estate beneficiary distinct from legal successor** — the people who receive from the estate that an A6 successor administers.
- **F3: Emergency contact / notified party** — designated for notification at separation, no consent authority.

**Agent-class participants (Class G):** [v0.5]

Non-human actors — AI models or automated systems — operating under a capability grant issued by a human operating party. Permitted grantor parties are the worker (Class A), employer-issued roles (Class B), client-party roles (Class B′), and — under the two chain-of-authority conditions specified in the Identity Verification Ceremony section — worker-side professional representatives (Class C). The agent holds its own DID/keypair under `seam:identityClass: Agent`, issued and scoped by the operating party at grant time and revocable at any time; but unlike Classes B through D, whose credential chains establish their right to act, the agent's DID establishes only *addressability* — the identity the authorization gate checks and the access log records. The authority lives in the grant.

Class G participants are structurally grantee-only. They cannot attest, cannot contribute a worker-submitted or employer-side account, cannot hold or exercise any Class A sub-role authority, cannot self-declare separation cause, cannot submit a contest on any party's behalf, and cannot sign any legal record component. These are schema-level constraints (SHACL-enforced, per the bundle schema), not UI-layer defaults. What an agent can do is act within its granted capability scope, with every invocation checked by `assertCapabilityCurrent()` and logged as a `seam:gateCheckRecord` under the agent's own identity. Attribution to the agent is operational — gate, audit, and revocation run against the agent's identity — while legal responsibility for every agent-performed action rests with the granting party and is resolvable from the record itself via the required grant reference (per Principle 6).

The bundle and legal record are not single artifacts handed from one party to another. They are structured documents with role-based views. Each participant class (and sub-class within Classes A, D, and F) sees the version of the record their role entitles them to see. The full multi-perspective record — all three views in contested cases — is accessible only to parties with explicit authorization from both primary parties, or by legal process. Class G participants are the exception to the role-based-view model: an agent holds no role-conditioned view of the bundle — its read and act surface is defined by the scope of its capability grant and checked at invocation, not by `seam:participantVisibility` tags.

---

## What the Pattern Inherits From the Local-First Argument

This is not a new architectural argument. It is the local-first argument applied to a domain that has not seen it:

- **Worker owns the substrate** — same claim as "user owns the document" in collaborative document tools, "patient owns the record" in fhir-seam, "user owns the social graph" in localfirst.social.
- **Platform as relay** — same posture as the WebSocket relay in localfirst.social: facilitate the handshake, exit the relationship.
- **Durable across platform disappearance** — the bundle is readable without the platform. If the company building the platform shuts down, the worker still has the bundle and the receiving party still has the bundle.
- **No accumulation as default** — the platform does not build a knowledge graph by aggregating worker data. The graph is on the worker's side. Aggregation is opt-in and reversible.

If the platform behaves like a conventional SaaS — accumulates the data, sits in the middle, sells access back to the worker — it is not implementing the pattern. It is using the pattern's vocabulary to ship the same product the category already has.

---

## What the Pattern Does Not Solve

The pattern is honest about its limits:

- **It does not solve the layoff.** It does not prevent the cost of being let go. It changes the recoverability of what comes next.
- **It does not solve hostile exits.** When an employer wants the knowledge severed (NDA enforcement, IP claims, post-termination disputes), the platform cannot override the legal substrate. It can record the dispute and preserve the worker's pre-lockout state, but the legal outcome happens elsewhere.
- **It does not solve the recruiting problem.** The structural condition that produces lengthy recruitment cycles — an industry that cannot retain or transfer what it knows — is upstream of what the pattern addresses. The employment seam reduces the cost of that symptom but does not change the condition.
- **It is not a guarantee that the receiving party reads the bundle.** A handoff that nobody opens is a delivered handoff, not a useful one. The pattern produces the artifact and the audit trail; it does not produce the reading.
- **It does not adjudicate.** The platform records the disagreement faithfully. It does not determine who was right. Courts, arbitrators, and administrative tribunals do that using the record the platform produced.

---

## Why This Is the Seventh Pattern, Not Just an Application

The first six Pattern Commons entries are domain-agnostic but were each derived from a specific prototype that demonstrated the seam in a single domain. The employment seam is a candidate seventh entry because:

1. **The domain is materially different.** The prior patterns operate in commercial, clinical, and social domains. The employment seam operates in the labor and legal domains, with HR/employment law and contractor-versus-employee distinctions that introduce constraints the prior patterns do not handle.
2. **The failure taxonomy is broader.** Nine explicit states, with the *account pre-empted* and *reclassification pending* states being classes of failure the prior patterns do not encounter.
3. **Multi-party from the start.** Even localfirst.social is fundamentally peer-to-peer between two parties. The employment seam involves a layered participant model with eight identity classes — primary parties, employer roles, client-party roles, professional representatives, institutional actors, witnesses, worker-adjacent individuals, and agent-class participants (non-human actors under revocable, human-issued capability grants) — each with role-conditioned access to a structured record, or, for agent-class participants, capability-scoped access checked at invocation.
4. **The legal substrate is part of the architecture.** The bundle is not just data. It is data plus a signed legal record. The prior patterns can be implemented without a legal substrate. This one cannot.
5. **Accessibility and equity are architectural concerns, not policy overlays.** The contemporaneity and tamper-evidence properties are what give the record evidentiary value in discrimination claims, ADA cases, ADEA cases, Title VII cases, and classification disputes. A pattern designed for the most demanding regulatory regime — EU AI Act labor implications, multi-jurisdictional immigration timelines, US anti-discrimination enforcement, contractor-classification ABC tests, EU Platform Work Directive presumptions — is not over-engineered. It is designed to be useful when it matters most.
6. **The synthesis claim emerges here.** The employment seam is the entry where the four-layer Seam Stack — substrate, governance, boundary, evidence — becomes architecturally necessary rather than incidental. Prior entries demonstrate aspects of it; this one requires all of it.

The employment seam is the first Pattern Commons entry that exists as a specification rather than a demonstrated prototype. That is a deliberate choice. The pattern should be readable, defensible, and adoptable as an architectural reference regardless of whether the reference implementation is built.

---

## Bundle Schema

The bundle schema specifies the canonical structure of a handoff bundle. The schema is expressed using the TCF tier vocabulary (Particles, Clusters, Zones, Structure) at the conceptual level, and using SHACL shapes over RDF at the implementation level, with JSON-LD as the canonical serialization for delivery.

v0.4 extends the v0.3 schema in three places: at the Zone level (additions to Zones 1, 2, and 5), at the bundle level (cross-cutting clusters that operate across the whole Structure rather than within a single Zone), and at the per-Particle level (attributes that attach to any Particle regardless of which Cluster it belongs to). The TCF tier vocabulary handles all three cleanly: Zone-level additions are new Clusters within existing Zones; bundle-level additions are Clusters at the Structure level; per-Particle additions are Taxonomy attributes carried by every Particle. Where v0.4 work adds resources that are not Particles (the standalone `seam:WeingartenEvent`, recordable in the worker's Pod independent of any seam firing), the spec is explicit that they sit outside the bundle structure and are referenced in by hash where relevant.

v0.5 extends the schema in one place: agent-class participation. Class G is added to the participant controlled vocabulary (`seam:identityClass: Agent`); three terms are added (`seam:agentCapabilityGrant`, `seam:agentRevocationState`, `seam:gateCheckRecord`); the grantee-only authority constraint is expressed as a SHACL shape; and the gate/evidence pair for agent-class participation is formalized (specified below, after the AI-provenance section). No v0.4.1 term is modified or renamed.

Each addition below is annotated with the secondary question (Q1–Q6) it resolves, for readers tracing the v0.3-to-v0.4 changes. Future readers do not need this annotation — the schema's organization is by structure (Zone, bundle level, per-Particle) rather than by question history.

### TCF tier mapping

The bundle is one **Structure** — the full handoff record for a single seam-firing event. The Structure contains five **Zones**, each a context container organized around a participant role's purpose. Zones contain **Clusters** (semantic objects) which contain **Particles** (the smallest indivisible governed units).

**Zone 1: The Identity Zone.** Who the parties are.

- *Cluster: Worker identity* — DID, WebID, legal name, employment relationship type (W-2 / 1099 / contractor / visa-status).
- *Cluster: Employer identity* — legal entity, EIN/equivalent, jurisdiction, employer-sponsored visa status if applicable.
- *Cluster: Witnessing parties* — union representative, legal counsel for either side, any other party present at the seam-firing — each with their own DID/credential.
- *Cluster: Pod provider context* (`seam:podProviderContext`) — references the worker's Pod provider's attestation by hash. Records the provider's commitment to six minimum requirements: standards conformance (Solid spec compliance, signed by the provider), worker-controlled keys (the worker holds the signing keys; the provider does not), export and migration (the provider supports cryptographic-continuity migration to another provider), notice obligations (the provider commits to notifying the worker of policy changes, breaches, and shutdown intent within bounded windows), no silent retention (the provider commits to deleting worker data on request, with cryptographic verification of deletion where possible), and liability disclosure (the provider's terms specify what the provider is liable for when the substrate fails). These commitments are recorded as a Verifiable Credential issued by the provider; the bundle references the VC by hash. *Q-source: Q4.*
- *Cluster: Credential context* (`seam:credentialContext`) — for every signing party in the bundle, a credential-context record that captures the credential's issuer, regime (eIDAS / NIST 800-63 / DIATF / eduGAIN / etc.), native assurance level (the regime's own term — "substantial," "high," IAL2/IAL3, etc.), the canonical 1–5 assurance level (per the Seam Stack canonical scale at `seamstack.org/vocab/assurance/`), the jurisdiction the credential was issued under, and the credential's issuance date. The canonical scale is provided as a useful fiction (per Principle 3); the underlying regime material supports adjudication. *Q-source: Q5.*

**Zone 2: The Relationship Zone.** What the relationship was.

- *Cluster: Employment terms* — role, start date, classification, compensation structure at a level the worker chooses to disclose, location, jurisdiction.
- *Cluster: Transition trigger* — resignation / layoff / termination for cause / contract end / project handoff / stage transition / re-engagement — with the trigger party named: worker-initiated, employer-initiated, mutual, third-party-initiated.
- *Cluster: Separation cause* — worker-submitted account, employer-submitted account, escrow log of what was actually said when. Three views preserved separately in contested cases.
- *Cluster: Relationship structure* (`seam:RelationshipStructure`) — the new contractor-and-vendor cluster. Records primary employer DID, operational counterparty DID (the entity directing the work, distinct from the primary employer in B2B contractor arrangements), relationship type (employee / independent contractor / dependent contractor / vendor / agency-placed worker / other-with-explanation), classification basis (governing law, jurisdiction), and *classification attestation* organized in three tiers:
    - **Tier 1: Declared classification.** Each party's declared classification of the relationship. Mandatory; bundle cannot complete without it. Recorded as separately-signed Particles by each party.
    - **Tier 2: Controlling test acknowledgment.** Each party's acknowledgment of which controlling test applies in the relevant jurisdiction (FLSA economic-realities test, state ABC test, IRS 20-factor test, EU Platform Work Directive presumption, etc.). Mandatory. Acknowledgment is not agreement on outcome — parties may acknowledge the same controlling test and still disagree on its application.
    - **Tier 3: Indicia.** Per-indicium attestations the relevant test treats as probative — degree of control, integration into the business, opportunity for profit or loss, investment in equipment, permanency, skill required, manner of payment, and so on. Opt-in per Particle (per Principle 1). Each party attests to indicia independently; asymmetric attestation is recorded faithfully as multi-perspective per the schema's `seam:MultiPerspectiveAccount` mechanism.
    
    Visibility scope follows the regulatory-floor pattern: state agencies and courts always see the full classification attestation; future employers never see it without explicit per-disclosure consent from the worker. *Q-source: Q1.*
- *Cluster: MSA / SOW reference* — for contractor and vendor cases, references to the master service agreement and the relevant statement of work by content hash. The agreements themselves are not embedded in the bundle (they may be confidential to one or both parties); only their hashes are recorded, allowing later verification that the parties were operating under the agreements they claim. *Q-source: Q1.*
- *Cluster: Collective bargaining context* (`seam:CollectiveBargainingContext`) — for CBA-governed workplaces, records the CBA reference by hash, the bargaining unit identifier, the union's organizational DID, the jurisdictional scope of the CBA, and a Weingarten rights acknowledgment indicating whether the worker invoked Weingarten representation in any investigatory interaction within the seam window. *Q-source: Q3.*
- *Cluster: Seam-firing context* (`seam:SeamFiringContext`) — for re-engagement seams, records the prior bundle reference (by content hash and IRI), the prior bundle's verification status (verified / unverifiable — see *prior-bundle-unverifiable* failure state), and an employer-continuity classification (same legal entity / successor entity / materially changed entity). For materially-changed-employer cases, the new entity gets a different DID; automatic role-identifier match from the prior bundle fails; the worker must opt in to expanded successor-attribution. This is the cryptographic protection that prevents a successor entity from inheriting employee-side commitments without the worker's explicit re-engagement consent. *Q-source: Q2.*
- *Cluster: Re-engagement posture* (`seam:reEngagementPosture`) — for re-engagement sub-cases involving prior contested separations. Recorded value: `LeaveAsRecorded` (the prior contest stands, both parties acknowledge re-engagement does not resolve it), `JointResolution` (the parties record a joint resolution of the prior contest as part of the new seam), `WorkerWaiver` (the worker waives the prior contest as a condition of re-engagement), or `Unresolved` (the parties did not address the prior contest in this seam). *Q-source: Q2.*

**Zone 3: The Knowledge Zone.** What's being handed off.

- *Cluster: Project handoffs* — project name, status, key contacts, decisions, in-flight work. One Cluster per active project.
- *Cluster: Stakeholder relationships* — people the worker had operational relationships with (internal and external), with the worker's framing of each relationship's status.
- *Cluster: Artifacts* — documents, code, designs, communications. References to artifacts the worker produced, with provenance and access status.
- *Cluster: Tacit knowledge* — things the worker knew that aren't in any document, recorded as the worker's own framing, not extracted.

**Zone 4: The Account-Timeline Zone.** What systems were locked when.

- *Cluster: Account access events* — lockout/restoration timestamps, authorizing party (potentially multiple parties in contractor cases — the operational counterparty, the worker's primary employer, or both), system affected, authorization basis.
- *Cluster: IT log* — the locking party's IT system's log of access events, contributed by IT directly. In layered-employer cases, multiple IT logs may be contributed (one per locking party); each is signed by its respective party's IT role and the bundle records which party controls which system.

This Zone is the load-bearing one in the *account pre-empted* failure state. Both parties contribute; both copies must agree on the timestamps; divergence is the evidence of dispute. The temporal-precedence cryptographic argument — that the lockout signature with its RFC 3161 timestamp can be proven to precede the worker's pre-lockout substrate signature — operates at the IT log level regardless of which party fired the lockout.

**Zone 5: The Legal Record Zone.** What the bundle attests to.

- *Cluster: Seam-firing attestation* — timestamp, parties present, parties absent, mode of seam-firing.
- *Cluster: Bilateral signatures* — worker's signature, employer's signature, witnessing-party signatures, each with key material and timestamp.
- *Cluster: Tamper-evidence envelope* — hash of canonical Structure, RFC 3161 timestamps, OpenTimestamps proof, signature scheme metadata.
- *Cluster: Regulatory declarations* — `seam:regulatoryRegimeFlags` indicating which regulatory regimes apply (EU AI Act / Title VII / ADA / ADEA / immigration / UI / COBRA / professional licensing / GDPR / CCPA / SOX / Dodd-Frank / EU Whistleblower Directive / state-level protected-disclosure statutes / FLSA / state ABC tests / EU Platform Work Directive / NLRA / WARN / European Works Council Directive / Collective Redundancies Directive / eIDAS 2.0 / DIATF), and AI-provenance attestations for any AI-assisted components.
- *Cluster: Grievance procedure* (`seam:GrievanceProcedure`) — for CBA-governed seams where a grievance has been filed before, during, or as part of the seam firing. Records filing status, deadlines (per the CBA's procedural windows), filing party (worker, union, employer-side), current step in the grievance process (informal resolution / first step / second step / arbitration demand / arbitration outcome), and an arbitration outcome reference appended post-hoc via cryptographic linkage when the grievance reaches arbitration. The post-hoc append is itself signed and timestamped; the original bundle is not modified, but a linked supplementary record extends it. *Q-source: Q3.*

### Bundle-level Clusters (cross-cutting)

The following Clusters operate at the Structure level — they describe properties of the bundle as a whole rather than properties of any specific Zone. The TCF tier vocabulary handles this cleanly: the Structure itself is a context container, and bundle-level Clusters are direct children of the Structure rather than children of a Zone.

- *Cluster: Mass-event context* (`seam:massEventContext`) — for seams firing as part of a declared mass event. Records event identifier (a stable reference shared across all seams in the event), scope (number and class of affected workers), trigger (WARN-Act-qualifying layoff / acquisition-driven separation / bankruptcy-driven layoff / European Works Council consultation / other-with-explanation), notice date (the regulatory-required notice date, distinct from the seam-firing date), and legal regime (WARN / state mini-WARN / European Works Council Directive / Collective Redundancies Directive / etc.). When this Cluster is set, the escrow window in Phase 7 of the ceremony extends from 72 hours to 168 hours; the rest of the ceremony is unchanged. *Q-source: Q6.*

- *Cluster: Contribution mode* (`seam:contributionMode`) — applies to employer-side contributions only, with values: `per-seam` (contribution is assembled and signed for this individual seam), `batched` (contribution is assembled across multiple seams in a declared mass event and signed once with the seam's hash linked to the batch), or `delegated` (contribution is assembled by a party other than the named employer, e.g., an outsourced HR services firm, with delegation chain recorded). The architectural commitment surfaces here: worker-side review is *not* batchable. Even when employer-side contribution is `batched` or `delegated`, the worker side of each seam fires independently with the worker's own review window. This is Principle 5 made structural. *Q-source: Q6.*

- *Cluster: Relay capacity disclosure* (`seam:relayCapacityDisclosure`) — referenced VC. The platform attests to its operational capacity at the time of the seam firing — escrow size, throughput, the specific platform instance's identity, any degraded-mode declarations active during the seam window. This protects against the platform claiming, after the fact, that operational constraints prevented compliance with the ceremony when the contemporaneous record would show otherwise. *Q-source: Q6.*

- *Cluster: Witnessing posture* (`seam:WitnessingPosture`) — the temporal posture of any witnessing-party contributions. Values: `contemporaneous` (the witness's contribution was made at seam-firing time), `async-within-window` (the witness's contribution was made within the escrow window, after seam-firing but before bundle delivery), `post-hoc` (the witness's contribution is appended to the bundle after delivery via supplementary linked record, with the post-hoc nature recorded explicitly). *Q-source: Q6.*

- *Cluster: Class-action aggregation consent* (`seam:classActionAggregationConsent`) — an independent consent layer, separate from the worker's general consent to the bundle's existence. Each worker-party retains the choice to decline aggregation for class-action discovery purposes even when other affected workers in the same mass event consent. Default is null (no consent recorded — neither given nor declined); explicit consent or explicit decline is recorded with its own signature and timestamp. *Q-source: Q6.*

- *Cluster: Trust-list reference* (`seam:trustListReference`) — for cross-border seams where parties operate under different identity regimes, a snapshot reference to the relevant trust lists at signing time. The bundle records the trust list identifier (e.g., the EU LOTL — List of Trusted Lists; the UK DIATF certified-providers list; etc.), the snapshot hash, and the timestamp of the snapshot. This makes the trust state at signing time auditable years later, even after the trust lists have evolved. *Q-source: Q5.*

- *Cluster: Legal recognition declaration* (`seam:legalRecognitionDeclaration`) — at bundle level, each party's declaration of which jurisdiction's legal-recognition regime they expect to govern enforcement of the bundle. This is a declaration, not a determination — actual jurisdiction in any later proceeding is decided by that proceeding, not by the bundle. The declaration captures the parties' contemporaneous expectation, which is itself evidence in jurisdictional disputes. *Q-source: Q5.*

### Per-Particle Taxonomy attributes

Every Particle in the schema carries a Taxonomy attribute set. v0.3 defined four such attributes; v0.4 adds two:

```
seam:participantVisibility   — set of role identifiers entitled to see this Particle
seam:regulatoryRelevance      — which regulatory regimes this Particle is evidence for
seam:evidentiaryStatus        — uncontested / contested / escrow-only / signed-bilateral
seam:consentScope             — who has consented to what disclosure of this Particle
seam:carriedForward           — for re-engagement seams: full / summary-only / reference-only / excluded  [v0.4, Q2]
```

Plus the credential-context Cluster's components, which attach at the per-Particle level for any Particle signed by a party:

```
seam:credentialContext        — for every Particle signed by a party, the credential context of that party's signing credential at the moment of signing  [v0.4, Q5]
```

The `seam:carriedForward` attribute, set on Particles in re-engagement seams, indicates how each Particle from the prior bundle is treated in the new seam:

- `full` — the Particle is included in full, with cryptographic reference to its prior signature (the prior signature is preserved; a new signature does not overwrite it).
- `summary-only` — the Particle is replaced with a summary, with reference to the full prior version. Useful for tacit-knowledge Clusters where the worker's framing has evolved.
- `reference-only` — the Particle is referenced by hash but not included in the new bundle. The prior bundle contains it; the new bundle merely points to it.
- `excluded` — the Particle from the prior bundle is explicitly excluded from the new seam. The exclusion is recorded; the prior version remains in the prior bundle.

Per Principle 1, the carry-forward decision is per Particle, not per Cluster or per Zone. A worker re-engaging with a former employer can carry forward project-context Particles in full while excluding tacit-knowledge Particles entirely.

### Standalone resource: `seam:WeingartenEvent`

Some events recordable in the worker's substrate are not seams. The `seam:WeingartenEvent` resource is the v0.4 example: when a worker invokes their Weingarten right to representation in an investigatory interview, that invocation can be recorded in the worker's Pod with the worker's signature, the union representative's signature (if a representative was made available) or a record of refusal (if the employer declined representation), and a contemporaneous timestamp. The resource sits outside any specific seam's bundle. If a seam later fires (the investigatory interview leads to discipline or termination), the bundle's `seam:CollectiveBargainingContext` cluster references the prior `seam:WeingartenEvent` by content hash, and the Weingarten event becomes part of the evidentiary trail. If no seam fires (the interview concludes without discipline), the Weingarten event remains in the worker's Pod as a standing record.

This pattern — substrate-recordable events that may or may not become seam evidence later — generalizes. v0.4 names only the Weingarten case; future versions may name others. *Q-source: Q3.*

### Schema language

The schema is expressed in three layered forms, each serving a different reader:

1. **Master authority — SHACL shapes over RDF, organized by Solid Shape Trees.** Every Particle, Cluster, Zone, and the Structure is defined as an RDF resource with a SHACL shape. The bundle on the worker's Solid Pod conforms to these shapes. Role-conditioned views are SHACL shapes that select subgraphs.

2. **Delivery serialization — JSON-LD with a documented context.** When the bundle is delivered, it is serialized to JSON-LD using the published context. Same graph, no information loss. JSON-LD is also valid JSON, so non-RDF-aware receiving systems can parse it as JSON.

3. **Fallback validation — JSON Schema.** Published alongside the JSON-LD context for systems that cannot process JSON-LD semantics. Provides structural validation without requiring an RDF stack.

### Vocabulary

The schema draws on existing standards where they exist:

- **schema.org** — for general entities (Person, Organization, Role, Place, etc.)
- **FOAF (Friend of a Friend)** — for identity and relationship properties
- **Dublin Core** — for provenance, dates, and metadata
- **W3C Verifiable Credentials Data Model 2.0** — for signature envelopes

A new RDF vocabulary at `https://seamstack.org/vocab/employment-seam/0.5#` defines the terms specific to this pattern: `seam:Seam`, `seam:SeamFiring`, `seam:AccountTimelineEvent`, `seam:BilateralSignature`, `seam:MultiPerspectiveAccount`, `seam:workerSubmittedAccount`, `seam:employerSideAccount`, `seam:escrowLog`, `seam:SeparationCause`, `seam:RelationshipStructure`, `seam:CollectiveBargainingContext`, `seam:GrievanceProcedure`, `seam:SeamFiringContext`, `seam:WeingartenEvent`, `seam:participantVisibility`, `seam:identityClass`, `seam:regulatoryRelevance`, `seam:evidentiaryStatus`, `seam:consentScope`, `seam:aiProvenance`, `seam:regulatoryRegimeFlags`, `seam:credentialContext`, `seam:trustListReference`, `seam:legalRecognitionDeclaration`, `seam:massEventContext`, `seam:contributionMode`, `seam:relayCapacityDisclosure`, `seam:WitnessingPosture`, `seam:classActionAggregationConsent`, `seam:carriedForward`, `seam:reEngagementPosture`, `seam:podProviderContext`, `seam:agentCapabilityGrant` [v0.5], `seam:agentRevocationState` [v0.5], `seam:gateCheckRecord` [v0.5], and the controlled vocabularies for participant roles, identity classes (including `seam:identityClass: Agent` [v0.5]), and regulatory regimes.

A separately-published canonical assurance scale at `https://seamstack.org/vocab/assurance/` defines the 1–5 levels referenced by `seam:credentialContext`, with explicit update policy. Both vocabularies must resolve and be maintained across versions; this is a real maintenance commitment, named explicitly in the open questions section below.

### Role-conditioned access at the schema level

Every Particle in the schema carries a Taxonomy attribute set:

```
seam:participantVisibility  — set of role identifiers entitled to see this Particle
seam:regulatoryRelevance    — which regulatory regimes this Particle is evidence for
seam:evidentiaryStatus       — uncontested / contested / escrow-only / signed-bilateral
seam:consentScope            — who has consented to what disclosure of this Particle
seam:carriedForward          — for re-engagement seams (see above)
```

Role-conditioned views are SHACL shapes that select Particles where `seam:participantVisibility` includes the requesting role. The role identifiers are drawn from the controlled vocabulary defined in the seam vocab and correspond to the human identity classes and their sub-classes:

- `seam:Worker_AsEmploymentParty`, `seam:Worker_AsCitizen`, `seam:Worker_AsDataSubject`, `seam:Worker_AsNaturalPerson`, `seam:Worker_AsRepresentative`, `seam:Worker_AsEstate` (Class A sub-classes)
- `seam:HRRole`, `seam:DirectManagerRole`, `seam:ITRole`, `seam:LegalRole_EmployerSide`, `seam:BargainingUnitLiaison_EmployerSide` (Class B)
- `seam:EngagementManager`, `seam:VMOContact`, `seam:ITRole_ClientSide`, `seam:LegalRole_ClientSide` (Class B′) [v0.4]
- `seam:LegalRole_WorkerSide`, `seam:ImmigrationCounsel`, `seam:TaxPreparer`, `seam:BenefitsAdministrator` (Class C)
- `seam:UnionRepresentative_Steward`, `seam:UnionRepresentative_BusinessRep`, `seam:UnionRepresentative_Counsel`, `seam:UnionRepresentative_Investigator` (Class D, union sub-classes — refined in v0.4)
- `seam:DeferredParty_StateAgency`, `seam:DeferredParty_Court`, `seam:DeferredParty_FutureEmployer` (Class D, other)
- `seam:WitnessingParty_SelfAsserted` (Class E)
- `seam:Dependent`, `seam:EstateBeneficiary`, `seam:EmergencyContact` (Class F)

Class G agent-class participants carry `seam:identityClass: Agent` in the participant model but hold no `seam:participantVisibility` role identifier [v0.5]: agent-class participants are grantees, not record audiences. What an agent may read or act on is defined by the scope of its `seam:agentCapabilityGrant` and checked at invocation by `assertCapabilityCurrent()`; the access log (`seam:gateCheckRecord`), not a role-conditioned view, is the agent's record surface.

Each Particle is tagged at authoring time with the set of roles entitled to see it. A worker's tacit-knowledge Cluster might be tagged `{seam:Worker_AsEmploymentParty, seam:LegalRole_WorkerSide}` only — the employer never sees it; future employers never see it; the operational counterparty never sees it. The seam-firing timestamp is tagged with all roles — everyone sees it. The IT log is tagged for both legal roles and the court because account-pre-empted failure makes it bilaterally relevant. In contractor cases, classification attestations are tagged for state agencies and courts (always) and for future employers (never, without explicit per-disclosure consent), per the regulatory-floor pattern named in the relationship-structure cluster discussion.

This makes role-based access a query, not a permission. A party requesting a view of the bundle gets back the SHACL-validated subgraph where their role identifier is in `seam:participantVisibility`. The platform enforces this at the schema level. There is no "hide this field at the application layer" vulnerability because the application layer never sees Particles outside its role's visibility set.

### AI-provenance — the Intelligence Layer made concrete

Every Particle carries an optional Intelligence Layer attribute set per the TCF's Intelligence Layer governance dimension:

```
seam:aiProvenance
  ├─ seam:aiAssisted          — boolean
  ├─ seam:aiModel              — model identifier (e.g., "claude-opus-4-7")
  ├─ seam:aiInputs             — references to the inputs the model received
  ├─ seam:humanReviewStatus   — none / reviewed / accepted / modified
  ├─ seam:reviewerIdentity    — DID/WebID of the human reviewer (if any)
  └─ seam:reviewTimestamp     — RFC 3161-stamped timestamp of human review
```

If `seam:aiAssisted` is true and `seam:humanReviewStatus` is `none`, the Particle is flagged at the schema level as ungoverned-AI-output. EEOC investigators, EU AI Act auditors, and the worker's legal counsel can all query the bundle for AI-assisted-but-unreviewed Particles — that query is part of their role-conditioned views, not a feature bolted on. This is what makes the spec architecturally aligned with the EU AI Act's labor provisions rather than merely compatible with them.

### Agent-class participation: grant, gate, evidence, and revocation [v0.5]

The `keyhive-employment-seam` prototype's Counter-Passed resolutions established `assertCapabilityCurrent()` and `seam:aiProvenance` as an adjacent gate/evidence pair. v0.5 formalizes that relationship at the spec level, together with the grant and revocation properties Class G requires.

**`seam:agentCapabilityGrant` — the grant (Governance layer).** Records the capability grant authorizing an agent-class participant. Minimum fields: granting-party DID, granted agent DID, capability name, grant timestamp, scope, and scoping-party signature. When the granting party is a Class C representative, one additional field is required: a reference to the grantor's own worker-issued authorization VC (the matter-scoped authorization the Class C ceremony already requires). This is the chain-of-authority condition: legal-responsibility resolution runs entirely in-record — `seam:gateCheckRecord` → grant reference → Class C DID (a juridical person with professional liability) → authorization VC → worker — with no external lookup. The grant records that its capability scope sits within the authorization VC's scope; per Principle 4, the spec records the claimed containment rather than certifying it — SHACL validates the *presence* of the authorization reference, and whether scope was actually exceeded is adjudicated in the forum, with the chain as evidence. The full grant schema (scoping mechanism, expiry, refresh, audit-key references) is named as implementation-facing open work below.

**`assertCapabilityCurrent()` — the gate (Governance/Boundary layers).** A runtime authorization gate that answers: "Is this agent-class participant currently permitted to perform this action?" It is checked at every invocation. It does not read `seam:aiProvenance`. It does not depend on what any prior action's provenance record says. Gate results are: `pass`, `blocked-revoked`, `blocked-unconfirmed`.

**`seam:aiProvenance` — the evidence (Evidence layer).** A descriptive record of what an AI model did and whether a human reviewed it, per the attribute set above. It carries no grant/revoke/authorization semantics. It is not informed by the gate's result. It is populated by the operating party (or the agent, under the operating party's authority) at the time an AI-assisted action is performed.

**`seam:gateCheckRecord` — gate-check events as first-class evidence-layer material.** Every `assertCapabilityCurrent()` invocation — pass or block — writes an access log entry. That entry belongs in the same evidentiary shape as `seam:aiProvenance`: a descriptive record of what the governance layer did, not an extension of the governance layer's authorization logic. The `seam:gateCheckRecord` resource type carries, as required fields: agent DID, grant reference (granting-party DID or grant identifier), capability name, invocation timestamp, and gate result (`pass` / `blocked-revoked` / `blocked-unconfirmed`); blocked invocations additionally carry a reference to the revocation state that triggered the block. The grant reference is required so that the responsible legal party is resolvable from the record itself, without external DID-document lookup — attribution to the agent is operational; legal responsibility rests with the granting party (per Principle 6). This makes the gate's behavior auditable under the same Evidence-layer framework that `seam:aiProvenance` uses, without either field set depending on the other. The access-log gate-check record is a first-class evidence artifact for agent-class participants, parallel to `seam:aiProvenance` for AI-generated content.

**`seam:agentRevocationState` — revocation (Governance layer).** The two-state revocation lifecycle for agent-class participants: `revoked-local` (revocation fired by the granting party; confirmation propagating) → `revoked-confirmed` (revocation signal received and confirmed). Both states are logged under the agent's identity, and the gate blocks in either state — `blocked-unconfirmed` while confirmation is propagating, `blocked-revoked` once confirmed. The gate fails closed: an agent whose revocation is issued but not yet confirmed is blocked, not permitted pending confirmation.

**The grantee-only SHACL shape.** The Class G authority prohibition is expressed as a SHACL shape that fails validation for any bundle in which an agent-class participant's contribution appears at an authorship surface: the worker-submitted or employer-side accounts (the Zone 2 separation-cause cluster and the contested `seam:MultiPerspectiveAccount` structures) or the Zone 5 legal-record signatures. A conforming implementation has no code path by which an agent-class participant attests, contributes an account, or signs; the shape makes that a validation failure, not a policy.

### Multi-perspective in contested cases

The hardest part of the schema design is the multi-perspective record. Most schemas assume a single authoritative version of each fact. The employment seam requires that contested facts preserve each party's account separately, never collapsed.

In the schema:

- A Particle whose `seam:evidentiaryStatus` is `seam:Uncontested` has a single value.
- A Particle whose `seam:evidentiaryStatus` is `seam:Contested` is represented as a `seam:MultiPerspectiveAccount` resource with the following required structure:

```
seam:workerSubmittedAccount   — exactly one: the worker's version, with worker's signature
seam:employerSideAccount      — one or more: each employer-side party's version, with that
                                  party's signature and the issuing-entity role-class
                                  identifier (Class B for primary employer, Class B′ for
                                  operational counterparty; in CBA-governed cases, Class D
                                  union representatives may also contribute employer-side
                                  responses to bargaining-unit attestations)
seam:escrowLog                 — exactly one: the platform's log of what was actually
                                  delivered/signed/timestamped, with platform's signature
```

The schema *requires* exactly one workerSubmittedAccount, exactly one escrowLog, and at least one employerSideAccount per contested Particle. Attempts to serialize a `seam:Contested` Particle that violates these cardinalities are SHACL validation failures. This makes the multi-perspective discipline structural, not disciplinary: a bundle that collapses contested facts into a single narrative cannot be produced without violating the schema, and SHACL validators will reject it before delivery.

The worker side carries one account because the worker is one juridical actor across the A1–A6 sub-classes — which sub-class the worker is signing in is recorded by the credential context, not by spawning a separate account per sub-class. A5 worker-designated representatives and A6 estate successors who contribute their own perspectives do so as witnessing-party Clusters in Zone 1, not as additional worker accounts in the contested-Particle structure. The escrow log carries one entry because there is one platform recording one escrow session — even where multiple platforms are conceivable, each seam-firing has one platform-of-record. The employer side is N because layered-employer arrangements (primary employer plus operational counterparty in contractor cases) are a structural fact about the relationship, not a stylistic choice; the schema records who attested to what without forcing distinct entities into a single account.

The escrow log is the load-bearing element here. It is not an opinion about who was right; it is the record of what each party submitted at what time and what was actually exchanged. State agencies and courts get all views (their role-conditioned view includes `seam:Contested` Particles in full); future employers do not (their view excludes `seam:Contested` Particles entirely unless the worker explicitly consents).

The N-party generalization is a v0.4 change. v0.3 capped the structure at three views (worker / employer / escrow log), reflecting v0.3's two-party-plus-platform assumption; v0.4's recognition that contractor cases are first-class rather than a marginal variant requires generalizing to one-worker-plus-N-employer-side-plus-one-escrow-log. v0.3 bundles remain valid v0.3 bundles; v0.4 bundles use the generalized structure.

### Versioning and extensibility

**Versioning.** The employment-seam vocabulary is versioned. v0.5 of this spec corresponds to vocab version 0.5 (adding the Class G agent-class terms — the `seam:identityClass: Agent` controlled-vocabulary value, `seam:agentCapabilityGrant`, `seam:agentRevocationState`, and `seam:gateCheckRecord` — with no v0.4.1 term modified or renamed). The IRI for the vocabulary includes the version: `https://seamstack.org/vocab/employment-seam/0.5#`. Bundles declare which vocabulary version they conform to. Receiving parties can validate against the declared version. Future versions add terms; deprecations are explicit; no silent breakage. v0.5 is backward-compatible with v0.4.1 and, transitively, with v0.3 in the sense that a v0.3 or v0.4.1 bundle remains validly a bundle of its declared version; v0.5 adds terms and does not modify prior terms. (For the v0.4-to-v0.4.1 point-release history — the `seam:employerSubmittedAccount` → `seam:employerSideAccount` rename and cardinality change — see the changelog.)

**Extensibility.** Jurisdictions have local requirements the canonical schema does not anticipate. The schema permits jurisdiction-specific extensions through a `seam:jurisdictionalExtension` property that points to a separately-defined vocabulary (`https://seamstack.org/vocab/extensions/eu-ai-act/`, `https://seamstack.org/vocab/extensions/california/`, etc.). Extensions are namespaced; they cannot conflict with the canonical schema; they can add Particles but not modify existing ones. This lets the spec stay portable across jurisdictions without forking.

---

## Legal Record Format

The legal record format specifies the cryptographic envelope that protects the bundle and makes it evidentiary. The format satisfies four requirements: contemporaneity (provably written when the seam fires), tamper-evidence (bilateral copies that diverge under tampering), legibility to deferred parties without platform mediation, and GDPR/CCPA-compatible retention and deletion.

### The cryptographic stack — three layers

**Layer 1: Signature scheme.**

EdDSA (Ed25519) is the default signature scheme. ECDSA over P-256 is required for any party that signals legacy compatibility need (older HRIS platforms, some immigration agency intake systems). RSA is explicitly excluded — the spec does not require RSA support, and parties that can only verify RSA cannot serve as signing parties under this pattern.

A bundle in delivery form may carry signatures in either Ed25519 or P-256; verifiers must support both.

**Layer 2: Trusted timestamping.**

RFC 3161 Time-Stamp Protocol tokens from at least two independent qualified Time-Stamping Authorities. The recommendation is one US-jurisdiction TSA and one EU-jurisdiction TSA for cross-jurisdictional records, including any bundle subject to EU AI Act provisions or to immigration proceedings touching multiple jurisdictions. Two TSAs because a single TSA is a single point of compromise; if one TSA is later discredited or revoked, the second timestamp survives.

**Layer 3: Long-term tamper-evidence.**

OpenTimestamps proof anchoring the canonical bundle hash to the Bitcoin blockchain. The bundle's canonical hash (SHA-256 over the URDNA2015-canonicalized JSON-LD) is submitted to OpenTimestamps at seam-firing. OpenTimestamps aggregates submissions and publishes a calendar attestation that eventually anchors to the Bitcoin blockchain. The resulting `.ots` proof file is a permanent, externally-verifiable record that the bundle's hash existed at the seam-firing time. Verification requires only the original bundle and the `.ots` file — no platform, no server, no key infrastructure that could be retired.

OpenTimestamps is the only choice that survives the disappearance of every party except the verifier. RFC 3161 timestamps depend on the TSA's signing key remaining valid and the TSA remaining accessible. A platform-maintained chain depends on the platform existing. OpenTimestamps depends only on the Bitcoin blockchain continuing to exist as a public timestamping fabric — a much weaker dependency than any of the alternatives, and the only one that does not require trusting any specific institution.

This choice imports a small amount of cryptocurrency-ecosystem context into a spec that otherwise sits in the W3C/IETF/legal-tech world. OpenTimestamps itself is institutionally clean — it is an open protocol used independently by archival institutions, journalism organizations, and research projects. The spec does not require the platform or the parties to interact with cryptocurrency markets; it requires only that the OpenTimestamps proof be generated and stored. The architectural justification is that no other timestamping fabric currently has Bitcoin's combination of long-running public availability, no single point of institutional control, and broad cryptographic verification tooling. If a successor fabric emerges, the spec can adopt it; for now, Bitcoin via OpenTimestamps is the substrate that satisfies the architectural primitive.

The temporal-precedence property the OpenTimestamps anchor establishes is regime-independent: it holds regardless of which jurisdictional regime governs the parties' identity credentials. This matters in cross-border seams (per Q5 and Principle 3): the bundle's identity-attestation property is regime-conditional — different parties bring different credentials from different regimes — but the bundle's temporal-precedence property is uniform across all of them. A deferred party in any jurisdiction can verify the temporal precedence of the bundle's events without trusting any specific identity regime.

### The signature envelope — Verifiable Credentials and Verifiable Presentations

The signed bundle is wrapped in a **W3C Verifiable Credentials Data Model 2.0** envelope. The structure:

- The bundle itself (the JSON-LD canonical Structure) is the **credential subject** of a Verifiable Credential.
- Each signing party (worker, employer, witnessing parties) produces a **Verifiable Presentation** that contains the credential plus that party's signature. The presentation is the party's signed copy.
- All presentations of the same credential reference the same credential ID, the same content hash, and the same OpenTimestamps proof. Divergence in any of these is the cryptographic evidence of tampering.
- The signing proof type is **Data Integrity Proofs** with the `eddsa-rdfc-2022` cryptosuite (the W3C-recommended cryptosuite for Ed25519 signatures over RDF datasets).

For non-Solid receiving parties who cannot process JSON-LD natively, the same VC is also published as a **VC-JOSE** (JWT-formatted) variant. This is part of the same W3C Recommendation. A receiving party with a basic JWT verifier can validate the signature without RDF tooling. Information content is the same.

The full envelope, in delivery form:

```
DeliveryArtifact (.zip)
├── VerifiableCredential (the bundle as JSON-LD with Data Integrity Proofs)
│   ├── @context: [VC v2, schema.org, seamstack.org/vocab/employment-seam/0.5]
│   ├── credentialSubject: <the canonical bundle Structure>
│   ├── proof: <Ed25519 signature over canonicalized RDF, eddsa-rdfc-2022>
│   └── credentialStatus: <revocation list pointer>
├── VerifiablePresentations (one per signing party)
│   ├── Worker's signed presentation
│   ├── Employer's signed presentation (and operational counterparty's, in Class B′ cases)
│   └── Witnessing-party signed presentations (one per witness)
├── VC-JOSE variants (JWT-formatted for non-RDF receivers)
├── RFC 3161 Timestamp Tokens (two, from independent TSAs)
├── OpenTimestamps Proof (.ots file anchoring the canonical hash)
└── Trust-list snapshot references (when seam:trustListReference is set)
```

This is delivered to each signing party as a single archive. Each party stores their own copy. The platform retains nothing beyond the brief escrow window required to coordinate the bilateral signing.

### Canonicalization

Hashing JSON-LD requires a canonicalization step because the same RDF graph can be expressed in many byte-different JSON-LD documents. The W3C answer is **RDF Dataset Canonicalization (URDNA2015)**, standardized as `RDFC-1.0` in the 2024 W3C Recommendation. The hash is computed over the URDNA2015-canonicalized form. By choosing the W3C-recommended `eddsa-rdfc-2022` cryptosuite, the spec inherits this canonicalization decision rather than making it independently.

### Multi-perspective in the legal record

For uncontested Particles: the bundle is a single VC, signed bilaterally (worker + employer + any witnessing parties).

For contested Particles: the bundle contains a `seam:MultiPerspectiveAccount` resource which is itself a structured object. The worker's submitted account is signed by the worker. Each employer-side party's submitted account is signed by that party (one in W-2 cases; two in contractor cases with a primary employer plus operational counterparty; potentially more in CBA-governed cases where the bargaining unit contributes a separate response to specific employer-side attestations). The escrow log is signed by the platform. The bundle as a whole carries all signatures plus the seam-firing attestation, but the contested fact itself is preserved with its separately-signed views.

A court, EEOC investigator, state UI agency, or labor authority receiving a contested-case bundle gets:

- The worker's signed account (signed by the worker, with that party's key material)
- One or more signed employer-side accounts (each signed by that issuing party, with the role-class identifier — Class B, Class B′, or Class D as applicable — and that party's key material)
- The signed escrow log (signed by the platform, attesting only to what was submitted when, not to who was right)
- A signed seam-firing attestation that all views existed at seam-firing time
- Two RFC 3161 timestamps and an OpenTimestamps proof anchoring the moment

The deferred party sees the disagreement faithfully recorded, with each party's signed account separately. The cryptographic envelope is structurally incapable of collapsing the contested narrative.

### Retention, revocation, and the GDPR/CCPA pathway

**Platform escrow:** ≤72 hours from seam-firing in default mode; ≤168 hours when `seam:massEventContext` is set; configurable downward, never upward. Platform deletes its escrow copy after both parties confirm receipt or after the escrow window closes (whichever is sooner). The platform retains only the cryptographic hash of what it escrowed (not the content) for 7 years to support after-the-fact challenges that the escrow log is authentic.

**Bilateral copies:** retained by each party indefinitely or per their own retention policy. The worker's copy lives in their Solid Pod under their control. The employer's copy lives wherever the employer's records management policy specifies — typically retained for the longest of (a) statutory employment record retention requirements (US: typically 4–7 years for tax/payroll/I-9; longer for ADA/Title VII/ADEA potentially-relevant records; longer still for classification disputes that may surface years after the relationship ended), (b) the employer's litigation hold policy, or (c) the worker's request for retention.

**Deferred-party copies:** state agencies, courts, and other deferred parties retain whatever subset of the bundle they are entitled to under their own retention policies. The bundle does not constrain deferred-party retention; it constrains only what the deferred party is entitled to access.

**Revocation.** The W3C Bitstring Status List specification supports after-the-fact revocation. The platform maintains a status list at a stable URL that allows revocation of issued credentials in cases of fraud, identity compromise, or court order. Revocation does not delete the bundle; it marks it as no-longer-trustable, and any subsequent verification surfaces the revocation.

**GDPR/CCPA deletion.** The worker's right to erasure under GDPR Art. 17 / CCPA §1798.105 applies to the worker's copy of the bundle (which the worker controls in their Pod) and to any platform-retained data. It does *not* override the employer's lawful retention obligations under employment, tax, or anti-discrimination law — these are explicit GDPR exceptions. The deletion pathway:

- *Worker-controlled:* full deletion at any time, no platform involvement required.
- *Platform escrow:* auto-deleted within 72 or 168 hours per declared mode; worker can request immediate deletion.
- *Bilateral employer copy:* subject to employer's retention obligations; deletion request goes through the employer's GDPR/CCPA process; the platform is not involved.
- *Cryptographic hash-only retention (the platform's 7-year transparency record):* out of scope of GDPR/CCPA because it contains no personal data — only a hash.

The pathway is concrete enough to implement and honest about what the architecture cannot do: the worker cannot force the employer to delete the employer's copy of an employment record, because employment law explicitly requires the employer to retain it. The bundle architecture does not change that. What it does is ensure the worker has full control over the worker's copy, and that the platform itself accumulates nothing.

### What the legal record format requires vs. recommends

**Architectural primitives (required, non-substitutable):**

- Bilateral signed copies that diverge under tampering
- An external timestamping authority neither party controls
- A canonicalization algorithm such that the same RDF graph produces the same hash regardless of serialization
- A structurally-enforced multi-perspective record in contested cases
- A documented retention and deletion pathway compatible with GDPR/CCPA

**Recommended technologies (substitutable):**

- W3C Verifiable Credentials Data Model 2.0 with Data Integrity Proofs / `eddsa-rdfc-2022`
- RFC 3161 timestamps from at least two independent qualified TSAs
- OpenTimestamps for long-term tamper-evidence
- URDNA2015 (RDFC-1.0) for canonicalization
- W3C Bitstring Status List for revocation

A future builder could substitute, for example, an EU eIDAS Qualified Electronic Signature substrate for the VC layer, or a different long-term timestamping fabric if one becomes available. The spec recommends what is available now and architecturally aligned; the primitives are what cannot be substituted.

---

## Identity Verification Ceremony

The identity verification ceremony specifies what happens at the seam-firing moment: who does what, when, in what sequence, with what credential infrastructure. The ceremony differs by participant identity class.

### The eight identity classes

**Class A: Individual legal personalities — the worker.**

The worker is one individual, but operates in multiple legal personalities simultaneously, each potentially relevant at different points in the seam-firing ceremony or in deferred-party consultations of the record. All sub-classes share one self-sovereign DID/WebID as the primary identity anchor:

- **A1: Worker.** The role in the employment relation with the named employer. This is the role the seam fires around. Authority: to attest to the employment relation, to contribute the worker's view of separation cause, to control the worker's tacit-knowledge contributions.
- **A2: Citizen.** The legal personality through which the individual relates to state agencies — UI offices, EEOC, immigration agencies, courts. The same DID/WebID can carry citizen-level claims, backed by state-issued credentials in some interactions (USCIS-issued I-94 for immigration matters; SSN/EIN-equivalent attestation for tax-relevant claims; court-issued capacity attestations for guardianship matters). Authority: to invoke rights against state agencies, to file claims with EEOC/UI/etc., to receive deferred-party consultations of the record on behalf of state-mediated rights.
- **A3: Data subject.** The legal personality under data protection law — GDPR, CCPA, equivalent regimes. Data subject rights of access, rectification, erasure, portability, and objection operate independently of the employment relation. Authority: to exercise data subject rights against the platform, against the employer, and against deferred parties that hold copies.
- **A4: Natural person.** The general legal personality — capacity to contract, capacity to sign, capacity to revoke consent. Most ceremonies do not need to distinguish this from A1, but in cases where capacity is in question (a worker signing under impaired capacity, a guardianship case, an estate matter) the natural-person layer becomes load-bearing. Authority: to give or withhold consent, to sign or refuse to sign, to authorize representation.
- **A5: Worker representative (worker-designated).** The individual the worker has authorized to act for them. Distinct from Class C because A5 is a worker-designated representative who may or may not be a credentialed professional — a family member, a friend, a designated agent. Authority: only what the worker has explicitly authorized via a worker-issued VC scoped to the matter at hand. The worker can revoke A5's authority at any time.
- **A6: Estate / successor in interest.** When the worker has died or been declared incompetent, the estate or court-appointed successor inherits some authorities but not others. This is the personality through which a deceased worker's family might claim continuing benefits, contest a separation cause, or pursue post-mortem discrimination claims. Authority: limited to what the relevant law (probate, estate administration, court orders) grants.

**Class B: Employer-issued roles.**

These participants act as agents of the employer. Their identity is established by an employer-issued Verifiable Credential that attests "this individual holds this role at this employer as of this date." The credential is signed by the employer's own DID (typically a dedicated organization DID maintained by the employer's IT or identity team). The participant authenticates by presenting the employer-issued VC plus a signature from their personal key, which the VC binds to the role.

Sub-roles: HR, direct manager, IT, employer-side legal counsel, bargaining-unit liaison.

**Class B′: Client-party roles.**

In contractor and vendor arrangements, these participants act as agents of the operational counterparty rather than the worker's primary employer. Their identity is established by an operational-counterparty-issued Verifiable Credential, signed by the counterparty's organization DID. The credential infrastructure is parallel to Class B but issued by a structurally distinct entity. The participant authenticates by presenting the counterparty-issued VC plus a signature from their personal key.

Sub-roles: engagement manager, vendor-management-office contact, client-side IT, client-side legal counsel.

The structural distinction between B and B′ matters in classification disputes and in account-pre-empted failure cases. A bundle with both Class B and Class B′ contributions reflects a layered employer arrangement; a bundle with only Class B contributions reflects a direct W-2 arrangement. The relationship-structure cluster's classification attestations (Tier 1, Tier 2, Tier 3) are signed by the parties whose classes are present.

**Class C: Third-party-verified professional representatives.**

These participants act on behalf of the worker but are not employed by the worker. Their identity is established by a third-party verifier — a state bar association, a licensing board, a professional credential issuer (CPA board, USCIS-accredited representative registry, etc.). The VC is signed by the credentialing authority. The participant authenticates by presenting the credential plus the worker's authorization (a separate VC issued by the worker scoped to the matter at hand).

Sub-roles: worker-side legal counsel, immigration counsel, tax preparer, benefits administrator.

**Class D: Institutional actors.**

These participants are institutional actors. The institution maintains its own DID and issues credentials to its representatives; for state agencies and courts, the institution operates under government PKI (US federal PIV/CAC; eIDAS Qualified Certificates in the EU; equivalent national infrastructure elsewhere). The participant authenticates by presenting the institutional credential plus, where relevant, a case-specific authorization (a court order, an investigative warrant, the worker's consent for future-employer disclosure).

Union representatives are refined into four operational sub-classes — D1 Steward, D2 Business Representative, D3 Legal Counsel, D4 Investigator — corresponding to standard CBA grievance-procedure roles. Each is credentialed by the union (the local for stewards and investigators; the local or international for business representatives; bar plus union for counsel). The schema records the sub-class so deferred parties can interpret the witnessing posture appropriately.

Other Class D sub-roles: state agency, court, future employer (consent-gated).

**Class E: Self-asserted witnesses.**

Some seam-firings involve a witness who has no formal identity credential — a colleague present at a layoff conversation, a family member at a high-stakes resignation, a friend serving as the worker's chosen witness in a hostile separation. The pattern accommodates this by allowing the witness to sign with a self-asserted WebID at seam-firing and to have their signed account included in the bundle as a witnessing-party Cluster. The witnessing signature carries less evidentiary weight than a credentialed signature, but it carries some — courts and agencies routinely accept witness statements with attestations of identity. The schema makes the credential level explicit (`seam:identityClass: SelfAsserted`) so a deferred party reading the record knows what they are looking at.

**Class F: Worker-adjacent individuals.**

Individuals on the worker side whose interests are affected by the seam but who are not the worker themselves. Each has their own self-sovereign DID. Role-conditioned access is typically narrow and consent-gated by the worker. Sub-classes:

- **F1: Dependent receiving benefits continuation** — COBRA spouses, dependent children, domestic partners on shared health plans.
- **F2: Estate beneficiary distinct from legal successor** — the people who receive from the estate that an A6 successor administers.
- **F3: Emergency contact / notified party** — designated for notification at separation, no consent authority.

**Class G: Agent-class participants.** [v0.5]

These participants are non-human actors — AI models or automated systems — operating under a capability grant issued by a human operating party. Their participation in the employment-seam record is bounded by the Seam Stack's Governance and Boundary layers' grant/revoke/gate machinery.

*Grantor eligibility.* Permitted grantor parties are: the worker (Class A), employer-issued roles (Class B), client-party roles (Class B′), and worker-side professional representatives (Class C). Class C grantor eligibility is subject to two structural conditions:

1. **Chain-of-authority in-record.** A Class C-issued `seam:agentCapabilityGrant` must reference the grantor's own worker-issued authorization VC — the matter-scoped authorization the Class C ceremony already requires. Legal-responsibility resolution then runs entirely in-record: `seam:gateCheckRecord` → grant reference → Class C DID (a juridical person with professional liability) → authorization VC → worker. No external lookup is required, consistent with the design principle of cryptographic reference over platform-side resolution.
2. **Scope containment recorded, not certified.** The grant records that its capability scope sits within the authorization VC's scope. Per Principle 4, the spec records the claimed containment; whether scope was actually exceeded is adjudicated in the forum, with the chain as evidence. SHACL validates the presence of the authorization reference; it does not certify scope subsumption.

Classes D, E, and F are not grantor parties under this version of the spec; extending grantor eligibility further is a future-version question, not resolved here.

*Identity.* The agent holds a DID/keypair under `seam:identityClass: Agent`. The DID is issued by the operating party at the time of capability grant, scoped to the relationship, and revocable at any time. The agent's model identity — the specific AI system version — is recorded in `seam:aiProvenance` fields on every action it touches, alongside any `aiInputs`, `humanReviewStatus`, `reviewerIdentity`, and `reviewTimestamp` that apply. Authority flows from the grant, not the credential: unlike Classes B through D, whose credential chains establish their right to act, the agent's DID establishes only addressability — the identity the gate checks and the log records. The grant is the attestation; the agent's DID is the addressable identity the gate needs. The verification ceremony for agent-class participants is correspondingly lighter than for human classes — no credential chain from an external issuer.

*Authority scope — structurally grantee-only.* An agent-class participant cannot:

- Attest to the employment relation or any fact in the bundle
- Contribute a worker-submitted or employer-side account
- Hold or exercise any Class A sub-role authority (A1–A6)
- Self-declare separation cause
- Submit a separation-cause contest or dispute on behalf of any party
- Sign any legal record component

These are type-system and schema-level constraints, not UI-layer defaults. No code path in a conforming implementation permits an agent-class participant to exercise any of these authorities; the grantee-only SHACL shape (specified in the bundle schema) makes violation a validation failure.

*What an agent-class participant can do:*

- Be granted a named capability by a permitted grantor party
- Act within that capability scope, with each action gated by `assertCapabilityCurrent()` at invocation time
- Appear in the access log under its own identity, with `contactClass: agent` and the capability name recorded per invocation as a `seam:gateCheckRecord`
- Have its capability revoked at any time via seam-fire, with revocation entering the two-state lifecycle (`revoked-local` → `revoked-confirmed`) logged under the agent's identity
- Generate content or actions that, where AI-assisted, carry `seam:aiProvenance` fields — but those fields are attached to the *actions* the agent performs, not to the agent's identity itself

### The eight-phase ceremony

**Phase 0: Preconditions (continuous, not part of the seam itself).**

Before any seam can fire, the worker has a Solid Pod with a WebID and DID. The employer (and the operational counterparty in contractor cases) has an organization DID and credential issuance infrastructure. Both have published their DID documents to a resolvable location. Witnessing parties either have credentials of their own or will sign self-asserted. This is precondition work; if the precondition is not met, the seam cannot fire under the pattern. The pattern's existence assumes a future world in which Solid Pods and organization DIDs are common; in 2026 they are not, and the spec is honest that the precondition is part of the implementation cost.

The Pod provider context (per the bundle schema's `seam:podProviderContext` cluster) is established as part of preconditions. The worker's chosen provider attests to the six minimum requirements — standards conformance, worker-controlled keys, export and migration, notice obligations, no silent retention, liability disclosure — via a provider-issued VC. Migration to a new provider is itself a first-class operation: when a worker moves their Pod from one provider to another, the migration preserves cryptographic continuity (the worker's DID and signing keys persist; the provider's attestation reference updates). The bundle's Pod provider context cluster records the provider in effect at seam-firing.

For agent-class participants (Class G), preconditions are: the operating party holds an active identity anchor appropriate to their class (a Solid Pod and WebID for Class A and Class C grantors; an organization DID for Class B and B′ grantors); the capability grant is signed by the operating party's key and scoped to the specific agent instance (model version, deployment identifier); the agent's DID document is resolvable and references the grant; and, when the grantor is a Class C representative, the grant references the grantor's worker-issued authorization VC per the chain-of-authority condition. [v0.5]

**Phase 1: Seam-firing intent declaration (worker-side or employer-side or operational-counterparty-side).**

Either party can initiate. In contractor cases, the operational counterparty may also initiate. The initiator sends a signed *seam-firing intent* to the platform. The intent is a small Verifiable Credential containing: initiator DID, intended counterparty DID(s), seam type (entry / stage transition / exit / re-engagement), trigger code (resignation / layoff / termination for cause / contract end / project handoff / re-engagement / etc.), declared timestamp, and intended seam-firing time window. For re-engagement seams, the intent also references the prior bundle by content hash; if the prior bundle is unverifiable, the seam enters the *prior-bundle-unverifiable* failure state at this phase.

The platform validates the intent (signature valid, DID resolvable, declared seam type permitted by the platform's terms), assigns a seam-session identifier, and notifies the counterparty (or, in contractor cases, both counterparties).

This is the first contemporaneous record. Even if the counterparty never responds, the intent is timestamped and signed, and the initiator has a cryptographic record of having attempted to fire the seam at this moment. This is load-bearing in the *worker-unavailable*, *handoff-refused*, and *prior-bundle-unverifiable* failure states: the intent exists in the record even when no bilateral signature is achieved.

**Phase 2: Counterparty acknowledgment.**

The counterparty (or each counterparty in contractor cases) receives the notification, validates the intent's signature, resolves the initiator's DID, and either acknowledges, contests, or lets the window expire.

- *Acknowledges:* signs an acknowledgment VC bound to the seam-session identifier, returns to the platform.
- *Contests:* signs a contest VC declaring why (e.g., disputes the trigger code, disputes the timestamp, disputes the existence of the underlying employment relationship, disputes the classification of the relationship). This does not block the seam; it adds the contest to the multi-perspective record and the seam fires anyway with the dispute recorded. Classification contests in contractor cases trigger the *reclassification pending* failure state, which is finalized at Phase 5 rather than at Phase 2.
- *Window expires:* the seam-session enters the *worker-unavailable* or *refused* failure state per the failure taxonomy, and the bundle is finalized with whatever the initiator submitted plus the platform's escrow log of non-response.

**Phase 3: Bundle assembly (worker-side and employer-side, in parallel; plus operational-counterparty-side in contractor cases).**

Each party assembles their contribution to the bundle from their own Solid Pod (or, for the employer / operational counterparty, from their HRIS / IT systems / legal repository). The assembly is governed by the bundle schema: each party's contribution is validated against SHACL shapes before submission. AI-provenance attributes are populated for any AI-assisted Particles. Role-based visibility tags are applied per the schema's controlled vocabulary. The party's `seam:credentialContext` is populated from the credential the party will sign with — issuer, regime, native assurance level, canonical 1–5 assurance level, jurisdiction, issuance date.

The worker's contribution is assembled in the worker's Pod and signed with the worker's key. The employer's contribution is assembled by the assigned HR/IT roles and signed with each role's employer-issued credential plus the role-holder's personal key. In contractor cases, the operational counterparty's contribution is assembled by Class B′ roles and signed with the counterparty's organization credential plus each role-holder's personal key. All contributions are pushed to the platform's escrow under the seam-session identifier.

For re-engagement seams, the worker's contribution applies the `seam:carriedForward` attribute per Particle, indicating whether each prior-bundle Particle is carried forward in full, summarized, referenced, or excluded.

**Phase 4: Witnessing-party contributions.**

Witnessing parties (union representatives in their D1–D4 sub-classes, legal counsel, IT log contributions, self-asserted witnesses) submit their portions to the escrow. Each contribution is signed by the contributing party with the credential class appropriate to their participant type. The IT log specifically — the account-timeline contribution — is contributed by the locking party's IT role (employer's IT in W-2 cases; operational counterparty's IT in contractor cases where the counterparty fired the lockout; potentially both in layered-lockout cases), signed with the employer-issued or counterparty-issued IT credential, and is what makes the *account pre-empted* failure state cryptographically recordable: IT's signed log of lockout timestamps becomes part of the multi-perspective record whether IT intends it to be or not.

Trust-list snapshot references are captured in this phase for cross-border seams, with the trust list identifier, snapshot hash, and snapshot timestamp recorded against each cross-jurisdictional credential.

For declared mass events, employer-side `seam:contributionMode` may be set to `batched` or `delegated` per the bundle schema; the worker-side contribution remains per-seam.

**Phase 5: Bilateral signing of the assembled bundle.**

The platform composes the assembled bundle from all contributions, validates the full bundle against SHACL shapes (schema-level integrity check), generates the canonical RDF graph via URDNA2015, computes the canonical hash, and presents the assembled bundle to all primary parties for signing.

In two-party cases, this is bilateral (worker + employer). In contractor cases with three or more primary parties, signing is N-way: each party reviews their respective role-conditioned view of the assembled bundle and either signs, objects to a specific Particle (forcing the seam into *handoff-disputed* and triggering Phase 5b multi-perspective resolution), or refuses to sign (forcing *handoff-refused*).

Reclassification disputes are handled at Phase 5: the bundle records all parties' classification attestations as multi-perspective Particles; the seam fires successfully with the *reclassification pending* state recorded; adjudication happens in the relevant forum after seam firing.

**Phase 5b: Multi-perspective resolution (only if disputed).**

For any disputed Particle, the platform creates a `seam:MultiPerspectiveAccount` resource per the schema. Each party submits their account, signed. The platform contributes the escrow log of what was actually exchanged when, signed by the platform. All views are preserved separately. Phase 5 then resumes with the disputed Particles converted to MultiPerspectiveAccounts; all parties sign the bundle as a whole with the disputes recorded inside it.

**Phase 6: Cryptographic envelope assembly.**

Once all primary parties have signed (or one has signed and others have refused / let the window expire), the platform performs the final envelope work:

- Computes URDNA2015-canonicalized form of the full bundle including all signatures, MultiPerspectiveAccounts, and trust-list snapshot references.
- Submits the canonical hash to two independent RFC 3161 TSAs (one US-jurisdiction, one EU-jurisdiction).
- Submits the canonical hash to OpenTimestamps for Bitcoin-anchored long-term timestamping.
- Assembles the delivery artifact (`.zip` containing JSON-LD, VC-JOSE variant, RFC 3161 tokens, OpenTimestamps `.ots` proof, per-party Verifiable Presentations, trust-list snapshot references where applicable).
- Computes the per-party deliveries: each party gets the artifact plus their role-conditioned view metadata.

**Phase 7: Delivery and platform exit.**

The platform delivers the per-party artifact to each party's chosen delivery endpoint (the worker's Pod for the worker, the employer's records system for the employer, the operational counterparty's records system in contractor cases, witnessing parties' chosen endpoints). Each delivery is itself signed by the platform and acknowledged by the receiving party with a signed delivery receipt.

After all deliveries are acknowledged (or after the maximum escrow window — 72 hours in default mode, 168 hours when `seam:massEventContext` is set), the platform deletes its escrow copy of the bundle. Only the platform's hash-only transparency log is retained for the 7-year challenge window. The bundle now exists only on the parties' systems.

The platform has performed its irreducible role and exited the relationship. The bundle is durable; the legal record is verifiable; the platform is no longer load-bearing for either party's future use of the record.

### Failure-state handling in the ceremony

Each of the nine failure states maps to a specific exit point in the ceremony:

- **Handoff complete:** Phase 7 succeeds. All signatures, full timestamps, all deliveries acknowledged.
- **Handoff pending:** Phase 5 has not yet completed; bundle is in escrow within the 72h or 168h window. The ceremony has not yet failed.
- **Handoff disputed:** Phase 5b fired; the bundle includes MultiPerspectiveAccounts; Phase 6 completes the envelope with disputes recorded. From the platform's perspective this is a successful completion; from the parties' perspective the dispute persists into whatever forum will adjudicate it.
- **Handoff partial:** Phase 4 or Phase 5 completed for some Clusters but not others (NDA-blocked artifacts excluded, IP claim from operational counterparty blocking certain Particles, IT lockout that prevented full contribution from one party but not another). The bundle records explicitly which Clusters were transferred and which were blocked, with each blocking reason and each blocking party's signature where applicable. Multiple blocking parties are accommodated.
- **Handoff refused:** Phase 2 returned a refusal, or Phase 5 returned a sign-refusal. The bundle is finalized with the refusing party's signed refusal in the escrow log; the non-refusing parties' signed accounts stand alone; the legal record notes the refusal as the failure cause.
- **Worker unavailable:** Phase 2's window expired with no worker response, or the worker explicitly declined to participate. The bundle is finalized with the employer's contribution (and operational counterparty's, in contractor cases) plus the platform's signed escrow log of non-response. No fabrication of the worker's account is permitted; the absence is the record.
- **Account pre-empted:** Phase 4's IT log contribution shows lockout timestamps preceding the worker's Phase 3 assembly window. The worker's pre-lockout substrate (in the worker's Pod) is finalized as the worker's contribution; the locking party's IT log is finalized as that party's account-timeline contribution; the temporal precedence (lockout-before-assembly-window) is preserved cryptographically via RFC 3161 timestamps and the OpenTimestamps proof. The bundle records *which party's* IT lockout fired. The legal record records the lockout as the failure cause, not the worker's failure to contribute.
- **Reclassification pending:** Phase 5 completes with the relationship-structure cluster recording all parties' classification claims and attestations as multi-perspective Particles. From the ceremony's perspective the seam fires successfully; from the parties' perspective the classification dispute persists into the forum that will adjudicate it (state agency, court, EU labor authority).
- **Prior-bundle-unverifiable:** Phase 1's prior-bundle reference fails verification. The ceremony either proceeds without prior-bundle reference (if all parties consent — the unverifiability is recorded as part of the new bundle) or aborts (if any party requires verifiable continuity).

The architectural primitive that distinguishes the *account pre-empted* state from the others is **temporal precedence**: the cryptographic envelope can prove that the IT lockout timestamp preceded the worker's Phase 3 window. This is what makes the worker's pre-lockout substrate evidentially load-bearing rather than a post-hoc claim. The contemporaneity primitive does its hardest work here. The temporal-precedence property is regime-independent (per Principle 3): it holds across jurisdictional regimes regardless of which identity infrastructures the parties operate under.

### Key recovery and credential revocation

**Key recovery for the worker.** The worker's Solid Pod and DID are controlled by the worker's keys. Lost keys are catastrophic in any self-sovereign system. The pattern recommends (but does not require) social recovery via a Shamir-style key-share split among trusted contacts, or pod provider-mediated recovery for hosted Pods. The bundle architecture is robust to key loss after seam-firing: the bundle delivered to the worker is a self-contained artifact that can be verified by anyone using the worker's public key from the time of signing, even if the worker has since lost their private key. Key loss prevents the worker from signing *new* documents; it does not invalidate signatures from before the loss.

This is one of three honest limits the Pod provider question (Q4) surfaces: key loss is catastrophic for new signing; coercion of the provider is not solved by the architecture (a provider compelled by court order or regulatory action to act against the worker's interest is a legal problem outside the architecture's scope); and ecosystem health requires multiple operational models (hosted, self-hosted, institutional, cooperative) — a single dominant Pod provider would itself become an accumulation surface the pattern is designed to avoid.

**Credential revocation for employer-issued, counterparty-issued, and third-party credentials.** Roles change. HR staff leave. Lawyers move firms. Union representatives are replaced. VMO contacts rotate. The W3C Bitstring Status List supports after-the-fact revocation of issued credentials. A bundle signed by an HR role-holder whose credential was later revoked remains verifiable for the time-window during which the credential was valid (the RFC 3161 timestamp anchors the validity), but the revocation is publicly resolvable and a deferred party reading the record sees both the historical signature and the current revocation status. The legal weight depends on the regime — courts generally accept signatures valid at signing time even if later revoked, provided the revocation was not due to fraud — but the spec records both facts and lets the adjudicating body decide.

**Capability revocation for agent-class participants.** [v0.5] An agent's capability is revocable at any time by the granting party, and revocation is itself a recorded operation: it fires as a seam-scoped event and enters the two-state lifecycle recorded in `seam:agentRevocationState` — `revoked-local` (revocation fired by the granting party; confirmation propagating) → `revoked-confirmed` (revocation signal received and confirmed) — with both states logged under the agent's identity. The gate blocks in either state: invocations during propagation are logged as `blocked-unconfirmed` and invocations after confirmation as `blocked-revoked`, each as a `seam:gateCheckRecord` carrying the required grant reference. The gate fails closed — an agent whose revocation is issued but not yet confirmed is blocked, not permitted pending confirmation. Unlike credential revocation for human classes, agent capability revocation carries no signature-validity question backward in time by itself: an agent signs nothing (per the grantee-only constraint), so revocation's evidentiary surface is the gate-check log — which invocations were permitted, which were blocked, and under which revocation state — rather than the trust status of any signed artifact.

### What the ceremony does not include

- **The ceremony does not adjudicate.** Phases 5b and 6 record disputes; they do not resolve them. Resolution happens in the forum the dispute is taken to: court, arbitration, EEOC, state UI hearing, immigration adjudication, classification-determination proceeding, NLRB unfair labor practice charge, EU labor authority.
- **The ceremony does not authenticate beyond the cryptographic level.** A worker who has been coerced into signing under duress signs validly under the cryptographic envelope; the record shows a valid signature. Coercion is a legal challenge to be raised in the forum that adjudicates the underlying dispute, not a property the cryptographic ceremony can detect.
- **The ceremony does not establish identity beyond what the credential issuer attested.** If the employer or operational counterparty issued a credential to someone they should not have, the bundle records what they attested. The credential issuer's attestation is what the deferred party trusts; the ceremony does not second-guess the issuer.
- **The ceremony does not provide non-repudiation against compromised keys.** If a party's private key was compromised at the time of signing, signatures produced with the compromised key are still cryptographically valid. Compromise is a separate evidentiary challenge in the adjudicating forum.
- **The ceremony does not certify the legal recognition of cross-border credentials.** The `seam:legalRecognitionDeclaration` field captures each party's contemporaneous expectation of jurisdictional governance, not a determination of jurisdiction. Actual jurisdiction in any later proceeding is decided by that proceeding. Trust-list snapshots are operationally fragile in some regimes; the spec records the snapshot rather than guaranteeing its durability. Per Principle 3, the spec accommodates regime fragmentation rather than papering over it.

These limitations are inherited from the underlying cryptographic, identity, and jurisdictional standards. The pattern does not claim to solve them; it documents them so that builders and deferred parties understand what the ceremony does and does not establish.

---

## Reference Implementation Sketch

A reference implementation would consist of:

- **Local substrate.** A worker's Solid Pod (hosted or self-hosted) containing the worker's knowledge graph, structured around the worker's projects, contacts, decisions, and artifacts. Reuses the profile-map-as-local-CRM pattern (#3) and the attachArrayObserver pattern (#4) for hydration. The Pod's data is RDF, validated by SHACL shapes organized via Solid Shape Trees, accessed via Web Access Control / Access Control Policy.
- **Pod provider attestation.** Pod provision is treated as a first-class concern of the reference implementation. The provider attests to the six minimum requirements (standards conformance, worker-controlled keys, export and migration, notice obligations, no silent retention, liability disclosure) via a Verifiable Credential issued by the provider. Migration between providers is itself a supported operation, with cryptographic continuity preserved (the worker's DID and signing keys persist; the provider attestation reference updates). The reference implementation's Pod-provider component is most acute for gig-worker and 1099-classified populations, who are simultaneously the population most exposed to classification disputes and the population least served by existing Pod-provider markets; the implementation should prioritize Pod provision suitable for that population.
- **Bundle translator.** A versioned schema (employment-seam vocab v0.5) implemented as SHACL shapes, with translators from the worker's native format(s) to the canonical RDF bundle, and from the bundle to common receiving-party ingestion formats (JSON for HRIS systems, JSON-LD for Solid-aware parties, PDF/A for legal-record purposes, CSV/XML for legacy state-agency intake systems).
- **Identity-verification relay.** A lightweight server that confirms identity across the eight identity classes, holds the bundle in escrow briefly, delivers it on confirmation, and produces a signed legal record. Reuses the relay-exits-after-delivery posture from localfirst.social. Implements the eight-phase ceremony with the v0.4 extensions for cross-border credentials, mass events, and contractor cases, and the v0.5 agent-class grant/gate/revocation machinery (`assertCapabilityCurrent()` enforcement, `seam:gateCheckRecord` logging, two-state revocation).
- **Cryptographic envelope toolchain.** W3C Verifiable Credentials issuer and verifier libraries (`eddsa-rdfc-2022` cryptosuite). RFC 3161 TSA clients for at least two qualified TSAs. OpenTimestamps client. URDNA2015 canonicalization library. W3C Bitstring Status List implementation. Trust-list snapshot capture for cross-border seams.
- **Failure-state UI.** Explicit handling of all nine failure states, with worker-side messaging that does not assign blame to the worker for failure modes the worker did not cause. The *account pre-empted* state remains the load-bearing example; the v0.4 *reclassification pending* and *prior-bundle-unverifiable* states require their own UI treatment.
- **Role-conditioned access layer.** SHACL-shape-based view derivation for each participant type. The worker sees the full bundle in their Pod. Deferred parties see consent-gated slices. Legal and state parties see what the evidentiary record requires. Class B′ contributions are visible to the operational counterparty's role-conditioned view; Class D union sub-classes have differentiated visibility per CBA grievance procedure. Class G agent-class participants hold no view; their capability-scoped access is enforced at the gate.
- **Optional alumni network.** An opt-in, worker-owned graph of past handoffs, surfaced as a discovery and re-engagement layer. The graph lives on the worker's substrate. The platform does not aggregate it. Re-engagement seams (the v0.4 first-class case) reference prior bundles cryptographically, not through platform-side memory.

This is a sketch, not a build plan. The contractor case is plausibly the strongest first reference implementation candidate — the legal stakes are highest, the existing process is thinnest, and the population is structurally underserved. The sketch is now concrete enough that a competent builder could begin implementing against it: the schema is defined, the legal record format is specified, the identity ceremony is sequenced, the failure paths are mapped, the Pod provider conformance requirements are named. The agent-class machinery additionally has a partial existence proof: the `keyhive-employment-seam` prototype implements the capability gate, the `contactClass: agent` contact model, and the two-state revocation lifecycle at prototype scale. Open questions below address tertiary refinements rather than secondary ones.

---

## Open Questions

The three load-bearing technical questions from v0.2 — bundle schema, legal record format, identity verification ceremony — were resolved in v0.3. The six secondary open questions from v0.3 — sub-contractor and vendor cases, return-employee cases, collective bargaining operational depth, Pod provider operational model, cross-border identity reconciliation, mass-event handling — are resolved in v0.4. Brief references to where each closure lives:

- **Sub-contractor and vendor cases (Q1):** §11 (Class B′ in the layered participant model), §12 (`seam:RelationshipStructure` cluster, three-tier classification attestation, MSA/SOW reference), §14 (contractor classification regimes), failure taxonomy (*reclassification pending* state), changelog.
- **Return-employee cases (Q2):** §12 (`seam:SeamFiringContext` cluster, `seam:reEngagementPosture`, `seam:carriedForward` per-Particle attribute), failure taxonomy (*prior-bundle-unverifiable* state), §14 (ADP returnee data anchor).
- **Collective bargaining (Q3):** §11 (Class D refinement into D1–D4 sub-classes), §12 (`seam:CollectiveBargainingContext` cluster, `seam:GrievanceProcedure` cluster, standalone `seam:WeingartenEvent` resource), §14 (collective bargaining regimes).
- **Pod provider operational model (Q4):** §12 (`seam:podProviderContext` cluster, six minimum requirements), §13 (Phase 0 preconditions, key recovery), §16 (reference implementation Pod provision treatment).
- **Cross-border identity reconciliation (Q5):** §12 (`seam:credentialContext`, `seam:trustListReference`, `seam:legalRecognitionDeclaration`), §13 (Phase 3 credential context, Phase 4 trust-list capture), §14 (cross-border identity infrastructure).
- **Mass-event handling (Q6):** §12 (`seam:massEventContext`, `seam:contributionMode`, `seam:relayCapacityDisclosure`, `seam:WitnessingPosture`, `seam:classActionAggregationConsent`), §13 (Phase 7 extended escrow window), §14 (mass-event regimes).

v0.5 resolves the agent-as-governed-party question set carried from the `keyhive-employment-seam` prototype work. Where the closures live:

- **Attribution model (first-class contact vs. credential-bound instrument):** ruled for first-class contact — Class G — with the grantee-only scope as a hard architectural constraint and the grant reference as a required field of every agent-attributed record (layered participant model, Class G ceremony treatment, Principle 6, `seam:gateCheckRecord`). Attribution to the agent is operational; legal responsibility is resolvable in-record to a juridical person.
- **Class C grantor eligibility:** resolved in — worker-side professional representatives are permitted grantor parties under the two chain-of-authority conditions (Class G ceremony treatment; `seam:agentCapabilityGrant` conditional required field). Classes D, E, and F remain non-grantors.
- **Gate/evidence relationship:** `assertCapabilityCurrent()` and `seam:aiProvenance` formalized as an adjacent pair — operational and descriptive respectively, no dependency in either direction — with gate-check events named first-class evidence-layer material via `seam:gateCheckRecord` (bundle schema, agent-class participation section).
- **Principles posture:** resolved — Principle 6 added as the spec's participant-scope commitment, closing the open meta-question v0.4 deferred to this version's authoring session. The principles taxonomy is now: one foundational positive commitment, four constraints, one operative choice, one participant-scope commitment. Whether the shape should grow further remains a judgment for future versions' authoring sessions, under the same discipline: a new principle must have done real work before it is named.

The remaining open questions are tertiary:

- **Provider attestation Verifiable Credential type.** The Pod provider conformance attestation is a Verifiable Credential whose specific schema needs drafting. This is real standards work, not a free externality. Initial draft is implementation-phase work; long-term home is the seamstack.org documentation alongside the assurance scale.
- **Vocabulary maintenance commitment.** The IRIs at `https://seamstack.org/vocab/employment-seam/0.5#` and `https://seamstack.org/vocab/assurance/` must resolve and be maintained across versions. Includes the controlled vocabularies for participant roles (Classes A1–A6, B, B′, C, D sub-classes including D1–D4, E, F1–F3, G), identity classes, regulatory regimes, and the canonical assurance scale. This is durable namespace work, not a free externality, and committing to it is a real maintenance obligation.
- **Reference implementation scope.** Whether a partial proof-of-concept is achievable on the conference timeline, and whether the contractor case is the first implementation target (the spec's hint above), are open implementation decisions. The spec does not lock the choice; the architecture supports either path. A reference implementation may be built, partially built, or not built at all without changing the spec's defensibility as a pattern.
- **`seam:agentCapabilityGrant` full schema.** [v0.5] The fields named in the bundle schema are the minimum required; the full schema (scoping mechanism, expiry, refresh, audit-key references) is implementation-facing work for a future session.
- **Multi-agent chains.** [v0.5] Whether an agent-class participant can itself authorize a sub-agent, and if so what the grant chain's attestation model looks like, is explicitly out of scope in this version. The prototype does not implement it; the spec does not pre-judge it. Principle 6 pre-disciplines the question without pre-deciding it: every link of any future chain must resolve to a juridical person.
- **EU AI Act regime treatment for agent-class participation.** [v0.5] The EU AI Act's transparency and human oversight requirements for high-risk AI systems may impose constraints on agent-class participation in employment-seam records — specifically on `humanReviewStatus` adequacy and `reviewerIdentity` authentication — that a future version should address. This version names the surface but makes no ruling.
- **`seam:agentRevocationState` relationship to the exposure-record surface.** [v0.5] The relationship between the two-state revocation model and the `keyhive-employment-seam` prototype's exposure-record surface is implementation-pending, not spec-settled.

---

## Scope Boundary: Continuous-State and Ping Infrastructure

The session work that produced v0.1 and v0.2 of this spec identified two extensions of the employment seam pattern that are architecturally coherent but deliberately out of scope here: a continuous-state model in which the employment relationship persists at lower intensity across the formal seam (rather than terminating cleanly at the boundary event), and a low-friction signaling layer between former parties modeled on the localfirst.social ping pattern. Both extensions have real architectural merit and real implications for how re-engagement and boomerang cases are handled. They are not in this spec because they change the pattern's center of gravity in ways that deserve their own treatment. Both are addressed in the companion blue-sky essay, *[working title TBD]*, published separately under Systems of Thought.

The `weightsAvailability` sub-attribute, co-registered as a v0.5 candidate alongside the agent-as-governed-party entry, is likewise not in this version: the two candidates are independent, and `weightsAvailability` awaits its own authoring treatment. One interaction point is noted for that future session: `seam:agentCapabilityGrant`'s scope field may benefit from a `weightsAvailability`-aware value when the granted agent is an open-weight model whose weights are independently verifiable — a question this version names but does not establish as a constraint.

---

## How This Sits Relative to the Series

The local-first prototype series has demonstrated the seam argument across four domains: governance monitoring (no seam), commerce (one seam per transaction), healthcare (one seam per intake, higher stakes), and social networking (a seam per connection, distributed).

The employment seam is the first Pattern Commons entry that has not been built. It exists as a specification, derived from a concept brainstorm and four sessions of architectural and technical refinement. That is a deliberate choice. The pattern should be readable, defensible, and useful as an architectural reference regardless of whether any particular implementation follows.

If a reference implementation is built, the contractor case is plausibly the first one to implement, not the W-2 case. The legal stakes are highest in contractor classification disputes, the existing process is thinnest in B2B contractor arrangements, and the population most exposed (gig workers, 1099-classified workers, dependent contractors under emerging EU and state-level presumption regimes) is also the population least served by existing handoff and offboarding tooling. The spec accommodates this by treating Class B′ and the relationship-structure cluster as first-class rather than as W-2 variants; the architecture is ready for the contractor case as the first reference implementation, if a builder takes that path.

The pattern's adoption is asymmetric by design (per Principle 5). The architecture optimizes for worker-side evidentiary protection over employer-side operational convenience when the two are in tension; this makes it more attractive to plaintiff-side firms, worker-side unions, gig-worker advocacy organizations, and labor-side regulators (DOL, state unemployment insurance offices, EEOC, EU labor authorities) first. Employer adoption follows from regulatory pressure rather than from operational convenience. The spec is more useful for naming this asymmetry than for performing a balance the architecture does not deliver — and being explicit about it lets potential adopters on either side make an informed decision about whether the pattern fits what they are trying to do.

Whether the employment seam becomes the fifth prototype in the series, a published specification adopted by another builder, or remains a documented pattern that informs future work is an open question — and an open invitation.

---

## Changelog

**v0.5 (August 8, 2026).** Agent-as-governed-party formalized, applying the Panel Pass-reconciled candidate entry of August 7–8, 2026, plus two rulings made in the v0.5 authoring session. Class G (agent-class participants) added as the eighth identity class: non-human actors under revocable, human-issued capability grants, structurally grantee-only, with the authority prohibition expressed as a SHACL shape rather than a UI-layer default. Grantor surface: Classes A, B, B′, and — per this session's first ruling — Class C, under two structural conditions (chain-of-authority in-record: a Class C-issued grant must reference the grantor's worker-issued authorization VC, making legal-responsibility resolution run entirely in-record to the worker; scope containment recorded, not certified, per Principle 4). Classes D, E, F remain non-grantors. Three vocabulary terms added at the bumped IRI `https://seamstack.org/vocab/employment-seam/0.5#`: `seam:agentCapabilityGrant` (with the grantor's authorization-VC reference as a conditional required field for Class C grantors), `seam:agentRevocationState` (two-state lifecycle: `revoked-local` → `revoked-confirmed`, gate fails closed), and `seam:gateCheckRecord` (required fields: agent DID, grant reference, capability name, invocation timestamp, gate result — the grant reference required so the responsible juridical person is resolvable from the record itself). `seam:identityClass: Agent` added to the controlled vocabulary. The gate/evidence relationship formalized: `assertCapabilityCurrent()` (operational, Governance layer) and `seam:aiProvenance` (descriptive, Evidence layer) are an adjacent pair with no dependency in either direction; gate-check events are first-class evidence-layer material. Per this session's second ruling, Principle 6 added — "Agents are governed parties, never authors of record" — as the spec's participant-scope commitment, closing the principles-posture question v0.4.1 left open; the principles taxonomy is restated as one foundational positive commitment, four constraints, one operative choice, and one participant-scope commitment, and the section is renamed "The Six Design Principles." Phase 0 gains agent preconditions; the ceremony gains the Class G identity treatment (grant-as-attestation, DID-as-addressability, lighter ceremony); key-recovery gains the agent capability-revocation treatment (revocation's evidentiary surface is the gate-check log, since agents sign nothing). Class G is the exception to the role-conditioned view model: agents hold no `seam:participantVisibility` identifier; the grant/gate is their access surface (an authoring-session articulation consistent with, but not stated in, the candidate entry). Two corrections against the candidate entry's draft language are recorded: the grantee-only SHACL shape's authorship surfaces are the Zone 2 separation-cause accounts, the contested `seam:MultiPerspectiveAccount` structures, and the Zone 5 legal-record signatures (the candidate's "Zone 4 worker/employer account" reference was a zone mis-reference — Zone 4 is the Account-Timeline Zone); and the design-principles heading is renumbered for the sixth principle. Provenance: the candidate entry's §2 attribution ruling carries a Panel Pass (August 8, 2026, verdict (b) — sound with the strengthening amendment, stamp retired); the candidate's §§3–5 and this session's two rulings are single-context material adopted by operator declaration and remain un-paneled. Co-registered `weightsAvailability` sub-attribute deliberately not included (independent candidate; one grant-scope interaction point named in the scope boundary for its future session). Carried open items: `seam:agentCapabilityGrant` full schema; multi-agent chains (pre-disciplined, not pre-decided, by Principle 6); EU AI Act regime treatment for agent-class participation; `seam:agentRevocationState` relationship to the prototype's exposure-record surface. v0.5 is backward-compatible with v0.4.1: terms added, none modified or renamed.

**v0.4.1 (May 1, 2026).** Quality-pass tightenings from the v0.4 close-out review, applied without reopening any v0.4 resolution: (1) `seam:employerSubmittedAccount` renamed to `seam:employerSideAccount` with cardinality generalized from exactly-one to one-or-more, resolving the naming asymmetry the N-party generalization introduced (union-contributed responses and operational-counterparty accounts are employer-side, not employer-submitted); the multi-perspective cardinality rationale paragraph added (one worker account because one juridical actor; one escrow log because one platform-of-record; N employer-side accounts because layered-employer arrangements are structural facts). (2) The temporal-precedence property's regime-independence made explicit (legal record format; ceremony failure-state handling), connecting the OpenTimestamps anchor to the cross-border credential heterogeneity Q5 introduced. (3) The design-principles section's Q-derivation annotations trimmed to the changelog; principles stand on their own in the body. (4) The A5/A6 witnessing-role clarification: worker-designated representatives and estate successors contributing their own perspectives do so as witnessing-party Clusters, not as additional worker accounts. No schema semantics changed beyond the rename and cardinality generalization; v0.4 bundles serialize validly as v0.4.1 bundles after applying the term rename.

**v0.4 (April 30 – May 1, 2026).** Six secondary questions resolved: contractor/vendor cases (Class B′, `seam:RelationshipStructure`, three-tier classification attestation, MSA/SOW references, *reclassification pending* failure state); return-employee cases (`seam:SeamFiringContext`, `seam:reEngagementPosture`, `seam:carriedForward`, *prior-bundle-unverifiable* failure state, ADP returnee data); collective bargaining depth (D1–D4 union sub-classes, `seam:CollectiveBargainingContext`, `seam:GrievanceProcedure`, standalone `seam:WeingartenEvent`); Pod provider operational model (`seam:podProviderContext`, six minimum provider requirements, migration as first-class operation); cross-border identity (`seam:credentialContext`, `seam:trustListReference`, `seam:legalRecognitionDeclaration`, canonical 1–5 assurance scale as useful fiction); mass events (`seam:massEventContext`, `seam:contributionMode`, `seam:relayCapacityDisclosure`, `seam:WitnessingPosture`, `seam:classActionAggregationConsent`, 168h escrow extension, worker-side unbatchability). Multi-perspective structure generalized from three-view to one-worker-plus-N-employer-side-plus-one-escrow-log. Failure taxonomy expanded from seven to nine states. Six design principles named (Principle 0 through Principle 5). Case anchors added (Lyft NJ, Uber/Lyft MA, *Manoli*, Amity, Microsoft, FedEx Ground; *Weingarten*, *Troy Grove*; eIDAS 2.0, DIATF, EUDI Wallet milestones; ADP March 2025 returnee data).

**v0.3 (April 30, 2026, PM).** The three load-bearing technical questions resolved: bundle schema (TCF tier mapping, five Zones, SHACL/JSON-LD/JSON Schema layering, role-conditioned access at schema level, AI-provenance attributes); legal record format (Ed25519/P-256, dual RFC 3161 TSAs, OpenTimestamps, VC 2.0 envelope with `eddsa-rdfc-2022`, URDNA2015 canonicalization, retention/revocation/GDPR pathway); identity verification ceremony (seven identity classes, eight-phase ceremony, failure-state mapping, key recovery, credential revocation). Failure taxonomy at seven states. Regulatory durability section expanded.

**v0.2 (April 30, 2026, AM).** Framing session. The Seam Stack named as the four-layer reference architecture (Substrate / Governance / Boundary / Evidence). Platform accountability section added (recorder posture, four architectural conditions, funding neutrality). Layered participant model introduced at seven classes. The pattern positioned as specification-first (the first Pattern Commons entry that exists as a spec rather than a demonstrated prototype).

**v0.1 (April 29, 2026).** Initial spec from the onoff.work concept board and first refinement session. The pattern in one sentence, the problem, the architectural claim, series positioning, minimum server-dependent surface, initial failure taxonomy, format translation, regulatory durability sketch, participant sketch, what the pattern does not solve, seventh-pattern argument, reference implementation sketch, open questions.

---

*This specification was produced through AI-assisted session work governed by the Session Harness discipline: versioned documents, explicit mode declarations, operator-confirmed rulings, compression blocks, and confidence-tagged ledger deltas. Single-context material is identified as such in the changelog; Panel Pass and Counter-Pass provenance is recorded where it exists. The spec practices the provenance discipline it specifies.*

**UX Minds, LLC · J. Wright · August 8, 2026**
