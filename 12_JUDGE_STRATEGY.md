# RECLAIMGRID AI — JUDGE STRATEGY & DEMO STORY

## CONTROL
- PROJECT: ReclaimGrid AI
- CONTROL CODE: RG-ACT3
- FILE: 12_JUDGE_STRATEGY.md
- DESIGN DATE: 2026-10-06
- STATUS: PRE-KICKOFF JUDGE-EXPERIENCE DESIGN / NOT IMPLEMENTED
- PURPOSE: Maximize the product's score against the official ACT III judging criteria without bloating V1.

## OFFICIAL JUDGING CRITERIA
Current ACT III event page lists:
1. Application of Technology
2. Presentation
3. Business Value
4. Originality

Official page:
https://lablab.ai/ai-hackathons/amd-developer-hackathon-act-iii

Track 3 specifically rewards:
- real merchant/customer problem
- useful commercial action
- relevant recommendation/personalization
- measurable effect on revenue, margin, conversion, retention, inventory, or service quality
- transparent non-LLM-only forecasting/decision logic where predictions are used

---

# 1. WIN CONDITION

The project should make a judge understand this in under 30 seconds:

> A failed delivery or return creates several possible recovery paths. Most tools automate a step. ReclaimGrid issues a Recovery Decision Certificate: it computes full path economics, shows the exact Decision Hinge where the winner changes, quantifies Decision Exposure, and deterministically gates the case to ACT NOW, ASK FIRST, or HUMAN REVIEW. AMD-hosted AI safely structures messy operational evidence and drafts the targeted evidence request.

Then prove it live.

A podium-level submission should also make the judge see **proof, not promise**:
- RecoveryBench measured results
- adversarial authority-boundary result
- deterministic fixture pass count
- real AMD runtime telemetry
- p50/p95 latency
- sanitized cost/runtime evidence when measured

---

# 2. APPLICATION OF TECHNOLOGY

## Weak version
"AMD hosts an LLM that explains our result."

This risks looking decorative.

## Strong version
AMD-hosted open model performs the **Case Interpreter**:
- messy operational note in
- bounded structured signals out
- exact evidence spans
- deterministic Evidence Status
- explicit unknowns / ambiguity flags

Those accepted signals visibly affect:
- case normalization
- state classification
- policy/eligibility inputs

Then a second AMD inference performs the grounded Decision Explainer.

Judge proof:
- AMD Developer Cloud / Instinct / ROCm runtime evidence
- live/sanitized inference
- app-visible structured extraction
- exact evidence spans + GROUNDED / AMBIGUOUS / INCOMPLETE status
- application-visible explanation
- deterministic fallback if AI fails
- RecoveryBench quality result
- measured latency/runtime evidence

Target judge reaction:
"AMD is central to handling unstructured evidence, but the team designed safe boundaries."

---

# 3. BUSINESS VALUE

Do not pitch "AI efficiency" vaguely.

Show three hard outputs:

## A. Expected Future Recovery Contribution
Winner vs runner-up in one case.

## B. Opportunity Cost Avoided
ReclaimGrid EFRC - static baseline EFRC.

## C. Portfolio synthetic result
Across frozen fixtures:
- baseline total
- ReclaimGrid total
- absolute uplift
- percentage uplift
- changed decisions

Important:
Some cases should have zero uplift because the baseline was already correct. That increases credibility.

Target judge reaction:
"I can see exactly where the money comes from."

---

# 4. ORIGINALITY

Do not claim:
- first returns AI
- first NDR automation
- first disposition optimizer

Those are not defensible.

Demonstrate originality through the combined product behavior:

1. **Recovery Decision Graph**
   Multi-stage downstream value propagation.

2. **Counterfactual path economics**
   Same case, same assumptions, all valid paths compared.

3. **Break-even robustness**
   Shows when the recommendation changes under uncertainty.

4. **Evidence-grounded AMD AI**
   AI extracts evidence; it does not own financial truth.

5. **Decision Hinge / Next Best Evidence**
   A fragile decision reveals the threshold and the specific evidence worth collecting before action.

6. **Decision Ledger**
   Every recommendation is reconstructable and human-governed.

Target judge reaction:
"This is not another chatbot or static return rule engine."

---

# 5. PRESENTATION

## The visual aha moment
A judge should see:

messy note
-> structured AMD evidence
-> recovery graph
-> path values
-> winner
-> break-even line
-> ROBUST/FRAGILE
-> Decision Exposure
-> ACT NOW / ASK FIRST / HUMAN REVIEW
-> Next Best Evidence
-> Recovery Decision Certificate
-> human approval

This is better than a dashboard full of cards.

## Main screen hierarchy
Top:
- Case ID / state / short story

Left:
- Source note + AMD extracted evidence

Center:
- Recovery Decision Graph

Right:
- Winner / runner-up / EFRC / value gap

Bottom:
- break-even / sensitivity visual
- Decision Hinge card
- Decision Exposure
- Action Gate
- Next Best Evidence action
- Recovery Decision Certificate summary
- baseline comparison
- explanation
- approval

Keep one hero screen if possible.

Add a compact **Proof** tab/drawer:
- RecoveryBench
- deterministic core tests
- adversarial escape count
- AMD GPU / ROCm / model / vLLM
- p50/p95 latency
- last audited SHA

The Proof surface should use measured values only.

---

# 6. 90-SECOND DEMO SCRIPT

## 0–12 sec — Problem
"After a failed delivery or return, merchants often optimize the next step instead of the total recovery path. That can leave money behind."

## 12–28 sec — AMD Case Interpreter
Paste/select the synthetic carrier/customer note.
Show AMD extracting:
- customer unavailable
- wants redelivery
- address confirmed
- exact evidence spans
- Evidence Status = GROUNDED / AMBIGUOUS / INCOMPLETE

## 28–50 sec — Recovery Decision Graph
Show:
- RETRY path
- STOP/RTO path
- downstream recovery
- deterministic EFRC calculation

## 50–70 sec — Robustness + Recovery Decision Certificate
Show:
- retry = 46.20
- stop = 35.00
- break-even = 55.6%
- plausible success range crosses threshold
- decision = FRAGILE
- Decision Exposure = calculated from the stated range
- Action Gate = ASK FIRST
- Next Best Evidence = confirm customer availability

Line:
"ReclaimGrid doesn't just say retry. It proves where retry stops being the right decision, how much value is exposed if our assumption is wrong, and whether to act, ask, or hand off."

## 68–80 sec — AMD explanation + approval
Show grounded explanation and AMD-drafted confirmation message based on the deterministic hinge.
Human approves the demo decision.

## 80–90 sec — Business proof
Show frozen synthetic portfolio:
- baseline vs ReclaimGrid
- changed decisions
- opportunity cost avoided

Close:
"AMD understands the messy evidence. Deterministic recovery economics decides the money. Humans stay in control."

---

# 7. 3-MINUTE DEMO EXPANSION

If final video allows around 3 minutes:
- 90-second hero flow
- 30-second open-box secondary case
- 20-second AMD architecture proof
- 20-second failure/fallback
- 20-second market/business result

Do not spend time on:
- login
- settings
- CRUD
- integrations
- generic chatbot conversation

---

# 8. HARD QUESTIONS AND ANSWERS

## "Why not just use an LLM?"
Because the LLM is not trusted with financial truth. It extracts unstructured evidence and explains a deterministic decision package. Path economics and break-even thresholds are reproducible without AI.

## "Is this already what returns platforms do?"
Returns platforms already automate returns, exchanges, NDR recovery, and disposition. ReclaimGrid's hackathon focus is different: multi-stage counterfactual recovery-path economics plus explicit decision robustness and evidence-grounded AI.

## "Where does AMD matter?"
AMD serves the open model that interprets messy carrier/return notes into structured evidence and explains the canonical decision. The live product shows that inference.

## "Are these real customer results?"
No. The evaluation is explicitly synthetic. The business claim is expected value under frozen assumptions, not proven merchant ROI.

## "What happens if AI fails?"
The deterministic recovery graph still works. AI interpretation/explanation enters a visible unavailable/manual-review state.

## "How do you know the recommendation is reliable?"
The product shows the exact formulas and the break-even threshold. It labels a recommendation fragile if the winner changes within the stated plausible assumption range. RecoveryBench reports DEV and locked HOLDOUT quality separately.

## "What if the highest-value path is bad for the customer?"
It never reaches the optimizer if it violates the Policy & Service Feasibility Envelope. Merchant policy, approved customer remedy/SLA, evidence sufficiency, and operational availability are hard constraints before EFRC optimization.

## "Why not put customer lifetime value into the score?"
Because V1 has no defensible CLTV data. We prefer explicit service/customer constraints to fabricated loyalty dollars or hidden weights.

---

# 9. FEATURE SCORECARD

| Feature | Technology | Business Value | Originality | Presentation | Priority |
|---|---:|---:|---:|---:|---|
| Recovery Decision Graph | 3 | 5 | 5 | 5 | MUST |
| Policy & Service Feasibility Envelope | 2 | 5 | 4 | 5 | MUST |
| Deterministic EFRC | 3 | 5 | 4 | 4 | MUST |
| Break-even robustness | 2 | 5 | 5 | 5 | MUST |
| AMD Case Interpreter | 5 | 4 | 4 | 5 | MUST |
| Decision Explainer | 4 | 3 | 2 | 4 | MUST |
| Decision Hinge / Next Best Evidence | 3 | 5 | 5 | 5 | MUST (hero) |
| Decision Exposure / Action Gate | 3 | 5 | 5 | 5 | MUST (hero) |
| Recovery Decision Certificate | 3 | 5 | 5 | 5 | MUST |
| RecoveryBench + Proof surface | 5 | 4 | 4 | 5 | MUST |
| Decision Ledger | 3 | 4 | 4 | 4 | MUST |
| Baseline portfolio evaluation | 2 | 5 | 3 | 4 | MUST |
| Value Leak Map | 2 | 4 | 3 | 4 | SHOULD |
| Multimodal condition AI | 5 | 3 | 2 | 5 | STRETCH |
| Shopify/courier integration | 2 | 3 | 1 | 2 | EXCLUDE |
| Autonomous execution | 3 | 2 | 2 | 2 | EXCLUDE |

Scale is internal planning only: 1 low contribution, 5 high contribution.

---

# 10. SCOPE DEFENSE

When time becomes tight, preserve in this order:
1. deterministic graph/economics
2. hero fixture
3. robustness/break-even
4. Decision Hinge / Next Best Evidence
5. Decision Exposure / Action Gate
6. Recovery Decision Certificate
7. AMD Case Interpreter
8. grounded explanation
9. human approval
10. synthetic baseline evaluation
11. Decision Ledger
12. polish

Kill first:
- portfolio Value Leak Map
- multimodal
- fancy animations
- extra case types
- integrations

---

# 11. FINAL POSITIONING

## Strong primary line
**Find the best recovery path — and prove why it wins.**

## 20-second pitch
ReclaimGrid AI helps ecommerce teams recover more value from failed deliveries and returns. It issues a Recovery Decision Certificate that maps every allowed path, calculates downstream economics, shows the break-even point where the best choice changes, quantifies decision exposure, and gates the case to act now, ask first, or human review. AMD-hosted AI turns messy carrier and return notes into evidence-grounded signals and targeted evidence-request drafts, while deterministic math and human approval keep the financial decision auditable.

## What we are not
- returns portal
- support chatbot
- courier automation suite
- warehouse system
- autonomous refund agent

## What we are
A transparent recovery-path decision layer.

## NEXT SAFE ACTION
Preserve this judge story while waiting for G1. Any future feature proposal must demonstrate that it improves one of the four official judging criteria more than it increases build risk.
