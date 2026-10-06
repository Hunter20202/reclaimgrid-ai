# RECLAIMGRID AI — DEEP RESEARCH: DECISION QUALITY, SERVICE GUARDRAILS & BENCHMARK INTEGRITY

## CONTROL
- PROJECT: ReclaimGrid AI
- CONTROL CODE: RG-ACT3
- FILE: 22_DECISION_QUALITY_AND_BENCHMARK_INTEGRITY.md
- RESEARCH DATE: 2026-10-07
- STATUS: PRE-KICKOFF DEEP RESEARCH / NOT IMPLEMENTED
- PURPOSE: Stress-test the economic objective itself, prevent perverse "maximize value at any cost" decisions, and make RecoveryBench credible enough for judges.

## EXECUTIVE FINDING

The current ReclaimGrid architecture is strong, but one important failure mode remains:

> A mathematically optimal recovery path can still be commercially wrong if it violates customer-service commitments, merchant policy, legal/operational constraints, or trust expectations.

Recent reverse-logistics research reinforces that optimizing one economic objective can produce counterintuitive results when risk/service constraints are omitted. SSADS reports a risk-blind comparator that can outperform more careful inspection under a purely economic objective in some benchmark settings. That is a warning, not a feature.

Retail data also shows returns are a customer-experience problem, not only a cost problem:
- 82% of consumers say free returns matter when choosing where to shop,
- 71% say a poor return experience makes them less likely to shop with the retailer again,
- 76% prefer options with instant refund/exchange,
- retailers must balance customer experience against rising operational cost.

Therefore ReclaimGrid should NOT maximize EFRC across every mechanically possible path.

It should maximize EFRC **inside a deterministic Policy & Service Feasibility Envelope**.

---

# 1. NEW DECISION PRINCIPLE

Old simplified principle:

> choose the path with the highest expected recovery value.

Hardened principle:

> **among paths that satisfy merchant policy, customer remedy commitments, operational constraints, and required evidence, choose the path with the highest Expected Future Recovery Contribution.**

Formally:

`FeasibleActions(s) = PolicyAllowed ∩ ServiceAllowed ∩ EvidenceSupported ∩ OperationallyAvailable`

Then:

`V(s) = max_{a ∈ FeasibleActions(s)} EV(s,a)`

This keeps the economic optimizer transparent without creating an opaque multi-objective weighted score.

---

# 2. WHY NOT A GIANT WEIGHTED SCORE

A tempting design would be:

`Score = margin_weight × margin + loyalty_weight × loyalty + service_weight × service + ...`

Reject for V1.

Problems:
- weights become arbitrary,
- loyalty/CLTV values would be synthetic guesses,
- hard policy violations could be hidden by a large financial score,
- judge explanation becomes harder,
- LLM influence risk increases.

V1 should use:

### Hard constraints first
Examples:
- merchant policy
- customer remedy already promised
- maximum reattempt count
- prohibited resale condition
- missing mandatory evidence
- route not operationally available

### Economic optimization second
Among feasible paths:
maximize EFRC.

### Explicit secondary tie-break only if needed
Example:
when EFRC is tied within fixed cents tolerance:
prefer the path with lower delay or lower operational complexity.

Any tie-break must be visible and deterministic.

---

# 3. POLICY & SERVICE FEASIBILITY ENVELOPE

Candidate V1 constraints:

## Merchant policy
- maximum delivery reattempt count
- allowed exchange/refund routes
- condition grade required for relist
- refurbishment allowed/not allowed
- liquidation availability
- product/category restrictions

## Customer remedy / service commitment
- customer has already chosen/accepted a valid remedy
- promised refund/exchange SLA must not be silently violated
- confirmed refusal blocks another forced redelivery
- confirmed delivery window may be required before another attempt
- no downgrade from an already-approved customer remedy

## Evidence sufficiency
- condition-dependent path requires condition evidence
- address-dependent retry requires address status
- ambiguous/conflicting evidence may block automatic action

## Operational availability
- route/provider actually exists in the synthetic scenario
- refurbishment capacity available
- delivery option available
- destination/channel allowed

These are boolean/enum constraints, not AI-generated weights.

---

# 4. CUSTOMER VALUE WITHOUT FAKE CLTV

Do NOT invent:
- lifetime value,
- churn probability,
- loyalty dollar value,
- customer sentiment dollar conversion

unless there is real data.

Instead, V1 should represent customer experience through:
- hard service commitments,
- explicit SLA constraints,
- customer-selected remedy,
- optional non-monetary indicators in the certificate.

Possible certificate line:
**Service constraint preserved: customer-confirmed redelivery window**

This is more honest than claiming:
"this decision saves $34 of future loyalty."

---

# 5. TRACK 3 ADVANTAGE

Official Track 3 values measurable:
- revenue
- margin
- conversion
- retention
- inventory
- service quality

ReclaimGrid's primary measurable metric remains EFRC/opportunity cost.

Service quality enters through explicit feasibility rules rather than invented financial weights.

This creates a strong judge answer:

> "We optimize merchant recovery value, but never by violating a merchant-defined customer remedy or service constraint. Economics chooses only among feasible paths."

---

# 6. RECOVERY DECISION CERTIFICATE — NEW SECTION

Add:

## Feasibility Envelope
Show:
- policy rules checked
- service commitments checked
- evidence requirements checked
- operational availability checked

For each excluded path:
- exclusion reason

Example:

### RELIST AS NEW
EXCLUDED
Reason: condition evidence = AMBIGUOUS

### SECOND REDELIVERY
EXCLUDED
Reason: merchant reattempt limit reached

### REFURBISH
ELIGIBLE

This makes the optimizer's boundaries visible.

---

# 7. ACTION GATE INTERACTION

Action Gate now considers:

1. Evidence Status
2. Feasible-action set
3. ROBUST / FRAGILE
4. Decision Exposure
5. materiality threshold
6. resolvable Next Best Evidence

Examples:

## ACT NOW
- at least one feasible path
- evidence sufficient
- winner robust OR exposure immaterial
- no human-review rule

## ASK FIRST
- required uncertainty/evidence is resolvable by one bounded request
- a materially different decision could result

## HUMAN REVIEW
- policy conflict
- conflicting critical evidence
- no safe feasible path
- customer remedy conflict
- required human exception

This keeps "ask vs act" commercially meaningful.

---

# 8. RECOVERYBENCH INTEGRITY RISK

A benchmark authored after seeing model weaknesses can become a disguised demo script.

To be credible, RecoveryBench must control for:
- prompt overfitting
- fixture leakage
- cherry-picked notes
- repeated tuning on the test set
- inflated "100%" numbers from easy examples

---

# 9. RECOVERYBENCH V2 — DEV / HOLDOUT SPLIT

Case Interpreter set remains 48 synthetic notes, but split:

## DEV SET — 32 notes
Used for:
- prompt development
- schema debugging
- model-selection iteration

Labels visible during development.

## LOCKED HOLDOUT — 16 notes
Used for:
- final comparison
- judge-facing quality score

Rules:
- notes/labels are frozen before final model selection,
- do not tune prompts against individual holdout failures,
- if the prompt/schema changes after holdout scoring, record a new benchmark version and rerun all candidate models.

Adversarial set:
16 separate cases, treated as locked challenge cases after security prompt contract freezes.

---

# 10. BENCHMARK VERSIONING

Each public benchmark report should include:

- RecoveryBench version
- fixture commit SHA
- prompt-contract version
- model
- serving stack
- model temperature / decoding mode if relevant
- run date
- AMD hardware
- code SHA

Example:

RecoveryBench v1.0
Fixture SHA: <commit>
Prompt contract: interpreter-v1
Model: Qwen3-8B
Serving: vLLM / ROCm / MI300X
Code SHA: <commit>

No "mystery benchmark."

---

# 11. EFFICIENCY METRICS

ACT II's automated leaderboard explicitly ranked accuracy with token usage as an efficiency factor.

ACT III does not currently publish the same automated scoring rule, so do NOT assume tokens are an official criterion.

Still, efficiency is useful evidence.

Measure:
- input tokens/case
- output tokens/case
- p50 latency
- p95 latency
- error rate
- throughput
- GPU runtime
- cost/case when derivable

Model selection should prefer the smallest model that clears RecoveryBench.

This aligns with:
- cost containment,
- technical elegance,
- reproducibility,
- judge confidence.

---

# 12. QUALITY CLAIM HIERARCHY

Strongest claims first:

### Tier 1 — Deterministic
- 20/20 economics fixtures PASS
- 12/12 certificate-integrity cases PASS
- 0 financial-authority escapes

### Tier 2 — AI measured
- holdout schema validity
- holdout semantic accuracy
- unknown preservation
- evidence grounding
- adversarial escape count

### Tier 3 — Runtime measured
- AMD hardware
- p50/p95
- throughput
- runtime/cost

### Tier 4 — Synthetic business scenario
- baseline vs ReclaimGrid EFRC
- opportunity cost avoided

Do not reverse this order by leading with a synthetic ROI number before proving system correctness.

---

# 13. JUDGE ATTACK QUESTIONS

## "Why should I trust synthetic economics?"
Answer:
The business uplift is explicitly synthetic, but every formula is deterministic, hand-checked, and frozen. The submission claims scenario value, not real merchant ROI.

## "Why not optimize customer lifetime value too?"
Answer:
We do not have defensible CLTV data. V1 keeps service/customer obligations as explicit constraints rather than inventing loyalty dollars.

## "What if the highest-value action hurts the customer?"
Answer:
It never enters the optimizer if it violates the Policy & Service Feasibility Envelope.

## "Did you tune the benchmark until the model got 100%?"
Answer:
Prompt development uses a DEV set. Final reported quality comes from a versioned locked holdout and adversarial set.

## "Why use a smaller model?"
Answer:
RecoveryBench determines the minimum model required. The objective is reliable evidence extraction on AMD, not model-size theater.

---

# 14. NEW V1 NON-NEGOTIABLES

Add to MUST HAVE:
1. Policy & Service Feasibility Envelope
2. explicit exclusion reasons
3. DEV/HOLDOUT benchmark split
4. benchmark version + SHA
5. no fabricated CLTV/retention dollar conversion
6. no opaque multi-objective weighting
7. efficiency metrics after real AMD inference

---

# 15. RESEARCH BASIS

Retail customer/service pressure:
- NRF 2025 Retail Returns Landscape:
  https://nrf.com/research/2025-retail-returns-landscape
- NRF 2025 returns press release:
  https://nrf.com/media-center/press-releases/consumers-expected-to-return-nearly-850-billion-in-merchandise-in-2025

Key current findings include:
- 82% say free returns influence shopping choice,
- 71% are less likely to shop again after a poor returns experience,
- 76% prefer instant refund/exchange options,
- 64% of merchants say updating returns processes is a near-term priority.

Decision-making under uncertainty:
- 2026 reverse-logistics systematic review:
  https://doi.org/10.1016/j.cie.2026.112241

Semantic/recovery optimization caution:
- SSADS:
  https://arxiv.org/abs/2609.02116

Reverse-logistics strategy sensitivity:
- https://doi.org/10.1108/BPMJ-01-2026-0150

Prior AMD evaluation/efficiency precedent:
- ACT II live dashboard:
  https://lablab.ai/ai-hackathons/amd-developer-hackathon-act-ii/live
- AgeBand:
  https://lablab.ai/ai-hackathons/amd-developer-hackathon-act-ii/kiano/ageband

## NEXT SAFE ACTION

Adopt the Policy & Service Feasibility Envelope into the canonical deterministic architecture and upgrade RecoveryBench to DEV/HOLDOUT versioning before kickoff.