# RECLAIMGRID AI — CHANGELOG

## CONTROL
- PROJECT: ReclaimGrid AI
- CONTROL CODE: RG-ACT3
- FILE: 08_CHANGELOG.md
- SNAPSHOT DATE: 2026-10-06
- STATUS: ACTIVE / CHRONOLOGICAL
- PURPOSE: Record repository and Control Room state changes over time. Decision rationale belongs in `07_DECISION_LOG.md`; this file records what changed and when.

## CHANGELOG RULE
For every material repository/control-system change, append an entry with:
- date/time if known,
- commit SHA,
- files changed,
- change summary,
- gate/status effect,
- verification result.

Do not rewrite prior entries except to fix factual errors.

---

## 2026-10-06 — Repository initialized

### Commit
`88dacc32281b1e61cf5168aca17aa40b36b3033e`

### Message
`Initial commit`

### Changes
- Created public GitHub repository: `Hunter20202/reclaimgrid-ai`
- Default branch: `main`
- Initialized repository with README.

### Gate effect
- G0 repository requirement moved from NOT STARTED to IN PROGRESS.

### Verification
PASS

---

## 2026-10-06 — Master state added

### Commit
`ff46c218293de3f3bcf45effb8714f6ef0321cdd`

### Message
`docs: add RG-ACT3 master state`

### Files
- `00_MASTER_STATE.md`

### Changes
- Established Control Room source-of-truth structure.
- Recorded G0 state.
- Recorded completed account/event/team setup.
- Recorded AMD credit blocker.
- Recorded security/cost stop rules.
- Recorded gate plan G0-G9.
- Recorded initial next safe action.

### Gate effect
- G0 control documentation started.

### Verification
PASS

---

## 2026-10-06 — Rules snapshot added

### Commit
`b3d5a41d81e7d7d1046be5a96773cc985e4dd3a5`

### Message
`docs: add verified ACT III rules snapshot`

### Files
- `01_RULES_SNAPSHOT.md`

### Changes
- Captured current ACT III event facts.
- Recorded online-build schedule inconsistency.
- Recorded current submission-close milestone.
- Recorded team, AMD, Track 3, repository, judging, prize, and credit facts.
- Added conservative pre-kickoff implementation guardrail.
- Defined G1 rules re-verification conditions.

### Gate effect
- G1 planning baseline created.
- G1 remains NOT STARTED / not eligible to PASS before kickoff re-verification.

### Verification
PASS

---

## 2026-10-06 — Product scope frozen provisionally

### Commit
`9b44ebf1e59f4054037ddf57ed11c24d18cebb75`

### Message
`docs: freeze provisional ReclaimGrid V1 scope`

### Files
- `02_PRODUCT_SCOPE.md`

### Changes
- Defined primary user and problem.
- Defined candidate case types and recovery routes.
- Defined deterministic Recovery Economics Engine role.
- Defined AMD AI role and limits.
- Defined human approval requirement.
- Defined synthetic-data strategy.
- Defined demo success metrics.
- Defined must-haves, should-haves, non-goals, and scope kill test.

### Gate effect
- G1 provisional scope baseline established.
- Product implementation remains blocked pre-kickoff.

### Verification
PASS

---

## 2026-10-06 — Architecture defined

### Commit
`ffdba38608b1d69d94d43159fcd1ed2658f90958`

### Message
`docs: define provisional ReclaimGrid architecture`

### Files
- `03_ARCHITECTURE.md`

### Changes
- Defined end-to-end decision flow.
- Separated deterministic economics from AMD AI.
- Defined component boundaries and trust boundaries.
- Defined AMD proof path.
- Defined AI timeout/invalid-output fallback.
- Defined minimal technology shape.
- Defined cost-containment architecture.
- Defined architecture acceptance tests.

### Gate effect
- G2-G5 planning baseline established.

### Verification
PASS

---

## 2026-10-06 — Security and cost guardrails frozen

### Commit
`80b2cdeaf87df2daf5e7878407740896bd844348`

### Message
`docs: freeze security and cost guardrails`

### Files
- `04_SECURITY_COST_GUARDRAILS.md`

### Changes
- Frozen secret-handling policy.
- Frozen synthetic-data/PII rules.
- Frozen AI trust and prompt-injection rules.
- Frozen human-approval boundary.
- Frozen AMD GPU/payment STOP conditions.
- Added logging, dependency, repository, network, input-validation, and demo-safety requirements.
- Added future security test set and release blockers.
- Added GPU cost-ledger requirement.

### Gate effect
- G0/G2/G6 security-cost baseline established.
- Paid GPU use remains blocked.

### Verification
PASS

---

## 2026-10-06 — Test and evidence plan added

### Commit
`1a65cb39d8d850917556d979e10ae6b7d9f2c788`

### Message
`docs: add gate test and evidence plan`

### Files
- `05_TEST_EVIDENCE_PLAN.md`

### Changes
- Defined G0-G9 PASS/FAIL evidence requirements.
- Defined deterministic economics test categories.
- Defined AMD proof evidence.
- Defined AI adversarial/fallback tests.
- Defined integration, security, judge-experience, freeze, and final-audit checks.
- Defined synthetic fixture matrix.
- Defined test-result format and blocker severity.

### Gate effect
- Future gate verification method established.

### Verification
PASS

---

## 2026-10-06 — Submission checklist added

### Commit
`6c6d348279b05e8b706a100ed11976246f2527f6`

### Message
`docs: add submission checklist`

### Files
- `06_SUBMISSION_CHECKLIST.md`

### Changes
- Defined planned submission assets.
- Defined public repo/app/video/deck validation.
- Defined evidence-to-claim mapping.
- Defined AMD wording rules.
- Defined business-value and originality claim rules.
- Defined final README expectations.
- Defined submission-form audit and final freeze behavior.

### Gate effect
- G7-G9 submission planning baseline established.

### Verification
PASS

---

## 2026-10-06 — Decision log established

### Commit
`00f2d21f19849c7507d9b53a795953e65e2dce5e`

### Message
`docs: add authoritative decision log`

### Files
- `07_DECISION_LOG.md`

### Changes
- Created append-only project decision record.
- Seeded D-001 through D-020.
- Recorded frozen, provisional, and active decisions.
- Added future decision-entry template.

### Gate effect
- Formal change-control mechanism established.

### Verification
PASS

---


---

## 2026-10-06 — Competitive research and product hardening

### Commits
- `ba518f363f222c6b81882d797480955908e71715` — added competitive research
- `52f9347bc04591aeed59c6b76a64917ac7e77a68` — upgraded V1 scope
- `06cce072b3f7dc44c53dcc650943e258fc83c78b` — upgraded architecture
- `6c0842a16ee6f4917c105bf2ddd95b7edb7f242a` — recorded new decisions
- `d4ca863eb5b7581064f3867a47921ccd7e1ab90f` — extended test plan
- `27a2e1925555b4f7132faf8053b594422050409b` — aligned submission story
- `f97c4679a0d61577422f9ab404e0ea6bd797ae79` — added economics design
- `d7c90610ac7e1ac60abe0d6a08df649f8219ac76` — added fixture blueprint
- `5ced65f9ad20c1188b148544445181eb37945a8a` — added judge strategy

### Files added
- `09_COMPETITIVE_RESEARCH_AND_PRODUCT_UPGRADE.md`
- `10_RECOVERY_ECONOMICS_DESIGN.md`
- `11_SYNTHETIC_FIXTURE_BLUEPRINT.md`
- `12_JUDGE_STRATEGY.md`

### Files materially upgraded
- `02_PRODUCT_SCOPE.md`
- `03_ARCHITECTURE.md`
- `05_TEST_EVIDENCE_PLAN.md`
- `06_SUBMISSION_CHECKLIST.md`
- `07_DECISION_LOG.md`

### Research findings
- Generic AI returns/NDR automation is too crowded to be sufficient differentiation.
- Competitor overlap was verified across Loop, Optoro, AfterShip, ClickPost, and ReverseLogix.
- Product core upgraded to a bounded Recovery Decision Graph.
- Multi-stage counterfactual recovery-path economics became the primary deterministic differentiator.
- Break-even/sensitivity analysis became mandatory V1.
- AMD AI role strengthened to evidence-grounded Case Interpreter plus grounded Decision Explainer.
- Decision Ledger added as a core trust/audit feature.
- Portfolio Value Leak Map and multimodal condition analysis were explicitly demoted to SHOULD/STRETCH.

### Formula/fixture hardening
- Defined Expected Future Recovery Contribution (EFRC).
- Defined sunk-cost fence.
- Defined bounded DAG/backward-induction model.
- Defined hero NDR break-even equation.
- Defined ROBUST vs FRAGILE based on plausible assumption ranges.
- Frozen synthetic fixture concepts including hero, policy exclusion, prompt injection, AI timeout, tie, and zero-baseline cases.

### Judge strategy
- Mapped core features to the four official ACT III judging criteria.
- Frozen a judge-first hero flow:
  messy note -> AMD evidence extraction -> recovery graph -> path economics -> break-even -> explanation -> human approval -> portfolio value proof.

### Gate effect
- G0 remains IN PROGRESS because AMD complimentary cloud credit is still pending.
- No implementation code was created.
- Pre-kickoff research/documentation authorization was respected.

### Verification
PASS


---

## 2026-10-06 — Competitive white-space, Decision Hinge, and AMD serving hardening

### Commits
- `a01f9c397fb6c060770dca9aa81a1ca89ae47940` — competitor matrix / white-space analysis
- `21272194a8f66257cc0dd6c9a15f1c812bd0b2f7` — Decision Hinge / Next Best Evidence design
- `99e22db4fc52cf4aaec5cd26dcfc86a786a1a223` — AMD model / serving plan
- `c3cf37c4602b48da82d5337e22de0a8b320c37da` — V1 scope updated
- `09ffbed4c0d65e5881bbbf5d4da085215afb23d2` — architecture updated
- `e4ad7347f0ff0ce51fb78ee852e01b438593fe2c` — test plan updated
- `0933859183463c8b85e8d5665a4efece97f6fad1` — judge story strengthened
- `b954d893c7ec7daf719d917ce6557b6026631136` — decision log updated
- `c28927e9bb38a9da6f13794deb1bce8250d49ea9` — submission claim mapping updated

### Files added
- `13_COMPETITOR_MATRIX_AND_WHITE_SPACE.md`
- `14_DECISION_HINGE_AND_NEXT_BEST_EVIDENCE.md`
- `15_AMD_MODEL_AND_SERVING_PLAN.md`

### New product hardening
- Public competitor materials were compared explicitly across Loop, Optoro, AfterShip, ClickPost, and ReverseLogix.
- ReclaimGrid positioning was sharpened to a recovery-intelligence **decision layer**, not a workflow-suite replacement.
- Decision Hinge became a hero-case MUST: show the uncertain variable and exact threshold where the winner flips.
- Next Best Evidence added for fragile decisions, reusing existing break-even math rather than introducing a new ML system.
- Formal EVPI/EVSI/Bayesian updating remains out of V1 scope.
- AMD model plan now starts with Qwen3-8B + vLLM for low-cost proof; Qwen3-32B / Qwen3-30B-A3B are escalation candidates only if fixture quality requires them.
- Structured JSON output plus semantic evidence-span validation is mandatory for the Case Interpreter.

### Gate effect
- G0 remains IN PROGRESS because complimentary AMD credit is not yet active.
- No implementation code created.
- No payment method added.
- No GPU launched.

### Verification
PASS

## CURRENT CONTROL-DOC SET AFTER THIS FILE

Expected canonical files:
- `00_MASTER_STATE.md`
- `01_RULES_SNAPSHOT.md`
- `02_PRODUCT_SCOPE.md`
- `03_ARCHITECTURE.md`
- `04_SECURITY_COST_GUARDRAILS.md`
- `05_TEST_EVIDENCE_PLAN.md`
- `06_SUBMISSION_CHECKLIST.md`
- `07_DECISION_LOG.md`
- `08_CHANGELOG.md`

Research/design extensions:
- `09_COMPETITIVE_RESEARCH_AND_PRODUCT_UPGRADE.md`
- `10_RECOVERY_ECONOMICS_DESIGN.md`
- `11_SYNTHETIC_FIXTURE_BLUEPRINT.md`
- `12_JUDGE_STRATEGY.md`
- `13_COMPETITOR_MATRIX_AND_WHITE_SPACE.md`
- `14_DECISION_HINGE_AND_NEXT_BEST_EVIDENCE.md`
- `15_AMD_MODEL_AND_SERVING_PLAN.md`

Plus:
- `README.md`

## CURRENT GATE STATE
- G0 — Registration & Environment: IN PROGRESS
- Main unresolved blocker: AMD complimentary Developer Cloud credit approval/activation not yet verified.
- No payment method added.
- No GPU resource created.
- No implementation code authorized yet.

## NEXT SAFE ACTION
Sync `00_MASTER_STATE.md` to the research-upgraded product state and keep implementation blocked until kickoff/G1 and AMD credit re-verification.
