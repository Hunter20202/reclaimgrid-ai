# RECLAIMGRID AI — DECISION HINGE & NEXT BEST EVIDENCE

## CONTROL
- PROJECT: ReclaimGrid AI
- CONTROL CODE: RG-ACT3
- FILE: 14_DECISION_HINGE_AND_NEXT_BEST_EVIDENCE.md
- DESIGN DATE: 2026-10-06
- STATUS: PRE-KICKOFF PRODUCT HARDENING / NOT IMPLEMENTED
- PURPOSE: Extend the existing robustness layer so ReclaimGrid not only says when a decision is fragile, but also identifies what evidence matters before the operator commits.

## WHY THIS EXISTS
A fragile decision is not merely "low confidence."

If two recovery paths switch order at a known threshold, the practical question is:

> What uncertain input is causing the decision to hinge, and what should the operator verify next?

This converts sensitivity analysis into an operational action.

## RESEARCH BASIS
Reverse-logistics research has long studied the **value of information** under uncertainty. The core insight is that information has operational value when reducing uncertainty can change or improve a decision.

Reference:
https://repub.eur.nl/pub/1447/

Recent 2026 reverse-logistics decision-support research also uses explicit sensitivity analysis to test whether a preferred strategy remains robust as failure rates change.

Reference:
https://doi.org/10.1108/BPMJ-01-2026-0150

ReclaimGrid's V1 does NOT need a complex probabilistic EVPI/EVSI model. It can create a judge-useful lightweight version from the break-even engine already required.

# 1. DECISION HINGE

For a fragile case, define:

- **Current Winner**
- **Runner-up**
- **Hinge Variable**
- **Current Assumption**
- **Plausible Range**
- **Break-even Threshold**
- **Direction of flip**

Example:

Current winner:
RETRY

Hinge variable:
Redelivery success probability

Current assumption:
68%

Plausible range:
45%–80%

Break-even:
55.6%

Meaning:
- above 55.6% -> RETRY wins
- below 55.6% -> STOP_AND_RTO wins

This is the Decision Hinge.

# 2. HINGE DISTANCE

A simple judge-readable measure:

For a probability:
`HingeDistance = |current_probability - break_even_probability|`

Example:
`|0.68 - 0.556| = 0.124`
= 12.4 percentage points.

Do not turn this into a universal "confidence score."

It is simply the distance from the current assumption to the decision flip.

# 3. HINGE EXPOSURE / MAXIMUM REGRET

Optional but low-cost and useful.

Across the explicit plausible interval for the hinge variable, calculate:

`Regret(x, chosen) = BestEV(x) - EV(chosen, x)`

Then:

`HingeExposure = max(Regret(x, base_winner))`

For a one-dimensional linear hero comparison, checking the relevant interval endpoints plus the break-even point is usually sufficient for the bounded V1 case.

Interpretation:
"If we commit to the current base-case winner and reality is at the unfavorable end of the plausible interval, what is the maximum expected value we could leave on the table?"

Use plain wording in UI:
- "Potential decision exposure: $X under stated scenario range."

Do not call this guaranteed loss.

# 4. NEXT BEST EVIDENCE

When a decision is FRAGILE, ReclaimGrid should produce one bounded recommendation for what to verify before committing.

The source of this recommendation is mostly deterministic:

## Hinge variable -> evidence type

### Redelivery success probability
Possible next evidence:
- customer availability confirmation
- corrected address confirmation
- delivery-window confirmation
- COD readiness if applicable

### Item condition
Possible next evidence:
- human grading
- additional photo
- packaging condition
- functional check

### Resale value
Possible next evidence:
- current marketplace quote
- internal recent resale price
- markdown rule

### Refurbishment cost
Possible next evidence:
- repair quote
- technician grade

### Inventory time-decay assumption
Possible next evidence:
- campaign/season deadline
- current markdown schedule

The deterministic system selects the hinge variable.
The AMD AI may draft the operational message used to collect that evidence.

# 5. AI BOUNDARY

AMD AI may:
- explain the Decision Hinge,
- draft a customer/warehouse question,
- summarize why the evidence matters,
- parse the response when it arrives.

AMD AI may NOT:
- invent the break-even threshold,
- invent the plausible range,
- invent canonical financial values,
- decide that an unverified answer is true.

# 6. HERO CASE EXAMPLE

For RG-001:

- base winner: RETRY
- break-even p: 55.6%
- plausible p range: 45%–80%
- decision: FRAGILE

Next Best Evidence:
**Confirm the customer can receive tomorrow at the corrected/confirmed delivery window.**

AMD draft:
A short customer message requesting availability confirmation.

If the evidence supports a merchant-defined updated probability above the threshold, the deterministic engine keeps RETRY.
If the confirmed evidence changes the assumption below the threshold, the engine flips to STOP_AND_RTO.

For hackathon V1, the updated probability can be a synthetic human-entered scenario value. The LLM must not derive an authoritative probability from prose.

# 7. REVIEW-ADVISED RULE

Do not invent a black-box confidence threshold.

Recommended explicit deterministic rule:

`REVIEW_ADVISED = decision_is_fragile AND HingeExposure >= merchant_materiality_threshold`

Where:
- `merchant_materiality_threshold` is a visible synthetic setting, e.g. $10 for demo.

If fragile but exposure is tiny:
- show fragile,
- but no special escalation is necessary.

If fragile and exposure is material:
- show REVIEW ADVISED,
- show Next Best Evidence.

This is transparent and explainable.

# 8. WHY THIS STRENGTHENS THE PRODUCT

## Versus AI confidence
"82% confidence" is hard to audit.

Decision Hinge says:
"the recommendation flips at 55.6%."

## Versus static rules
A static rule says retry or return.

Decision Hinge says:
"retry is best only under these conditions."

## Versus pure economics
Pure economics identifies a winner.

Next Best Evidence tells the operator how to reduce uncertainty before acting.

# 9. JUDGE EXPERIENCE

Recommended card:

### Decision Hinge
- Winner: RETRY
- Runner-up: STOP & RTO
- Value gap: $11.20
- Hinge: redelivery success probability
- Current: 68%
- Break-even: 55.6%
- Plausible range: 45–80%
- Status: FRAGILE
- Potential exposure: $X
- Next best evidence: Confirm customer availability

CTA:
**Request confirmation**

In V1 this CTA opens/shows an AMD-drafted message only. It does not send a real message.

# 10. SCOPE CONTROL

Mandatory for V1:
- show hinge variable and break-even threshold for hero fragile case,
- show Next Best Evidence for that case.

Should-have:
- generic mapping for 2–3 hinge variable types.

Stretch:
- formal Expected Value of Sample Information,
- Bayesian updating,
- learned probability calibration.

Do NOT implement those stretch methods during the hackathon unless every core gate is already stable.

# 11. TESTS

Mandatory future tests:
- robust case -> no unnecessary evidence request
- fragile case -> correct hinge variable
- threshold exactly inside range -> FRAGILE
- threshold outside range -> ROBUST
- materiality below threshold -> no REVIEW ADVISED
- materiality above threshold -> REVIEW ADVISED
- AMD message draft cannot alter economics
- missing hinge evidence remains unresolved, not guessed

## NEXT SAFE ACTION
Adopt Decision Hinge + Next Best Evidence into the V1 judge story while keeping formal value-of-information optimization out of scope.
