# RECLAIMGRID AI — ACT III RULES SNAPSHOT

## CONTROL
- PROJECT: ReclaimGrid AI
- CONTROL CODE: RG-ACT3
- FILE: 01_RULES_SNAPSHOT.md
- SNAPSHOT DATE: 2026-10-06
- STATUS: VERIFIED PRE-KICKOFF SNAPSHOT
- PURPOSE: Capture only currently verified AMD Developer Hackathon: ACT III facts and explicitly record unresolved inconsistencies before implementation starts.

## PRIMARY SOURCES
1. Official ACT III event page:
   https://lablab.ai/ai-hackathons/amd-developer-hackathon-act-iii
2. Official ACT III live page:
   https://lablab.ai/ai-hackathons/amd-developer-hackathon-act-iii/live
3. AMD AI Developer Program:
   https://developer.amd.com/ai-developer-program/
4. AMD AI Developer Program resources:
   https://developer.amd.com/resources/

## EVENT IDENTITY
- Event: AMD Developer Hackathon: ACT III
- Format: Hybrid
- Online participation is supported.
- On-site phase is in Rome, Milan, and Imperia, Italy.
- User participation mode for RG-ACT3: Online.

## VERIFIED BUILD / SUBMISSION TIMING

### Main event page
- Online build: 12–18 October 2026.
- On-site phase: 17–18 October 2026.
- Event schedule section on the main page currently says: "To be announced."

### Live page
- Kickoff / registration close: 12 October 2026 at 15:00 UTC.
- Submission close: 18 October 2026 at 15:00 UTC.
- Live page summary text also says: "Online Build: 12-17 October 2026."

### SCHEDULE INCONSISTENCY — DO NOT IGNORE
There is an unresolved official-page inconsistency:
- Main event page: online build 12–18 October.
- Live/dashboard-style text: online build 12–17 October.
- Live page submission deadline: 18 October 2026 at 15:00 UTC.

CONTROL RULE:
- Treat 18 October 2026 at 15:00 UTC as the currently visible submission-close milestone.
- Do not freeze the complete build window until kickoff or updated official schedule is re-verified.
- Re-check both official pages immediately before implementation begins and again before submission.

## PARTICIPATION / TEAM RULES
- Registration on the lablab.ai platform and lablab.ai Discord is required for participation.
- AMD AI Developer Program signup is required for approval to this hackathon.
- Previous AI or coding experience is not required.
- Teams consist of 1–6 people.
- A solo participant is therefore allowed through a one-person team.
- RG-ACT3 team mode: Solo / Closed.

## CHALLENGE REQUIREMENT — AMD IS MANDATORY
Every project must run a meaningful part of its workload on AMD infrastructure or AMD hardware.

Officially listed eligible AMD options include:
- AMD Developer Cloud
- AMD Instinct accelerators
- AMD ROCm
- AMD Ryzen AI
- AMD Radeon hardware
- Other approved AMD-powered infrastructure provided during the event

The AMD component must be part of the working product shown to judges.

CONTROL INTERPRETATION FOR RECLAIMGRID:
- A decorative mention of AMD is insufficient.
- The final demo must visibly prove that a meaningful AI workload is actually served or executed on AMD infrastructure.
- Evidence for the AMD path must be captured during G2 and preserved for judging.

## TRACK 3 — REINVENT COMMERCE
Current provisional track for ReclaimGrid AI:
- Track 3: Reinvent Commerce
- Track positioning: help a business understand customers and take better action.

Official demo guidance for Track 3:
- Turn customer or business data into a useful recommendation or action.
- If predicting demand, sales, or customer behaviour, explain how the prediction was calculated.
- A language model must not be the only forecasting method.

Officially stated qualities of strong projects include:
- A real customer or merchant problem
- A useful commercial action
- Relevant recommendations or personalization
- A measurable effect on revenue, margin, conversion, retention, inventory, or service quality

CONTROL FIT:
ReclaimGrid's deterministic Recovery Economics Engine plus AMD-hosted AI interpretation is aligned with this track because financial/scoring math is not delegated solely to an LLM.

TRACK STATUS:
- PROVISIONAL until kickoff/rules freeze.
- Reconfirm Track 3 wording and availability at G1.

## SUBMISSION REQUIREMENTS — CURRENT EVENT PAGE
Current ACT III page lists:

### Project information
- Project title
- Short description
- Long description
- Selected challenge / technology/category tags as applicable

### Presentation
- Cover image
- Demo/video presentation
- Pitch/slide presentation
- Clear explanation of problem and intended user

### App / repository
- Working prototype
- Public GitHub repository
- Demo application platform
- Application URL

RG-ACT3 repository already satisfies the public-repository prerequisite:
- https://github.com/Hunter20202/reclaimgrid-ai

## JUDGING CRITERIA
Current event page lists four core criteria:
1. Application of Technology
2. Presentation
3. Business Value
4. Originality

CONTROL CONSEQUENCE:
Every major feature must map to at least one of these four criteria. Features that do not materially improve technology proof, presentation, business value, or originality are candidates for removal.

## ORIGINALITY / LICENSING / SECRET HANDLING
Current ACT III event page states:
- Submissions must be original.
- Submissions must be MIT-compliant.
- Rules, prizes, and terms may change or be canceled.
- Prize distribution may take up to 90 days.

The event page also explicitly states for the Evolus track that API keys must never be committed and environment variables should be used. RG-ACT3 adopts this as a project-wide security baseline regardless of selected track.

CONTROL RULES:
- No secret, API key, password, token, OAuth state, or private credential may enter the repository.
- Use environment variables and example placeholders only.
- License choice must be checked against the final submission requirement before G8 freeze.

## PRIZES — CURRENTLY VERIFIED
Current official ACT III event page shows:
- Total prize pool: $12,000+
- AMD prizes: $5,000
- Google prizes: $5,000
- Evolus track prizes are also listed.
- Vibe Generation special prize is also listed.

IMPORTANT:
- Partner technologies such as Google and Evolus are optional for the main AMD project unless a partner-track requirement is intentionally selected.
- A project may qualify for the main challenge prize and eligible partner prizes according to the current event page.
- Prize details are volatile and must be rechecked at kickoff and before submission.

## AMD CLOUD CREDIT FACTS
AMD AI Developer Program currently advertises:
- $100 in AMD Developer Cloud credits for members.

AMD's resources page states:
- Complimentary credit is delivered through a unique redemption link after verification.
- Unless the confirmation email states otherwise, AMD Developer Cloud credits expire 30 days after successful account creation/login through the designated redemption link.

RG-ACT3 current status:
- Credit request submitted.
- Approval / activation link pending.
- AMD Developer Cloud account access works.
- A paid MI300X path was visible at $1.99/hour.
- Billing showed ACTION NEEDED.

HARD COST RULE:
- Do not add a payment method.
- Do not create a paid GPU.
- Do not launch GPU compute until complimentary credit is approved, visible, and the billing state is re-audited.
- If any downstream step requires card/payment, STOP and review before proceeding.

## PRE-KICKOFF BUILD POLICY

### What the official event page explicitly allows
Before kickoff, participants are encouraged to browse technologies/tutorials and prepare.

### What is NOT yet proven from the current ACT III pages
The current public pages do not clearly establish in this snapshot whether submission implementation code may be built before kickoff without restriction.

### RG-ACT3 INTERNAL GUARDRAIL
Until kickoff and G1 rules freeze:
ALLOWED:
- Research
- Product planning
- Architecture
- Control documentation
- Security/cost guardrails
- Test planning
- Demo/pitch planning
- Environment/account setup
- Repository/control-file setup

BLOCKED:
- Submission product implementation code
- Paid GPU usage
- Any action that could weaken originality/timing compliance

This is a conservative Control Room policy, not a claim that the official rules explicitly prohibit pre-kickoff coding.

## ELIGIBILITY / GEOGRAPHY STATUS
- Current event page says everyone is welcome regardless of previous AI/coding experience.
- This snapshot does not independently re-verify every country/prize restriction in sponsor/legal terms.
- Geographic/prize eligibility must be re-audited during G1 before rules are frozen.
- Do not make a final prize-eligibility claim from this file alone.

## CURRENT KNOWN OFFICIAL-PAGE INCONSISTENCIES
1. Online build window:
   - Main page: 12–18 Oct
   - Live page summary: 12–17 Oct
2. Main page schedule section:
   - "To be announced"
   - Live page already shows kickoff and submission-close milestones
3. Dynamic event content may change before kickoff.

These inconsistencies are blockers to final rules freeze, not blockers to pre-kickoff planning.

## G1 ENTRY CONDITIONS
Do not mark G1 PASS until all are re-verified after kickoff:
- Final build window
- Final submission deadline
- Final track list and Track 3 wording
- Final judging criteria
- Final submission fields
- Final repository/license requirements
- Final AMD technology requirement
- Final partner-prize rules
- Geographic/prize eligibility
- Any special kickoff-only requirements or event codes
- Whether any implementation timing restriction exists

## NEXT SAFE ACTION
Create `02_PRODUCT_SCOPE.md` to freeze the provisional ReclaimGrid V1 problem, user, inputs, deterministic economics engine, AMD AI role, explicit non-goals, and demo success metrics — without writing implementation code.
