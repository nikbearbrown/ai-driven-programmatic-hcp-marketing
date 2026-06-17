# AI-Driven Programmatic HCP Marketing
## Fellows as an External Innovation Lab for Pharma Marketing AI

**Working title:** AI-Driven Programmatic HCP Marketing — Fellows as an External Innovation Lab  
**Series context:** Applied AI, Pharma Marketing, and Human-Centered Commercial Innovation  
**Author:** Nik Bear Brown  
**Document:** Full TOC Draft — compiled from Tik TOC phase outputs  
**Version:** 1.0  
**Status:** Planning draft — chapter manuscript files not yet expanded to match the architecture

---

## Document Structure

1. Book Concept and Thesis
2. Learner Profile
3. Book Type and Deployment Specification
4. Field Positioning
5. Three-Act Learning Arc
6. Prerequisite Map
7. Learning Outcomes by Chapter
8. Chapter-by-Chapter TOC
9. Chapter Anatomy Template
10. Fellow Research Lab Strategy
11. Research Lanes for Fellows
12. Hard Topics, Contested Claims, Aging Risk
13. Market Positioning
14. Feature List
15. Out of Scope
16. Adoption Risk Register
17. Open Questions

---

# PART 1 — BOOK CONCEPT AND THESIS

## Book Concept Summary

> This book teaches **pharma marketing Fellows, analysts, and innovation teams how to turn current AI research into testable product opportunities** for HCP targeting, campaign lift, brand association, and patient-centered measurement. It does this by **mapping the pharma commercial machine, separating activation metrics from brand-equity metrics, teaching the relevant model families, and then giving Fellows a repeatable external innovation-lab workflow**: scout research, translate it into a commercial hypothesis, design a low-cost test, score the evidence, identify compliance and welfare risks, and hand only credible ideas to product teams for resourcing.

**One-sentence logline:**  
Fellows do not ship the product; they reduce uncertainty about which emerging AI ideas deserve product investment.

## Central Thesis

Pharma commercial AI is moving faster than the evidence base around it. Platforms can target HCPs by NPI, trigger messages at the point of care, personalize next-best action, generate content variations, and report script lift. But the hardest questions remain under-tested:

- Which models improve incremental prescribing rather than merely predicting likely prescribing?
- Which interventions build durable brand association rather than short-lived engagement?
- Which architectures, such as Mixture of Experts, are technically useful in HCP marketing rather than merely impressive in vendor language?
- Which commercial optimizations create patient value, and which simply increase branded volume?

The book argues that an external innovation lab can close part of this gap. Fellows are valuable because they sit between academic research, commercial strategy, product management, data science, and medical/legal/regulatory review. Their work is not to make grand claims. Their work is to create disciplined small tests that tell a company whether an idea is worth resourcing.

## Thesis Test

The TOC reflects the thesis at every act:

- **Act One:** The reader learns the commercial system and the measurement stack before any model is introduced. This prevents model-first thinking.
- **Act Two:** The reader learns model families and measurement methods by asking what they can improve: lift, incrementality, quality association, prescriber loyalty, or patient-centered outcomes.
- **Act Three:** The reader learns how Fellows run an innovation lab: research scan, hypothesis, experiment design, evidence ladder, compliance screen, and product handoff.

**Thesis test: PASS**

---

# PART 2 — LEARNER PROFILE

## Primary Reader

A Fellow working with or near a pharma marketing company, health data platform, agency, brand team, or commercial AI vendor. They are asked to watch the research frontier and identify ideas that might improve marketing performance or brand measurement.

**Specific person:** A graduate Fellow embedded with a healthcare marketing AI company for a semester. They understand that the company cares about script lift, HCP engagement, and productizable insights, but they also know that new AI research is noisy, vendor claims are often unverified, and pharma promotion has unusual regulatory and ethical constraints.

## Prior Knowledge Assumed

- Basic pharma vocabulary: brand, indication, HCP, NPI, script, claims, payer, MLR.
- Basic data vocabulary: model, feature, training data, test set, metric, validation, bias.
- Basic marketing vocabulary: targeting, segmentation, campaign, lift, brand, funnel.

## Prior Knowledge Not Assumed

- Deep pharmaceutical law.
- Production ML engineering.
- Advanced causal inference.
- Formal neural-network architecture.
- Full brand-equity research methodology.
- Access to proprietary claims or CRM data.

## Prior Misconceptions

1. **"Script lift is brand growth."**  
   Lift can be short-term activation. Brand growth includes NBRx, loyalty, retention, association, patient-type ownership, and price/access resilience.

2. **"The newest AI architecture is probably better."**  
   For structured HCP prediction, tree-based ensembles are often the baseline to beat. MoE may be useful in some settings, but not because the name sounds advanced.

3. **"MoE means any group of specialized models."**  
   In the research literature, MoE usually means jointly trained experts with a learned routing mechanism and standardized input/output spaces. Many commercial systems are better described as stacked ensembles or routed model portfolios.

4. **"Engagement proves impact."**  
   Opens, clicks, rep response, and content dwell time are not the same as incremental prescribing, durable brand association, or patient benefit.

5. **"Compliance comes after the prototype."**  
   In pharma, compliance risk is part of research design. A commercially clever idea that cannot survive MLR or privacy review is not a product opportunity.

## Motivation Type

Professional and intellectual. The Fellow wants to find ideas that matter, not merely summarize papers. The company wants a filter for deciding what deserves product, data science, or client-pilot resources.

---

# PART 3 — BOOK TYPE AND DEPLOYMENT SPECIFICATION

## Book Type

**Primary type:** Practitioner handbook with course-textbook structure.  
**Secondary type:** Fellowship lab manual.

This is not a reference book. The order matters. The reader must understand the commercial system before judging model architecture, and must understand measurement before proposing innovation.

## Deployment Specification

**Primary deployment context:**

- Pharma marketing innovation fellowships.
- Health AI commercial strategy programs.
- Internal training for HCP marketing platforms.
- Graduate professional seminars in health marketing analytics.
- Company-sponsored external innovation labs.

**Secondary deployment context:**

- Product strategy teams.
- Brand analytics teams.
- Agency innovation groups.
- Commercial data science onboarding.

## What the Book Is Not Designed For

- A general pharmaceutical marketing survey.
- A production MLOps manual.
- A regulatory law textbook.
- A vendor buying guide.
- A pure machine learning textbook.
- A patient advocacy handbook, although patient welfare remains an explicit evaluation criterion.

## How the TOC Signals Book Type

Each chapter produces a practical artifact:

- system map
- KPI stack
- HCP identity graph
- vendor claim audit
- model baseline memo
- MoE-vs-ensemble architecture brief
- uplift test design
- brand association instrument
- LLM research workflow
- innovation-lab operating protocol
- Fellow project proposal
- product handoff or kill memo

The book is therefore teachable as a course, usable as a lab manual, and defensible as a company innovation process.

---

# PART 4 — FIELD POSITIONING

## Positioning Statement

The competitive landscape is fragmented:

- Pharma marketing books explain promotion and brand planning but rarely explain modern AI targeting and model evaluation.
- Machine learning books explain models but rarely understand NPI identity graphs, claims lag, MLR review, payer access, or brand equity in prescription medicine.
- Vendor materials claim performance but often rely on proprietary attribution and non-independent evidence.
- Academic papers provide methods but rarely translate them into product decisions.

This book fills the gap by teaching Fellows to translate research into product-relevant experiments under pharma constraints.

## Comparable Texts

### Modern Healthcare Marketing in the Digital Era

**What it covers:** healthcare marketing, digital channels, contemporary promotional strategy.  
**What it misses:** NPI-level programmatic targeting, AI model evaluation, MoE-vs-ensemble distinctions, uplift experiments, and Fellow handoff workflows.  
**Why choose this book:** it is narrower, sharper, and built around research-to-product action.

### Traditional Pharmaceutical Marketing Texts

**What they cover:** detailing, DTC, brand planning, sales force strategy, regulatory context.  
**What they miss:** modern HCP identity graphs, EHR-triggered advertising, next-best action, LLM content intelligence, and AI measurement claims.  
**Why choose this book:** it treats AI-driven programmatic HCP marketing as the central object, not a late add-on.

### Marketing Analytics and Machine Learning Textbooks

**What they cover:** segmentation, targeting, prediction, experiments, causal inference, marketing measurement.  
**What they miss:** pharma-specific constraints: FDA label, fair balance, MLR, patient privacy, payer access, NPI identity, prescribing data, claims lag, and patient-welfare misalignment.  
**Why choose this book:** it teaches model judgment inside the commercial and ethical machinery of pharma.

## Consolidated Differentiation

This book is the external innovation-lab practicum for pharma commercial AI. It teaches Fellows to ask:

- What is the KPI?
- What is the model idea?
- What is the baseline?
- What is the evidence?
- What is the compliance risk?
- What is the patient-welfare risk?
- What would justify product investment?

---

# PART 5 — THREE-ACT LEARNING ARC

## Arc Statement

The book takes the reader from **interested observer of pharma AI claims** to **Fellow capable of producing a product-relevant research brief** by first establishing the commercial machine, then building the model and measurement toolkit, then applying that toolkit through a structured innovation-lab process.

## Act One — Establish: The Commercial Machine

**Chapters:** 1-4  
**Starting state:** The reader knows pharma marketing is regulated and data-driven but cannot map the full system.  
**Ending state:** The reader can explain how HCP targeting, brand measurement, data infrastructure, and current AI systems fit together.  
**Inciting question:** "When a platform claims AI-driven lift, what exactly was targeted, measured, and proven?"

## Act Two — Build: The Model and Measurement Toolkit

**Chapters:** 5-9  
**Starting state:** The reader can name the system but cannot yet evaluate model choice or measurement quality.  
**Ending state:** The reader can compare ensembles, MoE, uplift models, LLM workflows, and brand association instruments against specific pharma marketing tasks.  
**Hardest conceptual moment:** Chapter 6, because MoE sounds like the obvious advanced model until the tabular-data baseline and routing requirements are made explicit.

## Act Three — Apply: The External Innovation Lab

**Chapters:** 10-12  
**Starting state:** The reader has tools and examples.  
**Ending state:** The reader can run a small innovation-lab cycle and produce a go/no-go product handoff.  
**Transfer test:** The final deliverable is a Fellow research proposal with KPI, method, experiment, evidence threshold, compliance screen, patient-welfare check, and product owner.

---

# PART 6 — PREREQUISITE MAP

| Prerequisite | Safe to assume? | Where addressed |
|---|---|---|
| Pharma marketing channels | Probably | Chapter 1 |
| Brand KPIs | No | Chapter 2 |
| NPI and claims-data targeting | No | Chapter 3 |
| Commercial AI stack | No | Chapter 4 |
| Ensemble learning | No | Chapter 5 |
| MoE architecture | No | Chapter 6 |
| Incrementality/uplift | No | Chapter 7 |
| Brand association research | No | Chapter 8 |
| LLM evaluation | Probably not | Chapter 9 |
| Product handoff discipline | No | Chapters 10-12 |

**Front-loading decision:** The book does not open with AI models. It opens with the commercial system because model choice is meaningless until the learner knows the data, KPI, decision-maker, and risk surface.

---

# PART 7 — LEARNING OUTCOMES BY CHAPTER

| Chapter | Bloom's level | Learning outcome |
|---|---|---|
| 1. The Pharma Marketing Machine | Understand / Analyze | Map actors, incentives, channels, and ethical tensions in pharma marketing. |
| 2. From Campaign Lift to Brand Equity | Analyze | Distinguish activation metrics from brand-equity metrics and choose the right KPI for a research question. |
| 3. The HCP Identity Graph | Analyze / Apply | Explain how NPI, claims, CRM, EHR, and media signals become targeting infrastructure. |
| 4. What the Current AI Stack Actually Does | Analyze | Separate deployed AI capabilities from vendor positioning and identify evidence gaps. |
| 5. Ensembles, Boosting, and the Tabular Data Advantage | Apply | Choose appropriate baseline models for structured HCP prediction tasks. |
| 6. Mixture of Experts and Related Routing Models | Analyze / Evaluate | Evaluate whether MoE or routing architectures are appropriate for a pharma marketing problem. |
| 7. Uplift Modeling and Incrementality | Apply / Evaluate | Design an experiment that estimates incremental effect rather than propensity. |
| 8. Brand Association as a Measurable Outcome | Create | Design a study that tests whether content changes quality perception or patient-archetype ownership. |
| 9. LLMs for Commercial Research and Content Intelligence | Apply / Evaluate | Use LLMs to assist research while detecting bias, hallucination, weak evaluation, and compliance risk. |
| 10. The External Innovation Lab Operating Model | Create | Build a Fellow workflow from research scan to product opportunity memo. |
| 11. Fellow Research Portfolio | Create | Scope a research project that could plausibly justify company investment. |
| 12. From Prototype to Product Decision | Evaluate / Create | Decide whether a prototype should be killed, studied further, piloted, or handed to product. |

---

# PART 8 — CHAPTER-BY-CHAPTER TOC

## ACT ONE — ESTABLISH
*What this act does: gives Fellows the commercial and measurement map they need before touching model choice.*

### CHAPTER 1 — The Pharma Marketing Machine

**One-line:** Fellows learn to map the actors, incentives, channels, and ethical tensions that make pharma marketing different from ordinary marketing.

**Opening:** A point-of-care platform reports strong script lift. The Fellow must ask: who was targeted, what was measured, who benefits, and what is missing?

**Core content:**

- Direct-to-physician detailing.
- DTC demand generation.
- HCP, patient, payer, PBM, and manufacturer incentives.
- EHR and point-of-care messaging.
- Why pharma marketing is both data-rich and morally charged.

**Fellow artifact:** Pharma commercial ecosystem map.

**Bridge:** Once the system is visible, the next question is measurement: what counts as success?

### CHAPTER 2 — From Campaign Lift to Brand Equity

**One-line:** Fellows learn that campaign lift and brand equity are related but not interchangeable.

**Opening:** A campaign improves exposed-HCP scripts, but the brand loses new starts and share of mind. Did the campaign work?

**Core content:**

- TRx, NRx, NBRx/NBx, new patient starts.
- Prescriber loyalty and decile movement.
- Share of voice, share of mind, brand imagery.
- Quality association and patient-type ownership.
- Patient persistence, adherence, switching, and abandonment.

**Fellow artifact:** KPI stack and metric-choice memo.

**Bridge:** To measure any of these outcomes, the system needs a data spine. That spine is the HCP identity graph.

### CHAPTER 3 — The HCP Identity Graph

**One-line:** Fellows learn how NPI-level targeting turns claims, CRM, media, and EHR signals into addressable commercial intelligence.

**Opening:** A brand wants to target cardiologists likely to see eligible patients in the next 60 days. Which signals help, and where can they mislead?

**Core content:**

- NPI as identity primitive.
- Claims and prescription feeds.
- Physician master data.
- CRM engagement and field activity.
- Endemic media behavior.
- EHR triggers and claims lag.
- Privacy, linkage, and bias risks.

**Fellow artifact:** HCP identity graph diagram.

**Bridge:** Once the data infrastructure is clear, the reader can evaluate what the current AI stack actually does with it.

### CHAPTER 4 — What the Current AI Stack Actually Does

**One-line:** Fellows learn to distinguish real deployed capabilities from vendor positioning.

**Opening:** A vendor calls itself an AI operating system for healthcare marketing. What would prove that claim matters?

**Core content:**

- Next-best action.
- Predictive audience modeling.
- Trigger-based point-of-care messaging.
- MLR acceleration.
- Field-force intelligence.
- Omnichannel orchestration.
- Vendor-generated evidence and independent validation gaps.

**Fellow artifact:** Vendor claim audit.

**Bridge:** The first technical question is not "what is the fanciest model?" It is "what baseline must any model beat?"

## ACT TWO — BUILD
*What this act does: gives Fellows the model and measurement tools needed to evaluate research ideas.*

### CHAPTER 5 — Ensembles, Boosting, and the Tabular Data Advantage

**One-line:** Fellows learn why gradient-boosted tree ensembles are the practical baseline for many HCP prediction tasks.

**Opening:** A team wants to replace XGBoost with a neural model because "AI is better now." Should they?

**Core content:**

- Bagging, boosting, and stacking.
- Random forests, XGBoost, LightGBM, CatBoost.
- Why tabular data often favors trees.
- Propensity scoring and calibration.
- Feature leakage and claims-lag traps.
- Baseline discipline.

**Fellow artifact:** Baseline model recommendation.

**Bridge:** With the tabular baseline established, the book can fairly ask what MoE adds and where it does not.

### CHAPTER 6 — Mixture of Experts and Related Routing Models

**One-line:** Fellows learn to evaluate MoE as architecture, not as marketing vocabulary.

**Opening:** A platform says it uses Mixture of Experts. Is it true MoE, a stacked ensemble, a rules router, or a metaphor?

**Core content:**

- Jacobs-style adaptive mixtures.
- Sparse-gated modern MoE.
- Expert routing, shared input/output spaces, and end-to-end training.
- Expert collapse and load balancing.
- Mixtral/DeepSeek-style LLM MoE as reference architecture.
- MoE vs ensembles for tabular commercial data.
- Therapy-area expert routing as a product hypothesis.

**Fellow artifact:** MoE-vs-ensemble architecture brief.

**Bridge:** Architecture still does not answer the causal marketing question: who changed because of the intervention?

### CHAPTER 7 — Uplift Modeling and Incrementality

**One-line:** Fellows learn to move from "who is likely to prescribe?" to "who is persuadable?"

**Opening:** The model targets physicians who would have prescribed anyway. The campaign looks efficient but creates little incremental value.

**Core content:**

- Propensity vs uplift.
- Treatment and control groups.
- Heterogeneous treatment effects.
- Holdouts and matched controls.
- Incremental scripts, incremental starts, and incremental loyalty movement.
- Measurement circularity in vendor-reported lift.

**Fellow artifact:** Uplift experiment design.

**Bridge:** Incrementality measures behavioral movement. Branding also requires measuring whether the meaning of the brand changed.

### CHAPTER 8 — Brand Association as a Measurable Outcome

**One-line:** Fellows learn to test whether AI-driven content changes brand meaning, not just exposure or behavior.

**Opening:** A brand wants physicians to associate its label with quality, safety, or a specific patient archetype. How can that be measured?

**Core content:**

- HCP brand funnel.
- Unaided and aided recall.
- Brand imagery.
- Quality association.
- Patient-type ownership.
- Message recall and confidence.
- Longitudinal brand tracking.
- Linking association to NBRx, loyalty, and retention.

**Fellow artifact:** Brand association instrument and analysis plan.

**Bridge:** LLMs can help scan, code, and generate research material, but they must be treated as tools, not judges of truth.

### CHAPTER 9 — LLMs for Commercial Research and Content Intelligence

**One-line:** Fellows learn how to use LLMs for research acceleration without mistaking generated output for validated evidence.

**Opening:** A Fellow wants to use LLMs to summarize papers, evaluate brand messages, and generate content variants. What can be trusted?

**Core content:**

- Literature triage.
- Claims-library mapping.
- Creative and message variation.
- LLM-as-judge limitations.
- Bias in personalized marketing language.
- Source grounding.
- MLR and fair-balance risk.

**Fellow artifact:** LLM-assisted research workflow and risk audit.

**Bridge:** The toolkit is now built. The final act teaches how to run it as an external innovation lab.

## ACT THREE — APPLY
*What this act does: turns research literacy into a repeatable product opportunity process.*

### CHAPTER 10 — The External Innovation Lab Operating Model

**One-line:** Fellows learn the operating rhythm for turning research into product-relevant tests.

**Opening:** Fellows find ten interesting papers. Which one becomes a product experiment?

**Core content:**

- Research scouting.
- Commercial hypothesis writing.
- KPI mapping.
- Feasibility scoring.
- Evidence ladders.
- Compliance pre-screening.
- Prototype types.
- Product opportunity memos.

**Fellow artifact:** Innovation-lab operating protocol.

**Bridge:** With the workflow defined, Fellows need a portfolio of research lanes that are plausible enough to run.

### CHAPTER 11 — Fellow Research Portfolio

**One-line:** Fellows learn how to scope concrete research projects that could justify company resources.

**Opening:** A company wants ideas worth resourcing, not academic summaries. What projects should Fellows propose?

**Core content:**

- MoE-vs-ensemble benchmark.
- Uplift model pilot.
- Brand association study.
- HCP journey simulator.
- EHR-message ethics audit.
- LLM brand-quality measurement.
- Patient-centered KPI pilot.

**Fellow artifact:** Full Fellow project proposal.

**Bridge:** A project proposal is not enough. The company needs a decision.

### CHAPTER 12 — From Prototype to Product Decision

**One-line:** Fellows learn how to decide whether an idea should be killed, studied further, piloted, or handed to product.

**Opening:** A prototype improves engagement but not incrementality and raises compliance concerns. What is the correct decision?

**Core content:**

- Product handoff.
- MLR and legal review.
- Engineering estimate.
- Client-pilot design.
- Evidence thresholds.
- Post-launch monitoring.
- Patient-welfare check.

**Fellow artifact:** Product handoff or kill memo.

**Terminal deliverable:** A complete research-to-product brief for one Fellow project.

---

# PART 9 — CHAPTER ANATOMY TEMPLATE

Each chapter should follow the same instructional rhythm:

1. **Opening problem:** a concrete pharma marketing situation.
2. **Why the Fellow should care:** the product or measurement decision at stake.
3. **Core concept:** the model, metric, system, or method.
4. **Worked example:** a plausible HCP marketing or brand-measurement scenario.
5. **Evidence check:** what is independent, vendor-generated, hypothetical, or contested.
6. **Compliance and welfare check:** what could go wrong.
7. **Fellow artifact:** the reusable output the chapter trains.
8. **Bridge:** how the artifact prepares the next chapter.

---

# PART 10 — FELLOW RESEARCH LAB STRATEGY

## Lab Premise

The Fellows function as an external innovation lab. Their comparative advantage is disciplined curiosity before product commitment. They can explore ideas that are too early for engineering investment but too promising to ignore.

## The Lab Loop

1. **Scout:** Find current research, platform claims, or emerging methods.
2. **Translate:** Convert the idea into a pharma commercial hypothesis.
3. **Anchor:** Name the KPI: lift, NBRx, loyalty, SOV, association, persistence, appropriateness.
4. **Baseline:** Identify what the method must beat.
5. **Test:** Design a low-cost experiment, benchmark, simulation, or validation study.
6. **Screen:** Identify privacy, MLR, fair-balance, equity, and patient-welfare risks.
7. **Score:** Decide whether evidence supports killing, monitoring, piloting, or handoff.
8. **Handoff:** Write the memo product teams can actually use.

## Evidence Ladder

| Level | Evidence type | Product implication |
|---|---|---|
| 0 | Interesting paper or vendor claim | Watch only |
| 1 | Plausible hypothesis mapped to KPI | Fellow brief |
| 2 | Reproducible benchmark or simulation | Internal discussion |
| 3 | Small offline test against baseline | Product discovery |
| 4 | Prospective pilot or holdout study | Product resourcing |
| 5 | Client-validated incremental impact | Roadmap candidate |
| 6 | Monitored deployment with compliance and patient-welfare checks | Product feature |

---

# PART 11 — RESEARCH LANES FOR FELLOWS

| Lane | Core question | Marketing KPI | Branding KPI | Likely owner |
|---|---|---|---|---|
| MoE vs ensemble benchmark | Does routing improve any HCP prediction task beyond gradient boosting? | Lift, NBRx, audience precision | Segment-specific message fit | Data science |
| Uplift modeling | Which HCPs change because of an intervention? | Incremental scripts, cost per incremental start | Durable prescriber movement | Measurement analytics |
| Brand association measurement | Does content change perceived quality or patient-type association? | Downstream NBRx by exposed segment | Quality association, share of mind | Brand strategy |
| LLM research assistant | Can LLMs accelerate evidence scanning and claims mapping without hallucination? | MLR support, content throughput | Message consistency | Content operations |
| HCP journey simulation | Can simulated journey states improve next-best action timing? | Engagement, conversion, retention | Patient archetype ownership | NBA/product |
| EHR-message ethics audit | Does POC messaging create safety, cognitive-load, or trainee risks? | Usable clinical-moment engagement | Trust and credibility | Compliance/product |
| Patient-centered KPI pilot | Can commercial optimization include appropriateness and outcome checks? | Quality-adjusted starts | Trust, value story | Medical/commercial strategy |

## Example Fellow Project: MoE vs Ensemble Benchmark

**Question:** Does a routed expert model outperform a strong gradient-boosting baseline for HCP next-best-action or NBRx prediction?  
**Baseline:** XGBoost/LightGBM with calibrated probabilities.  
**Candidate method:** Routed model by therapy area, specialty, patient mix, or channel preference.  
**Success threshold:** Meaningful improvement in out-of-time validation, calibration, subgroup robustness, or incremental actionability.  
**Kill criterion:** No lift over tree ensemble, worse calibration, or complexity not justified by business value.  
**Product handoff:** Only if routing produces interpretable segment-specific gains that a product team can operationalize.

## Example Fellow Project: Brand Association Measurement

**Question:** Does AI-personalized content increase association of Brand X with quality, safety, or a specific patient archetype?  
**Method:** Pre/post HCP survey plus blinded message recall and claims-linked downstream behavior where available.  
**Marketing KPI:** Subsequent NBRx or trial among exposed HCPs.  
**Branding KPI:** Change in aided/unaided association, confidence, and patient-type ownership.  
**Risk:** Engagement may increase without belief change; belief may change without clinical appropriateness.  
**Product handoff:** Only if the study design can survive MLR and separates exposure, recall, belief, and prescribing behavior.

---

# PART 12 — HARD TOPICS, CONTESTED CLAIMS, AGING RISK

## Hard Topics

**MoE relevance:**  
The chapter must avoid implying that MoE is automatically superior for HCP marketing. For tabular prediction, ensembles are often the baseline. MoE earns attention only where routing, specialization, multi-task learning, or sequential/contextual data create a real advantage.

**Brand association measurement:**  
Brand meaning is harder to measure than scripts. The book must make brand association concrete through instruments, longitudinal tracking, and linkage to behavior without pretending that survey response equals prescribing loyalty.

**Incrementality:**  
Vendor-reported lift often relies on proprietary methods. The book must teach holdout logic, causal skepticism, and measurement circularity.

**Patient welfare:**  
The book is about pharma marketing, but it must not normalize commercial optimization as the only objective. Every major project should include a patient-welfare check.

## Contested Claims

- AI-driven marketing lift figures are often vendor-generated.
- EHR-integrated advertising has limited independent clinical evaluation.
- LLM-generated marketing evaluation remains weak without human expert review.
- Brand equity can preserve revenue without proving clinical superiority.
- Co-pay and access programs can improve adherence while also reducing generic substitution.

## Aging Risk

Fast-aging material:

- Named vendor features.
- Market-size estimates.
- Platform claims.
- LLM model rankings.
- FDA enforcement posture.

Slow-aging material:

- KPI distinctions.
- NPI/claims logic.
- MoE vs ensemble architecture.
- Incrementality design.
- Brand association measurement.
- Product handoff discipline.
- Patient-welfare critique.

---

# PART 13 — MARKET POSITIONING

## Primary Market

- Pharma commercial innovation fellowships.
- Healthcare AI product strategy programs.
- HCP marketing platform onboarding.
- Graduate/professional courses in health marketing analytics.
- Agency innovation labs.

## Secondary Market

- Brand analytics teams.
- Medical affairs/commercial interface teams.
- Responsible AI programs with healthcare focus.
- Product managers in regulated marketing technology.

## Adoption Argument

The book is adoptable because it gives every learner a concrete output. It is not just a reading text. A 12-week or semester deployment can assign one chapter per week and culminate in a product-ready Fellow brief.

---

# PART 14 — FEATURE LIST

| Feature | Priority | Purpose |
|---|---|---|
| Fellow research brief template | Must have | Standardizes final deliverable |
| KPI stack diagram | Must have | Prevents metric confusion |
| HCP identity graph figure | Must have | Makes data infrastructure visible |
| MoE vs ensemble comparison | Must have | Prevents architecture hype |
| Uplift experiment worksheet | Must have | Teaches incrementality |
| Brand association instrument | Must have | Makes branding measurable |
| Vendor claim audit rubric | Should have | Builds evidence discipline |
| Patient-welfare checklist | Should have | Prevents commercial-only optimization |
| Synthetic data exercises | Could have | Enables hands-on practice without proprietary claims data |
| D3 interactive figures | Could have | Supports teaching and web companion use |

---

# PART 15 — OUT OF SCOPE

| Topic | Reason excluded |
|---|---|
| Full FDA promotional law | Too large; the book teaches research design under constraints, not legal doctrine. |
| Production MLOps | Fellows need evaluation and product handoff, not deployment infrastructure. |
| Therapy-area clinical depth | The method should transfer across categories. |
| Complete causal inference textbook | The book teaches usable incrementality design, not full econometric theory. |
| Vendor-by-vendor buyer guide | Ages too quickly and distracts from method. |

---

# PART 16 — ADOPTION RISK REGISTER

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| Book becomes a topic survey | Medium | High | Every chapter must produce a Fellow artifact. |
| Too technical for marketing readers | Medium | Medium | Open every model chapter with a pharma case. |
| Too light for data science readers | Medium | Medium | Include baselines, validation, leakage, and kill criteria. |
| Vendor examples age quickly | High | Medium | Treat vendors as examples, not structure. |
| Compliance risk is underplayed | Medium | High | Add MLR/privacy/fair-balance screen to every handoff. |
| Patient-welfare critique feels bolted on | Medium | High | Include welfare check in each major project template. |
| MoE chapter overpromises | Medium | Medium | Force comparison against ensemble baseline. |

## Top Three Risks

1. **Unclear book type:** It must remain a practitioner handbook with course structure, not a general survey.
2. **Evidence overclaiming:** The book must distinguish independent research, vendor metrics, plausible hypotheses, and untested ideas.
3. **Weak product handoff discipline:** The Fellow-lab premise works only if the final artifact is useful to product teams.

---

# PART 17 — OPEN QUESTIONS

1. Should the book include a synthetic HCP dataset for exercises, or stay at the research-design level?
2. Should each chapter include a short "company sponsor question" that product teams can answer?
3. Should patient-centered measurement be integrated into every chapter artifact or concentrated in the final chapters?
4. Should the MoE chapter include code-level examples, or remain architecture/product focused?
5. Should the final Fellow brief be designed as a slide deck, memo, or both?

---

# FINAL SHAPE

This is a 12-chapter practitioner handbook for Fellows functioning as an external innovation lab. The book's durable contribution is not that it catalogues AI tools. Its contribution is a disciplined conversion process:

```text
latest research
    -> commercial hypothesis
    -> KPI and baseline
    -> low-cost test
    -> evidence score
    -> compliance and welfare screen
    -> product handoff or kill decision
```

That process is the book.
