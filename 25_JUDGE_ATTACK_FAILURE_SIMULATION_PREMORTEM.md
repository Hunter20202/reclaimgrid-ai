# RECLAIMGRID AI — JUDGE ATTACK, FAILURE SIMULATION & PRE-MORTEM

## CONTROL
- PROJECT: ReclaimGrid AI
- CONTROL CODE: RG-ACT3
- FILE: 25_JUDGE_ATTACK_FAILURE_SIMULATION_PREMORTEM.md
- DATE: 2026-10-07
- STATUS: PRE-KICKOFF RED-TEAM / NOT IMPLEMENTED
- PURPOSE: Assume skeptical judges, live-demo failure, synthetic-data criticism, AI-necessity criticism, and novelty attacks before build begins.

## EXECUTIVE VERDICT

The current product is strong enough to keep.

The remaining risk is no longer "is the idea interesting?"

The remaining risks are:
1. judge does not understand it fast enough,
2. judge thinks AMD is decorative,
3. judge thinks synthetic economics are arbitrary,
4. judge thinks the baseline is weak,
5. judge sees false precision in probability assumptions,
6. live AMD inference fails,
7. presentation becomes too dense,
8. business-value claims overreach the evidence,
9. multiple uncertainties invalidate the one-dimensional hinge,
10. the public app is technically polished but does not prove why ReclaimGrid is better.

This pre-mortem hardens those failure points.

---

# 1. OFFICIAL JUDGE BAR — CURRENT PAGE

Current ACT III official page says projects are judged on:
- Application of Technology
- Presentation
- Business Value
- Originality

Track 3 asks the demo to turn customer/business data into a useful recommendation or action and show measurable impact on revenue, margin, conversion, retention, inventory, or service quality.

AMD requirement:
a meaningful part of the working product shown to judges must run on AMD infrastructure/hardware.

Current page also shows:
- online phase 12–18 Oct 2026
- $12,000+ total prize pool
- $5,000 AMD prizes
- $5,000 Google prizes
- MIT-compliant submissions
- Event Schedule still "To be announced"

Official source:
https://lablab.ai/ai-hackathons/amd-developer-hackathon-act-iii

CONTROL NOTE:
These event details remain volatile until G1 kickoff freeze.

---

# 2. PRIOR WINNER LESSON — TECHNICAL DEPTH IS NOT ENOUGH

A recent AMD submission, Apohara-ContextForge, reported:
- 310 unit tests
- 15/15 benchmark scenarios
- substantial technical optimization claims

But visible feedback said the presentation was too dense and needed:
- simpler business story,
- clearer user workflow,
- stronger competitor comparison.

Source:
https://lablab.ai/submissions/jgjdir9i67lr88o7gjccqlqj

Conclusion:
ReclaimGrid must not let research depth become demo density.

Judge-facing language must be dramatically simpler than internal architecture language.

---

# 3. PRESENTATION LANGUAGE FREEZE

Internal term -> Judge-facing label

- EFRC -> Expected Recovery Value
- Decision Hinge -> Flip Point
- Decision Exposure -> Value at Risk if Assumption Is Wrong
- Policy & Service Feasibility Envelope -> Business Rules & Customer Commitments
- Evidence Status -> Evidence Quality
- Recovery Decision Certificate -> Decision Certificate
- Counterfactual path economics -> Compare Every Valid Recovery Path
- Action Gate -> Act / Ask / Review

Technical terms remain in:
- README
- architecture
- Proof tab
- appendix/deck

Hero UI should lead with plain language.

---

# 4. JUDGE ATTACK: "WHY IS AMD/AI NEEDED?"

## Attack
"The deterministic engine makes the decision. Isn't AMD just decorating the product?"

## Strong answer
The deterministic engine intentionally owns money and policy.
AMD solves a different hard problem:
**turning messy operational evidence into structured decision inputs safely and quickly.**

Without the model:
- an operator must manually normalize the carrier/customer note,
- mark unknowns,
- identify evidence,
- then feed the structured case into the economics engine.

With AMD:
- raw note becomes bounded structured evidence,
- exact source spans are preserved,
- missing/ambiguous fields are surfaced,
- the deterministic engine can act on accepted evidence.

The fallback proves safety, not irrelevance.

## Required visible proof
Hero must visibly show:

RAW NOTE
-> AMD INTERPRETER
-> exact grounded facts
-> Evidence Quality
-> deterministic decision

Do not hide AMD in a backend badge.

---

# 5. JUDGE ATTACK: "WHY NOT JUST A RULE ENGINE?"

## Attack
"Could this be a spreadsheet or rules engine?"

## Answer
Rules decide what is allowed.
ReclaimGrid then evaluates the downstream expected value of every feasible recovery path, including what happens if the first action fails.

The strongest proof is not prose.
It is an ablation.

## NEW REQUIRED BASELINES

### Baseline A — Static Policy
Example:
first NDR -> retry once.

### Baseline B — Myopic Greedy
Choose the action with the highest immediate next-step value and ignore downstream path consequences.

### ReclaimGrid
Compare full feasible recovery paths including downstream outcomes.

All three use:
- same case,
- same costs,
- same probabilities,
- same service/policy constraints.

This isolates the value of multi-stage path reasoning.

---

# 6. JUDGE ATTACK: "YOUR SYNTHETIC PROBABILITIES ARE MADE UP"

## Attack
"Where did 68% retry success come from?"

## Correct answer
For the hackathon, it is an explicitly synthetic scenario assumption.
We do not present it as a learned or empirical forecast.

The product's job is:
- show the assumption,
- show its provenance,
- show the plausible range,
- show the exact flip point,
- show whether the decision depends on it.

Future production deployments could estimate/calibrate these inputs from merchant history.

## NEW REQUIRED ASSUMPTION REGISTER

Every uncertain canonical input must record:

- field
- base value
- low/high range
- unit
- provenance
- entered_by
- evidence/reference if available

Allowed provenance in V1:
- SYNTHETIC_FIXTURE
- MERCHANT_PROVIDED
- POLICY_DEFINED
- DERIVED_DETERMINISTIC

Not allowed:
- AI_GUESSED
- HIDDEN_DEFAULT

Example:
```text
redelivery_success_probability
base: 0.68
range: 0.45–0.80
provenance: SYNTHETIC_FIXTURE
```

Certificate must expose material assumptions.

---

# 7. JUDGE ATTACK: "YOU CAN CHOOSE THE RANGE TO FORCE ASK_FIRST"

## Attack
"If you choose 45–80%, you control whether the decision looks fragile."

## Answer
Correct — the range is an input, so provenance must be explicit.

The product does not claim the range is objectively true.
It says:
**given this declared range, here is whether the recommendation is robust.**

## Control
- range provenance visible,
- no model-generated hidden interval,
- locked fixture values,
- sensitivity result changes transparently if the range changes.

---

# 8. JUDGE ATTACK: "WHAT IF TWO UNCERTAINTIES MATTER?"

## Attack
"One-dimensional break-even is oversimplified."

## Answer
V1 deliberately limits sensitivity to one dominant uncertain variable for explainability.

But it must not falsely label a case robust when multiple unresolved material uncertainties exist.

## NEW RULE
If more than one decision-relevant uncertain variable is simultaneously:
- unresolved,
- material,
- and capable of changing the winner,

then:
**do not issue ROBUST.**

Preferred V1 behavior:
- Action Gate -> HUMAN_REVIEW
- certificate says MULTI_FACTOR_UNCERTAINTY
- no fake single-variable certainty

This preserves scope without false precision.

---

# 9. JUDGE ATTACK: "YOUR BASELINE IS A STRAWMAN"

## Control
Use both:
- Static Policy baseline
- Myopic Greedy baseline

Report:
- cases where baseline already wins/ties
- cases where ReclaimGrid changes action
- cases where no uplift exists

Do not optimize fixture composition to manufacture a huge uplift.

## Strong business chart
For each case:
- Static Policy EV
- Myopic Greedy EV
- ReclaimGrid EV

Then aggregate.

If ReclaimGrid ties:
show the tie.

---

# 10. JUDGE ATTACK: "IS THIS REAL ROI?"

## Answer
No.

Use phrase:
**synthetic scenario economics**

Do not say:
- proven merchant ROI
- saves X% in production
- increases profit by X% for real retailers

Allowed:
- "On our frozen synthetic benchmark, ReclaimGrid avoids X of modeled opportunity cost versus the stated baselines."

This claim must be reproducible from fixtures.

---

# 11. JUDGE ATTACK: "WHAT IS ACTUALLY ORIGINAL?"

## Weak answer
"We use AI and economics for returns."

Reject.

## Strong answer
"The hackathon differentiation is the Decision Certificate: it compares full delivery-to-recovery paths, shows the exact assumption where the winner flips, quantifies the modeled downside of being wrong, and gates the operator to act, ask, or review — while AMD structures messy evidence but cannot control the financial decision."

Do not claim:
- first ever
- nobody else does return optimization
- unique in all commerce

---

# 12. JUDGE ATTACK: "AMD COULD BE REPLACED BY ANY GPU"

## Correct answer
Do not make a false hardware exclusivity claim.

Say:
- AMD is the real infrastructure used for the working AI component,
- MI300X/ROCm/vLLM runtime is measured and shown,
- the application is architected around an open-model, self-hostable inference boundary,
- RecoveryBench demonstrates the chosen AMD-hosted model meets the task requirement.

Do NOT claim:
- ReclaimGrid only works on AMD,
- AMD is faster than NVIDIA unless directly benchmarked,
- AMD uniquely enables the deterministic economics.

Official requirement is meaningful AMD use, not fabricated hardware superiority.

---

# 13. JUDGE ATTACK: "IF AI FAILS, YOUR PRODUCT STILL WORKS — SO IS AI MEANINGFUL?"

## Answer
Safety fallback is a strength.

Distinguish:
- **manual structured fallback**: operator supplies structured evidence
- **AMD-assisted path**: raw unstructured note is normalized automatically

Judge should see the difference in workflow burden.

## Optional measured proof
RecoveryBench may report:
- AMD interpreter latency,
- structured-output quality,
- number of decision-relevant fields extracted from raw notes.

Do not invent human time-saved metrics unless actually measured.

---

# 14. LIVE DEMO PRE-MORTEM

Assume the demo fails.

## Failure A — GPU endpoint unavailable
Fallback:
- UI visibly says LIVE AMD UNAVAILABLE
- deterministic case still works from frozen structured evidence
- Proof tab shows previously verified AMD run as RECORDED
- demo video contains real LIVE_AMD capture

Do not silently substitute mock.

## Failure B — model returns invalid JSON
- validator rejects
- Evidence Quality = INVALID
- no economic mutation
- fallback/manual structured path

## Failure C — model extracts wrong field
- evidence span + semantics fail benchmark or human check
- critical ambiguity -> HUMAN_REVIEW
- no automatic high-impact action

## Failure D — network/function timeout
- clean timeout
- one manual retry maximum
- no retry storm
- deterministic core preserved

## Failure E — React graph fails
Fallback:
- certificate still shows path table
- graph is visualization, not source of truth

## Failure F — Proof metrics fail to load
- local committed sanitized report fallback
- do not invent metrics

## Failure G — rate limit triggers during judge demo
Mitigation:
- only hero interaction requires minimal AI calls
- preflight quota before recording/live session
- rate-limit rule must leave enough capacity for normal judge path

---

# 15. SUBMISSION REVIEW PRE-MORTEM

Assume a judge spends only 60–90 seconds.

They must learn, in order:

### 0–10 sec
Problem:
"After a failed delivery or return, the best next action depends on what happens after that action too."

### 10–25 sec
AMD:
raw note -> grounded structured evidence.

### 25–50 sec
Decision:
compare valid paths -> winner/challenger -> flip point.

### 50–65 sec
Risk/action:
Value at Risk -> ACT / ASK / REVIEW.

### 65–80 sec
Proof:
RecoveryBench + AMD runtime + deterministic tests.

### 80–90 sec
Business:
synthetic baseline comparison.

Do not start with:
- architecture diagram
- ROCm explanation
- 15 feature cards
- competitor history
- formula derivation

---

# 16. DEMO INTERACTION BUDGET

Hero demo should require at most:

1. Select/open RG-001
2. Run AMD Evidence Analysis
3. Approve / show ASK FIRST message

Everything else should appear automatically.

No login.
No setup wizard.
No free-form chatbot.
No settings journey.

---

# 17. RECOVERY DECISION CERTIFICATE — JUDGE ORDER

Display order:

1. Recommended action
2. Why
3. Expected Recovery Value
4. Challenger
5. Flip Point
6. Value at Risk
7. Act / Ask / Review
8. Next Best Evidence
9. Business/customer constraints preserved
10. Assumption provenance
11. AMD evidence
12. technical proof link

The judge should not need to understand every internal term before seeing the decision.

---

# 18. NEW ASSUMPTION / PROVENANCE TESTS

Required:
- no canonical uncertain input without provenance
- no AI_GUESSED provenance allowed
- hidden default rejected
- changed range changes robustness transparently
- certificate lists material assumptions
- synthetic assumption clearly labeled
- deterministic derived value identifies source inputs

---

# 19. NEW MULTI-UNCERTAINTY TESTS

Required:
- one dominant uncertainty -> normal hinge flow
- two non-material uncertainties -> normal flow allowed
- two material winner-changing uncertainties -> MULTI_FACTOR_UNCERTAINTY
- MULTI_FACTOR_UNCERTAINTY cannot produce ROBUST
- Action Gate defaults to HUMAN_REVIEW unless a bounded rule explicitly resolves one factor

No multidimensional optimization is added.

---

# 20. BUSINESS-VALUE PROOF HIERARCHY

Show in this order:

1. system correctness
2. safety/constraint correctness
3. AI evidence quality
4. AMD runtime proof
5. baseline comparison
6. synthetic economic uplift

Reason:
a large synthetic uplift is meaningless if the engine is wrong.

---

# 21. "KILL THE FEATURE" PRE-MORTEM

If any new feature does not directly improve:
- judge comprehension,
- measured proof,
- business-value evidence,
- AMD meaningfulness,
- or demo reliability,

kill it.

Do not add:
- chat
- dashboard analytics
- customer segmentation
- live courier integration
- CLTV model
- fraud model
- Shopify connector
- generative visual effects
- more agents

---

# 22. JUDGE RED-TEAM SCORECARD

Before G7, score each from 0–2:

## Application of Technology
- AMD visible in core workflow
- real runtime proof
- AI has a meaningful but bounded role

## Presentation
- problem clear in 10 sec
- decision clear in 50 sec
- proof clear in 80 sec

## Business Value
- real merchant problem
- two fair baselines
- reproducible synthetic economics

## Originality
- competitor overlap acknowledged
- Decision Certificate behavior clear
- no first-ever overclaim

Target:
**8/8 before G8 freeze.**

Any 0 blocks submission freeze.
A 1 requires explicit remediation or accepted rationale.

---

# 23. PRE-MORTEM CONCLUSION

If ReclaimGrid loses despite technically working, the most likely reasons are:

1. judges think it is too complex,
2. AMD looks bolted on,
3. synthetic assumptions look arbitrary,
4. business uplift looks rigged,
5. novelty claim is too broad,
6. live AI is unreliable,
7. proof is buried.

The hardening response is now frozen:
- plain-language UI
- visible AMD evidence transformation
- Assumption Register
- Static + Myopic baselines
- multi-factor uncertainty fail-safe
- Decision Certificate first
- Proof surface second
- live/recorded mode honesty

## NEXT SAFE ACTION

Sync these attack findings into canonical scope/tests/judge/submission controls.
After that, avoid additional feature ideation pre-kickoff unless a new official rule or materially stronger competitive finding appears.
