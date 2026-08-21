**Status:** Draft v0.1 — speculative, single-context; no Counter-Pass; no prototype

---

# Pattern Commons #9 — The Governed Content Production Crossing

---

## What This Entry Is — and Is Not

This is the third Pattern Commons entry authored before its prototype
exists, following the precedent established by PC#8. It is issued as
**speculative design intent** from a blue-sky session: the domain is
identified, the problem is named, the divergences from PC#0's
constitutive properties are sketched, but no Counter-Pass has run and
no prototype evidence exists.

This entry's epistemic position:

- **Every design resolution here is first-pass speculation** (~,
  single-context, ungoverned session). Nothing is Counter-Passed. Nothing
  is prototype-verified. The intent is to produce a spec surface legible
  enough to govern a future governed drafting session.
- **NI-5 is in force throughout.** Zero generality claims. The
  architecture is local-first specific on current evidence.
- **Artifact B is untouched.** The TCF is untouched. Neither framework
  is amended by this entry; both are invoked as governing context.
- **The RA connection is the strategic motivation, not the spec
  claim.** The relationship between this entry and the TCF's RA mapping
  candidacy is named explicitly here — it is the reason this entry
  exists — but establishing that claim requires a future governed
  session, a pre-registration spec, and a mapping run under isolation
  discipline. This document produces none of those. It is the upstream
  input a pre-registration spec would consume.
- **What "design intent" means here:** enough structure to ask the right
  open questions (OQ-series), identify what a Counter-Pass would stress-
  test, and surface the RA pre-registration claim this domain enables.

Per PC#0's conformance requirements, this document (1) cites PC#0 as
the parent pattern, (2) specifies what diverges from the four
constitutive properties and the Seam Stack, (3) names the seam trigger
explicitly, and (4) adopts `seam:CrossingRecord` as the base shape for
all governed-event records.

---

## The Pattern in One Sentence

The governed content production crossing is the boundary event that fires
when a content object reaches the TCF tier-compliance threshold required
for governed publication — moving from local-first, author-controlled
substrate to a committed, externally legible surface — and the
architectural argument is that the crossing must be **granted, gated by
TCF tier compliance, and recorded before it fires**, making TCF tier
boundaries schema-checkable enforcement gates rather than editorial
conventions.

---

## The Problem It Solves

Content governance frameworks and local-first data governance frameworks
have been developing in parallel without a formal crossing point. The
TCF governs meaning — from Quark constraints through Particle fields,
Cluster assemblies, Zone arrangements, and Structure delivery. The Seam
Stack governs crossings — the moment data moves between parties, between
substrates, between epistemic regimes.

The gap: **publication is a crossing, and it currently has no governed
record.** When a content object moves from a draft Automerge document
on an author's local substrate to a CMS, a public AT Protocol PDS
record, a Ghost post, or any externally legible surface, four things
happen that have no architectural home in either framework as currently
specified:

1. **The author's intent is not recorded.** There is no crossing record
   capturing which TCF tier compliance state the content object was in
   at publication time, who authorized the crossing, or what gate
   conditions were checked.
2. **TCF tier compliance is editorial, not enforced.** A Quark-level
   constraint violation (non-approved terminology, exceeded character
   limits, missing epistemic status declaration) can cross the boundary
   without triggering a gate. The constraint exists; the enforcement
   surface does not.
3. **The `tcf:register` field has no enforcement home.** The UFO Lexicon
   carries `tcf:register` (PROPOSED: `plain | contextual |
   governed-internal`) as a candidate gate, with the `weakest-status
   propagation` rule inverted — most restrictive register requirement
   propagates up, not down. But there is currently no gate at which this
   field blocks a crossing. It enforces editorially, not architecturally.
4. **The TCF cannot make the RA claim without schema-checkable
   boundaries.** The TCF's RA mapping candidacy — the claim that the
   seven TCF tiers instantiate the Resonance Architecture's
   organizational grammar — requires schema-checkable tier boundaries to
   be evidentially distinguishable from a structural analogy. A
   `seam:CrossingRecord` emitted at the TCF tier-compliance threshold
   produces exactly that artifact: the tier boundary between
   governed-internal and publicly committed becomes machine-checkable.

The governed content production crossing addresses all four by treating
publication not as a content operation but as a **governed crossing
with a TCF-compliance gate.**

---

## The Seam Trigger

Per PC#0, the trigger is named explicitly:

**The seam fires when a content object is submitted for publication from
a local-first, author-controlled substrate to an externally legible
surface, and the submission carries a declaration of which TCF tier
compliance state the object has reached.**

"Externally legible surface" for this entry's reference implementation:
any destination that makes the content object readable to parties beyond
the author's capability-governed peer set — a CMS content type commit,
an AT Protocol PDS record, a Ghost post, a public Automerge document
shared outside the author's controlled subnet.

The trigger is **the publication submission**, not CMS acceptance,
indexing, or delivery to readers. Post-crossing events (relay
distribution, search indexing, AI training ingestion) are out-of-reach
limits named in the Known Limits section — not scope this gate claims.

State changes that do **not** fire this seam:
- Local edits on the author's substrate, regardless of tier
- Sync among capability-governed peers on the same substrate
- In-progress draft promotion within the governed internal workflow (a
  draft advancing from Particle to Cluster is an internal state
  change, not a crossing)
- Export to a counterparty within the same Seam Stack instantiation
  (those are PC#7 or equivalent)

---

## Why This Domain Is Different From PC#8

PC#8's crossing fires on **substrate topology change**: the epistemic
properties of the target regime (revocation semantics, exposure bounds,
record integrity) differ from the local-first side. The domain question
is what the architecture can honestly claim at a regime boundary.

PC#9's crossing fires on **content governance state**: the TCF tier
compliance of the content object itself determines whether the gate
passes. The domain question is what the content object can honestly
claim about its own governed state at the moment it becomes publicly
committed.

The two crossings can compose — a content object that passes the TC#9
gate may then cross a substrate boundary (PC#8). They are not the same
event. PC#9 fires first, on the author's side. PC#8 fires at the
substrate edge, on the transition. A sequenced crossing that triggers
both is a chained crossing under Form C's chaining semantics.

---

## Carry-In: What This Entry Inherits Unchanged

The four constitutive properties of the governed crossing (PC#0) —
declared scope, grant, gate, record — carry in full. Key inherited
constraints:

- **The finality-arbiter-free constraint.** No field or mechanism in
  this entry requires a coordinating party at record-emission time.
- **The Q6 lock.** `lineageAnchorType: author-declared` is the current
  default. `timestamp-signed` infrastructure would convert pre-crossing
  ordering discipline into a structural invariant; locked pending that
  infrastructure.
- **The `seam:CrossingRecord` base shape.** Identity group, provenance
  linkage group, lineage anchoring group, evidence scope group —
  all inherited.
- **Boundary principles in scope:** P8 (explicit, minimal, designed);
  P9 (exposure claims are upper bounds); P10 (data shapes carry lineage
  and horizons); P11 (agents are governed parties); P12 (longevity
  commitments have terms); P13 (governance composes beyond the
  individual); P14 (relay boundaries are governed crossings). All
  PROPOSED per UFO Lexicon v2.x.
- **The gate fails closed.** Unconfirmed compliance state blocks;
  silence blocks; a missing conditional group blocks.

**Gate qualification specific to this entry:** The gate checks TCF tier
compliance state as declared at submission time. It cannot verify that
the content object was authored in compliance — it checks the
compliance declaration and the presence of required fields, not the
epistemological authenticity of the author's claim. The Q6 lock applies
here as elsewhere: author-declared is the current ceiling.

---

## The Vocabulary Extension — Candidate Slots (~)

This section is first-pass speculation. All values PROPOSED, pending a
governed drafting session.

### New `governanceEvent` value (~)

| Value | Definition |
|---|---|
| `content-production-crossing` | A governed crossing whose trigger is the publication of a content object from an author-controlled local-first substrate to an externally legible surface, at a declared TCF tier-compliance threshold. The event-class discriminant for content production crossing records. |

### New `boundType` candidate (~)

The `boundType` question for this seam is genuinely open (see OQ-3).
Candidate resolution:

- A content object that crosses to a public CMS may be `exposure-upper-
  bound` (named counterparty, enumerable distribution) or closer to
  `exposure-unbounded` (public web, AI crawling, indefinite
  redistribution).
- The appropriate `boundType` may be **target-surface-dependent**, not
  a fixed vocabulary value for this seam type.
- Candidate: a `declaredBoundType` field on the grant (by analogy with
  PC#8), fixed at submission time, allowing the crossing record to carry
  whatever bound the target surface warrants.

This is OQ-3. Not resolved here.

### New gate-condition field group (~)

The critical vocabulary addition for this entry is not a `boundType`
value but a **TCF-compliance field group** on the grant and the gate
check. Candidate:

| Field | Purpose |
|---|---|
| `tcfComplianceTier` | The TCF tier the content object has been declared to have reached at submission time. Controlled vocabulary: `particle` / `cluster` / `zone` / `structure` / `ecosystem` / `biome`. Gate checks presence and minimum-tier threshold against the crossing's declared scope. |
| `tcfRegister` | The `tcf:register` value (`plain` / `contextual` / `governed-internal`) the content object carries. Gate checks that the declared register matches the target surface's register requirement. The most-restrictive-propagates rule: if any Quark in the object's chain carries `governed-internal`, the object cannot cross to a public surface without an explicit operator override recorded in the crossing record. |
| `tcfEpistemicStatus` | The `tcf:epistemic-status` declaration carried by the object at submission time (`confirmed` / `inferred` / `unverified` / `time-sensitive`). Carried into the crossing record as a declared value; does not block the crossing but is material to the Evidence layer's `evidenceDecay` calculation (see OQ-4). |
| `tcfQuarkViolations` | A structured list of Quark-level constraint violations present in the object at submission time, if any. The gate's minimum-tier check determines whether violations block (above threshold: block) or are recorded-with-crossing (below threshold: record-and-pass with operator acknowledgment). |

---

## The Grant Model (~)

The grant authorizes a specific content object (or content object class,
for standing grants) to cross to a specific target surface at or above a
declared TCF tier threshold.

**Minimum required fields on the grant (~):**

| Field | Purpose |
|---|---|
| `crossingType: content-production` | Discriminant. Triggers the TCF-compliance conditional field group. |
| `minimumTcfTier` | The lowest TCF tier at which the gate will pass this crossing. Objects below this tier block. Operator-set at grant time. |
| `targetSurface` | URI or surface-class identifier for the publication destination. |
| `tcfRegisterRequirement` | The register constraint the target surface carries. Gate checks `tcfRegister` against this. |
| `declaredBoundType` | The `boundType` the crossing record will carry — fixed at grant time (see OQ-3). |

**Deliberate design question — standing vs. per-object grants (OQ-1):**
PC#7 uses per-crossing grants for high-stakes identity events. A
content production workflow may involve hundreds of crossings per day.
A standing grant (author-level, per target surface) with per-object
gate checks is likely the correct design for production workflows, but
this introduces a class of grant the existing architecture has not
fully specified. See OQ-1.

---

## The Gate (~)

The gate honestly enforces, pre-crossing and at crossing moment only:

1. **Grant current at act time** (`assertCapabilityCurrent()`,
   unchanged from the pattern).
2. **TCF tier threshold met.** The content object's declared
   `tcfComplianceTier` is at or above the grant's `minimumTcfTier`.
   SHACL-enforceable at the Governance layer against the Quark-level
   schema constraints.
3. **Register constraint satisfied.** The object's `tcfRegister` is
   compatible with the target surface's `tcfRegisterRequirement`. The
   most-restrictive-propagates rule enforced; `governed-internal` blocks
   to public surfaces without explicit operator override.
4. **No blocking Quark violations.** Violations at or above the
   minimum tier threshold block. Violations below threshold are
   recorded-and-passed with operator acknowledgment.
5. **Record-before-crossing ordering.** The crossing record is minted
   before the publish submission fires. Under the Q6 lock this is
   author-declared ordering discipline; `timestamp-signed` would
   convert it to a structural invariant. See KL-3.
6. **The gate fires exactly once.** Its role completes at the crossing
   moment. Post-crossing content state (editorial updates, CMS
   revisions, reader responses) are not gate-visible events.

---

## The Record (~)

The crossing record carries the standard `seam:CrossingRecord` base
shape plus the TCF-compliance field group. It produces:

1. A **pre-crossing intent record** (minted before the publish call
   fires) carrying: `governanceEvent: content-production-crossing`;
   `tcfComplianceTier` declared at submission; `tcfRegister` declared;
   `tcfEpistemicStatus` declared; `tcfQuarkViolations` enumerated;
   gate result; `emittedAt`; `emittedBy`.
2. A **completion record** (minted after publication confirmation from
   the target surface) carrying: the target surface's assigned URI or
   content address; `authorizedContentDigest` (hash of the object
   authorized at gate time, by analogy with PC#8's content-binding
   field); chain reference to the intent record.

The chain between intent and completion records provides the
evidentiary artifact that makes TCF tier compliance a schema-checkable
boundary event rather than an editorial claim. This is the load-bearing
artifact for the RA mapping candidacy: the crossing record is the
proof that the tier boundary between governed-internal and publicly
committed has a machine-legible representation.

---

## The RA Pre-Registration Claim This Domain Enables (~)

This section is the strategic motivation for the entry, stated
precisely so it is neither inflated nor buried.

**The TCF's existing RA relationship is containment, not test evidence.**
The TCF is the Governance layer of the Seam Stack. Its seven tiers are
already cited in the RA's 7-tier table as a domain column
(Quarks–Biomes). The Seam Stack RA program spec named this explicitly
as Relationship 1 (containment): the Seam Stack inherits one TCF
instantiation of the tier spine at its Governance layer. Containment
is inheritance, not a test. It does not constitute independent evidence
for the isomorphism claim.

**What PC#9 changes:** If the governed content production crossing is
prototyped and the gate's TCF-compliance check is implemented against
SHACL shapes at the Quark level, the TCF tier boundaries become
**schema-checkable at the crossing event**. The `tcfComplianceTier`
field in the crossing record is a machine-legible attestation of which
tier boundary was crossed. The Quark-level SHACL shapes are the
invariants that enforce it. This gives the TCF the same evidentiary
property the Seam Stack used to pass its RA mapping: tier boundaries
verifiable against schemas, not against editorial convention or mapper
intuition.

**The pre-registration candidate (~):** A future TCF RA mapping session
could pre-register predictions against the seven-tier table using the
PC#9 crossing record as the schema anchor. The predicted tier column
would map TCF tiers against the RA operations — Quarks binding
(Bind/Sub-atomic), Particles instantiating (Instantiate/Nano), Clusters
bonding (Bond/Micro), Zones closing (Close/Zone), Structures completing
(Complete/Page), Ecosystems federating (Federate/System), Biomes
totalizing (Totalize/Ecosystem). P-2 (conditional/Branch Tier absent
or present) would be the first falsifier. The mapping would run in
isolation discipline against the TCF schema artifacts, not against the
tier definitions alone.

**The sequencing discipline:** PC#9 spec → PC#9 prototype → TCF SHACL
shapes at gate → TCF RA pre-registration spec → TCF RA mapping session →
TCF RA formalization spec → `THEORY.md` amendment. Nothing in this
entry compresses any step in that sequence. The RA claim is the
motivation; it is not the output of this spec.

---

## Known Limits (~)

The KL inventory for a first-pass spec. Each item names the class of
evidence that would close it.

**KL-1 — Standing grant architecture unspecified.** A content
production workflow with hundreds of daily crossings requires a standing
grant model not present in the existing grant architecture. The
per-crossing grant model from PC#7 is not the right shape here; a
per-surface, author-level standing grant with per-object gate checks is
the candidate. Closing evidence: a governed design session producing a
standing-grant spec compatible with the existing grant field group.

**KL-2 — TCF SHACL shapes not yet specified.** The gate's
`tcfComplianceTier` check requires SHACL shapes at the Quark level that
can validate a content object against its declared tier's constraints.
The TCF v1.6/v1.7 specifies the tier structure; it does not provide
machine-executable SHACL shapes. Closing evidence: a TCF schema
extension session producing per-tier SHACL shapes, governed under TCF
v1.8 or equivalent.

**KL-3 — Record-before-crossing ordering is author-declared.** Under
the Q6 lock, pre-crossing ordering is a discipline, not a structural
invariant. A `timestamp-signed` infrastructure would make the ordering
verifiable. Closing evidence: `timestamp-signed` infrastructure
unlocked (see PC#8 KL-9 parallel).

**KL-4 — `tcfRegister` enforcement surface.** The `tcf:register` field
is PROPOSED in the UFO Lexicon and has no governed promotion path yet.
The gate cannot enforce a PROPOSED field as a hard block without a
governed amendment session promoting the field and specifying its
enforcement shape. Closing evidence: a UFO Lexicon amendment session
promoting `tcf:register` and naming the enforcement surface (gate vs.
warning vs. recorded-violation).

**KL-5 — `boundType` target-surface dependency unresolved.** The
appropriate `boundType` for a content production crossing varies by
target surface (CMS with enumerable readership vs. public web vs.
AT Protocol relay). A `declaredBoundType` on the grant is the candidate
resolution, but the interaction between this field and the existing
`boundType` vocabulary's ordering rule requires a governed design
session. See OQ-3. Closing evidence: a governed design session resolving
OQ-3 and producing a `declaredBoundType` field spec.

**KL-6 — `tcfQuarkViolations` field shape unspecified.** The field is
named here as a structured list; its schema is not specified. The
gate's behavior on violations at vs. below the minimum tier threshold
is described conceptually but not schema-grounded. Closing evidence:
a governed design session producing the field spec and the gate's
violation-handling logic.

**KL-7 — Post-crossing content state is out-of-reach.** Editorial
updates, CMS revisions, and syndication after the crossing are not
gate-visible. A crossing record minted at v1.0 of a content object
does not automatically update when the object is revised. Whether
revisions require new crossing records (by analogy with PC#8's
completion record) or whether a standing record model is appropriate
is unresolved. Closing evidence: a governed design session addressing
content lifecycle and revision semantics in the crossing record model.

**KL-8 — AI training ingestion as out-of-reach limit.** A content
object that crosses to any public surface is potentially ingested by
AI training pipelines. The crossing record cannot govern this; the
gate cannot see it. This is an out-of-reach limit analogous to PC#8's
KL-11 (derived content). It is named here, not claimed. The
`tcf:epistemic-status` and `tcfEpistemicStatus` fields in the crossing
record are the honest disclosure surface; they do not constitute
enforcement. Closing evidence: not available within this architecture.

**KL-9 — Chained crossing with PC#8 unspecified.** A content production
crossing that terminates at an AT Protocol PDS is a candidate chained
crossing (PC#9 fires, then PC#8 fires). The chaining semantics,
particularly how the PC#9 completion record's URI becomes the PC#8
intent record's `chainReference`, are not specified. Closing evidence:
a governed design session producing a chained-crossing spec for the
PC#9 → PC#8 composition.

**KL-10 — TCF's own RA mapping is out-of-scope for this entry.** The
RA pre-registration claim described in the "RA Pre-Registration Claim"
section above requires a separate pre-registration spec, a fresh siloed
mapping session, and certification under `ra-session-conductor`. None
of that is produced here. This entry is an upstream input to that
sequence, not a step in it.

---

## Open Questions (OQ-Series)

**OQ-1 — Standing grant vs. per-crossing grant.** Content production
workflows differ from employment seam workflows in volume and cadence.
Is the right grant model a standing grant (author-level, per target
surface, renewed on a horizon), a per-object grant, or a hybrid? The
existing PC#7 grant architecture assumes low-volume, high-stakes
crossings. This is an operator decision before the governed drafting
session opens.

**OQ-2 — Minimum tier threshold: who sets it?** The `minimumTcfTier`
field on the grant requires someone to set the threshold. Candidates:
the author (self-governing), the target surface (CMS policy), or a
third party (editor, publisher, platform). Each has different
implications for the finality-arbiter-free constraint. If the target
surface sets the threshold, is the gate still a person-side
enforcement? This is a design question for the governed drafting
session.

**OQ-3 — `boundType` resolution.** Is `boundType` target-surface-
dependent for this seam, or is there a fixed value appropriate to
content production crossings? The `declaredBoundType` on the grant is
the candidate, but its interaction with the vocabulary ordering rule
requires a governed design session.

**OQ-4 — `evidenceDecay` derivation from `tcf:epistemic-status`.** The
Evidence layer's `evidenceDecay` field (in the `seam:CrossingRecord`
base shape) is the date after which a record's claims require re-
verification. For time-sensitive content (`tcf:epistemic-status:
time-sensitive`), this date should be derivable from the Quark-level
temporal validity constraint. Is this a field the gate can compute and
carry into the crossing record, or is it author-declared at submission
time? Closing evidence: a governed design session resolving the
`evidenceDecay` derivation logic.

**OQ-5 — Pattern Commons entry number.** This spec assigns #9 by
inference from the existing series (#0–#8). The operator should verify
against the live repo index before the governed drafting session assigns
a canonical number.

**OQ-6 — Relationship to GSEF.** A Quark-level schema change under the
TCF's high-scrutiny change control is a GSEF changeClass C or D event
if it touches anything participating in the crossing-record vocabulary.
Does the PC#9 gate need to be aware of the GSEF lineage record for the
Quark shapes it checks? Or is the gate's SHACL shape version-pinned to
the grant's declaration and the GSEF's propagation is a separate
concern? This is the most technically complex open question and is
deferred to the governed drafting session.

---

## What Comes Next

This spec is an upstream input, not a canonical document. The sequencing
before a governed drafting session can open:

1. **Operator review of OQ-1 and OQ-2** — the grant model and threshold-
   setter questions are operator decisions that constrain the design
   space before the session opens. Both can be resolved quickly with a
   written operator decision.
2. **TCF SHACL shape scoping (KL-2)** — the gate's enforceability
   depends on schema artifacts that don't yet exist. A scoping note on
   what per-tier SHACL shapes would look like is a prerequisite for the
   governed drafting session, not necessarily a full spec.
3. **`tcf:register` Lexicon promotion (KL-4)** — if the register
   check is a hard gate condition, the field needs a governed promotion
   path before the gate spec can be written. Alternatively, the gate
   can treat it as a recorded-violation (below the blocking threshold)
   until promotion.
4. **PC#9 governed drafting session** — under Session Harness v0.2,
   Mode 1, with this spec as carry-in. Counter-Pass program follows
   drafting.
5. **Prototype** — the first crossing record emitted from a real content
   object to a real target surface, with SHACL gate checks running
   against per-tier Quark shapes.
6. **TCF RA pre-registration spec** — only after a prototype exists and
   the gate's schema-checkable tier boundary has been demonstrated.

---

*This document is part of the Pattern Commons, the architectural-pattern
documentation series produced alongside the local-first prototype work.
It is published under the same methodology disclosure as the rest of
Systems of Thought: AI-collaborative drafting, human authorial
responsibility, intellectual direction held by the named author.*

*⚑ SINGLE-CONTEXT — NOT PANELED. All claims ~. No Counter-Pass. No
ledger deltas. Blue-sky / speculative session; ungoverned per session-open
declaration. NI-5: local-first specific on current evidence — zero
generality claims in this entry.*
*Delivery-not-application enforced. Canonical files on operator's machine.*

*UX Minds, LLC · J. Wright · August 20, 2026*
