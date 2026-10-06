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


---

## 2026-10-06 — Frontier red-team and Recovery Decision Certificate

### Commits
- `01ba8b74c3e85d3f00ce2cb2683340bc7371737f` — frontier red-team + certificate design
- `8442d935e36eccfb5158d6553395bc8c9339d42e` — Decision Exposure / Action Gate economics
- `e53515c34ea509c915677d28f430c4ddc5846974` — third competitor red-team addendum
- `f2f35722cee27f9d2493ae589a80f08d09119a10` — Next Best Evidence hardened with deterministic Action Gate
- `a87c043487061961b970ce106268afcf43f24425` — V1 centered on Recovery Decision Certificate
- `21dac5d9cb8c0e19ce547fa107b41cb6f35a5684` — architecture adds Decision Exposure / Action Gate / certificate
- `cb32940b4d593acacb723726eeeba42b59b9ef96` — certificate/action-gate tests
- `348d6331109e0455711ddd4da3589ab60004432b` — judge story centered on certificate
- `d1ec26851f70f78aa1bc743596c28d777f176cfd` — submission claim mapping updated
- `7035aaa4c2395f0834c403d2afab02bc20625bdd` — decisions D-033 through D-037
- `556651dd9195c994ca3c77e25531cde6926822b2` — hero fixture gets concrete Decision Exposure / Action Gate
- `c4a69a0379e865cd80419216f232df8a2a6d587e` — hero materiality threshold aligned

### File added
- `16_FRONTIER_RED_TEAM_AND_DECISION_CERTIFICATE.md`

### Frontier findings
- Narvar's 2026 public material already frames post-purchase as agentic/context-aware decisioning across delivery/returns/claims.
- Happy Returns supports agent-driven return flows through MCP.
- ReverseLogix can ask for more information, preserve AI evidence, and route with rules.
- September 2026 SSADS research already combines narrative return-note extraction with a separate reverse-logistics optimizer.

### Product response
- Generic "agentic post-purchase" and "semantic extraction + optimizer" are no longer treated as originality.
- Recovery Decision Certificate becomes the primary judge artifact.
- Decision Exposure quantifies scenario-bounded regret of the base winner.
- Deterministic Action Gate selects ACT NOW / ASK FIRST / HUMAN REVIEW.
- Next Best Evidence is valuable because it is tied to the exact Decision Hinge, not because asking for more information is novel.
- One-dimensional uncertainty per case remains a hard V1 scope boundary.

### Hero fixture
RG-001 now has:
- RETRY EFRC = 46.20
- STOP & RTO EFRC = 35.00
- break-even = 55.6%
- plausible range = 45%–80%
- Decision Exposure = 9.50
- synthetic merchant materiality threshold = 5.00
- Action Gate = ASK_FIRST
- Next Best Evidence = customer availability confirmation

### Gate effect
- G0 remains IN PROGRESS.
- AMD complimentary cloud credit is still pending.
- No product implementation code was created.
- No paid GPU action occurred.

### Verification
PASS


### Frontier follow-up
- `6a1d7978d7e9076758689a6d2df2d1a99d9d28b7` — aligned Recovery Decision Certificate hero values with RG-001 (Decision Exposure 9.50, materiality threshold 5.00, Action Gate ASK_FIRST).


---

## 2026-10-07 — Critical-path execution hardening

### Commits
- `6d6a3949411af97952cb07d6fb8516b96c707a57` — added dependency-based hackathon critical path
- `1ebfea5937865f6e8dd7f18e4de9823acc13706a` — refreshed official-page schedule/track inconsistency
- `ad7dfcf20c89a66aad218b696aacd9b492198985` — recorded parallel-gate and credit-blocker decisions
- `4a2bfd1c3604c717731af2aab4c6e40489c3204c` — moved credit activation blocker from G0 to G2
- `e0f79c3f2927dfe1a0051b8cf6f3e24a624ef1e6` — G0 PASS + master-state critical-path sync

### Execution finding
Complimentary AMD credit activation is not an official prerequisite for beginning local deterministic product work after kickoff.

### Control change
- G0 now covers registration and safe account/environment access and is PASS.
- Credit activation is a G2 AMD Proof blocker.
- After G1, G2 AMD Proof and G3 Economics Core may proceed as independent lanes.
- Strict serial gate sequencing is replaced by dependency-based gate control after G1.
- No paid GPU/card authorization was added.

### Schedule risk
Current official pages still conflict:
- main page: online phase 12–18 Oct
- live dashboard: online build 12–17 Oct
- live dashboard: submission closes 18 Oct 15:00 UTC
- main page publishes Track 3
- live dashboard currently says Tracks: TBA

Internal build-freeze target remains 17 Oct until kickoff clarifies this.

### Gate effect
- G0: PASS
- G1: WAITING FOR KICKOFF
- G2: BLOCKED BY CREDIT ACTIVATION
- G3: BLOCKED ONLY BY PRE-KICKOFF G1 HOLD

### Verification
PASS


---

## 2026-10-07 — Consolidated deep-research / podium-bar hardening

### Research added
- `18_DEEP_RESEARCH_WINNING_BAR.md` — prior AMD winner patterns, market/research synthesis, podium-level proof bar
- `19_RECOVERYBENCH_EVAL_PLAN.md` — frozen product/AI/economics/adversarial/runtime evaluation plan
- `20_AI_EVIDENCE_QUALITY_CONTRACT.md` — deterministic evidence status replacing model self-confidence
- `21_TRACK_FIT_AND_PIVOT_AUDIT.md` — Track 3, pivot alternatives, and partner-prize strategy

### Key research conclusions
- Prior AMD podium projects consistently strengthen their story with measurable evals, adversarial/failure proof, GPU telemetry, tests, and latency/throughput/cost evidence.
- A working UI alone is not the target bar.
- ReclaimGrid remains the strongest current concept; no pivot is recommended before G1.
- Generic NDR, disposition AI, fraud classification, forecasting, and generic returns-agent pivots were rejected for overlap/data/execution risk.
- Model-authored numerical confidence is removed from the authoritative Case Interpreter contract.
- Deterministic Evidence Status is now GROUNDED / AMBIGUOUS / INCOMPLETE / INVALID.
- RecoveryBench becomes the task-specific model-selection and proof framework.
- Final app should include a compact measured Proof surface.
- Partner prizes remain subordinate to the main Track 3 product.

### Canonical docs synchronized
- `02_PRODUCT_SCOPE.md`
- `03_ARCHITECTURE.md`
- `05_TEST_EVIDENCE_PLAN.md`
- `06_SUBMISSION_CHECKLIST.md`
- `07_DECISION_LOG.md`
- `11_SYNTHETIC_FIXTURE_BLUEPRINT.md`
- `12_JUDGE_STRATEGY.md`
- `15_AMD_MODEL_AND_SERVING_PLAN.md`

### Commits in this consolidated pass
- `bc09bdb0f5ea0b4cd82ca8475d376da728ec1919` — deep winning-bar research
- `fa9377239cceeb1edbbb7dc18296857b0b626628` — RecoveryBench eval plan
- `52b1fa4ba5efadfc82a09d061a6daaed346141bb` — evidence-quality contract
- `82e86f7d8a241f1a00b9716d6430538b018768b5` — track/pivot/partner audit
- `16f052428ae9deb23da15b75a8c0b5faf6e66e30` — product scope sync
- `db27bee020f356f76208190b8dc093e7cfd136ea` — architecture sync
- `06b12fbbc413379a542ce69b90d2ad5059a835a6` — test-plan sync
- `765e987358742e16e0c755d4753783e2f54aa699` — submission-proof sync
- `37bdb90e88f98839596ec66e79c546cb019bb75e` — fixture evidence-status sync
- `bf16cd6ac345aa05bd058d6d5bbe17770eb57ff4` — judge proof-bar sync
- `9f9959c0b529fff50dc49f96c719ce2663ec3be4` — AMD model-plan sync
- `21544f18092163351691d568a78927c32a453f5a` — deep-research decisions D-041 through D-045

### Implementation state
- No submission implementation code was created.
- No paid GPU action occurred.
- G0 remains PASS.
- G1 remains waiting for kickoff.
- G2 remains blocked by complimentary credit activation.
- G3 remains blocked only by pre-kickoff G1 hold.

### Verification
PASS


### Deep-research consistency cleanup
- `164fab5a1757a388a77125599933ec5ac1eb8505` — removed stale confidence reference from product scope
- `5d029688a2f812bb47c4d95de73bc69cf44f1b0d` — removed stale confidence references from architecture
- `1d3fe04433fc7d8c2c00af3d032e792686769ab5` — replaced stale confidence test with deterministic Evidence Status
- `74c21493969ab9850c2de5eb826f62573c7aa854` — aligned judge story to Evidence Status
- `55564ec3433a5ba69460d042c5bb66c30684421f` — fixed submission-checklist numbering


### Fresh official-page correction
- `227d698e32d94b1be0917845a5d506320bd43945` — refreshed ACT III prize snapshot to the currently visible $11,000+ and marked partner-prize amounts as volatile.


---

## 2026-10-07 — Decision-quality and benchmark-integrity deep research

### Research added
- `22_DECISION_QUALITY_AND_BENCHMARK_INTEGRITY.md`

### Key findings
- Pure EFRC maximization is insufficient if policy, customer remedy, service commitments, evidence sufficiency, or operational availability are omitted.
- NRF data reinforces that returns materially affect repeat-purchase behavior and retailer strategy, so service/customer constraints cannot be ignored.
- V1 now uses a deterministic **Policy & Service Feasibility Envelope** before EFRC optimization.
- V1 explicitly rejects fabricated CLTV/churn/loyalty-dollar scoring and opaque weighted multi-objective formulas.
- RecoveryBench now uses **DEV 32 + locked HOLDOUT 16** for Case Interpreter evaluation.
- Benchmark reports must record version, fixture SHA, prompt contract, model, serving stack, hardware, code SHA, and run date.
- If prompt/schema changes after HOLDOUT scoring, benchmark version/rerun is required.
- Efficiency metrics are measured as evidence, but ACT II token-efficiency scoring is not assumed to be an ACT III rule.

### Canonical docs synchronized
- `02_PRODUCT_SCOPE.md`
- `03_ARCHITECTURE.md`
- `05_TEST_EVIDENCE_PLAN.md`
- `06_SUBMISSION_CHECKLIST.md`
- `07_DECISION_LOG.md`
- `10_RECOVERY_ECONOMICS_DESIGN.md`
- `12_JUDGE_STRATEGY.md`
- `19_RECOVERYBENCH_EVAL_PLAN.md`

### Commits
- `1d32a9f21c6cecc6c4efcb8d0da888b8a85ec56f` — deep decision-quality / benchmark-integrity research
- `387f5628a72583e19aa183fd8eea7f3497cf06a4` — product-scope feasibility envelope
- `bc3de1f5fd8f3dfa791e5fdc6084d6a7bc9bc8b7` — architecture feasibility envelope
- `2750afbc0df16a9ae3d862b7a7a1101438fec392` — constraint-first economics
- `5a15c0a681544890d6ef8d64add9220edb93c16a` — RecoveryBench holdout/versioning controls
- `f5798d174e6f569e1412f3386e1579104b55a0df` — feasibility/benchmark-integrity tests
- `d3c75e6b1d697b83fe6fb47432d726842e0eb237` — decisions D-046 through D-048
- `a2b5941ecb59bd6c897115009a0c8c1b887b452b` — submission proof claims
- `2659c8bbf730e6cf2dcd44bc31ac8d1dc882bb04` — judge defense

### Gate effect
- No implementation code created.
- G0 remains PASS.
- G1 remains waiting for kickoff.
- G2 remains blocked by complimentary credit activation.
- G3 remains blocked only by G1 pre-kickoff hold.

### Verification
PASS


---

## 2026-10-07 — Technical feasibility, build blueprint, and implementation-risk freeze

### Research / design added
- `23_TECHNICAL_FEASIBILITY_AND_BUILD_BLUEPRINT.md`
- `24_IMPLEMENTATION_SEQUENCE_AND_RISK_REGISTER.md`

### Technical findings
- V1 does not need SSR, a database, auth, an ORM, queues, a vector DB, or an agent framework.
- Default stack is Node 22.12+ + Vite/React/TypeScript + Zod + read-only React Flow + Vitest + Playwright.
- Netlify static hosting + TypeScript Functions provides a low-risk same-origin secret boundary for AMD inference.
- Netlify synchronous functions currently have a 60-second hard limit; ReclaimGrid uses a much lower 25-second application timeout.
- Netlify function rate limiting can protect external AI spend; initial target is 4 AI calls / 60s / IP+domain.
- Public browser requests must not carry arbitrary prompts/model names/token limits.
- AMD live inference gets a hard `AMD_LIVE_ENABLED` kill switch.
- DEV_MOCK / LIVE_AMD / VERIFIED_RECORDED modes are explicitly separated.
- React Flow remains read-only; hardcoded deterministic layout avoids graph-editor/autolayout complexity.

### AMD model-plan correction
Fresh AMD Enterprise AI support research shows:
- Qwen3-32B: optimized MI300X path
- Llama-3.1-8B-Instruct: optimized MI300X path
- current support data does not justify assuming Qwen3-8B is the lowest-friction Instinct path

Therefore:
- inspect actual cloud image first
- test at most Qwen3-32B and Llama-3.1-8B-Instruct
- RecoveryBench chooses final model
- do not build a model zoo

### Exact milestone sequence
Frozen M0–M15:
- M0 scaffold
- M1 contracts
- M2 Policy & Service Feasibility
- M3 graph/economics
- M4 robustness/exposure
- M5 Action Gate
- M6 certificate
- M7 RecoveryBench
- M8 judge UI
- M9 AI gateway/mock
- M10 real AMD proof
- M11 grounded explainer
- M12 integration
- M13 Proof surface
- M14 security/release
- M15 judge/submission

### Risk controls
A formal risk register now covers:
- credit delay
- model setup
- schema quality
- public GPU abuse
- function timeout
- financial math
- graph cycle/double counting
- AI authority escape
- benchmark overfit
- UI scope
- React Flow complexity
- Netlify deploy
- live AMD outage
- partner-prize scope creep

### Canonical docs synchronized
- `03_ARCHITECTURE.md`
- `04_SECURITY_COST_GUARDRAILS.md`
- `05_TEST_EVIDENCE_PLAN.md`
- `07_DECISION_LOG.md`
- `15_AMD_MODEL_AND_SERVING_PLAN.md`
- `17_HACKATHON_CRITICAL_PATH.md`

### Commits
- `096c04ae4f6f74b8fb323d5a1707f49aff92678d` — exact technical build blueprint
- `b302ec268220532265ebc792e861fdb27785ac56` — M0–M15 implementation sequence and risk register
- `c8b04bc13325bda24986f4045268974db1a09d15` — architecture stack freeze
- `3e583e7408e20d9856d7c4f3a560c5329167f401` — public AI proxy/cost controls
- `8abb950a14935e6a3246e5b02b1d319a6189634c` — blueprint tests
- `5dd3e8d93834bc8d4ea8f2a245db04b95e32b0d8` — MI300X model ladder correction
- `43da532c287be764f49ad3361f071c31d6d5ea79` — critical path bound to milestones
- `26d5f4759f22144f2100e55df26587f6777c9679` — decisions D-049 through D-053

### Gate effect
- No implementation code created.
- G0 PASS.
- G1 waiting for kickoff.
- G2 blocked by safe AMD compute/credit.
- G3 blocked only by G1 pre-kickoff hold.

### Verification
PASS
