# AI-Driven Programmatic HCP Marketing — Learning Architecture

**Author:** Nik Bear Brown

*Tik TOC Phase 2: Learning Architecture.*

---

## Sequencing Model and Justification

**Primary model:** Problem -> Solution with a spiral return to measurement.

The reader first learns the commercial system, then the measurement problem, then the data infrastructure, then the model toolkit, then the innovation-lab workflow. This order matters because model sophistication is meaningless until the learner knows which pharma KPI is being moved and which risk surface is being activated.

**Most likely breakdown chapter:** Chapter 6, because MoE is conceptually attractive but easy to confuse with ordinary stacked models. The chapter must be concrete and comparative, not model-worship.

**Transition chapter:** Chapter 7, because uplift modeling moves the book from predictive targeting to causal commercial experimentation.

## Three-Act Learning Arc

**Act One — Establish the machine:** Chapters 1-4 teach the commercial system, measurement stack, data infrastructure, and deployed AI landscape.

**Act Two — Build the toolkit:** Chapters 5-9 teach the model and measurement methods Fellows can use to evaluate new research ideas.

**Act Three — Apply through the lab:** Chapters 10-12 teach the external innovation-lab process, project portfolio, and product handoff criteria.

**Arc statement:** The reader moves from "I can describe pharma AI marketing" to "I can design, evaluate, and hand off a research-backed product opportunity."

## Learning Outcomes

| Chapter | Bloom's level | Learning outcome |
|---|---|---|
| 1. The Pharma Marketing Machine | Understand / Analyze | Map the actors, incentives, channels, and ethical tensions in pharma marketing. |
| 2. From Campaign Lift to Brand Equity | Analyze | Distinguish activation metrics from brand-equity metrics and choose the right KPI for a research question. |
| 3. The HCP Identity Graph | Analyze / Apply | Explain how NPI, claims, CRM, EHR, and media signals become targeting infrastructure. |
| 4. What the Current AI Stack Actually Does | Analyze | Separate deployed AI capabilities from vendor positioning and identify evidence gaps. |
| 5. Ensembles, Boosting, and the Tabular Data Advantage | Apply | Choose appropriate baseline models for structured HCP prediction tasks. |
| 6. Mixture of Experts and Related Routing Models | Analyze / Evaluate | Evaluate whether MoE or routing architectures are technically appropriate for a pharma marketing problem. |
| 7. Uplift Modeling and Incrementality | Apply / Evaluate | Design an experiment or quasi-experiment that estimates incremental effect rather than propensity. |
| 8. Brand Association as a Measurable Outcome | Create | Design a study that tests whether content changes brand association, quality perception, or patient-archetype ownership. |
| 9. LLMs for Commercial Research and Content Intelligence | Apply / Evaluate | Use LLMs to assist research while detecting bias, hallucination, weak evaluation, and compliance risk. |
| 10. The External Innovation Lab Operating Model | Create | Build a Fellow workflow from research scan to product opportunity memo. |
| 11. Fellow Research Portfolio | Create | Select and scope a research project that could plausibly justify company investment. |
| 12. From Prototype to Product Decision | Evaluate / Create | Decide whether a prototype should be killed, studied further, piloted, or handed to product. |

## Outcome Map

| Chapter | Assessable? | Maps to course/practitioner need? | Primary artifact |
|---|---|---|---|
| 1 | Yes | Yes | Pharma commercial system map |
| 2 | Yes | Yes | KPI stack and metric-choice memo |
| 3 | Yes | Yes | HCP identity graph diagram |
| 4 | Yes | Yes | AI stack evidence audit |
| 5 | Yes | Yes | Baseline model recommendation |
| 6 | Yes | Yes | MoE-vs-ensemble architecture brief |
| 7 | Yes | Yes | Uplift / incrementality test design |
| 8 | Yes | Yes | Brand association measurement plan |
| 9 | Yes | Yes | LLM research workflow and risk audit |
| 10 | Yes | Yes | Innovation-lab operating protocol |
| 11 | Yes | Yes | Fellow project proposal |
| 12 | Yes | Yes | Product handoff or kill memo |

## Prerequisite Dependency Map

| Chapter | Depends on |
|---|---|
| 1 | Basic understanding that pharma marketing is regulated and data-driven |
| 2 | Chapter 1 |
| 3 | Chapters 1-2 |
| 4 | Chapters 1-3 |
| 5 | Chapters 2-3; basic ML vocabulary |
| 6 | Chapter 5 |
| 7 | Chapters 2-5 |
| 8 | Chapters 2 and 7 |
| 9 | Chapters 2, 4, and 8 |
| 10 | Chapters 1-9 |
| 11 | Chapters 5-10 |
| 12 | Chapters 10-11 |

**Broken sequences:** Do not teach MoE before ensembles; the reader needs the tabular baseline before evaluating whether a complex routing architecture earns its keep. Do not teach uplift before campaign and brand metrics; causal lift requires knowing what outcome is being incremented.

**Load-bearing chapters:** 2, 5, 7, 10, and 12. If these fail, the book becomes a topic survey instead of an innovation-lab handbook.
