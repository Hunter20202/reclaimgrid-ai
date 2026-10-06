# RECLAIMGRID AI — PRODUCT SCOPE

## CONTROL
- PROJECT: ReclaimGrid AI
- CONTROL CODE: RG-ACT3
- FILE: 02_PRODUCT_SCOPE.md
- SNAPSHOT DATE: 2026-10-07
- STATUS: PROVISIONAL V1 SCOPE FREEZE — RESEARCH UPGRADED
- CURRENT GATE: G1 — Rules & Scope Freeze (WAITING FOR KICKOFF)
- IMPLEMENTATION STATUS: NOT STARTED
- PURPOSE: Freeze the strongest judge-ready V1 scope before kickoff without writing submission implementation code.

## PRODUCT ONE-LINER
ReclaimGrid AI is an AMD-powered Recovery Decision Graph that maps the economically valid recovery paths after ecommerce delivery failures and returns, calculates which path preserves the most value, and shows whether that decision is robust or fragile under uncertainty.

## TAGLINE
**Find the best recovery path — and prove why it wins.**

## JUDGE-VISIBLE CORE OUTPUT
The primary product artifact is the **Recovery Decision Certificate**.

For the hero case it must combine:
- accepted source evidence,
- eligible/excluded recovery paths,
- winner + runner-up,
- EFRC values and value gap,
- Decision Hinge,
- break-even threshold,
- ROBUST / FRAGILE,
- Decision Exposure,
- deterministic Action Gate: ACT NOW / ASK FIRST / HUMAN REVIEW,
- Next Best Evidence when relevant,
- AMD-grounded explanation/draft,
- human approval state.

This certificate is the compact proof that ReclaimGrid is a decision layer, not a generic workflow suite.

## CORE PROBLEM
Ecommerce merchants lose money after failed deliveries, returns, open-box parcels, damaged returns, and aging returned inventory because decisions are often made one step at a time through static rules, siloed tools, or manual judgment.

The stronger question is not:
"What should we do next?"

It is:
**Which permitted recovery path produces the best bounded economic outcome from this point forward, including downstream outcomes if the first action succeeds or fails?**

## PRIMARY USER
### V1 user
Small-to-mid-size ecommerce operations / post-purchase / returns team.

### User job-to-be-done
Given a failed-delivery or return case, choose a recovery path quickly while:
- protecting recoverable value,
- understanding the economic consequence of alternatives,
- seeing when the decision is sensitive to uncertain assumptions,
- avoiding opaque AI-only financial decisions.

## V1 CASE TYPES
V1 should support a deliberately small set of synthetic cases:
1. Failed delivery / NDR
2. Returned/open-box item
3. Aging returned inventory

Additional case types are deferred unless the core engine is already stable.

## RECOVERY DECISION GRAPH
ReclaimGrid models a case as a small state graph rather than one isolated recommendation.

Candidate states:
- DELIVERY_EXCEPTION
- CUSTOMER_RESPONSE
- RETURN_TO_ORIGIN
- RETURN_RECEIVED
- RECOVERY_INVENTORY
- CLOSED

Candidate actions depend on state and may include:
- redelivery / reattempt
- request correction / reschedule
- return to origin
- exchange / store credit
- refund / close
- restock / relist
- refurbish then relist
- liquidation

Exact state/action set is frozen in G3 and must remain small enough for a reliable hackathon demo.

## V1 INPUTS
Candidate bounded synthetic schema:
- case_id
- current_state
- case_type
- item_value
- product_cost
- shipping_cost
- reverse_shipping_cost
- redelivery_cost
- refurbishment_cost
- expected_resale_value
- expected_liquidation_value
- inventory_age_days
- condition
- customer/carrier free-text note
- merchant policy constraints
- customer remedy / service constraints
- operational availability constraints
- route/action eligibility flags
- explicit uncertain assumptions such as redelivery_success_probability or resale_probability

No AI-generated financial number becomes canonical input without explicit human confirmation.

## POLICY & SERVICE FEASIBILITY ENVELOPE

ReclaimGrid must not maximize recovery value across every mechanically possible action.

First compute:

`FeasibleActions = PolicyAllowed ∩ ServiceAllowed ∩ EvidenceSupported ∩ OperationallyAvailable`

Candidate hard constraints:
- merchant reattempt limit
- approved customer remedy / promised SLA
- confirmed refusal or delivery-window requirement
- condition-grade restrictions
- evidence required for condition/address-dependent actions
- route/provider/capacity availability

Paths outside the envelope are excluded with explicit reasons.

V1 must NOT invent customer lifetime value, churn probability, loyalty dollars, or hidden multi-objective weights.

Among feasible paths only, deterministic EFRC chooses the best recovery path.

See `22_DECISION_QUALITY_AND_BENCHMARK_INTEGRITY.md`.

## DETERMINISTIC RECOVERY PATH OPTIMIZER

### Role
This is the financial authority for V1.

For a bounded acyclic recovery graph:

**Expected Value(state, action)**
= Immediate Net Contribution
+ sum over outcomes [ Probability(outcome) × Expected Value(next_state) ]

using only explicit, validated assumptions and costs.

### It must
- evaluate all eligible paths,
- include downstream recovery consequences,
- apply explicit costs,
- enforce the Policy & Service Feasibility Envelope,
- rank feasible paths,
- expose the math,
- show the winning path and runner-up,
- show the value gap,
- preserve identical results for identical inputs.

### Non-negotiable rule
The language model must NOT:
- invent financial inputs,
- silently change costs/probabilities,
- become the sole forecaster,
- decide hidden financial weights,
- override deterministic policy eligibility,
- directly execute consequential business actions.

## ROBUSTNESS / BREAK-EVEN ENGINE
A single expected-value number is not enough.

For the top competing paths, V1 must analyze the dominant uncertain variable and show:
- current assumption,
- break-even threshold,
- winner-to-runner-up value gap,
- ROBUST or FRAGILE decision label.

Examples:
- redelivery wins only if success probability stays above X%
- refurbish wins only if resale value remains above $Y
- liquidation becomes better after inventory age/markdown crosses threshold Z

V1 should prefer one-dimensional sensitivity per case. Two-variable sensitivity is stretch only.

## DECISION HINGE / NEXT BEST EVIDENCE
For any FRAGILE hero decision, V1 must turn sensitivity into an operational next step.

Show:
- hinge variable,
- current assumption,
- plausible range,
- break-even threshold,
- hinge distance,
- optional bounded Hinge Exposure,
- one "Next Best Evidence" action.

Example:
If RETRY wins at 68% but flips below 55.6%, ReclaimGrid may advise confirming customer availability before committing.

Rules:
- the hinge and threshold come from deterministic math,
- Decision Exposure is calculated over the declared one-dimensional plausible range,
- the deterministic Action Gate chooses ACT NOW / ASK FIRST / HUMAN REVIEW,
- AMD AI may draft the information-gathering message,
- AMD AI may not invent the probability/value or choose the Action Gate,
- formal EVPI/EVSI optimization is out of V1 scope.

See `14_DECISION_HINGE_AND_NEXT_BEST_EVIDENCE.md`.

## AMD AI LAYER

### Mandatory meaningful workload 1 — Case Interpreter
The AMD-hosted open model receives messy return/NDR text and returns a bounded schema such as:
- reason_code
- customer_intent
- address_status
- condition_hint
- urgency_hint
- evidence spans by field
- ambiguity_flags
- missing_fields

The AI must ground extracted signals in exact source text and explicitly preserve unknowns.

Model-authored numerical confidence is NOT authoritative and is excluded from the canonical Case Interpreter contract.

Application-side evidence status is deterministic:
- GROUNDED
- AMBIGUOUS
- INCOMPLETE
- INVALID

See `20_AI_EVIDENCE_QUALITY_CONTRACT.md`.

### Mandatory meaningful workload 2 — Decision Explainer
The model receives the canonical deterministic decision package and may:
- explain why the winning path wins,
- summarize the tradeoff versus the runner-up,
- describe the break-even/sensitivity result,
- draft a merchant next-action note,
- optionally draft a customer-facing message.

It may not alter canonical economics.

### Optional stretch — Multimodal condition signal
Only if AMD runtime/credits/model support are stable:
- analyze a synthetic returned-item image,
- produce bounded condition evidence,
- require human confirmation before deterministic use.

This is not a V1 blocker.

## DECISION LEDGER
Every judge-visible decision should preserve:
- source inputs,
- AI-extracted signals,
- evidence spans + deterministic Evidence Status,
- policy rules fired,
- eligible/excluded paths,
- deterministic calculations,
- winning path,
- runner-up,
- break-even/robustness result,
- human approval/rejection.

This is both an explainability feature and a trust artifact.

## HUMAN APPROVAL
V1 is decision support, not unrestricted autonomous execution.

Before any consequential action:
- show winning path,
- show expected recovery value,
- show runner-up and value gap,
- show assumptions,
- show robustness/break-even,
- show AI explanation,
- require explicit human approval.

For the hackathon V1, approval records a demo decision only. It must not trigger a real refund, payment, shipment, inventory mutation, or customer account change.

## SYNTHETIC DEMO DATA
Default data source: reproducible synthetic ecommerce recovery cases.

Required fixture types:
- clear-win case
- close-call case
- policy-excluded path
- missing-information case
- free-text AMD AI interpretation case
- fragile decision case
- robust decision case
- AI unavailable/fallback case

## BASELINE
Use a defensible stage-specific static policy baseline with the same canonical inputs.

Example:
- first NDR -> reattempt once
- clean received return -> restock
- damaged/open-box -> liquidate
- otherwise -> refund/close

The baseline must not be intentionally weak, must not use worse inputs, and must not call AI.

## DEMO SUCCESS METRICS

Primary:
1. Total baseline expected recovered value
2. Total ReclaimGrid expected recovered value
3. Absolute uplift
4. Percentage uplift
5. Cases where the chosen path changes
6. Average opportunity-cost avoided

Decision quality:
7. Robust vs fragile recommendation count
8. Number of ineligible paths safely excluded
9. Break-even threshold shown for hero case

AMD / proof:
10. Valid structured extraction
11. Evidence-grounding and UNKNOWN-preservation metrics
12. Prompt-injection authority escapes = 0 on the frozen adversarial suite
13. Judge-visible real AMD inference
14. Measured p50/p95 latency and runtime metadata
15. AI failure fallback without economics failure

## HERO DEMO CASE
Preferred hero:
**Failed delivery where the obvious next action is not automatically optimal.**

Show:
1. messy carrier/customer note,
2. AMD AI evidence-grounded extraction,
3. eligible recovery graph,
4. reattempt path including downstream RTO recovery if failure occurs,
5. immediate-RTO alternative,
6. deterministic path values,
7. winning path,
8. break-even redelivery-success threshold,
9. AMD AI explanation,
10. human approval.

This single case proves cross-stage reasoning, deterministic economics, AMD value, uncertainty handling, and governance.

## SECONDARY DEMO CASE
Returned/open-box item.

Compare:
- restock/relist,
- refurbish then relist,
- liquidation.

Show a fragile case where the best choice changes at a resale-value or refurbishment-cost threshold.

## V1 MUST-HAVES
- synthetic case dataset
- Recovery Decision Graph
- deterministic multi-stage path expected value
- Policy & Service Feasibility Envelope
- explicit exclusion reasons for infeasible paths
- winning path + runner-up + value gap
- break-even / robustness analysis
- Decision Hinge + Next Best Evidence for the hero fragile case
- Decision Exposure + deterministic Action Gate
- Recovery Decision Certificate
- visible formulas/assumptions
- AMD AI evidence-grounded case extraction with deterministic Evidence Status
- RecoveryBench frozen evaluation suite with DEV / locked HOLDOUT split
- benchmark version + fixture/prompt/code SHA
- judge-visible Proof surface with measured AMD/eval evidence
- AMD AI grounded explanation
- human approval
- Decision Ledger
- baseline-vs-ReclaimGrid evaluation
- clean end-to-end demo
- public GitHub repository
- judge-visible proof that AMD powers meaningful AI workload

## V1 SHOULD-HAVES
Only after MUST-HAVES are stable:
- portfolio Value Leak Map showing economic leakage by cause
- simple assumption slider
- worst/base/best scenarios
- concise dashboard
- downloadable decision evidence

## V1 STRETCH
- multimodal AMD condition signal
- two-variable sensitivity heatmap
- portfolio-level avoidable value leak map

## V1 NON-GOALS
Explicitly OUT OF SCOPE unless later re-authorized:
- full Shopify integration
- full WooCommerce integration
- real courier/NDR integration
- real payment/refund execution
- real inventory mutation
- generic customer support chatbot
- generic returns management suite
- generic inventory management
- end-to-end warehouse management
- omnichannel ERP
- autonomous multi-agent system
- model training / fine-tuning
- reinforcement-learning optimizer
- giant forecasting model
- dozens of states/routes
- production multi-tenant SaaS
- complex authentication/roles
- large database architecture
- mobile app
- partner-track complexity that does not strengthen core scoring

## DIFFERENTIATION
ReclaimGrid must NOT present itself as merely:
- an NDR chatbot,
- a returns chatbot,
- a returns portal,
- a generic "highest recovery channel" router,
- a generic AI agent that recommends actions.

Core differentiation:
**Multi-stage counterfactual recovery-path economics + break-even/robustness analysis + evidence-grounded AMD AI + human-governed decision ledger.**

## SAFE ORIGINALITY CLAIM
Do not claim no competitor does returns optimization.

Safe framing:
**AI automation, failed-delivery recovery, and return disposition already exist. ReclaimGrid's hackathon differentiation is transparent multi-stage recovery-path economics, decision robustness, and evidence-grounded AMD AI rather than AI financial authority.**

## JUDGING ALIGNMENT
Application of Technology:
- AMD-hosted case interpretation and grounded explanation are central to the flow.

Business Value:
- expected recovered value, opportunity cost, and baseline uplift are measurable.

Originality:
- recovery graph + counterfactual path economics + break-even robustness.

Presentation:
- messy note -> AMD extraction -> path graph -> math -> threshold -> Decision Exposure -> Action Gate -> Next Best Evidence -> Recovery Decision Certificate -> approval is visually clear.

## SCOPE KILL TEST
Any proposed V1 feature must pass all three:
1. Does it strengthen a judging criterion?
2. Does it materially improve the end-to-end demo or measurable business value?
3. Can it be built, tested, and explained safely within hackathon time?

If NO to any one, defer it.

## PROVISIONAL FREEZE RULE
This upgraded scope is the pre-kickoff default.

Changes are allowed only if:
- kickoff rules require them,
- AMD environment constraints require them,
- a critical technical feasibility issue appears,
- or a clearly superior simplification is verified.

All material changes must be recorded in `07_DECISION_LOG.md`.

## EXIT CRITERIA FOR PRODUCT SCOPE
Before implementation begins, G1 must confirm:
- Track 3 remains valid,
- official implementation timing permits build,
- AMD proof path is feasible,
- state/action graph is bounded,
- path equations are bounded,
- uncertainty variables are bounded,
- baseline is defined,
- metrics are defined,
- non-goals remain excluded.

## RECOVERYBENCH / PROOF REQUIREMENT
Podium-oriented V1 must include a frozen, reproducible evaluation suite and a compact judge-facing Proof surface.

RecoveryBench covers:
- Case Interpreter quality
- evidence grounding
- unknown preservation
- adversarial trust-boundary tests
- deterministic economics fixtures
- Recovery Decision Certificate integrity
- real AMD runtime performance

No benchmark number is published until measured.

See:
- `19_RECOVERYBENCH_EVAL_PLAN.md`
- `20_AI_EVIDENCE_QUALITY_CONTRACT.md`

## RESEARCH BASIS
See:
- `09_COMPETITIVE_RESEARCH_AND_PRODUCT_UPGRADE.md`
- `13_COMPETITOR_MATRIX_AND_WHITE_SPACE.md`
- `14_DECISION_HINGE_AND_NEXT_BEST_EVIDENCE.md`
- `15_AMD_MODEL_AND_SERVING_PLAN.md`
- `16_FRONTIER_RED_TEAM_AND_DECISION_CERTIFICATE.md`
- `18_DEEP_RESEARCH_WINNING_BAR.md`
- `19_RECOVERYBENCH_EVAL_PLAN.md`
- `20_AI_EVIDENCE_QUALITY_CONTRACT.md`
- `21_TRACK_FIT_AND_PIVOT_AUDIT.md`
- `22_DECISION_QUALITY_AND_BENCHMARK_INTEGRITY.md`

## NEXT SAFE ACTION
Keep implementation blocked until kickoff/rules re-verification and AMD credit state permit progression. Use the research window only for further validation, math design, fixture design, and judge-story hardening.


---

## JUDGE-HARDENING ADDENDUM — 2026-10-07

### Assumption Register
Every uncertain canonical input used by the economics engine must record:
- field name
- base value
- low/high range
- unit
- provenance
- entered_by
- evidence/reference when available

Allowed V1 provenance:
- synthetic fixture
- merchant provided
- policy defined
- deterministic derivation

An AI model may not silently create a canonical financial/probability assumption.
Material assumptions must appear in the Decision Certificate.

### Fair baseline ablation
Final evaluation uses two non-AI baselines with the same inputs and constraints:

1. **Static Policy** — fixed stage-specific merchant rule.
2. **Myopic Greedy** — highest immediate feasible next-step value, ignoring downstream recovery consequences.

ReclaimGrid then evaluates complete feasible recovery paths including downstream outcomes.

This comparison isolates the value of multi-stage path reasoning and prevents a deliberately weak baseline.

### Multi-factor uncertainty fail-safe
V1 keeps one-dimensional sensitivity for explainability.

If multiple unresolved material uncertain variables can each change the winning path:
- do not label the case ROBUST,
- mark multi-factor uncertainty,
- route to HUMAN REVIEW unless one explicit bounded rule resolves the ambiguity.

V1 must prefer honest escalation over false precision.

### Judge-facing wording
Prefer:
- Expected Recovery Value
- Flip Point
- Value at Risk
- Act / Ask / Review
- Decision Certificate

Keep internal terms such as EFRC, Decision Hinge, and Decision Exposure in technical proof/documentation.

Research basis:
`25_JUDGE_ATTACK_FAILURE_SIMULATION_PREMORTEM.md`
