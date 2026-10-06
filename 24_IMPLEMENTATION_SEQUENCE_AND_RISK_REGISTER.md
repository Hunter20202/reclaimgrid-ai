# RECLAIMGRID AI — IMPLEMENTATION SEQUENCE, RISK REGISTER & FEATURE-KILL ORDER

## CONTROL
- PROJECT: ReclaimGrid AI
- CONTROL CODE: RG-ACT3
- FILE: 24_IMPLEMENTATION_SEQUENCE_AND_RISK_REGISTER.md
- DATE: 2026-10-07
- STATUS: PRE-KICKOFF EXECUTION BLUEPRINT / NOT IMPLEMENTED
- PURPOSE: Remove architecture decisions from the live build window and define exact milestone order, acceptance gates, fallback paths, and kill rules.

## OPERATING PRINCIPLE

The user receives one action at a time.
The Control Room may switch lanes when an external dependency is blocked.

Implementation must optimize for:
1. correctness,
2. judge-visible proof,
3. reliable demo,
4. AMD meaningfulness,
5. polish,

in that order.

No feature may jump ahead of a failed core gate.

---

# 1. BUILD LANE OVERVIEW

After G1 PASS:

## Lane B — deterministic product core
Starts immediately.

## Lane A — AMD proof
Starts as soon as safe credited AMD compute is available.

## UI lane
Starts once canonical deterministic output contracts are stable.

The lanes converge at G5 integration.

---

# 2. M0 — REPOSITORY SCAFFOLD

## Goal
Create only the build skeleton.

## Work
- Node 22.12+ check
- Vite React TypeScript scaffold
- strict TypeScript
- dependencies
- .gitignore
- .env.example
- scripts
- Netlify config
- base CI
- empty module tree

## Minimum dependencies
Runtime:
- react
- react-dom
- zod
- @xyflow/react
- one decimal arithmetic library only if chosen

Dev:
- typescript
- vite
- vitest
- eslint
- @playwright/test
- @netlify/functions
- @netlify/vite-plugin if needed for chosen local workflow

## M0 PASS
- clean install
- typecheck
- lint
- empty tests
- production build
- no secret
- no implementation logic yet
- checkpoint SHA

---

# 3. M1 — DOMAIN CONTRACTS

## Goal
Freeze types before algorithms.

## Build
- case schema
- policy/service constraint schema
- evidence schema
- graph schema
- action/outcome schema
- certificate schema
- RecoveryBench report schema

## M1 PASS
- Zod schemas compile
- valid fixture parses
- invalid enum rejected
- missing required financial field rejected
- model output cannot contain canonical financial authority fields
- checkpoint SHA

No UI before this PASS.

---

# 4. M2 — POLICY & SERVICE FEASIBILITY ENVELOPE

## Goal
Prove constraint-first behavior.

## Build
Pure function:

`getFeasibleActions(case, evidence, policy, availability)`

Output:
- eligible actions
- excluded actions
- exact reason codes

## Required reason codes
Examples:
- POLICY_RETRY_LIMIT
- CUSTOMER_REFUSED
- CUSTOMER_REMEDY_CONFLICT
- EVIDENCE_REQUIRED
- ROUTE_UNAVAILABLE
- CONDITION_NOT_ALLOWED

## M2 PASS
- higher raw-value path can be excluded
- evidence-dependent path blocks on AMBIGUOUS/INCOMPLETE
- no AI can add an ineligible action
- deterministic repeatability
- RecoveryBench feasibility tests PASS
- checkpoint SHA

---

# 5. M3 — RECOVERY DECISION GRAPH + ECONOMICS

## Goal
Make the financial engine independently correct.

## Build
- bounded DAG validation
- path traversal/backward induction
- EFRC
- baseline
- winner/runner-up
- value gap

## M3 PASS
- no graph cycle
- no double-counted cost
- hand fixtures match
- winner tests 100%
- baseline tests
- tie rule
- zero denominator handling
- checkpoint SHA

This is the core product milestone.

---

# 6. M4 — ROBUSTNESS / DECISION EXPOSURE

## Build
- break-even
- plausible interval
- ROBUST / FRAGILE
- hinge distance
- Decision Exposure

## M4 PASS
- RG-001 hand result:
  - Retry 46.20
  - Stop/RTO 35.00
  - break-even about 55.6%
  - Decision Exposure 9.50
- threshold edge cases
- deterministic tolerance
- no hidden probability mutation
- checkpoint SHA

---

# 7. M5 — ACTION GATE + NEXT BEST EVIDENCE

## Build
Pure deterministic function:

Inputs:
- Evidence Status
- feasibility state
- robustness
- Decision Exposure
- merchant materiality threshold
- resolvable evidence mapping

Output:
- ACT_NOW
- ASK_FIRST
- HUMAN_REVIEW

## M5 PASS
- RG-001 -> ASK_FIRST
- robust valid case -> ACT_NOW
- ambiguity/policy conflict -> HUMAN_REVIEW
- model cannot override gate
- checkpoint SHA

---

# 8. M6 — RECOVERY DECISION CERTIFICATE

## Build
Assemble all canonical data into one immutable certificate object.

Certificate:
- provenance
- evidence
- feasibility
- paths
- economics
- robustness
- exposure
- action gate
- next evidence
- baseline
- human approval state

## M6 PASS
- certificate integrity fixtures 100%
- no duplicated/independent calculations in UI
- certificate regenerated identically
- no secret/PII
- checkpoint SHA

At this point G3 Economics Core can be considered for PASS if all associated tests/evidence pass.

---

# 9. M7 — RECOVERYBENCH V1 INFRASTRUCTURE

## Build
- 32 DEV interpreter fixtures
- 16 locked HOLDOUT fixtures
- 16 adversarial fixtures
- 20 economics fixtures
- 12 certificate fixtures
- runner
- JSON report
- Markdown summary
- version metadata

## M7 PASS
- deterministic layers run locally
- DEV/HOLDOUT separated
- fixture SHA recorded
- benchmark version recorded
- no public AI quality score yet
- checkpoint SHA

---

# 10. M8 — JUDGE UI SHELL

## Build
One-screen app:
- Evidence panel
- Feasibility panel
- RecoveryGraph
- Decision Certificate
- Proof drawer
- synthetic-data label

Initially:
AI section = DEV_MOCK clearly labeled.

## M8 PASS
- RG-001 fully understandable without explanation
- graph readable
- certificate values match domain outputs
- no user can edit canonical money accidentally
- responsive enough for demo laptop
- screenshot evidence
- checkpoint SHA

---

# 11. M9 — AI GATEWAY / MOCK PROVIDER

## Build
- provider interface
- mock provider
- evidence validator
- Netlify function request schema
- timeout
- rate limit
- kill switch
- fixed case allowlist
- fixed model server-side

## M9 PASS
- arbitrary prompt rejected
- unknown case ID rejected
- oversized/malformed request rejected
- no secret in client bundle
- timeout/fallback works
- mock never labeled AMD
- checkpoint SHA

---

# 12. M10 — REAL AMD PROOF

Prerequisite:
safe AMD credit/compute.

## Sequence
1. verify billing/credit
2. create shortest safe compute resource
3. capture hardware/runtime
4. start supported vLLM path
5. smoke request
6. structured output
7. DEV RecoveryBench subset
8. if quality insufficient -> test one stronger candidate
9. freeze model
10. run HOLDOUT
11. run adversarial set
12. measure p50/p95
13. capture token/runtime data
14. stop/delete GPU
15. recheck billing/credit

## M10 PASS
- real AMD Case Interpreter
- structured output
- evidence validation
- model selected by benchmark
- runtime evidence
- no financial-authority escape
- GPU shutdown verified
- checkpoint/evidence SHA

This is G2 PASS candidate.

---

# 13. M11 — GROUNDED DECISION EXPLAINER

## Build
Input:
certificate only.

Output:
- why winner wins
- hinge explanation
- Action Gate explanation
- Next Best Evidence message

## M11 PASS
- cannot change winner
- cannot change values
- cannot invent missing assumptions
- contradiction detector/test
- timeout fallback
- short bounded output
- checkpoint SHA

This completes the core G4 AI layer.

---

# 14. M12 — END-TO-END INTEGRATION

Flow:
case
-> AMD interpreter
-> evidence validator
-> feasibility
-> graph/economics
-> hinge/exposure
-> Action Gate
-> certificate
-> AMD explanation
-> approval

## M12 PASS
- RG-001 live path
- secondary open-box path
- AI unavailable path
- adversarial path
- Playwright hero/fallback/proof tests
- no stale mock labels
- checkpoint SHA

G5 PASS candidate.

---

# 15. M13 — PROOF SURFACE

## Show only measured facts
- RecoveryBench version
- HOLDOUT metrics
- adversarial escapes
- deterministic fixture counts
- certificate-integrity counts
- GPU
- ROCm
- vLLM
- model
- p50/p95
- token use
- sanitized runtime/cost
- audited SHA

## M13 PASS
Judge understands proof in under ~20 seconds.

No placeholder metric.

---

# 16. M14 — SECURITY / COST / RELEASE HARDENING

## Run
- secret scan
- npm audit
- dependency review
- prompt injection suite
- client bundle check
- rate-limit test
- kill-switch test
- malformed request tests
- public endpoint abuse review
- production build
- Playwright
- RecoveryBench final report

## M14 PASS
G6 evidence/security candidate PASS.

---

# 17. M15 — JUDGE EXPERIENCE / SUBMISSION

Only after core PASS.

- polish
- video
- cover
- slides
- README
- claim/evidence match
- submission links
- final freeze
- G7/G8/G9

---

# 18. FEATURE-KILL ORDER

If time slips, kill in this exact order:

1. multimodal condition AI
2. Value Leak Map
3. two-variable sensitivity
4. downloadable certificate
5. fancy graph animation
6. extra case types
7. extra dashboard cards
8. secondary model benchmark
9. secondary demo case polish
10. optional partner integration

Never kill:
- feasibility envelope
- deterministic economics
- break-even
- Decision Exposure
- Action Gate
- Recovery Decision Certificate
- RecoveryBench
- real AMD proof
- fallback
- core security

---

# 19. TECHNICAL RISK REGISTER

## R1 — AMD credit delayed
Probability: HIGH
Impact: HIGH

Mitigation:
- G3/UI build independently after G1
- support escalation
- AI gateway already abstracted

Trigger:
24h after kickoff still no safe compute

Action:
escalate officially; continue deterministic lane.

---

## R2 — AMD model startup/setup burns hours
Probability: MEDIUM
Impact: HIGH

Mitigation:
- one documented candidate first
- vLLM only
- no model zoo
- prewritten smoke command/checklist

Kill rule:
if first large candidate setup becomes unstable, drop to simpler compatible candidate.

---

## R3 — model fails structured output quality
Probability: MEDIUM
Impact: MEDIUM-HIGH

Mitigation:
- Zod
- vLLM structured output
- short enums
- non-thinking default
- RecoveryBench DEV first

Escalation:
one stronger model only.

---

## R4 — public AMD endpoint abuse
Probability: MEDIUM
Impact: HIGH

Mitigation:
- Netlify server-side proxy
- case allowlist
- no arbitrary prompt/model/max_tokens
- 4/min rate limit
- kill switch
- short max output

---

## R5 — inference exceeds function timeout
Probability: MEDIUM
Impact: HIGH

Mitigation:
- 25s application timeout
- shorter prompt/output
- smaller model
- non-thinking
- same-region choice only after measurement

Do not:
move core judge interaction to background jobs.

---

## R6 — financial math mismatch
Probability: LOW-MEDIUM
Impact: CRITICAL

Mitigation:
- centralized decimal adapter
- hand fixtures
- 100% deterministic fixture gate
- no UI math

Release blocker:
any mismatch.

---

## R7 — graph logic cycle / cost double count
Probability: LOW
Impact: CRITICAL

Mitigation:
- DAG validator
- explicit state-relative cost fence
- fixtures
- cycle rejection

Release blocker:
any failure.

---

## R8 — AI changes financial authority
Probability: MEDIUM
Impact: CRITICAL

Mitigation:
- schema excludes finance/action authority
- evidence validator
- prompt injection tests
- certificate built from deterministic package only

Release blocker:
any authority escape.

---

## R9 — benchmark overfitting
Probability: MEDIUM
Impact: HIGH

Mitigation:
- DEV 32 / HOLDOUT 16
- versioning
- fixture SHA
- rerun after contract change

---

## R10 — UI becomes a dashboard maze
Probability: MEDIUM
Impact: MEDIUM

Mitigation:
- one hero screen
- certificate is primary
- proof drawer
- kill generic analytics

---

## R11 — React Flow complexity
Probability: LOW-MEDIUM
Impact: LOW-MEDIUM

Mitigation:
- read-only
- hardcoded positions
- no graph editing
- remove MiniMap if unnecessary

Fallback:
replace with simple SVG/CSS path cards.

---

## R12 — Netlify deployment issue
Probability: LOW-MEDIUM
Impact: HIGH

Mitigation:
- deploy early after M8
- static SPA first
- function only after static deploy stable
- avoid framework adapter complexity

---

## R13 — live AMD endpoint unavailable at judging
Probability: MEDIUM
Impact: HIGH

Mitigation:
- video captures LIVE_AMD
- Proof surface contains verified recorded evidence
- deterministic app remains functional
- current mode clearly labeled

Do not fake live status.

---

## R14 — partner integration derails core
Probability: MEDIUM
Impact: HIGH

Mitigation:
partner work blocked until core G5 PASS + time threshold.

---

# 20. INTERNAL TIME-BUFFER RULE

Until official schedule is clarified:
- treat Oct 17 as build freeze
- Oct 18 submission only

Internal completion priorities:
- deterministic core first third of build window
- UI + RecoveryBench second third
- AMD/integration no later than middle-to-late window
- final day before freeze reserved for evidence/security/demo

If AMD credit arrives late:
never delay deterministic milestones waiting for it.

---

# 21. DEFINITION OF "STRONG PRODUCT" FOR THIS HACKATHON

Not:
most features.

It means:
- one sharp problem
- one memorable artifact
- deterministic correctness
- real AMD contribution
- measurable proof
- explicit uncertainty
- commercially sane constraints
- safe failure
- judge-readable demo
- no overclaim

## NEXT SAFE ACTION

Pre-kickoff architecture is now sufficiently specified.

Only material unknowns worth further research are:
- kickoff rules/track changes,
- actual AMD credit/runtime environment,
- exact model performance under RecoveryBench.

Do not add more product features pre-kickoff unless new evidence reveals a material gap.
