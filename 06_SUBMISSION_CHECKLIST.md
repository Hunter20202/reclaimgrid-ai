# RECLAIMGRID AI — SUBMISSION CHECKLIST

## CONTROL
- PROJECT: ReclaimGrid AI
- CONTROL CODE: RG-ACT3
- FILE: 06_SUBMISSION_CHECKLIST.md
- SNAPSHOT DATE: 2026-10-06
- STATUS: PRE-KICKOFF SUBMISSION PLANNING FREEZE
- CURRENT GATE: G0 — Registration & Environment
- IMPLEMENTATION STATUS: NOT STARTED
- PURPOSE: Define all submission assets, required fields, evidence-to-claim mappings, and final pre-submit validation before any submission content is produced.

## SUBMISSION PRINCIPLE
Every claim in the final submission must be backed by either:
- product behavior,
- deterministic test evidence,
- AMD runtime evidence,
- synthetic dataset results,
- repository documentation,
- or a judge-visible demo artifact.

No unsupported claim is allowed.

## 1. PROJECT IDENTITY

### Canonical name
ReclaimGrid AI

### Canonical one-liner
AMD-powered Recovery Decision Graph that compares economically valid recovery paths after ecommerce delivery failures and returns, then shows which path wins and whether the decision is robust under uncertainty.

### Canonical tagline
Find the best recovery path — and prove why it wins.

### Primary provisional track
Track 3 — Reinvent Commerce

Track remains provisional until G1 rules freeze.

## 2. REQUIRED SUBMISSION ASSETS

Current planned asset set:
- Project title
- Short description
- Long description
- Track/category selection
- Technology tags
- Cover image
- Public GitHub repository
- Working demo/application URL
- Demo/video presentation
- Pitch/slide presentation
- Problem statement
- Intended user
- Architecture explanation
- AMD technology proof
- Business-value proof
- Originality/differentiation statement
- Safety/trust explanation if useful

Final fields must be rechecked from the live submission form before G8.

## 3. PUBLIC REPOSITORY

Current canonical repository:
https://github.com/Hunter20202/reclaimgrid-ai

Final repo checks:
- public access works
- main branch is authoritative
- README is accurate
- license matches final event requirement
- no secrets
- no PII
- no unrelated files
- no broken links
- final tested SHA is recorded
- evidence files are sanitized
- no misleading mock presented as live AMD proof

## 4. WORKING DEMO URL

Must:
- load without account setup if reasonably possible
- open reliably in a judge browser
- have a stable final URL
- show the core workflow immediately
- not depend on hidden local state
- not expose keys/tokens
- have a fallback plan if live AMD inference is unavailable

Final smoke tests:
- fresh/private browser
- desktop viewport
- reload
- direct deep link if used
- AI success path
- AI failure/fallback path

## 5. COVER IMAGE

Goal:
Communicate commerce recovery + decision intelligence + AMD-powered AI quickly.

Must:
- use ReclaimGrid AI name consistently
- be readable at thumbnail size
- avoid unsupported financial claims
- avoid clutter
- avoid logos that violate event/platform rules
- not contain private dashboard/account screenshots

Create only after product UI/brand direction is stable.

## 6. DEMO VIDEO

### Target
Concise judge-first demo.

### Planned sequence
1. Problem: value is lost because recovery decisions are made one step at a time.
2. Show a messy synthetic failed-delivery note.
3. Run AMD-hosted Case Interpreter and show bounded evidence-grounded extraction.
4. Show the Recovery Decision Graph.
5. Show eligible/excluded paths.
6. Show deterministic multi-stage path economics.
7. Show winner, runner-up, and value gap.
8. Show break-even threshold / ROBUST or FRAGILE result.
9. Show grounded AMD explanation.
10. Show explicit human approval.
11. Show baseline-vs-ReclaimGrid aggregate result.
12. Close with AMD proof, business value, and differentiation.

### Video rules
- no passwords/tokens
- no unrelated browser tabs
- no private account information
- no fake "live AMD" claim
- show labels for synthetic data
- keep financial claims tied to stated assumptions

Exact duration must follow final event requirements.

## 7. PITCH / SLIDE PRESENTATION

Recommended minimal deck:

1. ReclaimGrid AI / one-line value
2. The post-purchase recovery problem
3. Why current static/manual rules leave value behind
4. Product workflow
5. Deterministic Recovery Economics Engine
6. AMD AI contribution
7. Example case + transparent math
8. Synthetic dataset business result
9. Architecture + safety/human approval
10. Differentiation / why this is not a generic returns chatbot
11. Market / who benefits
12. Closing / next step

If event limits slide count/time, compress without losing:
- problem
- product
- AMD proof
- measurable value
- originality

## 8. SHORT DESCRIPTION

Final short description must communicate:
- target user/problem
- deterministic economics
- AMD AI contribution
- outcome

Do not finalize wording until G7/G8.

Avoid:
- vague "AI-powered platform"
- guaranteed savings
- broad all-in-one claims
- unsupported production-scale claims

## 9. LONG DESCRIPTION

Must cover:
- problem
- user
- current failure mode
- ReclaimGrid workflow
- deterministic economics
- AMD workload
- human approval
- synthetic demo methodology
- measurable result
- architecture
- security/safety
- limitations
- differentiation

Every quantitative claim must link mentally or explicitly to evidence.

## 10. EVIDENCE-TO-CLAIM MAP

### Claim: "ReclaimGrid compares recovery paths economically."
Evidence required:
- deterministic multi-stage path equations
- graph fixtures
- hand-calculated path tests
- winner/runner-up/value-gap tests
- visible math in product

### Claim: "ReclaimGrid shows when a decision is robust."
Evidence required:
- break-even formula
- sensitivity fixture
- threshold hand-check
- ROBUST/FRAGILE rule
- hero-case UI

### Claim: "ReclaimGrid tells the operator what evidence matters next."
Evidence required:
- deterministic hinge variable
- break-even threshold
- mapping from hinge variable to evidence type
- AMD-drafted message constrained by the hinge
- test proving AI cannot alter the economics

### Claim: "ReclaimGrid knows when to act, ask, or escalate."
Evidence required:
- Decision Exposure formula and fixture
- visible merchant materiality threshold
- deterministic Action Gate rule
- ACT NOW fixture
- ASK FIRST fixture
- HUMAN REVIEW fixture
- test proving model output cannot override Action Gate

### Claim: "ReclaimGrid produces an auditable Recovery Decision Certificate."
Evidence required:
- certificate generated from canonical package
- source evidence spans
- path math
- hinge/break-even
- Decision Exposure
- Action Gate
- human approval
- reconstruction test

### Claim: "AMD powers meaningful AI work."
Evidence required:
- AMD Developer Cloud / AMD Instinct / ROCm runtime proof
- real Case Interpreter inference
- schema-valid extraction
- evidence span/confidence shown in app
- grounded Decision Explainer output
- G2 evidence

### Claim: "The LLM is not the sole financial decision maker."
Evidence required:
- architecture
- deterministic code/tests
- AI-unavailable fallback
- explanation of authority split

### Claim: "ReclaimGrid can improve expected recovered value."
Evidence required:
- synthetic baseline
- synthetic ReclaimGrid result
- formulas
- aggregate uplift
- assumptions disclosed

### Claim: "The workflow is human-governed."
Evidence required:
- approval UI
- no external execution
- architecture/security docs

### Claim: "This is more than a returns chatbot."
Evidence required:
- deterministic economics
- eligibility logic
- route ranking
- measurable baseline comparison
- AMD AI limited to interpretation/explanation/action drafting

## 11. BUSINESS-VALUE CLAIM RULES

Allowed style:
- "On our synthetic evaluation set..."
- "Under the stated assumptions..."
- "Expected recovered value increased by..."
- "The engine changed the baseline route in X of Y cases."

Not allowed without real-world validation:
- guaranteed revenue lift
- proven merchant ROI
- guaranteed margin recovery
- production-scale performance claims
- customer adoption claims
- false integration claims

## 12. ORIGINALITY / DIFFERENTIATION

Final submission should clearly distinguish ReclaimGrid from:
- NDR automation tools
- returns portals
- support chatbots
- generic LLM decision assistants

Canonical differentiation:
**A judge-visible Recovery Decision Certificate combining multi-stage counterfactual path economics, exact Decision Hinge / break-even robustness, bounded Decision Exposure, deterministic act/ask/review gating, Next Best Evidence, evidence-grounded AMD AI, and explicit human approval.**

Do not claim no competitor exists.
Do not claim first-in-world unless independently proven.

## 13. AMD TECHNOLOGY SECTION

Must identify precisely:
- AMD infrastructure used
- AMD accelerator/resource used
- ROCm/serving stack if applicable
- model used
- what exact workload runs there
- why that workload matters to product value

Must not say:
- "built on AMD" if only a trivial test used AMD
- "AMD-powered" without judge-visible proof

## 14. SECURITY / TRUST SECTION

Optional in final copy but required in build:
- synthetic demo data
- deterministic financial authority
- bounded AI
- schema validation
- human approval
- no live consequential actions
- fallback if AI fails

Use this to strengthen credibility, not overwhelm pitch.

## 15. TECHNOLOGY TAGS

Potential tags may include:
- AMD
- ROCm
- AMD Instinct
- vLLM / SGLang if actually used
- open-source LLM model if actually used
- TypeScript / framework actually used

Do not add a technology tag unless it is present in the final working project.

## 16. APPLICATION / REPOSITORY CONSISTENCY

Before submission:
- product name matches everywhere
- tagline matches
- route names match
- metrics match
- architecture matches implemented reality
- model name matches actual runtime
- AMD resource name matches actual evidence
- screenshots match final UI
- README matches live build
- demo video matches final or clearly equivalent build

## 17. FINAL README REQUIREMENTS

README should eventually include:
- what ReclaimGrid is
- problem
- architecture
- deterministic vs AI split
- AMD role
- local/deployment instructions
- environment-variable setup without secrets
- synthetic dataset note
- test commands
- demo flow
- limitations
- license
- evidence references

Do not create implementation instructions before the implementation exists.

## 18. LINK VALIDATION

Before G8 PASS test every final link:
- GitHub repo
- deployed app
- demo video
- slide deck
- any evidence link
- any documentation link

Test:
- logged out where possible
- private/incognito browser
- no permission request
- no broken redirect
- no expired link

## 19. SUBMISSION-FORM AUDIT

Before entering final content:
1. Inspect all required fields.
2. Record field names.
3. Record character limits.
4. Record file-size/type limits.
5. Record video/deck requirements.
6. Record track/category options.
7. Record any license declaration.
8. Record any eligibility declaration.
9. Record any partner-track opt-in.
10. Record final deadline shown in the actual form.

Do not rely on an older rules snapshot for form-specific constraints.

## 20. PRE-SUBMIT VALIDATION

Immediately before submission verify:
- correct team: ReclaimGrid AI
- correct event: AMD Developer Hackathon: ACT III
- correct track
- all mandatory fields complete
- public repo accessible
- app accessible
- video accessible
- deck accessible
- cover image correct
- no placeholder text
- no unsupported claims
- no secret/PII
- AMD proof real and accurate
- synthetic-data disclosure present where appropriate
- final main SHA recorded
- final tests PASS
- no paid GPU unnecessarily running

## 21. FINAL FREEZE RULE

Once G8 PASS is declared:
- stop feature work
- stop cosmetic experimentation
- do not change architecture casually
- only fix submission blockers
- re-run impacted tests after any change
- update final main SHA after every accepted fix

## 22. SUBMISSION CONFIRMATION EVIDENCE

After final submit capture:
- success/confirmation state
- submission URL
- submission time
- final main SHA
- final app URL
- final video/deck references

Avoid capturing private account data.

## 23. POST-SUBMIT RULE

After submission:
- do not alter frozen evidence unless necessary
- do not delete the live demo before judging
- monitor only if required
- if a critical issue appears, verify whether the platform allows an update before changing anything

## 24. CLAIM RED-TEAM

Before final submission, challenge every major claim:
- Can a judge verify it?
- Is it based on synthetic data?
- Is an assumption missing?
- Does the demo actually show it?
- Is AMD's role meaningful?
- Is the LLM being credited for deterministic math?
- Does wording imply production proof we do not have?
- Is the originality claim overstated?

Any weak claim must be rewritten or removed.

## 25. G8 SUBMISSION ASSET PASS CONDITIONS

All must PASS:
- title
- short description
- long description
- track/category
- cover image
- public repo
- working app URL
- demo video
- slide deck
- AMD proof
- business-value evidence
- originality statement
- link audit
- security/privacy audit
- final regression tests
- final main SHA

## NEXT SAFE ACTION
Keep submission content unfrozen until the product is implemented and G7/G8 evidence exists. During pre-kickoff, use this file only to harden claim/evidence mapping.
