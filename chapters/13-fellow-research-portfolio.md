# Chapter 13 — The Fellow Research Portfolio (Run One)

## 1. Chapter overview

By the end of this chapter you will be able to take one research idea — your own thread, or one drawn from the lab's standing menu — and run it all the way through on **public data**: state the question, name the dataset and a synthetic fallback, choose an identification strategy you can defend, pre-register a **success threshold and a kill criterion**, place the result on the Evidence Ladder, flag the compliance and patient-welfare exposure, and write a plain-language readout that a non-technical partner decision-maker could act on. This is the chapter where the toolkit (Acts One and Two) and the lab model (Chapter 11) and the identification strategies (Chapter 12) stop being vocabulary and become a finished artifact. The work is organized into four research **tracks** — Lift and attribution, Brand and physician identity, Model architecture and segmentation, and Privacy, fairness, and accountability — and the chapter walks each one with at least one fully specified, runnable project. The discipline you are training is not cleverness. It is honesty: a project that ends in a defensible "no" is a successful project, because it has reduced the partner's uncertainty about where to spend.

## 2. Learning objectives

By the end of this chapter you will be able to:

1. **(Create)** Run a portfolio project end to end on public or synthetic data — from question to scored result.
2. **(Evaluate)** Score the evidence honestly against the Evidence Ladder and flag the compliance and patient-welfare risk it carries.
3. **(Create / Part B)** Produce the result plus a plain-language readout for a partner decision-maker, using the seven-field project card the portfolio enforces.

## 3. Opening case — the company wants ideas worth resourcing, not paper summaries

A Fellow finishes her first portfolio cycle and brings three things to the lab review. The first is a four-page literature summary on next-best-action models in pharma, well-organized and accurately cited. The second is a slide that says "MoE platforms claim 4–44% script lift" with the range pulled from vendor decks. The third is a notebook she half-built, then abandoned because "the data didn't really let me answer it."

The lab lead reads all three and asks one question: "If I hand any of these to Graham's data-science team on Monday, what would they *do* with it?"

Silence. The summary is true and useless — it tells the partner what the field already says about itself. The slide repeats a vendor claim the book's entire thesis is built to distrust. The abandoned notebook is the only one that was trying to do real work, and she killed it for the right instinct (the data wouldn't support the claim) but the wrong reason (she treated "the data won't let me prove the strong version" as failure, when it is itself the finding).

The lesson lands hard because it inverts the academic reflex. A graduate seminar rewards the comprehensive review. The lab does not. The lab is an *external-innovation function*: its only product is reduced uncertainty about where the partner should commit proprietary data and engineering. A paper summary reduces no uncertainty. A reproduced vendor claim reduces no uncertainty — it launders one. The abandoned notebook, *rewritten as "here is what public data can and cannot establish about this claim, here is the design that would settle it, and here is the level of evidence I reached,"* reduces a great deal of uncertainty. The company wants ideas worth resourcing, not paper summaries. This chapter is about producing the third thing on purpose.

## 4. Prerequisites

You should arrive able to:

- Place an artifact on the **Evidence Ladder** (Chapter 11) and state why public-data work tops out around Level 3.
- Convert a research finding into a falsifiable hypothesis tied to a KPI (Chapter 11).
- Select an **identification strategy** — natural experiment, difference-in-differences with staggered adoption, regression discontinuity, instrumental variables — and name its identifying assumption (Chapter 12).
- Locate and load the **public-data stack**: CMS Open Payments, Medicare Part D Prescriber data, Medicaid State Drug Utilization Data (SDUD), ICER value reports (Chapter 12).
- Distinguish **propensity from incrementality** (Chapter 8) and **lift from brand** (Chapter 2).
- Build and honestly evaluate a **gradient-boosted tree baseline** (Chapter 6) and tell genuine MoE from relabeled stacking (Chapter 7).
- Use an LLM for extraction and scanning *with* a validation harness (Chapter 10).

## 5. The portfolio and its discipline

Every project in this portfolio ships the same **seven-field card**, and your Part B project must ship it too:

| Field | What it answers |
|---|---|
| **Question** | The falsifiable claim, tied to lift or brand. |
| **Public dataset (+ synthetic fallback)** | What you ran on, and what you'd simulate if access fails. |
| **Identification strategy** | How you impute the missing counterfactual (or: why this is a benchmark/audit, not a causal claim). |
| **Success threshold + kill criterion** | Pre-registered: what result would justify a handoff, and what result would make you walk away. |
| **Evidence-Ladder level reached** | The honest level — and why public data caps you there. |
| **Compliance + patient-welfare flags** | MLR / fair-balance / Sunshine / HIPAA exposure, and the welfare question, both *flagged and routed*, never adjudicated. |
| **Likely partner owner** | Who on the partner side would receive this if it advances. |

Two rules govern the whole card. First, the **kill criterion is pre-registered** — you write down what would make you abandon the project *before* you see the result, so that a disappointing finding cannot be quietly relabeled as a success. This is the antidote to the vendor-deck culture the book exists to push against. Second, the **Evidence-Ladder ceiling is the firewall made operational**. A Fellow on public data reaches roughly Level 3 (a small offline test that beats a baseline). Levels 4–6 — prospective pilot, client-validated impact, monitored deployment — require the partner's proprietary data and live inside the partner's walls. If your card claims Level 4 on Open Payments and Part D, you have either misunderstood the ladder or broken the firewall.

**A note on the standing blocker.** Two of the four tracks below — Track A (which shows vendor lift is inflated) and Track D (proxy discrimination, coupon suppression) — produce findings that critique the partner's own products at the moment the partner is deciding whether to spend. Whether the lab is *allowed* to run these as written, and who signs off on their framing, is **not settled** [contested — see pantry, Risk 1 / Open Question 1]. The honest posture, carried throughout, is **collaborative de-risking**: you are testing the partner's own claims so the partner does not get caught believing them. That framing is a working assumption, not a resolved agreement, and you should treat it as an open blocker rather than a green light.

## Core sections — walking the four tracks

### 5.1 Track A — Lift and attribution (likely owner: measurement analytics)

**The logic.** This track attacks the field's largest open methodological problem. Industry script-lift figures (4–44%) are *all vendor-generated* — no independent academic literature validates the causal attribution models behind them (`pharma-ai-hcp-marketing-synthesis.md` §1, §8). They are structurally inflated by **attribution circularity** (the platform that serves the ad also measures the lift on the same NPI data) and by selection: targeting concentrates on high-decile prescribers who both get targeted *and* prescribe anyway, so exposed-vs-unexposed confounds the ad's effect with the propensity that earned it (the Chapter 8 inversion as a measurement problem). The Fellow's job is not a better lift number but to **show, on public data, how much of a naive estimate is selection**, and to specify what a credibly identified estimate would require.

**Three projects:**

- **A1 — Script-lift attribution audit.** Reconstruct a vendor-style "lift" estimate (exposed-vs-unexposed, no control) using Open Payments as a promotion-dose proxy and Part D as the prescribing outcome, joined on NPI. Then re-estimate with a credible design — matching plus an explicit Rosenbaum-style sensitivity analysis, and difference-in-differences where a dated policy shock exists — and *quantify the gap*. The deliverable answers: "how much of the headline lift is selection?"
- **A2 — EHR / point-of-care natural experiment.** No peer-reviewed randomized study exists for point-of-care or EHR advertising — the single largest validation gap in the field (`pharma-marketing-evidence-synthesis.md` §3, which cites vendor-sourced 19–25% EHR lift with no independent confirmation). On public data the Fellow cannot observe EHR exposure at all, so this is *design-grade*: specify the natural experiment that *would* identify point-of-care lift (a health-system exposure on/off rollout, for example), run a power and simulation analysis showing the sample and design a real pilot would need, and hand the partner the artifact that justifies running one. This tops out at Level 2 — and saying so plainly is the point.
- **A3 — Omnichannel attribution decomposition.** Using Part D plus Open Payments, decompose observed prescribing change into promotion channels (meals, payments, timing) with an honest accounting of what *cannot* be separated without exposure-level data. The contribution is showing the identification ceiling of public data, not pretending past it.

#### Worked project A1 (Track A exemplar)

- **Question:** How much of a vendor-style script-lift estimate is causal, and how much is selection?
- **Dataset:** Open Payments (promotion dose per NPI) + Medicare Part D Prescriber (prescribing outcome per NPI), joined on NPI. Synthetic fallback: simulate exposure correlated with a latent prescribing propensity, so the "true" effect is known and the selection inflation can be measured directly.
- **Identification:** First estimate the naive exposed-vs-unexposed difference (no control). Then re-estimate via matching plus Rosenbaum sensitivity analysis, and — where a dated state policy shock is available (a gift ban, an AMC detailing restriction; see Larkin et al. 2017 [verify effect sizes], Chapter 12) — a heterogeneity-robust difference-in-differences (Callaway & Sant'Anna 2021 [verify]). Report the gap between the naive and design-based estimates.
- **Success threshold:** A reportable, defensible quantification of the selection inflation — the naive lift exceeds the design-based estimate by a margin you can put a confidence interval around.
- **Kill criterion:** No identifying variation and no credible counterfactual → downgrade to a design-only memo (which is still a result: "public data cannot settle this; here is what would").
- **Evidence-Ladder level:** L2–L3.
- **Compliance + welfare flags:** None acute. The *finding itself* — that lift is inflated — is partner-sensitive (Risk 2); frame it as de-risking the partner's own attribution claims, not as an accusation.
- **Likely owner:** Measurement analytics.

**The failure mode to teach.** The tempting mistake is to report the matched estimate as "the causal effect." Matching only adjusts for *observed* confounders; unobserved physician propensity still contaminates the comparison. The honest version reports a residual-confounding *sensitivity* — "an unobserved confounder of strength Γ would be needed to explain away this effect" — rather than a single point claim. A Fellow who writes "we found the true lift is 12%" has reproduced the vendor's sin with better tools.

### 5.2 Track B — Brand and physician identity (likely owner: brand strategy)

**The logic.** Brand equity in pharma is not name awareness — it is the physician remembering the **patient type** ("for *this* patient, after *this* prior therapy, Brand X is my default"; `pharma-brand-measurement-synthesis.md` §3). The book's spine asks whether AI-driven promotion builds *durable association* or buys *short-lived engagement*. This track tests the qualitative industry claims (mind-share leads market share; equity tracks value) with public data and dated natural experiments. The hard constraint: public data sees *behavior* (prescribing) well and *attitudes* poorly, so several B projects must **proxy equity from behavioral persistence** and label the proxy honestly.

**Four projects:**

- **B1 — SOMi→SOMa predictive validity.** Test whether share-of-mind (SOMi, attitudinal) predicts later share-of-market (SOMa, behavioral) with a lag. This is the industry's central leading-indicator claim — asserted qualitatively, *not* rigorously tested on linked survey-plus-claims data, and therefore an **open research question, not an established fact** [contested — see pantry]. The public-data version proxies SOMi from a public attention signal (literature or CME mentions, journal indices) and tests lagged prediction of Part D share. The proxy is weak; be honest that this may top out at L2.
- **B2 — Prescribing-habit durability across therapeutic classes.** Measure how persistent branded-prescribing patterns are across classes (chronic vs. acute, high-risk vs. easily substitutable) using Part D panels. This operationalizes "habit" and shows where equity is *structurally* durable versus fragile.
- **B3 — Brand-equity vs. ICER clinical-value correlation.** Test whether brand equity or promotion intensity predicts prescribing persistence *after controlling for ICER clinical-value score*. An **uncorrelated** finding — equity sustained on low-value drugs — would be a high-impact policy result. Whether brand equity tracks clinical value is **genuinely open and empirical** [contested — see pantry]; this project is designed to test it, not to assert the answer.
- **B4 — LOE persistence as a natural experiment.** Generic-entry date is exogenous and dated. Estimate how much branded share persists after loss of exclusivity, and whether persistence correlates with pre-LOE equity or promotion after controlling for market type and clinical value, using a difference-in-differences / event study around entry (`pharma-brand-measurement-synthesis.md` §4).

#### Worked project B3 (Track B exemplar) — brand-equity vs. ICER

- **Question:** Does brand equity / promotion predict prescribing persistence after controlling for independent clinical value?
- **Dataset:** ICER reports (clinical-value score, extracted with LLM assistance *and validated* per Chapter 10) + Part D (branded-share persistence) + Open Payments (promotion intensity).
- **Identification:** Persistence regressed on equity/promotion, conditioning on ICER value plus market controls; the headline is the *partial* association of equity net of value. This is associational by design — flag it. The LOE event-study (B4) is the stronger causal companion.
- **Success threshold:** Equity predicts persistence with clinical value held constant → equity functions as "commercial memory, not clinical value" (a high-impact finding).
- **Kill criterion:** The equity effect vanishes once value is controlled, *or* ICER coverage is too sparse for the drug set to support the regression.
- **Evidence-Ladder level:** L2 (associational); L3 when paired with the LOE event-study.
- **Compliance + welfare flags:** An equity-not-value finding *is* a patient-welfare finding — the system pays a premium for non-superior drugs. Route the framing carefully.
- **Likely owner:** Brand strategy.

**The failure mode to teach.** Treating ICER's value score as ground truth. ICER's QALY methodology is contested (disability and equity critiques; industry pushback), and — more subtly — drugs that reach ICER review are a *selected set*: the most-promoted, most-contested drugs are exactly the ones ICER evaluates. Conditioning on a covariate that is itself selected by the treatment is a trap. The honest version flags the QALY controversy *and* the selection-into-review problem, and treats ICER as one value benchmark among several, not as truth.

### 5.3 Track C — Model architecture and segmentation (likely owner: data science)

**The logic.** Vendors label tabular targeting stacks "Mixture of Experts." The book's established position (Chapter 7, `moe-vs-ensemble-synthesis.md`): on medium-sized tabular data, gradient-boosted tree ensembles are state of the art (Grinsztajn et al., NeurIPS 2022 [verify]), and most "MoE" platforms are stacked ensembles relabeled — legitimate ML, but not MoE, and not obviously better than a tuned ensemble. Genuine MoE means token-level routing, a shared trunk, and joint end-to-end training; a tabular NPI-propensity stack has none of the conditions that make those pay off. These projects produce *benchmark* and *audit* evidence the partner's data-science team can act on directly.

**Three projects:**

- **C1 — Ensemble-vs-genuine-MoE benchmark on NPI propensity.** *(The TIKTOC worked example.)* Build a calibrated XGBoost/LightGBM baseline on a public NPI-propensity task constructed from Part D + Open Payments + specialty features, and compare a routed / MoE-style model.
- **C2 — "Natural N" physician archetypes via routing geometry.** Ask whether routing or clustering geometry reveals a *stable* number of physician archetypes — a "natural N" of segments — rather than an arbitrary k chosen for convenience. Segmentation grounded in structure, not in a slide template.
- **C3 — Algorithmic audit of public "MoE" platform claims.** Apply the three architectural criteria (token-level routing? shared trunk? jointly trained?) and the six buyer questions (Chapter 7) to public vendor "MoE" descriptions and reach a verdict. Pure desk research, no proprietary data — a publishable technology audit that tops out at L2 (an audit, not a benchmark).

#### Worked project C1 (Track C exemplar) — the MoE-vs-ensemble benchmark

- **Question:** Does a routed / MoE-style model beat a tuned gradient-boosting baseline on an NPI/NBRx-proxy task?
- **Dataset:** A constructed NPI-propensity table from Part D + Open Payments + specialty/geography features. Synthetic fallback: a simulated NPI feature matrix with known structure.
- **Identification (benchmark, not causal):** A calibrated XGBoost/LightGBM baseline vs. a routed model, compared on **out-of-time validation, calibration curves, and subgroup robustness** — not AUC alone.
- **Success threshold:** A *meaningful, interpretable* gain in out-of-time validation, calibration, or subgroup robustness.
- **Kill criterion:** No lift over the tree ensemble, *or* worse calibration, *or* complexity not justified by business value. (Given the tabular-data evidence, this is the *expected* result.)
- **Evidence-Ladder level:** L2–L3.
- **Compliance + welfare flags:** Minimal — this is a model bake-off. But note: a "no lift" result *protects* the partner from an unjustified architecture investment. A "no" is a result.
- **Likely owner:** Data science. **Handoff** only if routing yields operationalizable, segment-specific gains.

**The failure mode to teach.** The rigged benchmark: the Fellow lovingly tunes the fancy routed model and leaves the baseline at defaults, then "discovers" the fancy model wins. The integrity check is **equal tuning effort on both models and calibration reporting, not just AUC**. A benchmark where the baseline was sandbagged is worse than no benchmark, because it manufactures exactly the false positive the lab exists to prevent. The honest C1, where a well-tuned XGBoost beats or ties the routed model, is a *successful project*: it saves the partner the engineering budget.

### 5.4 Track D — Privacy, fairness, and accountability (likely owner: compliance + medical-commercial)

**The logic.** This is the adversarial track — empirically answerable fairness and welfare questions the field leaves unexamined (two causal/empirical projects, one framework). It carries the highest partner-framing tension (Risk 2/4): frame as collaborative de-risking, secure partner sign-off, and route any legal *conclusion* to counsel. Whether and how adversarial these projects can be, given a named partner, is the **standing blocker** [contested — see pantry, Risk 1].

**Three projects:**

- **D1 — Proxy-discrimination detection in rep/targeting assignment.** Test whether propensity/targeting models encode proxies for physician *susceptibility* — or for protected-correlated attributes (geography, practice setting, area patient demographics) — rather than for clinical need. **Proxy discrimination** is a facially neutral feature acting as a stand-in for a protected attribute (the redlining analogy; `_lib_math-weapons-of-math-destruction...`). Method: train a public-data propensity model, then test whether its scores are predicted by protected-correlated proxies *after* conditioning on legitimate clinical-need features, with a causal-graph framing for which paths count as "proxy" paths. Whether targeting models *do* encode susceptibility proxies is **unexamined and answerable, not established** [contested — see pantry]. Public-data sufficiency is a real risk (Risk 5): physician-level protected attributes are not in Part D or Open Payments, so this likely relies on area-level proxies and tops out at L2.
- **D2 — Co-pay-coupon generic-suppression causal estimate.** Replicate and extend the Dafny–Ody–Schmitt design (cross-state and coupon-legality variation; coupons are banned in Medicare) to estimate how much coupons suppress generic substitution and raise system cost. The cleanest causal Track-D project, and a direct test of the contested claim that co-pay coupons are pro-patient (the honest answer is "nuanced," not "yes").
- **D3 — Accountability framework for commercial HCP-targeting AI.** A normative/structural deliverable, not an estimate: what monitoring, disclosure, auditability, and patient-welfare checks a *deployed* targeting system should carry. This routes directly into the Chapter 14 patient-welfare gate and post-launch monitoring plan.

#### Worked project D2 (Track D exemplar) — co-pay-coupon generic suppression

- **Question:** How much do co-pay coupons suppress generic substitution and raise system cost?
- **Dataset:** Medicaid SDUD (state × quarter generic vs. branded units and spend) + LOE/generic-entry dates; coupon-legality variation (the Medicare ban; state rules) as the design.
- **Identification:** Difference-in-differences / cross-state-legality contrast around generic entry — the Dafny–Ody–Schmitt template (Dafny, Ody & Schmitt 2017, *AEJ: Economic Policy*; NBER w22745 [verify vintage and effect sizes]), heterogeneity-robust if the timing is staggered.
- **Success threshold:** A credible, signed estimate of generic-substitution suppression with valid pre-trends (an event-study plot with leads near zero).
- **Kill criterion:** No clean legality or timing variation; pre-trends fail.
- **Evidence-Ladder level:** L3 — this design is well-precedented.
- **Compliance + welfare flags:** **HIGH.** This directly tests a partner product line (co-pay programs; Doceree's Co-Pay.com). A suppression finding has clear patient-welfare and policy weight. Secure partner sign-off on framing (Risk 2/4); route any *legal* characterization to counsel.
- **Likely owner:** Compliance + medical-commercial.

**The failure mode to teach.** Ecological inference. SDUD is aggregated to NDC × state × quarter — it does not observe individual patients or individual substitution decisions. Reporting "coupons cause patients to stay on the brand" overclaims patient-level behavior from state-level aggregates. The honest version states the estimate at the level the data supports (state-quarter generic share) and explicitly flags that individual substitution is *inferred*, not observed.

## 6. Worked example — a completed portfolio project, scored

Below is what a finished Track-C C1 project looks like when it is handed to the lab review — the artifact this chapter trains. (The Chapter 14 worked example takes a project *card* like this one and turns it into a test/build/kill memo; here the job ends at "run it and score it honestly.")

> **Project card — C1: Ensemble vs. routed model on NPI propensity**
>
> **Question.** On a public NPI-propensity task, does a routed (MoE-style) model produce a meaningful, interpretable improvement over a tuned gradient-boosting baseline?
>
> **Dataset.** NPI-propensity table built from Medicare Part D Prescriber (2-year-lagged outcome) + CMS Open Payments (promotion-dose features) + NPPES specialty/geography. ~N physicians in two target classes. Synthetic fallback prepared (simulated feature matrix with known interaction structure) in case the join coverage is too thin for a class.
>
> **Identification.** Benchmark, not causal. Both models tuned with equal effort and the same compute budget (this is logged). Evaluation: out-of-time validation (train on year *t*, test on *t+1*), calibration curves (reliability + Brier score), and subgroup robustness across specialty and decile bands. AUC reported but *not* the headline.
>
> **Success threshold (pre-registered).** Routed model improves out-of-time calibration *and* holds or improves subgroup robustness, with the gain large enough to matter operationally — not a third-decimal AUC bump.
>
> **Kill criterion (pre-registered).** No improvement over the tuned tree ensemble, or worse calibration, or a gain too small to justify the routing infrastructure.
>
> **Result.** The tuned LightGBM baseline matched the routed model on AUC and *beat* it on calibration (lower Brier, better reliability in the tails). Subgroup robustness was equivalent. The routed model added substantial training and inference complexity for no operational gain. **Kill criterion met.**
>
> **Evidence-Ladder level.** L3 (a small offline test that beats the baseline — here, the baseline *is* the winner).
>
> **Compliance + welfare flags.** Minimal. Note for the handoff: a "no lift" finding protects the partner from an unjustified architecture investment.
>
> **Likely owner.** Data science.
>
> **Plain-language readout (for a non-technical decision-maker).** "We tested whether the fancier 'mixture-of-experts' model the vendor deck describes would actually beat a standard, well-tuned model on the kind of physician-targeting task we care about. With equal effort on both, the standard model was as accurate and *better calibrated* — its probability estimates were more trustworthy — at a fraction of the complexity. Recommendation: do not invest engineering in the routed architecture for this task. The standard model is the right tool. This 'no' just saved us the build."

Notice what makes this a *finished* artifact rather than a notebook: the kill criterion was written before the result; the result is reported against it without spin; the ladder level is honest; and the plain-language readout tells the partner what to *do*. The "no" is the deliverable.

## 7. Common misconceptions

- **"A comprehensive literature review is a portfolio project."** No. A review summarizes what the field says about itself. A portfolio project *tests* a claim and reduces uncertainty. The lab grades the second, not the first (the opening case).
- **"If public data can't prove the strong version, the project failed."** No. "Public data establishes X, cannot establish Y, and here is the design that would" is a result — often the most valuable one, because it tells the partner exactly what proprietary work to fund.
- **"A negative result wasted the cycle."** No. The C1 "no lift" outcome saved an engineering budget; the A1 "the lift is mostly selection" outcome stopped the partner believing its own attribution. A pre-registered kill is the portfolio's honesty mechanism, not its failure mode.
- **"Open Payments + Part D is a causal pipeline."** No. On their own they yield *associations*, which the literature already establishes (and physicians dispute via the third-person effect). A causal estimate requires an identification design layered on top (Chapter 12). The datasets are the substrate; the design is the contribution.
- **"My matched estimate is the causal effect."** No. Matching adjusts only for observed confounders. Report a residual-confounding sensitivity, not a point claim (the A1 failure mode).
- **"ICER value is ground truth."** No. The QALY method is contested and ICER-reviewed drugs are a selected set. Use it as one flagged benchmark (the B3 failure mode).

## 8. Evidence check

- **Independent / established:** Tree ensembles are SOTA on medium tabular data (Grinsztajn et al., NeurIPS 2022 [verify]). Co-pay coupons raise branded sales by suppressing generic substitution (Dafny, Ody & Schmitt 2017 [verify vintage/effect sizes]). Detailing and industry payments are *associated* with increased branded prescribing (multiple systematic reviews; `pharma-marketing-evidence-synthesis.md` §1).
- **Vendor-generated (treat as claims, not evidence):** All 4–44% script-lift figures; the 19–25% EHR-lift range; "20:1 ROI" claims. None is independently audited (`pharma-ai-hcp-marketing-synthesis.md` §1, §8).
- **Hypothetical / design-grade:** A2 (point-of-care lift) and D1 (proxy discrimination) top out at simulation/design on public data because the exposure and protected-attribute data do not exist publicly (Risk 5).
- **Contested / open research questions (flagged, not asserted):** whether mind-share leads market share (SOMi→SOMa, B1); whether brand equity tracks clinical value (B3); whether targeting models encode susceptibility proxies (D1); whether co-pay coupons are net pro-patient (D2). These are the questions the portfolio is built to *test*, and the book's position is to keep them open until tested.

## 9. Compliance + patient-welfare check

- **MLR / FDA fair balance:** No project here generates HCP-facing claims, so MLR exposure is low at this stage — but any *handoff* that would lead to content (Chapter 14) inherits it. Flag, don't adjudicate.
- **Sunshine Act / Open Payments:** Using Open Payments is the *intended* public use of disclosed transfers of value; no exposure created. (Note current-year CMS de minimis thresholds if you summarize them.)
- **HIPAA / privacy:** All datasets are de-identified or aggregated public files; no PHI touched. D1's area-level proxies must not be re-identified to individuals.
- **Patient-welfare flags by track:** Track A (lift inflation → partner-sensitive but welfare-neutral); Track B (equity-not-value → the system pays a premium for non-superior drugs); Track D (coupon suppression and susceptibility proxies → the sharpest welfare findings in the book). Track D and the welfare-positive findings in B feed directly into the Chapter 14 **patient-welfare gate**. Every welfare-relevant finding is *flagged and routed*, never adjudicated as a legal or policy conclusion.

## 10. Exercises

1. **(Understand)** For each of the four tracks, write the one-sentence "lab value" — what uncertainty a project in that track reduces for the partner. Then identify which track each of these belongs to: "do targeting scores predict practice ZIP demographics after controlling for specialty?"; "does the routed model beat XGBoost on calibration?"; "does branded share survive generic entry?"; "is the headline lift mostly selection?"

2. **(Apply)** Take the C1 worked example and *rig* it: describe exactly what you would change to make the routed model appear to win (tuning asymmetry, metric selection, subgroup cherry-picking). Then write the three integrity checks a reviewer should apply to catch each rig. This trains you to spot the failure mode by building it.

3. **(Apply+)** Choose one project from Tracks A, B, or D and write its full seven-field card *including a pre-registered kill criterion*. Your kill criterion must be specific enough that, after seeing the result, no honest person could relabel a failure as a success. State the Evidence-Ladder ceiling and justify it from the data's limits.

4. **(Create / Part B — produce)** Run one project end to end on public or synthetic data — your own thread if you have one, otherwise an exemplar above. Produce: (a) the completed seven-field card, (b) the analysis notebook, and (c) a **plain-language readout** (≤150 words) that a non-technical partner decision-maker could act on. The readout must state what you found, the honest evidence level, and what you recommend the partner *do*. A defensible "no" earns full marks.

## 11. Five-part AI exercise block

**When to use AI.** Use an LLM to draft the analysis plan, scaffold the notebook, extract structured fields from ICER PDFs (B3), and propose the identification strategy's diagnostics. AI is strong at turning "I want to test whether equity predicts persistence net of value" into a covariate list, a model spec, and a checklist of pre-trend and sensitivity tests.

**When NOT to use AI.** Do not let an LLM decide whether your *signal is real*, whether your benchmark is fairly tuned, whether your kill criterion was met, or whether the partner could defend the finding to a regulator or audit committee. These are the judgments the lab exists to supply, and they are exactly where fluent-but-wrong output is most dangerous.

**LLM exercise.** Prompt: *"Draft an analysis plan for testing whether co-pay coupons suppress generic substitution using Medicaid SDUD and coupon-legality variation. Give me the design, the identifying assumption, the diagnostics, and the code."* Run it, then audit the output against Chapter 12: does it hand you a heterogeneity-robust DiD (Callaway–Sant'Anna) or a biased two-way-fixed-effects regression? Does it include a pre-trends plot? Does it flag ecological inference?

**CLI exercise.** Use a coding agent to build the C1 benchmark: construct the NPI-propensity table from public files, train a tuned LightGBM baseline and a routed model with *logged equal tuning budgets*, and emit calibration curves plus a Brier score for each. The deliverable is a reproducible script and a one-paragraph result against the pre-registered threshold.

**AI validation.** Take any LLM-generated "evidence summary" or analysis the block produced and run the validation harness from Chapter 10: check every citation resolves and says what is claimed; check the benchmark was not silently rigged (equal tuning? calibration reported, not just AUC?); check no causal claim rests on Open Payments + Part D alone. Write down the one place the AI was fluent and wrong.

## 12. AI Use Disclosure

When you submit a portfolio project, your AI Use Disclosure must name **one judgment the AI could not make** — for example: "the LLM drafted the DiD code, but I judged that the signal survived the pre-trends check and that the partner could defend the kill to its data-science lead." Naming that judgment is the +5 Part B bonus criterion (the AI Use Disclosure must identify which claims are truly evidenced, whether the signal is real, or whether the partner could defend it). The disclosure is not a confession; it is the record of where human expertise was load-bearing.

## 13. What would change my mind

The portfolio's stances are testable, and the book holds them open. I would revise the claim that **public-data lift estimates are mostly selection** if an A1-style audit, run honestly with a credible design, recovered a naive estimate close to the design-based one across multiple drug classes. I would revise the claim that **routed models do not beat tuned ensembles on tabular NPI tasks** if an equally tuned, calibration-reported C1 benchmark showed a meaningful, reproducible gain. I would revise the working assumption that **brand equity is often "commercial memory, not clinical value"** if B3/B4 found equity persistence tracking ICER value once selection-into-review is handled. And I would revise the framing that **Track A and D can be run as collaborative de-risking** if the partner agreement (Risk 1) lands somewhere that forecloses critical findings — in which case the honest move is to say so, not to soften the science.

## 14. Still puzzling

- Public data tops out around Level 3; how much of the partner's real uncertainty actually lives *below* Level 3, where the Fellow can reach it, versus above it, where only proprietary replication can?
- For tabular NPI tasks there is no token sequence and no obvious unit of routing — so what would "specialization" even *mean* for a physician-archetype model (C2), and is a "natural N" of segments a real structural fact or an artifact of the clustering objective?
- If the most-promoted drugs are also the ones ICER reviews, can *any* public-data design cleanly separate brand equity from clinical value, or is selection-into-review a ceiling on B3 no matter how careful the conditioning?

## 15. Summary

You can now run one research project end to end on public data and score it honestly. You can walk the four tracks — Lift/attribution, Brand/identity, Model architecture, Ethics/accountability — and specify, for any project, the seven-field card: question, dataset and synthetic fallback, identification strategy, pre-registered success threshold and kill criterion, Evidence-Ladder level, compliance and welfare flags, and likely partner owner. You know the exemplar per track (script-lift audit, brand-equity-vs-ICER, the MoE-vs-ensemble benchmark, coupon generic-suppression) and the characteristic failure mode of each (calling a matched estimate causal, treating ICER as ground truth, rigging the benchmark, ecological inference). Most of all, you have internalized the discipline that distinguishes the lab from the seminar: a pre-registered "no" is a result, and the deliverable is reduced uncertainty, not a paper summary.

## 16. Key terms

- **Portfolio project:** one research idea run end to end on public/synthetic data and scored against a pre-registered threshold.
- **Seven-field card:** the standard project specification — question, dataset (+ fallback), identification, success threshold + kill criterion, ladder level, compliance + welfare flags, likely owner.
- **Kill criterion:** the pre-registered result that makes you walk away; the portfolio's honesty mechanism.
- **Attribution circularity:** the bias from the same platform serving the ad and measuring the lift.
- **Proxy discrimination:** a facially neutral feature standing in for a protected attribute (the redlining analogy).
- **Ecological inference:** inferring individual behavior from aggregated (e.g., state-level) data — a trap in SDUD-based work.
- **Evidence-Ladder ceiling:** the level (≈L3) public data can reach; the firewall made operational.
- **Brand equity (pharma):** the physician remembering the *patient type*, not the name.

## 17. Bridge

You have a scored project — a result, a ladder level, a set of flags. But a scored project is not yet a decision. The partner does not need to know *that* the routed model lost or *that* the lift is mostly selection; the partner needs to know what to *do* about it: test it further, replicate it on proprietary data, shelve it, or ship it. Chapter 14 turns the scored project into that decision — the product-handoff brief — and introduces the criterion that can override even a strong commercial result: the patient-welfare gate.

## 18. Further reading

- Grinsztajn, Oyallon & Varoquaux, "Why do tree-based models still outperform deep learning on tabular data?" *NeurIPS* 2022. — The benchmark anchor for Track C. [verify citation details against the MoE synthesis]
- Dafny, Ody & Schmitt, "When Discounts Raise Costs: The Effect of Copay Coupons on Generic Utilization," *AEJ: Economic Policy* 9(2), 2017 (NBER w22745). — The Track-D D2 template. [verify vintage and effect sizes]
- Larkin et al., "Association Between Academic Medical Center Pharmaceutical Detailing Policies and Physician Prescribing," *JAMA* 317(17), 2017. — The natural-experiment model behind A1's policy-shock arm. [verify effect sizes]
- Callaway & Sant'Anna, "Difference-in-Differences with multiple time periods," *Journal of Econometrics* 225(2), 2021. — The heterogeneity-robust estimator A1/B4/D2 require. [verify]
- O'Neil, *Weapons of Math Destruction.* — The proxy-discrimination and feedback-loop framing for Track D1 (`pantry/_lib_math-weapons-of-math-destruction...`).
- `pantry/pharma-brand-measurement-synthesis.md` (§§3–4, 6) and `pantry/pharma-marketing-evidence-synthesis.md` (§§1, 4, 8). — The brand-equity, LOE, ICER-value, and market-failure grounding for Track B and the welfare flags.

---

## Prompts

*No figures have been generated for this chapter yet.*
*Run the Cowork enrichment pass to populate this section.*
