# RECLAIMGRID AI — TECHNICAL FEASIBILITY & EXACT BUILD BLUEPRINT

## CONTROL
- PROJECT: ReclaimGrid AI
- CONTROL CODE: RG-ACT3
- FILE: 23_TECHNICAL_FEASIBILITY_AND_BUILD_BLUEPRINT.md
- DATE: 2026-10-07
- STATUS: PRE-KICKOFF BUILD BLUEPRINT / NOT IMPLEMENTED
- PURPOSE: Freeze the lowest-risk technical shape so implementation can start immediately after G1 without re-architecting the product.

## EXECUTIVE DECISION

Recommended V1 stack:

- Node.js 22.12+ LTS-compatible toolchain
- Vite + React + TypeScript
- strict TypeScript
- Zod 4 for runtime schemas
- React Flow (`@xyflow/react`) for the read-only Recovery Decision Graph
- Vitest for domain/unit/RecoveryBench tests
- Playwright for end-to-end judge-path smoke tests
- Netlify static deploy + TypeScript Netlify Functions
- vLLM OpenAI-compatible AMD endpoint behind a same-origin serverless proxy
- no database
- no auth
- no ORM
- no queue
- no vector database
- no agent framework
- no client-side secret
- no direct browser-to-AMD endpoint

This shape is intentionally boring.

The product's originality must live in:
- recovery economics,
- feasibility envelope,
- uncertainty logic,
- Decision Certificate,
- RecoveryBench proof,

not in infrastructure.

---

# 1. WHY VITE + REACT, NOT A HEAVY META-FRAMEWORK

Current Vite supports React + TypeScript templates and requires Node 20.19+ or 22.12+.
Vitest currently requires Node 22.12+.
Playwright supports current Node 22.x.

Therefore freeze:
**Node 22.12+**

Vite gives:
- very fast local startup,
- simple static production output,
- TypeScript/React support,
- low framework risk.

ReclaimGrid does not need:
- SSR,
- server components,
- database rendering,
- complex routing,
- authentication middleware.

So a full SSR/meta-framework creates more moving parts than judge value.

Sources:
- https://vite.dev/guide/
- https://vitest.dev/guide/
- https://playwright.dev/docs/intro

---

# 2. DEPLOYMENT SHAPE

## Browser
Static React/Vite application.

Responsibilities:
- load synthetic fixture
- render source evidence
- render graph
- render deterministic calculations
- render Decision Certificate
- render Proof surface
- invoke same-origin AI proxy
- never receive AMD credentials

## Netlify Function
One narrow server-side AI gateway.

Responsibilities:
- validate request schema
- enforce case/action allowlist
- load canonical server-side fixture payload
- call AMD-hosted vLLM endpoint
- enforce max tokens / timeout / model
- validate response
- return bounded result + sanitized telemetry

## AMD
vLLM OpenAI-compatible server on approved AMD infrastructure.

Responsibilities:
- Case Interpreter
- grounded Decision Explainer

No financial calculation runs in the model.

---

# 3. WHY NETLIFY FUNCTIONS

Netlify's current Vite integration supports:
- static Vite deploys,
- TypeScript serverless functions,
- environment variables,
- local emulation,
- version-controlled deployment.

Current synchronous function limit is 60 seconds.

Therefore:
- ReclaimGrid AI calls must have an application timeout well below that limit,
- recommended hard timeout: **25 seconds**,
- no background function for judge-path inference.

If real AMD inference cannot reliably complete below the bounded synchronous timeout:
- reduce model/output length,
- use a smaller model,
- or change the serving path after measured evidence.

Do not hide an unreliable 60+ second inference behind asynchronous complexity.

Sources:
- https://docs.netlify.com/build/frameworks/framework-setup-guides/vite/
- https://docs.netlify.com/build/functions/configuration/

---

# 4. PUBLIC GPU-COST ABUSE CONTROL

A public AI proxy can burn credits.

Therefore final public AI route should NOT accept arbitrary prompts.

Recommended request:

```ts
{
  caseId: "RG-001",
  task: "interpret" | "explain"
}
```

Server-side function:
1. validates `caseId`,
2. loads the frozen synthetic case/decision package,
3. builds the prompt itself,
4. chooses the fixed server-side model,
5. sets bounded generation limits,
6. calls AMD.

The client may not send:
- arbitrary system prompt,
- model name,
- max tokens,
- endpoint URL,
- API key,
- canonical financial values.

This prevents:
- prompt abuse,
- token abuse,
- model switching,
- financial tampering.

## Rate limiting
Netlify currently supports rate limiting in function code on all plans.

Initial safe production rule:
- 4 AI requests / 60 seconds / IP+domain

Exact value may be adjusted only after measured demo behavior.

Source:
https://docs.netlify.com/manage/security/secure-access-to-sites/rate-limiting/

## Kill switch
Environment variable:
`AMD_LIVE_ENABLED=false`

When false:
- no AMD request is sent,
- UI shows live inference unavailable,
- verified recorded evidence remains visible in Proof surface,
- deterministic core remains fully functional.

---

# 5. AI GATEWAY ENVIRONMENT VARIABLES

Server-side only:

- `AMD_LIVE_ENABLED`
- `AMD_BASE_URL`
- `AMD_API_KEY` if the approved endpoint requires one
- `AMD_MODEL`
- `AMD_REQUEST_TIMEOUT_MS`

Rules:
- never prefix with `VITE_`
- never expose via frontend bundle
- never log secrets
- never return endpoint/auth metadata to browser

Allowed sanitized telemetry:
- model label
- AMD GPU label
- ROCm version
- serving-stack version
- latency
- token usage if available

---

# 6. vLLM CONTRACT

vLLM currently supports structured JSON outputs through its OpenAI-compatible server.

For Qwen3-family reasoning behavior, vLLM supports disabling thinking through chat-template kwargs.

Case Interpreter default:
- non-thinking
- structured JSON
- temperature 0 or deterministic-compatible low setting
- bounded output
- no tools

Decision Explainer default:
- non-thinking first
- bounded short prose
- no tools
- supplied canonical values only

Do not use model reasoning text as product evidence.

Sources:
- https://docs.vllm.ai/en/latest/features/reasoning_outputs/
- https://docs.vllm.ai/en/v0.31.0/features/structured_outputs/
- https://docs.vllm.ai/en/latest/cli/serve/

---

# 7. AMD MODEL DECISION

Do NOT freeze a final model pre-runtime.

Current AMD documentation shows strong vLLM support for Qwen models on Instinct hardware, including optimized one-GPU Qwen3-32B profiles on MI300X and newer Qwen-family support.

Model rule remains:
**smallest candidate that clears locked RecoveryBench thresholds.**

Practical runtime ladder:
1. lowest-risk compatible candidate
2. RecoveryBench DEV
3. if quality fails materially -> next stronger compatible candidate
4. locked HOLDOUT
5. freeze model

Do not burn credits benchmarking many models for curiosity.

Sources:
- https://enterprise-ai.docs.amd.com/en/latest/aims/docs-aim/instinct/Qwen/Qwen3-32B/README.html
- https://www.amd.com/en/developer/resources/technical-articles/2026/day-0-support-for-qwen-3-8-on-amd-instinct-gpus.html

---

# 8. FRONTEND GRAPH

Use `@xyflow/react` only as a visual renderer.

V1 graph should be:
- read-only,
- non-editable,
- fixed small node set,
- hardcoded deterministic positions or simple layout,
- no drag-to-edit graph semantics,
- no graph persistence.

Useful built-ins:
- `ReactFlow`
- `Controls`
- optional `MiniMap`
- custom nodes
- labeled edges

Do NOT add:
- Dagre/ELK unless layout becomes a real blocker,
- graph editor,
- user-created nodes,
- arbitrary graph mutation.

React Flow is actively maintained and provides built-in controls/minimap/custom nodes.

Sources:
- https://reactflow.dev/learn
- https://reactflow.dev/learn/concepts/built-in-components

---

# 9. FINANCIAL MATH IMPLEMENTATION

Do not use raw floating-point arithmetic scattered across components.

Recommended:
- canonical money inputs as decimal strings,
- one domain-level decimal arithmetic dependency OR one single fixed-point helper,
- all calculations centralized in `domain/economics`,
- round only at explicit presentation boundary,
- compare with explicit deterministic rules.

Preferred implementation for hackathon reliability:
**one decimal arithmetic library behind a tiny adapter**.

Reason:
- expected-value recursion,
- probability multiplication,
- break-even algebra,
- currency display,
- easier hand-fixture parity.

Do not let UI components calculate money.

Alternative integer/fixed-point implementation is acceptable only if it stays simpler than the decimal adapter.

---

# 10. RUNTIME SCHEMA VALIDATION

Use Zod 4.

Why:
- TypeScript-first
- runtime validation
- JSON Schema conversion support
- zero external dependencies inside Zod itself
- strict TypeScript compatible

Validate:
- fixture input
- merchant constraints
- model structured output
- AI proxy request/response
- certificate payload
- RecoveryBench result files

Source:
https://zod.dev/

---

# 11. EXACT MODULE TREE

Recommended:

```text
/
  src/
    app/
      App.tsx
      state.ts

    data/
      cases.ts
      policies.ts
      baselines.ts

    domain/
      schemas.ts
      feasibility.ts
      recoveryGraph.ts
      economics.ts
      robustness.ts
      decisionExposure.ts
      actionGate.ts
      certificate.ts
      baseline.ts
      types.ts

    ai/
      contracts.ts
      client.ts
      evidenceValidator.ts

    components/
      CaseEvidencePanel.tsx
      RecoveryGraph.tsx
      DecisionSummary.tsx
      DecisionHingeCard.tsx
      FeasibilityPanel.tsx
      DecisionCertificate.tsx
      ProofPanel.tsx

    recoverybench/
      runner.ts
      metrics.ts
      report.ts

    styles/
      app.css

  netlify/
    functions/
      ai.mts

  tests/
    unit/
      feasibility.test.ts
      economics.test.ts
      robustness.test.ts
      exposure.test.ts
      actionGate.test.ts
      certificate.test.ts
      evidenceValidator.test.ts

    fixtures/
      economics/
      interpreter-dev/
      interpreter-holdout/
      adversarial/
      certificates/

    e2e/
      hero.spec.ts
      fallback.spec.ts
      proof.spec.ts

  scripts/
    recoverybench.mts
    verify-evidence.mts

  evidence/
    README.md
    amd/
    recoverybench/
    screenshots/

  .env.example
  .gitignore
  netlify.toml
  package.json
  tsconfig.json
  vite.config.ts
```

No `src/server` framework layer.
No database folder.
No auth folder.

---

# 12. SINGLE-SCREEN JUDGE UX

Desktop-first hero screen:

## Top bar
- ReclaimGrid AI
- synthetic-demo badge
- AMD runtime status
- Proof button

## Left column — Evidence
- raw operational note
- exact AMD evidence spans
- deterministic Evidence Status
- feasibility constraints

## Center — Recovery Decision Graph
- current state
- action nodes
- outcome edges
- excluded path styling

## Right column — Decision Certificate
- winner
- challenger
- EFRC
- value gap
- break-even
- ROBUST / FRAGILE
- Decision Exposure
- Action Gate
- Next Best Evidence
- human approval

## Bottom / drawer — Proof
- RecoveryBench
- deterministic fixture pass
- adversarial result
- AMD hardware/runtime
- p50/p95
- audited SHA

Avoid:
- login
- settings
- sidebar maze
- generic chatbot panel
- dashboard with 20 cards

---

# 13. STATE MANAGEMENT

No Redux/Zustand unless implementation proves necessary.

V1 state can use:
- React state/reducer
- derived pure domain functions

Recommended source of truth:
`selectedCaseId`

Everything else is derived from:
- frozen fixture
- accepted AI evidence
- deterministic domain outputs

This minimizes stale state and debugging.

---

# 14. NO DATABASE

Reasons:
- synthetic fixtures are source data,
- no multi-user persistence required,
- no real transactions,
- no authentication,
- certificate can be regenerated,
- adding a DB creates migrations/secrets/network risk.

Evidence files can be committed as sanitized JSON/Markdown artifacts after tests.

---

# 15. TEST STACK

## Vitest
Use for:
- pure domain logic
- fixtures
- RecoveryBench deterministic layers
- AI validator

Current Vitest integrates directly with Vite.

## Playwright
Use only for high-value E2E:
1. hero case loads
2. graph renders
3. certificate values match
4. fallback state works
5. Proof surface renders
6. no client secret exists

Do not build a giant browser-test suite.

Sources:
- https://vitest.dev/guide/
- https://playwright.dev/docs/running-tests

---

# 16. CI GATE

One GitHub Actions workflow after G1:

```text
npm ci
npm run typecheck
npm run lint
npm run test
npm run build
npx playwright test
```

RecoveryBench deterministic subset should run in CI.

Real AMD inference must NOT run on every commit.

Reason:
- cost
- endpoint availability
- nondeterminism
- credit protection

AMD benchmark runs are explicit/manual evidence events.

---

# 17. LIVE / RECORDED AMD MODES

## DEV_MOCK
Before real AMD proof:
- clearly labeled mock
- deterministic fixture-based response
- never counted as AMD evidence

## LIVE_AMD
During approved GPU runtime:
- real vLLM call
- latency measured
- runtime metadata captured

## VERIFIED_RECORDED
After safe GPU shutdown:
- show previously captured real AMD result + evidence metadata
- clearly labeled recorded proof
- do not imply the current request is live

This prevents leaving an expensive GPU running solely to keep the public site alive.

Submission video must show LIVE_AMD.

---

# 18. FAILURE FALLBACK

If AMD call fails:
- deterministic core stays visible,
- Case Interpreter section = unavailable,
- manually/frozen structured evidence may drive the synthetic demo only if visibly labeled,
- Decision Explainer = unavailable,
- no fake AI result,
- certificate shows provenance.

If Netlify function times out:
- no automatic retry loop,
- one user-visible retry action max,
- GPU-cost guard preserved.

---

# 19. PERFORMANCE BUDGET

Client:
- one hero screen
- small synthetic dataset
- no large media
- no heavy chart library unless essential

AI:
- short note
- bounded schema
- short output
- non-thinking default
- server timeout 25s

Judge target:
- deterministic UI reacts instantly
- AMD call feels like one bounded evidence step, not the whole product

---

# 20. TECHNICAL FEASIBILITY VERDICT

### Deterministic core
LOW RISK

### RecoveryBench
LOW-MEDIUM RISK
Main challenge is disciplined fixture/version control, not computation.

### React graph/certificate UI
LOW RISK

### Netlify deployment
LOW RISK

### AMD vLLM integration
MEDIUM RISK
Depends on credit, endpoint/network, model startup, exact image/runtime.

### Live public AMD availability
MEDIUM-HIGH RISK
Cost/abuse/uptime risks.
Mitigated by rate limit, allowlisted case IDs, kill switch, recorded proof mode.

### Overall
**FEASIBLE within hackathon scope if core remains narrow.**

## NEXT SAFE ACTION
Freeze the implementation sequence, milestone acceptance criteria, risk register, and feature-kill order so kickoff execution requires no architectural decision-making.
