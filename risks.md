# AI-Driven Programmatic HCP Marketing — Scope, Market, and Risk

**Author:** Nik Bear Brown

*Tik TOC Phase 4: Scope, Market, and Risk.*

---

## Differentiation Statements

1. **Research-to-product, not AI hype:** The book teaches Fellows how to turn current AI research into product-relevant experiments, not how to repeat vendor claims.
2. **Brand and activation together:** It connects campaign lift to brand formation: quality association, patient archetype ownership, prescriber loyalty, and share of mind.
3. **Model choice under pharma constraints:** It explains why ensembles often beat neural architectures for tabular HCP prediction while still identifying where MoE, routing, LLMs, and uplift models may matter.
4. **External innovation lab framing:** It defines a repeatable operating model for Fellows who scout, test, and hand off promising ideas to company product teams.
5. **Patient-welfare accountability:** It keeps the measurement gap visible: commercial KPIs are not the same as clinical value.

## Comparable Texts Analysis

### Comparable Text 1

- **Title / Author / Publisher / Year:** Modern Healthcare Marketing in the Digital Era / Kakhaber Djakeli / IGI Global / 2024.
- **Target reader and deployment context:** Healthcare marketing students and practitioners.
- **Why choose it over this book:** Broader overview of healthcare marketing.
- **Why choose this book over it:** This book is narrower and more operational: AI-driven HCP marketing, measurement, model evaluation, and Fellow research projects.

### Comparable Text 2

- **Title / Author / Publisher / Year:** General pharmaceutical marketing textbooks and industry handbooks.
- **Target reader and deployment context:** Pharma marketing courses and commercial teams.
- **Why choose it over this book:** More complete coverage of traditional pharma brand planning and regulation.
- **Why choose this book over it:** This book addresses the current AI targeting stack, NPI-level programmatic marketing, point-of-care platforms, model architecture, and incrementality.

### Comparable Text 3

- **Title / Author / Publisher / Year:** Marketing analytics and machine learning textbooks.
- **Target reader and deployment context:** Analytics courses, MBA/MSBA programs, data science teams.
- **Why choose it over this book:** Stronger mathematical coverage of general modeling.
- **Why choose this book over it:** This book explains how modeling choices behave inside pharma-specific data, regulation, measurement, and brand-equity constraints.

## Market Size Estimate

- **Courses/programs that could adopt:** Professional pharma marketing analytics programs, health AI seminars, health communication courses, commercial innovation fellowships, and company internal academies.
- **Copies per adoption:** 10-40 for internal Fellow cohorts; 20-80 for graduate/professional course use.
- **Primary or supplementary text:** Primary for a Fellow lab or short professional course; supplementary for broader healthcare marketing, pharmaceutical policy, or analytics courses.

## Feature List with Priority Tags

| Feature | Priority | Outcome served | Production effort | Producer | Dependency |
|---|---|---|---|---|---|
| Fellow research brief template | Must have | Product handoff | Low | Author | Chapters 10-12 |
| KPI stack diagrams | Must have | Measurement literacy | Medium | Author/graphics | Chapters 2 and 8 |
| MoE vs ensemble comparison figure | Must have | Model judgment | Medium | Author/graphics | Chapters 5-6 |
| Uplift experiment worksheet | Must have | Incrementality design | Medium | Author | Chapter 7 |
| Brand association survey instrument | Must have | Branding research | Medium | Author | Chapter 8 |
| Vendor claim audit rubric | Should have | Evidence quality | Low | Author | Chapters 4 and 10 |
| Patient-centered KPI checklist | Should have | Welfare alignment | Low | Author | Chapters 8 and 12 |
| Synthetic data exercise | Could have | Hands-on modeling | High | Data/engineering | Chapters 5-7 |
| D3 visualizations | Could have | Teaching clarity | Medium | Author/graphics | All chapters |

## Out of Scope

| Topic | Reason for exclusion | Reopen condition | Acknowledge in preface? |
|---|---|---|---|
| Full MLOps implementation | Too far from Fellow research/product-brief purpose | If book becomes technical lab manual | Yes |
| Comprehensive FDA promotional law | Would require a separate legal text | If regulatory reviewers are primary audience | Yes |
| Deep therapeutic-area clinical guidance | The book teaches method across categories | If a therapy-area edition is planned | Yes |
| Full statistics textbook treatment of causal inference | The reader needs usable experiment design | If adopted in an analytics degree course | Yes |
| Vendor-by-vendor buyer guide | Ages quickly and risks becoming a market report | If updated annually | Yes |

## Adoption Risk Register

| Risk | Category | Likelihood | Impact | Trigger | Mitigation | Contingency |
|---|---|---|---|---|---|---|
| Book becomes a topic survey instead of a lab handbook | Pedagogy | Medium | High | Chapters describe ideas but do not produce Fellow artifacts | Every chapter must end with a research or product artifact | Cut or rewrite chapters without artifact output |
| Too technical for marketing readers | Market | Medium | Medium | MoE/uplift chapters over-index on math | Use concrete pharma cases before equations | Move math depth into appendices |
| Too light for data science readers | Market | Medium | Medium | Model chapters lack evaluation rigor | Include baseline, leakage, validation, and kill criteria | Add optional technical notes |
| Vendor claims age quickly | Aging | High | Medium | Named platform features change | Treat vendors as examples, not the backbone | Annual update note or web companion |
| Compliance risk is underplayed | Regulatory | Medium | High | Research projects ignore MLR/fair balance/privacy | Add compliance pre-screen to every handoff | Require MLR review gate in Chapter 12 |
| Patient-welfare critique feels bolted on | Ethical | Medium | High | Patient outcomes appear only at the end | Add patient-centered question to every research brief | Build final checklist into all project templates |
| MoE chapter overpromises relevance | Evidence | Medium | Medium | Readers infer MoE is superior for tabular HCP data | State ensemble baseline clearly | Require MoE justification test |

## Top 3 Adoption Risks

1. **Unclear book type:** It must stay a practitioner handbook with course structure. If it tries to be a full textbook, vendor report, and ML manual at once, it loses adoption clarity.
2. **Evidence overclaiming:** The book must distinguish independent evidence, vendor-generated metrics, plausible hypotheses, and untested product ideas.
3. **Weak product handoff discipline:** The Fellow-lab premise only works if the reader learns how to decide what should be killed, piloted, or handed to product.

## Research Lanes for Fellows

| Lane | Core question | Marketing KPI | Branding KPI | Likely product owner |
|---|---|---|---|---|
| MoE vs ensemble benchmark | Does routing improve any HCP prediction task beyond gradient boosting? | Lift, NBRx, audience precision | Segment-specific message fit | Data science |
| Uplift modeling | Which HCPs change because of an intervention? | Incremental scripts, cost per incremental start | Durable prescriber movement | Measurement/analytics |
| Brand association measurement | Does content change perceived quality or patient-type association? | Downstream NBRx by exposed segment | Quality association, share of mind | Brand strategy |
| LLM research assistant | Can LLMs accelerate evidence scanning and claims mapping without hallucination? | MLR cycle support, content throughput | Message consistency | Product/content ops |
| HCP journey simulation | Can simulated journey states improve next-best action timing? | Engagement, conversion, retention | Patient archetype ownership | NBA/product |
| EHR-message ethics audit | Does point-of-care messaging create safety, cognitive-load, or trainee risks? | Usable clinical-moment engagement | Trust and credibility | Compliance/product |
| Patient-centered measurement pilot | Can brand optimization include appropriateness and outcomes checks? | Quality-adjusted starts | Trust, reputation, value story | Medical/commercial strategy |
