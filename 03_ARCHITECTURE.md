# RECLAIMGRID AI — ARCHITECTURE

## CONTROL
- PROJECT: ReclaimGrid AI
- CONTROL CODE: RG-ACT3
- FILE: 03_ARCHITECTURE.md
- SNAPSHOT DATE: 2026-10-06
- STATUS: PROVISIONAL PRE-KICKOFF ARCHITECTURE FREEZE — RESEARCH UPGRADED
- CURRENT GATE: G0 — Registration & Environment
- IMPLEMENTATION STATUS: NOT STARTED
- PURPOSE: Define the smallest auditable architecture for the Recovery Decision Graph while keeping deterministic economics authoritative and AMD AI bounded.

## ARCHITECTURE PRINCIPLE
ReclaimGrid has three deliberately separated reasoning responsibilities:

1. **AMD-hosted Case Interpreter** converts messy operational text into bounded, evidence-grounded structured signals.
2. **Deterministic Recovery Decision Graph** computes economically valid multi-stage recovery paths and their expected value.
3. **AMD-hosted Decision Explainer** explains the deterministic result without changing it.

Human approval remains the final authority for consequential actions.

## HIGH-LEVEL FLOW

```text
Synthetic Case + Free-text Note
            |
            +------------------------+
            |                        |
            v                        v
Input Validation              AMD Case Interpreter
            |                        |
            |                 bounded signals +
            |                 confidence/evidence
            |                        |
            +------------+-----------+
                         |
                         v
               Human/Schema Validation
                         |
                         v
             Merchant Policy / Eligibility
                         |
                         v
               Recovery Decision Graph
                         |
                         v
          Multi-stage Path Expected Values
                         |
                         v
             Counterfactual Path Ranking
                         |
                         v
          Robustness / Break-even Analysis
                         |
                         v
                Canonical Decision Package
                         |
              +----------+----------+
              |                     |
              v                     v
      AMD Decision Explainer   Decision Ledger
              |                     |
              +----------+----------+
                         |
                         v
                   Human Approval
                         |
                         v
              Demo Recovery Decision
```

## A. DEMO CASE SOURCE
Use local synthetic JSON/CSV fixtures.

Goals:
- reproducibility
- no PII
- transparent assumptions
- reliable baseline comparison
- deterministic testability

No live merchant integration is required for V1.

## B. INPUT VALIDATOR / NORMALIZER
Responsibilities:
- validate numeric values
- normalize enums
- distinguish missing from zero
- bound free-text length
- preserve raw source text for evidence
- reject impossible or malformed inputs

Canonical financial values cannot come from unvalidated model output.

## C. AMD CASE INTERPRETER

### Purpose
Turn messy operational text into a bounded schema that the application can review and use safely.

Candidate output:
- reason_code
- customer_intent
- condition_hint
- urgency_hint
- confidence
- evidence_span
- missing_fields

### Rules
- source text is untrusted data
- unknown stays unknown
- no financial values may be invented
- evidence span must support the extracted signal
- output must pass schema validation
- low-confidence/ambiguous fields may require human confirmation

This is a meaningful AMD workload because it converts unstructured business evidence into structured decision inputs.

## D. MERCHANT POLICY / ELIGIBILITY LAYER
Responsibilities:
- define allowed states/actions
- exclude prohibited actions
- encode small deterministic merchant constraints
- prevent AI from directly enabling a forbidden path

Examples:
- reattempt count limit
- restock blocked for damage state
- liquidation unavailable for certain items
- refurbishment only when repair cost/value conditions are met

## E. RECOVERY DECISION GRAPH

### Concept
A small directed acyclic graph of recovery states and actions.

Candidate states:
- DELIVERY_EXCEPTION
- CUSTOMER_RESPONSE
- RETURN_TO_ORIGIN
- RETURN_RECEIVED
- RECOVERY_INVENTORY
- CLOSED

Exact V1 graph is frozen in G3.

### Why a graph
It allows the engine to include downstream recovery value in today's decision instead of evaluating only the immediate next action.

Example:
Reattempt delivery can lead to:
- successful delivery
- failed reattempt -> RTO -> returned-item recovery

The downstream value must be included in the reattempt path economics.

## F. DETERMINISTIC PATH ECONOMICS ENGINE

### Financial authority
All canonical route/path economics are deterministic.

For a bounded acyclic graph:

`EV(state, action) = immediate_net_contribution + Σ p(outcome) × EV(next_state)`

The exact equation set and probability assumptions are frozen in G3.

### Responsibilities
- compute path values
- apply costs and explicit assumptions
- enforce eligibility
- rank paths
- expose formulas
- return winner and runner-up
- calculate baseline comparison
- remain reproducible

Candidate output:
- case_id
- current_state
- eligible_actions
- excluded_actions + reasons
- path_values
- winning_path
- runner_up_path
- winner_value
- runner_up_value
- value_gap
- assumptions_used
- baseline_path
- baseline_value
- uplift_absolute
- uplift_percent

## G. ROBUSTNESS / BREAK-EVEN ENGINE

### Purpose
Prevent false precision when the winner depends on uncertain assumptions.

For the dominant uncertain variable in the hero case, compute:
- current assumption
- break-even threshold
- winner/runner-up value gap
- ROBUST or FRAGILE label

Examples:
- minimum redelivery-success probability for reattempt to remain best
- minimum resale value for refurbish to beat liquidation

V1 priority:
- one-dimensional sensitivity

Stretch:
- two-variable scenario matrix/heatmap

No large stochastic simulation is required.

## H. CANONICAL DECISION PACKAGE
Before AI explanation, generate a deterministic package containing:
- validated case inputs
- AI-extracted signals that were accepted
- policy results
- eligible/excluded paths
- path calculations
- winner and runner-up
- value gap
- break-even/robustness result
- baseline comparison

This package is the single source of truth for the explanation UI.

## I. AMD DECISION EXPLAINER
The AMD-hosted model receives the canonical decision package and may:
- explain why the winner wins
- explain the tradeoff against runner-up
- explain the break-even threshold
- draft merchant next action
- draft customer message

It may NOT:
- change financial values
- change winner
- alter eligibility
- invent missing assumptions
- execute any action

If the explanation contradicts the canonical package, reject or visibly flag it.

## J. OPTIONAL MULTIMODAL CONDITION SIGNAL
Stretch only if AMD credits/model/runtime are stable.

Flow:
synthetic returned-item image
-> AMD-hosted multimodal model
-> bounded condition hint + evidence
-> human confirmation
-> deterministic engine

This must not become a G2/G4 blocker.

## K. DECISION LEDGER
Persist/display enough evidence to reconstruct a decision:
- source case
- accepted AI extraction
- evidence span/confidence
- policy rules fired
- formulas/assumptions
- path ranking
- break-even result
- AMD explanation status
- human approval/rejection
- timestamps where useful

No enterprise database is required; lightweight in-memory/local/demo persistence is sufficient unless implementation proves otherwise.

## L. HUMAN APPROVAL LAYER
Judge-facing UI should show:
- case summary
- source evidence
- recovery graph
- excluded paths
- path values
- winner/runner-up
- value gap
- break-even threshold
- baseline comparison
- AMD explanation
- explicit approval

For V1, approval records only a demo outcome.

No real refund, payment, courier, customer, or inventory mutation.

## M. OPTIONAL VALUE LEAK MAP
Should-have/stretch after core stability.

Aggregate synthetic cases by cause and show economic leakage, not just counts.

Example:
- address failures -> $X avoidable recovery gap
- open-box damage -> $Y recovery gap

This helps Track 3 judges see business-level insight from case decisions.

## N. AMD AI GATEWAY
One narrow provider interface should isolate model-serving specifics.

Candidate:
- AMD Developer Cloud
- AMD Instinct
- ROCm
- vLLM or SGLang
- open model selected after environment validation

Responsibilities:
- bounded prompts
- structured output
- timeout
- sanitized metadata
- clean error state
- no arbitrary tool execution

The app should remain model-agnostic behind this interface.

## O. AMD PROOF PATH
Minimum judge proof:
1. Real inference on AMD infrastructure.
2. AMD/Instinct/ROCm serving evidence.
3. Case Interpreter output used by the product.
4. Judge-visible evidence span/confidence.
5. Grounded Decision Explainer output.
6. Sanitized model/runtime metadata.
7. Deterministic engine still works when AMD inference is unavailable.

This makes AMD central but not financially authoritative.

## P. FALLBACK BEHAVIOR

### Case Interpreter unavailable
- allow synthetic pre-structured case input
- label AI interpretation unavailable
- deterministic graph remains usable

### Case Interpreter invalid
- reject output
- preserve raw note
- require manual/synthetic structured signal
- do not guess

### Decision Explainer unavailable
- show canonical math/robustness without AI prose

### AI timeout
- bounded timeout
- no uncontrolled retry
- deterministic result remains usable

### No eligible path
- display explicit blocked state
- require review

### AMD credit/GPU unavailable
- no paid resource automatically
- mock/provider stub allowed only for development after kickoff
- mock must never be presented as AMD proof
- G2 cannot PASS without real AMD evidence

## Q. COST CONTAINMENT
- no training/fine-tuning
- no always-on GPU by default
- no background inference
- no agent swarm
- no large batch calls
- minimum proof calls
- start GPU only when needed
- shut down/delete immediately after test
- track runtime/credit burn

## R. SECURITY MINIMUM
Before G6 PASS:
- secrets in environment variables only
- `.env` ignored
- placeholder-only `.env.example`
- strict input/schema validation
- AI output validation
- prompt-injection tests
- output escaping
- dependency audit
- synthetic data only
- no model-controlled shell/database/payment tools
- no secrets in Git history/evidence

## S. PROVISIONAL TECHNOLOGY SHAPE
Candidate minimal implementation:
- one web app
- TypeScript frontend/server
- local synthetic fixtures
- domain modules for graph/economics/robustness
- one AMD inference API boundary
- no database unless necessary
- no auth unless deployment requires it
- simple deployable architecture

Framework choice remains unfrozen until build authorization.

## T. LOGICAL MODULE BOUNDARIES

```text
/data
  synthetic cases
  baseline rules

/domain
  schemas
  policy
  recovery-graph
  economics
  robustness
  decision-package

/ai
  provider interface
  AMD gateway
  case-interpreter contract
  decision-explainer contract
  response schemas

/app
  case input
  graph view
  decision view
  approval flow
  metrics

/evidence
  decision ledger
  AMD proof
  test outputs
```

Conceptual only; not implementation authorization.

## U. FAILURE MODES TO TEST
- malformed numeric input
- unknown enum
- missing assumption
- no eligible path
- graph cycle introduced accidentally
- tie
- zero/negative uplift
- break-even outside valid range
- AI timeout
- AI malformed JSON
- AI evidence span unsupported
- AI invents financial number
- AI contradicts canonical winner
- prompt injection in case note
- AMD endpoint unavailable
- duplicate case ID

## V. ARCHITECTURE ACCEPTANCE TEST
Before implementation, all must be true:
1. Deterministic path economics works with AI off.
2. AI cannot overwrite financial truth.
3. Recovery graph includes downstream outcomes.
4. Winner and runner-up are transparent.
5. Break-even/robustness is reproducible.
6. AMD performs meaningful visible work.
7. Human approval remains in loop.
8. Demo can run on synthetic data.
9. Core flow survives AI failure.
10. GPU cost is tightly bounded.
11. Architecture can be explained in under one minute.
12. Every major component improves judging value.

## W. ARCHITECTURE NON-GOALS
Do not add:
- microservices
- queues
- Kubernetes
- vector database without need
- agent framework
- workflow engine
- production warehouse
- event streaming
- complex auth
- multi-tenant billing
- RL optimizer
- model training

## RESEARCH BASIS
See:
`09_COMPETITIVE_RESEARCH_AND_PRODUCT_UPGRADE.md`

## NEXT SAFE ACTION
Keep implementation blocked until kickoff/rules re-verification. During the wait window, only continue research, formula design, synthetic fixture design, and judge-story hardening.
