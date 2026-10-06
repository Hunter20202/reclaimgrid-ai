# RECLAIMGRID AI — DECISION LOG

## CONTROL
- PROJECT: ReclaimGrid AI
- CONTROL CODE: RG-ACT3
- FILE: 07_DECISION_LOG.md
- SNAPSHOT DATE: 2026-10-06
- STATUS: ACTIVE / APPEND-ONLY
- PURPOSE: Authoritative record of material project decisions affecting rules, scope, architecture, security, cost, AMD usage, testing, and submission.

## APPEND-ONLY RULE
Do not rewrite history to make past decisions look cleaner.

For every material change:
- add a new decision entry,
- reference the previous decision if superseded,
- record why it changed,
- record affected gate(s),
- record security/cost/demo impact,
- record the commit SHA when available.

A decision may be:
- ACTIVE
- SUPERSEDED
- REJECTED
- DEFERRED
- PROVISIONAL
- FROZEN

---

## D-001 — Product identity
- DATE: 2026-10-06
- STATUS: FROZEN
- DECISION: Product name is **ReclaimGrid AI**.
- REASON: Selected as the working hackathon product for AMD Developer Hackathon: ACT III.
- IMPACTED GATES: G0-G9
- NOTES: Canonical repository name is `reclaimgrid-ai`.

## D-002 — Control Room operating model
- DATE: 2026-10-06
- STATUS: FROZEN
- DECISION: Use a gate-based Control Room workflow with one safe verified action at a time.
- REASON: Reduce execution error, preserve auditability, and keep user actions bounded.
- IMPACTED GATES: G0-G9
- NOTES: No gate advances unless the prior gate is verified PASS.

## D-003 — Primary track
- DATE: 2026-10-06
- STATUS: PROVISIONAL
- DECISION: Primary target is **Track 3 — Reinvent Commerce**.
- REASON: ReclaimGrid converts post-purchase case data into an economically ranked action and aligns with commerce decision support.
- IMPACTED GATES: G1, G7, G8, G9
- REVIEW TRIGGER: Kickoff/rules update or track wording changes.

## D-004 — Core product thesis
- DATE: 2026-10-06
- STATUS: FROZEN
- DECISION: ReclaimGrid is a **post-purchase recovery decision engine**, not a generic returns chatbot or returns portal.
- REASON: Existing failed-delivery/returns automation is crowded; differentiation must come from bounded recovery economics plus AMD-hosted AI interpretation/explanation.
- IMPACTED GATES: G1-G8

## D-005 — Deterministic financial authority
- DATE: 2026-10-06
- STATUS: FROZEN
- DECISION: Recovery-value calculations, route eligibility, and route ranking are deterministic and authoritative.
- REASON: Financial logic must be reproducible, inspectable, and not solely dependent on an LLM.
- IMPACTED GATES: G3-G7
- SECURITY IMPACT: Reduces hallucination/authority risk.

## D-006 — AMD AI responsibility
- DATE: 2026-10-06
- STATUS: FROZEN
- DECISION: AMD-hosted AI is limited to bounded tasks such as free-text interpretation, explanation, tradeoff summarization, and message drafting.
- REASON: AI should add semantic value without becoming the source of financial truth.
- IMPACTED GATES: G2, G4, G5, G7
- NOTES: Final model is not yet selected.

## D-007 — Human approval
- DATE: 2026-10-06
- STATUS: FROZEN
- DECISION: Consequential recovery actions remain human-approved.
- REASON: V1 is decision support, not unrestricted autonomous execution.
- IMPACTED GATES: G4-G7
- SECURITY IMPACT: Blocks model-triggered real refunds, shipping, payments, or inventory mutation.

## D-008 — Synthetic-data default
- DATE: 2026-10-06
- STATUS: FROZEN
- DECISION: V1 uses synthetic ecommerce cases by default.
- REASON: Reproducibility, privacy, lower integration risk, and better test evidence.
- IMPACTED GATES: G3-G8
- SECURITY IMPACT: Avoids real customer PII.

## D-009 — V1 scope restraint
- DATE: 2026-10-06
- STATUS: FROZEN
- DECISION: Exclude full Shopify/WooCommerce integration, real refunds, real courier actions, production multi-tenancy, giant agent systems, training/fine-tuning, and broad ERP/inventory scope.
- REASON: Maximize judge-visible value within hackathon time.
- IMPACTED GATES: G1-G7
- COST IMPACT: Reduces infrastructure and integration cost.

## D-010 — AMD meaningful-workload proof
- DATE: 2026-10-06
- STATUS: FROZEN
- DECISION: Final demo must prove that AMD infrastructure powers a meaningful AI workload inside the product.
- REASON: AMD participation requirement must be demonstrated, not merely mentioned.
- IMPACTED GATES: G2, G6, G7, G8, G9
- EVIDENCE EXPECTED: AMD runtime/resource proof + real inference + application-visible result.

## D-011 — AMD Developer Cloud serving direction
- DATE: 2026-10-06
- STATUS: PROVISIONAL
- DECISION: Candidate serving path is an open model on AMD Developer Cloud / AMD Instinct using ROCm-compatible serving such as vLLM or SGLang.
- REASON: Matches event technology and product workload while avoiding model training.
- IMPACTED GATES: G2, G4
- REVIEW TRIGGER: Actual cloud availability, credit approval, compatibility, latency, or cost.

## D-012 — Hard payment block
- DATE: 2026-10-06
- STATUS: FROZEN
- DECISION: Do not add a payment method or launch paid GPU compute without explicit cost review and authorization.
- REASON: AMD Developer Cloud currently exposes a paid MI300X path while complimentary credit approval is still pending.
- IMPACTED GATES: G0, G2, G6
- COST IMPACT: Prevent accidental spend.
- STOP CONDITION: Any card, billing authorization, deposit, paid quota, or auto-recharge prompt.

## D-013 — Credit state
- DATE: 2026-10-06
- STATUS: ACTIVE
- DECISION: AMD complimentary cloud-credit request is treated as **SUBMITTED / PENDING APPROVAL**, not active credit.
- REASON: Confirmation page acknowledged the request but did not prove usable credit balance.
- IMPACTED GATES: G0, G2
- NEXT REVIEW: Activation/approval email or visible credit balance.

## D-014 — Public GitHub repository
- DATE: 2026-10-06
- STATUS: FROZEN
- DECISION: Canonical project repository is:
  `Hunter20202/reclaimgrid-ai`
- REASON: Public repository is required for project continuity and current submission planning.
- IMPACTED GATES: G0-G9
- SOURCE-OF-TRUTH RULE: Repository state overrides memory/chat summaries when they conflict.

## D-015 — Pre-kickoff implementation guardrail
- DATE: 2026-10-06
- STATUS: ACTIVE
- DECISION: Pre-kickoff work is restricted to research, architecture, documentation, security/cost controls, testing plans, environment/account setup, and submission planning.
- REASON: Current public ACT III pages do not clearly establish unrestricted pre-kickoff submission-code development.
- IMPACTED GATES: G0, G1
- BLOCKED: Product implementation code until rules are re-verified and Control Room authorizes build.

## D-016 — Schedule ambiguity
- DATE: 2026-10-06
- STATUS: ACTIVE
- DECISION: Do not treat the complete build window as finally frozen.
- REASON: Official pages currently conflict:
  - main event page: online build 12–18 October 2026
  - live/dashboard-style text: 12–17 October 2026
  - submission close currently visible as 18 October 2026 at 15:00 UTC
- IMPACTED GATES: G1, G8, G9
- REVIEW TRIGGER: Kickoff and final submission audit.

## D-017 — Minimal architecture
- DATE: 2026-10-06
- STATUS: PROVISIONAL
- DECISION: Prefer a small single-web-app architecture with deterministic domain logic, synthetic local data, and one narrow AMD AI gateway.
- REASON: Reliability, explainability, cost containment, and demo simplicity.
- IMPACTED GATES: G2-G6
- REJECTED BY DEFAULT: Microservices, Kubernetes, vector database, agent framework, workflow engine, large production database.

## D-018 — AI failure must not break economics
- DATE: 2026-10-06
- STATUS: FROZEN
- DECISION: Deterministic recovery ranking must remain usable when AI is unavailable, invalid, or timed out.
- REASON: Core business decision cannot depend on generative-service availability.
- IMPACTED GATES: G3-G7
- TEST REQUIREMENT: AI-offline fallback is mandatory.

## D-019 — Submission claim discipline
- DATE: 2026-10-06
- STATUS: FROZEN
- DECISION: Final quantitative claims must be explicitly tied to synthetic evaluation and stated assumptions unless real-world evidence later exists.
- REASON: Avoid misleading production/ROI claims.
- IMPACTED GATES: G7-G9
- ALLOWED STYLE: "On our synthetic evaluation set..." / "Under the stated assumptions..."

## D-020 — Evidence-before-PASS
- DATE: 2026-10-06
- STATUS: FROZEN
- DECISION: A gate cannot PASS without reproducible evidence and a verified main SHA.
- REASON: Visual confidence alone is insufficient.
- IMPACTED GATES: G0-G9

## D-021 — Competitive red-team finding
- DATE: 2026-10-06
- STATUS: FROZEN
- DECISION: Generic AI returns/NDR automation, confidence/explanation, highest-recovery disposition, and human-review workflows are not sufficient differentiation.
- REASON: 2026 competitor research found substantial overlap across Loop, Optoro, AfterShip, ClickPost, ReverseLogix, and related platforms.
- IMPACTED GATES: G1, G3, G4, G7
- DEMO/JUDGING IMPACT: The product must visibly demonstrate a more specific decision-science advantage.
- EVIDENCE: `09_COMPETITIVE_RESEARCH_AND_PRODUCT_UPGRADE.md`.

## D-022 — Recovery Decision Graph upgrade
- DATE: 2026-10-06
- STATUS: PROVISIONAL
- PREVIOUS DECISION: D-004, D-005
- DECISION: Upgrade the core from single-step route ranking to a bounded **Recovery Decision Graph** that propagates downstream recovery value across multi-stage outcomes.
- REASON: Multi-stage counterfactual path economics is more defensible and more judge-distinct than generic next-action recommendation.
- IMPACTED GATES: G1, G3, G5, G7
- COST IMPACT: Low; implementable with a small deterministic DAG and backward induction rather than heavy ML.
- DEMO/JUDGING IMPACT: Stronger originality, measurable business value, and visual clarity.
- REVIEW TRIGGER: G1/G3 feasibility freeze.

## D-023 — Decision robustness is mandatory V1
- DATE: 2026-10-06
- STATUS: PROVISIONAL
- DECISION: V1 must show a break-even threshold / one-dimensional sensitivity analysis for the top competing recovery paths and label decisions ROBUST or FRAGILE.
- REASON: Expected-value recommendations without sensitivity can create false precision; robustness is both commercially useful and judge-distinct.
- IMPACTED GATES: G3, G5, G7
- COST IMPACT: Low if limited to one dominant uncertain variable per case.
- DEMO/JUDGING IMPACT: Strengthens originality, transparency, and trust.
- REVIEW TRIGGER: G3 equation design.

## D-024 — AMD AI upgraded to evidence-grounded Case Interpreter
- DATE: 2026-10-06
- STATUS: PROVISIONAL
- PREVIOUS DECISION: D-006, D-010
- DECISION: The primary AMD-hosted AI workload must include bounded extraction of structured signals from messy NDR/return text with confidence, evidence span, and explicit missing fields; grounded explanation remains a second AI task.
- REASON: This makes AMD operationally central rather than decorative while preserving deterministic financial authority.
- IMPACTED GATES: G2, G4, G5, G7
- SECURITY IMPACT: Model output remains untrusted and schema-validated; AI cannot invent canonical financial values.
- DEMO/JUDGING IMPACT: Stronger Application of Technology score and clearer judge-visible AMD role.
- REVIEW TRIGGER: G2 model/runtime validation.

## D-025 — Decision Ledger
- DATE: 2026-10-06
- STATUS: PROVISIONAL
- DECISION: V1 must expose a decision ledger containing accepted AI evidence, policy rules, path calculations, winner/runner-up, break-even result, and human approval state.
- REASON: The ledger turns explainability and auditability into a concrete product feature rather than a documentation claim.
- IMPACTED GATES: G3-G7
- SECURITY IMPACT: Synthetic data only; no secret/PII logging.
- DEMO/JUDGING IMPACT: Strengthens trust, presentation, and originality.

## D-026 — Value Leak Map is should-have, not core blocker
- DATE: 2026-10-06
- STATUS: DEFERRED
- DECISION: Portfolio-level economic leakage by failure cause is a SHOULD-HAVE/STRETCH feature after the core graph is stable.
- REASON: It improves Track 3 business insight but must not steal time from the core decision engine.
- IMPACTED GATES: G5, G7
- COST IMPACT: Low-to-moderate.
- REVIEW TRIGGER: Core G3/G4 stability.

## D-027 — Multimodal condition analysis is stretch only
- DATE: 2026-10-06
- STATUS: DEFERRED
- DECISION: AMD-hosted image/condition interpretation may be added only if credits, runtime, model compatibility, and core stability permit.
- REASON: Visually impressive but overlaps existing market capabilities and increases GPU/runtime complexity.
- IMPACTED GATES: G2, G4, G7
- COST IMPACT: Potentially higher GPU/runtime cost.
- REVIEW TRIGGER: After G4 core PASS.

## D-028 — Safe originality framing
- DATE: 2026-10-06
- STATUS: FROZEN
- DECISION: Do not claim first-ever or that competitors lack returns optimization. Position differentiation around transparent multi-stage counterfactual recovery-path economics, robustness/break-even analysis, and evidence-grounded AMD AI.
- REASON: Competitor research proves adjacent capabilities already exist.
- IMPACTED GATES: G7-G9
- DEMO/JUDGING IMPACT: More credible pitch and lower overclaim risk.

## D-029 — Decision Hinge / Next Best Evidence
- DATE: 2026-10-06
- STATUS: PROVISIONAL
- PREVIOUS DECISION: D-023
- DECISION: For the hero FRAGILE case, V1 must identify the decision hinge (uncertain variable + break-even threshold) and recommend one bounded Next Best Evidence action before commitment.
- REASON: Sensitivity becomes operationally useful only when the user knows what evidence matters next. Reverse-logistics value-of-information literature supports the idea that reducing the right uncertainty can improve decisions.
- IMPACTED GATES: G3, G4, G5, G7
- COST IMPACT: Low; reuses the existing break-even engine.
- DEMO/JUDGING IMPACT: Strong "aha" moment and clearer commercial action.
- SCOPE LIMIT: Formal EVPI/EVSI, Bayesian updating, and learned probability calibration remain out of V1.
- EVIDENCE: `14_DECISION_HINGE_AND_NEXT_BEST_EVIDENCE.md`.

## D-030 — Position ReclaimGrid as a decision layer, not a workflow suite
- DATE: 2026-10-06
- STATUS: FROZEN
- PREVIOUS DECISION: D-004, D-021
- DECISION: Position ReclaimGrid as a recovery-intelligence decision layer that can sit above existing carrier, returns, WMS, inventory, or support systems rather than replacing mature workflow platforms.
- REASON: Competitor research shows workflow automation breadth is already strong in Loop, AfterShip, ClickPost, Optoro, and ReverseLogix.
- IMPACTED GATES: G1, G5, G7, G8
- DEMO/JUDGING IMPACT: Reduces direct feature-comparison risk and sharpens differentiation.
- EVIDENCE: `13_COMPETITOR_MATRIX_AND_WHITE_SPACE.md`.

## D-031 — AMD model selection ladder
- DATE: 2026-10-06
- STATUS: PROVISIONAL
- PREVIOUS DECISION: D-011, D-024
- DECISION: When credit becomes active, use Qwen3-8B + vLLM for the first AMD smoke/structured-output proof. Test Qwen3-32B or Qwen3-30B-A3B only if 8B fails task-quality thresholds and cost remains safe.
- REASON: AMD officially demonstrates Qwen3-8B on one MI300X and documents Qwen3-32B / Qwen3-30B-A3B support on one MI300X. The product's AI tasks are narrow and do not justify starting with a large model.
- IMPACTED GATES: G2, G4
- COST IMPACT: Minimizes credit burn and setup risk.
- SECURITY IMPACT: vLLM structured JSON output + application semantic validation remains mandatory.
- DEMO/JUDGING IMPACT: Increases probability of reliable AMD proof.
- EVIDENCE: `15_AMD_MODEL_AND_SERVING_PLAN.md`.
- REVIEW TRIGGER: Actual AMD credit activation and runtime availability.

## D-032 — Structured output is mandatory for Case Interpreter
- DATE: 2026-10-06
- STATUS: PROVISIONAL
- DECISION: The AMD Case Interpreter must use schema-constrained structured output plus semantic evidence-span validation; free-form extraction is not sufficient.
- REASON: vLLM supports structured outputs, but schema validity alone does not prove semantic correctness.
- IMPACTED GATES: G2, G4, G6
- SECURITY IMPACT: Reduces malformed/unsafe model-output risk.
- EVIDENCE: `15_AMD_MODEL_AND_SERVING_PLAN.md`.

## D-033 — Frontier red-team narrows originality
- DATE: 2026-10-06
- STATUS: FROZEN
- DECISION: Do not claim originality from agentic post-purchase decisioning, semantic return-note extraction, AI evidence review, dynamic return journeys, or ask-for-more-information workflows individually.
- REASON: Narvar's 2026 agentic post-purchase positioning and September 2026 SSADS research materially overlap those patterns; Happy Returns and ReverseLogix further reduce uniqueness of generic agentic returns/evidence workflows.
- IMPACTED GATES: G1, G4, G7, G8
- DEMO/JUDGING IMPACT: Forces a narrower, more defensible combined behavior.
- EVIDENCE: `16_FRONTIER_RED_TEAM_AND_DECISION_CERTIFICATE.md`.

## D-034 — Recovery Decision Certificate becomes primary judge artifact
- DATE: 2026-10-06
- STATUS: PROVISIONAL
- PREVIOUS DECISION: D-025, D-029
- DECISION: The hero experience must produce one Recovery Decision Certificate combining source evidence, path economics, winner/challenger, Decision Hinge, break-even, robustness, Decision Exposure, Action Gate, Next Best Evidence, AMD grounded output, and human approval.
- REASON: A single concrete certificate is easier to understand, demo, audit, and distinguish than a collection of dashboard features.
- IMPACTED GATES: G3-G8
- COST IMPACT: Low; assembly layer reuses existing canonical outputs.
- DEMO/JUDGING IMPACT: Stronger presentation, originality, and trust.
- REVIEW TRIGGER: G5 judge-flow implementation.

## D-035 — Decision Exposure
- DATE: 2026-10-06
- STATUS: PROVISIONAL
- PREVIOUS DECISION: D-023, D-029
- DECISION: V1 calculates maximum regret of the base-case winner across the single declared plausible interval and exposes it as Decision Exposure.
- REASON: A fragile label alone does not quantify whether uncertainty is economically material.
- IMPACTED GATES: G3, G5, G7
- COST IMPACT: Low for one-dimensional linear cases.
- CLAIM LIMIT: Decision Exposure is scenario-bounded opportunity cost, not guaranteed loss or failure probability.
- REVIEW TRIGGER: G3 hand-calculation validation.

## D-036 — Deterministic Action Gate
- DATE: 2026-10-06
- STATUS: PROVISIONAL
- DECISION: V1 derives ACT NOW / ASK FIRST / HUMAN REVIEW deterministically from robustness, Decision Exposure, a visible synthetic materiality threshold, evidence availability, and policy state.
- REASON: "Ask for more information" is common; the differentiator is the explicit economic rule controlling when to ask versus act or hand off.
- IMPACTED GATES: G3-G7
- SECURITY IMPACT: LLM cannot choose or override action mode.
- DEMO/JUDGING IMPACT: Converts uncertainty analysis into a useful commercial action.
- REVIEW TRIGGER: G3/G5 rule freeze.

## D-037 — One-dimensional uncertainty remains hard scope boundary
- DATE: 2026-10-06
- STATUS: FROZEN
- DECISION: V1 limits Decision Exposure and break-even analysis to one dominant uncertain variable per case.
- REASON: Preserves explainability and build reliability; avoids full stochastic/robust optimization complexity.
- IMPACTED GATES: G3-G7
- REJECTED FOR V1: multi-dimensional robust optimization, formal EVPI/EVSI, Bayesian updating, large scenario trees, minimax-regret optimization over many variables.

## D-038 — Credit activation is a G2 blocker, not a global build blocker
- DATE: 2026-10-07
- STATUS: FROZEN
- PREVIOUS DECISION: D-013, D-015
- DECISION: AMD complimentary credit activation does not block G0 completion or post-kickoff deterministic/local implementation. It blocks real AMD proof and therefore blocks G2 PASS.
- REASON: Official ACT III rules require meaningful AMD usage in the working product, but do not require complimentary credit to be active before local deterministic product work begins.
- IMPACTED GATES: G0, G1, G2, G3
- COST IMPACT: No paid GPU authorization is added. Payment/card hard-stop remains unchanged.
- DEMO/JUDGING IMPACT: Prevents wasting the short competition window while preserving genuine AMD proof requirements.
- EVIDENCE: `17_HACKATHON_CRITICAL_PATH.md`.
- REVIEW TRIGGER: Kickoff or official infrastructure guidance changes.

## D-039 — Independent gates may proceed in parallel after G1
- DATE: 2026-10-07
- STATUS: FROZEN
- PREVIOUS DECISION: D-002
- DECISION: Replace strict "every prior gate must PASS" sequencing with dependency-based gate control after G1. AMD Proof and Economics Core may proceed as independent lanes once their own prerequisites are met.
- REASON: G2 AMD credit availability is externally controlled, while G3 deterministic economics is local and independent. Strict serial sequencing would create avoidable schedule risk.
- IMPACTED GATES: G2-G5
- SECURITY IMPACT: No weakening of evidence, security, or payment controls.
- DEMO/JUDGING IMPACT: Increases probability of finishing a working product on time.
- EVIDENCE: `17_HACKATHON_CRITICAL_PATH.md`.

## D-040 — Conservative internal build-freeze target
- DATE: 2026-10-07
- STATUS: PROVISIONAL
- DECISION: Until kickoff resolves official-page inconsistencies, use 17 Oct 2026 as the internal build-freeze target and reserve 18 Oct for submission verification.
- REASON: Live dashboard currently says online build 12–17 Oct while submission closes 18 Oct 15:00 UTC; main page says online phase 12–18 Oct.
- IMPACTED GATES: G1, G7, G8, G9
- DEMO/JUDGING IMPACT: Adds schedule buffer and reduces last-day integration risk.
- REVIEW TRIGGER: Kickoff.

## D-041 — Podium bar becomes proof-heavy
- DATE: 2026-10-07
- STATUS: FROZEN
- DECISION: ReclaimGrid must ship not only the working product but also a judge-visible evaluation/proof surface: RecoveryBench, deterministic fixture results, adversarial proof, AMD runtime telemetry, and measured latency.
- REASON: Prior AMD podium submissions repeatedly showed measurable evaluation, adversarial/failure evidence, GPU telemetry, latency/throughput/cost, and reproducible tests rather than relying only on product claims.
- IMPACTED GATES: G2-G8
- DEMO/JUDGING IMPACT: Raises credibility across Application of Technology, Presentation, Business Value, and Originality.
- EVIDENCE: `18_DEEP_RESEARCH_WINNING_BAR.md`, `19_RECOVERYBENCH_EVAL_PLAN.md`.

## D-042 — Remove model-authored numerical confidence
- DATE: 2026-10-07
- STATUS: FROZEN
- PREVIOUS DECISION: D-024, D-032
- DECISION: Model-authored numerical confidence is removed from the authoritative Case Interpreter contract.
- REASON: Current calibration research shows verbalized/self-reported LLM confidence can be miscalibrated and task-dependent. Exact evidence, explicit unknowns, ambiguity flags, and application validation are more auditable.
- IMPACTED GATES: G2, G4-G7
- SECURITY IMPACT: Reduces false-authority risk from fluent but uncalibrated model outputs.
- REPLACEMENT: deterministic Evidence Status = GROUNDED / AMBIGUOUS / INCOMPLETE / INVALID.
- EVIDENCE: `20_AI_EVIDENCE_QUALITY_CONTRACT.md`.

## D-043 — RecoveryBench is the model-selection and proof gate
- DATE: 2026-10-07
- STATUS: PROVISIONAL
- DECISION: Model selection and final AI-quality claims must be based on the frozen RecoveryBench suite, not generic model reputation or benchmark prestige.
- REASON: ReclaimGrid's narrow tasks require task-specific evidence-grounding, unknown preservation, injection resistance, and latency testing.
- IMPACTED GATES: G2, G4, G6, G7
- COST IMPACT: Start with Qwen3-8B; test a larger model only if frozen quality thresholds are missed.
- EVIDENCE: `19_RECOVERYBENCH_EVAL_PLAN.md`.

## D-044 — No pivot; Track 3 remains the primary strategy
- DATE: 2026-10-07
- STATUS: PROVISIONAL UNTIL G1
- PREVIOUS DECISION: D-003
- DECISION: Keep ReclaimGrid as the Track 3 — Reinvent Commerce default. Do not pivot to generic NDR automation, disposition AI, fraud classification, demand forecasting, or a generic returns agent.
- REASON: Deep comparison found ReclaimGrid's current certificate/economics/evidence design has the best balance of Track fit, business value, originality, synthetic-data feasibility, AMD meaningfulness, and solo-build reliability.
- IMPACTED GATES: G1-G9
- REVIEW TRIGGER: Kickoff track/rule changes or verified technical infeasibility.
- EVIDENCE: `21_TRACK_FIT_AND_PIVOT_AUDIT.md`.

## D-045 — Partner prizes are subordinate to the core
- DATE: 2026-10-07
- STATUS: FROZEN
- DECISION: Priority order is: main AMD/Track 3 quality first; Vibe special through the same core; Google only if kickoff requirements/model fit align naturally; Evolus only as a late-stage extension after core integration PASS and adequate time remains.
- REASON: Partner integrations can create prize optionality but can also damage the main submission through scope and integration risk.
- IMPACTED GATES: G1, G5-G9
- COST IMPACT: No new paid dependency authorized.
- EVIDENCE: `21_TRACK_FIT_AND_PIVOT_AUDIT.md`.
## D-046 — Constraint-first optimization
- DATE: 2026-10-07
- STATUS: FROZEN
- PREVIOUS DECISION: D-005
- DECISION: ReclaimGrid must maximize EFRC only inside a deterministic Policy & Service Feasibility Envelope.
- REASON: A purely economic objective can produce commercially wrong decisions if policy, customer remedy, evidence sufficiency, or route availability is omitted. Recent reverse-logistics research and retail data reinforce the need to balance economic recovery with service/customer constraints.
- IMPACTED GATES: G3, G5-G7
- SECURITY/SAFETY IMPACT: Higher raw EFRC can never override a hard feasibility constraint.
- EVIDENCE: `22_DECISION_QUALITY_AND_BENCHMARK_INTEGRITY.md`.

## D-047 — No opaque CLTV / loyalty weighting in V1
- DATE: 2026-10-07
- STATUS: FROZEN
- DECISION: V1 must not invent customer lifetime value, churn probability, loyalty dollars, or hidden weighted multi-objective scores.
- REASON: Synthetic V1 lacks defensible behavioral data for those quantities. Service/customer value is represented through explicit constraints and visible tie-break rules.
- IMPACTED GATES: G3, G5, G7-G9
- DEMO/JUDGING IMPACT: More honest, auditable commercial reasoning.
- EVIDENCE: `22_DECISION_QUALITY_AND_BENCHMARK_INTEGRITY.md`.

## D-048 — RecoveryBench locked holdout and versioning
- DATE: 2026-10-07
- STATUS: PROVISIONAL
- PREVIOUS DECISION: D-043
- DECISION: RecoveryBench's 48 interpreter notes are split into DEV 32 + locked HOLDOUT 16. Public quality claims must separate DEV and HOLDOUT, record fixture/prompt/model/code identity, and version/rerun the benchmark if the contract changes after holdout scoring.
- REASON: Prevent prompt overfitting, fixture leakage, and cherry-picked public benchmark claims.
- IMPACTED GATES: G2, G4, G6, G7
- DEMO/JUDGING IMPACT: Makes the Proof surface materially more credible.
- EVIDENCE: `19_RECOVERYBENCH_EVAL_PLAN.md`, `22_DECISION_QUALITY_AND_BENCHMARK_INTEGRITY.md`.
## D-049 — Low-risk web stack freeze
- DATE: 2026-10-07
- STATUS: PROVISIONAL UNTIL G1
- DECISION: Default V1 implementation stack is Node 22.12+, Vite + React + TypeScript, Zod 4, @xyflow/react, Vitest, Playwright, Netlify static deploy + TypeScript Functions, no database/auth/agent framework.
- REASON: The product does not require SSR, persistence, or complex infrastructure; minimizing framework surface increases the probability of a reliable hackathon build.
- IMPACTED GATES: G1, G3-G7
- EVIDENCE: `23_TECHNICAL_FEASIBILITY_AND_BUILD_BLUEPRINT.md`.
- REVIEW TRIGGER: G1 or a verified build blocker.

## D-050 — Public AMD inference must use a bounded same-origin proxy
- DATE: 2026-10-07
- STATUS: FROZEN
- DECISION: Browser may not call AMD directly. Public AI requests go through a server-side Netlify Function accepting only allowlisted case/task identifiers with rate limiting, timeout, token bounds, fixed model selection, and a live-inference kill switch.
- REASON: Prevent secret exposure, prompt abuse, model switching, and GPU-credit exhaustion.
- IMPACTED GATES: G4-G6
- SECURITY/COST IMPACT: High positive impact.
- EVIDENCE: `23_TECHNICAL_FEASIBILITY_AND_BUILD_BLUEPRINT.md`, `04_SECURITY_COST_GUARDRAILS.md`.

## D-051 — Read-only graph visualization
- DATE: 2026-10-07
- STATUS: FROZEN
- DECISION: React Flow is used only as a small read-only visualization layer with deterministic positions. No graph editing, persistence, auto-layout dependency, or user-created graph state in V1.
- REASON: Judge value comes from seeing the recovery paths, not editing them.
- IMPACTED GATES: G5, G7
- COST/RISK IMPACT: Reduces UI/debugging risk.

## D-052 — AMD model ladder follows current MI300X support
- DATE: 2026-10-07
- STATUS: PROVISIONAL
- PREVIOUS DECISION: D-031, D-043
- DECISION: Do not assume Qwen3-8B is the first MI300X model. Current AMD support tables show Qwen3-32B and Llama-3.1-8B-Instruct as optimized MI300X paths. Inspect the actual cloud image, run the lowest-friction documented candidate, compare at most those two through RecoveryBench, then freeze one.
- REASON: Deployment reliability is more important than speculative parameter-count optimization.
- IMPACTED GATES: G2, G4
- COST IMPACT: Limits model testing to two candidates.
- REVIEW TRIGGER: Actual Developer Cloud runtime.

## D-053 — Exact M0–M15 implementation sequence
- DATE: 2026-10-07
- STATUS: FROZEN
- DECISION: Build milestones and feature-kill order are fixed in `24_IMPLEMENTATION_SEQUENCE_AND_RISK_REGISTER.md`. Core correctness/proof precedes visual polish.
- REASON: Removes architectural decision-making from the short build window and prevents scope creep.
- IMPACTED GATES: G1-G9
## D-054 — Material assumptions require provenance
- DATE: 2026-10-07
- STATUS: FROZEN
- DECISION: Every uncertain canonical input used by recovery economics must record base/range/unit/provenance; material assumptions are visible in the Decision Certificate.
- REASON: Synthetic assumptions are acceptable only when explicit and not presented as learned forecasts.
- IMPACTED GATES: G3, G5, G7-G9
- EVIDENCE: `25_JUDGE_ATTACK_FAILURE_SIMULATION_PREMORTEM.md`.

## D-055 — Dual fair baselines
- DATE: 2026-10-07
- STATUS: FROZEN
- DECISION: Final evaluation compares ReclaimGrid against both a Static Policy baseline and a Myopic Greedy immediate-step baseline using identical inputs and feasibility constraints.
- REASON: Avoid a strawman comparison and isolate the value of downstream path reasoning.
- IMPACTED GATES: G3, G6-G8

## D-056 — Multi-factor uncertainty fails safe
- DATE: 2026-10-07
- STATUS: FROZEN
- DECISION: If multiple unresolved material uncertain variables can change the winner, V1 must not label the case ROBUST; it marks multi-factor uncertainty and defaults to HUMAN REVIEW unless a bounded rule resolves it.
- REASON: One-dimensional sensitivity is a scope limit, not permission to create false certainty.
- IMPACTED GATES: G3, G5-G7

## D-057 — Judge-facing language is plain
- DATE: 2026-10-07
- STATUS: FROZEN
- DECISION: First-view UI/pitch uses plain labels such as Expected Recovery Value, Flip Point, Value at Risk, Act/Ask/Review, and Decision Certificate. Internal terms remain in Proof/README.
- REASON: Prior AMD submission feedback shows technically strong projects can lose clarity through presentation density.
- IMPACTED GATES: G5, G7-G9

## D-058 — No AMD hardware-superiority overclaim
- DATE: 2026-10-07
- STATUS: FROZEN
- DECISION: Claim only measured AMD usage/performance. Do not claim AMD is uniquely required or faster than another hardware vendor without a direct benchmark.
- REASON: Official requirement is meaningful AMD integration, not unsupported hardware superiority.
- IMPACTED GATES: G2, G7-G9

---

## FUTURE DECISION ENTRY TEMPLATE

### D-XXX — <decision title>
- DATE: YYYY-MM-DD
- STATUS: PROVISIONAL | FROZEN | ACTIVE | SUPERSEDED | REJECTED | DEFERRED
- PREVIOUS DECISION: D-XXX or N/A
- DECISION:
- REASON:
- ALTERNATIVES CONSIDERED:
- IMPACTED GATES:
- SECURITY IMPACT:
- COST IMPACT:
- DEMO/JUDGING IMPACT:
- EVIDENCE:
- MAIN SHA:
- REVIEW TRIGGER:
- NOTES:

## NEXT SAFE ACTION
Keep implementation blocked pre-kickoff. Continue only research/math/fixture/judge-story hardening until G1 authorization and AMD credit status allow progression.
