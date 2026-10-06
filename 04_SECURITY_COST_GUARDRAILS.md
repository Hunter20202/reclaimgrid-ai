# RECLAIMGRID AI — SECURITY & COST GUARDRAILS

## CONTROL
- PROJECT: ReclaimGrid AI
- CONTROL CODE: RG-ACT3
- FILE: 04_SECURITY_COST_GUARDRAILS.md
- SNAPSHOT DATE: 2026-10-06
- STATUS: PRE-KICKOFF SECURITY/COST FREEZE
- CURRENT GATE: G0 — Registration & Environment
- IMPLEMENTATION STATUS: NOT STARTED
- PURPOSE: Freeze the minimum security, privacy, AI-trust, logging, dependency, and GPU-cost controls before any product implementation begins.

## PRIMARY RULE
ReclaimGrid must fail safe before it fails open.

When security, payment, credential, data-handling, or AI-authority state is ambiguous:
**STOP, inspect, and require explicit authorization before continuing.**

## 1. SECRET HANDLING

### Never allowed in repository
Do not commit:
- passwords
- OTPs
- API keys
- access tokens
- refresh tokens
- session cookies
- OAuth state
- SAML RelayState
- private SSH keys
- cloud credentials
- database credentials
- payment details
- private activation links if they contain secret-bearing parameters

### Runtime rule
Secrets must be supplied only through:
- environment variables
- secure platform secret storage
- local untracked configuration

### Repository rule
Allowed:
- `.env.example`
- placeholder names such as `AMD_API_KEY=your_key_here`

Blocked:
- real values
- copied browser tokens
- screenshots containing secrets
- logs containing credentials

### Git rule
If a secret is ever committed:
1. STOP development.
2. Revoke/rotate the secret immediately.
3. Remove it from current source.
4. Audit Git history.
5. Rewrite history if needed.
6. Re-verify no secret remains.
7. Record the incident in the decision/security log.

Deleting the file alone is not enough.

## 2. PII / DATA MINIMIZATION

### V1 default
Use synthetic ecommerce cases only.

### Do not collect or store real customer PII for the hackathon demo unless explicitly re-authorized.
Avoid:
- real names
- phone numbers
- email addresses
- home addresses
- payment details
- tracking numbers tied to real customers
- real merchant order IDs
- private customer messages

### If an example needs human-readable identity
Use synthetic labels such as:
- Customer A
- Case RG-001
- Merchant Demo Store

### Browser/account data
Personal information entered into AMD, GitHub, Lablab, Discord, or other account forms must remain in those account systems.
Do not copy it into:
- repository files
- demo data
- screenshots
- logs
- issue text

## 3. AI TRUST BOUNDARY

The AI model is untrusted application input.

### AI may
- interpret bounded free text
- extract structured attributes within an allowed schema
- explain deterministic results
- summarize tradeoffs
- draft text
- identify uncertainty

### AI may not
- invent canonical financial inputs
- alter deterministic route values
- override policy eligibility
- create hidden weights
- approve its own recommendation
- execute external actions
- write directly to payment, courier, inventory, or merchant systems
- control shell/database/cloud operations without an explicit application-side allowlist and human authorization

### Canonical authority order
1. Validated source inputs
2. Deterministic merchant policy
3. Deterministic recovery economics
4. Human approval
5. AI explanation/drafting as non-authoritative support

## 4. AI INPUT CONTROLS

Before any model call:
- validate schema
- bound string length
- normalize known enums
- reject malformed numeric data
- remove unnecessary PII
- include only the minimum context required
- separate trusted calculation output from untrusted free text
- prevent raw secrets from entering prompts

### Prompt-injection assumption
Any free-text return reason or note may contain adversarial instructions.

Therefore:
- user/case text is data, not system instruction
- model prompt must clearly separate instruction from case content
- the application must not expose tools or privileged actions to case text
- AI output must still pass deterministic validation

## 5. AI OUTPUT CONTROLS

Where structured output is used:
- enforce JSON/schema validation
- reject unknown action types
- reject missing required fields
- reject invalid enum values
- reject financial numbers that conflict with deterministic canonical values
- cap output length

Where natural-language explanation is used:
- render it separately from authoritative calculations
- label it as AI-generated explanation
- never hide assumptions or route math behind prose

## 6. HUMAN APPROVAL CONTROL

Any consequential action must require human approval.

For V1:
- approval is demo-only
- no real refund
- no real payment
- no real shipment
- no real inventory update
- no customer-account mutation
- no irreversible merchant action

The demo may record:
- Approved
- Rejected
- Alternative Selected

but must not execute external business actions.

## 7. AMD GPU / CLOUD COST CONTROL

### Current known state
- AMD Developer Cloud account access: PASS
- Complimentary credit request: SUBMITTED / PENDING APPROVAL
- Paid MI300X path was visible at $1.99/hour
- Billing displayed ACTION NEEDED

### Hard blocks
Until complimentary credit is approved and visibly available:
- DO NOT add a payment method
- DO NOT create a paid GPU droplet
- DO NOT enable auto-billing
- DO NOT accept a paid upgrade
- DO NOT request paid quota merely to test
- DO NOT start a GPU resource

### After complimentary credit approval
Before first GPU launch:
1. Verify credit balance/benefit is visible.
2. Verify expected hourly cost.
3. Verify whether credit will actually offset that resource.
4. Verify shutdown/deletion method.
5. Set a strict experiment budget.
6. Record start time.
7. Shut down/delete immediately after the test.
8. Re-check remaining credit.

### Default resource strategy
- smallest viable AMD resource that proves the required workload
- shortest possible runtime
- no idle GPU
- no always-on endpoint unless judge demo requires it
- no training/fine-tuning
- no background jobs
- no uncontrolled retry loop

## 8. PAYMENT STOP CONDITION

Immediate STOP if any page or workflow asks for:
- credit card
- debit card
- billing authorization
- deposit
- paid subscription
- auto-recharge
- charge confirmation
- paid quota increase
- unexpected invoice acceptance

Do not proceed until the cost path is explicitly reviewed and authorized.

## 9. RATE / RETRY CONTROL

Any external AI request must later implement:
- bounded timeout
- bounded retry count
- exponential or fixed backoff if retry exists
- no infinite loop
- no automatic high-volume batch
- visible failure state

Default target:
- zero retry or one controlled retry for judge demo unless testing proves otherwise.

## 10. LOGGING RULES

Allowed to log:
- case_id using synthetic identifiers
- route selected
- deterministic values
- model request status
- response validation status
- latency
- model/runtime name
- AMD proof metadata
- fallback state
- demo approval decision

Do not log:
- secrets
- auth headers
- cookies
- full tokens
- passwords
- real customer PII
- private account information
- raw browser URLs containing secret-bearing query strings

### Error logging
Errors should be useful but sanitized.
Prefer:
- `AMD inference timeout after N seconds`

Avoid:
- dumping full request headers
- dumping environment variables
- dumping complete provider responses if they may contain secrets

## 11. DEPENDENCY SAFETY

Before G6 PASS:
- use a lockfile
- pin or constrain dependency versions appropriately
- run dependency vulnerability audit
- remove unused packages
- avoid packages with unnecessary privilege/scope
- prefer mature, maintained dependencies
- avoid adding a package for trivial functionality
- review install scripts for unusual packages if introduced

No dependency may be added solely for convenience if it materially expands attack surface without judge value.

## 12. FILE / REPOSITORY SAFETY

Required before implementation:
- `.gitignore` must exclude `.env`, local secret files, build artifacts as appropriate, and temporary credential files
- public repository must not expose private data
- sample fixtures must be synthetic
- screenshots/evidence committed to repo must be scrubbed

### Binary/evidence rule
Before committing screenshots or logs:
- inspect for names/email/address/token
- crop/redact sensitive account UI
- remove browser URL bars if they expose secret query parameters

## 13. NETWORK / EXTERNAL ACTION POLICY

V1 should minimize external dependencies.

Allowed external calls:
- AMD-hosted model inference needed for the hackathon
- deployment/runtime services explicitly approved for the demo

Not allowed by default:
- unsolicited outbound webhooks
- real customer messaging
- real payment APIs
- real courier mutation APIs
- real merchant admin actions
- arbitrary URL fetch from model output

Any new external integration requires a security/cost review before implementation.

## 14. INPUT VALIDATION MINIMUM

Numeric fields:
- finite
- bounded
- non-negative unless explicitly defined otherwise
- correct units/currency assumptions

Enums:
- exact allowlist

Text:
- bounded length
- normalized safely
- treated as untrusted

Identifiers:
- synthetic
- expected format
- no path traversal semantics

Files, if introduced later:
- type allowlist
- size bound
- no executable uploads
- no direct trust of filename/content type

## 15. FINANCIAL SAFETY

The deterministic engine must:
- show formulas/assumptions
- avoid hidden AI-generated financial values
- handle division by zero
- handle no-eligible-route state
- handle missing cost data explicitly
- avoid presenting uncertain inputs as precise facts

The demo must not claim guaranteed revenue recovery.

Preferred language:
- expected recovery value
- estimated uplift under stated assumptions
- simulated result on synthetic cases

Avoid:
- guaranteed savings
- guaranteed margin improvement
- guaranteed recovery

## 16. MODEL / PROMPT SAFETY

Prompts must not contain:
- secrets
- hidden merchant credentials
- real customer PII
- unnecessary account metadata

Model response should be constrained to:
- explanation
- structured extraction
- bounded message drafting

The model must not be given tools that can:
- pay
- refund
- deploy
- delete cloud resources
- modify GitHub
- message real customers
- mutate merchant systems

unless a later gate explicitly authorizes and isolates such capability.

## 17. DEMO SAFETY

Before recording or live judging:
- use synthetic cases only
- verify no secret in browser tabs
- close unrelated private tabs if screen sharing
- hide account profile menus
- ensure terminal history does not expose tokens
- ensure `.env` is not shown
- use sanitized logs
- prove AMD workload without exposing credentials
- test fallback before demo

## 18. SECURITY TESTS REQUIRED LATER

Minimum future test set:
- secret scan
- `.env` ignore verification
- invalid numeric input
- unknown enum
- oversized free text
- prompt-injection case
- malformed AI JSON
- AI financial-value contradiction
- AI timeout
- AI service unavailable
- no eligible route
- division-by-zero uplift
- dependency audit
- production build
- synthetic-data-only verification

Exact commands are frozen in G6.

## 19. HARD STOP CONDITIONS

STOP immediately if any of the following occurs:
1. Payment/card requirement appears.
2. Credit balance is unclear before GPU launch.
3. Secret/token appears in repository or logs.
4. Real customer PII enters demo data.
5. AI output can overwrite deterministic financial truth.
6. AI can trigger an external consequential action without human approval.
7. Dependency introduces unresolved critical vulnerability.
8. Official hackathon rule changes invalidate current architecture/scope.
9. AMD workload cannot be proved as meaningful.
10. Unplanned cloud cost begins accumulating.
11. A public screenshot/log exposes private account data.
12. Any implementation begins before the Control Room authorizes post-kickoff build.

## 20. RELEASE BLOCKERS

G6 cannot PASS while any remains:
- known secret exposure
- unresolved critical/high dependency issue with realistic exploit path
- missing input validation
- missing AI output validation
- no AI timeout/fallback
- no deterministic-vs-AI authority separation
- real PII in demo
- unclear GPU cost behavior
- uncontrolled external action
- missing AMD proof
- unreviewed public evidence containing sensitive data

## 21. COST LEDGER REQUIREMENT

Once GPU usage begins, maintain a simple ledger:
- date/time started
- resource type
- hourly price
- starting credit balance
- stop/delete time
- estimated spend
- remaining credit
- purpose/test performed

This may live in test/evidence documentation; no billing secrets should be stored.

## 22. SECURITY OWNERSHIP

Control Room rule:
- User executes account/payment-sensitive clicks.
- ChatGPT may inspect non-secret state and guide.
- No password/OTP/token should be pasted into chat.
- Any ambiguous cost/security screen must be inspected before proceeding.

## 23. ACCEPTANCE TEST

This guardrail file is effective only if the implementation later satisfies:
1. No secrets in Git.
2. No real customer PII required.
3. AI cannot control financial truth.
4. AI cannot execute consequential actions.
5. Deterministic path works if AI fails.
6. GPU usage is bounded and explicitly cost-audited.
7. Payment cannot be triggered accidentally.
8. Logs are useful and sanitized.
9. External integrations are minimized.
10. Demo evidence can be shared publicly without leaking private data.

## NEXT SAFE ACTION
Create `05_TEST_EVIDENCE_PLAN.md` defining the future gate-by-gate verification matrix, deterministic test cases, AMD proof evidence, security checks, demo evidence, and pass/fail criteria — without writing implementation code.
