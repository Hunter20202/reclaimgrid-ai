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
`V(s) = max over eligible actions a of EV(s,a)`

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

# 8. OPEN-BOX RETURN CASE

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

# 9. INVENTORY TIME DECAY

Returned inventory can lose recoverable value with delay.

Simple optional V1 model:

`AdjustedResaleValue = BaseResaleValue × (1 - decay_rate × days_waited)`

with floor at zero.

Alternative:
Use explicit synthetic markdown tiers rather than continuous decay.

V1 choice should prioritize explainability.

No learned demand forecast is required.

---

# 10. BASELINE FAIRNESS

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

# 11. OPPORTUNITY COST

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

# 12. POLICY CONSTRAINTS

The optimizer is not allowed to maximize over impossible or forbidden paths.

Examples:
- no more reattempts after limit
- damaged item cannot be sold as new
- certain products cannot be refurbished
- liquidate route unavailable in a region
- action missing required data is blocked

Mathematically:
`EligibleActions(s) ⊆ AllActions(s)`

Optimization only occurs over `EligibleActions(s)`.

---

# 13. MISSING DATA

Never convert missing into zero silently.

If a mandatory value is missing:
- block affected path,
- explain missing field,
- allow other fully specified paths if safe,
- or require human input.

AI may identify that a field is missing; AI may not invent it.

---

# 14. PROBABILITY SOURCE DISCIPLINE

For the synthetic hackathon demo, probabilities are explicit scenario assumptions.

Label them clearly:
- synthetic assumption
- merchant-provided assumption
- or derived fixture assumption

Do not claim they are empirically trained probabilities.

Future product potential may learn/calibrate them from historical data, but that is outside V1.

---

# 15. PRECISION / ROUNDING

Recommended internal math:
- decimal currency representation or integer cents
- avoid binary floating-point equality for money
- round only at presentation boundaries when possible

Tie rule:
- define deterministic epsilon or exact cents comparison
- if economically equal within chosen tolerance, prefer the lower-risk / lower-cost action only if that rule is explicit

Exact implementation rule freezes in G3.

---

# 16. REQUIRED HAND-CALCULATED FIXTURES

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

# 17. VISUAL OUTPUT CONTRACT

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
- Baseline decision + EFRC
- Opportunity cost avoided
- Human approval

---

# 18. WHY THIS IS JUDGE-STRONG

Application of Technology:
- AMD extracts meaningful unstructured evidence used by the decision system.

Business Value:
- economics is directly quantified.

Originality:
- multi-stage path value + explicit break-even robustness.

Presentation:
- graph + winner + threshold creates a visual "aha" moment.

Trust:
- no black-box AI financial authority.

---

# 19. RESEARCH BASIS

Recent reverse-logistics decision-support work explicitly uses simulation, multi-criteria ranking, and sensitivity analysis to test strategy robustness under operational uncertainty:
https://doi.org/10.1108/BPMJ-01-2026-0150

Industry validation for highest-value reverse-logistics decisioning:
https://www.mckinsey.com/industries/logistics/our-insights/from-cost-center-to-competitive-advantage-modernizing-reverse-logistics-with-ai

This document does not claim these mathematical ideas are novel by themselves. ReclaimGrid's hackathon product value comes from combining them into a transparent post-purchase Recovery Decision Graph with evidence-grounded AMD AI.

## NEXT SAFE ACTION
Design the synthetic fixture blueprint and hero-case numbers so every important equation, robustness state, and judge claim can be proven before implementation.
