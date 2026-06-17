# AI-Driven Programmatic HCP Marketing — Chapter Specifications

**Author:** Nik Bear Brown

*Tik TOC Phase 3: Chapter Specifications.*

---

## Chapter 1 — The Pharma Marketing Machine

**Capability built:** Map the actors, incentives, channels, and data flows that make pharma marketing different from ordinary consumer marketing.

**Opening problem:** A Fellow sees a vendor claim of 25% script lift from point-of-care targeting. What system produced that number, who benefits, and what is missing from the claim?

**Core blocks:** detailing and DTC; HCP vs patient vs payer decision-making; commercial incentives; POC and EHR messaging; evidence-quality hierarchy.

**Exercises:** Draw the pharma commercial ecosystem; identify the incentive of each actor; classify a campaign claim as commercial, clinical, or evidentiary.

## Chapter 2 — From Campaign Lift to Brand Equity

**Capability built:** Choose the right KPI for a marketing or branding research question.

**Opening problem:** A campaign shows lift, but the brand is losing new starts. Did the campaign help?

**Core blocks:** TRx, NRx, NBRx/NBx; script lift and incrementality; prescriber loyalty deciles; share of voice; share of mind; brand association and quality perception.

**Exercises:** Build a KPI stack for a launch brand; distinguish activation from brand formation; write a measurement plan for "quality association with a label."

## Chapter 3 — The HCP Identity Graph

**Capability built:** Explain how data becomes NPI-level targeting and measurement infrastructure.

**Opening problem:** A brand wants to target cardiologists likely to see eligible patients in the next 60 days. What signals can be used, and what are their limits?

**Core blocks:** NPI and physician master data; claims and prescription feeds; CRM activity; endemic media behavior; EHR triggers; claims lag and linkage limits.

**Exercises:** Diagram an HCP identity graph; identify likely data latency; list privacy and bias risks in an NPI audience.

## Chapter 4 — What the Current AI Stack Actually Does

**Capability built:** Separate deployed commercial AI from vendor framing.

**Opening problem:** A platform claims to be an AI operating system for healthcare marketing. What capabilities are real, and what evidence would prove product value?

**Core blocks:** next-best action; predictive audience modeling; trigger-based POC; MLR acceleration; field-force intelligence; omnichannel orchestration; vendor-generated evidence.

**Exercises:** Audit a vendor claim; classify an AI use case by maturity; identify the missing validation study.

## Chapter 5 — Ensembles, Boosting, and the Tabular Data Advantage

**Capability built:** Recommend practical baseline models for structured HCP marketing data.

**Opening problem:** A team wants to replace XGBoost with a neural model because "AI is better now." Should they?

**Core blocks:** bagging, boosting, stacking; gradient-boosted trees; tabular-data benchmarks; propensity models; calibration; feature leakage.

**Exercises:** Choose a model family for NPI propensity scoring; define a leakage check; write a baseline model card.

## Chapter 6 — Mixture of Experts and Related Routing Models

**Capability built:** Evaluate whether MoE, routing, or stacked experts are appropriate for a pharma marketing problem.

**Opening problem:** A vendor says its platform uses Mixture of Experts. Is that a true sparse neural architecture, a stacked ensemble, or just a metaphor?

**Core blocks:** Jacobs-style MoE; sparse routing; Switch/Mixtral/DeepSeek-style modern MoE; expert collapse; load balancing; MoE vs ensemble; tabular-data limits.

**Exercises:** Compare MoE and ensemble architecture; design a routing hypothesis for therapy-area experts; decide whether MoE is justified for a claims-based task.

## Chapter 7 — Uplift Modeling and Incrementality

**Capability built:** Design tests that estimate causal response rather than likelihood to prescribe.

**Opening problem:** The model targets physicians who would have prescribed anyway. How do we find persuadable HCPs?

**Core blocks:** propensity vs uplift; treatment/control logic; heterogeneous treatment effects; holdouts; matched controls; switchers, sleepers, and sure things; measurement circularity.

**Exercises:** Design an uplift test for a digital HCP campaign; define treatment and control groups; write the decision rule for incremental lift.

## Chapter 8 — Brand Association as a Measurable Outcome

**Capability built:** Design research that measures whether content changes brand meaning, not just behavior.

**Opening problem:** A brand wants physicians to associate its label with quality, safety, or a specific patient archetype. How can a Fellow test whether that association changed?

**Core blocks:** HCP brand funnel; aided and unaided recall; brand imagery; patient-type ownership; quality association; survey design; language-model-assisted coding; longitudinal tracking.

**Exercises:** Create a brand association instrument; design a before/after study; write an analysis plan linking association to NBRx or loyalty.

## Chapter 9 — LLMs for Commercial Research and Content Intelligence

**Capability built:** Use LLMs as research assistants and evaluators without confusing generated output with validated evidence.

**Opening problem:** A Fellow wants to use LLMs to scan papers, evaluate claims, and generate message variants. What can be trusted?

**Core blocks:** literature triage; claims-library mapping; content variation; LLM-as-judge limits; marketing creativity evaluation; bias testing; source grounding; MLR risk.

**Exercises:** Build an LLM research workflow; audit a generated claim; compare human expert scoring with LLM scoring.

## Chapter 10 — The External Innovation Lab Operating Model

**Capability built:** Run a Fellow research process that can feed a product roadmap.

**Opening problem:** Fellows find ten interesting papers. Which one becomes a product experiment?

**Core blocks:** research scouting; hypothesis writing; KPI mapping; feasibility scoring; compliance pre-screen; evidence ladder; prototype types; handoff memo.

**Exercises:** Score three research ideas; write a one-page product opportunity brief; build an evidence-to-investment rubric.

## Chapter 11 — Fellow Research Portfolio

**Capability built:** Scope concrete research projects that could justify company resources.

**Opening problem:** The company wants ideas worth resourcing, not academic summaries. What projects should Fellows propose?

**Core blocks:** MoE-vs-ensemble benchmark; uplift model pilot; brand association study; HCP journey simulator; EHR message ethics audit; LLM brand-quality measurement; patient-centered KPI pilot.

**Exercises:** Select a portfolio project; define required data; identify the product owner; state the kill criteria.

## Chapter 12 — From Prototype to Product Decision

**Capability built:** Decide whether a Fellow project should be killed, studied further, piloted, or productized.

**Opening problem:** A prototype improves engagement but not incrementality, and raises compliance concerns. What is the correct decision?

**Core blocks:** product handoff; MLR and legal review; engineering estimate; client pilot design; evidence thresholds; monitoring after deployment; patient-welfare check.

**Exercises:** Write a handoff memo; run a go/no-go decision; design post-launch monitoring for commercial and patient-centered outcomes.

---

## Coverage Gaps

| Topic | Why excluded | Acknowledged in preface? |
|---|---|---|
| Full FDA promotional law | Too large for the book's research-to-product scope | Yes |
| Production ML infrastructure | The reader needs research design and product translation, not MLOps depth | Yes |
| General pharma marketing history | Covered only where needed to understand current AI marketing | Yes |
| Therapeutic-area clinical depth | Projects should adapt to therapy areas; the book teaches method | Yes |

## Hard Chapters

Chapter 6 is the hardest because MoE can become either too technical or too hand-wavy. It should stay anchored in the Fellow question: does this architecture improve a measurable pharma marketing or branding task enough to justify product investment?

Chapter 8 is the second hardest because brand association is less cleanly measured than scripts. It must show how to turn perception, quality association, and patient-archetype ownership into defensible research instruments.

## Aging Risk Audit

Fast-aging material includes named vendors, current spend figures, AI platform features, and model leaderboard claims. Slower-aging material includes the measurement stack, causal-inference logic, ensemble-vs-MoE distinctions, research design, product handoff discipline, and patient-welfare critique.
