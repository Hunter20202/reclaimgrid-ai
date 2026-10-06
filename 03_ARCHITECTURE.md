# RECLAIMGRID AI — ARCHITECTURE

## CONTROL
- PROJECT: ReclaimGrid AI
- CONTROL CODE: RG-ACT3
- FILE: 03_ARCHITECTURE.md
- SNAPSHOT DATE: 2026-10-06
- STATUS: PROVISIONAL PRE-KICKOFF ARCHITECTURE FREEZE
- CURRENT GATE: G0 — Registration & Environment
- IMPLEMENTATION STATUS: NOT STARTED
- PURPOSE: Define the smallest auditable architecture that separates deterministic recovery economics from AMD-hosted AI assistance.

## ARCHITECTURE PRINCIPLE
ReclaimGrid is a decision-support system with two deliberately separated reasoning layers:

1. **Deterministic recovery economics** decides the financial ranking.
2. **AMD-hosted AI** interprets unstructured context and explains/drafts bounded next actions.

The AI layer must never silently become the source of financial truth.

## HIGH-LEVEL FLOW

```text
Synthetic Case Data
      |
      v
Input Validation / Normalization
      |
      v
Merchant Policy + Route Eligibility
      |
      v
Deterministic Recovery Economics Engine
      |
      v
Recovery Route Ranking
      |
      +----------------------+
      |                      |
      v                      v
Structured Decision      Free-text Context
      |                      |
      +----------+-----------+
                 |
                 v
       AMD-hosted AI Layer
                 |
                 v
 Explanation / Structured Interpretation /
 Merchant Note / Customer Message Draft
                 |
                 v
        Policy & Output Guardrails
                 |
                 v
          Human Approval UI
                 |
                 v
      Suggested Recovery Action
```

## COMPONENTS

### A. Demo Case Source
Purpose:
- provide reproducible synthetic ecommerce recovery cases
- avoid PII and external integration dependencies
- make baseline-vs-ReclaimGrid comparison repeatable

Expected form:
- local JSON/CSV fixture or similarly simple static dataset

No live merchant data is required for V1.

### B. Input Validator / Normalizer
Responsibilities:
- reject malformed numeric fields
- reject impossible values
- normalize case type and condition labels
- enforce allowed enumerations
- distinguish missing from zero
- bound free-text length
- preserve source values for auditability

The validator must run before financial calculations or AI calls.

### C. Merchant Policy / Eligibility Layer
Responsibilities:
- determine which recovery routes are allowed
- encode deterministic merchant constraints
- prevent AI from enabling a prohibited route

Examples:
- redelivery may be blocked after a route-specific limit
- restock may be blocked for certain damage states
- liquidation may be unavailable for specific product classes
- exchange/store credit may require defined eligibility

V1 policies remain intentionally small and explicit.

### D. Deterministic Recovery Economics Engine
This is the financial authority.

Responsibilities:
- compute route-specific expected recovery values
- apply explicit cost assumptions
- apply deterministic route exclusions
- return route math
- rank eligible routes
- expose alternatives
- preserve identical output for identical normalized input + assumptions

Required output shape concept:
- case_id
- eligible_routes
- excluded_routes + reason
- route_values
- ranked_routes
- winning_route
- winning_expected_recovery_value
- assumptions_used
- baseline_route
- baseline_expected_recovery_value
- uplift_absolute
- uplift_percent

Exact schema and equations are frozen in G3, not here.

### E. AMD AI Gateway
Purpose:
Provide one narrow interface between the application and the AMD-hosted model.

Candidate deployment:
- AMD Developer Cloud
- AMD Instinct GPU
- ROCm-compatible serving
- vLLM or SGLang
- open model selected only after environment validation

Responsibilities:
- send bounded prompts
- enforce timeouts
- request structured output when applicable
- record model/server metadata for proof
- return failure states cleanly
- prevent arbitrary application control

The rest of the product should not depend on a specific model vendor API shape.

### F. AI Tasks
Authorized AI tasks:
1. Extract bounded structured meaning from a free-text return/NDR reason.
2. Explain the deterministic ranking in plain language.
3. Summarize route tradeoffs.
4. Draft a merchant-facing next-action note.
5. Draft a customer-facing message.
6. Flag ambiguity / missing data.

Unauthorized AI tasks:
- invent prices/costs
- alter route values
- change deterministic eligibility
- execute refunds/shipments
- write directly to merchant systems
- decide a final consequential action without human approval

### G. Policy / Output Guardrails
Every AI response must pass application-side checks before display/use.

Controls:
- schema validation
- allowed action enum
- maximum text length
- no hidden route mutation
- no financial-number replacement
- reject output that contradicts deterministic winner without explicitly labeling it as commentary
- safe fallback when parse fails

### H. Human Approval Layer
The UI should show:
- case summary
- eligible/excluded routes
- recovery math
- ranked options
- baseline comparison
- AI explanation
- assumptions
- approve / reject / inspect alternative

For V1, "Approve" records a demo decision only.
It must not trigger a real refund, courier action, payment, or inventory mutation.

### I. Evidence / Telemetry Layer
V1 needs lightweight evidence capture, not enterprise observability.

Record enough to prove:
- deterministic result
- baseline result
- AI request status
- AI response status
- AMD serving metadata
- fallback activation if any
- human approval/rejection in demo
- timestamps where useful

Do not log secrets or sensitive credentials.

## TRUST BOUNDARIES

### Trusted deterministic core
Trusted for financial ranking:
- normalized numeric inputs
- explicit policy rules
- explicit route equations
- deterministic ranking code

### Untrusted / bounded AI output
Treat model output as untrusted application input.

Required behavior:
- validate
- constrain
- never directly execute
- never accept model-generated financial values as authoritative
- render explanations separately from canonical calculations

### External infrastructure boundary
AMD Developer Cloud is external compute.
Credentials stay in environment variables or secure runtime configuration.

No:
- API key in source code
- token in commits
- token in screenshots used for judging
- secret in logs

## DATA FLOW OWNERSHIP

### Canonical financial data
Owned by deterministic engine.

### Canonical policy data
Owned by merchant-policy configuration / code.

### Canonical explanatory text
Generated by AI but treated as non-authoritative narrative.

### Canonical final action
Chosen by the human approval step for the V1 demo.

## AMD PROOF PATH

The final judge demo must prove AMD is doing meaningful work, not just appearing in the architecture diagram.

Minimum proof package should include:
1. A working AI inference path hosted on AMD infrastructure.
2. Visible AMD Developer Cloud / AMD Instinct / ROCm-related serving evidence.
3. A case where unstructured text is interpreted or the deterministic result is explained by the AMD-hosted model.
4. Model response displayed inside the product.
5. Repository documentation describing the AMD serving path.
6. Evidence that the deterministic financial ranking still works if the model is unavailable.

Potential evidence artifacts:
- architecture screenshot
- server/runtime metadata
- terminal/service startup evidence with secrets redacted
- demo recording showing a live AMD-backed inference
- captured request/response timing without credentials

Exact proof artifacts are frozen in G2.

## FALLBACK BEHAVIOR

### If AI service is unavailable
The app must:
- keep deterministic route ranking functional
- display a clear "AI explanation unavailable" state
- not block financial decision inspection
- allow human review of deterministic math

### If AI times out
The app must:
- stop waiting after a bounded timeout
- avoid repeated uncontrolled retries
- return fallback state
- preserve deterministic result

### If AI output is invalid
The app must:
- reject malformed output
- not partially trust invalid structured fields
- optionally retry once with a constrained repair prompt if G4 authorizes it
- otherwise fall back safely

### If route inputs are invalid
The app must:
- block calculation
- identify validation errors
- avoid AI calls that would mask bad financial input

### If AMD credits / GPU are unavailable
Before implementation or demo:
- do not create paid infrastructure automatically
- preserve a local/mock interface for UI integration testing
- do not falsely present mock inference as AMD proof
- G2 cannot PASS without real AMD evidence

## COST CONTAINMENT ARCHITECTURE
Because GPU credit is limited:
- no always-on GPU by default
- no large training job
- no fine-tuning in V1
- no background inference
- no AI call for deterministic-only cases unless demo value justifies it
- cache/reuse static demo explanation only during non-proof development when appropriate
- start GPU only when needed and shut it down immediately after verified use
- measure runtime and credit burn during G2

Any design requiring persistent paid infrastructure must be rejected unless explicitly re-authorized.

## SECURITY MINIMUM
Before G6 PASS:
- secrets only in environment variables
- `.env` ignored
- `.env.example` contains placeholders only
- strict request/input validation
- strict AI response validation
- output escaping
- dependency audit
- no real customer PII in demo
- no hidden external write actions
- no model-controlled shell/database/payment actions
- no secrets in Git history

## PROVISIONAL TECHNOLOGY SHAPE
Not final; subject to kickoff and feasibility.

Candidate minimal app:
- single web application
- TypeScript-based frontend/server boundary
- deterministic economics module
- local synthetic dataset
- small API route/server function for AMD inference
- no production database unless evidence shows it is necessary
- no auth unless required by deployment
- simple deployable architecture optimized for judge demo reliability

Framework choice is intentionally not frozen in this file.

## MODULE BOUNDARIES
Suggested logical modules:

```text
/data
  synthetic cases
  baseline rules

/domain
  schemas
  policy
  economics
  ranking

/ai
  provider interface
  AMD gateway
  prompt contracts
  response schemas

/app
  case input
  decision view
  approval flow
  metrics/demo dashboard

/evidence
  AMD proof notes
  demo fixtures
  test outputs
```

These are conceptual boundaries, not authorization to create implementation code pre-kickoff.

## FAILURE MODES TO TEST LATER
- malformed numeric input
- negative/unsupported costs
- no eligible routes
- tie between top routes
- missing free-text note
- ambiguous reason
- AI timeout
- AI malformed JSON
- AI contradicts deterministic math
- AMD endpoint unavailable
- baseline route excluded
- division-by-zero in uplift percentage
- extreme but valid values
- duplicate case IDs

## ARCHITECTURE ACCEPTANCE TEST
Before implementation, architecture must satisfy all:
1. Deterministic financial logic can run without AI.
2. AI cannot overwrite financial truth.
3. AMD powers a meaningful visible workload.
4. Human approval remains in the loop.
5. Demo can run on synthetic data.
6. Core demo survives AI failure.
7. No real external consequential action is required.
8. GPU cost can be tightly controlled.
9. Every major component contributes to judge value.
10. Architecture can be explained in under one minute.

## ARCHITECTURE NON-GOALS
Do not add preemptively:
- microservices
- message queues
- Kubernetes
- vector database
- agent framework
- workflow engine
- production data warehouse
- event streaming
- complex auth
- multi-tenant billing
- full observability stack

A tool is added only when a verified requirement demands it.

## CHANGE CONTROL
This architecture is provisional until G1/G2 feasibility verification.

Architecture changes after freeze must record:
- reason
- impacted gate
- security/cost effect
- demo effect
- decision outcome

in `07_DECISION_LOG.md` once created.

## NEXT SAFE ACTION
Create `04_SECURITY_COST_GUARDRAILS.md` to freeze secret handling, PII rules, AI trust boundaries, GPU/payment controls, dependency safety, logging rules, and stop conditions before any implementation begins.
