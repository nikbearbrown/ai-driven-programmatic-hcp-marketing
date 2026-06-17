# Chapter 9 — Brand Association as a Measurable Outcome (Research Notes)

**Chapter one-line (TIKTOC):** Fellows learn to design tests of whether AI-driven content shifts *durable* association — "Brand X is for *this* patient" — rather than short-lived engagement. (Spiral return on Ch 2's brand half, escalated to measurement design.)

**Spine fit:** This is the **brand** half of the lift-vs-brand spine. The measurable outcome is durable *quality association*, not incremental scripts.

**Reuse base:** `pantry/pharma-brand-measurement-synthesis.md` (strong — NBRx, loyalty deciles, SOV, brand-formation loop, FMCG-vs-pharma split, patient-welfare gap). This notes file restructures that synthesis into A–G form and ADDS the computational-measurement angle (implicit association, conjoint, word-embeddings) from web research, plus the ICER brand-equity-vs-clinical-value question.

> Sourcing rule for this book: every empirical number carries a citation or a `[verify]` / `[INFERRED]` flag. The brand-equity↔ICER correlation and the brand-WEAT application are **open questions / proposals**, not demonstrated results — see Section G.

---

## A. Conceptual foundations

**1. Pharma brand equity = remembering the patient type, not the name.**
The strongest equity signal is not unaided recall of "Brand X." It is the durable mental rule:
> *For this patient profile, in this disease state, after this prior therapy, Brand X is my default.*
(Source: `pharma-brand-measurement-synthesis.md` §3, §5.) This is the construct the chapter teaches Fellows to *measure*. It is more constrained than the FMCG "I wear Calvin Klein" identity statement, and far more valuable — because it predicts repeat prescribing at the moment of choice.

**2. The brand-formation loop (why association is the load-bearing link).**
Clinical evidence/label → KOL interpretation + guidelines → detailing/CME/congress → **HCP mental association ("Brand X is for this kind of patient")** → first trial → observed outcome → repeat or abandon → habit/loyalty/advocacy/switching. The association node is where marketing content acts; everything downstream (NBRx, loyalty deciles, persistence) is a *behavioral consequence* of the association. (Source: synthesis §3.)

**3. The brand-measurement stack is layered.** Attitudinal/equity → behavioral prescribing → prescriber loyalty → SOV/investment → patient journey → economic/payer value. The attitudinal layer is where "association" lives; the behavioral and economic layers are where you check whether the association *paid off* in durable, value-justified prescribing. (Source: synthesis §1 table.)

**4. The attitudinal toolkit (operational definitions).**
- **Unaided (spontaneous) recall** — names the brand without prompting; indexes top-of-mind salience. (Qualtrics: https://www.qualtrics.com/articles/strategy-research/what-is-brand-awareness/ ; Ipsos Encyclopedia – Awareness: https://www.ipsos.com/en/ipsos-encyclopedia-awareness)
- **Aided awareness** — recognizes the brand when prompted. The unaided→aided gap signals how much exposure is needed to embed the brand.
- **Favorability / familiarity / message association / perceived efficacy & safety / prescribing intent / NPS-style advocacy / share of mind** — the standard custom-survey + syndicated-panel battery (Kantar/Ipsos/M3/Medscape/IQVIA-DRG trackers). (Source: synthesis §1; Kantar brand-growth metrics: https://www.kantar.com/inspiration/research-services/choosing-the-right-metrics-for-brand-growth-pf)
- **Patient-selection criteria** — notable because pharma launch trackers already capture "for which patient" data; this *is* the thesis-construct living inside commercial trackers. (ZoomRx: https://zoomrx.com/blog/kantar-vs-zoomrx-pharma-launch-tracking ; Inizio: https://inizio.com/insights/measuring-brand-equity-a-brands-beating-heart/)
- *Caveat:* attitudinal measures are self-reported and can overstate actual prescribing. "Share of mind" is an industry term without a citable academic formula — flag if used. (See G.)

**5. The two measurement paradigms the chapter contrasts.**
- **Explicit / attitudinal** (surveys, conjoint) — what HCPs say.
- **Implicit / computational** (IAT, word-embedding association) — automatic associations the HCP may not self-report. The pedagogical move: a content variant might shift *implicit* association before (or without) shifting *explicit* survey answers — and might shift recall transiently without shifting durable association at all.

---

## B. Domain examples + failure case

**Opening case (from TIKTOC):** A physician says "[Brand X has the] best efficacy data" but has never switched a stable patient through three generic entries. The *stated* association (efficacy belief) and the *behavioral* association (default for stable patients) diverge. The chapter's job: how do you measure which one is real and durable?

**Example methods in the wild:**
- **Conjoint / discrete-choice experiment (DCE) on physicians.** A 2024/2025 DCE of ~1,047 Chinese physicians tested brand-name vs. certified-generic prescribing using price, hospital cost-control, clinical safety/efficacy info, and reimbursement rate as attributes — entering brand alongside identical clinical specs isolates the *pure brand premium* (utility assigned to the name net of efficacy/safety). (PMC11806230: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC11806230/) `[verify exact brand part-worth magnitude]`
- **WEAT (word-embedding association test)** as "an IAT you run on text" — measures differential cosine similarity between target word sets and attribute sets; Caliskan, Bryson & Narayanan (2017, *Science*) showed embeddings reproduce human IAT associations. (GESIS tutorial: https://methodshub.gesis.org/library/tutorials/weat/1/)
- **Biomedical embeddings as the substrate.** word2vec trained on ~16M PubMed abstracts recovered drug–disease relations via cosine similarity, validated against MeSH/DrugBank. (PLOS One / PMC8519453: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC8519453/)

**Failure case (the one the chapter should foreground): the transient recall bump mistaken for durable association.**
A content campaign produces a spike in aided recall and favorability measured *immediately* post-exposure. The brand team books it as equity built. But the change was peripheral-route (driven by a credible source / repetition, not deep processing), and on a delayed post-test it has decayed back toward baseline — no durable "for this patient" rule was formed. The persistence literature (Petty/Haugtvedt) shows central-route, high-elaboration change persists while peripheral change decays; a single post-exposure measurement *cannot* distinguish the two. (Haugtvedt & Petty, need-for-cognition & attitude persistence: https://richardepetty.com/wp-content/uploads/2019/01/1989-acr-haugtvedt-petty-need-for-cognition-and-attitude-persistence.pdf) **Measurement lesson:** you need a delayed re-measurement and a decay curve, not one survey.

A second failure case from the IAT literature: treating an implicit measure as a validated oracle. The IAT's predictive validity is contested (see D) — an implicit-association readout is a signal, not proof.

---

## C. Connections

- **To Ch 2 (lift vs. brand):** Ch 2 defines the brand dependent variable (NBRx, loyalty deciles, SOV, SOM, the brand-formation loop); Ch 9 escalates to *how you design a test* that measures the association outcome with a control. Direct spiral.
- **To Ch 10 (LLMs for research):** word-embedding association and corpus mining of CME/literature is exactly the LLM/NLP tooling Ch 10 governs — and the same validation discipline (don't trust a fluent association readout without checking it) applies.
- **To Ch 8 (uplift/incrementality):** brand-association studies still need a **control** (LO 3, LO 4). A favorability shift without a control group is the brand-side analog of a lift claim without a holdout.
- **To Ch 11–14 (the lab):** the Ch 13 portfolio Track B includes "brand-equity vs. ICER clinical-value correlation" and "SOMi→SOMa predictive-validity test" — Ch 9 supplies the instruments those projects run.
- **To the patient-welfare gate (Ch 14):** the brand-equity↔ICER question *is* the welfare check in measurable form — does durable association track clinical value, or commercial memory?

---

## D. Current state (sourced)

**Implicit Association Test (IAT).**
- Mechanism: Greenwald, McGhee & Schwartz (1998) — reaction-time sorting indexes automatic associations below survey-reportable awareness. (iMotions: https://imotions.com/blog/learning/research-fundamentals/implicit-association-test/)
- Marketing use: surfaces automatic brand attitudes that diverge from explicit reports; a "multidimensional IAT" (md-IAT) is promoted as valid/reliable for brand attitudes — but this rests largely on proponents/vendors. (PMC3016338: https://pmc.ncbi.nlm.nih.gov/articles/PMC3016338/)
- **Validity is contested (teach this honestly):** Greenwald et al. (2009) meta-analysis (122 reports, ~14,900 subjects) found mean predictive r ≈ .274 (https://faculty.washington.edu/agg/pdf/GPU&B.meta-analysis.JPSP.2009.pdf); Oswald et al. (2013) found much weaker prediction, aggregate r ≈ .148 (as low as ~.07 for negative microbehaviors, CI spanning zero) — no better than explicit measures (https://pubmed.ncbi.nlm.nih.gov/23773046/). Test–retest reliability is mediocre (~r ≈ .5 adults). Schimmack argues incremental validity is overstated (~.16) once measurement error is modeled (non-peer-reviewed blog: https://replicationindex.com/2021/06/13/predictive-validity-race-iat/).
- **HCP use:** the IAT is heavily used to measure *clinician implicit bias toward patient groups* (race, drug use) — FitzGerald & Hurst (2017) systematic review found 15/17 HCP-bias studies used the IAT (https://bmcmedethics.biomedcentral.com/articles/10.1186/s12910-017-0179-8). **Gap:** no peer-reviewed study uses an IAT to measure physician implicit attitudes toward a specific drug *brand* (see G).

**Conjoint / DCE.** Governed by ISPOR Good Research Practices (https://pubmed.ncbi.nlm.nih.gov/27325321/). Standard attributes: efficacy, safety, dosing, cost; including price yields willingness-to-pay. Entering brand as an attribute isolates brand premium. Recent: Chinese physician DCE (PMC11806230, above); health-economics DCE systematic review, *PharmacoEconomics* 2025 (https://link.springer.com/article/10.1007/s40273-025-01495-y).

**Word-embedding association.** WEAT (Caliskan 2017) is the IAT-on-text anchor. Cosine similarity between brand vector and attribute/concept set = the association measure (Springer marketing chapter: https://link.springer.com/chapter/10.1007/978-3-032-08086-8_10 ; ACL: https://aclanthology.org/N19-1181/). Biomedical embeddings recover drug–disease links (PMC8519453). **Operationalizing the thesis-construct:** build a WEAT where X={Brand X tokens}, Y={competitor}, A={patient-archetype descriptors}, B={other patients}, over a CME/clinical-literature corpus; the differential cosine association = computational measure of "Brand X is for THIS patient." This is a *proposal built on validated components*, not an existing cited result (see G).

**Durable vs transient.** Mere-exposure (Zajonc) builds favorability via repetition but is not uniformly durable; effects move with delay (POQ: https://academic.oup.com/poq/article-abstract/40/2/229/1877131). Durable = flat decay curve across a delayed post-test; transient = immediate bump decaying to baseline. Maps to ELM central vs peripheral route durability.

**ICER value framework.** Independent non-profit; cost-per-QALY + evLYG; commonly cited threshold range **$100k–$150k/QALY** (broader $50k–$200k); ultra-rare up to ~$500k/QALY. (ICER methods: https://icer.org/our-approach/methods-process/cost-effectiveness-the-qaly-and-the-evlyg/ ; framework PDF: https://icer.org/wp-content/uploads/2020/10/ICER-value-assessment-framework-Updated-050818.pdf) Closest available evidence on value vs. commercial success: net prices exceeded the $100k/QALY value-based price for ~81% of drugs and $150k for ~71% (Wouters et al. 2021, https://www.sciencedirect.com/science/article/pii/S1098301521001066). This links *price* (not brand equity) to ICER value.

---

## E. Teaching

- **The inversion to plant:** awareness/recall ≠ brand equity. The strongest equity is the physician's patient-type rule, which is *behavioral and durable*, not a survey answer.
- **The measurement-design skill:** every association claim needs (1) a control/variant comparison and (2) a delayed re-measurement to separate durable from transient. Teach with the transient-recall-bump failure first.
- **Two-paradigm framing (great for an exercise):** have Fellows design BOTH an explicit instrument (survey/conjoint) and an implicit/computational one (IAT-style or WEAT on a CME corpus) for the same association, then predict where they'll diverge.
- **Honesty about the implicit tools:** the IAT's predictive validity is genuinely contested — use it as a teaching case for "a popular instrument with a real validity fight," not as a validated oracle. Same for treating a WEAT cosine as ground truth.
- **The high-impact open question (motivates Ch 13 Track B):** does brand equity predict prescribing persistence *after controlling for ICER clinical-value score*? An uncorrelated finding would be a major policy result — and it's testable on public data (Open Payments + Part D + ICER).
- **Named Fellow artifact (per anatomy template):** an *association instrument* — a study design that measures durable quality association with a control and a delayed post-test.

---

## F. Library files (copied to pantry, prefixed `_lib_`)

- `_lib_why-machines-learn.md` — *Why Machines Learn* (Anil Ananthaswamy). Background on embeddings/vector geometry; supports the cosine-similarity / WEAT mechanism intuitively. (Direct mentions of embeddings are light; use for the math intuition.)
- `_lib_keeping-up-with-the-quants.md` — *Keeping Up with the Quants*. General analytics framing; light brand-equity/embedding mentions; useful for the "how to frame a measurement question" pedagogy.

*Note:* The MD library is a general AI/business/science collection with no pharma-brand-measurement or computational-brand-association depth. The strong base for this chapter is the existing `pharma-brand-measurement-synthesis.md` plus the web research above. Other `_lib_` files in pantry (causal inference, randomistas, book-of-why, etc.) were copied by prior agents for Ch 5/8/12 and are relevant to the control-group point (C) but not central here.

---

## G. Gaps / flags

1. **No published IAT measuring physician implicit attitudes toward a drug brand.** HCP IAT work targets patient-group bias, not brand. Present as a genuine gap (strong for the thesis), do NOT imply one exists.
2. **No published brand-vs-patient-archetype WEAT on CME/clinical text.** The method (WEAT + biomedical embeddings) is component-wise validated; the specific application is a *proposal*, not a result. Label as such.
3. **No study correlating brand equity with ICER value.** Evidence links *price* (not brand equity) to ICER value and shows divergence. The brand-equity↔ICER correlation is an OPEN question (= Ch 13 Track B). Do not cite as demonstrated.
4. **md-IAT "valid and reliable for brands"** rests on proponents/vendors; the broader IAT validity literature (Oswald 2013, Schimmack) is sharply critical. Present as contested.
5. **Effect sizes** (Greenwald r≈.274; Oswald r≈.148/.07) read from author PDF / PubMed abstracts, not full re-tabulation. `[verify]` against primary PDFs before print.
6. **Vendor tracker methodology** (Kantar/Ipsos/ZoomRx): construct *definitions* reliable; proprietary formulas and "share of mind" lack a citable academic standard. `[verify]` any precise proprietary claim.
7. **Schimmack/Replicability-Index** is a credible academic blog but non-peer-reviewed; cite with that caveat or find the peer-reviewed equivalent.
8. **Chinese physician DCE brand part-worth magnitude** not independently verified beyond the abstract. `[verify]` the utility value before quoting.
9. **ICER threshold figures** verified from ICER's own documents but the threshold range is itself contested in health-econ; present as ICER's stated range, not a universal truth.
