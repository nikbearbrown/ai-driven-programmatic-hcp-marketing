# Chapter 12 — Research Design and Public Data for Marketing Science

> Chapter 8 inverted your instinct: a good predictor is not a good
> intervention, because propensity is not incrementality. Chapter 11 told
> you the lab's higher rungs require a *credibly identified* test. This
> chapter supplies the designs — natural experiments, difference-in-
> differences, regression discontinuity, instrumental variables — that
> recover causal effects when a randomized holdout is impossible, which on
> public data it almost always is. And it maps the public-data stack to the
> questions each design can answer.

## 12.1 Chapter overview

By the end of this chapter you will be able to select an identification strategy for a research question given the public data available, state the assumption each design buys, name the diagnostic that would falsify it, and place the result on the Evidence Ladder. The chapter's organizing claim is that, on public data, **the contribution is the identification argument, not the dataset.** Open Payments and Part D are commodities; what makes a finding causal is the structure — a policy shock, a threshold, an instrument — you layer on top.

## 12.2 Learning objectives

By the end of this chapter you will be able to:

1. **(Apply)** Select an identification strategy for a question given available public data.
2. **(Analyze)** Evaluate the identifying assumptions each design requires against the pharma context.
3. **(Create / Part B)** Design a credibly identified study for your own thread on public data.

## 12.3 Opening case: a state turns off detailing, and a natural experiment appears

A state enacts a physician gift ban on a known date. The neighboring states do not. Overnight, the state's prescribers are "treated" — they can receive far less commercial promotion — while across the border, prescribers continue as before. A Fellow can compare the change in branded-drug share among the state's prescribers (Medicare Part D plus Medicaid State Drug Utilization Data) to the change among neighbor-state prescribers over the same window. The neighbor states supply the counterfactual: what the treated state's prescribing *would have done* absent the ban.

This is the workhorse of public-data pharma research — a natural experiment — and it has a published exemplar. Between 2006 and 2012, nineteen academic medical centers across five states restricted pharmaceutical-rep detailing visits, mostly meal and gift bans. Larkin, Loewenstein, and colleagues used a difference-in-differences/event-study design on physician prescribing and found the restrictions *caused* a shift away from detailed branded drugs toward cheaper generics — 8 of 11 centers that prohibited visits and gifts saw significant reductions in detailed-drug prescribing, versus 1 of 8 that did not restrict (Larkin et al., *JAMA* 317(17):1785–1795, 2017). A dated, plausibly exogenous access rule; non-restricting controls; a clean prescribing outcome. That is the template, and the rest of the chapter is how to build and stress-test it.

## 12.4 Prerequisites

You should carry the propensity-vs-incrementality inversion and the holdout ideal from Chapter 8 (these designs *substitute* for a holdout when none is possible), the evidence frame from Chapter 5 (these designs are the *answer* to "association ≠ causation"), the claims-lag constraint from Chapter 3 (it lives in the data here too), and the Evidence Ladder and firewall from Chapter 11 (public-data designs top out around Level 3).

## 12.5 Core sections

### 12.5.1 The identification problem

The fundamental problem of causal inference is that for any unit you observe either the treated or the untreated outcome, never both. Every identification strategy is a different argument for how to *impute the missing counterfactual* from observable units. Natural experiments find a treatment assignment that is "as good as random" with respect to the outcome; difference-in-differences imputes the counterfactual trend from a control group; regression discontinuity imputes it from units just across a threshold; instrumental variables impute it from variation driven by an instrument that touches the outcome only through the treatment.

The misconception to kill first: *"with enough controls in a regression, I have a causal estimate."* No. Controlling for *observed* confounders does nothing about *unobserved* ones — physician quality, patient mix, local market dynamics. The designs below are valuable precisely because they neutralize unobserved confounding through *structure* — a policy shock, a threshold, an instrument — not through a longer covariate list (`_lib_ai-applied-causal-inference-powered-by-ml-and-ai.md`; `_lib_math-causal-inference-mit-press-essential-knowledge-series.md`).

### 12.5.2 Natural experiments

A natural experiment exploits a real-world event that assigns "treatment" to some units and not others in a way plausibly unrelated to the outcome. In HCP marketing the recurring sources are:

- **State detailing/disclosure and gift-ban laws** — Minnesota (gift disclosure since 1993; gift cap), Vermont (2009 gift ban plus disclosure), and others create cross-state variation in how much promotion physicians may receive.
- **Academic-medical-center detailing-access rules** — the 2006–2012 wave of rep-visit restrictions; physicians at restricting centers are treated, others are controls. This is the Larkin design (§12.3).
- **Formulary changes** — a payer moving a drug across tiers, or imposing/removing prior authorization, shifts the friction a physician faces at known dates.
- **Loss of exclusivity (LOE) / generic entry** — a dated, exogenous economic shock that changes substitution economics overnight; a clean event for studying brand-equity persistence (§12.5.6).

The misconception: *"any before/after comparison is a natural experiment."* No — the assignment must be plausibly *exogenous* to the outcome trend. A policy adopted *because* prescribing was already changing is endogenous and invalidates the design. Always ask: why did *these* units get treated *when* they did, and is that reason correlated with the outcome? An early disclosure-law study found such laws changed reporting but did little to behavior (Ross et al., *JAMA*, 2007), a useful reminder that "treatment" must be the thing you think it is.

### 12.5.3 Difference-in-differences, including staggered adoption

Difference-in-differences (DiD) compares the *change* in outcome for a treated group to the *change* for a control group across a pre/post boundary. The double-differencing removes any time-invariant difference between groups and any common time shock. The identifying assumption is **parallel trends**: absent treatment, the treated group's outcome would have evolved along the same path as the control's. Under parallel trends, DiD identifies the **Average Treatment effect on the Treated (ATET)**.

The clean 2×2 case (two groups, two periods) is rare in policy data. The realistic pharma case is **staggered adoption**: units adopt the policy at different dates (academic centers restricting detailing across 2006–2012; states passing gift laws in different years). Here lies the chapter's most important "do it right" lesson. The naive fix — a two-way fixed-effects (TWFE) regression with unit and time fixed effects and a treatment dummy — is now known to be **biased under heterogeneous treatment effects**, because it uses *already-treated* units as controls for *later-treated* units ("forbidden comparisons"; the Goodman-Bacon decomposition, 2021). The estimate can be wrong in *sign and magnitude*.

The modern fix is a heterogeneity-robust estimator that builds clean group-time treatment effects using only never-treated or not-yet-treated units as controls: **Callaway & Sant'Anna (2021)** (*Journal of Econometrics* 225(2):200–230; the `did` R package), with de Chaisemartin & D'Haultfœuille (2020/2022), Sun & Abraham (2021), and Borusyak et al. as alternatives — collectively the post-2020 "DiD revolution." Any Fellow DiD on staggered policy adoption that still uses plain TWFE is dated and likely biased.

Three diagnostics are required: (a) an **event-study / pre-trends plot** (the leads should be near zero); (b) awareness that parallel trends is *functional-form dependent* — parallel trends in levels need not hold in logs, so the outcome transformation is a real modeling choice; and (c) reporting the estimator and the comparison group (never-treated vs. not-yet-treated). King et al. (2013) is a published, citable DiD on medical-school gift-restriction policies and reduced prescribing of newly marketed psychotropics (PMC3623604).

### 12.5.4 Regression discontinuity design (RDD)

RDD exploits a rule that assigns treatment based on whether a continuous "running variable" crosses a **threshold**. Units just below and just above the cutoff are nearly identical except for treatment status, so the jump in outcome at the cutoff identifies a local causal effect (a LATE at the threshold). Pharma/health thresholds that make RDD viable:

- **The Medicare Part D coverage-gap ("donut hole") spending threshold** — out-of-pocket cost jumps when cumulative spending crosses the gap entry point, and utilization, discontinuation, and switching change sharply (Polinski et al., 2011; PMC3156689).
- **Low-Income Subsidy (LIS) eligibility income threshold** — beneficiaries just above vs. below the income cutoff face different out-of-pocket costs; used to estimate the price elasticity of adherence (PMC7741637).
- **Formulary tier / prior-authorization thresholds** — coverage rules that flip at a defined criterion.

The misconception: *"RDD needs a randomized component."* No — it needs a *sharp, externally enforced cutoff* and a smooth running variable; identification comes from continuity of potential outcomes at the cutoff. The key threat is **manipulation/sorting** around the threshold — test with a density (McCrary) check — plus any confounder that *also* jumps at the same cutoff.

### 12.5.5 Instrumental variables (IV)

When treatment is endogenous (chosen, not assigned) and no clean natural experiment exists, an **instrument** Z can recover a causal effect if it (1) is *relevant* (predicts the treatment), (2) satisfies the *exclusion restriction* (affects the outcome only through the treatment), and (3) is *as-good-as-randomly assigned*. IV estimates a LATE — the effect for "compliers" whose treatment status responds to the instrument. In public-data pharma-marketing work, candidate instruments are scarce and the exclusion restriction is usually the hard sell; plausible families include geographic or temporal variation in promotion exposure driven by something exogenous (rollout order, distance to a detailing hub) — each defended case by case.

The misconception: *"any variable correlated with treatment is an instrument."* No — relevance is testable (report the first-stage F; weak instruments bias the estimate toward OLS), but the exclusion restriction is *fundamentally untestable* and must be defended on substantive grounds. IV is the design most easily abused; flag it for heavy scrutiny in any Fellow brief. (IV and DML-for-first-stages are treated at length in `_lib_ai-applied-causal-inference-powered-by-ml-and-ai.md`.)

### 12.5.6 A worked design family: LOE as a brand-persistence natural experiment

Loss of exclusivity is the cleanest dated shock in the data. At LOE, small-molecule brands typically erode steeply via generic substitution; the generic-entry date is exogenous and known. That makes LOE a natural experiment for a brand question the book cares about: *does brand equity slow erosion after controlling for clinical value?* Pair Part D prescriber data (the outcome — branded share over time) with ICER value scores (the clinical-value covariate). A persistence effect *net of value* is evidence of equity; no effect once value is controlled is evidence that "loyalty" was really clinical value all along (`pharma-brand-measurement-synthesis.md` §4).

### 12.5.7 The public-data stack

The designs are nothing without data. Four public sources carry most of the load. **Lead with the design, not the dataset** — but know precisely what each dataset contains, its coverage, its access, and its limits.

| Dataset | What it contains | Coverage | Access | Questions it supports |
|---|---|---|---|---|
| **CMS Open Payments** | Industry transfers of value to physicians and teaching hospitals — three record types (general payments, research payments, ownership/investment). Payer name, amount, date, nature of payment, drug/device, recipient NPI. | First published Sept 2014 (covering Aug–Dec 2013); annual since. 2013–2017 on the Archived page; 2018–present in the search tool / bulk download. `[verify latest year]` | Free download + API (openpaymentsdata.cms.gov); no DUA. | The promotion "dose" at the physician level. Pair with Part D for payment→prescribing studies. **Association-grade alone** (see §12.8). |
| **Medicare Part D Prescriber PUF** | Drugs prescribed per provider under Part D: NPI, drug brand+generic, total claims, 30-day fills, beneficiary counts, total cost. Built from Prescription Drug Event records. | CY 2013–present, annual; ~2-year lag. `[verify latest year]` | Free download + interactive (data.cms.gov); no DUA. | The **outcome variable** for most lift/attribution and brand-persistence work. **Does not directly observe NBRx / new starts** (see §12.8); Medicare population skew. |
| **Medicaid State Drug Utilization Data (SDUD)** | State Medicaid outpatient drug utilization by NDC: units reimbursed, prescriptions, amounts reimbursed, by year+quarter, by state. | Since the Medicaid Drug Rebate Program's start; current public files recent years, quarterly. `[verify latest year]` | Free download (data.medicaid.gov); no DUA. | The **state × time** outcome panel — ideal for state-policy natural experiments and LOE substitution. NDC×state×quarter (no physician identity); complements, does not replace, Part D. |
| **ICER value assessments** | Independent clinical + cost-effectiveness reports: QALY/evLYG cost-effectiveness ratios, value-based price benchmarks, evidence ratings. Flags <$50k/QALY high-value, >$175k/QALY low-value (thresholds `[verify]` current). | Per-drug/condition reports, rolling; draft → comment → revised. | Free public PDFs (icer.org); requires structured extraction. | The **clinical-value covariate** — test brand equity / promotion *against* independent value. |

### 12.5.8 A decision tree from question to design

- A policy adopted at *different dates* across units → **staggered DiD** (Callaway–Sant'Anna, with an event-study plot).
- A single dated shock with a clean control group → **2×2 DiD / event study** (the opener).
- A *sharp eligibility or spending cutoff* → **RDD** (with a density test).
- An *exogenous shifter of exposure* with a defensible exclusion restriction → **IV** (with first-stage F).

Make yourself justify the *assumption* each design buys — parallel trends, continuity at the cutoff, the exclusion restriction — and name the diagnostic that would falsify it. That justification is the contribution.

## 12.6 Worked example: the staggered gift-ban study, done wrong then right

**Process.** A Fellow studies staggered state gift bans, predicting they reduce branded share.

1. *Naive attempt.* Run a TWFE regression — state and year fixed effects, a treatment dummy — and read off a single coefficient: a plausible-looking negative number. Ship it? No.
2. *The trap.* Because the bans were adopted in different years and the effect plausibly varies by cohort and over time, TWFE uses *already-banned* states as controls for *later-banned* states. Those "forbidden comparisons" can bend the estimate in sign and magnitude (Goodman-Bacon).
3. *The fix.* Re-estimate with a Callaway–Sant'Anna group-time ATT using not-yet-treated controls, and produce an event-study plot. The pre-trend leads sit near zero (good); the post-treatment path shows the real, heterogeneity-robust effect — which differs from the TWFE number.
4. *Place it.* This is a small offline causal test on public data — Evidence Ladder **Level 3**. It cannot reach client-validated impact (Level 5); that needs the partner's proprietary panel (Stage 2, across the firewall).

**Lesson.** Same data, same question — the *estimator* changed the answer. The Fellow's contribution was the identification discipline, not the dataset.

**Limit.** Part D's ~2-year lag bounds how recent the window can be; the Medicare population skew limits generalization to the commercially insured (where coupons operate); and SDUD's NDC-level aggregation means no physician-level mechanism. State all three in the brief.

## 12.7 Common misconceptions

- **"Enough control variables make a regression causal."** Controls handle *observed* confounders only. Structure (shock, threshold, instrument) is what neutralizes the unobserved ones.
- **"Any before/after is a natural experiment."** Only if the assignment is plausibly exogenous to the outcome trend. Endogenous adoption invalidates it.
- **"Run TWFE and you've done staggered DiD."** TWFE is biased under heterogeneous effects. Use Callaway–Sant'Anna (or a sibling) and show pre-trends.
- **"RDD needs randomization."** It needs a sharp, enforced cutoff and a smooth running variable; watch for sorting at the threshold.
- **"A correlated variable is an instrument."** Relevance is testable; the exclusion restriction is not — defend it substantively or don't use IV.
- **"Open Payments + Part D = a causal pipeline."** Alone they yield associations. The design layered on top is what makes it causal.

## 12.8 Evidence check

- **Peer-reviewed exemplars:** Larkin et al., *JAMA* 2017 (AMC detailing restrictions); King et al., 2013 (gift-restriction DiD, PMC3623604); Dafny, Ody & Schmitt, *AEJ: Economic Policy* 2017 (copay coupons raise branded sales 60%+ by suppressing generic substitution; NBER w22745 — confirm whether the chapter cites w22745 or the later w29735 update, and the exact effect sizes `[verify]`); Polinski et al., 2011 (Part D coverage-gap RDD).
- **Methods canon:** Callaway & Sant'Anna (2021); Goodman-Bacon (2021); de Chaisemartin & D'Haultfœuille (2020/2022); Sun & Abraham (2021).
- **Dataset limits (flag in every brief):** **Open Payments is association-grade alone** — payment↔prescribing correlation is real and replicated but confounded; a causal claim needs a design. **Part D does not directly observe NBRx / new starts** — new-to-brand is a longitudinal-patient construct; Fellows must *proxy* new starts and label them as proxies. **Medicare/Medicaid population skew** limits external validity to the commercially insured.
- **`[verify]`:** latest published year for Open Payments / Part D PUF / SDUD; current ICER $/QALY thresholds; the Gleevec/CML price-elasticity RDD's peer-review status (arXiv 2305.06076 — do not cite as established until confirmed).

## 12.9 Compliance and patient-welfare check

These designs are methodologically neutral, but they are also the tools that expose welfare-relevant findings — the coupon studies show copay coupons can *raise* total spending by suppressing generic substitution (Dafny et al.), and the same machinery can test whether targeting encodes susceptibility proxies. Any such finding is **routed to medical/legal/regulatory and compliance counsel**, framed as collaborative de-risking, with the partner signing off on pointed framing (Chapter 11). The patient-welfare question — does a promotion effect serve the patient or merely branded volume? — is a required field in any brief built on these methods.

## 12.10 Exercises

1. **(Understand)** For each of the four designs, state the identifying assumption in one sentence and the single diagnostic that would falsify it.
2. **(Apply)** Given a question — "did a 2019 state prior-authorization change reduce a brand's share?" — pick a design, name the dataset(s), and justify the assumption it buys.
3. **(Apply+ / Analyze)** Take a published payment→prescribing *association* finding. Explain why it is not causal, and design the natural experiment or RDD that would make it causal on public data — naming the Evidence Ladder level it could reach.
4. **(Create / Part B — produce)** Write the **identification-design memo** for your own thread: question, dataset(s), design, the identifying assumption stated explicitly, the diagnostic that would falsify it, and the Evidence Ladder level it can reach.

## 12.11 Five-part AI exercise block

1. **When to use AI:** drafting an analysis plan, generating event-study plotting code, summarizing a dataset's data dictionary, suggesting candidate instruments to *then* scrutinize.
2. **When NOT to use AI:** judging whether the exclusion restriction holds, deciding whether pre-trends are "close enough" to zero, or accepting AI-generated DiD code without checking the estimator.
3. **LLM exercise:** ask a model to "draft a staggered difference-in-differences analysis plan and code for state gift bans on Part D data."
4. **CLI / code exercise:** run the code it gives you against a small public extract and produce the event-study plot.
5. **AI-validation exercise (load-bearing):** inspect the code from #3. If it handed you a plain TWFE regression — which models frequently do — catch it, and replace it with a heterogeneity-robust estimator (Callaway–Sant'Anna) plus a pre-trends check. The catch *is* the human judgment the chapter trains.

## 12.12 AI Use Disclosure (Part B)

Name the judgment in your identification-design memo that the AI could not make: whether the design's assumption is *defensible* in your pharma context, whether the pre-trends/diagnostic actually passes, or whether the public-data result generalizes past the Medicare/Medicaid skew. Naming it earns the Part B bonus.

## 12.13 What would change my mind

If a credible public dataset emerged with linked patient-level new-start and commercially insured data — closing the NBRx and population-skew gaps — then more brand-persistence and lift questions could be answered directly on public data, raising the public-data ceiling above Level 3. Today no such public dataset exists; the proprietary panels that have it sit on the partner's side of the firewall.

## 12.14 Still puzzling

The most policy-relevant promotion effects operate on the *commercially insured* population — where coupons work and where most branded volume lives — but the cleanest public outcome data (Part D, SDUD) is Medicare and Medicaid. Every public-data finding therefore carries an external-validity asterisk pointing at exactly the population that matters most. Can a clever design bridge that gap, or is the commercial-population effect structurally invisible to public data? The book leaves this open.

## 12.15 Summary

You can now choose an identification strategy from the question and the available public data, state the assumption it buys and the diagnostic that would falsify it, and avoid the staggered-DiD trap by using a heterogeneity-robust estimator with an event-study plot. You know the four-dataset public stack — Open Payments, Part D Prescriber, Medicaid SDUD, ICER — what each contains, its coverage and access, and its limits: Open Payments is association-grade alone, Part D does not directly observe new starts, and Medicare/Medicaid skew bounds generalization. And you can place any public-data design on the Evidence Ladder, where it tops out around Level 3.

## 12.16 Key terms

- **Identification** — the argument for how to impute the missing counterfactual from observable units.
- **Natural experiment** — an event that assigns treatment plausibly unrelated to the outcome.
- **Difference-in-differences (DiD)** — comparing the change in a treated group to the change in a control; identifies the ATET under parallel trends.
- **Parallel trends** — the DiD assumption that, absent treatment, treated and control would have moved together; functional-form dependent.
- **Staggered adoption / TWFE bias** — units treated at different dates; plain two-way fixed effects is biased under heterogeneous effects ("forbidden comparisons").
- **Callaway–Sant'Anna estimator** — a heterogeneity-robust DiD using not-yet-treated/never-treated controls.
- **Regression discontinuity (RDD)** — identifies a local effect at a sharp threshold via continuity of potential outcomes.
- **Instrumental variable (IV)** — recovers a complier (LATE) effect via an instrument satisfying relevance and the (untestable) exclusion restriction.
- **Open Payments / Part D PUF / SDUD / ICER** — the public-data stack: promotion dose, prescribing outcome, state×time panel, and clinical-value covariate.

## 12.17 Bridge

You have the designs and the data. Now run one. Chapter 13 puts you inside the Fellow research portfolio — choosing a track (lift, brand, models, or ethics), executing one low-cost project end to end on public data, scoring the evidence, flagging the risk, and producing the plain-language readout a partner decision-maker can act on.

## 12.18 Further reading

- Larkin, I., Loewenstein, G., et al. (2017). *Association Between Academic Medical Center Pharmaceutical Detailing Policies and Physician Prescribing.* JAMA 317(17):1785–1795. The opener's real study; the template natural experiment.
- Callaway, B., & Sant'Anna, P. (2021). *Difference-in-Differences with Multiple Time Periods.* Journal of Econometrics 225(2):200–230. The heterogeneity-robust staggered-DiD standard (`did` package).
- Dafny, L., Ody, C., & Schmitt, M. (2017). *When Discounts Raise Costs: The Effect of Copay Coupons on Generic Utilization.* AEJ: Economic Policy 9(2):91–123 (NBER w22745 — confirm vintage `[verify]`). Cross-state legality as the design; the welfare-relevant coupon result.
- Polinski, J. M., et al. (2011). *Changes in Drug Utilization during a Gap in Insurance Coverage.* (Part D coverage-gap RDD; PMC3156689.)
- *Applied Causal Inference Powered by ML and AI* (`_lib_ai-applied-causal-inference-powered-by-ml-and-ai.md`). The methods workhorse: DiD/ATET, IV, RDD, and DML for high-dimensional first stages.
- CMS Open Payments (openpaymentsdata.cms.gov), Medicare Part D Prescriber PUF (data.cms.gov), Medicaid SDUD (data.medicaid.gov), ICER (icer.org) — the public-data stack, with data dictionaries.
