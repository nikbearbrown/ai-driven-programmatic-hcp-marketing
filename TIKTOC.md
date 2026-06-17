# AI-Driven Programmatic HCP Marketing
## Decoding the Prescription: AI, Brand Science, and the Research a Fellow Can Run

**Working title:** AI-Driven Programmatic HCP Marketing — Decoding the Prescription
**Series:** Irreducibly Human / AI+1: What AI Can and Can't Do · Northeastern University College of Engineering
**Author:** Nik Bear Brown · Humanitarians AI (publisher, 501(c)(3)) · with the Humanitarians AI Fellows
**Document:** Full TOC Draft — compiled from all phase outputs, grounded in `pantry/`
**Version:** 1.0
**Status:** Pre-draft — partner-collaboration framing + data access unresolved (see Risk 1, the blocker)

---

## Document structure
1. Book Concept and Thesis
2. Learner Profile
3. Book Type and Deployment Specification
4. Field Positioning
5. Three-Act Learning Arc
6. Prerequisite Map
7. Assessment Structure
8. Chapter-by-Chapter TOC
9. Chapter Anatomy Template
10. Case Study Strategy
11. Hard Topics, Contested Claims, Aging Risk
12. Market Positioning
13. Feature List
14. Out of Scope
15. Adoption Risk Register
16. Open Questions

---

# PART 1 — BOOK CONCEPT AND THESIS

## Book concept summary

> This book teaches **the research-to-product layer of pharma HCP marketing — the judgment a
> Fellow can supply that a model and a vendor deck cannot** — to **data-capable Humanitarians AI
> Fellows working alongside a real pharma marketing-technology partner**, by **running an external
> innovation lab: scan current AI and brand-science research, turn it into a testable commercial
> hypothesis, test it on public data, score the evidence honestly, flag the compliance risk, and
> hand a credible idea to the partner's product and data-science teams**. It fills the gap left by
> pharma-marketing texts (no AI), ML handbooks (no pharma constraints), and vendor white papers
> (claims without independent validation). It succeeds if the Fellow can take a current research
> finding and produce a **sourced, public-data-tested, compliance-aware product-handoff brief** that
> says *test it, build it, or kill it — and why* on the two questions that matter: does it move
> **lift** (incremental prescribing) or **brand** (durable quality association)?

## One-sentence logline

The Fellow does not ship the platform; the Fellow reduces the partner's uncertainty — testing on
public data which research ideas earn proprietary data and engineering resources.

## Central thesis

"This book argues that pharma has built the most sophisticated behavioral-targeting infrastructure
in any regulated industry while leaving almost none of its effectiveness claims independently
validated — which means the scarce, valuable work is not building models but **deciding which
modeling ideas actually improve incremental prescribing or durable brand equity** rather than merely
predicting likely prescribers or buying short-lived engagement, and this matters because an external
lab that tests that question cheaply, on public data, before engineering investment is the discipline
the field is missing and the one a Fellow is uniquely positioned to provide."

## Thesis test

- **Act One** establishes what the commercial machine optimizes and where its effectiveness claims
  outrun the evidence — the Fellow ends able to ask *who benefits from this measurement, and who
  doesn't?* ✓
- **Act Two** builds the model + measurement toolkit honestly — ensembles usually beat "MoE" on
  tabular data; lift requires a control; brand requires measuring durable association — so the
  Fellow can match a method to a question and a test. ✓
- **Act Three** runs the lab: a research thread, tested on public data, scored, compliance-flagged,
  and written as a product-handoff brief for the partner. ✓

**Thesis test: PASS**

---

# PART 2 — LEARNER PROFILE

## Primary reader

A **Humanitarians AI Fellow** — a data-capable graduate student, early-career data scientist, or
research analyst — embedded with (or collaborating with) a pharma marketing-technology partner,
agency, or brand team. They can run Python and a notebook, read a research paper, and reason about
data; they are **not** production ML or MLOps engineers, and they are **not** pharma-marketing
insiders.

**Specific person:** a second-year MS (data science / applied AI / health informatics) Fellow who
has been handed a vendor deck claiming "44% script lift from an AI-powered Mixture-of-Experts
platform," suspects something is off, and wants to know what a credible, independent test of that
claim would actually require — and whether they could run one.

## Prior knowledge assumed
- Python + notebooks; basic statistics/ML (regression, classification, train/test, AUC)
- Comfort reading a research paper and a dataset dictionary
- General AI literacy (what an LLM is; what a predictive model does)

## Prior knowledge NOT assumed
- Pharma commercial operations (detailing, MLR, formulary, NPI, claims) — **taught**
- Causal inference / uplift / experimental design — **taught** (Ch 8, 12)
- Deep-learning architecture internals beyond intuition — **taught at the needed depth** (Ch 6–7)
- Health-policy or regulatory law — **flagged as risk, routed to experts**, not taught as authority

## Prior misconceptions (what they think they know that is wrong)
1. "A model that predicts prescribers well will lift prescribing" — propensity ≠ incrementality (Ch 8).
2. "If the platform says Mixture of Experts, it's running MoE" — usually it's stacked models relabeled (Ch 7).
3. "Engagement (opens, clicks) measures whether the message worked" — engagement is a surrogate, not belief or scripts (Ch 2, 9).
4. "Brand = awareness" — pharma brand equity is the physician remembering the **patient type**, not the name (Ch 9).
5. "Lift the vendor reports is the lift the campaign caused" — attribution is structurally biased upward (Ch 2, 8/lift, 12).

## Motivation type
Primarily **professional/research** (the Fellow is doing real work with a partner and wants
publishable-or-productizable output), secondarily **academic** (course/fellowship requirement). The
design honors the professional motive: the terminal deliverable is a real product-handoff brief, not
a textbook exercise.

## Prerequisite map
| Prerequisite | Safe to assume? | If not: where addressed |
|---|---|---|
| Python + basic ML | Yes | — |
| Reading a paper / dataset | Yes | — |
| Pharma commercial stack | No | Weeks 1, 3, 4 (primary instruction) |
| Causal inference / uplift | No | Weeks 8, 12 (primary instruction) |
| MoE / ensemble internals | Probably not | Weeks 6–7 (primary instruction) |
| Public datasets (Open Payments, Part D, ICER) | No | Week 12 + used throughout Act III |
| Regulatory law (FDA/Sunshine/HIPAA/privacy) | No | Flagged as risk to route to counsel; not taught as authority |

**Front-loading decision:** the pharma commercial stack is the load-bearing "No" — it is front-loaded
into Act One (Weeks 1–5) because every model and metric choice is meaningless without it. No Chapter 0
needed; causal and architecture gaps are taught at first use.

---

# PART 3 — BOOK TYPE AND DEPLOYMENT SPECIFICATION

## Book type
**PRIMARY:** Fellows lab / practitioner research-agenda book — chapter = a capability a Fellow acts on,
culminating in a real research-to-product brief for a partner.
**SECONDARY:** Course textbook — adoptable as a 14–15-week graduate seminar in applied AI, health
marketing analytics, or computational social science (chapter = week).
**NOT:** a field-defining monograph (it is a working toolkit, not a single argument to read cover to
cover), and **not** a vendor handbook (it independently tests vendor claims).

## Deployment specification
- **Primary adoption:** Humanitarians AI fellowship cohorts collaborating with a pharma marketing-tech
  partner; the book is the onboarding text + research agenda + handoff discipline.
- **Secondary adoption:** graduate seminars (College of Engineering / Information Science / public
  health analytics); professional-development cohorts on AI in pharma commercial.
- **What it is NOT for:** clinical AI (diagnosis/treatment); DTC consumer advertising; drug-pricing
  policy as a primary subject; production platform engineering; legal/regulatory authority.
- **How the TOC signals type to a reviewer:** three labeled acts (System / Toolkit / Lab), a research
  finding flagged in every chapter, a public-data research portfolio in Act III, and a terminal
  product-handoff brief — a faculty member or a fellowship lead can map it to 14–15 weeks in minutes.

## The partner-collaboration spine (defining constraint)
This book is built for a **live external-innovation-lab collaboration with a pharma marketing-tech
partner.** That imposes a non-negotiable design rule, present from Chapter 11 and enforced throughout:

> **Public data and public methodology only in the book and its repo.** Fellows test ideas on
> public datasets (CMS Open Payments, Medicare Part D, ICER, syndicated/synthetic substitutes). The
> **partner** replicates promising methods on its proprietary data *internally* (Stage 2 of the
> pipeline). Nothing confidential — partner internal metrics, named-vendor figures, any patent or
> product IP — enters the public book or repo; sensitive working material lives in `private/`
> (gitignored). The firewall protects the partner's IP *and* the Fellow's research independence.

---

# PART 4 — FIELD POSITIONING

The competitive landscape is clean — each existing source serves a different reader or layer:

- **General pharma-marketing texts** (channels, brand planning, sales-force strategy) explain the
  business but not the AI, the measurement science, or independent validation.
- **ML handbooks** explain model families but treat pharma constraints (NPI identity, claims lag,
  MLR, FDA fair balance, payer friction, privacy) as someone else's problem.
- **Vendor white papers** claim lift and "AI/MoE" but conflate prediction with causation and never
  validate independently.
- **Health-economics / causal-inference texts** (Hernán & Robins; Cunningham) teach identification
  to epidemiologists/economists, not to a Fellow doing commercial research with a martech partner.

**The gap this book fills:** no book teaches a data-capable Fellow to **test, on public data, whether
a current AI or brand-science idea actually moves pharma marketing lift or brand equity — and to hand
the credible ones to a partner for productization**, in the partner's domain, with the regulatory and
patient-welfare constraints load-bearing.

**Positioning statement:** *For Humanitarians AI Fellows who need to turn current research into
defensible commercial experiments with a pharma marketing-tech partner, this is the external-lab
field guide that tests claims on public data and produces product-handoff briefs — unlike vendor
material, which asserts lift it never independently validates, and unlike ML or health-economics
texts, which teach the methods but not the pharma research-to-product loop.*

---

# PART 5 — THREE-ACT LEARNING ARC

## Arc statement
This book takes the reader from **a Fellow who can be impressed by a vendor lift claim** to **a Fellow
who can independently test whether a research idea earns the partner's resources**, by first mapping
what the pharma commercial machine optimizes and where its claims outrun evidence (Act One), then
building the model + measurement toolkit honestly under pharma constraints (Act Two), then running the
lab — research thread → public-data test → evidence score → compliance flag → product-handoff brief
(Act Three).

## Pebble-in-the-pond opening
Week 1 puts a real artifact on the page — a CDS Hooks / point-of-care co-pay message firing inside the
clinical workflow — and a vendor "44% lift" claim the Fellow cannot yet refute. The need-to-know is
created before any theory. The Fellow's **own research thread** (Part B) is chosen by Week 5 and
carried to the final brief.

## Act One — The System (Weeks 1–5)
- **Start:** can name "AI targets doctors."
- **End:** can read the commercial stack, name what each layer optimizes, and map a claim to the
  (missing) evidence behind it.
- **Transition to Act II:** the Fellow can state, for a tactic, the metric a model would have to move
  and whether that metric is lift or brand.

## Act Two — The Toolkit (Weeks 6–10)
- **Start:** has named the questions but can't choose methods.
- **End:** can pick ensemble vs. MoE vs. uplift vs. LLM for a question, and design the test that would
  produce credible evidence.
- **Hardest moment:** Week 8 (incrementality) — propensity-vs-causation inverts the Fellow's instinct
  that a good predictor is a good intervention.
- **Transition to Act III:** the Fellow can pair a method with a public dataset and a study design.

## Act Three — The Lab (Weeks 11–14)
- **Start:** has the toolkit.
- **End:** has run a research thread on public data and written a product-handoff brief (test/build/kill)
  with evidence score, compliance flags, and a patient-welfare check — defensible to the partner.

## The research thread across the arc (Part A / Part B)
| Stage | Part A (instructor's worked partner-relevant case) | Part B (Fellow's own research thread) |
|---|---|---|
| Wk 1–4 | Worked HCP stack + claim teardown | Pick a question: a lift thread or a brand thread |
| Wk 5 | Evidence map of the worked case | Evidence map of own thread; pick public dataset |
| Wk 6–10 | Method chosen + test designed for the case | Method + test designed for own thread |
| Wk 11–12 | Lab workflow + identification strategy on the case | Lab workflow + identification on own thread |
| Wk 13 | Worked portfolio project run | Own project run on public data |
| Wk 14 | Worked handoff brief | Own product-handoff brief (terminal deliverable) |

---

# PART 6 — PREREQUISITE MAP (dependency chain)

| Week | Depends on | Note |
|---|---|---|
| 1 | — | Pebble: the point-of-care artifact + the unrefutable claim |
| 2 | 1 | Lift vs. brand: the two dependent variables |
| 3 | 1–2 | Identity graph + targeting data |
| 4 | 1–3 | What the AI stack does (first vendor-claim audit) |
| 5 | 1–4 | The evidence problem (own thread + dataset chosen here) |
| 6 | 5 | Ensembles (the baseline every claim must beat) |
| 7 | 6 | MoE vs. relabeled stacking (needs the ensemble baseline) |
| 8 | 2,5 | Uplift/incrementality (needs lift definition + evidence frame) |
| 9 | 2 | Brand association (spiral return on Ch 2's brand half — escalates to measurement design) |
| 10 | 5–9 | LLMs for research + validation |
| 11 | all toolkit | Lab operating model + IP firewall |
| 12 | 8,11 | Identification strategies + public data sources |
| 13 | 11–12 | Run a portfolio project |
| 14 | 13 | Prototype-to-product brief (terminal) |

**Load-bearing chapters:** Ch 2 (the lift/brand split everything routes through), Ch 5 (evidence frame),
Ch 11 (the lab model + firewall). Skipping any breaks Act III.

---

# PART 7 — ASSESSMENT STRUCTURE

| Component | Points | Weeks |
|---|---|---|
| Reading responses (5 × 30) | 150 | 1, 2, 5, 7, 9 |
| Weekly lab exercises (8 × 25) — LLM/CLI tasks producing an artifact | 200 | 3–10, 13 |
| Vendor-claim audit (midterm) | 100 | 4 |
| Evidence map + dataset selection checkpoint | 100 | 5 |
| Method + test-design checkpoint | 100 | 10 |
| Lab project run (public data) | 150 | 13 |
| **Final: product-handoff brief** | 200 | 14 |
| **Base total** | **1000** | |
| Part B bonus (own research thread, up to 8 × 5) | +40 | per lab exercise |

**Part B bonus rule:** any lab exercise run on the Fellow's own research thread earns +5, provided the
**AI Use Disclosure** names one judgment the AI could not make (which claims are truly evidenced,
whether the signal is real, whether the partner could defend it to a regulator or an audit committee).

---

# PART 8 — CHAPTER-BY-CHAPTER TOC

## ACT ONE — THE SYSTEM (Weeks 1–5)
*Establishes how pharma HCP marketing and its AI actually work, and where effectiveness claims outrun
independent evidence.*

### WEEK 1 — The Machine Nobody Sees
**One-line:** Fellows learn to describe the full HCP marketing stack — identity graph → programmatic
impression → attribution — precisely enough to critique, and to name the structural anomaly that the
payer is not at the table.
**Learning outcomes:**
1. (Understand) Explain why the split of prescriber / patient / payer / institution breaks ordinary
   advertising theory.
2. (Apply) Trace the data flow from a brand objective through NPI identity to a point-of-care impression.
3. (Analyze) Distinguish what the stack optimizes from what patient welfare would require.
**Opening:** a real point-of-care / CDS Hooks co-pay message firing inside the EHR — the literal
delivery artifact — worked backward to the infrastructure that produced it. *(Partner's domain;
illustrative, public-sourced — no partner-confidential material.)*
**Core content:** the structural anomaly; NPI targeting stack; SMART-on-FHIR / point-of-care as a
commercial channel; the closed feedback loop; co-pay cards and the lost price signal.
**Research finding for Fellows:** EHR/point-of-care advertising is the fastest-growing channel with the
thinnest independent evidence — the single largest open validation gap. *(Verify channel-growth and
evidence claims against primary sources before publication.)*
**Assessment:** Reading Response #1. **LLM exercise:** map a public vendor description into the stack
layers. **Bridge:** the stack optimizes *something* — lift or brand? Week 2 splits them.

### WEEK 2 — Lift vs. Brand: The Two Dependent Variables
**One-line:** Fellows learn to decide whether a question is about campaign **lift** (incremental scripts)
or **brand formation** (durable "Brand X is for this patient"), and to pick the right metric.
**Learning outcomes:**
1. (Understand) Define TRx/NRx, **NBRx/new starts**, persistence, loyalty deciles, share of voice, share of mind.
2. (Evaluate) Judge when a metric (e.g., engagement) is a misleading surrogate.
3. (Apply / Part B) Map a stated commercial goal to a primary outcome metric and its failure modes — and choose your own thread.
**Opening:** a brand with healthy TRx but collapsing NBRx — "winning refills, losing decisions."
**Core content:** the brand-formation loop; NBRx as leading indicator; loyalty deciles; SOV vs. SOM;
why pharma brand equity = remembering the patient type. *(Grounded in `pantry/pharma-brand-measurement-synthesis.md`.)*
**Research finding for Fellows:** the SOMi→SOMa leading-indicator claim (mind-share predicts share growth
with a lag) is asserted qualitatively in industry but not rigorously tested on linked survey+claims data —
a tractable study (see Ch 13). **Assessment:** Reading Response #2. **Bridge:** to move either metric you
must reach the right HCP — the identity graph.

### WEEK 3 — The HCP Identity Graph and the Targeting Data
**One-line:** Fellows learn how prescribing data is legally obtained and resolved to NPI identity, what
the feature vector actually contains, and where it is biased.
**Learning outcomes:**
1. (Apply) Trace the pipeline: pharmacy claims → HIPAA de-identification → NPI identity resolution → bid-time decision.
2. (Analyze) Identify feature-vector components in a physician propensity model and assess appropriateness.
3. (Evaluate) Assess data lag and identity error as sources of targeting and measurement bias.
**Opening:** the AMA Physician Masterfile — the bridge from de-identified claims to physician identity,
and why its existence is the legal foundation of NPI targeting.
**Core content:** HIPAA safe-harbor de-identification; claims layer (IQVIA/Symphony); NPI identity graph;
the propensity feature vector (incl. Open Payments history); claims lag.
**Research finding for Fellows:** whether propensity models encode proxies for physician *susceptibility*
(not just clinical need) is unexamined and answerable with public data — a fairness/accountability
question (see Ch 13, Track D). **Assessment:** lab exercise (inspect a public claims/Open-Payments
extract). **Bridge:** given the substrate, what does the AI stack do on top of it?

### WEEK 4 — What Today's AI Stack Actually Does (and Claims)
**[MIDTERM: VENDOR-CLAIM AUDIT]**
**One-line:** Fellows learn to separate a genuinely deployed AI capability from marketing language across
next-best-action, predictive audiences, trigger messaging, MLR acceleration, and omnichannel.
**Learning outcomes:**
1. (Understand) Describe each production use case and its target KPI; rate it deployed / emerging / aspirational.
2. (Evaluate) Audit a vendor capability claim against "what KPI, what data, what evidence."
3. (Analyze / Part B) Apply the audit to a claim relevant to your own thread.
**Opening:** "the world's first AI-powered operating system for healthcare marketing, powered by an
adaptive Mixture of Experts" — is it true? what would it mean? what is it actually?
**Core content:** the capability inventory; deployed vs. sandbox; the labeling problem (first pass);
omnichannel orchestration.
**Assessment:** Midterm vendor-claim audit (100). **Bridge:** to judge the claims honestly, the Fellow
needs the model and measurement toolkit — and the evidence frame.

### WEEK 5 — The Evidence Problem
**One-line:** Fellows learn to distinguish peer-reviewed evidence from vendor-generated claims and rate
the evidence quality of each major channel — then lock their own research thread + public dataset.
**Learning outcomes:**
1. (Analyze) Evaluate an effectiveness claim against the standard for causal inference (association ≠ causation).
2. (Evaluate) Rate evidence quality per channel using a structured taxonomy.
3. (Create / Part B) Write the evidence map for your own thread and select the public dataset you'll use.
**Opening:** a vendor case study claiming 44% script lift where every sentence is true and none of it is
causal evidence. *(Illustrative; numbers labeled and to be `[verify]`-checked.)*
**Core content:** association vs. causation in promo analytics; what the peer-reviewed detailing
literature shows; the meal/Open-Payments association findings; the EHR-ad evidence gap; attribution
circularity (the platform that serves the ad also measures the lift).
**Research finding for Fellows:** the script-lift attribution gap is the field's largest open
methodological problem — no independent peer-reviewed study validates the causal attribution models
behind the 19–44% lift claims. *(Verify the specific study counts/effect sizes against primary sources.)*
**Assessment:** Reading Response #3 + Evidence-map & dataset checkpoint (100). **Bridge:** Act Two builds
the toolkit, starting with the baseline that usually wins.

## ACT TWO — THE TOOLKIT (Weeks 6–10)
*Builds the model + measurement vocabulary honestly, under pharma constraints. Each chapter adds one
tool and a test design.*

### WEEK 6 — Ensembles and the Tabular-Data Advantage
**One-line:** Fellows learn why gradient-boosted tree ensembles are the practical baseline for NPI
propensity and structured commercial prediction — the baseline any fancier claim must beat.
**Learning outcomes:**
1. (Understand) Explain bagging, boosting, stacking, and the bias–variance/covariance floor.
2. (Evaluate) Justify tree ensembles as SOTA on medium tabular data (Grinsztajn et al., NeurIPS 2022).
3. (Apply / Part B) Specify an ensemble baseline + honest evaluation for a propensity task in your thread.
**Opening:** an XGBoost propensity model as the unglamorous baseline that beats most "AI platform" claims.
**Core content:** the three ensemble paradigms; why trees handle uninformative features and irregular
targets natively; honest evaluation. *(Grounded in `pantry/moe-vs-ensemble-synthesis.md`.)*
**Assessment:** lab exercise (build/eval a baseline on public data). **Bridge:** vendors say "MoE" — real
upgrade or relabel?

### WEEK 7 — Mixture of Experts and Related Routing Models (and When the Word Is Marketing)
**One-line:** Fellows learn MoE precisely and learn to tell genuine sparse MoE from ensemble stacking
sold under a transformer-era label.
**Learning outcomes:**
1. (Understand) Explain sparse gating (Shazeer 2017), top-k routing, load balancing, expert collapse;
   trace Switch → Mixtral 8x7B → DeepSeek-V3 (256 fine-grained experts, aux-loss-free balancing, shared experts).
2. (Analyze) Explain output standardization + joint training as the real architectural difference from stacking; what experts actually specialize in (syntactic > semantic).
3. (Evaluate) Apply the buyer verification questions to a "MoE" platform claim and reach a verdict; judge when MoE is meaningful (scale, token/sequence, multi-task) vs. irrelevant (tabular NPI prediction).
**Opening:** a "MoE targeting engine" reframed as XGBoost + bid model + rules with a learned aggregator —
legitimate, but not MoE, and not obviously better than a tuned ensemble.
**Core content:** the formal MoE layer; the load-balancing-vs-specialization tension; the tabular
exception; the six buyer questions. **Research finding for Fellows:** a systematic audit of public
"MoE" pharma-platform claims against the three architectural criteria (token-level routing? shared trunk?
jointly trained?) is a publishable technology-audit study (Ch 13, Track C). **Assessment:** lab exercise
(claim teardown). **Bridge:** architecture aside — predicting a prescriber is not changing one.

### WEEK 8 — Uplift and Incrementality: Measuring Real Lift
**[HARDEST CONCEPTUAL MOMENT]**
**One-line:** Fellows learn to move from "who will prescribe?" to "whose behavior changed *because of*
the intervention?" — the inversion that breaks the propensity instinct.
**Learning outcomes:**
1. (Understand) Define uplift/CATE, treatment/control, holdouts, the fundamental problem of causal inference.
2. (Analyze) Distinguish propensity from incrementality and locate where platforms conflate them.
3. (Create / Part B) Design a holdout/uplift study for your thread with a defensible incrementality readout.
4. (Evaluate) Critique a "lift" claim that lacks a control group.
**Opening:** a "next-best-action lift" number that evaporates against a proper holdout.
**Core content:** uplift modeling; holdout design; natural experiments (state detailing restrictions,
policy changes); why targeting high-decile prescribers and measuring their response inflates estimates.
**Research finding for Fellows:** no peer-reviewed study has evaluated EHR/point-of-care advertising with
a randomized/pre-registered design — fillable via a health-system exposure partnership (Ch 13, Track A).
**Assessment:** Reading Response #4. **Bridge:** lift is activation; does the intervention also build
durable brand belief?

### WEEK 9 — Brand Association as a Measurable Outcome
**One-line:** Fellows learn to design tests of whether AI-driven content shifts durable association —
"Brand X is for *this* patient" — rather than short-lived engagement. *(Spiral return on Ch 2, escalated
to measurement design.)*
**Learning outcomes:**
1. (Understand) Explain the brand-formation loop and the strongest equity signal (the physician remembers the patient type).
2. (Apply) Operationalize association/quality-label outcomes (message association, perceived efficacy/safety, patient-archetype ownership, share of mind) into measurable designs.
3. (Create / Part B) Design a study testing whether a content variant shifts quality association — survey-based and/or embedding/implicit-association based — with a control.
4. (Evaluate) Distinguish a durable association shift from a transient recall bump.
**Opening:** a physician who says "best efficacy data" but has never switched a stable patient through
three generic entries — what actually drives that behavior, and how do you measure it?
**Core content:** attitudinal toolkit; implicit association testing for HCPs; conjoint; word-embedding
association from literature/CME; the brand-equity-vs-clinical-value question. *(Grounded in the brand
synthesis.)* **Research finding for Fellows:** does brand equity predict prescribing persistence after
controlling for ICER clinical-value score? An uncorrelated finding is a high-impact policy result (Ch 13,
Track B). **Assessment:** Reading Response #5. **Bridge:** much of this scanning/content work invites LLMs
— where do they help, where do they lie?

### WEEK 10 — LLMs for Commercial Research and Content Intelligence
**[METHOD + TEST-DESIGN CHECKPOINT]**
**One-line:** Fellows learn to use LLMs for literature scanning, claims-library mapping, and creative/bias
evaluation — with mandatory human validation against the fluency trap.
**Learning outcomes:**
1. (Apply) Use an LLM to scan research and map claims to evidence with provenance.
2. (Evaluate) Validate LLM output for hallucinated citations, fair-balance/regulatory risk, and fluent-but-wrong analysis.
3. (Create / Part B) Build an evaluation harness separating "useful draft" from "trustworthy claim" for your thread.
**Opening:** an LLM "evidence summary" that cites a study that doesn't say what it claims.
**Core content:** LLM-assisted scanning/mapping; the validation harness; why human expert review is
load-bearing; fair-balance and MLR risk in generated content. **Assessment:** Method + test-design
checkpoint (100). **Bridge:** the toolkit is built — how does a Fellow turn it into a repeatable lab with
a partner?

## ACT THREE — THE LAB (Weeks 11–14)
*Turns the toolkit into an external-innovation-lab process: research → public-data test → evidence score
→ compliance flag → product-handoff brief.*

### WEEK 11 — The External Innovation Lab Operating Model (and the IP Firewall)
**One-line:** Fellows learn the end-to-end workflow — scout → hypothesis → cheap public-data test →
evidence score → compliance risk → product-handoff memo — and the public-data/IP firewall that governs
partner collaboration.
**Learning outcomes:**
1. (Understand) Describe the lab's role (reduce the partner's uncertainty, not own production) and the four-stage productization pipeline (open research → proprietary replication → prototype → resourced).
2. (Apply) Convert a research finding into a falsifiable commercial hypothesis and a low-cost test.
3. (Evaluate) Apply the IP firewall: public data/method in the book and repo; partner-confidential material stays in `private/`; nothing proprietary is published.
4. (Create) Draft the skeleton of a product-handoff brief for medical/legal/regulatory/data-science/commercial stakeholders.
**Opening:** a one-page handoff memo that earns — or refuses — engineering resources.
**Core content:** the workflow; evidence-quality scoring; compliance risk (MLR, FDA fair balance,
Sunshine Act, HIPAA/privacy) as flags routed to counsel; the firewall; partner sign-off on framing.

**The Evidence Ladder (the lab's shared vocabulary — taught here, used in Ch 13–14):**

| Level | Evidence | What it unlocks |
|---|---|---|
| 0 | Interesting paper or vendor claim | Watch only |
| 1 | Plausible hypothesis mapped to a KPI | Fellow brief |
| 2 | Reproducible benchmark or simulation (public data) | Internal discussion |
| 3 | Small offline test that beats the baseline | Product discovery |
| 4 | Prospective pilot or holdout study | Product resourcing |
| 5 | Client-validated incremental impact | Roadmap candidate |
| 6 | Monitored deployment w/ compliance + patient-welfare checks | Product feature |

A handoff brief must name the artifact's ladder level — and a Fellow on public data tops out around
Level 3; Levels 4–6 require the partner's proprietary replication (Stage 2+). That boundary *is* the
firewall, made operational.

**Assessment:** lab exercise (firewall + hypothesis + ladder level for own thread). **Bridge:** to
test credibly you need identification strategy and the right public data.

### WEEK 12 — Research Design and Public Data for Marketing Science
**One-line:** Fellows learn the causal-inference toolkit (natural experiments, difference-in-differences,
regression discontinuity, instrumental variables) and map public data sources to research questions.
**Learning outcomes:**
1. (Apply) Select an identification strategy for a question given available public data.
2. (Analyze) Evaluate the identifying assumptions each design requires against the pharma context.
3. (Create / Part B) Design a credibly identified study for your thread on public data.
**Opening:** a state detailing-restriction policy change as a natural experiment (before/after, neighbor-
state control).
**Core content:** the identification problem; natural experiments (disclosure laws, AMC access rules,
formulary changes, LOE); DiD with staggered adoption; RDD at formulary/payment thresholds; IV; the public
data stack — **CMS Open Payments**, **Medicare Part D prescriber data**, **ICER** value assessments,
state Medicaid claims. **Assessment:** lab exercise (identification design). **Bridge:** with a design and
data, run a real project.

### WEEK 13 — The Fellow Research Portfolio (Run One)
**[LAB PROJECT RUN]**
**One-line:** Fellows execute one low-cost research project on public data that tests the book's two
questions — does it move lift, does it build association — and report honestly.
**Learning outcomes:**
1. (Create) Run a portfolio project end to end on public/synthetic data.
2. (Evaluate) Score the evidence and flag compliance/ethics risk.
3. (Create / Part B) Produce the result + plain-language readout for a partner decision-maker.
**The portfolio (choose one thread; full menu in the repo):**
- **Track A — Lift & attribution:** script-lift attribution audit; EHR/point-of-care natural experiment; omnichannel attribution decomposition (Part D + Open Payments).
- **Track B — Brand & physician identity:** SOMi→SOMa predictive-validity test; prescribing-habit durability across therapeutic classes; brand-equity vs. ICER clinical-value correlation; LOE persistence as a natural experiment.
- **Track C — Model architecture & segmentation:** ensemble-vs-genuine-MoE benchmark on NPI propensity; "natural N" physician archetypes via routing geometry; algorithmic audit of public "MoE" platform claims.
- **Track D — Privacy, fairness, accountability:** proxy-discrimination detection in rep assignment; co-pay-coupon generic-suppression causal estimate; accountability framework for commercial HCP-targeting AI.
**Each project ships:** hypothesis · public dataset (+ synthetic fallback) · **success threshold +
kill criterion** · evidence-ladder level reached · compliance + patient-welfare flags · **likely
partner owner** · handoff recommendation.

*Worked example (MoE-vs-ensemble benchmark): **Question** — does a routed expert model beat a tuned
gradient-boosting baseline on an NPI/NBRx task? **Baseline** — calibrated XGBoost/LightGBM. **Success
threshold** — meaningful, interpretable gain in out-of-time validation, calibration, or subgroup
robustness. **Kill criterion** — no lift over the tree ensemble, worse calibration, or complexity not
justified by business value. **Owner** — data science. **Handoff** — only if routing yields
operationalizable segment-specific gains.*

**Likely owner by lane:** Lift/attribution → measurement analytics; Brand/identity → brand strategy;
Model architecture → data science; LLM/content → content operations; NBA/journey → NBA-product;
Ethics/accountability → compliance + medical-commercial.

**Assessment:** Lab project run (150). **Bridge:** which of these deserves the partner's resources?

### WEEK 14 — From Prototype to Product Decision (The Fellows Brief)
**[FINAL — PRODUCT-HANDOFF BRIEF]**
**One-line:** Fellows decide whether a project earns productization, proprietary-data replication, MLR
review, engineering investment, partner client testing — or rejection — and write the brief that says so.
**Learning outcomes:**
1. (Evaluate) Apply explicit handoff criteria (evidence strength, lift/association magnitude, compliance
   risk, **patient-welfare gate**, build cost).
2. (Create) Produce the product-handoff brief and the rejection rationale (a "no" is a result).
3. (Apply) Stage a portfolio: test next / replicate on proprietary data / shelve / ship.
**Opening:** the terminal deliverable structure shown before any work — the brief a Fellow could hand
Graham's team.
**Core content:** handoff criteria; the four-stage pipeline revisited; the patient-welfare gate as a
required criterion (not an appendix); writing the test/build/kill recommendation.
**Final AI Use Disclosure (higher bar):** name three judgments across the project that required human
expertise no AI could supply (true evidence status, real-vs-noise signal, partner-defensibility).
**Assessment:** Product-handoff brief (200). Closes the arc: the Fellow as the honest filter between
research hype and committed partner resources.

---

# PART 9 — CHAPTER ANATOMY TEMPLATE

All 14 chapters follow this structure (series-consistent with the AI+1 books):
1. Chapter overview (1 paragraph; "what you'll be able to do")
2. Learning objectives (Bloom's explicit; Part A/B split where they differ)
3. Opening case — failure-first, in the HCP-marketing/AI deployment domain
4. Prerequisites as specific capabilities
5. Core content sections (4–6): concept → example → application
6. Mid-chapter checkpoint (ungraded)
7. Worked example (Part A) + Part B extension (the Fellow's own thread)
8. **Evidence check** — what here is independent vs. vendor-generated vs. hypothetical vs. contested
9. **Compliance + patient-welfare check** — MLR / FDA fair-balance / privacy risk and a welfare check,
   in *every* chapter (the discipline is pervasive, not a final-chapter appendix)
10. **Named Fellow artifact** — the reusable output this chapter trains (system map → KPI stack →
    identity graph → vendor audit → baseline memo → MoE brief → uplift design → association instrument →
    LLM workflow → lab protocol/Evidence Ladder → project proposal → handoff/kill memo)
11. **Research finding for Fellows** (the open question this chapter exposes — the agenda thread)
12. Assessable exercises (≥3; ≥1 at Apply+; ≥1 Part B)
13. **Five-part AI exercise block** (When to Use AI / When NOT / LLM exercise / CLI exercise / AI Validation) — the series signature
14. **AI Use Disclosure** (Part B: domain-specific, bonus criteria)
15. Chapter summary (capabilities gained)
16. Key terms (5–10, plain language)
17. Bridge question
18. Further reading (3–5 annotated; every empirical claim sourced or `[verify]`-tagged)
19. Prompts/figure metadata → `prompts/` (non-shipped), per series tooling

**Enforcement:** a draft missing items 8, 9, 10, 13, or 18 (evidence check, compliance+welfare check,
named artifact, five-part block, sourced further reading) is incomplete — do not advance to review.

---

# PART 10 — CASE STUDY STRATEGY

## Domain coverage map (no domain in >3 opening cases)
| Domain | Chapters |
|---|---|
| Point-of-care / EHR messaging (partner's world) | 1, 8, 12 |
| NPI targeting / propensity | 3, 6, 7 |
| Brand measurement / loyalty | 2, 9 |
| Evidence / attribution | 4, 5, 13 |
| Ethics / accountability | 3, 11, 13 |
| Fellow's own thread (Part B) | 5–14 |

## Escalation
- Act One: single concept, clear answer (read the system).
- Act Two: multiple concepts, judgment required (choose method + test).
- Act Three: one continuing thread (the Fellow's own), full synthesis, no single right answer.

## Sourcing requirement (load-bearing for THIS book)
Every empirical number carries **a citation or an `[INFERRED]`/`[verify]` label** — non-negotiable,
because the book's own thesis is that pharma effectiveness claims go unvalidated. The accuracy pass
(`ACCURACY-REVIEW.md`) runs over every chapter's statistics before publication.

---

# PART 11 — HARD TOPICS, CONTESTED CLAIMS, AGING RISK

## Contested claims
| Claim | Status | Book's position |
|---|---|---|
| "MoE" platforms run genuine MoE | Mostly false in practice | Usually stacked ensembles relabeled; apply the buyer questions |
| Vendor script-lift = caused lift | Disputed | Attribution structurally inflated; demand a control |
| Engagement measures message success | Misleading | Surrogate, not belief or scripts |
| Brand equity tracks clinical value | Open/empirical | Testable (ICER vs. equity); may be uncorrelated |
| Co-pay coupons are pro-patient | Nuanced | Improve affordability but can suppress generic substitution |
| Targeting models encode susceptibility proxies | Unexamined | Empirically answerable with public data; flag, don't assert |

## Hard chapters
- **Wk 7 (MoE):** must stay honest without becoming an ML-theory course for a non-engineer-leaning reader.
- **Wk 8 (incrementality):** the propensity→causation inversion; teach with a holdout that fails first.
- **Wk 11 (lab + firewall):** the partner-IP and critical-framing tensions are real; needs care.

## Aging risk
| Content | Risk | Cadence |
|---|---|---|
| Specific models (DeepSeek-V3, Mixtral) | High | Each offering — stable principle + dated example |
| Platform/vendor specifics | High | Each offering |
| Public-dataset schemas/links | Medium | Each offering |
| Regulatory state (Sunshine/FDA/AI Act) | Medium-High | Annual |
| Brand-measurement + causal fundamentals | Low | On major results |

---

# PART 12 — MARKET POSITIONING SUMMARY

Primary "market" is the **Humanitarians AI fellowship + partner pipeline** (the book is the operating
manual). Secondary market: graduate seminars and professional-development cohorts in AI-for-pharma-
commercial. Differentiation is clean (Part 4): the only book that teaches a Fellow to **test current
research on public data and hand credible results to a pharma martech partner**, with regulatory and
patient-welfare constraints load-bearing. Adoption estimate (secondary/course): ~30–80 course/cohort
adoptions/yr at steady state; primary value is the fellowship-partner research pipeline itself.

---

# PART 13 — FEATURE LIST

| Feature | Priority | Effort |
|---|---|---|
| 14-chapter / 3-act architecture | ESSENTIAL | Low |
| Lift-vs-brand spine | ESSENTIAL | Low |
| Public-data Fellow research portfolio (Tracks A–D) | ESSENTIAL | Medium |
| Product-handoff brief (terminal deliverable) | ESSENTIAL | Medium |
| Public-data / IP firewall + `private/` discipline | ESSENTIAL | Low (built) |
| Five-part AI exercise blocks + AI Use Disclosure | ESSENTIAL | Medium |
| Accuracy/[verify] pass over all statistics | ESSENTIAL | Medium |
| Part A / Part B dual path (own thread) | IMPORTANT | Medium |
| Synthetic datasets for prototypes | IMPORTANT | Medium |
| Instructor's / fellowship-lead manual | IMPORTANT* | High |
| Figures (brutalist system) + D3 | VALUABLE | Medium |
| Slide decks / portal | ASPIRATIONAL | High |

*Essential for any lead who is not the author. **MVT = ESSENTIAL features**, adoptable by the
fellowship as-is.

---

# PART 14 — OUT OF SCOPE

| Topic | Why excluded / better covered |
|---|---|
| Clinical AI (diagnosis, prognosis, treatment) | Distinct field; converges only at the EHR layer |
| DTC consumer advertising | Different reader/literature; this book is HCP-facing |
| Drug-pricing policy (full) | Touched via LOE/coupons; full analysis is its own book |
| International markets | US data/regulatory focus; international only where it illuminates the US gap |
| Production platform / MLOps engineering | The lab tests; the partner builds |
| Legal/regulatory authority | Risks are flagged and routed to counsel, not adjudicated here |

All exclusions acknowledged in the preface with a pointer. The **partner's proprietary methods and
data** are out of scope by design (the firewall) — a feature, not a gap.

---

# PART 15 — ADOPTION RISK REGISTER

| # | Risk | Likelihood | Impact | Status |
|---|---|---|---|---|
| **1** | **Partner-collaboration framing + data access unresolved** (public-only scope; sign-off on pointed chapters; whether/what proprietary replication is in-scope) | **High** | **High** | **BLOCKER — resolve with Graham before drafting Act III** |
| 2 | Critical-of-industry tone vs. a named partner (Ch 8/lift, Ch 13 Track D) | Med-High | High | Reframe as collaborative de-risking; partner sign-off on framing |
| 3 | Field velocity (models, platforms, regs date fast) | High | Med-High | Stable principle + dated example; annual review |
| 4 | Un-validated statistics shipped (the book's own sin) | High if unmanaged | High | Mandatory `ACCURACY-REVIEW.md` / `[verify]` pass |
| 5 | Public-data sufficiency for some tracks (D1, C-series) | Medium | Medium | Primary tracks use public data; proprietary tracks are secondary |
| 6 | Reader skill spread (non-engineer vs. data-science Fellow) | Medium | Medium | Part A/B dual path; teach causal/architecture at first use |
| 7 | IP leak into public repo | Low-Med | High | `private/` + the `doctor` PII/IP-leak check; firewall in instructions |
| 8 | Series hands-on layer not yet present in this scaffold | High (now) | Medium | Add five-part blocks + running thread during drafting |

---

# PART 16 — OPEN QUESTIONS

| # | Question | Stakes | Deadline | Owner |
|---|---|---|---|---|
| 1 | What is the partner-collaboration agreement — public-only scope, IP firewall terms, who signs off on framing? | The whole Act III + tone | Before Act III drafting | Nik + Graham |
| 2 | Which public/synthetic datasets are standardized for the Ch 13 portfolio? | Reproducibility of every prototype | Before Ch 12–13 drafting | Author + Fellows |
| 3 | Is patient-welfare a per-project gate or a capstone? | Assessment + ethics posture | Before Ch 14 | Author (recommend: gate) |
| 4 | How adversarial can the proxy-discrimination / attribution chapters be given the partner? | Relationship + credibility | With #1 | Nik + Graham |
| 5 | Course-textbook second config (15-week seminar) vs. fellowship-only — both, or primary one? | Market + manual scope | Pre-proposal | Author |
| 6 | How much implementation vs. research-design does the book require? | Difficulty + audience fit | Before drafting | Author (recommend: design-first, code in exercises) |

---

*Full TOC Draft v1.0 — compiled from all phase outputs, grounded in `pantry/` (MoE-vs-ensemble and
brand-measurement syntheses) and the existing `book.md` / `outline.md`.*
*One blocker before drafting Act III: Risk 1 (partner-collaboration framing + data access).*
