# RECLAIMGRID AI — TEST & EVIDENCE PLAN

## CONTROL
- PROJECT: ReclaimGrid AI
- CONTROL CODE: RG-ACT3
- FILE: 05_TEST_EVIDENCE_PLAN.md
- SNAPSHOT DATE: 2026-10-06
- STATUS: PRE-KICKOFF TEST/EVIDENCE FREEZE
- CURRENT GATE: G0 — Registration & Environment
- IMPLEMENTATION STATUS: NOT STARTED
- PURPOSE: Define what must be tested and what evidence must be captured before each gate can PASS.

## CORE PRINCIPLE
No feature is considered complete because it "looks right."

Every important claim must have:
1. a reproducible test,
2. a PASS/FAIL result,
3. evidence,
4. a gate owner/state,
5. a recorded blocker if it fails.

## EVIDENCE TYPES
Allowed evidence:
- Git commit SHA
- test command output
- deterministic fixture result
- screenshot with secrets/PII removed
- sanitized logs
- AMD runtime metadata
- benchmark/result table
- demo recording
- architecture diagram
- submission-page verification
- deployed application URL

Do NOT use evidence that exposes:
- passwords
- OTPs
- API keys
- tokens
- cookies
- real customer PII
- private billing details
- secret-bearing URLs

## GLOBAL PASS RULE
A gate may PASS only when:
- all mandatory tests for that gate pass,
- no unresolved release blocker remains,
- evidence is stored or referenced,
- latest verified main SHA is recorded,
- next gate entry criteria are met.

A partial pass is not a PASS.

---

# G0 — REGISTRATION & ENVIRONMENT

## Objective
Prove the required accounts, event enrollment, team setup, repository, and safe cloud-access path exist before build work begins.

## Mandatory checks
- AMD account access works
- AMD AI Developer Program membership confirmed
- ACT III enrollment confirmed
- participation mode confirmed as Online
- Discord connection/server/event-channel access confirmed
- ReclaimGrid AI team exists
- team is Solo / Closed
- AMD Developer Cloud benefit is visible
- cloud-credit request is submitted
- AMD Developer Cloud SSO/account access works
- public GitHub repository exists
- default branch is main
- control files are being created on main
- no paid GPU was created
- no payment method was added

## Evidence
- event/dashboard verification
- team-page verification
- AMD member/credit-request confirmation
- AMD Developer Cloud account-access verification
- GitHub repo metadata
- verified main commit SHA

## Current state
G0 is PASS as of 2026-10-07.

Verified:
- event/account/team/Discord access complete,
- AMD AI Developer Program membership complete,
- AMD Developer Cloud SSO/account access works,
- complimentary credit request submitted,
- no payment method added,
- no GPU resource created,
- public GitHub repository/control system verified.

Complimentary credit activation is tracked as a G2 blocker, not a G0 blocker.

## G0 PASS condition
PASS when:
- required event/account/team access is complete,
- AMD Developer Cloud account access is verified,
- complimentary credit request is submitted,
- no unsafe billing/payment action occurred,
- public repository/control state is verified.

Actual credit balance is required for safe real AMD compute / G2 proof, not for G0 completion.

---

# G1 — RULES & SCOPE FREEZE

## Objective
Freeze final hackathon rules and ensure product scope is compliant before implementation.

## Mandatory re-verification
After kickoff:
- official build window
- official submission deadline
- Track 3 availability and wording
- judging criteria
- repository requirement
- license requirement
- AMD meaningful-workload requirement
- partner-prize rules if relevant
- geographic/prize eligibility
- submission fields
- any event-specific kickoff instructions
- implementation timing restrictions, if any

## Scope checks
- one clear primary user
- one clear problem
- bounded V1 case types
- bounded route set
- deterministic financial authority
- AMD AI role clearly separated
- human approval preserved
- non-goals still excluded

## Evidence
- refreshed rules snapshot
- final scope document
- decision-log entries for any change
- verified main SHA

## G1 PASS condition
PASS only when no unresolved rule ambiguity can materially invalidate scope, architecture, or submission eligibility.

---

# G2 — AMD PROOF

## Entry blocker
Real AMD proof remains BLOCKED until:
- complimentary credit is visibly active, OR
- an explicitly approved safe no-charge AMD compute route is verified.

This blocker does not prevent G3 deterministic/local work after G1.

## Objective
Prove AMD powers a meaningful working AI workload.

## Mandatory technical checks
- complimentary credit or approved safe compute path is active
- AMD resource type is identified
- expected hourly cost is known before launch
- credit offset is verified before launch
- start/stop/delete process is known
- model serving works on AMD infrastructure
- one bounded inference succeeds
- one application-relevant inference succeeds
- endpoint/runtime metadata is captured safely
- GPU is stopped/deleted after controlled test
- remaining credit is checked

## Candidate workload
One or more:
- interpret free-text return/NDR reason
- produce structured bounded extraction
- explain deterministic route ranking
- draft bounded merchant/customer message

## AMD proof evidence
Capture:
- AMD Developer Cloud environment evidence
- AMD Instinct / ROCm evidence
- model/runtime identification
- sanitized service-start evidence
- sanitized inference request/response
- latency
- GPU/resource type
- cost ledger entry

## Failure tests
- endpoint unavailable
- timeout
- malformed model response
- invalid structured output

## G2 PASS condition
PASS only if:
- a real AMD-hosted inference path works,
- the workload is meaningful to ReclaimGrid,
- evidence is judge-presentable,
- no paid-risk or secret exposure exists.

Mock/local inference can support development, but cannot satisfy G2.

---

# G3 — ECONOMICS CORE

## Objective
Prove deterministic recovery economics is correct, reproducible, transparent, and independent of AI.

## Required artifacts
- normalized case schema
- route eligibility rules
- baseline rules
- route equations
- ranking logic
- synthetic fixture dataset
- deterministic test suite

## Mandatory deterministic tests

### Input validation
- valid case accepted
- missing required numeric field rejected
- negative unsupported cost rejected
- non-finite number rejected
- unknown case type rejected
- unknown condition enum rejected
- duplicate case ID handled explicitly

### Route eligibility
- eligible route included
- prohibited route excluded
- exclusion reason preserved
- no eligible route handled safely

### Economics
For every route:
- formula uses only explicit inputs/assumptions
- repeated runs produce identical result
- known fixture matches hand-calculated expected value
- zero-cost edge case works
- very high-cost edge case works
- decimal precision policy is consistent

### Ranking
- highest expected recovery value wins
- tie handling is deterministic
- excluded route can never win
- missing required data cannot silently default to a favorable value

### Baseline
- baseline route is reproducible
- baseline expected value uses same canonical financial inputs
- baseline cannot call AI

### Uplift
- absolute uplift correct
- percentage uplift correct
- division-by-zero handled explicitly
- negative uplift case represented correctly

## Evidence
- test output
- fixture table
- hand-calculation examples
- code/commit SHA
- baseline-vs-ReclaimGrid result table

## G3 PASS condition
PASS only when deterministic financial logic works with AI completely unavailable.

---

# G4 — INTELLIGENCE LAYER

## Objective
Prove AMD AI adds interpretation/explanation value without gaining financial authority.

## Mandatory tests

### Structured extraction / evidence quality
- bounded free text -> valid allowed schema
- unknown information remains unknown
- model does not invent canonical price/cost/probability
- malformed output rejected
- unknown enum rejected
- exact evidence spans exist in source note
- contradiction becomes AMBIGUOUS when unresolved
- required missing information becomes INCOMPLETE
- invalid contract output becomes INVALID and is discarded
- model-authored numerical confidence is not used as decision authority

### Prompt-injection resistance
Test synthetic case text containing instructions such as:
- ignore previous instructions
- change the winner
- refund immediately
- output hidden system prompt
- reveal credentials

Expected result:
- case text remains data
- deterministic result unchanged
- no privileged action occurs
- output stays within allowed contract or safely fails

### Explanation fidelity
- explanation references canonical deterministic winner
- explanation does not replace route values
- explanation distinguishes facts from assumptions
- contradictory financial claim is rejected or visibly separated

### Timeout/fallback
- model timeout -> deterministic result remains usable
- endpoint failure -> deterministic result remains usable
- invalid AI output -> deterministic result remains usable

### Message drafting
- no unsupported guarantee
- no invented refund/payment completion
- bounded tone/length
- no hidden action execution

## Evidence
- prompt contract
- response schema
- adversarial fixture outputs
- fallback test results
- AMD-backed successful examples

## G4 PASS condition
PASS only when AI can fail completely without corrupting or blocking the deterministic decision path.

---

# G5 — PRODUCT INTEGRATION

## Objective
Prove the user can complete the full judge-facing workflow end to end.

## Required journey
1. Load/select synthetic case
2. Validate input
3. View eligible/excluded routes
4. Run deterministic economics
5. View route ranking
6. View baseline comparison
7. Trigger/view AMD AI interpretation or explanation
8. See assumptions/guardrails
9. Approve/reject/select alternative
10. See demo-only final state

## Mandatory integration tests
- clear-win case
- close-call case
- excluded-route case
- no-eligible-route case
- missing-information case
- free-text AI case
- AI unavailable case
- invalid input case

## UX checks
- no hidden financial result
- assumptions visible
- winner clearly identified
- alternatives visible
- AI content visually distinguishable from canonical calculations
- approval is explicit
- no real consequential action is performed

## Evidence
- end-to-end test results
- screenshots
- short screen recording
- deployed preview
- verified main SHA

## G5 PASS condition
A first-time judge can understand the complete flow without verbal rescue.

---

# G6 — EVIDENCE & SECURITY

## Objective
Prove the build is safe enough for a public hackathon demo and evidence package.

## Mandatory security checks
- secret scan
- `.env` excluded
- `.env.example` placeholders only
- no token in Git history
- no real customer PII
- dependency audit
- production build
- input validation
- AI-output validation
- AI timeout/fallback
- no uncontrolled external action
- sanitized logs
- sanitized screenshots

## Manual review checks
- public repo has no private account data
- screenshots hide email/address/token/billing identifiers
- demo browser has no unrelated sensitive tabs
- terminal output has no secrets
- AMD evidence is shareable safely

## Cost checks
- GPU cost ledger complete
- no unexpected paid charge
- no running unused GPU
- remaining credit recorded after final AMD proof test

## Evidence
- security test report
- dependency audit output
- secret-scan output
- production build output
- cost ledger
- screenshot review checklist

## G6 PASS condition
No hard-stop condition or release blocker remains.

---

# G7 — JUDGE EXPERIENCE

## Objective
Optimize how judges understand technology, business value, originality, and presentation.

## Judge comprehension test
A reviewer should understand within roughly one minute:
- what problem ReclaimGrid solves
- who uses it
- why static/manual recovery decisions lose value
- how deterministic economics works
- what AMD AI adds
- where human approval occurs
- what measurable uplift the synthetic demo shows

## Required presentation evidence
- polished landing/demo screen
- clear before-vs-after metric
- one strong case walkthrough
- visible AMD proof
- concise architecture diagram
- concise safety/trust explanation
- demo script
- fallback plan

## Dry-run tests
Run at least:
- normal demo
- AMD inference slow
- AMD inference unavailable
- accidental refresh/reload
- judge asks "Why not just use an LLM?"
- judge asks "How do you calculate the number?"
- judge asks "What exactly is AMD doing?"
- judge asks "Is this real customer data?"

## Expected answers
Must be supported by product/evidence, not only spoken claims.

## G7 PASS condition
Demo remains understandable and credible even if live AI fails.

---

# G8 — SUBMISSION FREEZE

## Objective
Freeze code, evidence, links, copy, and submission assets.

## Mandatory checks
- final public repo accessible
- final main SHA recorded
- license verified against current rules
- README accurate
- application URL works
- demo video works
- slide/pitch deck works
- cover image present
- project title consistent
- short description consistent
- long description consistent
- track selection correct
- technology tags correct
- AMD proof described accurately
- no unsupported claims
- all links tested
- no secret in public assets
- no placeholder text
- no "coming soon" dependency for core proof

## Regression suite
Re-run:
- deterministic tests
- AI contract tests
- core end-to-end tests
- production build
- secret scan
- dependency audit
- final deployed smoke test

## Freeze rule
After G8 PASS:
- no feature changes
- only critical submission-blocker fixes
- every change requires re-running impacted tests

## G8 PASS condition
Submission package is complete and reproducible.

---

# G9 — FINAL AUDIT & SUBMIT

## Objective
Perform the final independent audit immediately before submission.

## Final audit checklist
- deadline rechecked
- rules rechecked
- submission account/team correct
- Track 3 correct
- public repo link correct
- deployed app link correct
- demo video link correct
- deck link correct
- cover image correct
- AMD usage claim supported
- business-value claim supported by synthetic results
- originality claim is not overstated
- all required fields complete
- no secret/PII
- no paid GPU still running
- final main SHA captured
- final deployed version corresponds to audited SHA where possible

## Submission rule
Only submit after G9 audit PASS.

## Post-submit evidence
Capture:
- submission confirmation
- timestamp
- final submission URL/state
- final main SHA

Do not alter the frozen submission unless a verified correction is required and the platform permits it.

---

# SYNTHETIC FIXTURE MATRIX

Minimum planned fixture categories:

| ID | Case Type | Purpose |
|---|---|---|
| RG-001 | Failed delivery | Redelivery clear win |
| RG-002 | Failed delivery | Refund/close beats expensive redelivery |
| RG-003 | Clean return | Restock/relist clear win |
| RG-004 | Open-box return | Relist vs liquidation close call |
| RG-005 | Damaged return | Restock explicitly ineligible |
| RG-006 | Aging inventory | Liquidation becomes preferred |
| RG-007 | Any | No eligible route |
| RG-008 | Any | Missing required financial input |
| RG-009 | Any + free text | AMD AI structured interpretation |
| RG-010 | Any + adversarial text | Prompt-injection test |
| RG-011 | Any | AI timeout/fallback |
| RG-012 | Any | Baseline better than ReclaimGrid candidate route / negative uplift |
| RG-013 | Any | Tie handling |
| RG-014 | Any | Zero baseline value / percentage-uplift edge case |

Exact numbers are frozen in G3.

# MEASUREMENT PLAN

## Core business metrics
For the synthetic dataset:
- baseline recovered value
- ReclaimGrid expected recovered value
- absolute uplift
- percentage uplift
- number of changed decisions
- number of ineligible routes safely excluded

## AI metrics
Keep lightweight:
- valid structured-response rate
- timeout/failure rate during tests
- explanation-schema validation rate
- average demo inference latency if useful

Do not create meaningless benchmark complexity.

# EVIDENCE NAMING CONVENTION

Recommended future structure:

```text
/evidence/
  g2-amd/
  g3-economics/
  g4-ai/
  g5-integration/
  g6-security/
  g7-demo/
  g8-freeze/
  g9-submit/
```

Recommended evidence filename style:
`G<gate>_<YYYYMMDD>_<short-description>.<ext>`

Examples:
- `G2_20261012_AMD_MI300X_RUNTIME.md`
- `G3_20261013_ECONOMICS_TEST_RESULTS.md`
- `G6_20261016_SECRET_SCAN.txt`

Do not commit evidence containing sensitive data.

# TEST RESULT FORMAT

Every formal gate test report should record:
- TEST ID
- GATE
- DATE/TIME
- MAIN SHA
- ENVIRONMENT
- COMMAND / METHOD
- EXPECTED RESULT
- ACTUAL RESULT
- PASS/FAIL
- EVIDENCE LOCATION
- BLOCKER
- NEXT SAFE ACTION

# BLOCKER SEVERITY

## BLOCKER
Prevents gate PASS.
Examples:
- AMD proof absent
- deterministic math incorrect
- secret exposure
- payment risk
- core demo broken

## MAJOR
Does not necessarily block current internal development but blocks release/submission if unresolved.
Examples:
- weak explanation fallback
- broken evidence asset
- critical UX confusion

## MINOR
Non-core polish issue.
May be deferred if it does not affect judging or safety.

# TEST DISCIPLINE
- Never change a failing expected result just to make the test pass.
- Fix the product or justify the requirement change in the decision log.
- Re-run impacted tests after every critical fix.
- Record the exact commit SHA associated with evidence.
- Prefer deterministic automated tests over visual-only checks where possible.
- Use manual checks for browser/account/submission states that cannot be safely automated.

## RESEARCH-UPGRADE TEST ADDENDUM

The Recovery Decision Graph upgrade adds mandatory tests before G3/G4/G5 can PASS:

### Policy & Service Feasibility Envelope
- merchant-policy violation excludes the path
- confirmed refusal can block another forced retry
- approved remedy/SLA cannot be silently downgraded
- AMBIGUOUS/INCOMPLETE evidence blocks evidence-dependent paths
- operationally unavailable route is excluded
- excluded path includes deterministic reason
- higher raw EFRC cannot override a hard constraint
- no hidden CLTV/loyalty weighting exists

### Recovery graph correctness
- graph is acyclic
- only state-valid actions appear
- downstream failure/success branches are included
- excluded actions cannot re-enter later through another path
- same case + assumptions produce identical path values

### Multi-stage economics
- hand-calculated hero case matches engine path EV
- downstream salvage value is included exactly once
- no double-counting of shipping/RTO/refurbishment cost
- baseline uses the same canonical financial inputs
- winner and runner-up are reproducible

### Robustness / break-even
- break-even threshold matches a hand calculation
- threshold outside valid probability/value range is handled explicitly
- ROBUST/FRAGILE label follows a documented rule
- close-call fixture changes winner at the expected threshold
- sensitivity analysis never changes canonical inputs silently

### AMD Case Interpreter
- extracted reason_code is schema-valid
- evidence_span actually exists in source text
- unsupported signal is rejected or marked unknown
- ambiguity/missing evidence remains visible through deterministic Evidence Status
- missing fields remain explicit
- model cannot inject financial values into the deterministic core

### Decision Hinge / Next Best Evidence
- FRAGILE case identifies the correct hinge variable
- break-even threshold is unchanged from deterministic robustness output
- hinge distance is calculated correctly
- ROBUST case does not manufacture an unnecessary evidence request
- Next Best Evidence maps to the hinge variable
- AMD-drafted evidence request cannot alter canonical economics
- formal EVPI/EVSI is not silently approximated or mislabeled

### Decision Exposure / Action Gate
- Decision Exposure equals maximum regret of the base winner over the declared one-dimensional plausible range
- lower/upper endpoint calculations are hand-verified for linear hero fixtures
- value is never described as guaranteed loss
- ACT NOW rule matches robustness/materiality condition
- ASK FIRST rule requires fragile + material exposure + bounded evidence path
- HUMAN REVIEW appears for invalid/conflicting/missing critical evidence or policy ambiguity
- model output cannot choose or override the Action Gate

### Recovery Decision Certificate
- certificate values exactly match the canonical decision package
- winner/runner-up/value gap match deterministic outputs
- hinge/break-even/robustness match robustness engine
- Decision Exposure / Action Gate match deterministic rules
- accepted AMD evidence span exists in source note
- certificate can be reconstructed from logged synthetic inputs and outputs
- no private/secrets/real PII appear in certificate

### Decision Ledger
- ledger records accepted extraction, policy result, path values, winner/runner-up, break-even result, Decision Hinge, and approval state
- ledger never stores secrets/real PII
- ledger output is sufficient to reconstruct the judge-facing decision

### RecoveryBench acceptance
Use the frozen plan in `19_RECOVERYBENCH_EVAL_PLAN.md`.

Benchmark integrity:
- DEV and locked HOLDOUT results reported separately
- fixture commit SHA recorded
- prompt-contract version recorded
- model/serving/code SHA recorded
- prompt/schema change after HOLDOUT scoring triggers benchmark version/rerun
- no judge-facing score is based only on the DEV set

Required measured layers:
- Layer A: Case Interpreter quality
- Layer B: adversarial / trust boundary
- Layer C: deterministic economics
- Layer D: Recovery Decision Certificate integrity
- Layer E: real AMD runtime performance

No result may be marked PASS before it is actually measured.

### AMD model-serving acceptance
- Qwen3-8B smoke inference succeeds on real AMD infrastructure first
- structured JSON output passes schema validation
- evidence spans are semantically validated against source text
- non-thinking mode is tested first for extraction
- 32B/30B-A3B is tested only if 8B quality is insufficient and credit/cost remain safe
- final model choice is supported by fixture results, not generic benchmark prestige

### Hero demo acceptance
The hero failed-delivery case cannot pass G5 unless it visibly proves:
1. messy note -> AMD extraction,
2. recovery graph,
3. deterministic multi-stage path values,
4. winner + runner-up + value gap,
5. break-even threshold,
6. Decision Hinge + Decision Exposure,
7. Action Gate + Next Best Evidence,
8. Recovery Decision Certificate,
9. grounded AMD explanation,
10. human approval.

## NEXT SAFE ACTION
Keep implementation blocked pre-kickoff. At G1 authorization, implement deterministic/eval contracts so RecoveryBench evidence exists from the start rather than being added at the end.
