# RECLAIMGRID AI — TRACK FIT, PIVOT KILL TEST & PARTNER-PRIZE AUDIT

## CONTROL
- PROJECT: ReclaimGrid AI
- CONTROL CODE: RG-ACT3
- FILE: 21_TRACK_FIT_AND_PIVOT_AUDIT.md
- DATE: 2026-10-07
- STATUS: PRE-KICKOFF STRATEGY AUDIT
- PURPOSE: Decide whether ReclaimGrid should remain Track 3, whether a pivot is justified, and whether partner-prize integrations are worth the build risk.

## EXECUTIVE DECISION

Primary strategy remains:
**Track 3 — Reinvent Commerce**

No pivot is recommended.

Partner technology should be added only after the core product is stable and only if the integration:
- is low-risk,
- reuses the AMD endpoint,
- does not change the hero story,
- and creates a real second-prize opportunity.

Main prize remains the priority.

---

# 1. TRACK 3 FIT

Official Track 3 asks for:
- a real merchant/customer problem,
- customer/business data -> useful recommendation/action,
- measurable effect on revenue, margin, conversion, retention, inventory, or service quality,
- transparent prediction logic rather than LLM-only forecasting.

ReclaimGrid maps strongly:
- merchant problem: value leakage after failed delivery/return,
- business data: operational notes + item economics + policy + recovery/inventory assumptions,
- useful commercial action: ACT NOW / ASK FIRST / HUMAN REVIEW,
- measurable effect: EFRC / opportunity cost avoided / Decision Exposure,
- deterministic prediction/decision math,
- AMD model is a bounded evidence interpreter.

Official source:
https://lablab.ai/ai-hackathons/amd-developer-hackathon-act-iii

## Fit verdict
**STRONG**

---

# 2. TRACK 1 — INTELLIGENT INDUSTRY

Could ReclaimGrid be reframed around warehouse/reverse-logistics operations?

Possibly.

But Track 1 specifically emphasizes factories/manufacturers:
- machines
- sensors
- quality
- maintenance
- safety
- production efficiency

A warehouse-return decision product would be a weaker narrative fit than Track 3.

Verdict:
**NO PIVOT**

---

# 3. TRACK 2 — HEALTH & WELLBEING

No fit without replacing the core problem.

Verdict:
**REJECT**

---

# 4. TRACK 4 — NEW EXPERIENCE

ReclaimGrid is a business decision system, not a generative media/experience product.

Verdict:
**REJECT**

---

# 5. PIVOT TOURNAMENT

The following alternatives were challenged against:
- official fit,
- originality,
- business value,
- AMD meaningfulness,
- data feasibility,
- solo-build feasibility,
- demo clarity.

## Candidate A — ReclaimGrid Recovery Decision Certificate
Strengths:
- strong Track 3 fit
- direct margin/recovery economics
- reproducible synthetic data
- clear deterministic/AI split
- strong uncertainty story
- measurable proof
- bounded scope

Risk:
- crowded adjacent returns market

Mitigation:
Recovery Decision Certificate + Decision Hinge + Decision Exposure + RecoveryBench.

Verdict:
**KEEP**

## Candidate B — Generic NDR Autopilot
Problem:
AfterShip, ClickPost, Narvar overlap heavily.

Verdict:
**KILL**

## Candidate C — Return Disposition AI
Problem:
Optoro, ReverseLogix, McKinsey-described market direction overlap heavily.

Verdict:
**KILL**

## Candidate D — Return Fraud Classifier
Potential business value is high.

But:
- strong competitors exist,
- realistic labeled fraud data is hard,
- false-positive claims become difficult to defend,
- merchant risk/fairness complexity rises.

Verdict:
**KILL FOR THIS HACKATHON**

## Candidate E — Dynamic Personalized Return Policy
Interesting:
customer history + CLTV + product economics -> dynamic terms.

But:
- requires credible behavior/CLTV estimates,
- fairness/customer-experience risks,
- harder synthetic evaluation,
- weakens simple hero story.

Verdict:
**DEFER AS FUTURE PRODUCT EXTENSION**

## Candidate F — Demand / Inventory Planner
Official Track 3 example.

But:
- needs realistic time series,
- forecasting evaluation is more complex,
- crowded market,
- less unique judge artifact.

Verdict:
**KILL**

## Candidate G — Evolus Returns Agent
Could qualify for partner prize.

But as a main concept:
- pushes toward generic workflow automation,
- adds mandatory Evolus integration,
- risks distracting from Recovery Decision Certificate.

Verdict:
**NOT PRIMARY**

---

# 6. GOOGLE PARTNER PRIZE

Current official page says:
- Google technologies are optional,
- eligible use may qualify for Google prize,
- current page shows a $5,000 Google prize.

But detailed Google qualification requirements are not clearly published in the currently reviewed page content.

Control rule:
**Do not add Google technology solely for prize eligibility until exact requirements are published/verified at kickoff.**

Potential low-risk path if allowed:
- use an eligible Google open model as the AMD-hosted Case Interpreter only if it also wins RecoveryBench.

Never select a worse model just for a partner badge.

---

# 7. EVOLUS PARTNER PRIZE

Current event page says Evolus track requires:
- free event workspace,
- own open model served on AMD through vLLM,
- at least two Evolus building blocks,
- app drives Evolus via APIs,
- event code at kickoff,
- workspace includes 50,000 platform credits and no credit card.

This is technically compatible with ReclaimGrid because we already plan:
- AMD-hosted open model,
- vLLM,
- human handoff.

Possible late-stage partner extension:
**ASK FIRST workflow**

Example:
- Recovery Decision Certificate emits ASK_FIRST,
- Evolus workflow drafts/structures the evidence-request process,
- human receives response,
- case returns to ReclaimGrid.

But this must be treated as optional.

## Evolus entry condition
Only consider after:
- G5 core integration PASS,
- no main-prize blocker,
- at least one full day remains before internal build freeze,
- integration can be completed without changing canonical economics.

Verdict:
**OPTIONAL LATE-STAGE PARTNER EXTENSION**

---

# 8. VIBE GENERATION SPECIAL PRIZE

Current official page lists a Vibe Generation special prize with judging themes:
- strategic thinking / quantified value / commercial attitude,
- technical execution / orchestration / ability to ship,
- taste / originality / human+AI workflow.

ReclaimGrid naturally maps well:
- quantified economic value,
- deterministic + AMD AI orchestration,
- human approval and Next Best Evidence,
- distinct judge UI.

No extra Vibe-specific technology requirement is currently stated in the reviewed page.

Control rule:
Optimize the core product naturally for these qualities.
Do not add extra features just for the special prize.

---

# 9. STRATEGIC PRIORITY ORDER

1. Main AMD prize / Track 3 quality
2. Vibe special prize through the same core product
3. Google partner prize only if requirements and model fit align naturally
4. Evolus partner prize only after core PASS and sufficient time remains

No partner prize may weaken the main submission.

---

# 10. FINAL PIVOT RULE

Do not pivot from ReclaimGrid unless one of these occurs at kickoff:
- Track 3 is removed/materially changed,
- official rules make the product noncompliant,
- AMD technical constraints make the core AI workload infeasible,
- a demonstrably stronger concept is found with lower execution risk and substantially higher judge fit.

Absent one of these:
**NO PIVOT.**

## NEXT SAFE ACTION
Keep ReclaimGrid as Track 3 provisional default. Recheck partner requirements at kickoff, but do not integrate partner technology before the core is stable.
