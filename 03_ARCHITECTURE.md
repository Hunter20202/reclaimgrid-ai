# RECLAIMGRID AI — ARCHITECTURE

## CONTROL
- PROJECT: ReclaimGrid AI
- CONTROL CODE: RG-ACT3
- FILE: 03_ARCHITECTURE.md
- SNAPSHOT DATE: 2026-10-07
- STATUS: PROVISIONAL PRE-KICKOFF ARCHITECTURE FREEZE — RESEARCH UPGRADED
- CURRENT GATE: G1 — Rules & Scope Freeze (WAITING FOR KICKOFF)
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
            |                 exact evidence spans
            |                        |
            +------------+-----------+
                         |
                         v
               Human/Schema Validation
                         |
                         v
       Policy & Service Feasibility Envelope
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
        Decision Hinge / Next Best Evidence
                         |
                         v
            Decision Exposure / Action Gate
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
- address_status
- condition_hint
- urgency_hint
- evidence spans by semantic field
- ambiguity_flags
- missing_fields

No model-authored numerical confidence is part of the authoritative contract.

### Rules
- source text is untrusted data
- unknown stays unknown
- no financial values may be invented
- evidence span must support the extracted signal
- output must pass schema validation
- exact evidence spans must exist in the source note
- unresolved contradiction becomes AMBIGUOUS
- required missing information becomes INCOMPLETE
- contract failure becomes INVALID and is discarded

This is a meaningful AMD workload because it converts unstructured business evidence into structured decision inputs.

## D. EVIDENCE VALIDATOR / STATUS
Application-side logic validates every accepted semantic field.

Deterministic states:
- GROUNDED
- AMBIGUOUS
- INCOMPLETE
- INVALID

Checks:
- allowed enum
- exact source-span containment
- semantic support
- contradiction flags
- missing required fields
- no financial-authority fields

INVALID AI output is discarded.
AMBIGUOUS / INCOMPLETE states feed the deterministic Action Gate.

See `20_AI_EVIDENCE_QUALITY_CONTRACT.md`.

## E. POLICY & SERVICE FEASIBILITY ENVELOPE
Responsibilities:
- define allowed states/actions,
- enforce merchant policy,
- preserve approved customer remedy / service commitments,
- require decision-relevant evidence,
- require operational route availability,
- exclude prohibited or unsupported actions,
- prevent AI from directly enabling a forbidden path.

Formally:
`FeasibleActions = PolicyAllowed ∩ ServiceAllowed ∩ EvidenceSupported ∩ OperationallyAvailable`

Examples:
- reattempt count limit,
- confirmed refusal blocks forced redelivery,
- promised refund/exchange SLA cannot be silently violated,
- restock blocked for incompatible damage state,
- condition-dependent route blocked when condition evidence is AMBIGUOUS/INCOMPLETE,
- liquidation unavailable when no channel exists,
- refurbishment requires route availability and required evidence.

V1 does not monetize speculative CLTV/loyalty or use an opaque weighted multi-objective score.
Economics optimizes EFRC only after hard feasibility filtering.

## F. RECOVERY DECISION GRAPH

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

## G. DETERMINISTIC PATH ECONOMICS ENGINE

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

## H. ROBUSTNESS / BREAK-EVEN ENGINE

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

## I. DECISION HINGE / NEXT BEST EVIDENCE

For FRAGILE cases, the deterministic layer derives:
- hinge variable,
- current assumption,
- break-even threshold,
- plausible interval,
- hinge distance,
- optional bounded Hinge Exposure,
- evidence type most likely to reduce the relevant uncertainty.

The AMD model may draft the operational question/message used to collect that evidence, but it may not calculate or alter the canonical threshold.

This layer must reuse existing robustness math rather than create a separate learned model.

See:
`14_DECISION_HINGE_AND_NEXT_BEST_EVIDENCE.md`

## J. DECISION EXPOSURE / ACTION GATE

For the hero one-dimensional uncertainty case:

- compute the maximum regret of the base-case winner across the declared plausible interval,
- expose that value as Decision Exposure,
- compare it to a visible synthetic merchant materiality threshold,
- derive one deterministic action mode:
  - ACT NOW
  - ASK FIRST
  - HUMAN REVIEW

The Action Gate must remain application logic, not model judgment.

AMD may draft an ASK FIRST message only after the deterministic gate selects that mode.

See:
`16_FRONTIER_RED_TEAM_AND_DECISION_CERTIFICATE.md`

## K. RECOVERY DECISION CERTIFICATE

Assemble one judge-facing artifact from canonical data:
- source/accepted evidence,
- policy/eligibility,
- full path values,
- winner/runner-up/value gap,
- hinge/break-even,
- robustness,
- Decision Exposure,
- Action Gate,
- Next Best Evidence,
- grounded AMD explanation/draft,
- human approval,
- baseline comparison.

The certificate is a presentation/audit object, not an alternate decision engine.

## L. CANONICAL DECISION PACKAGE
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

## M. AMD DECISION EXPLAINER
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

## N. OPTIONAL MULTIMODAL CONDITION SIGNAL
Stretch only if AMD credits/model/runtime are stable.

Flow:
synthetic returned-item image
-> AMD-hosted multimodal model
-> bounded condition hint + evidence
-> human confirmation
-> deterministic engine

This must not become a G2/G4 blocker.

## O. DECISION LEDGER
Persist/display enough evidence to reconstruct a decision:
- source case
- accepted AI extraction
- exact evidence spans + deterministic Evidence Status
- policy rules fired
- formulas/assumptions
- path ranking
- break-even result
- AMD explanation status
- human approval/rejection
- timestamps where useful

No enterprise database is required; lightweight in-memory/local/demo persistence is sufficient unless implementation proves otherwise.

## P. HUMAN APPROVAL LAYER
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

## Q. OPTIONAL VALUE LEAK MAP
Should-have/stretch after core stability.

Aggregate synthetic cases by cause and show economic leakage, not just counts.

Example:
- address failures -> $X avoidable recovery gap
- open-box damage -> $Y recovery gap

This helps Track 3 judges see business-level insight from case decisions.

## R. AMD AI GATEWAY
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

## S. AMD PROOF PATH
Minimum judge proof:
1. Real inference on AMD infrastructure.
2. AMD/Instinct/ROCm serving evidence.
3. Case Interpreter output used by the product.
4. Judge-visible exact evidence spans + deterministic Evidence Status.
5. Grounded Decision Explainer output.
6. Sanitized model/runtime metadata.
7. Deterministic engine still works when AMD inference is unavailable.

This makes AMD central but not financially authoritative.

## T. FALLBACK BEHAVIOR

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

## U. COST CONTAINMENT
- no training/fine-tuning
- no always-on GPU by default
- no background inference
- no agent swarm
- no large batch calls
- minimum proof calls
- start GPU only when needed
- shut down/delete immediately after test
- track runtime/credit burn

## V. SECURITY MINIMUM
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

## W. PROVISIONAL TECHNOLOGY SHAPE
Pre-kickoff technical feasibility research now freezes the default V1 build shape, subject only to G1 rule changes or a verified implementation blocker:

- Node.js 22.12+
- Vite + React + TypeScript
- strict TypeScript
- Zod 4
- @xyflow/react as a read-only graph renderer
- Vitest
- Playwright
- Netlify static deploy + TypeScript Netlify Functions
- one same-origin server-side AMD AI proxy
- local synthetic fixtures
- no database
- no auth
- no ORM
- no vector database
- no queue
- no agent framework

The browser must never call the AMD endpoint directly or receive AMD credentials.

The public AI function accepts only a bounded case/task contract, not arbitrary prompts/model names/token limits.

See:
- `23_TECHNICAL_FEASIBILITY_AND_BUILD_BLUEPRINT.md`
- `24_IMPLEMENTATION_SEQUENCE_AND_RISK_REGISTER.md`

## X. LOGICAL MODULE BOUNDARIES

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
  decision-hinge
  decision-exposure
  action-gate
  decision-certificate
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
  RecoveryBench reports
  AMD proof
  test outputs
```

Conceptual only; not implementation authorization.

## Y. FAILURE MODES TO TEST
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
- fragile decision with wrong hinge variable
- Next Best Evidence contradicts hinge variable
- Decision Exposure calculation wrong
- Action Gate mode inconsistent with deterministic rule
- Recovery Decision Certificate disagrees with canonical package
- duplicate case ID

## Z. ARCHITECTURE ACCEPTANCE TEST
Before implementation, all must be true:
1. Deterministic path economics works with AI off.
2. AI cannot overwrite financial truth.
3. Recovery graph includes downstream outcomes.
4. Winner and runner-up are transparent.
5. Break-even/robustness is reproducible.
6. Fragile hero decisions expose a deterministic Decision Hinge and bounded Next Best Evidence.
7. Decision Exposure and Action Gate are reproducible.
8. Recovery Decision Certificate is fully reconstructable from canonical data.
9. AMD performs meaningful visible work.
10. Human approval remains in loop.
11. Demo can run on synthetic data.
12. Core flow survives AI failure.
13. GPU cost is tightly bounded.
14. Architecture can be explained in under one minute.
15. Every major component improves judging value.

## AA. ARCHITECTURE NON-GOALS
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

## PROOF / EVALUATION SURFACE
Final app should expose a compact Proof surface backed only by measured data:
- RecoveryBench version / fixture SHA / prompt-contract version
- DEV vs locked HOLDOUT result separation
- deterministic fixture pass count
- adversarial authority escapes
- AMD GPU / ROCm / serving stack / model
- p50 / p95 inference latency
- throughput if measured
- sanitized runtime/cost evidence
- last audited commit SHA

No placeholder performance metric may appear in final submission.

See `19_RECOVERYBENCH_EVAL_PLAN.md`.

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
- `22_DECISION_QUALITY_AND_BENCHMARK_INTEGRITY.md`

## NEXT SAFE ACTION
Keep implementation blocked until kickoff/rules re-verification. During the wait window, only continue research, formula design, synthetic fixture design, and judge-story hardening.
