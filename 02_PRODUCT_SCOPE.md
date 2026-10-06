# RECLAIMGRID AI — PRODUCT SCOPE

## CONTROL
- PROJECT: ReclaimGrid AI
- CONTROL CODE: RG-ACT3
- FILE: 02_PRODUCT_SCOPE.md
- SNAPSHOT DATE: 2026-10-06
- STATUS: PROVISIONAL V1 SCOPE FREEZE
- CURRENT GATE: G0 — Registration & Environment
- IMPLEMENTATION STATUS: NOT STARTED
- PURPOSE: Freeze the smallest judge-ready V1 scope before kickoff without writing submission implementation code.

## PRODUCT ONE-LINER
ReclaimGrid AI is an AMD-powered post-purchase recovery decision engine that helps ecommerce merchants choose the highest-value recovery action for failed deliveries and returns.

## CORE PROBLEM
Ecommerce merchants lose money after failed deliveries, returns, open-box parcels, damaged returns, and aging returned inventory because the next action is often selected through static rules, fragmented workflows, or manual judgment.

The decision is not simply:
- refund vs redeliver
- keep vs discard
- chatbot vs human

The real problem is:
**Which permitted recovery route produces the best bounded economic outcome for this specific case, under merchant policy and operational constraints?**

## PRIMARY USER
### V1 user
Small-to-mid-size ecommerce operations / post-purchase / returns team.

### User job-to-be-done
Given a failed-delivery or return case, quickly decide what to do next while protecting recoverable value and avoiding an opaque AI-only financial decision.

## V1 CASE TYPES
V1 may accept synthetic examples from:
1. Failed delivery / NDR case
2. Customer return
3. Open-box / damaged returned parcel
4. Aging returned inventory

Not every case type must receive a unique workflow. They can share one normalized decision pipeline.

## V1 INPUTS
The demo should use a bounded, synthetic case schema containing only fields needed for recovery economics.

Candidate input fields:
- case_id
- case_type
- item_value
- product_cost
- shipping_cost
- reverse_shipping_cost
- redelivery_cost
- expected_resale_value
- expected_liquidation_value
- expected_refurbishment_cost
- inventory_age_days
- damage/open-box condition
- customer reason or free-text note
- merchant policy constraints
- route eligibility flags
- selected risk/operational assumptions

Exact schema is frozen later in G3.

## AUTHORIZED RECOVERY ROUTES
V1 should rank a small, explainable set of recovery options.

Candidate routes:
1. Redelivery
2. Exchange / Store Credit
3. Restock / Relist
4. Liquidation
5. Refund / Close Case

A route must be excluded when merchant policy or case state makes it ineligible.

## DETERMINISTIC RECOVERY ECONOMICS ENGINE

### Role
The deterministic engine is the financial authority for V1.

It must:
- calculate bounded recovery value for each eligible route
- apply explicit costs
- apply explicit recovery assumptions
- rank routes
- expose the math
- return the winning route and alternatives
- remain reproducible for the same inputs

### Example decision concept
For each route:

Expected Recovery Value
= Expected Recoverable Revenue
- Incremental Fulfillment / Handling Cost
- Reverse Logistics Cost
- Refurbishment / Discount Cost
- Route-Specific Loss Allowance

The exact formula set is NOT yet frozen and must be finalized in G3.

### Non-negotiable rule
The language model must NOT:
- invent financial inputs
- silently change costs
- become the sole forecaster
- decide hidden financial weights
- override deterministic eligibility rules
- directly execute a consequential merchant action

## AMD AI LAYER

### Meaningful AMD workload
A meaningful AI workload must run on AMD infrastructure/hardware in the final judge demo.

### V1 AI responsibilities
The AMD-hosted model may:
- interpret an unstructured return/NDR reason
- convert free text into bounded structured attributes
- explain why the deterministic engine ranked a route first
- summarize tradeoffs between top routes
- draft a merchant-facing next-action note
- draft a customer-facing message
- surface missing information or uncertainty

### V1 AI boundary
The AMD model is an interpretation/explanation/action-drafting layer, not the source of financial truth.

### Candidate serving direction
Open model served through AMD Developer Cloud using an AMD Instinct GPU with ROCm-compatible serving such as vLLM or SGLang.

Final model choice is intentionally NOT frozen pre-kickoff.

## DECISION PIPELINE
Business / Case Data
-> Input Validation
-> Deterministic Recovery Economics Engine
-> Eligibility Filter
-> Recovery Route Ranking
-> AMD-hosted AI Interpretation / Explanation
-> Policy Guardrails
-> Human Approval
-> Suggested Recovery Action

## HUMAN APPROVAL
V1 is decision support, not unrestricted autonomous execution.

Before any consequential action:
- show recommended route
- show expected recovery value
- show alternatives
- show key assumptions
- show AI explanation
- require explicit human approval

No real refund, payment, shipment, customer account change, inventory mutation, or external merchant action is required for the hackathon V1.

## SYNTHETIC DEMO DATA
Default V1 data source: synthetic ecommerce recovery cases.

Reasons:
- reproducible demo
- no customer PII
- no external merchant integration dependency
- deterministic test coverage
- easier evidence generation
- lower security and operational risk

Synthetic dataset should include:
- clear-win cases
- close-call cases
- invalid/ineligible route cases
- missing-information cases
- at least one free-text reason requiring AMD AI interpretation

## DEMO SUCCESS METRICS
The V1 demo must prove value with measurable before/after or baseline comparison.

Minimum metrics:
1. Total baseline recovered value
2. Total ReclaimGrid recommended recovered value
3. Absolute recovered-value uplift
4. Percentage recovered-value uplift
5. Number / percentage of cases where ReclaimGrid changes the baseline route
6. Explanation trace showing why a route won
7. AMD AI proof for at least one meaningful case

Optional if time permits:
- recovered margin
- avoided loss
- route confidence / uncertainty flag
- processing time per case
- human approval rate in synthetic walkthrough

## BASELINE
V1 needs a simple, defensible comparison baseline.

Candidate baseline:
Static merchant rule set such as:
- failed delivery -> redeliver once
- clean return -> restock
- damaged/open-box -> liquidation
- otherwise -> refund

The exact baseline must be frozen in G3 and applied consistently across the synthetic dataset.

## JUDGE STORY
The judge experience should answer, in order:

1. What money is being lost?
2. Why is the current rule/manual decision weak?
3. What data does this case contain?
4. Which recovery routes are actually eligible?
5. What does the deterministic engine calculate?
6. Which route ranks highest and by how much?
7. What does AMD-hosted AI contribute that deterministic math cannot?
8. What human approves?
9. Across the dataset, how much additional value is recovered?

## V1 MUST-HAVES
A judge-ready V1 must contain:
- synthetic case dataset
- deterministic recovery-economics calculations
- route eligibility logic
- route ranking
- visible math / assumptions
- AMD-hosted AI interpretation or explanation
- policy guardrails
- human approval step
- baseline-vs-ReclaimGrid value comparison
- clean end-to-end demo
- public GitHub repository
- evidence that AMD powers a meaningful AI workload

## V1 SHOULD-HAVES
Only after must-haves are stable:
- scenario comparison
- editable assumptions
- merchant policy presets
- CSV import/export
- concise dashboard
- case audit trail
- downloadable decision evidence

## V1 NON-GOALS
Explicitly OUT OF SCOPE unless later re-authorized:
- full Shopify integration
- full WooCommerce integration
- real courier/NDR integration
- real payment/refund execution
- real inventory mutation
- customer support chatbot
- generic returns management suite
- generic inventory management
- end-to-end warehouse management
- omnichannel ERP
- autonomous multi-agent system
- model training / fine-tuning
- giant forecasting model
- dozens of recovery routes
- production multi-tenant SaaS
- authentication/roles unless absolutely necessary for demo
- large database architecture
- mobile app
- partner-track complexity that does not improve core scoring

## DIFFERENTIATION
ReclaimGrid must NOT present itself as merely:
- an NDR chatbot
- a returns chatbot
- a returns portal
- a generic recommendation engine

Core differentiation:
**Deterministic, economically bounded recovery-route ranking + AMD-hosted AI interpretation/explanation + human-governed action.**

## SAFETY / TRUST REQUIREMENTS
- deterministic financial authority
- transparent route math
- explicit assumptions
- bounded model output
- schema validation
- no secret in repository
- synthetic data by default
- human approval before consequential action
- graceful fallback when AI is unavailable
- no claim that AI guarantees recovered revenue

## SCOPE KILL TEST
Any proposed V1 feature must pass all three:
1. Does it strengthen a judging criterion?
2. Does it improve the end-to-end demo or measurable business value?
3. Can it be built, tested, and explained safely within hackathon time?

If the answer is NO to any one, defer it.

## PROVISIONAL FREEZE RULE
This scope is frozen for pre-kickoff planning.

Changes are allowed only if:
- kickoff rules require them,
- AMD environment constraints require them,
- a critical technical feasibility issue is found, or
- a clearly superior judge-value simplification is verified.

Any scope change must be recorded in 07_DECISION_LOG.md once that file exists.

## EXIT CRITERIA FOR PRODUCT SCOPE
Before implementation begins, G1 must confirm:
- Track 3 remains valid
- official implementation timing permits build
- AMD proof path is feasible
- deterministic engine inputs/routes are bounded
- baseline is defined
- demo metrics are defined
- non-goals remain excluded

## NEXT SAFE ACTION
Create `03_ARCHITECTURE.md` defining the planned components, data flow, trust boundaries, deterministic-vs-AI responsibility split, AMD proof path, and failure/fallback behavior — without writing application code.
