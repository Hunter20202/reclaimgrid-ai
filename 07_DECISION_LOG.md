# RECLAIMGRID AI — DECISION LOG

## CONTROL
- PROJECT: ReclaimGrid AI
- CONTROL CODE: RG-ACT3
- FILE: 07_DECISION_LOG.md
- SNAPSHOT DATE: 2026-10-06
- STATUS: ACTIVE / APPEND-ONLY
- PURPOSE: Authoritative record of material project decisions affecting rules, scope, architecture, security, cost, AMD usage, testing, and submission.

## APPEND-ONLY RULE
Do not rewrite history to make past decisions look cleaner.

For every material change:
- add a new decision entry,
- reference the previous decision if superseded,
- record why it changed,
- record affected gate(s),
- record security/cost/demo impact,
- record the commit SHA when available.

A decision may be:
- ACTIVE
- SUPERSEDED
- REJECTED
- DEFERRED
- PROVISIONAL
- FROZEN

---

## D-001 — Product identity
- DATE: 2026-10-06
- STATUS: FROZEN
- DECISION: Product name is **ReclaimGrid AI**.
- REASON: Selected as the working hackathon product for AMD Developer Hackathon: ACT III.
- IMPACTED GATES: G0-G9
- NOTES: Canonical repository name is `reclaimgrid-ai`.

## D-002 — Control Room operating model
- DATE: 2026-10-06
- STATUS: FROZEN
- DECISION: Use a gate-based Control Room workflow with one safe verified action at a time.
- REASON: Reduce execution error, preserve auditability, and keep user actions bounded.
- IMPACTED GATES: G0-G9
- NOTES: No gate advances unless the prior gate is verified PASS.

## D-003 — Primary track
- DATE: 2026-10-06
- STATUS: PROVISIONAL
- DECISION: Primary target is **Track 3 — Reinvent Commerce**.
- REASON: ReclaimGrid converts post-purchase case data into an economically ranked action and aligns with commerce decision support.
- IMPACTED GATES: G1, G7, G8, G9
- REVIEW TRIGGER: Kickoff/rules update or track wording changes.

## D-004 — Core product thesis
- DATE: 2026-10-06
- STATUS: FROZEN
- DECISION: ReclaimGrid is a **post-purchase recovery decision engine**, not a generic returns chatbot or returns portal.
- REASON: Existing failed-delivery/returns automation is crowded; differentiation must come from bounded recovery economics plus AMD-hosted AI interpretation/explanation.
- IMPACTED GATES: G1-G8

## D-005 — Deterministic financial authority
- DATE: 2026-10-06
- STATUS: FROZEN
- DECISION: Recovery-value calculations, route eligibility, and route ranking are deterministic and authoritative.
- REASON: Financial logic must be reproducible, inspectable, and not solely dependent on an LLM.
- IMPACTED GATES: G3-G7
- SECURITY IMPACT: Reduces hallucination/authority risk.

## D-006 — AMD AI responsibility
- DATE: 2026-10-06
- STATUS: FROZEN
- DECISION: AMD-hosted AI is limited to bounded tasks such as free-text interpretation, explanation, tradeoff summarization, and message drafting.
- REASON: AI should add semantic value without becoming the source of financial truth.
- IMPACTED GATES: G2, G4, G5, G7
- NOTES: Final model is not yet selected.

## D-007 — Human approval
- DATE: 2026-10-06
- STATUS: FROZEN
- DECISION: Consequential recovery actions remain human-approved.
- REASON: V1 is decision support, not unrestricted autonomous execution.
- IMPACTED GATES: G4-G7
- SECURITY IMPACT: Blocks model-triggered real refunds, shipping, payments, or inventory mutation.

## D-008 — Synthetic-data default
- DATE: 2026-10-06
- STATUS: FROZEN
- DECISION: V1 uses synthetic ecommerce cases by default.
- REASON: Reproducibility, privacy, lower integration risk, and better test evidence.
- IMPACTED GATES: G3-G8
- SECURITY IMPACT: Avoids real customer PII.

## D-009 — V1 scope restraint
- DATE: 2026-10-06
- STATUS: FROZEN
- DECISION: Exclude full Shopify/WooCommerce integration, real refunds, real courier actions, production multi-tenancy, giant agent systems, training/fine-tuning, and broad ERP/inventory scope.
- REASON: Maximize judge-visible value within hackathon time.
- IMPACTED GATES: G1-G7
- COST IMPACT: Reduces infrastructure and integration cost.

## D-010 — AMD meaningful-workload proof
- DATE: 2026-10-06
- STATUS: FROZEN
- DECISION: Final demo must prove that AMD infrastructure powers a meaningful AI workload inside the product.
- REASON: AMD participation requirement must be demonstrated, not merely mentioned.
- IMPACTED GATES: G2, G6, G7, G8, G9
- EVIDENCE EXPECTED: AMD runtime/resource proof + real inference + application-visible result.

## D-011 — AMD Developer Cloud serving direction
- DATE: 2026-10-06
- STATUS: PROVISIONAL
- DECISION: Candidate serving path is an open model on AMD Developer Cloud / AMD Instinct using ROCm-compatible serving such as vLLM or SGLang.
- REASON: Matches event technology and product workload while avoiding model training.
- IMPACTED GATES: G2, G4
- REVIEW TRIGGER: Actual cloud availability, credit approval, compatibility, latency, or cost.

## D-012 — Hard payment block
- DATE: 2026-10-06
- STATUS: FROZEN
- DECISION: Do not add a payment method or launch paid GPU compute without explicit cost review and authorization.
- REASON: AMD Developer Cloud currently exposes a paid MI300X path while complimentary credit approval is still pending.
- IMPACTED GATES: G0, G2, G6
- COST IMPACT: Prevent accidental spend.
- STOP CONDITION: Any card, billing authorization, deposit, paid quota, or auto-recharge prompt.

## D-013 — Credit state
- DATE: 2026-10-06
- STATUS: ACTIVE
- DECISION: AMD complimentary cloud-credit request is treated as **SUBMITTED / PENDING APPROVAL**, not active credit.
- REASON: Confirmation page acknowledged the request but did not prove usable credit balance.
- IMPACTED GATES: G0, G2
- NEXT REVIEW: Activation/approval email or visible credit balance.

## D-014 — Public GitHub repository
- DATE: 2026-10-06
- STATUS: FROZEN
- DECISION: Canonical project repository is:
  `Hunter20202/reclaimgrid-ai`
- REASON: Public repository is required for project continuity and current submission planning.
- IMPACTED GATES: G0-G9
- SOURCE-OF-TRUTH RULE: Repository state overrides memory/chat summaries when they conflict.

## D-015 — Pre-kickoff implementation guardrail
- DATE: 2026-10-06
- STATUS: ACTIVE
- DECISION: Pre-kickoff work is restricted to research, architecture, documentation, security/cost controls, testing plans, environment/account setup, and submission planning.
- REASON: Current public ACT III pages do not clearly establish unrestricted pre-kickoff submission-code development.
- IMPACTED GATES: G0, G1
- BLOCKED: Product implementation code until rules are re-verified and Control Room authorizes build.

## D-016 — Schedule ambiguity
- DATE: 2026-10-06
- STATUS: ACTIVE
- DECISION: Do not treat the complete build window as finally frozen.
- REASON: Official pages currently conflict:
  - main event page: online build 12–18 October 2026
  - live/dashboard-style text: 12–17 October 2026
  - submission close currently visible as 18 October 2026 at 15:00 UTC
- IMPACTED GATES: G1, G8, G9
- REVIEW TRIGGER: Kickoff and final submission audit.

## D-017 — Minimal architecture
- DATE: 2026-10-06
- STATUS: PROVISIONAL
- DECISION: Prefer a small single-web-app architecture with deterministic domain logic, synthetic local data, and one narrow AMD AI gateway.
- REASON: Reliability, explainability, cost containment, and demo simplicity.
- IMPACTED GATES: G2-G6
- REJECTED BY DEFAULT: Microservices, Kubernetes, vector database, agent framework, workflow engine, large production database.

## D-018 — AI failure must not break economics
- DATE: 2026-10-06
- STATUS: FROZEN
- DECISION: Deterministic recovery ranking must remain usable when AI is unavailable, invalid, or timed out.
- REASON: Core business decision cannot depend on generative-service availability.
- IMPACTED GATES: G3-G7
- TEST REQUIREMENT: AI-offline fallback is mandatory.

## D-019 — Submission claim discipline
- DATE: 2026-10-06
- STATUS: FROZEN
- DECISION: Final quantitative claims must be explicitly tied to synthetic evaluation and stated assumptions unless real-world evidence later exists.
- REASON: Avoid misleading production/ROI claims.
- IMPACTED GATES: G7-G9
- ALLOWED STYLE: "On our synthetic evaluation set..." / "Under the stated assumptions..."

## D-020 — Evidence-before-PASS
- DATE: 2026-10-06
- STATUS: FROZEN
- DECISION: A gate cannot PASS without reproducible evidence and a verified main SHA.
- REASON: Visual confidence alone is insufficient.
- IMPACTED GATES: G0-G9

---

## FUTURE DECISION ENTRY TEMPLATE

### D-XXX — <decision title>
- DATE: YYYY-MM-DD
- STATUS: PROVISIONAL | FROZEN | ACTIVE | SUPERSEDED | REJECTED | DEFERRED
- PREVIOUS DECISION: D-XXX or N/A
- DECISION:
- REASON:
- ALTERNATIVES CONSIDERED:
- IMPACTED GATES:
- SECURITY IMPACT:
- COST IMPACT:
- DEMO/JUDGING IMPACT:
- EVIDENCE:
- MAIN SHA:
- REVIEW TRIGGER:
- NOTES:

## NEXT SAFE ACTION
Create `08_CHANGELOG.md` to record repository/control-system changes chronologically and distinguish document/state changes from decision changes.
