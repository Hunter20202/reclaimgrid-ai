# RECLAIMGRID AI — HACKATHON CRITICAL PATH & PARALLEL GATES

## CONTROL
- PROJECT: ReclaimGrid AI
- CONTROL CODE: RG-ACT3
- FILE: 17_HACKATHON_CRITICAL_PATH.md
- DATE: 2026-10-07
- STATUS: PRE-KICKOFF EXECUTION HARDENING
- PURPOSE: Prevent AMD credit approval latency from wasting the short competition window while preserving all cost/security rules.

## WHY THIS CHANGE IS NEEDED

The official ACT III main page requires:
- a working product,
- a meaningful workload on AMD infrastructure/hardware,
- Track 3 demo proof of useful commercial action and measurable business effect.

The official page advertises $100 AMD credits, but the event requirement is meaningful AMD usage in the working product — not that complimentary credit must already be active before local product work begins.

Therefore:
**complimentary credit activation must not remain a blocker for all product implementation after kickoff.**

It blocks real AMD proof.
It does NOT need to block deterministic economics, synthetic fixtures, tests, or local UI work.

Official source:
https://lablab.ai/ai-hackathons/amd-developer-hackathon-act-iii

## CURRENT SCHEDULE RISK

Current official pages remain inconsistent:
- main event page: online phase 12–18 Oct 2026
- live dashboard: online build 12–17 Oct 2026
- live dashboard: submission closes 18 Oct 2026 15:00 UTC
- live dashboard currently shows Tracks: TBA
- main event page currently shows four tracks including Track 3 — Reinvent Commerce

Execution rule:
Use the stricter build assumption until kickoff:
**Treat 17 Oct as the practical build-freeze target and 18 Oct 15:00 UTC as submission deadline unless kickoff states otherwise.**

Do not wait until 18 Oct to finish product work.

## GATE GOVERNANCE UPGRADE

Old rule:
"No gate advances unless prior gate PASS."

Problem:
If complimentary credit is delayed, G2 AMD Proof could block G3 Economics Core even though the economics core does not require AMD.

New rule:
**No dependent gate advances until its prerequisites PASS. Independent lanes may proceed in parallel after G1.**

This is safer for a time-boxed hackathon.

## G0 — REGISTRATION & SAFE ACCESS

G0 PASS should require:
- ACT III enrollment
- online participation
- team created
- Discord/event access
- public repo
- AMD AI Developer Program membership
- AMD Developer Cloud SSO/account access
- complimentary credit request submitted
- no payment method added
- no accidental paid resource

Actual complimentary credit activation is NOT required for G0 PASS.

Credit activation becomes a G2 blocker.

## G1 — RULES & SCOPE FREEZE

At kickoff:
- recheck official track list
- recheck build window
- recheck deadline
- recheck judging
- recheck repository/license/submission rules
- recheck AMD requirement
- freeze final V1 scope
- authorize implementation

G1 is the implementation-start gate.

## PARALLEL LANE A — G2 AMD PROOF

Can begin when:
- complimentary credit is visibly active, OR
- an explicitly safe approved no-charge AMD route is available.

Tasks:
- Qwen3-8B + vLLM smoke proof
- structured Case Interpreter
- grounded explanation
- AMD runtime evidence
- cost ledger
- stop/delete resource

If credit is delayed:
Lane A stays BLOCKED.
Other independent lanes continue.

## PARALLEL LANE B — G3 ECONOMICS CORE

Can begin immediately after G1 PASS.

Does NOT require AMD credit.

Tasks:
- M0 repository scaffold
- M1 schemas/contracts
- M2 Policy & Service Feasibility Envelope
- M3 Recovery Decision Graph + EFRC
- M4 break-even / ROBUST-FRAGILE / Decision Exposure
- M5 Action Gate + Next Best Evidence
- M6 Recovery Decision Certificate
- M7 RecoveryBench infrastructure
- Recovery Decision Certificate assembly
- hand-calculated fixture tests

This is the highest-value local build lane.

## PARALLEL LANE C — JUDGE UI SHELL

May begin after the deterministic output contract is stable enough.

Tasks:
- M8 single-screen hero shell
- read-only graph visualization
- Decision Certificate layout
- feasibility/exclusion panel
- baseline comparison
- Proof drawer
- AMD evidence area with clearly labeled mock/unavailable development state
- human approval UI

Important:
Any mock AI output used before real AMD proof must be visibly marked development/mock and must never be used as submission proof.

## G4 — INTELLIGENCE LAYER

Prerequisites:
- G2 real AMD serving proof
- stable Case Interpreter schema
- stable deterministic decision package

Tasks:
- production prompt contracts
- semantic evidence validation
- injection tests
- grounded explainer
- timeout/fallback

## G5 — PRODUCT INTEGRATION

Prerequisites:
- G3 deterministic core PASS
- G4 intelligence layer PASS
- judge UI shell stable

Then integrate:
case -> AMD evidence -> graph -> economics -> hinge -> exposure -> action gate -> certificate -> explanation -> approval.

## G6–G9
Remain sequential:
- G6 Evidence & Security
- G7 Judge Experience
- G8 Submission Freeze
- G9 Final Audit & Submit

## CREDIT DELAY CONTINGENCY

### If credit arrives before kickoff
Excellent:
- G1 at kickoff
- start G2 and G3 in parallel immediately

### If credit arrives during build window
Do not stop local work.
- G3/UI continue
- begin G2 the moment safe credit is verified
- integrate through the prebuilt AI gateway

### If credit is still absent by approximately 24 hours after kickoff
Escalate through official AMD/lablab support/Discord channels while continuing deterministic/UI work.

### If credit is still absent near midpoint
Recheck official event-provided AMD infrastructure options and mentor guidance.
Do not add a payment method without explicit cost authorization.

### If no safe AMD path exists by final integration phase
Submission is at risk because AMD meaningful workload is mandatory.
Escalate immediately; do not fake AMD proof.

## FROZEN MILESTONE ORDER
After G1 PASS, execute the verified milestone sequence from `24_IMPLEMENTATION_SEQUENCE_AND_RISK_REGISTER.md`:

M0 scaffold
-> M1 contracts
-> M2 feasibility
-> M3 economics
-> M4 robustness/exposure
-> M5 action gate
-> M6 certificate
-> M7 RecoveryBench
-> M8 UI
-> M9 AI gateway/mock
-> M10 real AMD proof
-> M11 grounded explainer
-> M12 integration
-> M13 Proof surface
-> M14 security/release
-> M15 judge/submission

Do not skip a failed milestone to work on polish.

## PRACTICAL BUILD-FREEZE TARGET

Because the live page says online build 12–17 Oct:
- target core feature complete: by 15 Oct
- target integrated demo: by 16 Oct
- target build freeze/security/evidence: 17 Oct
- 18 Oct reserved for submission verification only

These are internal risk-control targets, not official deadlines.

## ONE-ACTION RULE DURING BUILD

The user's operating style remains:
- one exact action at a time,
- verify output,
- checkpoint SHA,
- continue.

Parallel gates mean the Control Room may switch lanes when one lane is externally blocked.
It does NOT mean giving the user multiple tasks at once.

## NEXT SAFE ACTION

Before kickoff:
- no implementation code,
- continue only research/control hardening,
- treat AMD credit activation as a G2 blocker, not a global blocker.

At kickoff:
1. perform G1 rules re-verification,
2. authorize implementation,
3. begin G3 deterministic core immediately even if G2 credit is still pending.
