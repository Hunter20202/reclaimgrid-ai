# RECLAIMGRID AI — COMPETITIVE RESEARCH & PRODUCT UPGRADE

## CONTROL
- PROJECT: ReclaimGrid AI
- CONTROL CODE: RG-ACT3
- FILE: 09_COMPETITIVE_RESEARCH_AND_PRODUCT_UPGRADE.md
- RESEARCH DATE: 2026-10-06
- STATUS: PRE-KICKOFF RESEARCH / PRODUCT HARDENING
- PURPOSE: Red-team the ReclaimGrid concept against the 2026 market and strengthen it for AMD Developer Hackathon: ACT III without writing submission implementation code.

## EXECUTIVE CONCLUSION

The original idea remains commercially relevant, but a generic combination of:
- returns/NDR automation,
- AI recommendations,
- return disposition routing,
- confidence/explanations,
- or "highest recovery channel"

is NOT sufficiently differentiated on its own.

The market already contains strong products that automate failed-delivery recovery, returns/exchanges, AI-assisted decisioning, and return disposition. ReclaimGrid must therefore compete on a more specific decision-science layer:

> **ReclaimGrid maps the economically valid recovery paths across a post-purchase failure, calculates their counterfactual expected value, shows whether the winning decision is robust to uncertainty, and uses AMD-hosted AI to turn messy operational evidence into bounded structured signals and explanations.**

The recommended upgraded product core is called the **Recovery Decision Graph**.

---

# 1. WHY THIS PROBLEM IS LARGE

## Retail returns
The National Retail Federation's 2025 Retail Returns Landscape projected:
- $849.9B in total U.S. retail returns in 2025
- 19.3% of online sales returned

Source:
https://nrf.com/research/2025-retail-returns-landscape

## Reverse-logistics cost
McKinsey reported in February 2026 that:
- consumers returned nearly $1T in U.S. merchandise in 2024
- retailers spend an estimated $200B annually recovering value from returned goods
- leading approaches combine product, demand, condition, supply-chain cost, and operational data to route returns toward higher-value outcomes

Source:
https://www.mckinsey.com/industries/logistics/our-insights/from-cost-center-to-competitive-advantage-modernizing-reverse-logistics-with-ai

Conclusion:
The business problem is strong and quantifiable. The challenge is differentiation, not demand justification.

---

# 2. COMPETITOR RED-TEAM

## Loop Returns
Observed 2026 capabilities include:
- AI-powered Background Agents reviewing returns and recommending/taking actions
- reasoning transparency and confidence
- return predictions
- smart exchanges and AI product recommendations
- return insights ranked by dollar impact

Sources:
https://help.loopreturns.com/en/articles/12608193
https://changelog.loopreturns.com/
https://help.loopreturns.com/en/articles/13680897

Implication:
"AI looks at return context and recommends an action with explanation" is already commoditizing.

## Optoro
Observed capabilities include:
- SmartDisposition decision engine
- routing returned inventory to profitable recovery channels
- restock/resale/recommerce optimization
- measurable net-recovery positioning

Sources:
https://www.optoro.com/returns-processing/
https://www.optoro.com/

Implication:
"Choose the highest recovery channel for a returned item" is not unique.

## AfterShip
Observed 2026 capability:
- AI post-purchase agent handles shipment exceptions
- failed-delivery context gathering
- drafts fixes for approval
- redelivery/customer-contact workflows

Source:
https://www.aftership.com/ai

Implication:
"AI for post-purchase shipment exception recovery" is already present.

## ClickPost
Observed capabilities:
- failed-delivery/NDR recovery
- multi-channel outreach
- courier update automation
- AI carrier allocation
- automated returns/exchanges
- RTO-reduction positioning

Sources:
https://www.clickpost.ai/solutions/d2c/electronics-solution
https://www.clickpost.ai/blog/what-is-ndr-rto-in-ecommerce

Implication:
"NDR recovery + returns in one post-purchase platform" is also not enough by itself.

## ReverseLogix
Observed 2026 capabilities include:
- AI/Vision-assisted grading
- fraud/condition evidence
- rules-based disposition
- human review
- restock/open-box/refurbish/resell/recycle routing
- return-value and audit-trail positioning

Sources:
https://www.reverselogix.com/platform/ai/
https://www.reverselogix.com/product/recommerce/

Implication:
"AI evidence + human review + disposition rules + audit trail" is also an established pattern.

---

# 3. GAP WE SHOULD TARGET

Across the reviewed products, the strongest defensible hackathon gap is not simply automation.

The proposed gap is:

## A. Multi-stage recovery economics
Instead of asking only:
"What is the next action?"

ask:
"What is the best economically valid recovery path, including what happens if the first action succeeds or fails?"

Example:
- Reattempt delivery now
  - success -> keep sale
  - failure -> RTO -> inspect -> relist/liquidate
versus
- stop reattempts -> RTO immediately -> restock/relist

This propagates downstream recovery value into today's decision.

## B. Counterfactual path comparison
For every feasible path, compute what would happen under the same canonical case assumptions.

The product should show:
- winning path
- runner-up
- value gap
- excluded paths and why

## C. Decision robustness, not false precision
A single expected-value number can look authoritative while resting on uncertain probabilities.

ReclaimGrid should additionally show:
- break-even threshold
- sensitivity to uncertain inputs
- whether the recommendation is ROBUST or FRAGILE

Example:
"Redelivery remains the best path as long as success probability stays above 43%."

That is much more decision-useful than:
"AI confidence: 82%."

## D. Evidence-grounded AI extraction
AMD-hosted AI should not invent economics.

Its central job should be:
- turn messy carrier/return notes into a bounded schema
- attach confidence
- quote/evidence the text span supporting each extracted signal
- explicitly mark missing/unknown fields

Example output fields:
- reason_code
- customer_intent
- condition_hint
- urgency_hint
- confidence
- evidence_span
- missing_fields

The deterministic engine then decides what those validated signals permit.

## E. Decision ledger
Every recommendation should be explainable after the fact:
- original inputs
- AI-extracted signals
- evidence spans
- policy rules fired
- eligible/excluded paths
- deterministic formulas
- winning path
- sensitivity/break-even
- human approval

This becomes a public judge-facing trust artifact.

---

# 4. UPGRADED CORE — RECOVERY DECISION GRAPH

## Product thesis
ReclaimGrid is an explainable **Recovery Decision Graph** for post-purchase failures.

It models the case as states and allowed transitions rather than one isolated recommendation.

### Example states
- DELIVERY_EXCEPTION
- CUSTOMER_RESPONSE
- RETURN_TO_ORIGIN
- RETURN_RECEIVED
- RECOVERY_INVENTORY
- CLOSED

### Example actions
Depending on state:
- reattempt delivery
- request correction
- redirect/pickup
- return to origin
- exchange/store credit
- refund/close
- restock/relist
- refurbish
- liquidate

Exact V1 state/action set remains intentionally small.

---

# 5. DETERMINISTIC RECOVERY PATH OPTIMIZER

For a small acyclic recovery graph, define:

Expected Value(state, action)
= Immediate Net Contribution
+ Sum over outcomes [
    Probability(outcome) × Expected Value(next_state)
  ]

minus explicit action-specific costs already represented in the path.

The engine must:
- use explicit assumptions only
- respect policy constraints
- preserve identical results for identical inputs
- expose calculations
- never let the LLM replace canonical values

Implementation may use simple backward induction / dynamic programming over a bounded DAG.

No reinforcement learning or model training is required for V1.

---

# 6. ROBUSTNESS / BREAK-EVEN ENGINE

For the top two paths, calculate whether the decision changes when uncertain variables move.

Priority uncertain variables:
- probability of redelivery success
- resale probability
- resale value / markdown
- inventory time decay
- refurbishment success/cost

V1 should avoid a giant stochastic model.

Recommended V1:
- one-dimensional sensitivity for the dominant uncertain parameter per case
- optional two-variable scenario matrix if easy

Outputs:
- ROBUST / FRAGILE
- current assumption
- break-even value
- winner-to-runner-up value gap
- optional worst/base/best scenario

This is a major originality and trust feature.

---

# 7. AMD AI ROLE — UPGRADED

AMD AI must be operationally meaningful.

## Mandatory AI task 1 — Case Interpreter
Input:
- messy NDR / return note

Output:
- bounded structured signals
- confidence
- evidence span
- unknown/missing fields

This directly influences:
- case normalization
- state classification
- route eligibility inputs

But it must NOT create financial values.

## Mandatory AI task 2 — Decision Explainer
Input:
- canonical deterministic decision package

Output:
- concise explanation
- tradeoff summary
- merchant next-action draft
- optional customer message draft

The model receives canonical calculations and is explicitly prohibited from changing them.

## Optional stretch — Multimodal condition signal
If AMD credits/runtime/model support are stable:
- returned-item photo
- AMD-hosted multimodal model
- bounded condition hint + evidence
- human-confirmed before deterministic use

This is STRETCH only because it increases technical and GPU risk.

---

# 8. VALUE LEAK MAP — HIGH-VALUE STRETCH FEATURE

Aggregate synthetic cases by failure cause and quantify economic leakage.

Instead of:
"32 address issues"

show:
"Address-related delivery failures account for $X of avoidable recovery gap in this simulation."

Possible categories:
- address issue
- customer unavailable
- refused delivery
- wrong size/fit
- damaged/open-box
- delayed return processing
- aging inventory

This closes the loop from:
case-level action -> portfolio-level business insight.

This is strongly aligned with Track 3's goal of helping a business understand data and take better action.

Do not build this until the core path optimizer is stable.

---

# 9. WHY THIS FITS THE OFFICIAL ACT III TRACK

Official Track 3 asks for:
- a real customer/merchant problem
- useful commercial action
- relevant recommendation/personalization
- measurable effect on revenue, margin, retention, inventory, or service quality
- non-LLM-only forecasting when predictions are used

Official event page:
https://lablab.ai/ai-hackathons/amd-developer-hackathon-act-iii

ReclaimGrid's upgraded fit:
- merchant problem: post-purchase value leakage
- commercial action: choose recovery path
- measurable metric: expected recovered value / margin
- deterministic calculation: transparent path economics
- AMD AI: bounded evidence extraction and explanation
- human governance: explicit approval

---

# 10. JUDGING-CRITERIA OPTIMIZATION

## Application of Technology
Strongest demo proof:
- AMD-hosted open model
- real inference
- bounded structured extraction from messy operational text
- evidence span + confidence
- application-visible effect on the recovery graph
- second AMD inference for grounded explanation

## Business Value
Strongest proof:
- baseline-vs-ReclaimGrid synthetic evaluation
- aggregate recovered-value uplift
- per-case opportunity-cost gap
- sensitivity/break-even decision

## Originality
Strongest differentiators:
- multi-stage recovery path economics
- counterfactual comparison of allowed paths
- break-even/robustness analysis
- AI evidence grounding rather than AI financial authority

## Presentation
Strongest visual story:
1. messy case arrives
2. AMD AI extracts evidence
3. Recovery Decision Graph appears
4. paths get deterministic values
5. winner + break-even threshold appears
6. human approves
7. portfolio value impact updates

---

# 11. DEMO HERO CASE

Recommended hero case:
**Failed delivery where the obvious next action is not automatically optimal.**

Inputs include:
- item value/margin
- redelivery cost
- RTO cost
- estimated redelivery success probability
- returned-item recovery value if redelivery fails
- free-text carrier/customer note

Demo:
1. AMD AI extracts reason/customer intent from free text.
2. Engine builds eligible recovery paths.
3. Reattempt path includes downstream fallback value if it fails.
4. Immediate-RTO path is calculated under same assumptions.
5. Engine selects winner.
6. Robustness engine shows the break-even success probability.
7. AI explains the math without changing it.
8. Human approves.

Why this hero works:
- shows failed-delivery + return lifecycle in one case
- shows AMD as meaningful
- shows deterministic math
- shows counterfactual reasoning
- shows explainability
- shows business value

---

# 12. SECONDARY CASE

Recommended secondary case:
**Returned open-box item with uncertain resale economics.**

Compare:
- restock/relist
- refurbish then relist
- liquidation
- refund/close as applicable

Show:
- policy exclusion
- value comparison
- resale-value sensitivity
- fragile decision -> human review

This proves the engine is a reusable recovery system, not a one-off NDR calculator.

---

# 13. BASELINE STRATEGY

A weak strawman baseline will reduce credibility.

Recommended baseline:
**Stage-specific deterministic static policy** such as:
- first NDR -> reattempt once
- clean received return -> restock
- damaged/open-box -> liquidate
- otherwise -> refund/close

Then compare:
- same cases
- same canonical costs
- same assumptions

ReclaimGrid improvement comes from:
- downstream path value
- context-sensitive eligibility
- explicit counterfactual comparison

Not from secretly giving ReclaimGrid better inputs.

---

# 14. METRICS TO SHOW

Primary:
- total baseline expected recovered value
- total ReclaimGrid expected recovered value
- absolute uplift
- percentage uplift

Decision-quality:
- cases where route/path changes
- average opportunity-cost avoided
- robust vs fragile recommendations
- number of policy-excluded unsafe/ineligible paths

AMD layer:
- structured extraction validity rate
- AI latency
- fallback count
- evidence-grounded extraction examples

Do not overfit the demo to dozens of vanity metrics.

---

# 15. WHAT NOT TO ADD

Do not weaken the product with:
- generic chatbot
- generic support assistant
- full Shopify integration
- courier integration
- payments/refunds execution
- huge autonomous-agent framework
- model training
- complex reinforcement learning
- vector database without a real need
- many screens
- broad ERP features

The project should feel mathematically strong, visually clear, and intentionally small.

---

# 16. MARKET POSITIONING AFTER RED-TEAM

Old framing:
"AI-powered returns/NDR recovery decision engine."

Too crowded.

Recommended framing:
> **ReclaimGrid is a recovery-path decision system that calculates the economic consequence of every allowed post-purchase recovery path, shows when the winning decision is robust or fragile, and uses AMD-hosted AI to convert messy operational evidence into safe, explainable decisions.**

Short tagline:
> **Find the best recovery path — and prove why it wins.**

Alternative:
> **Recover value with decisions you can audit.**

---

# 17. ORIGINALITY CLAIM DISCIPLINE

Do NOT claim:
- nobody has return disposition software
- nobody uses AI in returns
- nobody optimizes recovery
- first-ever system

Safe claim:
> In the competitors reviewed for this research, AI automation, disposition routing, and failed-delivery recovery are already established. ReclaimGrid therefore differentiates its hackathon implementation around transparent multi-stage counterfactual recovery-path economics, robustness/break-even analysis, and evidence-grounded AMD AI.

This is defensible and honest.

---

# 18. PRIORITY FREEZE

## MUST HAVE
1. Recovery Decision Graph
2. Deterministic multi-stage path expected value
3. Policy/eligibility constraints
4. Winning path + runner-up + value gap
5. Break-even / robustness analysis
6. AMD AI evidence-grounded case extraction
7. AMD AI grounded explanation
8. Human approval
9. baseline-vs-ReclaimGrid synthetic evaluation
10. judge-visible AMD proof

## SHOULD HAVE
- portfolio Value Leak Map
- worst/base/best scenarios
- simple interactive assumption slider

## STRETCH
- AMD multimodal photo condition signal
- two-variable sensitivity heatmap

## EXCLUDE
Everything in the existing V1 non-goal list unless a later gate explicitly re-authorizes it.

---

# 19. RESEARCH SOURCES

Official ACT III:
https://lablab.ai/ai-hackathons/amd-developer-hackathon-act-iii

NRF 2025 Retail Returns Landscape:
https://nrf.com/research/2025-retail-returns-landscape

McKinsey reverse logistics AI:
https://www.mckinsey.com/industries/logistics/our-insights/from-cost-center-to-competitive-advantage-modernizing-reverse-logistics-with-ai

Loop Background Agents:
https://help.loopreturns.com/en/articles/12608193

Loop 2026 releases:
https://changelog.loopreturns.com/

Optoro Returns Processing:
https://www.optoro.com/returns-processing/

AfterShip AI:
https://www.aftership.com/ai

ClickPost failed-delivery recovery:
https://www.clickpost.ai/solutions/d2c/electronics-solution

ReverseLogix AI:
https://www.reverselogix.com/platform/ai/

ReverseLogix recommerce:
https://www.reverselogix.com/product/recommerce/

Recent reverse-logistics decision-support research:
https://doi.org/10.1108/BPMJ-01-2026-0150

## NEXT CONTROL ACTION
Update product scope, architecture, decision log, changelog, and master state to adopt the Recovery Decision Graph + robustness/break-even upgrade while keeping implementation blocked until kickoff/rules re-verification.
