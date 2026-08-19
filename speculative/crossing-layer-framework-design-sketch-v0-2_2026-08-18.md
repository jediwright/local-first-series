# Crossing-Layer Framework — Speculative Design Sketch

⚑ STAMP: SINGLE-CONTEXT — NOT PANELED
Speculative-register sketch. Not verdict-bearing. No claim herein migrates to
publication-track copy, Pattern Commons entries, vocab namespaces, or the
Survival Ledger without a governed Mode 1 pass. The collision check (run and
reconciled 2026-08-18 — see §8) appends verified landscape findings to this
speculative artifact; it does not convert the sketch to a paneled document.
**Publication candidate** for the GitHub speculative post, subject to the
register-explainer README accompanying it in whatever directory hosts it.

**Version:** v0.2 (v0.1 → v0.2 revision, post-collision-check)
**Date:** 2026-08-18
**Register:** CONTEXTUAL
**Mode:** Speculative (blue-sky) — feeds a future Mode 1 design/scoping session
**Ledger:** SL-0123 assigned at the v0.2 revision session close (Mode 1
revision session, 2026-08-18), pending operator tail verification against the
canonical Survival Ledger (expected tail at assignment: SL-0122). Speculative
*content* herein remains non-verdict-bearing; the delta records the revision
event and publication-candidate status, not the sketch's claims.
**Lineage:** Session of 2026-08-18 ("could the Seam Stack extend the frameworks
we're blocked by" → "explore ways to mature what we have into a new external
foundational framework"). Prior art in-project:
`substrate-crossing-seam-design-sketch_2026-08-17.md` (format precedent),
`seam-stack_README.md`, PC#0 v0.1.1, PC#7 v0.5, PC#8 v0.1.4 + build plan v0.1,
`form-c-next-steps-spec_2026-08-08.md` (watch items), PC#8 Phase 0–2 session
records, `collision_check_substrate_neutral_governed_crossing.md` (2026-08-18).

**Changelog:**
- **v0.2 (2026-08-18).** Post-collision-check revision. Category claim
  replaced throughout with the narrowed four-criteria language from PC#8
  v0.1.4 §Landscape Position (canonical wording; no independent re-drafting).
  §5 updated: AWS Dogwood (primary adjacency), Denis et al. 2024 (tertiary),
  Keyhive gate-on-sync vs. govern-the-crossing distinction, empirical-asymmetry
  note (SL-0121). §8 embedded collision-check task spec retired; replaced with
  run-and-reconciled summary. Evidence posture updated in §3 (F-3) and §4 for
  the KL-1/KL-2 joint conversion (SL-0121) — "near-zero evidence base"
  superseded; NI-5 stack-scoping language retained. TCP/TLS analogy retained
  with publication-track hygiene note. Publication-candidate status declared.
  Forks F-1/F-2 remain OPEN — this revision resolves neither.
- **v0.1 (2026-08-18).** Initial speculative sketch.

---

## 1. The reframe under test

**Current framing:** The Seam Stack is a four-layer architectural *pattern*.
Pattern Commons entries document instances of it. Prototypes consume substrates
(Automerge+Keyhive, atproto) and are blocked when those substrates are immature.

**Proposed framing:** The Seam Stack matures into a **crossing-layer
framework** — the reference implementation of governed crossings, riding on
any conforming substrate. The framework is never blocked; only individual
*substrate adapters* are. The category the framework would occupy is defined
by the four narrowed criteria in §5 — substrate-neutral via published
conformance contract; crossing as governed object with middleware-enforced
write-before-fire ordering; no external finality arbiter in the crossing
path; tamper-evident post-hoc evidence envelope — as reconciled through the
2026-08-18 collision check (verdict: ADJACENT, category unoccupied; see §8).

The one-line analogy (cleared for speculative register — see §8 hygiene note):
**Keyhive is to this framework what TCP is to TLS.** The transport layer is
being solved by others; the trust protocol that rides on it is the position
the four criteria define. Nobody blocked on TCP maturity by writing TLS —
they defined the protocol against an interface and let transports mature
underneath. *(Hygiene note: Sweep 6 and the full LFC Berlin 2026 sweep found
no competing use of this analogy in the target domain; it may be used in
speculative-register drafting but requires a final collision check before any
publication-track use.)*

### What the framework is NOT

- Not a CRDT engine, sync protocol, or capability-crypto core. Substrate work
  is explicitly out of scope — that layer is mature-in-progress (Ink & Switch,
  Automerge core, Keyhive, atproto) and competing there is a decade-scale
  error.
- Not a hosted service, relay network, or platform. The relay-facilitates-
  and-exits discipline (Seam Stack Boundary layer) applies to the framework's
  own architecture.
- Not (initially) a supported library with API stability promises. See fork
  F-2, spec-first default.

---

## 2. What the framework ships

Four deliverable classes, mapped to the existing four layers. The layer
responsibilities are unchanged; what changes is that three of the four ship
as executable/conformance artifacts rather than prose. Together they are the
implementation shape of the four category criteria (§5): the Substrate
Contract carries criterion (i); the crossing lifecycle carries (ii) and
(iii); the evidence envelope carries (iv).

| Layer | Today (pattern) | As framework |
|---|---|---|
| **Substrate** | Named technology choices per PC entry | **Substrate Contract** — a conformance interface any substrate adapter implements. Pluggable adapter boundary. |
| **Governance** | TCF vocabulary + spec prose; vocab IRIs live | **Executable vocab** — schema validation, admissibility checks, refusal as runtime behavior. IRIs remain the stable surface. |
| **Boundary** | Seam discipline documented per pattern | **Crossing lifecycle as code** — intent record, write-before-fire ordering, crossing state machine, timeout horizons. |
| **Evidence** | Unified crossing record schema; assurance scale | **Evidence envelope library** — CR emission, assurance tagging, timestamp anchoring, deferred-party legibility. |

### 2.1 The Substrate Contract (the load-bearing new artifact)

A conforming substrate provides, minimally (draft list — Mode 1 refines):

1. **Authenticated identity** — party-bound, verifiable, with a stable
   reference (DID, WebID, fingerprint — mechanism-agnostic).
2. **Revocable grants with queryable grant state** — the framework must be
   able to ask "what access does actor X hold on object Y *now*" and get an
   answer the substrate stands behind. (Keyhive: `accessForDoc`; the
   MindooDB `wasAllowedAt()` existence proof suggests historical queryability
   as a SHOULD, not MUST.)
3. **Durable, ordered writes** — sufficient to implement write-before-fire.
   Does not require global consensus; requires local durability plus an
   observable propagation event (Jetstream commit event, sync confirmation).
4. **No finality-arbiter requirement** — the substrate must not force an
   external arbiter into the crossing path. (This is the divergent bet
   against Ossa-class designs, imported as a contract constraint. It is a
   *bet*, tagged as such.)
5. **End-to-end confidentiality (tiered)** — MUST for adapter class A
   (Keyhive-class); explicitly declared-absent for class B (atproto public
   PDS), with the exposure named in the adapter's declared limits rather
   than hidden. The PC#8 `boundType: 'exposure-upper-bound'` discipline
   generalizes here.

**Existing adapter evidence:** two partial adapters already exist in
prototype form — (a) Automerge+Keyhive (PC#7, 191/191 tests, contract items
1–2–5 demonstrated; item 3 partial), (b) atproto/bsky PDS (PC#8 Phases 0–2,
contract items 1 and 3 demonstrated: check:pds Run 0 through the Phase 2
firehose and CID verification runs; item 5 declared-absent by design). The
framework move *extracts* the contract from what these two already share,
rather than inventing it.

### 2.2 The methodology as product surface

Differentiator claim (speculative): no framework in the visible landscape
ships with a survival ledger, Counter-Passed specs, pre-registered acceptance
criteria, and named known limits as *framework documentation*. Shipping the
governance methodology alongside the code makes the framework
self-demonstrating with respect to the Full Personhood essay's legibility
argument. Cost: the methodology docs become public API of a sort — versioned,
answerable, and a maintenance surface. Mode 1 decides how much of the harness
apparatus is published vs. referenced.

---

## 3. Pre-registered forks (decision points, not discussion points)

Declared here per anti-retroactivity discipline. Each fork must be resolved
in a governed session before the corresponding work item opens; none blocks
this sketch.

### F-1 — Naming/identity fork ★ one-way door — OPEN
**Options:**
- (a) The Seam Stack *becomes* the framework — same name, "pattern" →
  "framework" reframe. Minimal new surface; risks retroactively changing the
  meaning of every existing citation (essay footnote 7, PC entries, vocab
  IRIs, seamstack.org copy).
- (b) New named thing that *implements* the Seam Stack — pattern stays
  pattern; framework is its reference implementation. Cleaner citation
  hygiene; costs a second name to establish.

**Constraint:** becomes one-way once the Full Personhood essay circulates to
frontier-tier reviewers with the current "pattern" language. If outreach
proceeds before F-1 resolves, option (b) is the de facto default.
**Owner:** operator decision, governed session, before any public framing
change. **Not resolved by the v0.2 revision.**

### F-2 — Spec-first vs. code-first — OPEN
**Options:**
- (a) **Spec-first (working default):** publish the Substrate Contract +
  conformance spec + the two existing prototypes as *reference evidence*, not
  supported code. Early-Solid model. Adoption surface remains the Pattern
  Commons (people implement patterns, not import a package). Fits solo-
  operator capacity; defers API-stability commitments.
- (b) Code-first: extract a real library (`@seam-stack/crossing` or
  equivalent) from the PC#7/PC#8 codebases. Higher adoption ceiling; commits
  to triage, semver, and stranger-support at a capacity the operator does not
  currently have.

**Default rationale:** the death-by-success problem is the dominant risk for
a solo operator with a day job. Spec-first keeps the institution-not-tenant
position without the support treadmill. Revisit at first external
implementation signal. **Not resolved by the v0.2 revision.**

### F-3 — Sequencing against PC#8 evidence — GATE CONDITION MET
**Options as originally declared:**
- (a) **Evidence-gated (working default):** framework framing does not go
  public before PC#8 Phases 1–2 produce empirical crossing evidence.
- (b) Parallel-track: spec drafting proceeds now in governed sessions,
  unpublished, so the framework spec is ready when evidence lands.

**Status update (2026-08-18):** The evidence condition F-3(a) gated on is
now met. PC#8 Phase 2 closed with the joint KL-1/KL-2 conversion event
(SL-0121, repo HEAD `7f905a9`): write-before-fire ordering held across all
runs, intent-without-completion legibility demonstrated on the live stack,
`seamCrossingRef` present in the raw Jetstream firehose payload with 4/4
sub-field parity, and 3/3 CID round-trips plus 3/3 independent recomputes
confirming content-addressing. The original rationale — "a *foundational
framework* with a near-zero evidence base is a manifesto" — is superseded:
the evidence base is no longer near-zero, and the architectural bet
(write-before-fire, no finality arbiter) now has prototype backing on this
stack. **NI-5 remains in force:** the evidence is stack-scoped (one
substrate pair, one lexicon); no generality claim is made or licensed by
this update. The publication gate F-3 imposed is satisfied; what remains
gating public framing changes is F-1 (naming), not evidence.

**Note:** (a) and (b) compose — (b) is about *drafting*, (a) about
*publication*. With the evidence condition met, the residual fork content
collapses into F-1/F-2 sequencing.

### F-4 — Vocab namespace continuity — OPEN (default standing)
If F-1 resolves to (b), do the live IRIs
(`jediwright.github.io/seam-stack/vocab/...`) stay under the seam-stack
namespace with the framework referencing them, or does the framework mint its
own? **Default: IRIs never move.** Resolvable-IRI stability is the whole
point of having them; the framework references, it does not re-mint.

---

## 4. What this reframe changes about current blockers

| Blocker (today's framing) | Reframed (framework framing) |
|---|---|
| Keyhive pre-alpha; `create2()` awaiting "a nicer way" | Adapter-A maturity issue. Framework unblocked; adapter carries a declared limit + watch item. |
| Subduction 0.16.0 pin; wasm init ordering | Adapter-A implementation notes (already recorded in sub-package README). |
| `findWithProgress` absent from SDK | Candidate Substrate Contract SHOULD-item; zerno study session feeds contract drafting rather than unblocking. |
| Brigstow / SedimentreeSource unshipped | Adapter-A *successor* viability watch — monitoring purpose shifts from "when do we get unblocked" to "when does a next-gen adapter become implementable." |
| Jetstream filter quirk; relay variance | Adapter-B implementation notes (Phase 0 findings F-series; held through the full Phase 2 firehose run). |
| ~~Near-zero empirical evidence~~ **Evidence base: stack-scoped closing evidence in hand** | **Superseded 2026-08-18.** KL-1/KL-2 joint conversion (SL-0121): write-before-fire, intent legibility, firehose survival, and CID content-addressing demonstrated on the Automerge+Keyhive → atproto stack. Remaining evidence limits are the ones the PC#8 KL table names (KL-3 through KL-12, including the PDS-migration half of KL-2's original scope) — declared limits, not an absent base. NI-5: stack-scoped; no generality claim. |

The general move: every blocker becomes either (a) an adapter-scoped declared
limit, (b) a Substrate Contract requirement discovered empirically, or
(c) a named evidence limit with its closing-evidence class stated. Nothing is
hidden; everything is relocated to where it is answerable.

---

## 5. Landscape position (reconciled — canonical language from PC#8 v0.1.4)

The category claim below is the narrowed four-criteria language from PC#8
v0.1.4 §Landscape Position (the reconciliation session's canonical wording;
verbatim, tightened only where the sketch context requires). It supersedes
the v0.1 category framing wherever the earlier wording appears in citation.

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

### Adjacencies (collision check 2026-08-18; three flanks requiring narrowing)

**Primary — AWS Dogwood (released August 6, 2026).** The most dangerous
adjacency; differentiation front-loaded here per the reconciliation. Dogwood
introduces temporal conditions on sequences of prior tool-call events,
requires a durable event log, and runs at a gateway that intercepts before
effects fire — surface-level, "governed sequences of crossing events with a
durable record required" describes both Dogwood and this framework. The
architectural distinctions:

- **(ii) Log-consuming, not log-producing.** Dogwood is a policy language
  that *consumes* a durable event log the deployer must supply — its own
  documentation warns that timestamps must be trusted, events authenticated,
  and traces durably stored, requirements *placed on the deployer*. This
  framework's middleware *produces* the crossing record as a precondition of
  the crossing; write-before-fire is enforced by the middleware, not
  delegated to deployer infrastructure.
- **(iii) Managed arbiter required.** AgentCore Gateway is the centralized
  arbiter; the reference interpreter is not production-ready, and the only
  production path runs through AWS infrastructure. This framework's crossing
  path requires no such arbiter.
- **(i) Substrate-locked — shelf-life caveat.** Dogwood is tied to Amazon
  Bedrock AgentCore Gateway; no published conformance contract exists for
  substituting local-first substrates. This is the most visible
  differentiator today but has the **shortest shelf life**: Dogwood's
  published roadmap includes further temporal operators, and a third-party
  implementation against a different substrate is possible. The (ii) and
  (iii) distinctions are architectural and survive a future Dogwood substrate
  extension — they are the ones that must remain prominent.
- **(iv)** Dogwood makes no evidence-envelope claim.

**Secondary — Keyhive/Beelay (Ink & Switch).** The local-first community's
most serious access-control work; shares criterion (iii) (coordination-free,
arbiter-free). The distinction in one sentence: **Keyhive gate-on-sync; this
framework govern-the-crossing.** Keyhive governs *who may cross* by
preventing unauthorized synchronization; this framework governs *authorized
crossings* as first-class objects — in Keyhive, an authorized crossing fires
without a pre-committed record, a declared exposure position, or an evidence
envelope for parties who arrive after the fact.

**Tertiary — Denis et al. 2024 (DIFC for distributed systems).** Computers &
Security 144 (2024), DOI 10.1016/j.cose.2024.103975 — the closest academic
precedent in the IFC line: decentralized information-flow control using
events as the unit of IFC, no central authority. The split: Denis et al.
govern *implicit* information-flow confidentiality and integrity within a
unified computation model (a deployed-nowhere theoretical model); this
framework governs *explicit* authorized crossings — intentional, governed
acts with a durable pre-committed evidence envelope legible to third
parties — and has prototype evidence on a live stack.

**Carried entries (from PC#8 recon, unchanged):** grjte/Groundmist (closest
local-first precedent, deferred authorization), Jake Lazaroff (crossing
invisible by design; his LFC Berlin 2026 talk names the gap and defers it —
citable in his own characterization), Martin Kleppmann (framing voice),
Daniel Holmgren (atproto protocol), Ossa/Parker (finality arbiter required —
the divergent bet), Jacob et al. arXiv:2604.23560 (formal verification,
upstream of the crossing). The broader IFC tradition (Jif, LIO, FlowCaml,
Troupe) is distinguishable as a class: compile-time/label-propagation
noninterference vs. runtime governance of intentional authorized crossings
with post-hoc auditability.

**Empirical asymmetry (as of 2026-08-18):** KL-1 and KL-2 converted from
prototype-pending to closing evidence (PC#8 Phase 2 joint conversion,
SL-0121). The claim is no longer spec-vs-spec against Dogwood; it is
**prototype-evidence vs. spec**. Dogwood has no published prototype evidence
of middleware-enforced write-before-fire ordering. This asymmetry is real and
should be maintained in any comparative framing. (NI-5: the evidence is
stack-scoped; the asymmetry claim is about *this stack's* demonstration, not
generality.)

---

## 6. Relationship to existing program (nothing moves yet)

- **PC#8** — Phases 0–2 complete; KL-1/KL-2 converted (SL-0121). If the
  framework framing survives, PC#8 retroactively becomes "adapter-B
  evidence" — but that relabeling is a Mode 1 act, not a now act. Phase 3
  lifecycle tests remain optional enrichment.
- **Full Personhood essay** — no language changes. The held items (R-1
  resolution session, footnote 23/24 fix) are unaffected and remain gates on
  wider circulation. F-1 adds a *soft* dependency: resolve naming before
  frontier reviewer outreach if feasible, since the essay's "pattern" language is
  what gets anchored in reviewers' heads.
- **THEORY.md** — unchanged; merger-ready as-is. If F-1(a) is chosen,
  THEORY.md gets a queued amendment (queue-don't-reopen), not an edit.
- **Boundary Principles 7.6/7.1** — unaffected.
- **Vocab namespaces** — frozen per F-4 default. The substrate-crossing
  PROPOSED cluster's promotion (Lexicon v2.1 → v2.2 CV-table session) is a
  separate governed session; nothing here anticipates its outcome.

---

## 7. Speculative-to-governed handoff (status-updated next steps)

Ordered; each is its own session or sub-item.

1. ~~**Collision check**~~ — **RUN AND RECONCILED** (2026-08-18; see §8).
   Verdict ADJACENT; category unoccupied; narrowing applied in §5 above and
   canonically in PC#8 v0.1.4 §Landscape Position.
2. **Mode 1 scoping session:** resolve F-1 and F-2; draft Substrate Contract
   v0.1 (extract from PC#7 + PC#8 shared surface per §2.1). The F-3
   drafting/publication split is moot (evidence condition met; see §3).
3. **Counter-Pass on Substrate Contract v0.1** (siloed project, standard
   discipline).
4. **Publication gate:** the F-3 evidence condition is satisfied (SL-0121).
   Remaining publication-track gates are F-1 resolution (for any public
   framing change) and, for the category claim itself, the CV-table
   promotion threshold (NI-5 holds until that session closes).

Estimated shape: step 2 is one session; step 3 standard Counter-Pass
cadence. No further SL-IDs pre-assigned.

---

## 8. Collision check: run and reconciled

The collision-check task spec formerly embedded here (v0.1 §8) served its
purpose and is retired. Summary of record:

- **Run:** 2026-08-18, siloed adversarial context. Six sweeps completed;
  none waived (policy-engine class incl. Dogwood; capability tooling
  UCAN/Biscuit; IFC line; local-first ecosystem; Cambria post-mortem;
  TCP/TLS analogy hygiene).
- **Verdict:** **ADJACENT** — the category as stated is not occupied by any
  currently shipping, named framework; three flanks require rhetoric
  narrowing (Dogwood primary, Keyhive/Beelay secondary, Denis et al. 2024
  tertiary). Narrowing applied.
- **Residual risk:** the check's largest unresolved residual — LFC Berlin
  2026 talk content — was **CLOSED** in the reconciliation session by direct
  schedule fetch and targeted talk reads (full three-day schedule; no
  competing claim found).
- **Canonical differentiation text:** PC#8 v0.1.4 §Landscape Position
  (`local-first-series/pattern-commons/pattern-commons-08-substrate-crossing-seam-v0-1-4_2026-08-18.md`,
  SL-0122). §5 above carries that language into this sketch; where the two
  diverge, the PC#8 entry governs.
- **Source artifact:** `collision_check_substrate_neutral_governed_crossing.md`
  (2026-08-18).

---

## 9. Open questions carried (not forks — genuinely unresolved)

- Q1: Does the Substrate Contract's item 4 (no finality arbiter) belong as
  MUST, or as a declared architectural bet with a conforming-with-arbiter
  profile allowed? (Touches the Ossa divergence directly.)
- Q2: Where does agent governance (AI agents as governed parties with
  capability lifecycles — Seam Stack Governance layer claim) sit in the
  framework: core, or first extension module?
- Q3: Is there a minimal conformance test suite that could certify an
  adapter, and is building one compatible with F-2 spec-first?
- Q4: `wasAllowedAt()`-style historical grant queryability — SHOULD or MUST?
  (Evidence-layer implications for deferred parties.)

---

*Speculative design sketch v0.2 — 2026-08-18 · J. Wright / UX Minds, LLC*
*AI-collaborative synthesis; human authorial responsibility and intellectual*
*direction held by the named author.*
*Canonical copy: operator's machine. Delivery-not-application enforced.*
*SINGLE-CONTEXT — NOT PANELED · CONTEXTUAL register · SL-0123 (revision*
*event delta; pending operator tail verification).*
