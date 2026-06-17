# Chapter 12 — Research Design and Public Data for Marketing Science
*Why the dataset is the commodity and the identification argument is the contribution.*

In 2017, a team of researchers published a study in *JAMA* with a finding that the pharmaceutical industry had good reason to find uncomfortable (Larkin et al., *JAMA* 317(17):1785–1795, 2017). Across nineteen academic medical centers that adopted policies restricting pharmaceutical sales-representative visits between 2006 and 2012, physicians shifted their prescribing away from the detailed branded drugs — the ones representatives had been promoting — and toward non-detailed drugs, which are largely generics. Using a difference-in-differences design comparing 2,126 attending physicians at the nineteen centers against roughly 24,600 matched controls, the study estimated that exposure to a detailing policy was associated with a decrease in detailed-drug market share of about 1.7 percentage points and a corresponding rise in non-detailed-drug share. The effect concentrated where the policies had teeth: of the eleven centers whose policies combined gift limits, restrictions on representative access, *and* explicit enforcement mechanisms, eight showed a significant change in prescribing; among the eight centers that lacked one or more of those three elements, only one did.

The paper is worth examining not just for what it found but for how it found it. The researchers did not run a randomized trial. They could not — you cannot randomly assign academic medical centers to restrict detailing and wait to see what happens. They did not run a regression with a long list of control variables and call the coefficient causal. What they did was find a structure in the real world that did the randomization for them. Academic medical centers adopted detailing restrictions at different times, for institutional reasons having nothing to do with what their physicians happened to be prescribing. That staggered adoption — some centers treated in 2006, others in 2009, still others in 2012, and some never treated at all — created a natural experiment. The never-treated and not-yet-treated centers supplied the counterfactual: what the treated centers' prescribing would have looked like absent the restriction.

That is the template. A policy shock, a comparison group it did not reach, and an outcome you can measure. Everything else in this chapter is how to build one, stress-test one, and know when you cannot.

---

The fundamental problem of causal inference is simple to state and impossible to escape. For any physician you observe, you see either the world in which they received heavy detailing or the world in which they did not — never both. The causal effect of detailing on that physician is the difference between the two worlds. One of those worlds is missing. Every identification strategy is a different argument for how to reconstruct the missing world from observable units. Nothing more.

The mistake that ends most causal claims before they start is believing that a longer list of control variables closes the gap. It does not. Statistical controls handle confounders you can observe and measure. The confounders that actually threaten causal claims in pharmaceutical marketing — physician quality, patient mix, local market dynamics, unobserved selection into high-detailing practices — are precisely the ones you cannot fully observe. Adding more covariates to a regression does not neutralize unobserved confounding. Structure does.

Structure means a feature of the world that assigns treatment for reasons plausibly unrelated to the outcome. A state passes a gift-ban law because a legislator champions it, not because that state's physicians were already trending toward generics. An academic medical center restricts rep visits because its conflict-of-interest committee recommends it, not because prescribing had already started to shift. A Medicare spending threshold triggers a coverage gap because of a budget formula written in 2003, not because the patients who hit it are different from the ones who fall just short. In each case, the treatment assignment carries information — it encodes something about who got treated and when — but it is the *right kind* of information: information about the institutional or legislative or administrative process, not about the outcome you are trying to explain. That is what "as good as random with respect to the outcome" means, and it is the thing you are always trying to establish.

![Two parallel timelines for one physician: World A — heavy detailing, observed with measured outcomes; World B — no detailing, an unobserved ghost box with the outcome missing. An arrow reads "Causal effect = World A outcome minus World B outcome." A footer notes that every design is a different argument for imputing World B from other observable physicians.](../images/12-research-design-public-data-fig-01.png)

*Figure 12.1 — The fundamental problem of causal inference*

<!-- → [DIAGRAM: The fundamental causal inference problem. Two parallel timelines for one physician: "World A — heavy detailing" (observed, with outcomes) and "World B — no detailing" (unobserved, outcome missing). Arrow labeled "Causal effect = World A outcome − World B outcome." Below: "Every design is a different argument for how to impute World B from other observable physicians." Caption: "The missing counterfactual is the central problem. Structure is the solution."] -->

---

The first and most useful identification design for public-data pharma research is the **natural experiment** — a real-world event that assigns treatment to some units and not others in a way you can argue is exogenous to the outcome.

In the HCP marketing context, the recurring sources are well-catalogued. State-level detailing disclosure and gift-ban laws — Minnesota has required gift disclosure since 1993, Vermont banned gifts outright in 2009 — create cross-state variation in how much promotion physicians may receive, variation driven by legislative politics rather than prescribing trends. Academic medical center detailing-access rules, the wave the Larkin study exploited, create variation at the institutional level. Formulary changes — a payer moving a drug to a higher tier, imposing prior authorization, lifting it — shift the friction physicians face at known, administratively determined dates. And **loss of exclusivity**, when a small-molecule brand faces its first generic entrant, creates a dated, exogenous economic shock: the exact date of generic entry is set by patent expiration and FDA approval, not by anything the physicians or the brand were already doing.

Each of these is a natural experiment in the rough sense. Whether any specific one qualifies in the precise sense requires asking a pointed question: *why did these units get treated when they did, and is that reason correlated with the outcome?* A gift ban adopted in a state precisely because branded prescribing was already rising is endogenous — the policy was triggered by the trend, not by something orthogonal to it. An early disclosure-law study found such laws changed reporting behavior while doing little to prescribing, a useful reminder that the treatment must be the thing you think it is.

The test is not just plausibility. It is the story. Can you tell a credible account of why the institutional politics or the legislative calendar or the patent clock produced the treatment assignment, and why that account makes no reference to the prescribing outcome? If you can tell that story and defend it against the obvious objections, you have the exogeneity argument. If you cannot, you have an association.

---

The workhorse design for translating a natural experiment into a number is **difference-in-differences**. The logic is disarmingly simple: compare the change in outcome for a treated group to the change in outcome for a control group across the event. The double-differencing — one difference across groups, one across time — removes any fixed difference between groups (treated physicians were always different from controls) and any common shock (both groups experienced the same time trend). What remains is the change in the treated group over and above whatever the control group experienced — and under one assumption, that is the causal effect.

The assumption is **parallel trends**: absent treatment, the treated group's outcome would have evolved along the same path as the control's. It is the identifying assumption of every DiD design, and it is the one you must defend most carefully, because it is the one that is easiest to wave past. The pre-treatment event-study plot is the main diagnostic: if treated and control units were moving together before the policy, you have evidence (not proof) that they would have continued to move together absent the policy. Parallel trends is functional-form dependent — trends that are parallel in levels may not be parallel in logs — which means the choice of outcome transformation is a real modeling decision, not a cosmetic one.

The clean case — two groups, two time periods — is rare in policy data. The realistic case for state gift bans, for academic medical center access restrictions, for any rolling policy adoption is **staggered adoption**: units receive treatment at different dates spread across years. And here lies the trap that has invalidated a generation of published estimates.

The naive fix for staggered adoption is a two-way fixed effects regression — unit fixed effects, time fixed effects, a single treatment dummy — and then reading off one coefficient. The problem, formalized by Goodman-Bacon (2021, *Journal of Econometrics* 225(2):254–277) and now widely understood, is that the TWFE estimator uses *already-treated* units as controls for *later-treated* units. Those are forbidden comparisons: a state that banned gifts in 2007 is being used as a counterfactual for a state that banned gifts in 2011, but the 2007 state has been treated for four years and its prescribing has already adjusted. The comparison conflates the causal effect you want with dynamics you did not intend to estimate. The resulting coefficient can be wrong in sign and magnitude.

The modern fix is a family of heterogeneity-robust estimators — **Callaway and Sant'Anna (2021, *Journal of Econometrics* 225(2):200–230)** is the most widely adopted, with de Chaisemartin and D'Haultfœuille (2020, *American Economic Review*), Sun and Abraham (2021, *Journal of Econometrics*), and Borusyak, Jaravel and Spiess (2024, *Review of Economic Studies*) as close alternatives — that construct group-time average treatment effects using only never-treated or not-yet-treated units as controls. For a current synthesis, see Baker, Callaway, Cunningham, Goodman-Bacon and Sant'Anna, "Difference-in-Differences Designs: A Practitioner's Guide" (arXiv:2503.13323, forthcoming *Journal of Economic Literature*). The estimates are then aggregated across groups and time periods in a way that is explicit about what is being averaged and weighted. Any staggered DiD analysis that still uses plain TWFE is dated. Not wrong by convention — wrong by math.

![Three panels on staggered adoption. Left: three units adopting treatment in 2006, 2009, and 2012, plus a never-treated control. Center: a two-way fixed-effects comparison marked in red, where an early-treated unit is wrongly used as a control for a later-treated unit — the forbidden comparison. Right: the Callaway–Sant'Anna fix, where each treated cohort is compared only to not-yet-treated and never-treated units.](../images/12-research-design-public-data-fig-02.png)

*Figure 12.2 — Staggered adoption: TWFE forbidden comparisons vs. clean controls*

<!-- → [DIAGRAM: Staggered adoption illustration. Left panel: three units adopting treatment in years 2006, 2009, and 2012, plus a never-treated control unit. Center panel: forbidden comparison in TWFE — early-treated unit used as control for late-treated unit. Right panel: Callaway-Sant'Anna — each treated cohort compared only to not-yet-treated and never-treated units. Caption: "TWFE uses forbidden comparisons under heterogeneous effects. The modern fix uses only clean controls."] -->

---

When the treatment is not a policy adopted at different times but a rule that assigns based on whether a continuous variable crosses a threshold, the right design is **regression discontinuity**.

The Medicare Part D coverage gap is the cleanest example in the public data. When a beneficiary's cumulative drug spending crosses a defined threshold in a calendar year, the out-of-pocket share jumps sharply — the "donut hole" in the original Part D design. Beneficiaries just below the threshold and beneficiaries just above it are nearly identical in every measurable way. They have similar diagnoses, similar drug regimens, similar demographic profiles. The only thing that differs is which side of the spending line they happen to have crossed. That near-identity in a neighborhood around the cutoff is what RDD exploits: the jump in outcome at the threshold identifies the causal effect of the coverage change.

The identifying assumption is continuity of potential outcomes at the cutoff — the treated and untreated outcomes would both have been smooth functions of the running variable absent the threshold rule. The threat is sorting: if physicians or patients can manipulate whether they fall just above or just below the cutoff, the near-identity around the threshold breaks down. The McCrary density test (McCrary, 2008, *Journal of Econometrics* 142(2):698–714) — checking whether the distribution of the running variable is smooth at the cutoff, or whether there is a suspicious bunching on one side — is the standard diagnostic.

Low-Income Subsidy eligibility in Part D creates a second RDD: beneficiaries just above and below the income cutoff face different cost-sharing, and the discontinuity has been used to estimate the price elasticity of drug adherence. Formulary tier changes that flip at a defined criterion are another family. Wherever a policy rule creates a sharp threshold in a continuously distributed variable, and you can argue that the distribution is smooth and unsorted around the cutoff, RDD is the design.

---

When treatment is endogenous and no clean natural experiment or threshold exists, the remaining option is **instrumental variables**. The logic: find a variable Z that shifts treatment status without shifting the outcome through any channel other than the treatment. If Z predicts who gets treated (the relevance condition), if Z affects the outcome only through treatment (the exclusion restriction), and if Z is plausibly as-good-as-randomly assigned, then variation in Z can be used to recover the causal effect of treatment on the subset of units whose treatment status responds to Z — the **local average treatment effect** for compliers.

IV is the most powerful and most abused design in this toolkit. Relevance is testable: report the first-stage F-statistic, and treat a weak first stage (F below 10, conservatively) as a disqualifying problem, because weak instruments bias the estimate toward OLS and make standard errors unreliable. The exclusion restriction is not testable — it is a substantive claim that Z touches the outcome only through treatment, and every such claim is a theory that opponents can challenge on the grounds of pathways you did not consider. In public-data pharma work, candidate instruments are scarce. Geographic variation in promotion exposure driven by something exogenous — distance to a detailing hub, rollout order for a sales force expansion — can sometimes be defended. Each case requires its own argument, and each argument requires more than the claim that Z is correlated with treatment.

---

The four identification strategies map onto the public data in ways that are worth making explicit.

**CMS Open Payments** contains every industry transfer of value to a physician or teaching hospital: the payer, the recipient's NPI, the amount, the date, the nature of the payment, the associated drug or device. It is the promotion dose at the physician level. The data is free to download with no data use agreement required, and it covers August 2013 onward. Open Payments is association-grade alone. The payment-prescribing correlation is real and replicated in the literature — it is not a fabrication — but it is confounded by selection into high-detailing practices in ways that no covariate list can fully address. A design layered on top of Open Payments, using one of the strategies above, is what moves from association to evidence.

**Medicare Part D Prescriber Public Use Files** contain drug prescribing per provider: NPI, drug name, total claims, 30-day fills, beneficiary counts, total cost. This is the outcome variable for most lift and attribution work on public data. It is published annually with roughly a two-year lag, covers 2013 onward, and requires no data use agreement. Two limits are worth stating in every brief that uses it. First, Part D does not directly observe new-to-brand scripts — new starts are a longitudinal patient construct requiring a patient record, which Part D PUF does not supply. Fellows must proxy new starts from observed changes in physician-level volume and label them as proxies. Second, Part D covers the Medicare population: elderly and disabled beneficiaries. The commercially insured population, where most branded-drug volume lives and where copay coupons operate, is structurally invisible.

**Medicaid State Drug Utilization Data** contains state-level Medicaid outpatient drug utilization by NDC code: units reimbursed, prescriptions, amounts reimbursed, by state and quarter. There is no physician identity, but the state-by-time panel is exactly what state-policy natural experiments require. Pair SDUD with Open Payments for the state gift-ban design; SDUD supplies the outcome panel, Open Payments supplies the promotion dose.

**ICER value assessments** supply the clinical-value covariate that transforms a promotion-and-prescribing study into a welfare-relevant finding. ICER reports cost-effectiveness ratios and value-based price benchmarks; in its value framework it evaluates results against a cost-effectiveness range of roughly $50,000 to $200,000 per QALY, anchoring its health-benefit price benchmark to the $100,000–$150,000 band, so a drug coming in near or below $50,000 per QALY reads as high value and one well above $150,000–$200,000 reads as low value (ICER Value Assessment Framework). Confirm the current thresholds against ICER's published framework before quoting exact figures, since the range is periodically updated. When you pair a promotion effect — detailing increases branded share — with the ICER score for that drug, you can ask whether the effect is larger for high-value drugs (promotion serves patients) or for low-value ones (promotion serves volume). That question is testable on public data. No published study has answered it.

| Dataset | What it contains | Coverage | Access | What it supports | Critical limits |
| --- | --- | --- | --- | --- | --- |
| Open Payments | Industry transfer of value per NPI (promotion dose) | Aug 2013–present | Free download, no DUA | payment→prescribing natural experiments | Association-grade alone; requires a design |
| Part D Prescriber PUF | Prescribing outcome per NPI (claims, fills, beneficiaries, cost) | 2013–present, ~2-yr lag | Free download, no DUA | lift / brand-persistence outcomes | No new-to-brand (NBRx); Medicare population only |
| Medicaid SDUD | State × quarter outpatient drug utilization by NDC | Multi-year | Free download | state-policy DiD outcomes | No physician identity; aggregated |
| ICER assessments | Clinical-value / cost-effectiveness covariate | Rolling | Free PDFs | welfare-relevant covariate | QALY methodology contested; selected drug set |

*Table 12.1 — The public-data stack: the datasets are commodities; the identification argument is the contribution*

---

Put the pieces together and the decision is a short tree. If a policy was adopted at different times across units, the design is staggered DiD — Callaway and Sant'Anna, with an event-study plot, using not-yet-treated and never-treated controls. If a single dated shock hit one group and not another, the design is a 2×2 DiD or event study with a parallel-trends defense. If a sharp eligibility or spending cutoff exists, the design is RDD with a density check. If an exogenous shifter of exposure exists and the exclusion restriction can be defended, the design is IV with a reported first-stage F.

In every case, what you are required to produce is: the identifying assumption stated in plain English, the diagnostic that would falsify it, and the Evidence Ladder level the design can reach. Public-data designs of this kind top out around Level 3 — a small offline causal test. Level 4 (offline causal test on partner data) and Level 5 (client-validated business impact) require the proprietary panel on the other side of the firewall. Stating the ceiling is not a concession; it is the honest calibration that makes the estimate trustworthy.

The contribution is the identification argument. Open Payments and Part D are freely available to anyone with a laptop. The finding that is worth something is the finding that has a credible answer to "why is this causal rather than associated?" That answer is built from the structure in the world, the estimator chosen to exploit it, and the diagnostics that would catch it if the structure were not as clean as assumed.

## What Would Change My Mind

The ceiling on public-data causal designs — Level 3 on the Evidence Ladder — is imposed by the missing commercially insured population and the absence of patient-level new-start data. If a credible public dataset emerged that linked physician-level new starts with commercially insured patients, the ceiling would rise. Today no such dataset exists; the proprietary panels that have it sit across the firewall. I would also revise the claim that TWFE is biased in staggered settings if a compelling theoretical argument showed the heterogeneity in treatment effects is bounded tightly enough in the pharma-policy context that the bias is negligible — but I have not seen that argument made for this domain, and the Goodman-Bacon decomposition applies regardless of domain.

## Still Puzzling

The most policy-relevant promotion effects operate on the commercially insured — where copay coupons work and where most branded volume lives — but the cleanest public outcome data is Medicare and Medicaid. Every public-data finding carries an external-validity asterisk pointing at exactly the population that matters most. Whether a clever design can bridge that gap, or whether the commercial-population effect is structurally invisible to public data, is the question the book leaves open.

---

## Exercises

**Warm-up**

1. *(Recall — low difficulty) What this tests: the identifying assumption for each design.* For each of the four identification strategies — natural experiment/DiD, staggered DiD, RDD, and IV — state the identifying assumption in one sentence and name the single diagnostic that would falsify it.

2. *(Recall — low difficulty) What this tests: the TWFE bias problem.* Explain in plain language why a two-way fixed effects regression with a single treatment dummy is biased in a staggered adoption setting. Name the paper that formalized this problem and the estimator this chapter recommends as the fix.

3. *(Recall — low difficulty) What this tests: dataset limits you must state in every brief.* For each of the four public datasets in the stack, name one critical limit that must be stated in any brief that uses it. For Part D specifically, explain why it does not directly observe new-to-brand prescribing and what a Fellow must do instead.

**Application**

4. *(Apply — medium difficulty) What this tests: selecting and defending an identification strategy.* A state implemented a prior-authorization requirement for a high-cost branded drug in January 2019. Neighboring states did not. You have Medicaid SDUD for both states from 2015 through 2022. Specify the identification design, the comparison group, the identifying assumption, the pre-trends diagnostic you would run, and the Evidence Ladder level the result can reach.

5. *(Apply — medium difficulty) What this tests: converting an association finding to a causal design.* A published study finds a positive correlation between Open Payments meal receipts and branded statin prescribing using a multivariate regression with specialty, geography, and practice-size controls. Explain in two sentences why this is not a causal estimate despite the controls. Then design a natural experiment on public data that would make it causal, naming the data sources, the comparison group, and the identifying assumption.

6. *(Apply — medium difficulty) What this tests: catching a TWFE error in practice.* An LLM produces the following R code for a staggered DiD analysis: a `feols()` call with physician and year fixed effects and a single `treated` dummy. You run it and get a coefficient of −0.12 (p < 0.01). Explain why you cannot interpret this as the causal effect of the policy, what forbidden comparisons it likely contains, and what you would run instead.

**Synthesis**

7. *(Synthesis — high difficulty) What this tests: writing the identification-design memo.* Write the identification-design memo for a study testing whether state pharmaceutical gift bans caused a shift from branded to generic prescribing in Medicaid: the research question, the dataset(s), the identification design, the identifying assumption stated in plain English, the diagnostic that would falsify it, the Evidence Ladder level the result can reach, and the two dataset limits you would state in the brief.

8. *(Synthesis — high difficulty) What this tests: linking promotion effects to patient welfare.* You run the gift-ban DiD and find a significant reduction in branded-drug prescribing at restricting academic medical centers. Explain how you would use ICER value assessments to determine whether this reduction was welfare-improving or welfare-neutral — what additional analysis would you run, what result would suggest the reduction served patients, and what result would suggest it was clinically neutral.

**Challenge**

9. *(Challenge — open-ended) What this tests: designing a study at the boundary of what public data can support.* Design a study using only public data (Open Payments, Part D PUF, Medicaid SDUD, ICER) that addresses the question "does promotion of low-value drugs (ICER >$175k/QALY) produce a larger prescribing effect than promotion of high-value drugs (<$50k/QALY)?" Specify the identification strategy, the comparison structure, the identifying assumption, the dataset join logic, and the one inferential limit you cannot resolve with public data alone. State honestly what Evidence Ladder level it can reach and what the next step across the firewall would require.

---

## Prompts

### Figure 12.1 — The fundamental problem of causal inference

Build a single self-contained HTML file (inline CSS, D3 7.9.0 from cdnjs) rendering a conceptual two-timeline diagram, not a data chart — zero-baseline n/a. Data shape: one physician with two potential-outcome worlds, each an object {world, label, observed (boolean), outcome}. World A ("heavy detailing") is observed with a measured outcome; World B ("no detailing") is unobserved with a missing outcome. Marks: two horizontal timeline rows of equal width, each a labeled rectangle (box) with a short outcome glyph at its end; a connecting arrow between the two outcome ends annotated "Causal effect = World A outcome − World B outcome"; a footer line of body text reading that every design is a different argument for imputing World B from other observable physicians. Channels: encode observed vs. unobserved by fill and stroke — World A solid box with ink stroke and a real outcome value; World B distinct as a ghost/empty dashed box (stroke-dasharray, var(--color-border)) with no outcome value, using var(--color-red) only to mark the missing world. Two data colors max. No sort. Annotations: row labels left, the causal-effect arrow label centered (never on the arrow centerline), caption below. Title and desc for accessibility; ResizeObserver redraw. Deliverable: one HTML file.

### Figure 12.2 — Staggered adoption: TWFE forbidden comparisons vs. clean controls

Build a single self-contained HTML file (inline CSS, D3 7.9.0 from cdnjs) rendering a three-panel small-multiple conceptual diagram, not a quantitative chart — zero-baseline n/a. Data shape: an array of units {id, adoptionYear (2006, 2009, 2012, or null=never-treated)} on a shared year axis (≈2004–2014), plus a list of comparison edges {from, to, kind: "forbidden" | "clean"}. Marks: each panel is a grid of unit rows against the year axis; each unit row drawn as a pre-period segment and a post-treatment segment split at its adoption year (never-treated stays one segment); vertical tick marking each adoption year; comparison arrows between unit rows. Channels: encode treated/post state by segment fill; encode comparison validity by color — forbidden comparisons (early-treated used as control for late-treated) in var(--color-red), clean comparisons (vs. not-yet-treated / never-treated) in var(--color-ink). Two data colors max. Sort units by adoption year within each panel. Panels left→right: (1) adoption structure, (2) TWFE forbidden comparison in red, (3) Callaway–Sant'Anna clean controls. Annotations: panel titles, year ticks (monospace), legend, caption. Title/desc; ResizeObserver redraw. Deliverable: one HTML file.

---

## Chapter 12 Exercises: Research Design and Public Data for Marketing Science

**Project:** One Drug, End to End
**This chapter adds:** You design an identifiable public-data study of your drug — choosing among DiD, RDD, and IV, stating the identifying assumption, and naming the falsification test first — turning Chapter 11's cheap test into a credible identification argument.

*Worked example throughout: **Cardizem-X**, the branded cardiometabolic drug from Chapter 11, with its first generic entrant arriving at a dated, exogenous loss-of-exclusivity shock. Swap in your own drug and its policy shock wherever the notes say so.*

### Exercise 1 — When to Use AI

The dataset is the commodity; the identification argument is the contribution. Use AI for the scaffolding around the argument, not the argument itself.

1. **Summarize a data dictionary.** Point an LLM at the Medicare Part D Prescriber PUF and Medicaid SDUD field lists and ask it to tell you which fields supply your outcome (branded vs. generic share for Cardizem-X's NDC family) and which are missing. *Why AI works here:* the data dictionaries are public and fixed, so every field claim is checkable against the documentation in minutes — you are verifying a lookup, not trusting a judgment.
2. **Generate event-study plotting code.** Ask for R or Python that draws the pre-trend leads and post-treatment lags around the loss-of-exclusivity date. *Why AI works here:* plotting code either runs and produces the diagnostic figure or it errors; correctness is visible the moment the plot renders and you read the pre-period leads yourself.

**The tell:** in both tasks the output is independently checkable — against a published data dictionary or against a figure that either renders the diagnostic or does not. You are not asking the model to decide whether the design identifies anything.

### Exercise 2 — When NOT to Use AI

1. **Choosing — and defending — the estimator under staggered adoption.** *Why AI fails here:* prompted to "run a staggered difference-in-differences," LLMs routinely return two-way fixed-effects code, because TWFE dominated the training corpus; under heterogeneous effects that estimator uses already-treated units as controls (the forbidden comparisons Goodman-Bacon 2021 formalized) and can be wrong in sign. The model reproduces the literature's old default, not the correct fix.
2. **Judging whether parallel trends or the exclusion restriction holds.** *Why AI fails here:* parallel trends is a claim about your drug's specific legislative or patent history, and the exclusion restriction is untestable by construction — both require reading the institutional context (why Cardizem-X's generic entered when it did) that the model does not have. It will pronounce "trends look parallel" from a description, which is exactly the wave-past the chapter warns against.

**The tell:** AI as *reason* vs. *tool* — if your design identifies a causal effect because the model said the assumption holds, AI has become the reason; it may only draft the code around an identification argument you make and defend. **Series connection:** these are **T7 Wisdom** judgments — the identifying assumption and the estimator choice are the contribution itself, and no collective or model can supply the "why is this causal rather than associated?" answer for your drug.

### Exercise 3 — LLM Exercise

**What you're building:** the identification-design memo for your drug's loss-of-exclusivity study — research question, dataset, design, identifying assumption in plain English, the falsification test stated first, and the honest Evidence Ladder ceiling.

**Tool:** Claude, continuing the **Claude Project** "One Drug — Cardizem-X" from Chapter 11. Persistent context helps because the drug, class, KPIs, and firewall ceiling are already loaded; the model can carry the Chapter 11 cheap test forward instead of re-deriving it.

**The Prompt:**

```
Continuing the One Drug project for Cardizem-X (branded cardiometabolic drug, two generic
competitors, one branded competitor, loss of exclusivity ~18 months out). I work only on
PUBLIC data: CMS Open Payments, Medicare Part D Prescriber PUF, Medicaid SDUD, ICER value
scores. Reference "AI-Driven Programmatic HCP Marketing," Chapter 12.

Help me draft an IDENTIFICATION-DESIGN MEMO for this question: "Does branded share for
Cardizem-X persist after generic entry more than a no-equity baseline would predict, after
controlling for ICER clinical value?" The loss-of-exclusivity date is a dated, exogenous
shock set by patent expiration and FDA generic approval.

Produce, in this order, FALSIFICATION FIRST:
1. The single diagnostic that would FALSIFY the design (state it before anything else):
   for a DiD, the pre-trend event-study leads; name what pattern kills the design.
2. The identification design you recommend (natural experiment / DiD, RDD, or IV) and WHY,
   given that loss of exclusivity is a dated shock. If staggered across drugs or states,
   specify Callaway-Sant'Anna group-time ATT with not-yet-treated/never-treated controls,
   NOT plain two-way fixed effects.
3. The comparison/counterfactual group.
4. The identifying assumption in plain English (one paragraph).
5. The two Part D / SDUD dataset limits I must state in the brief (e.g., no new-to-brand
   scripts; Medicare-only population; ecological aggregation in SDUD).
6. The Evidence Ladder level this public-data design can honestly reach, and why it cannot
   exceed it.

If you reach for an estimator, name it explicitly and say why it is heterogeneity-robust.
Flag any number you are unsure of with [verify].
```

**What this produces:** a falsification-first identification-design memo for your drug, ready to drop into the Chapter 13 portfolio card and stress-tested against the TWFE trap.

**How to adapt:** replace Cardizem-X and its loss-of-exclusivity shock with your own drug and policy shock (a state gift ban, a formulary tier change, a prior-authorization rule); the same prompt runs on ChatGPT or Gemini, but reset it with the firewall and dataset constraints each session if you lack a persistent Project.

**Connection to previous chapters:** the memo upgrades Chapter 11's "cheap test" into a defensible identification argument and keeps Chapter 11's Evidence Ladder ceiling; the ICER value control reaches back to the welfare-relevance thread the book has carried since Chapter 2.

**Preview of next chapter:** Chapter 13 turns this single design into one of four portfolio cards for your drug, with the pre-registered kill criterion made explicit in the seven-field card.

### Exercise 4 — CLI Exercise

**What you're building:** a pre-trends sanity check for your drug — download a public slice, plot the branded-vs-generic series around the shock, and decide *before any model* whether the trends look parallel.

**Tool:** **Claude Code** — why: this is a focused download-plus-plot task in one working directory with a clear stopping condition, the kind of single-thread analysis Claude Code runs cleanly; the multi-file Cowork workflow is overkill here. · **Skill level:** intermediate.

**Setup (3-item checklist):**
- A folder `cardizem-x-did/` with a `data/` and `figs/` subfolder.
- Python 3 with pandas and matplotlib (or R with ggplot2) installed.
- `CLAUDE.md` noting: public data only; the parallel-trends check happens before estimation; flag a pre-trend divergence as a design warning, do not model past it.

**The Task:**

```
In cardizem-x-did/, write a script that:
- READS only a public Medicaid SDUD extract I place in data/ (two states or two NDC groups:
  the Cardizem-X branded NDC family and its generic equivalent) — do not download anything
  beyond the SDUD slice I name;
- WRITES only into figs/;
- LEAVES everything else alone.

Plot the branded series and the generic series across the pre- and post-generic-entry
periods, with a vertical line at the loss-of-exclusivity date. Output figs/pretrends.png.

STOP after the plot is written. Do NOT fit any DiD or regression model — the point is the
pre-trend eyeball check before modeling. Print a one-line prompt asking me: "Do the
pre-entry trends look parallel? If not, the identifying assumption is in trouble."
VERIFY by opening figs/pretrends.png and confirming both series and the event line render.
Do not commit or push.
```

**Expected output:** `figs/pretrends.png` showing the two series and the loss-of-exclusivity line, plus the printed parallel-trends question.

**What to inspect:** the pre-entry leads — do branded and generic move together before the shock? A divergence before the date is the warning the chapter names, and it means the design is in trouble regardless of what a model would later report.

**If it goes wrong:** if the script tries to fit a model or fetch extra data, stop it: "remove the modeling step and the extra download; this task is the pre-trends plot only." Recovery is trivial — delete `figs/` and rerun; nothing left the folder.

**CLAUDE.md note:** add "Run and read the pre-trends event-study plot before fitting any DiD; a pre-trend divergence is a design failure, not a nuisance to control away."

### Exercise 5 — AI Validation Exercise

**What you're validating:** an LLM-generated DiD analysis plan for your drug (from Exercise 3, or a deliberately flawed one) for the TWFE trap and the parallel-trends defense.

**Validation type:** identification-and-estimator audit. **Risk level:** high — a TWFE estimate under staggered adoption can be wrong in sign and magnitude, so a brief built on it misleads the partner about your drug's persistence.

**Setup:** use your Exercise 3 memo, or generate a flawed artifact: ask the model to "write R code for a staggered DiD on Cardizem-X branded share across states with a single treated dummy and unit + year fixed effects" — it will likely hand you TWFE. Validate that.

**The Validation Task:**

```
Validation Checklist — Chapter 12 (Research Design / Public Data)
For the pasted analysis plan or code, mark each Pass / Fail / Cannot-determine:

- Correctness: does the design actually identify a causal effect, or is it association
  with controls?
- Completeness: identifying assumption stated, falsification diagnostic named, Evidence
  Ladder ceiling stated, dataset limits listed?
- Scope: public/synthetic data only; no partner-proprietary panel assumed?
- Chapter-specific 1 (Estimator integrity): under staggered adoption, is the estimator
  heterogeneity-robust (Callaway-Sant'Anna or peer) rather than plain two-way fixed effects?
- Chapter-specific 2 (Parallel-trends defense): is there a pre-trend event-study plot and a
  plain-English defense of why pre-entry trends should be parallel for this drug?
- Failure-mode check: does the plan commit TWFE BIAS (single treated dummy + unit/year FE
  under staggered timing) or FAILED PRE-TRENDS (leads not near zero, waved past)? Is it
  fluent-but-wrong — confident code that quietly uses forbidden comparisons?
- Ground truth: is the identifying assumption checkable against a named diagnostic, or is the
  ground truth missing?
```

**What to do with findings:** all pass — advance the memo to the Chapter 13 portfolio card. One fail — fix it (replace TWFE with Callaway-Sant'Anna; add the event-study plot) and re-validate. Multiple fails — send it back to Exercise 3; a plan that fails both estimator and pre-trends checks is not patchable in prose.

**AI Use Disclosure prompt:** *Write two sentences naming what an AI tool did in your Chapter 12 work and the one judgment it could not make — for example, that you used Claude to draft the Callaway-Sant'Anna code and summarize the Part D dictionary for Cardizem-X, but you decided yourself whether parallel trends were defensible given the drug's specific patent and entry history, because that judgment requires the institutional context the model does not have.* (Mandatory.)

**Series connection:** the failure mode is **TWFE bias / failed pre-trends**, and the validating judgment is **T7 Wisdom** — the identifying assumption and the estimator choice are the human contribution that the chapter exists to train.

---

## References (fact-check pass)

The following sources cited in this chapter were confirmed during the 2026-06-17 fact-check pass:

1. Larkin, I., et al. "Association Between Academic Medical Center Pharmaceutical Detailing Policies and Physician Prescribing." *JAMA* 317(17):1785–1795 (2017). — citation and all reported specifics (~1.7pp effect, 19 centers, 11 with all three elements, 8 of 11 significant) confirmed.
2. Goodman-Bacon, A. "Difference-in-Differences with Variation in Treatment Timing." *Journal of Econometrics* 225(2):254–277 (2021). — confirmed.
3. Callaway, B., & Sant'Anna, P. H. C. "Difference-in-Differences with Multiple Time Periods." *Journal of Econometrics* 225(2):200–230 (2021). — confirmed.
4. de Chaisemartin, C., & D'Haultfœuille, X. "Two-Way Fixed Effects Estimators with Heterogeneous Treatment Effects." *American Economic Review* 110(9):2964–96 (2020). — confirmed.
5. Sun, L., & Abraham, S. "Estimating Dynamic Treatment Effects in Event Studies with Heterogeneous Treatment Effects." *Journal of Econometrics* 225(2):175–199 (2021). — confirmed.
6. Borusyak, K., Jaravel, X., & Spiess, J. "Revisiting Event-Study Designs: Robust and Efficient Estimation." *Review of Economic Studies* 91(6):3253–3285 (2024). — confirmed.
7. Baker, A., Callaway, B., Cunningham, S., Goodman-Bacon, A., & Sant'Anna, P. H. C. "Difference-in-Differences Designs: A Practitioner's Guide." arXiv:2503.13323 (forthcoming *Journal of Economic Literature*). — confirmed.
8. McCrary, J. "Manipulation of the Running Variable in the Regression Discontinuity Design: A Density Test." *Journal of Econometrics* 142(2):698–714 (2008). — confirmed.
9. CMS Open Payments (Aug 2013–present, free, no DUA); Medicare Part D Prescriber PUF (2013–present, ~2-yr lag, no DUA, no NBRx, Medicare population); Medicaid SDUD; ICER Value Assessment Framework ($50k–$200k/QALY range; $100k–$150k value-based price benchmark). — all confirmed (cms.gov; medicaid.gov; icer.org).

