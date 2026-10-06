# RECLAIMGRID AI — RECOVERY ECONOMICS DESIGN

## CONTROL
- PROJECT: ReclaimGrid AI
- CONTROL CODE: RG-ACT3
- FILE: 10_RECOVERY_ECONOMICS_DESIGN.md
- DESIGN DATE: 2026-10-06
- STATUS: PRE-KICKOFF FORMULA DESIGN / NOT IMPLEMENTED
- PURPOSE: Define a transparent, testable, state-relative economic model for the Recovery Decision Graph before coding begins.

## DESIGN GOAL
The economics engine must answer:

> From the current decision point forward, which allowed recovery path preserves the most expected economic value under explicit assumptions?

It must not mix:
- sunk costs,
- future costs,
- AI guesses,
- or hidden weights.

---

# 1. SUNK-COST FENCE

Every case has a **decision timestamp/state**.

Only cash/value changes that occur **after that decision point** are included in path comparison.

Costs already incurred before the decision point are sunk and excluded unless they differ between candidate paths.

Examples:
- original acquisition cost may already be sunk
- original outbound shipping may already be sunk
- a refund already issued before the current state is sunk
- future redelivery, reverse shipping, handling, refurbishment, markdown, and refund outflows are included if they still depend on the chosen path

This prevents double-counting and makes cross-path comparisons auditable.

---

# 2. VALUE UNIT

V1 uses one canonical metric:

**Expected Future Recovery Contribution (EFRC)**

Definition:
Expected merchant economic value from the current decision point forward, under the explicit synthetic assumptions for the case.

EFRC is not:
- accounting profit,
- guaranteed recovered revenue,
- a real-world ROI claim.

It is a scenario-comparison metric for the synthetic decision model.

---

# 3. TERMINAL OUTCOME VALUES

Every bounded recovery path ends in a terminal outcome with a state-relative value.

Illustrative terminal outcomes:

## SUCCESSFUL_DELIVERY
Potential future value:
- retained order value still at risk
- minus any remaining action cost

## REFUND_AND_RESTOCK
Potential future value:
- negative future refund outflow if not already sunk
- plus expected restock/resale value
- minus future return/handling cost

## REFUND_AND_REFURBISH_RESELL
Potential future value:
- negative future refund if applicable
- plus expected resale value after refurbishment
- minus refurbishment/handling cost

## REFUND_AND_LIQUIDATE
Potential future value:
- negative future refund if applicable
- plus liquidation proceeds
- minus future handling cost

## CLOSE_WITH_LOSS
Potential future value:
- negative future refund/write-off still pending
- minus remaining unavoidable costs

Exact values depend on the current state so the engine must not apply one universal formula blindly.

---

# 4. GENERAL GRAPH EQUATION

For a state `s` and allowed action `a`:

`EV(s,a) = ImmediateNet(s,a) + Σ_o [ P(o | s,a) × V(next(s,a,o)) ]`

Where:
- `ImmediateNet` = future cash/value change caused immediately by the action
- `o` = bounded outcome
- `P(o | s,a)` = explicit probability assumption
- `V(next)` = expected value of the next state or terminal outcome

For a terminal state:
`V(terminal) = TerminalFutureValue(terminal)`

For a non-terminal state:
`FeasibleActions(s) = PolicyAllowed ∩ ServiceAllowed ∩ EvidenceSupported ∩ OperationallyAvailable`

`V(s) = max over a ∈ FeasibleActions(s) of EV(s,a)`

Hard feasibility constraints are applied before economic optimization.

This is simple backward induction over a bounded DAG.

No reinforcement learning is required.

---

# 5. HERO NDR CASE EQUATION

At `DELIVERY_EXCEPTION`, compare:

## Action A — REATTEMPT
Let:
- `C_retry` = incremental reattempt cost
- `p` = probability reattempt succeeds
- `V_success` = future value if delivered successfully
- `V_fail` = optimal downstream value if retry fails and case moves to RTO/return recovery

Then:

`EV_retry(p) = -C_retry + p × V_success + (1-p) × V_fail`

## Action B — STOP_AND_RTO
Let:
- `V_stop` = downstream value of moving directly to RTO/return recovery

Then:

`EV_stop = V_stop`

Winning action:
- retry if `EV_retry > EV_stop`
- stop/RTO if `EV_stop > EV_retry`
- deterministic tie rule if equal

---

# 6. BREAK-EVEN PROBABILITY

Solve:
`EV_retry(p*) = EV_stop`

Given:
`EV_retry(p) = -C_retry + pV_success + (1-p)V_fail`

Then:

`p* = (V_stop + C_retry - V_fail) / (V_success - V_fail)`

when denominator is non-zero.

Interpretation:
- if current `p > p*`, retry is economically preferred
- if current `p < p*`, stop/RTO is preferred

Validation:
- if `p*` < 0, one action dominates throughout [0,1]
- if `p*` > 1, one action dominates throughout [0,1]
- if denominator = 0, report no finite probability threshold

This threshold is judge-visible.

---

# 7. ROBUST VS FRAGILE

Do NOT create an arbitrary AI confidence score.

Each synthetic uncertain parameter has an explicit plausible interval:
- low
- base
- high

Example:
- redelivery success probability: 0.45 / 0.65 / 0.80

Decision classification:

## ROBUST
The same winning path remains best across the entire plausible interval.

## FRAGILE
The winning path changes somewhere inside the plausible interval.

The break-even threshold shows exactly where.

This is more defensible than labeling a decision "high confidence" without a mathematical basis.

---

# 8. DECISION EXPOSURE

For the base-case winning action `a*` over the declared one-dimensional plausible interval `X=[L,U]`:

`Regret(x,a*) = BestEV(x) - EV(a*,x)`

`DecisionExposure(a*) = max_{x in X} Regret(x,a*)`

For V1's linear hero cases, evaluate:
- lower endpoint,
- upper endpoint,
- break-even point if it lies inside the interval.

Interpretation:
**Maximum expected-value opportunity cost of sticking with the base-case winner over the stated scenario range.**

This is not:
- guaranteed loss,
- probability of failure,
- AI confidence.

The UI should use wording such as:
"Potential decision exposure under stated scenario range."

---

# 9. ACTION GATE

Use a visible synthetic merchant materiality threshold `M`.

### ACT_NOW
When:
- decision is ROBUST, OR
- decision is FRAGILE but `DecisionExposure < M`.

### ASK_FIRST
When:
- decision is FRAGILE,
- `DecisionExposure >= M`,
- and one bounded evidence request maps to the hinge variable.

### HUMAN_REVIEW
When:
- required evidence is unavailable,
- policy is ambiguous,
- AI evidence is invalid/conflicting,
- no valid path remains,
- or rules explicitly require a person.

The Action Gate is deterministic.

AMD AI may draft an ASK_FIRST message but cannot choose `M`, alter the exposure calculation, or silently switch action mode.

---

# 10. RECOVERY DECISION CERTIFICATE

The judge-facing product object should assemble:

- current state
- source evidence
- accepted AMD extraction
- policy/eligibility
- full recovery paths
- winner and runner-up
- EFRC values
- value gap
- hinge variable
- plausible range
- break-even threshold
- ROBUST / FRAGILE
- Decision Exposure
- Action Gate
- Next Best Evidence
- AMD grounded explanation/draft
- human approval state
- baseline comparison

This certificate reuses the same canonical calculations and does not create a second source of truth.

---

# 11. OPEN-BOX RETURN CASE

At `RETURN_RECEIVED`, possible actions:

## RELIST
`EV_relist = p_resale × NetResaleValue - handling_cost - expected_markdown_cost`

## REFURBISH_THEN_RELIST
`EV_refurb = -refurb_cost + p_refurb_success × (p_resale_after × NetResaleAfterRefurb) + (1-p_refurb_success) × V_refurb_fail`

## LIQUIDATE
`EV_liquidate = liquidation_value - liquidation_handling_cost`

Policy may exclude RELIST for a damage grade.

Dominant uncertainty for the demo may be:
- resale value
- resale probability
- refurbishment cost

Only one dominant sensitivity dimension is mandatory.

---

# 12. INVENTORY TIME DECAY

Returned inventory can lose recoverable value with delay.

Simple optional V1 model:

`AdjustedResaleValue = BaseResaleValue × (1 - decay_rate × days_waited)`

with floor at zero.

Alternative:
Use explicit synthetic markdown tiers rather than continuous decay.

V1 choice should prioritize explainability.

No learned demand forecast is required.

---

# 13. BASELINE FAIRNESS

Baseline and ReclaimGrid must use:
- same canonical item values
- same costs
- same state
- same probability assumptions
- same terminal-value definitions

The only intended difference:
- baseline follows a fixed stage-specific rule
- ReclaimGrid evaluates all eligible counterfactual paths

This avoids a rigged comparison.

---

# 14. OPPORTUNITY COST

For each case:

`OpportunityCostAvoided = ReclaimGrid_EV - Baseline_EV`

Dataset total:

`TotalOpportunityCostAvoided = Σ case OpportunityCostAvoided`

If negative:
show it honestly.

A strong system must contain fixtures where:
- baseline is already optimal
- ReclaimGrid ties baseline
- ReclaimGrid changes the decision
- ReclaimGrid can expose a negative/fragile candidate

---

# 15. POLICY & SERVICE FEASIBILITY CONSTRAINTS

The optimizer is not allowed to maximize over impossible, unsupported, policy-violating, or service-violating paths.

Examples:
- no more reattempts after limit
- confirmed refusal blocks another forced redelivery
- approved customer remedy / promised SLA cannot be silently downgraded
- damaged item cannot be sold as new
- certain products cannot be refurbished
- liquidate route unavailable in a region
- action missing required evidence is blocked
- route/provider/capacity unavailable means the path is infeasible

Mathematically:
`FeasibleActions(s) ⊆ AllActions(s)`

Optimization only occurs over `FeasibleActions(s)`.

V1 explicitly rejects an opaque weighted score such as:
`w1 × margin + w2 × loyalty + w3 × service`

because the weights and loyalty values would not be defensible with synthetic data. Customer/service value is represented through transparent hard constraints and, only when required, explicit deterministic tie-break rules.

---

# 16. MISSING DATA

Never convert missing into zero silently.

If a mandatory value is missing:
- block affected path,
- explain missing field,
- allow other fully specified paths if safe,
- or require human input.

AI may identify that a field is missing; AI may not invent it.

---

# 17. PROBABILITY SOURCE DISCIPLINE

For the synthetic hackathon demo, probabilities are explicit scenario assumptions.

Label them clearly:
- synthetic assumption
- merchant-provided assumption
- or derived fixture assumption

Do not claim they are empirically trained probabilities.

Future product potential may learn/calibrate them from historical data, but that is outside V1.

---

# 18. PRECISION / ROUNDING

Recommended internal math:
- decimal currency representation or integer cents
- avoid binary floating-point equality for money
- round only at presentation boundaries when possible

Tie rule:
- define deterministic epsilon or exact cents comparison
- if economically equal within chosen tolerance, prefer the lower-risk / lower-cost action only if that rule is explicit

Exact implementation rule freezes in G3.

---

# 19. REQUIRED HAND-CALCULATED FIXTURES

Before G3 PASS:
1. hero NDR retry vs stop case
2. retry clearly dominates
3. stop/RTO clearly dominates
4. break-even lies inside plausible p interval
5. break-even lies outside [0,1]
6. open-box relist vs liquidation
7. refurbish path with downstream failure branch
8. policy-excluded highest-value route
9. no eligible path
10. baseline already optimal
11. negative uplift
12. zero baseline denominator for percentage uplift

Each fixture needs:
- input table
- hand calculation
- expected engine output

---

# 20. VISUAL OUTPUT CONTRACT

For the hero case, the UI should show:

- Current state
- Source note
- AMD extracted signals
- Eligible paths
- Excluded paths + reason
- Winner
- Runner-up
- Winner EFRC
- Runner-up EFRC
- Value gap
- Dominant uncertain assumption
- Plausible low/base/high
- Break-even threshold
- ROBUST / FRAGILE
- Decision Exposure
- Action Gate: ACT NOW / ASK FIRST / HUMAN REVIEW
- Next Best Evidence when applicable
- Recovery Decision Certificate status
- Baseline decision + EFRC
- Opportunity cost avoided
- Human approval

---

# 21. WHY THIS IS JUDGE-STRONG

Application of Technology:
- AMD extracts meaningful unstructured evidence used by the decision system.

Business Value:
- economics is directly quantified.

Originality:
- multi-stage path value + explicit break-even robustness + judge-visible Recovery Decision Certificate.

Presentation:
- graph + winner + threshold creates a visual "aha" moment.

Trust:
- no black-box AI financial authority.

---

# 22. RESEARCH BASIS

Recent reverse-logistics decision-support work explicitly uses simulation, multi-criteria ranking, and sensitivity analysis to test strategy robustness under operational uncertainty:
https://doi.org/10.1108/BPMJ-01-2026-0150

A 2026 systematic review emphasizes decision making under uncertainty as a growing reverse-logistics research area:
https://doi.org/10.1016/j.cie.2026.112241

Recent semantic-signal research also shows narrative return notes can feed a separate recovery optimizer, which means ReclaimGrid cannot claim that architecture alone as novel:
https://arxiv.org/abs/2609.02116

Industry validation for highest-value reverse-logistics decisioning:
https://www.mckinsey.com/industries/logistics/our-insights/from-cost-center-to-competitive-advantage-modernizing-reverse-logistics-with-ai

This document does not claim these mathematical ideas are novel by themselves. ReclaimGrid's hackathon product value comes from combining them into a transparent post-purchase Recovery Decision Graph with evidence-grounded AMD AI.

## NEXT SAFE ACTION
Keep the V1 uncertainty model one-dimensional per case. Implement Decision Exposure and Action Gate only after G1 authorizes build; do not expand into full stochastic/robust optimization during the hackathon.


---

## JUDGE-HARDENING ECONOMICS ADDENDUM — 2026-10-07

### Assumption provenance
Every uncertain canonical input used by break-even or Decision Exposure must carry provenance and a declared plausible range.

Allowed V1 sources:
- synthetic fixture
- merchant provided
- policy defined
- deterministic derivation

The model may not silently create canonical financial or probability assumptions.

### Two-baseline ablation
Business-value evaluation compares:
1. Static Policy
2. Myopic Greedy immediate-step optimization
3. ReclaimGrid full-path optimization

All three share identical canonical inputs and hard feasibility constraints.

### Multi-factor uncertainty fail-safe
One-dimensional sensitivity remains the V1 method.

If multiple unresolved material uncertain variables can each change the winning path:
- do not claim ROBUST,
- mark multi-factor uncertainty,
- default to HUMAN REVIEW unless an explicit bounded rule resolves the case.

This avoids false precision without adding multidimensional stochastic optimization.
