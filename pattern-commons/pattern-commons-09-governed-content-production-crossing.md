**Status:** v0.3 — governed (Session Harness v0.2, Mode 3 producer reconciliation); first pass halted non-converged at its G11 ceiling (SL-0162); **fresh Counter-Pass halted non-converged at its G11 ceiling (SL-0174 — SECOND HALTED PASS; seven iterations total, no constitutive property absent in any)**; §The Gate replaced by gate-steps rewrite (SL-0178, all eight ambiguity flags resolved); third Counter-Pass iteration 1 **CONVERGED WITH NARROWING** (SL-0180); operator closed at iteration 1; **third Counter-Pass CLOSED**; no prototype

⚑ SINGLE-CONTEXT — STAMP LIFTED (2026-08-28)
Carried from v0.1. **Lifted:** third Counter-Pass closed by operator at iteration 1 (CONVERGED WITH NARROWING, SL-0180; operator close decision 2026-08-28). Lift conditioned on noting that the three it-1 narrowings (N1–N3) are post-convergence prose — applied by producer reconciliation, not critic-tested in a subsequent iteration. All design resolutions ~ unless individually marked ✓. Narrowings applied through fresh-pass iteration 3 (reconciliations `producer-reconciliation-pc09-v0-2-iteration-1_2026-08-25.md`, `producer-reconciliation-pc09-v0-2-1-iteration-2_2026-08-25.md`, `producer-reconciliation-pc09-v0-2-2-iteration-3_2026-08-27.md`, `producer-reconciliation-pc09-v0-2-3-fresh-iteration-1_2026-08-27.md`, `producer-reconciliation-pc09-v0-2-4-fresh-iteration-2_2026-08-27.md`, `producer-reconciliation-pc09-v0-2-5-fresh-iteration-3_2026-08-27.md`); third-pass it-1 narrowings N1–N3 applied 2026-08-28 (post-convergence prose; not critic-tested).

---

# Pattern Commons #9 — The Governed Content Production Crossing

---

## Change Log — v0.1 → v0.2 (2026-08-24)

| Item | v0.1 state | v0.2 state |
|---|---|---|
| OQ-1 grant model | open (operator decision) | **RESOLVED ~** — hybrid: standing grant + per-object gate/record. Operator decision 2026-08-24, caveat: pending prototype validation. |
| OQ-2 threshold-setter | open (design question) | **RESOLVED ~** — layered: surface publishes requirement as data; author sets grant threshold at or above it; gate checks the author's value. Counter-Pass lane item 1. |
| OQ-3 `boundType` | open | **RESOLVED ~** — `declaredBoundType` on the standing grant, per surface class, with a monotonic ordering rule. Counter-Pass lane item 2. |
| OQ-4 `evidenceDecay` | open | **RESOLVED ~** — gate-computed for `time-sensitive`; author-declared otherwise; fail-closed on missing temporal validity. |
| OQ-5 entry number | open | **RESOLVED ✓** — live series index verified (00, 07, 08, 09) at `local-first-series` HEAD bb38dc2. |
| OQ-6 GSEF relationship | open | **RESOLVED ~** — gate is shape-version-pinned to the grant; GSEF lineage is Evidence-plane, never a gate condition. |
| KL-1 standing grant | unspecified | **NARROWED** — standing grant field group specified (§Grant Model); closing evidence now prototype-only. |
| KL-2 SHACL shapes | unspecified | **NARROWED** — shape families and gate read-surface specified in companion `tcf-runtime-spec-v0-1`; per-tier shape authoring still gated on TCF v1.8 Section B. |
| KL-4 `tcf:register` | unspecified | **DISPOSED** — recorded-violation until promoted. Gate never enforces the PROPOSED field's semantics; it enforces acknowledgment presence. See §KL-4 Disposition. |
| KL-6 `tcfQuarkViolations` | unspecified | **NARROWED** — shape specified as a filtered SHACL validation report (companion spec §6). |
| KL-9 chained crossing | unspecified | **NARROWED** — PC#9 → PC#8 composition note in Appendix A. |
| Record | intent + completion | + `surfaceValidationStatus` on completion record; + `tcfShapeVersion` on intent record. |
| Counter-Pass program | none | **DECLARED** — §Counter-Pass Program (criterion + lane). |

Everything not listed carries unchanged from v0.1.

## Change Log — v0.2 → v0.2.1 (2026-08-25, Counter-Pass iteration 1 reconciliation)

Source: `counter-pass-pc09-critic-iteration-1-v0-2_2026-08-25.md` (⚑ MEMORY-ABSENT / UNGROUNDED) reconciled in `producer-reconciliation-pc09-v0-2-iteration-1_2026-08-25.md`. Every change is a narrowing; no constitutive property was found absent.

| Row | Change |
|---|---|
| L1 arbiter-freedom | **Accept.** `surfacePublishedRequirement` → R (`unresolved` permitted); new `surfaceRequirementSnapshot` (resolved value + `resolvedAt` + digest); invariant 1 time-indexed at issuance; KL-12 scoped to raises. |
| L1 `surfaceValidationStatus` | **Accept.** Reading rule: `validated` = surface's own requirement, never a TCF-tier validation; `unknown` does not block completion. |
| L2 defaults | **Narrow.** `cms-enumerable` class definition tightened; default retained but invariant 5 requires `enumerabilityBasis` for any `exposure-upper-bound` grant (fails closed); class marked unevidenced. Option (ii), chosen over (i) on Artifact B's symmetric `boundType` rule. |
| L2 monotonic rule | **Narrow.** `declaredBoundType` closed to the two exposure values; which record named (intent: gate step 8; completion: producer discipline, widening recorded); Artifact B CP-F1/CP-F3 cross-reference added. |
| L2 `atproto-pds` | **Narrow.** Class-individuation rule added; class definition sentence added; token not renamed. |
| L3 stale shape | **Narrow.** KL-13 registered; reading rule for `tcfComplianceTier`; `tcfShapeDigest` on grant, gate step 2 verifies digest; `grantHorizon` SHOULD NOT exceed shape review window (MUST queued to companion §8 / GSEF PP-OI). |
| L4 step 4 | **Accept.** Retitled "Declared status consistent"; `tcfComputedStatusWitness` added; KL-11 order fixed by `tcfShapeVersion` pin; `tcf:statusStale` must be false; named-escape sentence in Carry-In. |
| L4 `evidenceDecay` | **Accept.** `confirmed` derivation names the member verification record (companion §3.3/§7.5) and states the Q6 ceiling; fail-closed block noted as backstop. |
| L5 ack presence | **Accept.** `registerAcknowledgment` folded into `operatorAcknowledgment`, defined as entry references `{nodeId, quarkId, reportDigest}`; gap 3 marked deferred; record-claim-not-gate-claim stated. |
| L5 SHACL | **Narrow.** SHACL provenance stated (inherited from TCF v1.7 Seam 1 via companion); RA decoupling out of lane → flag F-1 queued to KL-10 sequence. |
| M3 | **Accept.** Seam Trigger destination list narrowed to the three surface classes; Automerge share struck. |

## Change Log — v0.2.1 → v0.2.2 (2026-08-25, Counter-Pass iteration 2 reconciliation)

Source: `counter-pass-pc09-critic-iteration-2-v0-2-1_2026-08-25.md` (⚑ MEMORY-ABSENT / UNGROUNDED) reconciled in `producer-reconciliation-pc09-v0-2-1-iteration-2_2026-08-25.md`. Convergence **not met** at iteration 2 (five new in-lane attacks). Every change is a narrowing; no constitutive property was found absent. Five of six iteration-1 rejections conceded by the critic; one (R6-e) contested and reconciled.

| Row | Change |
|---|---|
| R6-e horizon ≤ review window | **Accept ground 2 ✓ / concede ground 1 / narrow, re-grounded.** KL-13 now cites invariant 2 (unconditional) for its bound and invariant 6 as the tightening. Invariant 6 rewritten: the GSEF lineage record (unified crossing-record schema §3.2) carries **no review-window field** — `deprecationHorizon` is the nearest and is set at the corrective change, after issuance. SHOULD stands on that ground; MUST is queued to the GSEF lineage schema (a forward review-window field must exist first), not to companion §8. |
| N1 `enumerabilityBasis` pointer | **Accept.** Field takes the snapshot shape: `{ basisRef, resolvedAt, sourceDigest, cardinality \| memberSetDigest }`. Readership widening mid-horizon registered as **KL-14** (KL-12-class: not gate-visible; completion-record widening obligation is the only disclosure). |
| N2 symmetric rule half-written | **Accept.** Invariant 5 rewritten as a two-direction issuance rule (5a basis required; 5b upper-bound on a non-enumerable class fails closed as overclaim; 5c unbounded on `cms-enumerable` is a class misfit, fails closed). Defaults are **non-overridable**: `declaredBoundType` MUST equal the class value. Fourth case (authenticated, non-enumerable CMS) named **out of declared scope**. |
| N3 "blocks (silence blocks)" | **Accept.** Reworded: an unclassified target has no admissible class; a grant naming `atproto-pds` for it is a misdeclaration under the Q6 ceiling — legible at completion at best, never gate-visible. Third escape (class misdeclaration) added to Carry-In. |
| N4 intent record ↔ grant join | **Accept, narrowed.** Join key exists by inheritance: `grantReference` is Required on every gate-check instance (unified schema §3.1, invariant C1) — it lives in the instance fields, not the provenance-linkage group. Named in the intent-record table; `tcfShapeDigest` copied onto the intent record; auditability claims restated as "from the record joined to its referenced grant." |
| N5 step-6 entry producer | **Accept.** The grant-relative register mismatch entry is **gate-minted** at step 6 (`quarkId: tcf:q/register/grant-requirement`, PROPOSED; `reportDigest` over `{ grantReference, tcfRegisterRequirement, tcfRegister }`), distinct from the store-produced §7.4 declared-vs-computed entry. Digest is deterministic from values the author holds before submission, so the acknowledgment can reference it ahead of minting without templating. Companion §6/§9 amendment queued (v0.1.1). |
| Concessions | R4-b, R5-b, R6-c, R7-c, R10-b conceded by the critic; no text change beyond what iteration 1 already applied. |

## Change Log — v0.2.2 → v0.2.3 (2026-08-27, Counter-Pass iteration 3 reconciliation — pass halted non-converged)

Source: `counter-pass-pc09-critic-iteration-3-v0-2-2_2026-08-27.md` (⚑ MEMORY-ABSENT / UNGROUNDED) reconciled in `producer-reconciliation-pc09-v0-2-2-iteration-3_2026-08-27.md`. Convergence **not met** at iteration 3 (four new in-lane attacks A–D) — **mandatory halt under G11**; the non-convergence is logged as a finding (SL-0162); a fresh pass is a separate session under brief v1.2. Every change is a narrowing; no constitutive property was found absent. Producer ~ calls 1 and 3 survived without attack; 2 and 4 narrowed (via B, C). No new fields, gate steps, or surface classes were added.

| Row | Change |
|---|---|
| A KL-14 disclosure null path | **Accept.** KL-14 rewritten: the completion-record widening obligation fires only on a `boundType` *value* change; within-bound readership widening has **no in-record disclosure path** — auditability is external-only (the `enumerabilityBasis` snapshot joined to the surface's historical ACL). Grant-table cross-reference corrected. A completion-side basis re-resolution (`enumerabilityBasisAtCompletion`) is **queued as a design question, not applied** — under it the `cardinality \| memberSetDigest` alternation becomes load-bearing. |
| B step-6 templating claim | **Accept.** "Cannot be templated" / "cannot pre-fill" struck as applied to the gate-minted entry: `reportDigest` is a per-grant constant and every triple component is computable before submission. What survives is the **per-object recorded assertion** (bound to grant, declared register, and object via `nodeId`), not a friction mechanism. Step 6 now specifies the minted `nodeId` = **the submitted root node**. Non-templatable digest input (needs a two-phase gate?) queued. |
| C pair-relative declared scope | **Accept.** Individuation rule amended: class membership is a property of the **(author, surface) pair at issuance** — surface behaviour plus, where the class definition requires it, issuance-time author resolvability. Inert for `public-web` / `atproto-pds`. `cms-enumerable` row and Seam Trigger scope restated as pair conditions; the "fourth CMS" exclusion corrected — an SSO-gated CMS **is reachable** for an author who can resolve readership at issuance; the excluded thing is the pair in which the author cannot. |
| D severity source | **Accept, critic's fix adopted.** `tcf:q/register/grant-requirement` is to be registered in the pinned shape library as a **declared-but-not-evaluated Quark carrying its severity**; gate step 6 reads severity from the library at the pinned version instead of minting a literal. `tcf:register` promotion then flips severity by shape-version bump, as the KL-4 Disposition claims; the entry's `shapeVersion` field becomes meaningful. Companion v0.1.1 amendment **scope extended** (§2.3/§6). |
| ~3 precision (producer-initiated) | Invariant 6's declarer bound: "declared **in the GSEF lineage record for the pinned version**" — exactly vacuous until that schema defines the field. Adopted from the critic's out-of-lane precision note on the producer's own authority. |

## Change Log — v0.2.3 → v0.2.4 (2026-08-27, fresh Counter-Pass iteration 1 reconciliation)

Sources: critic context A `counter-pass-pc09-critic-fresh-iteration-1-v0-2-3_2026-08-27.md` and context B `pre-existing-six-attack-critic-file-found-at-output-path_2026-08-27.md` (both ⚑ MEMORY-ABSENT; ⚑ UNGROUNDED; ⚑ SINGLE-CONTEXT), reconciled as a union with divergence table in `producer-reconciliation-pc09-v0-2-3-fresh-iteration-1-two-context_2026-08-27.md` (supersedes the same-date single-context reconciliation, which was never canonical). Convergence **not met** at fresh-pass iteration 1 (seven attack substances across the two contexts; iteration 2 pending — no halt arises at it-1). Every change is a narrowing; no constitutive property was found absent in either context. No new fields, gate steps, or classes.

| Row | Change |
|---|---|
| 1a alternation load-bearing under (i) | **Accept.** "Load-bearing only under (ii)" struck. Grant table / invariant 5a now scope the alternatives: `cardinality` grounds the *size* of the bound only; `memberSetDigest` grounds *membership* — membership substitution (same count, rotated readership) is externally auditable only where the snapshot carried `memberSetDigest`. |
| 1b external path conditional | **Accept.** KL-14 disclosure rewritten as conditional: auditable only where the surface retains a queryable ACL history the reader can access; otherwise within-bound widening is **undisclosed and unauditable**. |
| 2 triple binds node, not crossing | **Accept, precision.** Step 6 / KL-4 state the binding exactly: the acknowledgment triple binds (grant, declared register, root node); binding to *this* crossing is the enclosing intent record's `recordId`; the same triple recurs on later crossings of the same node. What Comes Next 10(B) (two-phase / non-templatable input) **closed: not required** — the disposition as written needs no anti-templating property. |
| 3a parenthetical propagation | **Accept.** `targetSurfaceClass` row: "individuated by behaviour plus pair-relative resolvability at issuance, see OQ-3." |
| 3b author basis lapse unnamed | **Accept.** **KL-15 registered** (KL-12-class): in-horizon loss of author resolvability — not gate-visible, not recordable, and (per 1b) not externally auditable. |
| 4a severity inert in gate | **Accept, reading (ii) adopted.** Step 6 / KL-4: the shape-version bump changes what the record *says*, not what this gate *does* — this gate remains acknowledgment-gated for this entry class at any severity; whether a promoted `tcf:register` blocks is a property of the enforcement surface the promotion session names. |
| 4b pre-record library | **Accept.** Step 6: pinned library lacking the `tcf:q/register/grant-requirement` Quark record → block (silence blocks; no acknowledgment can cure it). Companion v0.1.1 restated as a **hard precondition for grant issuance**. |
| 5 register "at or above" undefined | **Accept, confirmed new** (settled-check against it-1/it-2 transcripts: never previously raised). OQ-2 / invariant 1: the ≥ comparison binds **tier only**; the register half is deferred to `tcf:register` promotion (KL-4); the snapshot's `register` value is carried as evidence for that future comparison. |
| **Two-context addendum (same iteration; re-issue of v0.2.4).** Iteration 1 factually ran as two independent critic contexts (context B: an orphaned six-attack output found at the critic's output path — same kickoff, same date; placed as a parallel run; every adopted claim independently text-verified). Reconciled as a union with divergence table (`producer-reconciliation-pc09-v0-2-3-fresh-iteration-1-two-context_2026-08-27.md`). Not a Panel Pass (none declared); the SINGLE-CONTEXT stamp is unaffected. | |
| B#1 A↔C collision | **Accept ✓.** KL-14's "exits the class" gloss deleted — no post-issuance event exits a class fixed at issuance (it-3 C); the completion `boundType` re-assessment stated as an author declaration with no defined completion-time basis in v0.2.x (Q6 ceiling). |
| B#3 two-phase mis-posed | **Accept ✓ — reverses this iteration's own 10(B) closure.** Re-posed as the content-digest input question (pre-computable, non-templatable, no second phase); queued, not applied. |
| B#4 legible-never + ill-formed pair | **Accept ✓.** Carry-In third escape split by criterion: behaviour-misdeclaration legible at completion *at best*; resolvability-misdeclaration legible **never** (only issuance witness = 5a snapshot; `cardinality` arm is an author integer — third load-bearing instance). `targetSurface` MUST be a URI for `cms-enumerable`. 5c reworded to the pair grain. |
| B#6 digest-copy contradiction | **Accept ✓ — reverses context A's clearance of the OQ-6 digest copy.** "Without the grant join" struck (contradicted the adjacent `grantReference` row and N4); the copy stated as an unverified duplicate, step 2 never checks it, writer queued to Phase 0. |
| B#2, B#5 | Convergent with rows 1a/1b and 4a — no additional change; 4b's stricter treatment (context A) stands. |

## Change Log — v0.2.4 → v0.2.5 (2026-08-27, fresh Counter-Pass iteration 2 reconciliation)

Source: `counter-pass-pc09-critic-fresh-iteration-2-v0-2-4_2026-08-27.md` (⚑ MEMORY-ABSENT / UNGROUNDED / SINGLE-CONTEXT — NOT PANELED) reconciled in `producer-reconciliation-pc09-v0-2-4-fresh-iteration-2_2026-08-27.md`. Convergence **not met** at fresh-pass iteration 2 (three new in-lane attacks, all accepted as narrowings). No constitutive property found absent. Six consecutive iterations of fix-introduced surfaces.

| Row | Change |
|---|---|
| 1(i) Step 6 / WCN 8 — issuance-scope overclaim | **Accept ✓.** "Hard precondition for grant issuance" replaced with fire-time framing: "a precondition for any register mismatch to resolve via acknowledgment — a grant issued against a library lacking this Quark record will block uncurably at step 6 on every register mismatch for its full horizon." WCN 8 updated to match. |
| 1(ii) Register misdeclaration cure under missing-Quark block | **Accept ~, queued.** Misdeclaration-cure path confirmed structurally; Particle-tier sub-claim ~. Named as **WCN 10(D)** — fourth Carry-In escape candidate (register misdeclaration to evade a missing-Quark block) queued to fresh-pass it-3. Not added to Carry-In text at this step. |
| 2 Step 5 predicate scope vs. gate-minted entries | **Accept ✓.** Step 5 scoped to store-produced entries: one sentence added after the predicate stating that gate-minted entries (step 6) are added after step 5 runs and are not subject to its predicate. KL-4 Disposition: record-readability note added. "Inert by step order" (reading ii, 4a) survives unchanged. |
| 3 Pair grain / step 1 class-match / it-3 C + B#4 composition | **Accept ✓ — option (B) minimum-surface fix.** §Grant Model opening sentence qualified: URI grants → (author, surface) pair; class-identifier grants → (author, class) coverage. Seam Trigger qualified identically. Step 1: two-sentence annotation — URI grants: surface URI match; class-identifier grants: class-membership check against the declared class, not the individuation criteria (OQ-3 preserved). OQ-3 individuation note: one sentence added. |

## Change Log — v0.2.5 → v0.2.6 (2026-08-27, fresh Counter-Pass iteration 3 reconciliation — FRESH PASS HALTED NON-CONVERGED, second halted pass)

Source: `counter-pass-pc09-critic-fresh-iteration-3-v0-2-5_2026-08-27.md` (⚑ MEMORY-ABSENT / UNGROUNDED / SINGLE-CONTEXT — NOT PANELED) reconciled in `producer-reconciliation-pc09-v0-2-5-fresh-iteration-3_2026-08-27.md`. Convergence **not met** at fresh-pass iteration 3 (three new in-lane attacks A, B, C, all fix-introduced or fix-exposed) — **mandatory halt under G11; second halted pass; finding logged SL-0174**. Stamp not lifted. Every change is a narrowing; no constitutive property was found absent. Seven consecutive iterations of fix-introduced surfaces across both passes. Successor: targeted design session on gate-steps operational language (§What Comes Next, item 1).

| Row | Change |
|---|---|
| A Step 1 "class-membership check" → "consistency check" | **Accept.** The annotation introduced in fresh it-2 attack 3 used "class-membership check," implying a live evaluation of class membership by the individuation criteria — contradicting OQ-3's statement that "the gate never tests the individuation criteria." Correct to "Q6-ceiling consistency check": the gate compares the submission target against the declared class, not against an independently evaluated class assignment. "Class-membership check" struck throughout; "consistency check" with explicit Q6-ceiling framing substituted. OQ-3 individuation note updated correspondingly. |
| B Acknowledgment-validity timing stated explicitly | **Accept.** Fix 2 (fresh it-2) split report assembly into two ordered moments — §6 filtering (store entries, before step 5) and the gate-owned write at step 6 — leaving the `operatorAcknowledgment` validity rule ("checked when the report is assembled") placement unspecified and "invalid" semantics unstated. One sentence added to the `operatorAcknowledgment` table row and a cross-reference added in step 6: "Acknowledgment-reference validity is evaluated once, after step 6 minting, against the full assembled report; an acknowledgment referencing no entry at that point blocks (silence blocks)." |
| C1 OQ-2 register operands | **Accept ✓.** One sentence added to OQ-2: "The step-6 register comparison has no external operand in v0.2.x: both `tcfRegister` (author-declared on the object) and `tcfRegisterRequirement` (author-set on the grant) are author-authored values; the surface's register value is carried as unconsumed evidence in `surfaceRequirementSnapshot`." |
| C2 Gap 3 citation corrected | **Accept ~.** "The Problem It Solves" gap 3: "carried as a recorded mismatch (companion spec §7.4)" corrected to "recordable by join from intent record to grant, where the author's `tcfRegisterRequirement` happens to differ from the object's `tcfRegister`; §7.4 records declared vs computed register — a distinct comparison." |
| C3 WCN 10(D) closed as non-escape; witness split stated | **Accept ✓.** WCN 10(D) closed: "Register misdeclaration to evade a missing-Quark block" is dominated by ordinary permitted grant-issuance (setting `tcfRegisterRequirement` = `tcfRegister` at issuance, which invariant 1 permits outright) — not a distinct escape. Do not add a fourth Carry-In escape. Instead, witness split stated: the register branch has no external anchor in v0.2.x; Particle-tier `tcfRegister` is unwitnessed; composite-tier `tcfRegister` is witnessed by the store's §7.4 declared-vs-computed entry (a distinct comparison). Stated in OQ-2 and KL-4 Disposition. |

---

## What This Entry Is — and Is Not

v0.1 was blue-sky speculative intent. v0.2 is the same design carried through a governed drafting session: every open question has a written disposition, the grant and gate have field-level shape, and the document is Counter-Pass-ready. v0.2.x carries four Counter-Pass iterations of narrowing across two passes, both halted non-converged at their G11 ceilings (SL-0162, SL-0174). v0.3 is the same design with §The Gate rewritten from a convention document (SL-0178); the third Counter-Pass closed at iteration 1 CONVERGED WITH NARROWING (SL-0180; operator close 2026-08-28). The stamp is lifted. It is still un-prototyped.

- **Every resolution here is ~** (single-context, governed session, no adversarial pass) except OQ-5, which is ✓ by live-index read.
- **No generality claims.** The cluster-level NI-5 closure (SL-0128) applies to the substrate-crossing domain's evidence; it does not transfer to this domain, which has none. This entry adopts the same discipline by its own posture: local-first specific, one reference target-surface class demonstrated (AT Protocol PDS, via PC#8 evidence), nothing beyond it claimed.
- **Artifact B and the TCF are untouched.** The companion runtime spec is a *runtime* companion to the TCF, not an amendment; TCF v1.7's stubbed items remain stubbed and are queued to a TCF v1.8 session.
- **The RA connection is unchanged** — motivation, not claim (see v0.1 §RA Pre-Registration Claim, carried).
- **SHACL is inherited, not chosen here.** It comes from TCF v1.7 Seam 1 (CONFIRMED, v0.4.1 Bundle Schema) via the companion runtime; PC#9 makes no independent validator choice and claims no use-case-native justification for it. Schema-checkability is the property the gate needs; SHACL is how the inherited runtime delivers it. *(Counter-Pass it-1, L5.)*

Per PC#0's conformance requirements this document cites PC#0 as parent, specifies divergences from the four constitutive properties, names the seam trigger, and adopts `seam:CrossingRecord` as the base shape.

---

## The Pattern in One Sentence

The governed content production crossing is the boundary event that fires when a content object is submitted from a local-first, author-controlled substrate to an externally legible surface, and the architectural argument is that the crossing must be **granted (standing, horizon-bounded), gated (per-object, against schema-checked TCF tier compliance computed on the author's side), and recorded (per-object intent and completion) before it fires** — making TCF tier boundaries enforcement gates rather than editorial conventions.

---

## The Problem It Solves

Carried from v0.1 (four gaps: intent unrecorded; tier compliance editorial not enforced; `tcf:register` has no enforcement home; TCF cannot make the RA claim without schema-checkable boundaries) — with one correction. **Gap 3 is deferred, not addressed, in v0.2.x:** the KL-4 disposition gives `tcf:register` a *recording* home, not an enforcement home. v0.1's `governed-internal` → public-surface block is carried as a recorded mismatch (companion spec §7.4), not a block, until promotion. *(Counter-Pass it-1, A5.1.)*

One sharpening from this session's evidence. The target surfaces this pattern crosses to do not reliably enforce the author's schema. On the one surface class already crossed under PC#8, the PDS validates records against a Lexicon only when it knows the Lexicon; unknown Lexicons are written anyway ("fail-open"), and the response flags whether validation happened (`validationStatus: valid | unknown`). PC#8 finding A7 corroborates this from the prototype: the one write failure observed was client-side NSID validation, not PDS-side. **The surface is not an arbiter of the author's schema.** Enforcement that depends on it is not enforcement. That fact decides OQ-2 (below) and is why the gate lives on the author's side.

**Gap 3 status correction *(fresh it-3, C2)*:** "v0.1's `governed-internal` → public-surface block is carried as a recorded mismatch." This overstates. In v0.2.x the gap-3 scenario (a `governed-internal`-declared object on a `public-web` surface) mints a step-6 register entry **only if** the author's `tcfRegisterRequirement` on the grant differs from the object's `tcfRegister` — both author-authored values with no external operand (OQ-2). Companion §7.4 records declared vs *computed* register — a distinct comparison concerning the object's own compositional need, not its surface exposure. The gap-3 scenario is therefore **recordable by join** (intent record → grant → `tcfRegisterRequirement` vs `tcfRegister`), where those values happen to differ, not recorded as an entry in the general case.

---

## The Seam Trigger

Carried from v0.1: the seam fires on **publication submission** from a local-first author-controlled substrate to an externally legible surface, carrying a TCF tier-compliance declaration. Non-firing state changes carry unchanged (local edits; peer sync; intra-workflow tier promotion; same-instantiation export → PC#7).

**Amendment (v0.2.1, Counter-Pass M3).** The destination list is the three named surface classes in §Vocabulary (`cms-enumerable`, `public-web`, `atproto-pds`). v0.1's "public Automerge document shared outside the author's controlled subnet" is struck: it has no confirming counterparty and so cannot complete under this pattern; a share that leaves the capability-governed peer set for a differently-governed regime is a PC#8 substrate-crossing question, not a content-production crossing. **Declared scope: three surface classes, one evidenced.** Assessment grain: **per (author, surface) pair where `targetSurface` is a URI (`cms-enumerable`); per (author, class) where it is a class identifier (`public-web`, `atproto-pds`)** *(it-3, C; fresh it-2, attack 3)*. The scope boundary is a **pair condition, not a surface type** (for `cms-enumerable`): an authenticated CMS whose readership the *issuing author* cannot resolve at issuance (SSO-gated; roles held elsewhere) yields a pair that fits none of the three classes, and no class is minted for it here. The same CMS is in scope as `cms-enumerable` for an author who *can* resolve readership at issuance — class membership is a property of the pair (OQ-3, class individuation). A grant naming any v0.2.x class for a pair outside its class is a misdeclaration (OQ-3). *(Counter-Pass it-2, N2; it-3, C.)*

One addition, from the runtime companion: **tier promotion inside the author's substrate is not a crossing, but it is a gated write.** The write-time epistemic status gate (companion spec §5) fires on every write to the Quark-governed store; the PC#9 gate fires once, at submission. Two gates, two events, one shape library.

---

## Carry-In: What This Entry Inherits Unchanged

Carried from v0.1: finality-arbiter-free constraint; Q6 lock (`lineageAnchorType: author-declared`); `seam:CrossingRecord` base shape (identity, provenance linkage, lineage anchoring, evidence scope groups); boundary principles P8–P14 (PROPOSED, Lexicon v2.4); gate fails closed.

**Gate qualification (carried, restated):** the gate checks the compliance declaration and the presence of required fields against pinned shapes. It cannot verify authorial good faith. Under Q6, author-declared is the ceiling. Three escapes are named: inflating member Particles' declared statuses, or declaring nothing `time-sensitive` — both legible in the store but not gate-visible; and **misdeclaring `targetSurfaceClass`** — the gate reads the author's class, never evaluates the individuation criteria, so a wrong class passes every step. Its completion-legibility splits by criterion *(fresh it-1, B#4)*: a **behaviour-criterion** misdeclaration is legible at completion *at best* (`surfaceValidationStatus`, the surface's own response, can contradict the declared class); a **resolvability-criterion** misdeclaration (`cms-enumerable`) is legible at completion **never** — no completion field can reveal that the issuing author could not resolve readership; the only issuance witness is the 5a basis snapshot, whose `cardinality` arm is an author-supplied integer. **The gate makes manipulation enumerable, not impossible.** *(Counter-Pass it-1, A4.3; it-2, N3; fresh it-1, B#4.)*

---

## Open Question Dispositions

### OQ-1 — Grant model: **hybrid** ~

**Decision (operator, 2026-08-24):** standing grant, scoped author × target surface × minimum tier, renewed on a horizon; per-object gate check emitting a per-object intent/completion record pair.

**Grounding.** This is the capability-model default the local-first ecosystem already runs on, not a novelty. UCAN separates a standing *delegation* — carrying `exp` and optional `nbf` time bounds — from a per-action *invocation*, which must carry a unique CID checked against a local store of unexpired hashes to prevent replay. The UCAN revocation spec states the posture directly: proactive expiry through time bounds is preferred; revocation is the last line of defense. Keyhive is in the same capability family. AT Protocol's OAuth-scoped session over per-record `createRecord` writes is the same split at the surface edge. The standing grant is the delegation; the per-object gate is the invocation; the intent record is the unique, replay-resistant artifact.

**Caveat carried at operator request:** alignment with practice is not validation. The *content-tier gate* riding on this split has no precedent this session could cite. Status ~ until a prototype emits a real record pair.

**What it changes.** KL-1 narrows from "unspecified" to "specified, unprototyped." The grant field group (§Grant Model) is the deliverable.

### OQ-2 — Threshold-setter: **layered** ~ — Counter-Pass lane item 1

**Resolution:** the target surface *publishes* its tier/register requirement as data (a Lexicon, a CMS content-type policy document, a surface-class default). The author *sets* `minimumTcfTier` and `tcfRegisterRequirement` on the standing grant at or above that published requirement. The gate checks the author's values. The completion record carries `surfaceValidationStatus` recording what the surface actually did — as evidence, never as a gate condition. **Scope of "at or above" (fresh it-1, row 5):** the ≥ comparison is defined and enforced for **tier only** (invariant 1). No register ordering exists in v0.2.x — `tcf:register` is unruled (KL-4) — so the register half of "at or above" is **deferred to promotion**; the snapshot's `register` value is carried as evidence for that future comparison and is consumed by nothing today. **The step-6 register comparison has no external operand in v0.2.x:** both `tcfRegister` (author-declared on the object) and `tcfRegisterRequirement` (author-set on the grant) are author-authored values; the surface's register value is carried as unconsumed evidence in `surfaceRequirementSnapshot`. A step-6 mismatch entry therefore records the author contradicting the author's own grant requirement, not a surface-relative mismatch. **The register branch has no external anchor in v0.2.x; Particle-tier `tcfRegister` is unwitnessed** (no companion §7.4 entry covers Particle-tier objects — §7.4's declared-vs-computed entry is a composite-tier store operation); composite-tier `tcfRegister` is witnessed by the store's §7.4 declared-vs-computed entry — a distinct comparison from the gate's grant-requirement comparison. *(fresh it-3, C1/C3.)*

**Why layered and not surface-set.** The finality-arbiter-free constraint forbids a coordinating party at record-emission time. A surface-set threshold makes the surface that party. The fail-open evidence above makes the point sharper: a surface-set threshold would be a threshold the surface may not even check. Layering keeps person-side enforcement by construction: the surface's requirement is an *input* to the author's grant, and the record makes visible whether the surface independently validated.

**Why not author-only.** Author-only loses the surface's requirement entirely and makes a mismatch invisible until rejection. Layered records the requirement the author was setting against — as a *resolved value* (`surfaceRequirementSnapshot`), not merely a pointer, so the comparison remains auditable after the surface's requirement drifts. `surfacePublishedRequirement` is required, with `unresolved` as a permitted value: absence is a state the gate sees, never a silent author choice. *(Counter-Pass it-1, A1.1/A1.2.)*

**Third-party (editor/publisher) is not excluded** — it composes as a P13 multi-party governance case (a threshold set by consent record) and is out of scope for the reference implementation.

**Counter-Pass lane:** the critic may attack whether "surface publishes, author sets ≥" actually preserves finality-arbiter-freedom when the surface's published requirement changes mid-horizon, and whether `surfaceValidationStatus` is honestly evidence rather than a disguised gate.

### OQ-3 — `boundType`: **`declaredBoundType` on the grant, per surface class, monotonic** ~ — Counter-Pass lane item 2

**Resolution:** `declaredBoundType` is a required field on the standing grant, set per target surface class. Surface-class defaults for the reference implementation:

| Surface class | Default `declaredBoundType` |
|---|---|
| `cms-enumerable` — CMS whose readership is enumerable by the issuing author at issuance (ACL or counterparty set resolvable author-side). **Membership is a pair property (it-3, C):** a (author, surface) pair in which the author cannot resolve readership at issuance is not in this class, whatever the surface's behaviour — the same surface may be `cms-enumerable` for one author and out of declared scope for another (see Seam Trigger, declared scope). **Unevidenced class** — no prototype crossing. | `exposure-upper-bound` — **only with an `enumerabilityBasis` snapshot (invariant 5a); `exposure-unbounded` on this class is a class misfit and fails closed (5c)** |
| `public-web` — unauthenticated CMS, Ghost, static site. Non-enumerable by definition. | `exposure-unbounded` — **`exposure-upper-bound` on this class fails closed as overclaim regardless of basis (5b)** |
| `atproto-pds` — AT Protocol PDS, **public record, relay-distributed**. Non-enumerable by definition. A permissioned-space or non-relayed PDS record is not this class; it **has no admissible class in v0.2.x**. A grant naming `atproto-pds` for such a target is a misdeclaration under the Q6 ceiling — the gate does not evaluate the individuation criteria and cannot see it; it is legible at completion at best (Carry-In, third escape). Evidenced by PC#8. | `exposure-unbounded` (matches PC#8) — **`exposure-upper-bound` fails closed as overclaim (5b)** |

**Class individuation (amended it-3, C).** A surface class is individuated by gate-relevant behaviour — its fail mode, its credential model, and what it validates against — not by host infrastructure; a surface whose behaviour differs on any of these is a different class even on the same host *(Counter-Pass it-1, L2 Verdict C)* — **plus, where the class definition requires it, issuance-time author resolvability.** Because grants are issued per (author, surface) pair (§Grant Model), class membership is a property of **the pair at issuance**, not of the surface in itself. For `public-web` and `atproto-pds` the resolvability criterion is inert (non-enumerable for every author); for `cms-enumerable` it is the criterion. *(Counter-Pass it-3, C.)* The class is **author-set at issuance and not gate-evaluated**: no gate step tests the individuation criteria against the live surface or the pair. **For class-identifier grants (`public-web`, `atproto-pds`), gate step 1 performs a Q6-ceiling consistency check against the author's declared class — it checks whether the submission target is consistent with the declared class, not whether it would be independently assigned to that class by evaluating the individuation criteria.** *(Counter-Pass it-2, N3; fresh it-2, attack 3; fresh it-3, A.)*

**Defaults are not overridable.** `targetSurfaceClass` fixes `declaredBoundType`; the field remains on the grant because the bound is the author's explicit P9 assertion, not a derived value, but a grant whose `declaredBoundType` differs from its class value is invalid at issuance (invariant 5). A tight default is only coherent if it cannot be overridden in either direction — that is the symmetric rule, written in both directions. *(Counter-Pass it-2, N2.)*

`declaredBoundType` ∈ { `exposure-upper-bound`, `exposure-unbounded` } for the reference implementation. These are the two exposure-bound values of Artifact B's four-value `boundType` scale (`exposure-unbounded` < `exposure-upper-bound` < `confirmation` < `attestation`, ordered by admissible claim strength); `confirmation` and `attestation` are review-strength values that do not apply to a gate-check record. Any other value → grant invalid at issuance.

**Ordering rule:** the **intent record's** `boundType` MUST NOT claim a tighter bound than the grant's `declaredBoundType` (gate step 8). A grant declared `exposure-unbounded` cannot mint an intent record claiming `exposure-upper-bound`. The reverse (grant upper-bound, record unbounded) is permitted with the widening recorded as a violation entry. This is Artifact B's symmetric `boundType` rule (CP-F1/CP-F3) applied to the grant/record pair: overclaiming (record tighter than grant) is inadmissible per P9 and blocks; underclaiming (record wider than grant) is a substitution error, recorded. The **completion record's** `boundType` is not gate-visible (step 10): a completion widening beyond the intent record's value is a producer obligation under the Q6 ceiling and MUST be recorded as a violation entry on the completion record. *(Counter-Pass it-1, L2 Verdicts A/B.)*

**Counter-Pass lane:** the critic may attack whether a per-surface-class default is a hidden generality claim, and whether the monotonic rule interacts correctly with the existing `boundType` vocabulary ordering in Artifact B.

### OQ-4 — `evidenceDecay`: **gate-computed when `time-sensitive`; author-declared otherwise; fail-closed** ~

- If `tcfEpistemicStatus = time-sensitive`: the gate computes `evidenceDecay` = min over `time-sensitive` member Particles' `temporalValidity.validUntil` (companion spec §7.5). Missing temporal validity on a `time-sensitive` object **blocks** (fails closed). Under the companion runtime this block is a backstop — Family B rejects the case at write time (§3.2); it is reachable only via store corruption, which `E-STORE-INVALID` catches first.
- If `confirmed`: `evidenceDecay` = min over member Particles' `verificationRecord.recencyWindowEnd` (companion spec §3.3/§7.5). The verifying party (`verifiedBy`) and method are fields on that record; under Q6 the derived value is author-declared-ceiling regardless of the method recorded. If no member carries a recency window, author-declared. *(Counter-Pass it-1, L4 Verdict B.)*
- If `inferred` or `unverified`: author-declared, optional. An absent value is recorded as absent, not defaulted.

Rationale: the gate should compute what the store can compute and never invent what it cannot. This is the same posture as the propagation rule — computed where the inputs exist, declared where they do not, never silently defaulted.

### OQ-5 — Entry number: **#9** ✓

Verified by direct read of `jediwright/local-first-series` at HEAD bb38dc2 (2026-08-21): `pattern-commons/` contains 00, 07, 08, 09. Closed.

### OQ-6 — GSEF relationship: **shape-version-pinned gate; GSEF lineage is Evidence-plane** ~

**Resolution:** the standing grant carries `tcfShapeVersion` — the vocabulary IRI version of the Quark shape library the gate validates against. The gate validates against *that* version only. The intent record carries the same IRI. GSEF lineage records for the Quark shapes are Evidence-plane artifacts the crossing record may reference; they are never gate conditions.

**Consequences.**
1. A GSEF changeClass C or D event on the Quark shapes publishes a new vocabulary IRI. Standing grants pinned to the prior IRI remain valid through their horizon (TCF v1.7 Seam 1 DRAFTED rule: validate against the version governing creation, not a future version). New grants pin the new IRI.
2. Grant renewal at horizon is the natural moment shape-version advancement propagates into gate behavior. No mid-horizon re-pinning.
3. Consistent with GSEF's own fail-safe posture (Lexicon v2.4: absence of a `ResolutionRecord` blocks no gate).
4. Pin-by-IRI is pin-by-content: the companion store's `tcfShapeVersion` changes if and only if its `versionDigest` changes (companion §2.3), and the grant carries that digest as `tcfShapeDigest` — copied onto the intent record (v0.2.2) — so the binding is auditable from the record rather than trusted. Stale-shape exposure — a pinned version later found defective keeps minting through the horizon — is a named limit (KL-13), bounded by `grantHorizon`, disclosed via GSEF lineage on the Evidence plane. *(Counter-Pass it-1, L3.)*

**Why not GSEF-lineage-aware.** A gate that consults lineage at fire time reintroduces a coordination dependency at record-emission time and makes gate behavior a function of a mutable external record. Pinning makes the gate's behavior a function of the grant only.

---

## The Vocabulary Extension (~, PROPOSED)

All values PROPOSED in the Form C sub-register, pending Counter-Pass and Lexicon registration.

### `governanceEvent` value

| Value | Definition |
|---|---|
| `content-production-crossing` | Carried from v0.1 unchanged. |

### Standing grant field group

| Field | Req. | Purpose |
|---|---|---|
| `crossingType: content-production` | R | Discriminant. |
| `grantScope: standing` | R | Distinguishes from PC#7 per-crossing grants. |
| `targetSurface` | R | URI or surface-class identifier — **except for `cms-enumerable`, where it MUST be a URI**: pair-relative class membership needs a definite surface to form the (author, surface) pair, and step 1's match must be a surface match, not a class match *(fresh it-1, B#4 secondary)*. |
| `targetSurfaceClass` | R | `cms-enumerable` / `public-web` / `atproto-pds` (closed; individuated by behaviour **plus pair-relative resolvability at issuance**, see OQ-3 — *fresh it-1, 3a*). Fixes `declaredBoundType` (non-overridable, invariant 5). Author-set; not gate-evaluated. |
| `surfacePublishedRequirement` | R | URI of the surface's published tier/register requirement (Lexicon NSID, policy doc), or the literal `unresolved`. Never absent. |
| `surfaceRequirementSnapshot` | R iff resolved | `{ tier, register, resolvedAt, sourceDigest }` — the requirement value as resolved at issuance, plus a digest of the fetched policy document. What invariant 1 compares against; survives surface drift. |
| `minimumTcfTier` | R | Author-set, ≥ published requirement where one exists. `particle` / `cluster` / `zone` / `structure` / `ecosystem` / `biome`. |
| `tcfRegisterRequirement` | R | Author-set register constraint for this surface. Enforcement per KL-4 disposition: recorded, not blocking. |
| `declaredBoundType` | R | `exposure-upper-bound` / `exposure-unbounded` only (OQ-3). MUST equal the class value (invariant 5). |
| `enumerabilityBasis` | R iff `declaredBoundType: exposure-upper-bound` | **Snapshot, not pointer (v0.2.2):** `{ basisRef, resolvedAt, sourceDigest, cardinality \| memberSetDigest }` — the ACL or counterparty-set reference *and* the readership it resolved to at issuance (a count, or a digest over the canonical member set). Same shape discipline as `surfaceRequirementSnapshot`: the P9 factual assertion stays auditable after the ACL drifts — **by external join to the surface's historical ACL only, where the surface retains one; no record carries a within-bound widening disclosure** (invariant 5a; KL-14). **Alternative scoping (fresh it-1, 1a):** `cardinality` grounds the *size* of the bound only; `memberSetDigest` grounds *membership* — substitution within the bound is externally auditable only where the snapshot carried `memberSetDigest`. |
| `tcfShapeVersion` | R | Vocabulary IRI version pinned for gate validation (OQ-6). |
| `tcfShapeDigest` | R | `versionDigest` of the shape library at issuance (companion §2.3). Verified by gate step 2. |
| `grantHorizon` | R | Expiry. Named distinctly from PC#8's PROPOSED `crossingGrantHorizon` (KL-12 candidate) to avoid pre-empting that field's gate condition; convergence assessed at Lexicon registration. |

The grant is a delegation, not a `seam:CrossingRecord` instance; the record reaches it through the inherited `grantReference` (unified crossing-record schema §3.1, C1). Whether `grantReference` is content-addressed over the grant's canonical serialization is a Phase 0 implementation question. *(Counter-Pass it-2, N4.)*

### Per-object gate check field group (intent record)

| Field | Purpose |
|---|---|
| `tcfComplianceTier` | Declared tier at submission (carried from v0.1). **Reading rule:** asserts compliance relative to the co-carried `tcfShapeVersion` and nothing more. |
| `tcfComputedStatus` | The weakest-status-propagated epistemic status *computed* by the store at submission (companion spec §7), distinct from the declared value. Inherits KL-11's ~ until TCF v1.8 rules the order. |
| `tcfComputedStatusWitness` | **New (v0.2.1).** `{ nodeId, status }` of the weakest member that determined `tcfComputedStatus` under companion §7.1. One lookup makes gate step 4 auditable after the fact. |
| `tcfEpistemicStatus` | Declared status (carried). Gate checks declared == computed for composite tiers. |
| `tcfRegister` | Declared register (carried). |
| `tcfQuarkViolations` | Filtered SHACL validation report (companion spec §6). |
| `operatorAcknowledgment` | **New (v0.2.1; replaces v0.2's `registerAcknowledgment`).** List of entry references `{ nodeId, quarkId, reportDigest }` (companion §6), one per non-blocking `tcfQuarkViolations` entry. An acknowledgment that references no existing entry is invalid. **Acknowledgment-reference validity — each acknowledgment must reference an entry existing in the fully assembled report — is evaluated once, after step 6 minting; an acknowledgment referencing no entry at that point blocks (silence blocks).** This is the acknowledgment-side check, distinct from step 5’s entry-side coverage predicate: step 5 asks “does this entry have an acknowledgment?” (runs before step 6, on store-produced entries); this check asks “does this acknowledgment reference a real entry?” (runs once, after step 6 minting). The two directions are complementary and non-conflicting. *(fresh it-3, B; third-pass it-1, N3.)* **For gate-minted entries the reference triple is computable before submission** — the digest is a per-grant constant and only `nodeId` is per-object — so this validity rule is a record-claim discipline, not an anti-templating mechanism *(it-3, B)*. A *register acknowledgment* is an entry whose target has `constraintClass: register` (KL-4). |
| `tcfShapeVersion` | Copied from grant. |
| `tcfShapeDigest` | **New (v0.2.2; corrected fresh it-1, B#6; writer specified v0.3, N2).** Copied from grant. **Gate-owned: the gate writes this field to the intent record at record assembly** (AF-1; third-pass it-1, N2 — supersedes the v0.2.x “writer queued to Phase 0” note). Gate step 2 verifies the loaded library against the *grant's* digest, never against this copy; the copy exists for auditability by join from the record to its referenced grant. Auditability of step 2 runs *from the record joined to its referenced grant* (N4), consistent with the `grantReference` row below — the v0.2.2 claim \"without the grant join\" is struck as an overclaim. *(it-2, N4; fresh it-1, B#6.)* |
| `grantReference` | **Inherited, named here (v0.2.2).** Required on every gate-check instance under `seam:CrossingRecord` (unified schema §3.1; invariant C1). This is the join key to the standing grant; `surfaceRequirementSnapshot`, `enumerabilityBasis`, and the grant invariants are auditable *from the record joined to its referenced grant*, never from the intent record alone. *(Counter-Pass it-2, N4.)* |
| `evidenceDecay` | Per OQ-4. |

### Completion record additions

| Field | Purpose |
|---|---|
| `surfaceValidationStatus` | `validated` / `unknown` / `not-applicable`. What the surface reported it did (e.g. PDS `validationStatus`). Evidence, not gate. **`validated` means validated by the surface against the surface's own requirement** (e.g. a Lexicon); it is not, and cannot be read as, a TCF-tier validation — a consumer that treats it as corroborating `tcfComplianceTier` has misread the record. **`unknown` does not block completion.** `not-applicable` is set by surface class, which carries this single piece of validation semantics by design. *(Counter-Pass it-1, L1 Verdict B.)* |
| `authorizedContentDigest` | Carried from v0.1. |
| `chainReference` → intent `recordId`; `chainDepth: 1`; `lineageAnchorType: author-declared` | Per `seam:CrossingRecord` lineage group. |

---

## The Grant Model (~)

A standing grant authorizes an author to cross content objects to a target surface (or all surfaces of a target class) at or above `minimumTcfTier`, under one pinned shape version, until `grantHorizon`. **Where `targetSurface` is a URI, the grant is issued once per (author, surface) pair and renewed at horizon. Where `targetSurface` is a class identifier (`public-web`, `atproto-pds`), the grant covers all surfaces of that class the author reaches.** *(fresh it-2, attack 3.)* It is a delegation in the UCAN sense; it does nothing on its own.

**Standing-grant invariants:**
1. `minimumTcfTier` ≥ the tier in `surfaceRequirementSnapshot`, **as resolved at issuance**. **Binds tier only** — the register half of OQ-2's "at or above" is deferred to `tcf:register` promotion (KL-4); the snapshot's `register` is evidence, not a compared value *(fresh it-1, row 5)*. This is a grant-time fact, not a horizon-long invariant (KL-12). Unresolvable → grant records `surfacePublishedRequirement: unresolved`, carries no snapshot, and proceeds on the author's value (the fail-open surface case, made legible).
2. A grant is invalid outside `[issuedAt, grantHorizon]`. Clock drift accounted for at issuance (UCAN posture).
3. A grant pins exactly one `tcfShapeVersion`. Shape-version change does not invalidate an in-horizon grant.
4. Grants are not delegable in v0.2.x. Delegation (author → agent) is a P11/PC#7 composition, out of scope.
5. **Symmetric bound rule, both directions, at issuance.** `declaredBoundType` MUST equal the value fixed by `targetSurfaceClass` (OQ-3 table); any other pairing → grant invalid at issuance. Specifically:
   - **5a.** A grant declaring `exposure-upper-bound` MUST carry an `enumerabilityBasis` snapshot (resolved readership, not a pointer). Absent, or unresolvable at issuance → fails closed; no default is substituted. A tight bound is a factual assertion about the surface's readership (P9) and is admissible only with a recorded, resolved basis. **The snapshot's alternatives assert different facts** *(fresh it-1, 1a)*: `cardinality` asserts the bound's size; `memberSetDigest` asserts its membership. Both support the same `declaredBoundType` value, but the audit each can later ground differs (grant table; KL-14).
   - **5b.** `exposure-upper-bound` on a class defined as non-enumerable (`public-web`, `atproto-pds`) fails closed as **overclaim**, regardless of any basis supplied.
   - **5c.** `exposure-unbounded` on `cms-enumerable` fails closed as a **class misfit**: if the author cannot resolve a basis, the **pair** is not in `cms-enumerable` and has no admissible class in v0.2.x (Seam Trigger, declared scope — pair grain per it-3 C; wording fixed fresh it-1) — reclassification, not substitution.
   *(Counter-Pass it-1, L2 Verdict A; it-2, N1/N2.)*
6. `grantHorizon` SHOULD NOT exceed a forward review window for the pinned shape version **where one is declared in the GSEF lineage record for the pinned version** *(declarer bound it-3; exactly vacuous until that schema defines the field)* — resolved at issuance, never read at fire time. **As of v0.2.3 none is declared anywhere:** the GSEF lineage record (unified crossing-record schema §3.2) carries `deprecationHorizon`, set at a *corrective* change after issuance, and no forward review-window field. This invariant therefore binds nothing today; it states the tightening that applies once such a field exists. Promotion to MUST is queued to the **GSEF lineage-record schema** (a review-window field must be defined before a MUST can bind), not to companion §8, whose open item (whether changeClass D shortens in-flight horizons) is a fire-time question independent of this issuance-time cap. *(Counter-Pass it-1, A3.2; it-2, R6-e — re-grounded.)*

---

## The Gate (~)

Fires once per object, at submission. In order; first failure blocks; silence blocks.

**Step 1. Grant current at act time.**

`assertCapabilityCurrent()` — the gate checks that the grant is within its `[issuedAt, grantHorizon]` window at act time and that the grant's target matches the submission target.

- **URI grants** (`cms-enumerable`): the submission target URI must equal the grant's `targetSurface` URI exactly. Mismatch → block.
- **Class-identifier grants** (`public-web`, `atproto-pds`): the gate performs a **Q6-ceiling consistency check** — it compares the submission target against the author's declared `targetSurfaceClass`, not against an independently evaluated class assignment. The gate does not evaluate the individuation criteria (OQ-3). A submission target inconsistent with the declared class → block.

Grant outside horizon → block.

**Step 2. Shape version resolvable and digest-verified.**

The gate loads the shape library at the grant's pinned `tcfShapeVersion`. The loaded library's `versionDigest` must equal the grant's `tcfShapeDigest`. Cannot load, or mismatch → block. A library fetched on demand from the IRI at fire time does not satisfy this step: the pin binds content, not a location.

The intent record carries a `tcfShapeDigest` field copied from the grant. This copy is **gate-owned: the gate writes it to the intent record at record assembly**. Gate step 2 verifies against the grant's digest, never against this copy; the copy exists for auditability by join from the record to its referenced grant. *(AF-1 resolved.)*

**Step 3. Tier threshold met.**

`tcfComplianceTier` (author-declared on the intent record) must be ≥ `minimumTcfTier` (author-declared on the grant), under the tier vocabulary in the pinned shape library. Below threshold → block. Pass: proceeds silently.

**Step 4. Declared status consistent.**

**Applies to composite tiers (cluster and above) only. For Particle-tier submissions this step is a no-op: the gate proceeds to step 5 without evaluation.** *(AF-2 resolved.)*

For composite tiers: `tcfEpistemicStatus` (author-declared on the intent record) must equal `tcfComputedStatus` (gate-computed from the store at submission time via companion §7) and `tcf:statusStale` must be false (companion §5.2 step 6, §9). The status order is drawn from the pinned shape library (companion §3.4/§7.2); `tcfShapeVersion` fixes which order this check ran under.

- Declared status stronger than computed → block.
- Declared status weaker than computed → passes; recorded as a permitted substitution.
- `tcf:statusStale` true → block.

`tcfComputedStatusWitness` (`{ nodeId, status }` of the weakest propagating member, companion §7.1) is **gate-written to the intent record** regardless of outcome, making the check auditable after the fact.

**Step 5. No blocking Quark violations.**

**Predicate scope: store-produced entries only.** `tcfQuarkViolations` at the time this step runs contains entries assembled by the companion §6 filtering process before this step executes. Gate-minted entries (step 6) do not yet exist and are not subject to this predicate.

For each entry in `tcfQuarkViolations` at this point:

- Entry with `sh:severity sh:Violation` at or above `minimumTcfTier`, with a referencing `operatorAcknowledgment` entry → passes.
- Entry with `sh:severity sh:Violation` at or above `minimumTcfTier`, with no referencing acknowledgment → block.
- Entry below the Violation threshold or below `minimumTcfTier`: acknowledgment is still required. Present → passes and is recorded. Absent → block.

Acknowledgment is required for every entry in `tcfQuarkViolations`, regardless of severity. The gate fails closed on acknowledgment presence, not on the violation itself. *(AF-3 resolved: "non-blocking" described violation severity only, not acknowledgment requirement. That language is retired.)*

**Step 6. Register acknowledged.**

If `tcfRegister` (author-declared on the intent record) equals `tcfRegisterRequirement` (author-declared on the grant) → step passes silently; no entry minted.

If `tcfRegister` ≠ `tcfRegisterRequirement`:

1. The gate checks that the pinned shape library carries a Quark record for `tcf:q/register/grant-requirement` as a declared-but-not-evaluated entry providing `severity`. If the library carries no such record → block; no acknowledgment can cure a missing severity source; a grant issued against a library lacking this record will block uncurably at step 6 on every register mismatch for its full horizon.

2. The gate **mints** the following entry into `tcfQuarkViolations`:
`{ nodeId, quarkId: tcf:q/register/grant-requirement, constraintClass: register, severity, shapeVersion, reportDigest }`
   - `nodeId` is **author-supplied**: it is the id of the submitted root node, a value the author provides for the object. The gate reads it from the submission; it is not independently computed by the gate. *(AF-4 resolved.)*
   - `severity` is read from the pinned library's Quark record for `tcf:q/register/grant-requirement`.
   - `reportDigest` is gate-computed over the canonical JSON of `{ grantReference, tcfRegisterRequirement, tcfRegister }` — a per-grant constant, deterministic from values the author holds before submission.

3. **Acknowledgment-validity evaluation occurs once, after minting, against the full assembled report.** If `operatorAcknowledgment` contains an entry referencing the minted entry → passes; mismatch recorded. If no referencing acknowledgment → block. An acknowledgment referencing an entry that does not exist in the assembled report at this point → block.

The store's §7.4 register entry (declared vs. computed register — a composite-tier store operation) is a separate entry subject to step 5, not this step; it is acknowledged separately.

**Step 7. `evidenceDecay` derivable.**

Gate-computes `evidenceDecay` based on `tcfEpistemicStatus` (author-declared on the intent record):

- `time-sensitive`: gate computes minimum over `time-sensitive` member Particles' `temporalValidity.validUntil` (companion §7.5). Any member missing `temporalValidity.validUntil` → block.
- `confirmed`: gate computes minimum over member Particles' `verificationRecord.recencyWindowEnd` (companion §3.3/§7.5). If no member carries a recency window → author-declared value used.
- `inferred` or `unverified`: author-declared, optional. Absent value is recorded as absent; no default is substituted; no block.

Gate writes the derived or declared value to the intent record.

**Step 8. `boundType` monotonic.**

The intent record carries a `declaredBoundType` field, **author-declared on submission** — the author's P9 assertion about exposure. Invariant 5 fixes the *grant's* `declaredBoundType` per `targetSurfaceClass`; the intent record's value is constrained by the step-8 monotonic rule, not by identity to the grant's value. The gate checks it; it does not write it. *(AF-5 resolved.)*

The intent record's `declaredBoundType` MUST NOT claim a tighter bound than the grant's `declaredBoundType`, using Artifact B's ordering (`exposure-unbounded` < `exposure-upper-bound` < `confirmation` < `attestation`):

- Intent record tighter than grant (overclaim per P9) → block.
- Intent record wider than grant (underclaim): passes; gate **mints a `tcfQuarkViolations` entry** with `constraintClass: boundType-widening` — the gate is recording a bound widening relative to the grant, detected by comparing two author-declared values; the label is parallel to `constraintClass: register` at step 6. *(AF-6 resolved.)*

The completion record's `declaredBoundType` is **not gate-visible**; completion-side widening is a producer obligation under Q6 and must be recorded as a violation entry on the completion record by the author.

**Step 9. Record minted before crossing.**

The intent record must be complete — all gate-owned fields written (steps 2, 4, 6, 7, 8), all author-declared fields present — before the publish call fires. This is a **gate-enforced architectural invariant**: the gate withholds the publish call until record assembly is confirmed complete. Record assembly failure for any reason → block; the publish call does not fire. *(AF-7 resolved: enforcement mechanism is gate-withholds-publish, not a post-hoc check.)*

Q6 applies: the ordering is author-declared in the sense that the author's submission initiates the sequence; the gate's control of the publish call is the mechanism.

**Step 10. Fires exactly once.**

The gate fires once per object at submission. Post-crossing state is not gate-visible (KL-7). The completion record is minted by the author after surface confirmation; its `declaredBoundType` re-assessment is author-declared at completion under Q6.

**This step is an architectural statement, not a fire-time check.** There is no gate predicate that runs at step 10. It is stated as a numbered step to make the gate's scope boundary explicit: the gate's responsibility ends when the publish call fires and the intent record is in place. *(AF-8 resolved: steps 7–10 are all numbered prose steps; steps 7–9 carry block conditions; step 10 is explicitly an architectural statement with no predicate.)*

---

## Gate Properties (carried, restated for completeness)

1. **Grant current at act time.** Per OQ-1/OQ-2.
2. **Shape version resolvable and digest-verified.** Per OQ-6.
3. **Tier threshold met.** Per OQ-2.
4. **Declared status consistent.** Composite tiers only; no-op for Particle. Per companion §5.2/§7.
5. **No blocking Quark violations.** Store-produced entries only; acknowledgment required at every severity. Per companion §6.
6. **Register acknowledged.** Mints gate-owned entry; acknowledgment evaluated post-mint. Per KL-4 Disposition.
7. **`evidenceDecay` derivable.** Per OQ-4.
8. **`boundType` monotonic.** Intent record only; completion not gate-visible. Per OQ-3.
9. **Record-before-crossing.** Gate-enforced via publish-call control. Per KL-3/Q6.
10. **Fires exactly once.** Architectural boundary statement; no predicate. Per KL-7.

---

## The Record (~)

Carried from v0.1 (intent record before the publish call; completion record after surface confirmation), with the v0.2 field additions above. The intent record's `recordId` is the `chainReference` target for the completion record and — under chained crossing — for a downstream PC#8 intent record (Appendix A).

---

## KL-4 Disposition — `tcf:register` is recorded-violation until promoted

`tcf:register` is PROPOSED in UFO Lexicon v2.4 under the plain-register/TCF extension cluster. Its gate condition is a dedicated plain-register spec session. **This session cannot promote it** (queue-don't-reopen; the gate condition belongs to a different session type). Two options were available:

- *Block the gate on it.* Rejected: it would make a PROPOSED term govern output, which Lexicon Collision Prevention rule 6 forbids.
- *Recorded-violation until promoted.* Adopted.

**Mechanics.** The gate does not evaluate register semantics. It evaluates one thing: when the declared register and the grant's requirement differ, is an acknowledgment present *that references the specific mismatch entry*? That is a presence check on a field the gate owns (`operatorAcknowledgment`, bound to `{ nodeId, quarkId, reportDigest }`), not an enforcement of a field the Lexicon has not ruled. **What the binding buys, stated exactly (it-3, B):** for the gate-minted entry the digest is a per-grant constant; every component of the reference triple is computable before submission, and a template can pre-fill everything but `nodeId` — a value the author supplies for the object anyway. The it-1 sentence "a template cannot pre-fill a reference to an entry that does not yet exist" is **struck as applied to gate-minted entries**; it holds for store-produced entries, whose digests are content-dependent. What the check delivers is not friction but a **record claim** — the record carries the author's explicit, mismatch-bound acknowledgment, bound per **node** (`nodeId` = submitted root; the per-*crossing* binding is the intent record's `recordId` — *fresh it-1, row 2*) — **not a gate claim about register compliance.** *(Counter-Pass it-1, L5 Verdict A; it-3, B; fresh it-1, 2.)* The mismatch itself is recorded on the intent record as a `tcfQuarkViolations` entry with `tcf:constraintClass "register"` — **minted by the gate at step 6**, with **severity read from the pinned library's declared-but-not-evaluated Quark record** for `tcf:q/register/grant-requirement` (PROPOSED, runtime-side; companion v0.1.1 queued): the grant-relative comparison has no shape-library *evaluator*, but the library is the severity's *source*. *(Counter-Pass it-2, N5; it-3, D.)* When `tcf:register` is promoted with an enforcement surface named, what changes here is the **severity the record carries** — by shape-version bump (OQ-6), not by editing this gate — and *only* that: severity is behaviourally inert in this gate (step order; step 6 is severity-blind), so the bump changes what the record says, never what this gate does. Enforcement of the promoted term belongs to the surface the promotion session names, not to this gate. *(it-3, D — severity source; fresh it-1, 4a — reading (ii) specified.)* **Record-readability note *(fresh it-2, attack 2)*:** a `tcfQuarkViolations` entry added by step 6 does not retroactively satisfy step 5's block predicate — step 5 evaluated store-produced entries only (gate-minted entries post-date it). An auditor distinguishing store-produced from gate-minted entries should use `constraintClass: register` and `quarkId: tcf:q/register/grant-requirement`; gate-minted entries are correct gate behaviour, not gate failures.

**Register branch witness split *(fresh it-3, C3)*:** the step-6 comparison has no external anchor in v0.2.x (both operands are author-authored — see OQ-2). For Particle-tier objects, `tcfRegister` is unwitnessed: no companion §7.4 entry covers Particle-tier register (§7.4's declared-vs-computed entry is a composite-tier store operation); the only register evidence is the intent record's `tcfRegister` field and the grant's `tcfRegisterRequirement`. For composite-tier objects, `tcfRegister` is witnessed by §7.4's declared-vs-computed entry — but this is a distinct comparison (object's declared vs object's compositional need), not a surface-exposure record. An auditor wishing to reconstruct the surface-relative register picture must join the intent record to its referenced grant.

**Consequence for the "most-restrictive-propagates" rule (v0.1).** Carried as a computed value (companion spec §7.4) so that the register a composite object *would* need is visible in the record now, ahead of enforcement.

---

## Known Limits (~, revised)

| KL | v0.2 status | Closing evidence |
|---|---|---|
| KL-1 | NARROWED — standing grant specified | Prototype emits ≥1 real intent/completion pair under a standing grant |
| KL-2 | NARROWED — shape families + gate read-surface specified (companion) | TCF v1.8 Section B confirms field names; per-tier shapes authored under it |
| KL-3 | unchanged | `timestamp-signed` infrastructure |
| KL-4 | DISPOSED — recorded-violation; narrowed it-3: templating claim struck for gate-minted entries (B); severity sourced from the pinned library's declared-but-not-evaluated Quark (D) | Plain-register spec session promotes `tcf:register` and names enforcement surface |
| KL-5 | CLOSED by OQ-3 resolution (~) — narrowed it-1: vocabulary closed to two values; `cms-enumerable` tight bound requires basis; narrowed it-2: basis is a snapshot; symmetric rule written both directions; defaults non-overridable; narrowed it-3 (C): class membership is a property of the (author, surface) pair at issuance; the scope exclusion is a pair condition, not a surface type | Fresh Counter-Pass (brief v1.2) — the it-1/it-2/it-3 lane survived narrowed three times; the halted pass certifies nothing |
| KL-6 | NARROWED — violation shape specified (companion §6) | Prototype produces a real filtered report |
| KL-7 | unchanged — revision semantics unresolved | Governed design session on content lifecycle; candidate: revision = new crossing, `chainReference` to prior completion record |
| KL-8 | unchanged — AI ingestion out-of-reach | none available |
| KL-9 | NARROWED — Appendix A | Chained prototype run (PC#9 → PC#8) |
| KL-10 | unchanged | separate RA pre-registration sequence |
| **KL-11 (new)** — status ordering unspecified in TCF v1.7 | The weakest-status rule requires a total order over the four locked values; v1.7 does not state one. Companion spec proposes one (~) and queues it. | TCF v1.8 session rules the order |
| **KL-12** — surface requirement drift mid-horizon | If the surface **raises** its published requirement during a grant's horizon, the grant is stale but valid; `surfaceRequirementSnapshot` preserves what the author set against. Not gate-visible by design (OQ-6 posture). A *lowering* leaves the author's stricter value valid and is not a drift event for gate purposes. *(Scoped v0.2.1, Counter-Pass it-1 A1.3.)* | Counter-Pass lane item 1 (survived it-1, narrowed); prototype observation |
| **KL-13 (v0.2.1; citation corrected v0.2.2)** — pinned shape later found defective | A shape version pinned by an in-horizon grant is later found defective by a GSEF corrective change; grants keep minting against it through their horizon. Not gate-visible by design (OQ-6). Disclosure lives in the GSEF lineage record for the corrective change, on the Evidence plane; the join is the reader's. Exposure bounded by `grantHorizon` under **invariant 2** (unconditional); invariant 6 is the tightening that applies where a forward review window is declared — none is, as of v0.2.3. *(it-2, R6-e ground 2.)* | Prototype observation of a corrective shape event during an open horizon |
| **KL-14 (v0.2.2; rewritten v0.2.3, it-3 A)** — readership widening mid-horizon under a tight bound | A `cms-enumerable` pair's ACL or counterparty set widens after issuance. Not gate-visible (the gate reads the grant only — OQ-6 posture); KL-12-class limit. **Disclosure, stated exactly: within-bound widening (the count grows but the surface stays enumerable) has NO in-record disclosure path.** The completion record's widening obligation (OQ-3 ordering rule) fires only on a `boundType` *value* change — and that value, at completion, is an **author-declared re-assessment with no defined completion-time basis in v0.2.x** (`enumerabilityBasis` is issuance-only; no re-resolution field exists): admissible under the Q6 ceiling, legible in the record only as the bare declaration. *(The v0.2.3 gloss "only when the widening exits the class" is deleted — class membership is fixed at issuance (OQ-3, it-3 C), so no post-issuance event exits the class; fresh it-1, B#1.)* Auditability of within-bound widening is **external-only and conditional** *(fresh it-1, 1b)*: the `enumerabilityBasis` snapshot joined to the surface's historical ACL — a reader's join outside the record system, possible **only where the surface retains a queryable ACL history the reader can access; otherwise within-bound widening is undisclosed and unauditable.** The alternation is load-bearing for this audit **now, under option (i)** *(fresh it-1, 1a)*: a `cardinality` snapshot grounds bound-size drift only; membership substitution is auditable only from `memberSetDigest`. A completion-side re-resolution (`enumerabilityBasisAtCompletion`, same snapshot shape) would create an in-record path but adds a field — **queued as a design question, not applied**. *(it-2, N1; it-3, A; fresh it-1, 1a/1b.)* Author-side loss of resolvability is a distinct limit — KL-15. | Fresh pass (design question); prototype observation of an ACL change during an open horizon on a `cms-enumerable` crossing |
| **KL-15 (new, v0.2.4, fresh it-1 3b)** — author resolvability lapse mid-horizon | Class membership is a pair property **at issuance** (OQ-3, it-3 C); an in-horizon loss of the author's ability to resolve the basis (roles revoked; ACL read access withdrawn) makes the pair's class-admissibility fact cease to be true while the grant keeps minting `exposure-upper-bound` intent records against the issuance snapshot. KL-12-class: not gate-visible (OQ-6 posture — correct), not recordable (Q6 — correct), and **not externally auditable** — the surface's ACL history says nothing about the author's read access to it (KL-14's conditional path does not cover it). Surface-side drift is KL-14; this is the author-side lapse the pair-relative individuation created. | Prototype observation of a revoked basis-read permission during an open horizon on a `cms-enumerable` crossing; fresh pass |

---

## Counter-Pass Program (BOTH PASSES HALTED NON-CONVERGED — SL-0162, SL-0174; THIRD PASS CLOSED — CONVERGED WITH NARROWING, SL-0180)

**First pass:** v0.2 it-1 (2026-08-25, reconciled); v0.2.1 it-2 (2026-08-25, not converged: five new attacks); v0.2.2 it-3 (2026-08-27, not converged: four new attacks A–D) — **halted at the G11 ceiling, logged as SL-0162**; stamp not lifted.
**Fresh pass (brief v1.2 — lane opens on the it-3 narrowings):** v0.2.3 under test at iteration 1 (run 2026-08-27, reconciled, not converged: five in-lane attacks, rows 1–5, all accepted as narrowings — v0.2.4 issued two-context). v0.2.4 under test at iteration 2 (run 2026-08-27, reconciled, not converged: three new in-lane attacks — attacks 1(i)/1(ii)/2/3 — all accepted as narrowings — v0.2.5 issued). v0.2.5 under test at **iteration 3** (run 2026-08-27, reconciled, **not converged**: three new in-lane attacks A/B/C — all accepted as narrowings — this file, v0.2.6, is the reconciliation's issue) — **halted at the G11 ceiling, logged as SL-0174; SECOND HALTED PASS; stamp not lifted.** Pattern across both passes: **seven consecutive iterations** in which fixes introduced new surfaces; no constitutive property found absent in any of them. No constitutive property failed across seven iterations — the architectural design is stable; what is unstable is the operational language of the gate steps.

**Convergence criterion:** the critic returns no *new* attack on the four constitutive properties (declared scope, grant, gate, record) as instantiated in §Grant Model, §Gate, §Record, and the six OQ dispositions, within the lane, for one full iteration; *or* iteration 3 completes (mandatory halt; non-convergence logged as a finding).

**Critic's lane (in scope):**
1. OQ-2 layered threshold — finality-arbiter-freedom under mid-horizon requirement drift; `surfaceValidationStatus` as evidence vs. disguised gate.
2. OQ-3 `declaredBoundType` — hidden generality via surface-class defaults; monotonic rule vs. Artifact B `boundType` ordering.
3. OQ-6 shape-version pinning — whether pinning creates a stale-shape exposure the record cannot disclose.
4. Gate step 4 (declared == computed) — whether the check is honest under the Q6 ceiling.
5. KL-4 — whether "acknowledgment presence" is a real gate or a formality.

**Out of lane:** the RA pre-registration section (KL-10; separate sequence); TCF field names (queued to TCF v1.8); PC#0 constitutive properties themselves; any Lexicon promotion.

**Isolation:** fresh siloed project; document + adversarial brief only. Producer reconciliation returns to the main project. Checkpoint fired after iteration 2 (`session-handoff-pc09-counterpass-it2-reconciliation_2026-08-25.md`). Surviving verdicts → ledger deltas; narrowed verdicts recorded as narrowed.

**Third pass (v0.3 candidate, gate-steps rewrite from SL-0178):** v0.3-candidate under test at iteration 1 (run 2026-08-28; critic: CONVERGED WITH NARROWING — no new constitutive-property attack across all five lane items; lane items 1 and 4 clean; three prose narrowings N1–N3 applied by producer reconciliation). **Operator closed at iteration 1, 2026-08-28. CLOSED — SL-0180. Stamp lifted.**

---

## Appendix A — Chained-Crossing Note: PC#9 → PC#8 Composition (KL-9)

**Scenario.** A content object crosses under PC#9 to `targetSurfaceClass: atproto-pds`. The PC#9 gate fires on the author's side at submission. The PC#8 gate fires at the substrate edge on the transition. Two crossings, one sequence.

**Ordering invariant.** PC#9 intent → PC#9 gate pass → PC#8 intent → PC#8 gate pass → publish call → PC#8 completion → PC#9 completion. The PC#9 completion record is minted *last*, because "publication confirmation from the target surface" (PC#9's completion trigger) is exactly what the PC#8 completion record carries.

**Chain wiring.**

| Record | `chainReference` | `chainDepth` | `lineageAnchorType` |
|---|---|---|---|
| PC#9 intent | none (principal seam) | 0 | — |
| PC#8 intent | PC#9 intent `recordId` | 1 | `author-declared` |
| PC#8 completion | PC#8 intent `recordId` | 2 | `author-declared` |
| PC#9 completion | PC#8 completion `recordId` | 3 | `author-declared` |

The PC#9 completion record's `chainReference` points at the PC#8 completion record, not at its own intent record; its own intent is reachable by walking the chain to depth 0. `crossingIntentRef` on the PC#8 intent uses the `intent-sha256:` prefix over canonical JSON (live PC#8 divergence from spec abstract language; KL-SCHEMA cluster) and binds to the PC#9 intent record's canonical serialization.

**What each gate does not check.** PC#9 does not check substrate exposure semantics (PC#8's domain). PC#8 does not check TCF tier compliance (PC#9's domain). Neither re-runs the other's gate. This is Form C chaining: each seam governs its own trigger; composition is by record linkage, not by gate re-execution.

**`boundType` reconciliation.** PC#9's `declaredBoundType` for `atproto-pds` is `exposure-unbounded` (OQ-3 default), which matches PC#8's fixed value. No widening entry is generated. A future surface class where the two differ would produce a widening violation entry on the PC#9 intent record per OQ-3's ordering rule.

**Open for prototype.** Whether the PC#9 completion should also carry a direct `crossingCompletionRef` to its own intent (redundant with chain walk, but cheaper to verify) is a Phase-0 implementation question, not a spec question.

---

## What Comes Next

1. **Successor: targeted design session on gate-steps operational language** — the fresh pass halted non-converged at its G11 ceiling (SL-0174; second halted pass). Both passes' failure mode is identical: every iteration's narrowings rewrote text, and every rewrite introduced a new attackable surface. No constitutive property failed across seven iterations; the architectural design is stable. What is unstable is the operational language of the gate steps — specifically: step 1's class-consistency mechanism (A); assembly sequencing and acknowledgment-validity timing (B); register operand attribution and the witness split (C). **Recommended successor:** a targeted design session that produces a clean gate-steps section with all inputs named, all timing relations explicit, and all author/gate/store distinctions stated before the next Counter-Pass. The next Counter-Pass runs on that redesigned-gate v0.3-candidate, not on a further v0.2.x narrowing. *(See also: the convergence criterion itself — "no new attack for one full iteration" cannot be met while every iteration rewrites text; the design session breaks that cycle.)* Gates v0.3, the SINGLE-CONTEXT lift, and Lexicon registration.
2. **TCF v1.8 session** (separate; not this cluster): Section B field-name confirmation; status ordering ruling (KL-11).
3. **PC#9 Phase 0 build plan** — reference implementation against `atproto-pds` surface class, reusing PC#8's Phase 0/1 harness; standing grant + write-time gate + one real chained record set.
4. **Lexicon registration** of the PROPOSED field group after Counter-Pass close (governance action, not promotion — Collision Prevention rule 7 posture).
5. **RA pre-registration** — unchanged sequence; after prototype only. **Flag F-1 (queued from Counter-Pass it-1 L5 Verdict B, out of lane here):** state the RA-relevant property as *schema-checkability*, decoupled from SHACL, so the RA motivation does not inherit a validator choice it does not need.
6. **Prototype items added by it-1:** evidence a `cms-enumerable` crossing (class currently unevidenced); observe a corrective shape event during an open horizon (KL-13).
7. **Prototype items added by it-2:** observe an ACL widening during an open horizon on a `cms-enumerable` crossing (KL-14); decide whether `grantReference` is content-addressed (N4); emit one gate-minted register entry and one store-produced §7.4 entry on the same object and confirm they acknowledge separately (N5).
8. **Companion runtime spec v0.1.1 (queued, not applied here; scope extended it-3):** §6 — state that the gate mints the grant-relative register entry (`tcf:q/register/grant-requirement`) alongside filtering store reports; §9 row 6 — correct "§7.4 computed register vs grant requirement" to name the two distinct comparisons (store: declared vs computed; gate: declared vs grant requirement) *(it-2, N5)*; §2.3/§6 — register `tcf:q/register/grant-requirement` in the shape library as a declared-but-not-evaluated Quark carrying its severity, and state that gate step 6 reads severity from the library at the pinned version *(it-3, D)*. **Status (fresh it-1 4b; corrected fresh it-2 attack 1(i)): precondition for any register mismatch to resolve via acknowledgment** — a grant issued against a library lacking the Quark record will block uncurably at step 6 on every register mismatch for its full horizon; a library without this entry is not a valid issuance precondition per any written grant invariant, but is a horizon-long operational block on the mismatch branch.
9. **GSEF lineage-record schema (queued):** define a forward review-window field or rule that none is wanted; grant invariant 6 MUST/SHOULD resolves there. *(it-2, R6-e.)*
10. **Design questions (it-3; revised fresh it-1, two-context; fresh it-2):** *(A)* completion-side basis re-resolution (`enumerabilityBasisAtCompletion`) — an in-record disclosure path for within-bound widening, at the cost of a new field; the `cardinality | memberSetDigest` alternation is **already load-bearing under option (i)** (fresh it-1, 1a), so the question is whether the in-record path is worth the field, not whether the alternation matters. Still queued. *(B — re-posed, fresh it-1 B#3)* the original two-phase framing is closed as mis-posed; the live question is whether to add a per-object content digest of the submitted root (the completion record's `authorizedContentDigest`, computed at intent time) to `reportDigest`'s canonical input — pre-computable, non-templatable, no second phase. Not required by the KL-4 disposition's record-claim posture; queued as a design choice. *(C — new, B#6)* whether the intent record's `tcfShapeDigest` copy is a gate-owned write at record assembly or author/store-supplied — Phase 0. *(D — fresh it-2 attack 1(ii); assessed and closed fresh it-3, C3)* **Fourth Carry-In escape candidate — assessed: NOT a distinct escape.** "Register misdeclaration to evade a missing-Quark block" (declaring `tcfRegister` = `tcfRegisterRequirement` when the library lacks the Quark record) is dominated by ordinary permitted grant-issuance: an author who aligns the two values at issuance — which invariant 1 permits outright — never reaches the mismatch branch, missing Quark or not. Naming it as an escape attaches a general fact (the branch is author-elective at both ends) to a special case. **Do not add a fourth Carry-In escape.** The correct statement is the witness split (see OQ-2 and KL-4 Disposition): the register branch has no external anchor in v0.2.x; Particle-tier `tcfRegister` is unwitnessed; composite-tier is witnessed by §7.4's declared-vs-computed entry — a distinct comparison.

---

*This document is part of the Pattern Commons. AI-collaborative drafting, human authorial responsibility, intellectual direction held by the named author.*

*⚑ SINGLE-CONTEXT — STAMP LIFTED (2026-08-28). Third Counter-Pass closed at iteration 1 CONVERGED WITH NARROWING (SL-0180; operator close 2026-08-28). Lift conditioned on: N1–N3 are post-convergence prose, not critic-tested in a subsequent iteration. All resolutions ~ except OQ-5 ✓. First Counter-Pass iterations 1–3 reconciled and halted under G11; fresh pass (brief v1.2) iterations 1–3 reconciled and halted under G11 — thirteen attack substances total across both passes, all narrowings; seven consecutive iterations of fix-introduced surfaces, no constitutive property absent in any. Third pass it-1: CONVERGED WITH NARROWING — no constitutive-property attack; three prose narrowings (N1–N3). No prototype. No generality claims. Declared scope: three surface classes, one evidenced; URI grants assessed per (author, surface) pair, class-identifier grants per (author, class). Delivery-not-application enforced; canonical files on operator’s machine.*

*Session: Session Harness v0.2, Mode 3 (producer), CONTEXTUAL. v0.2 issued 2026-08-24 (SL-0146–SL-0149); v0.2.1 reconciliation 2026-08-25 (SL-0151–SL-0155); v0.2.2 reconciliation 2026-08-25 (SL-0156–SL-0160); v0.2.3 reconciliation 2026-08-27 (SL-0162–SL-0165); v0.2.4 fresh-pass it-1 two-context reconciliation 2026-08-27 (SL-0166–SL-0169); v0.2.5 fresh-pass it-2 reconciliation 2026-08-27 (SL-0170–SL-0173); v0.2.6 fresh-pass it-3 reconciliation 2026-08-27 (SL-0174–SL-0177); v0.3 third-pass it-1 reconciliation and close 2026-08-28 (SL-0178–SL-0183; tail SL-0180 verified by direct read: 180 headings, 1 footer, no gaps). SL-0150–SL-0160 and SL-0163–SL-0173: OPEN → CLOSED by sweep delta SL-0182. SL-0174 CLOSED (method finding — fresh-pass non-convergence at it-3; second halted pass). SL-0178 validation event closed by amendment SL-0183. SL-0180 CLOSED (third-pass convergence; operator close 2026-08-28).*

*UX Minds, LLC · J. Wright · August 28, 2026*
