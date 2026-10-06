# RECLAIMGRID AI — NEW-CHAT RESUME PACKET

## CONTROL
- PROJECT: ReclaimGrid AI
- CONTROL CODE: RG-ACT3
- FILE: 26_NEW_CHAT_RESUME_PACKET.md
- DATE: 2026-10-07
- PURPOSE: Make a new ChatGPT conversation recover the exact project state without relying on imperfect conversational memory.

## AUTHORITATIVE REPOSITORY
Repository:
https://github.com/Hunter20202/reclaimgrid-ai

Default branch:
main

Verified main immediately before this resume packet:
`afda1eda4b462302b23d8e639cd1a70ad6208304`

The live repository overrides remembered chat state.

## RESUME COMMAND
In any new chat, the user may say:

**RG-ACT3 RESUME**

or:

**RECLAIMGRID RESUME**

Required assistant behavior:
1. inspect the live latest `main` SHA,
2. read `00_MASTER_STATE.md`,
3. read this file `26_NEW_CHAT_RESUME_PACKET.md`,
4. inspect any canonical file named by the current NEXT SAFE ACTION,
5. compare live state with remembered state,
6. if SHA/state differs, trust the live repository,
7. continue from the first unresolved safe action only.

Never restart discovery from zero unless the repository is unavailable.

## USER WORKING STYLE
- Bangla-first.
- Technical terms may remain English with short Bangla explanation.
- One exact action at a time.
- User should not be asked to decide architecture/security/model/cloud details that the Control Room can determine.
- After each implementation step: verify output, checkpoint SHA, then continue.
- `next` means: inspect live state first, then perform/give only the next safe action.
- `check` means: verify current state without mutating unless explicitly authorized.
- Avoid giving a large batch of tasks to the user.

## CURRENT PROJECT THESIS
ReclaimGrid AI is an AMD-powered ecommerce recovery-intelligence decision layer for failed deliveries and returns.

It is NOT:
- a generic returns portal,
- a generic NDR bot,
- a support chatbot,
- a courier automation suite,
- a warehouse management system,
- an autonomous refund agent.

Core judge-facing promise:
**Find the best recovery path — and prove why it wins.**

## CURRENT PRIMARY TRACK
ACT III Track 3 — Reinvent Commerce.

Status:
PROVISIONAL until G1 kickoff rules re-verification because official pages have changed dynamically.

## CURRENT PRODUCT CORE
The frozen product flow is:

Synthetic Case + Raw Operational Note
-> Validation
-> AMD Case Interpreter
-> Evidence Validator / Evidence Quality
-> Policy & Service Feasibility Envelope
-> Recovery Decision Graph
-> Multi-stage Deterministic Path Economics
-> Counterfactual Ranking
-> Break-even / Flip Point
-> Decision Exposure / Value at Risk
-> Action Gate
-> Next Best Evidence
-> Recovery Decision Certificate
-> AMD Grounded Explanation
-> Human Approval
-> RecoveryBench Proof

## FINANCIAL AUTHORITY
LLM financial authority:
**ZERO**

Canonical financial/scoring calculations are deterministic.

AMD AI may:
- interpret messy operational evidence,
- return bounded structured semantic signals,
- cite exact evidence spans,
- preserve ambiguity/unknowns,
- explain an already-computed decision,
- draft a bounded evidence-request message.

AMD AI may NOT:
- author canonical prices,
- author canonical costs,
- author canonical probabilities,
- choose the winner,
- alter break-even,
- alter Decision Exposure,
- choose Action Gate,
- override policy/service constraints,
- execute consequential external actions.

## EVIDENCE QUALITY CONTRACT
Do not use model-authored numerical confidence as authority.

Deterministic Evidence Quality states:
- GROUNDED
- AMBIGUOUS
- INCOMPLETE
- INVALID

Exact evidence spans are preferred over model self-confidence.

## POLICY & SERVICE FEASIBILITY ENVELOPE
Before economics, a path must satisfy:

`FeasibleActions = PolicyAllowed ∩ ServiceAllowed ∩ EvidenceSupported ∩ OperationallyAvailable`

Hard constraints include:
- merchant rules,
- retry limit,
- approved customer remedy / SLA,
- evidence sufficiency,
- condition restrictions,
- route/provider availability.

Higher raw EFRC can never override a hard constraint.

V1 forbids:
- fabricated CLTV,
- fabricated churn probability,
- fabricated loyalty-dollar value,
- opaque weighted multi-objective scoring.

## RECOVERY ECONOMICS
Core metric:
Expected Future Recovery Contribution (EFRC), presented to judges as **Expected Recovery Value**.

Core differentiators:
- compare full feasible recovery paths,
- include downstream consequences,
- explicit break-even / Flip Point,
- ROBUST vs FRAGILE,
- Decision Exposure,
- Action Gate,
- Next Best Evidence.

## DECISION HINGE / ROBUSTNESS
Hero example RG-001:
- RETRY EFRC: 46.20
- STOP_AND_RTO EFRC: 35.00
- break-even redelivery success probability: ~55.6%
- base probability: 68%
- plausible range: 45%–80%
- status: FRAGILE
- Decision Exposure: 9.50
- synthetic materiality threshold: 5.00
- Action Gate: ASK_FIRST
- Next Best Evidence: confirm customer availability for next delivery window

## MULTI-FACTOR UNCERTAINTY
V1 uses one-dimensional sensitivity per case.

If multiple unresolved material uncertain variables can each change the winner:
- do not label ROBUST,
- mark multi-factor uncertainty,
- default Action Gate to HUMAN_REVIEW unless an explicit bounded rule resolves it.

Do not add multidimensional stochastic optimization in V1.

## ASSUMPTION REGISTER
Every material uncertain canonical input must expose:
- field
- base value
- plausible low/high range
- unit
- provenance
- entered_by
- evidence/reference when available

Allowed V1 provenance:
- synthetic fixture
- merchant provided
- policy defined
- deterministic derivation

AI-generated hidden assumptions are forbidden.

## FAIR BASELINES
Final evaluation must compare:
1. Static Policy
2. Myopic Greedy immediate-step value
3. ReclaimGrid full-path result

All three must use identical:
- inputs,
- policy/service constraints,
- probabilities,
- economics assumptions.

No strawman baseline.
At least some cases may tie or show no uplift.

## RECOVERY DECISION CERTIFICATE
This is the primary judge artifact.

It should show:
- recommended action,
- why,
- Expected Recovery Value,
- challenger,
- Flip Point,
- Value at Risk,
- Act / Ask / Review,
- Next Best Evidence,
- business/customer constraints preserved,
- assumption provenance,
- AMD evidence,
- technical proof link,
- human approval state.

## JUDGE-FACING LANGUAGE
Prefer plain first-view labels:
- Expected Recovery Value
- Flip Point
- Value at Risk
- Act / Ask / Review
- Decision Certificate
- Evidence Quality
- Business Rules & Customer Commitments

Keep internal terms such as EFRC, Decision Hinge, Decision Exposure, and Feasibility Envelope in technical docs/Proof/README.

## RECOVERYBENCH
Mandatory proof system.

Planned frozen sets:
- Case Interpreter: 48 notes
  - DEV: 32
  - locked HOLDOUT: 16
- adversarial: 16
- deterministic economics fixtures: 20
- certificate integrity fixtures: 12
- real AMD runtime measurements

Public benchmark must record:
- RecoveryBench version
- fixture SHA
- prompt-contract version
- model
- serving stack
- AMD hardware
- code SHA
- run date

If prompt/schema changes after HOLDOUT scoring:
increment benchmark version and rerun compared candidates.

## PODIUM PROOF TARGET
Final product should show:
- deterministic fixture correctness,
- certificate integrity,
- RecoveryBench holdout quality,
- adversarial authority escapes,
- AMD runtime evidence,
- GPU / ROCm / vLLM / model,
- p50/p95 latency,
- token/runtime/cost evidence when measured,
- last audited SHA.

No placeholder or invented metric.

## AMD MODEL / SERVING PLAN
Do not freeze the final model until real runtime is available.

Current documented MI300X candidate strategy:
- Qwen3-32B
- Llama-3.1-8B-Instruct

Inspect the actual AMD Developer Cloud runtime first.
Compare at most these two unless both materially fail.

Selection priority:
1. authority/safety boundary,
2. evidence grounding,
3. task accuracy,
4. reliability,
5. latency,
6. cost,
7. model prestige last.

Serving:
- vLLM OpenAI-compatible server
- structured output for Case Interpreter
- non-thinking default
- bounded prompts/output

## PUBLIC AI SECURITY / COST
Browser must never call AMD directly.

Use same-origin server-side proxy.

Client may not control:
- arbitrary prompt,
- model,
- max tokens,
- AMD endpoint,
- API key,
- canonical financial values.

Initial public rate-limit target:
- 4 AI calls / 60 seconds / IP+domain

Hard kill switch:
`AMD_LIVE_ENABLED=false`

Modes:
- DEV_MOCK
- LIVE_AMD
- VERIFIED_RECORDED

Never label mock/recorded output as live.

## DEFAULT IMPLEMENTATION STACK
Subject only to G1 rule change or a verified blocker:

- Node.js 22.12+
- Vite
- React
- TypeScript
- strict TypeScript
- Zod 4
- @xyflow/react read-only
- Vitest
- Playwright
- Netlify static deploy
- TypeScript Netlify Function for AMD proxy
- one decimal arithmetic adapter/library
- no database
- no auth
- no ORM
- no queue
- no vector DB
- no agent framework

## EXACT BUILD ORDER — M0 TO M15
After G1 PASS:

M0 — repository scaffold
M1 — domain contracts
M2 — Policy & Service Feasibility Envelope
M3 — Recovery Decision Graph + economics
M4 — robustness / Flip Point / Decision Exposure
M5 — Action Gate + Next Best Evidence
M6 — Recovery Decision Certificate
M7 — RecoveryBench infrastructure
M8 — judge UI shell
M9 — AI gateway + mock provider
M10 — real AMD proof
M11 — grounded Decision Explainer
M12 — end-to-end integration
M13 — Proof surface
M14 — security / cost / release hardening
M15 — judge experience / submission

Core correctness/proof precedes visual polish.

## FEATURE-KILL ORDER
If schedule slips, kill in this order:
1. multimodal condition AI
2. Value Leak Map
3. two-variable sensitivity
4. downloadable certificate
5. fancy graph animation
6. extra case types
7. extra dashboard cards
8. secondary model benchmark
9. secondary demo polish
10. optional partner integration

Never kill:
- feasibility envelope
- deterministic economics
- break-even
- Decision Exposure
- Action Gate
- Recovery Decision Certificate
- RecoveryBench
- real AMD proof
- fallback
- core security

## PARTNER-PRIZE PRIORITY
Priority:
1. Main AMD / Track 3 quality
2. Vibe special through same core
3. Google only if kickoff requirements/model fit align naturally
4. Evolus only after core G5 PASS and enough time remains

No partner integration may weaken the main submission.

## CURRENT OFFICIAL-PAGE CAUTION
Official ACT III page content has changed across snapshots.

Latest main-page recheck on 2026-10-07 currently showed:
- online phase 12–18 Oct 2026
- total prize pool $12,000+
- AMD prize $5,000
- Google prize $5,000
- Track 3 — Reinvent Commerce
- judging: Application of Technology, Presentation, Business Value, Originality
- Event Schedule still "To be announced"
- submissions described as original and MIT-compliant

However, live/dashboard pages previously showed:
- online build 12–17 Oct
- submission close 18 Oct 15:00 UTC
- Tracks: TBA

Therefore G1 MUST re-verify all official pages at kickoff.

## CURRENT GATE STATE
- G0: PASS
- G1: WAITING FOR KICKOFF / NOT YET PASSABLE
- G2: BLOCKED BY SAFE AMD CREDIT/COMPUTE
- G3: BLOCKED ONLY BY PRE-KICKOFF G1 HOLD
- G4–G9: NOT STARTED

Gate control after G1 is dependency-based:
- G2 AMD Proof and G3 Economics Core may proceed independently.
- Credit delay must not block deterministic/local build.
- G4 requires real AMD proof + stable schemas.
- G5 integrates deterministic + AI lanes.
- G6–G9 remain sequential.

## AMD CREDIT STATE
Last verified:
- complimentary credit request submitted
- approval/activation email not received
- visible complimentary credit not active
- Credits applied: $0.00
- Total usage: $0.00
- Estimated balance owed: $0.00
- payment method: none
- GPU resource: none
- paid MI300X path previously showed $1.99/hour and Billing ACTION NEEDED

Hard rule:
- no payment method
- no paid GPU
- no paid quota/upgrade action
- no GPU launch until a safe approved credited/no-charge route is verified

## CURRENT PRE-KICKOFF STATE
Product ideation is considered saturated.

Do not add cosmetic features.

Only meaningful pre-kickoff triggers:
1. official rule/track/deadline changes,
2. AMD credit/runtime availability,
3. materially stronger competitive evidence,
4. verified architectural blocker.

No implementation code before G1 authorization.

## NEW-CHAT NEXT SAFE ACTION
If resumed before kickoff and no AMD credit activation:
- verify live main SHA,
- verify `00_MASTER_STATE.md`,
- do not invent work,
- wait for a material trigger.

If AMD credit arrives before kickoff:
- read-only verify credit first,
- do not create a GPU until the safe plan is checked.

At kickoff:
1. perform G1 official rules/track/deadline re-verification,
2. freeze compliance,
3. authorize implementation if allowed,
4. start M0/M1 and G3 immediately,
5. run G2 in parallel when safe AMD compute is available.

## CANONICAL FILE MAP
Core control:
- `00_MASTER_STATE.md`
- `01_RULES_SNAPSHOT.md`
- `02_PRODUCT_SCOPE.md`
- `03_ARCHITECTURE.md`
- `04_SECURITY_COST_GUARDRAILS.md`
- `05_TEST_EVIDENCE_PLAN.md`
- `06_SUBMISSION_CHECKLIST.md`
- `07_DECISION_LOG.md`
- `08_CHANGELOG.md`

Research / hardening:
- `09_COMPETITIVE_RESEARCH_AND_PRODUCT_UPGRADE.md`
- `10_RECOVERY_ECONOMICS_DESIGN.md`
- `11_SYNTHETIC_FIXTURE_BLUEPRINT.md`
- `12_JUDGE_STRATEGY.md`
- `13_COMPETITOR_MATRIX_AND_WHITE_SPACE.md`
- `14_DECISION_HINGE_AND_NEXT_BEST_EVIDENCE.md`
- `15_AMD_MODEL_AND_SERVING_PLAN.md`
- `16_FRONTIER_RED_TEAM_AND_DECISION_CERTIFICATE.md`
- `17_HACKATHON_CRITICAL_PATH.md`
- `18_DEEP_RESEARCH_WINNING_BAR.md`
- `19_RECOVERYBENCH_EVAL_PLAN.md`
- `20_AI_EVIDENCE_QUALITY_CONTRACT.md`
- `21_TRACK_FIT_AND_PIVOT_AUDIT.md`
- `22_DECISION_QUALITY_AND_BENCHMARK_INTEGRITY.md`
- `23_TECHNICAL_FEASIBILITY_AND_BUILD_BLUEPRINT.md`
- `24_IMPLEMENTATION_SEQUENCE_AND_RISK_REGISTER.md`
- `25_JUDGE_ATTACK_FAILURE_SIMULATION_PREMORTEM.md`
- `26_NEW_CHAT_RESUME_PACKET.md` — this file

## SOURCE-OF-TRUTH PRIORITY
1. live verified GitHub main
2. `00_MASTER_STATE.md`
3. this resume packet
4. other canonical control/research files
5. current verified browser/account state
6. chat/memory summaries

If remembered state conflicts with live GitHub:
**GitHub wins.**

## FINAL RESUME RULE
A new chat must never assume the old remembered SHA is current.

Always recheck live `main` first.

Then continue only from the first unresolved safe action.
