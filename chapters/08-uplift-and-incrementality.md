# Chapter 8 — Uplift and Incrementality: Measuring Real Lift
*The model that predicts everything changes nothing.*

A platform reports a triumph. Physicians who received its AI-selected next-best-action message grew their new-to-brand prescriptions by 44% over the campaign window. The deck calls this "44% script lift." The number is real in the narrow sense that the arithmetic checks out. It is also almost certainly the wrong number, and you can show why with one move: ask where the holdout is.

`[the 44% figure is illustrative of the vendor range; verify against primary sources before citing]`

Here is what the 44% actually compares. The exposed physicians were the highest-propensity targets — the platform deliberately picked the doctors most likely to prescribe. Their post-campaign NBRx is being measured against their own prior period, or against unexposed low-propensity physicians who were never comparable in the first place. Three biases compound simultaneously. The first is targeting on the outcome: the treated group was selected *because* it was going to prescribe, so its growth is partly the growth it would have shown untreated. The second is regression to the mean and secular trend: the brand was already growing, and physicians selected at a high point drift back toward their average over time. The third is attribution circularity: the platform that served the ad also measured the lift, on its own data, with no independent firewall.

Now draw a holdout. Randomly withhold the message from a fraction of that *same* high-propensity target list. Measure incremental NBRx as treated-mean minus holdout-mean. The honest number is the gap between two comparable groups — and it is typically a fraction of 44%, sometimes inside the noise of zero.

The 44% was not fabricated. It was the answer to a different question. This chapter is about asking the right one.

---

Start with the inversion, because the whole chapter lives inside it.

Propensity answers one question: how likely is this physician to prescribe, given what we know about them? Incrementality answers a different question: how much did the prescription probability change *because of what we did*? These feel related. They come apart violently at the top of the propensity scale.

A physician with 95% propensity has almost no room to be moved. She would very likely prescribe anyway. The intervention's incremental return on her is near zero even though the model is certain about her. The incremental return on any campaign lives not among the predictable but among the **persuadable** — the physicians who are genuinely on the fence, for whom the message tips something.

This is why targeting on propensity and then measuring the treated group's outcome systematically inflates apparent lift. The high-propensity targets were going to prescribe regardless of what you did. Their prescribing gets credited to the campaign. The model you built to predict them was doing its job. The mistake was using a prediction model to answer a causation question.

A great predictor can be a terrible intervention target. Keep that sentence nearby. It is the inversion this chapter is built on, and it resolves the opening case in one step.

![Two-axis plot — x: propensity score (0 to 1), y: incremental effect (CATE); curve peaks in the middle persuadable range and is near zero at both tails; annotations at high-propensity end read "sure things — wasted spend," at low end "lost causes — wasted spend," in middle "persuadables — the only profitable target".](../images/08-uplift-and-incrementality-fig-01.png)

*Figure 8.1 — The propensity-versus-incrementality inversion*

<!-- → [DIAGRAM: Two-axis plot — x: propensity score (0 to 1), y: incremental effect (CATE); curve peaks in the middle persuadable range and is near zero at both tails; annotations at high-propensity end read "sure things — wasted spend," at low end "lost causes — wasted spend," in middle "persuadables — the only profitable target"] -->

---

The reason incrementality is hard is not statistical fussiness. It is logical, and understanding the logic matters before you trust any method that claims to solve it.

For any single physician, you could in principle observe $Y(1)$ — their prescribing if exposed — or $Y(0)$ — their prescribing if not exposed. You cannot observe both at the same time. The individual treatment effect, $Y(1) - Y(0)$, is unobservable *in principle.* Not because we lack data. Because the physician can only be in one world at once.

This is the fundamental problem of causal inference. It is not a problem that more data solves, or that a better algorithm solves. It is a structural feature of how time works. Any method that claims to estimate individual-level treatment effects is really estimating something slightly different: an average over physicians who are similar in measurable ways, in the hope that the unmeasured ways cancel out.

Because the individual effect is unrecoverable, we settle for averages over comparable groups. The **average treatment effect** is $E[Y(1) - Y(0)]$ across a population — the mean lift, if you could run the experiment on everyone. The **conditional average treatment effect**, or **CATE**, is $E[Y(1) - Y(0) \mid X = x]$ — the effect conditional on a physician's covariates. CATE is the heterogeneous, individualized quantity that uplift modeling targets: it is why two physicians with different features get different predicted lifts from the same campaign. The marketing term "uplift modeling" and the econometrics term "CATE estimation" describe the same task in two vocabularies.

| Marketing term | Econometrics term | What it means in plain language |
| --- | --- | --- |
| Uplift model | CATE estimator | Predicts the effect of treatment for a given physician |
| Propensity score | $P(\text{treat} \mid X)$ | Probability of being treated |
| Lift | ATE | Average effect across the population |
| Persuadables | High-CATE subgroup | Physicians where the treatment actually moves the needle |

*Table 8.1 — Terminology bridge: the same task in two vocabularies.*

---

Averaging only recovers a causal effect when the groups being compared are genuinely comparable. Three assumptions do that work, and each deserves to be understood at first use rather than memorized as a checklist.

**Unconfoundedness** — also called conditional exogeneity — means treatment is as-good-as-random given the covariates. A randomized holdout satisfies this by design: you flipped a coin, so there is no systematic difference between treated and held-out physicians beyond what the coin decided. Observational vendor "lift" merely *assumes* unconfoundedness — it assumes the exposed and unexposed groups are comparable after you condition on whatever features the model observed. That assumption is almost always violated in a targeting context, because targeting is the opposite of random. The platform selected the exposed group precisely because they were different from the unexposed group.

**Overlap**, or positivity, requires that treated and control physicians both exist across the covariate space. If every high-decile physician is treated and every low-decile physician is not, there is no overlap — nothing to compare at the top of the distribution where the action is. Without overlap, any estimated effect is extrapolated, not observed.

**SUTVA**, the stable unit treatment value assumption, says one physician's exposure does not change another's outcome. This is shaky in pharma. Key opinion leaders, shared practices, and referral networks all create spillover: a message that activates a high-volume prescriber at an academic medical center may diffuse through residents, fellows, and community physicians who share the workflow. Spillover inflates lift estimates in the treated cluster and deflates lift estimates in adjacent controls. It is the assumption that matters most in real pharma networks and gets stressed least in vendor methodology decks.

A **randomized holdout** is the cleanest instrument because it buys unconfoundedness directly. Randomly withhold the intervention from a subset of the target list; the holdout *is* the counterfactual. Every other method in this chapter is either an approximation to the holdout or a way to extract causal signal when a holdout is not available. None is as decisive as that single design move.

---

When you cannot randomize at will — or when you want to estimate heterogeneous effects from data you already have — you reach for CATE estimators. Know them and their failure modes; the derivations matter less than the intuition.

**Meta-learners** wrap any base learner — typically a gradient-boosted tree, which means the Chapter 6 baseline is literally the engine running inside them — and use that learner to estimate treatment effects. The S-, T-, and X-learner family is formalized in Künzel, Sekhon, Bickel, and Yu, "Metalearners for estimating heterogeneous treatment effects using machine learning" (*PNAS*, 2019).

The **S-learner** fits one model with treatment as a feature. Simple and often badly behaved: if the treatment signal is weak, a regularized base learner may shrink the treatment coefficient toward zero and miss the effect entirely.

The **T-learner** fits two separate models — one on the treated group, one on the control group — then differences their predictions. This works cleanly when groups are balanced. With imbalanced treatment assignment (which is typical in pharma targeting), the two models train on unequal sample sizes and the variance in the difference can overwhelm the signal.

The **X-learner** handles imbalance by cross-imputing: it estimates what each treated physician *would have* done in the control condition using the control model, and vice versa, then averages the imputed individual effects. It is stronger than the T-learner specifically when group sizes are unequal — which is almost always.

The **R-learner** takes a different route: it residualizes out the propensity and the baseline outcome using auxiliary nuisance models, then regresses the residualized outcome on the residualized treatment. The double residualization (Neyman-orthogonal) makes it robust to misspecification in either the propensity or the outcome model — and that robustness is worth the added complexity (Nie & Wager, "Quasi-oracle estimation of heterogeneous treatment effects," *Biometrika* 108(2):299–319, 2021).

**Causal forests** — from Wager and Athey ("Estimation and Inference of Heterogeneous Treatment Effects using Random Forests," *JASA* 113(523):1228–1242, 2018) — take a tree-based approach that splits on treatment-effect heterogeneity directly rather than outcome heterogeneity. They produce a CATE estimate with non-parametric confidence intervals at each leaf. One honest caveat to carry with them: causal-forest inference is theoretically valid mainly in low-dimensional settings and "can be more brittle... not as assumption-lean as inference based on OLS" in high dimensions. Do not oversell causal forests as assumption-free. They are not.

**Doubly-robust methods**, including the DR-learner, are consistent if *either* the propensity model or the outcome model is correctly specified — a practical safety net for observational CATE when you are not confident in either model alone.

Which estimator wins on your data is empirical, dataset-dependent, and not answerable in advance. Empirical comparisons of meta-learners and causal forests on large industrial marketing data (for example, on the public Criteo uplift dataset) report no universal winner — in some configurations the simple S-learner is hard to beat despite treatment imbalance — and find that calibration and ranking quality matter as much as the estimator family. [verify — unconfirmed: the precise per-estimator Qini rankings vary by study and configuration; treat the "no universal winner" conclusion as the robust finding, not any single leaderboard.] Treat "which CATE estimator is best" as a question you test, not a setting you assume.

| Estimator | Key idea | When it works best | When it breaks | One-line failure mode |
| --- | --- | --- | --- | --- |
| S-learner | One model with treatment as a feature | Strong treatment signal | Weak treatment signal | Regularization shrinks the treatment coefficient toward zero |
| T-learner | Two models, treated and control, differenced | Balanced groups | Imbalanced assignment | Variance in the difference overwhelms the signal |
| X-learner | Cross-imputes counterfactuals, then averages | Unequal group sizes | Very noisy base models | Inherits base-learner error through imputation |
| R-learner | Residualizes propensity and outcome (Neyman-orthogonal) | Either nuisance model is misspecified | Both nuisance models are poor | Double residualization cannot rescue two bad models |
| Causal forest | Splits on treatment-effect heterogeneity directly | Low-dimensional settings | High dimensions | Inference more brittle, not assumption-lean |
| DR-learner | Doubly robust: consistent if either model is right | Uncertain about either model | Both models wrong | No safety net when neither nuisance model holds |

*Table 8.2 — CATE estimator comparison. Which one wins on your data is empirical and dataset-dependent.*

---

Now the evaluation problem, which is harder than the estimation problem.

You cannot score an uplift model with ordinary accuracy, because the thing you are predicting — the individual treatment effect — is never observed. You cannot check whether your predicted CATE for physician A was right, because you can only observe one of her two potential outcomes. If you treated her, you see $Y(1)$ but not $Y(0)$. If you didn't, you see $Y(0)$ but not $Y(1)$. The individual label is always missing.

The standard solution is the **uplift curve** and its summary statistic, the **Qini coefficient**. Rank physicians by predicted uplift from highest to lowest. As you descend the ranking, plot the cumulative incremental response: treated-minus-control outcome, accumulated as you go down the list. A model that correctly identifies the persuadables concentrates incremental response at the top — the curve bows upward above the random-targeting diagonal. The Qini coefficient is the area between the model curve and the diagonal; more area means better uplift targeting.

The intuition to hold: a useful uplift model lets you spend on the persuadables and skip the sure things. If a model cannot concentrate incremental response at the top of its ranking, it has not learned to distinguish persuadables from sure things, and it will not improve on random targeting even if its propensity predictions are excellent.

![Uplift/Qini curve — x-axis: fraction of population targeted (0–1), y-axis: cumulative incremental response; three curves: perfect model (steep rise then flat), actual model (intermediate bow), random targeting (diagonal); shaded area between actual and diagonal labeled "Qini coefficient"; annotation: "sure things live below the knee; persuadables live above it".](../images/08-uplift-and-incrementality-fig-02.png)

*Figure 8.2 — The Qini curve: how much incremental response a ranking captures*

<!-- → [CHART: Uplift/Qini curve — x-axis: fraction of population targeted (0–1), y-axis: cumulative incremental response; three curves: perfect model (steep rise then flat), actual model (intermediate bow), random targeting (diagonal); shaded area between actual and diagonal labeled "Qini coefficient"; annotation: "sure things live below the knee; persuadables live above it"] -->

---

If you remember one picture from this chapter, make it this one.

Cross two binary questions: does this physician prescribe if treated? Does this physician prescribe if untreated? Four groups fall out.

**Persuadables** prescribe only if treated. They are the only group where the intervention produces a net gain. Every campaign dollar should be fighting its way toward them.

**Sure things** prescribe regardless of treatment. Treating them is wasted spend — and crediting their scripts to the campaign is precisely how a 44% figure gets built from a campaign that may have done nothing incremental at all.

**Lost causes** won't prescribe either way. Also wasted spend, for different reasons.

**Sleeping dogs** — sometimes called do-not-disturbs — are the counter-intuitive quadrant: treatment actively *reduces* the outcome. The message backfires. This happens in pharma contexts: a co-pay card for a drug a physician already resists prescribing on grounds of clinical inappropriateness may harden the resistance. A message that arrives in a crowded EHR workflow at the wrong moment may generate negative associations rather than positive ones. The sleeping-dog quadrant is a warning that uplift is directional, and that intervention can be harmful.

Targeting on high propensity targets the sure things. Uplift targeting targets the persuadables. That reframing is the chapter's entire argument in business language.

![Persuadables 2x2 — axes: "prescribes if treated" (yes/no) and "prescribes if untreated" (yes/no); four quadrants labeled persuadables, sure things, lost causes, sleeping dogs; arrows from "propensity targeting" pointing to sure-things quadrant; arrows from "uplift targeting" pointing to persuadables quadrant.](../images/08-uplift-and-incrementality-fig-03.png)

*Figure 8.3 — The persuadables 2×2: propensity targets sure things, uplift targets persuadables*

<!-- → [DIAGRAM: Persuadables 2x2 — axes: "prescribes if treated" (yes/no) and "prescribes if untreated" (yes/no); four quadrants labeled persuadables, sure things, lost causes, sleeping dogs; arrows from "propensity targeting" pointing to sure-things quadrant; arrows from "uplift targeting" pointing to persuadables quadrant] -->

---

A Fellow working with public data cannot run a live randomized holdout on a vendor's targeting system — that requires live infrastructure and a commercial partnership. But causal claims are still reachable through **natural experiments**, where a policy change acts as an as-good-as-random shock to exposure.

The flagship pharma example is academic medical center detailing restrictions. Larkin and colleagues (*JAMA* 2017;317(17):1785–1795) ran a difference-in-differences study on 19 AMCs across five states that restricted sales-rep detailing between 2006 and 2012 — 2,126 affected physicians against 24,593 matched controls, across 262 drugs in 8 classes. Restricting detailing produced modest but significant reductions in detailed-drug prescribing in 6 of 8 classes, with physicians shifting from expensive patent-protected drugs toward cheaper generics. A related study found AMC marketing restrictions associated with lower opioid prescribing — a patient-welfare-relevant variant (Eisenberg, Stone, Pittell & McGinty, "The Impact Of Academic Medical Center Policies Restricting Direct-To-Physician Marketing On Opioid Prescribing," *Health Affairs* 2020;39(6):1002–1010).

The template generalizes. The policy change is the shock; neighboring or matched physicians are the control. State disclosure laws, formulary changes, loss of exclusivity, and payment thresholds all supply credible counterfactuals without a vendor's cooperation. The public-data route to causal claims runs through these shocks, and Chapter 12 develops their identifying assumptions in detail.

The honesty caveat, modeled explicitly: natural experiments are not automatically clean. Difference-in-differences rests on a parallel-trends assumption — that treated and control physicians were on the same trajectory before the policy change — and any co-occurring shock can confound the estimate. Quasi-experiments buy you a counterfactual. They do not buy you certainty. They buy you a *defensible argument* that the groups were comparable before the shock, which you must make in plain language and subject to scrutiny.

---

Here is what the opening case would look like with the right design.

Take the next-best-action campaign and design the readout it should have had. From the high-propensity target NPI list, randomly withhold the message from 15% of physicians before the campaign launches — this is the holdout, drawn from the same propensity stratum. Define a single primary outcome: incremental NBRx over a fixed window, with claims-lag accounting so you are not measuring scripts the pipeline hasn't reported yet. Compute incremental scripts as treated-mean NBRx minus holdout-mean NBRx, per physician, over that window. Fit an X-learner with a gradient-boosted base on the treated and held-out data. Plot the Qini curve to see which physicians carried the incremental response.

The headline collapses toward the holdout-corrected number, because the holdout strips out the three compounding biases from the opening case: it is drawn from the same propensity stratum, so targeting-on-outcome is gone; it experiences the same secular trend as the treated group, so trend confound is gone; and it is a randomized comparison rather than a self-referential platform baseline, so circularity is gone. The Qini curve then identifies where the campaign's real value was concentrated — in a persuadable minority — which is useful information for the next campaign's targeting.

The limits worth naming. SUTVA can fail if treated and held-out physicians share a practice and talk. The window choice trades claims-lag bias against secular-trend bias. The holdout costs the brand the scripts it forgoes among true persuadables in the held-out group. A holdout is the gold standard, not a free lunch. And on public data you cannot run one at all — which is why the natural-experiment route exists, and why the absence of a peer-reviewed randomized evaluation of EHR advertising is the chapter's standing open question.

---

**What Would Change My Mind**

The chapter's position is that propensity-based lift is structurally inflated and that incrementality requires a control. A pre-registered randomized holdout — or a well-identified natural experiment with a defensible parallel-trends argument — showing a meaningful incremental effect that survives claims-lag accounting and subgroup checks would move a specific channel from "unknown" toward "evidenced." The position is not "all lift claims are false." It is "a lift claim without a counterfactual is unproven." Show the counterfactual, and the verdict flips on evidence. One such study on EHR advertising, run by an independent party, would substantially change the chapter's treatment of that channel.

**Still Puzzling**

- No peer-reviewed, randomized evaluation of EHR/point-of-care advertising exists. We genuinely do not know the true incremental effect of a co-pay message firing inside the clinical workflow. Until that study is run and published, the fastest-growing channel in pharma marketing rests on the thinnest causal evidence.
- The persuadables quadrant is theoretically clean. In practice, how do you find persuadables without first running the experiment that reveals them? The answer involves iterative holdout design and Bayesian updating across campaigns, and the industry is early in working it out.
- SUTVA fails in any network with spillover. In pharma, key opinion leader networks are precisely the mechanism of diffusion that makes marketing work — which means the assumption that validates the holdout may be violated at exactly the points where the effect is largest.

---

## Exercises

**Warm-up**

1. *(Factual recall — the inversion)* Explain, in two sentences, why targeting the highest-propensity physicians and measuring their post-campaign outcomes overstates incremental lift. Name the specific quadrant of the persuadables 2×2 that "wasted spend that looks like success" comes from.
   *What this tests: whether you can state the propensity-vs-incrementality inversion in plain language.*

2. *(Factual recall — identification assumptions)* Name the three assumptions required for a comparison to recover a causal effect. For each, state in one sentence whether a randomized holdout satisfies it by design or merely assumes it.
   *What this tests: the logical structure of causal identification, not memorized labels.*

3. *(Factual recall — evaluation)* Why can't you score an uplift model with ordinary accuracy? What does the Qini coefficient measure, and what does a higher Qini value tell you about a model's practical usefulness?
   *What this tests: the fundamental evaluation problem in uplift and the intuition behind the Qini curve.*

**Application**

4. *(Apply — critique a claim)* A vendor reports that physicians who received a co-pay assistance message wrote 31% more new-to-brand prescriptions than physicians who did not. Write a critique that names the three compounding biases from this chapter and states the single design change that would fix the estimate.
   *What this tests: applying the opening-case analysis to a new claim.*

5. *(Apply — estimator selection)* A brand team ran a campaign where 90% of high-propensity physicians were treated and 10% were held out. They want to estimate CATE using the holdout data. Which meta-learner is most appropriate given the imbalanced group sizes, and why? Name one alternative and its failure mode in this setting.
   *What this tests: applying the estimator taxonomy to a realistic data condition.*

6. *(Apply — natural experiment design)* A state passes a law restricting pharmaceutical sales-rep visits to academic medical centers, effective on a known date. Sketch a difference-in-differences design using this as a natural experiment: name the treated group, the control group, the identifying assumption, and the single biggest threat to that assumption.
   *What this tests: translating the natural-experiment concept into a concrete design with named assumptions.*

**Synthesis**

7. *(Synthesize — persuadables and Qini)* A campaign ran with a randomized holdout. The uplift model's Qini curve shows that the top 20% of predicted-uplift physicians account for 80% of the measured incremental response. The remaining 80% of targeted physicians are in the persuadables-or-worse range. What does this tell you about the campaign's efficiency, and what would you recommend for the next targeting pass?
   *What this tests: reading a Qini result as a business input, connecting uplift measurement back to targeting decisions.*

8. *(Synthesize — design for your thread)* For your research thread from Chapter 2, design either a randomized holdout (if a live system is in scope) or a natural-experiment study (on public data) with: the primary incrementality outcome, the comparison group, the identifying assumption you are relying on, and the threat to that assumption you most worry about.
   *What this tests: integration across Chapter 2 (dependent variable) and Chapter 8 (identification) — the Part B checkpoint for this unit.*

**Challenge**

9. *(Open-ended — SUTVA and networks)* The chapter notes that SUTVA fails when physician networks create spillover. Propose a study design — using public data or a realistic hypothetical — that would (a) estimate how much spillover exists in a specific pharma marketing context and (b) correct the holdout-based incremental estimate for spillover contamination. Name the data you would need and the assumption your correction relies on.
   *What this tests: pushing past the standard holdout design to a harder real-world problem, and identifying the assumption that the fix introduces.*

---

## Prompts

### Figure 8.1 — The propensity-versus-incrementality inversion

Generate a single self-contained HTML file (inline CSS, D3 7.9.0 from the cdnjs CDN) rendering a line chart. Chart type: an inverted-U curve. X-axis: propensity score, scaleLinear 0 to 1, with axis label "propensity score (likelihood to prescribe)". Y-axis: incremental effect (CATE), scaleLinear, zero-baseline, label "incremental effect (CATE)". Marks: one red curve that is near zero at the left tail, peaks at mid-propensity, and falls toward zero at the right tail; a marked peak point. Channels: x position encodes propensity, y position encodes incremental effect. Shade three zones under the plot — left "lost causes" (muted gray), middle "persuadables" (red tint, the only profitable target), right "sure things" (muted gray). No sorting. Annotate that the mid-propensity peak is the only profitable target and both tails are wasted spend. viewBox 700×420, margins {top:48,right:40,bottom:56,left:64}. Deliverable: one HTML file, inline CSS, var(--color-*) tokens, light/dark theming, accessible title/desc, hover/focus tooltips.

### Figure 8.2 — The Qini / uplift curve

Generate a single self-contained HTML file (inline CSS, D3 7.9.0 CDN) rendering a cumulative-gain chart. X-axis: fraction of population targeted, scaleLinear 0 to 1. Y-axis: cumulative incremental response, scaleLinear, zero-baseline. Marks: three curves sharing origin (0,0) and endpoint (1,1) — a perfect-model curve (ink, steep then flat), an actual-model curve (red, intermediate bow above the diagonal, the single red series), and a random-targeting straight diagonal (gray, dashed). Shade the area between the actual curve and the diagonal as the Qini coefficient. Add a knee marker on the actual curve with a dashed drop-line and labels "persuadables" above the knee, "sure things" below. Channels: y position encodes captured incremental response. viewBox 700×420 (or 450 if needed), margins {top:48,right:40,bottom:56,left:64}. Deliverable: one HTML file, inline CSS, var(--color-*), light/dark theming, accessible title/desc, hover/focus tooltips.

### Figure 8.3 — The persuadables 2×2

Generate a single self-contained HTML file (inline CSS, D3 7.9.0 CDN) rendering a 2×2 matrix diagram. Axes (categorical, no scales): x = "prescribes if treated" (no → yes), y = "prescribes if untreated" (yes top, no bottom). Four equal quadrant cells: top-left sleeping dogs (hazard, red tint), top-right sure things (wasted, gray), bottom-left lost causes (wasted, gray), bottom-right persuadables (only profitable, red focal outline). Two labeled arrow callouts: "propensity targeting" (gray arrow) pointing to sure things; "uplift targeting" (red arrow) pointing to persuadables. Channels: fill tint encodes profitability/hazard; outline weight marks the focal cell. Annotate that propensity targeting buys sure things (inflated lift) and uplift targeting buys persuadables (the recommended move). viewBox 700×450. Deliverable: one HTML file, inline CSS, var(--color-*), light/dark theming, accessible title/desc, hover/focus tooltips.

---

## Chapter 8 Exercises: Uplift and Incrementality

**Project:** One Drug, End to End
**This chapter adds:** An estimate of persuadables versus sure-things among your drug's prescribers — a Qini-evaluated uplift view that corrects the inflated "lift" your propensity baseline would have credited.

We carry **Jardiance (empagliflozin)** forward — branded SGLT2 inhibitor, branded rivals Farxiga and Invokana, generic alternatives metformin and sulfonylureas. Chapter 6 gave you a calibrated propensity baseline; Chapter 7 told you whether a vendor's "MoE" beat it. Both answer *who is likely to prescribe*. This chapter answers the harder, profitable question: *who would prescribe Jardiance only because you reached them* — the persuadables — and separates them from the sure things your propensity model loves.

### Exercise 1 — When to Use AI

1. Ask an LLM to scaffold an uplift analysis for a Jardiance natural experiment — draft the difference-in-differences setup, code the treated-minus-holdout incremental computation, and code a Qini curve from a dataframe with treatment and outcome columns. *Why AI works here:* code generation against a stated design — runnable output you can execute and read.
2. Have it explain the X-learner's cross-imputation, or the R-learner's double residualization, in plain language before you read Nie & Wager. *Why AI works here:* concept exposition of documented estimators — checkable against the primary papers.

**The tell:** you can independently evaluate the output — run the Qini code on synthetic data with a known effect, confirm the curve bows the right way; check the estimator explanation against the cited paper.

### Exercise 2 — When NOT to Use AI

1. Do not let the LLM certify that a Jardiance "lift" number is *causal*. It will accept a before/after or high-propensity-treated-vs-low-propensity-untreated comparison as evidence if you phrase it confidently — exactly the 44%-style trap. *Why AI fails here:* causal-ID — identification is an argument about how treatment was assigned in the world, not a property of the code.
2. Do not let the LLM rank Jardiance prescribers by *propensity* and call it an uplift targeting list. A propensity ranking targets the sure things; only an uplift ranking finds persuadables. *Why AI fails here:* ground-truth — the individual treatment effect is never observed, so the model cannot verify its CATE ranking against any label and will happily substitute the propensity score it *can* compute.

**The tell:** if the AI's "this lift is real" or "these are your high-uplift targets" is your *reason* to act, you have failed; if it is a *tool* output you then test against a holdout and a Qini curve, you are fine. **Series connection:** this is a **T7** judgment — propensity-mistaken-for-uplift. Confusing prediction for causation is the single most expensive error in the series, and no fluent output can resolve whether your parallel-trends assumption holds. The human owns the identification argument.

### Exercise 3 — LLM Exercise

**What you're building this chapter:** an incrementality design for Jardiance — either a randomized-holdout readout (if a live system is in scope) or a public-data natural-experiment (a detailing-restriction or formulary shock) — with a named identifying assumption and a Qini-based persuadables view.

**Tool:** Claude, run as a **Claude Project**. Persistent drug-context helps because this design reuses the Chapter 6 Jardiance propensity strata (the holdout must be drawn from the *same* propensity stratum to kill targeting-on-outcome) — a Project keeps that baseline and the Jardiance class context resident so the design stays consistent with what you already built.

**The Prompt:**

```
You are designing an incrementality study for a running case on one branded drug
carried end to end: Jardiance (empagliflozin), a branded SGLT2 inhibitor with
branded competitors (Farxiga, Invokana) and generic alternatives (metformin,
sulfonylureas). In Chapter 6 I built a calibrated propensity baseline for Jardiance
new-to-brand starts on public Open Payments + Part D data.

I want to separate PERSUADABLES (prescribe Jardiance only if reached) from SURE
THINGS (prescribe regardless). Design BOTH options and tell me which fits public
data:

OPTION A — randomized holdout (only if a live targeting system is in scope):
- From the high-propensity Jardiance target list, withhold the message from a
  random 15% drawn from the SAME propensity stratum.
- Define the primary outcome: incremental NBRx over a fixed window, with claims-lag
  accounting.
- Specify the CATE estimator (default X-learner with a gradient-boosted base, given
  imbalanced treatment) and the Qini curve to locate the persuadables.

OPTION B — natural experiment on PUBLIC data only:
- Use a detailing-restriction or formulary shock as an as-good-as-random change in
  Jardiance exposure.
- Name the treated group, the matched control, the difference-in-differences
  identifying assumption (parallel trends), and the single biggest threat to it.

For whichever you recommend for a public-data Fellow, state explicitly: the
identifying assumption, the threat I must defend in plain language, and what the
Qini curve will and will NOT tell me. Flag any class or competitor claim as
[verify]. Do NOT declare any effect causal — describe the argument I must make.

ADAPTATION: replace Jardiance and its class with your own drug. In ChatGPT or
Gemini, paste your Chapter 6 baseline strata at the top so the holdout is drawn
from the right stratum.
```

**What this produces:** a concrete incrementality design naming its identifying assumption and its persuadables readout — the artifact Chapter 9 contrasts with brand association and Chapter 10 stress-tests against the literature.

**How to adapt:** swap the drug; in ChatGPT/Gemini re-supply the Chapter 6 strata each session; in a Claude Project, store the baseline as Project knowledge.

**Connection to previous chapters:** the holdout must be drawn from the same Chapter 6 propensity stratum — your baseline is now an *input* to the causal design, not a competitor to it. The 44%-style inflation this kills is the same vendor pattern you graded in Chapter 5.

**Preview of next chapter:** uplift measures behavior change; Chapter 9 asks whether the *belief* behind the behavior — durable brand association — moved at all, and why a favorability spike without a control is as empty as a lift claim without a holdout.

### Exercise 4 — CLI Exercise

**What you're building:** the chapter in one table — naive before/after Jardiance "lift" beside the holdout-corrected incremental effect, on a dataset with a treatment indicator.

**Tool:** Claude Code (or Cowork) — it can read the file, compute both numbers, and emit the comparison. **Skill level:** beginner-to-intermediate.

**Setup:**
- [ ] A dataset (public or synthetic) with a treatment indicator and a binary/continuous outcome in `./data/`.
- [ ] Python+pandas, or `csvkit`.
- [ ] An `./outputs/` folder; source data read-only.

**The Task:**

```
Read ONLY the dataset in ./data/ (do not modify it). Compute two numbers for a
Jardiance-style treated group:
(a) NAIVE before/after lift for the treated group only (post mean minus pre mean,
    or treated post mean vs treated pre mean).
(b) HOLDOUT-CORRECTED incremental effect = treated-group mean MINUS control/holdout
    mean over the same window.

Report both side by side and the ratio (corrected / naive) as a percentage. Write
to ./outputs/incrementality-gap.txt. Do not write anywhere else. Stop when the file
exists, then print it so I can verify the numbers myself.
```

**Expected output:** two numbers and a ratio — the holdout-corrected effect as a fraction of the naive figure, often a small fraction or inside the noise of zero.

**What to inspect:** how much of the naive Jardiance "lift" survives the holdout correction? Is the control drawn comparably (same window, same stratum), or is it a non-comparable low-propensity group?

**If it goes wrong:** if Claude Code computes "lift" against a non-comparable control (failure), restate that the holdout must be same-stratum and same-window, and re-run; if it reports only the naive number, require both side by side.

**CLAUDE.md note:** add `Never report a lift number without its holdout-corrected counterpart and the comparability of the control group stated.`

### Exercise 5 — AI Validation Exercise

**What you're validating:** the causal claim in your Ex3 design / Ex4 output — specifically whether the AI smuggled an unconfoundedness assumption the data does not support, or treated a propensity ranking as an uplift ranking.

**Validation type:** identification-and-assumption audit of a causal artifact. **Risk level:** high — because a propensity-mistaken-for-uplift error sends the entire Jardiance budget at sure things while booking their inevitable scripts as campaign success, and the error is invisible in confident output.

**Setup:** use your Ex3 design and Ex4 numbers. If you want a specific failure to practice on, ask the AI to "estimate the causal effect of Jardiance messaging" from observational data and watch whether it flags or silently assumes randomness.

**The Validation Task:**

```
Validation Checklist — Chapter 8 (Jardiance incrementality)

Mark each Pass / Fail / Cannot-determine:
- Correctness: Is the incremental effect computed as treated-minus-holdout (not a
  before/after or non-comparable-group comparison)?
- Completeness: Is the identifying assumption (unconfoundedness for a holdout,
  parallel trends for a natural experiment) named explicitly?
- Scope: Is the holdout drawn from the SAME propensity stratum, and the analysis on
  public/synthetic data only?
- Persuadables criterion: Does the ranking come from an uplift/CATE estimator and a
  Qini curve — NOT from the Chapter 6 propensity score?
- Threat criterion: Is the single biggest threat to identification named (spillover/
  SUTVA, co-occurring shock) and addressed in plain language?
- Failure-mode check: Look specifically for propensity-mistaken-for-uplift
  (fluent-but-wrong: a propensity ranking presented as a persuadables list) and for
  missing ground truth (a causal claim with no counterfactual / no named
  assumption).
```

**What to do with findings:** all Pass — the design is defensible; the persuadables view is real. One Fail — repair it (draw the holdout from the right stratum, swap the propensity ranking for a CATE/Qini ranking) and re-validate. Multiple Fails — discard the causal claim entirely; an uplift estimate without a defensible counterfactual is not evidence.

**AI Use Disclosure prompt:** *Write two sentences naming exactly what the AI did and the one judgment it could not make. Example: "I used Claude to draft the Qini computation and the difference-in-differences scaffold for the Jardiance study; I decided whether the parallel-trends assumption was defensible and whether my ranking measured uplift rather than propensity, because the model cannot reason about whether a co-occurring shock confounded the estimate."* (Mandatory.)

**Series connection:** the failure mode is **propensity-mistaken-for-uplift** at tier **T7** — the deepest error in the series, because prediction and causation feel identical in fluent output and only a counterfactual tells them apart.

## References (fact-check pass)

1. Künzel S.R., Sekhon J.S., Bickel P.J., Yu B. "Metalearners for estimating heterogeneous treatment effects using machine learning." PNAS 2019, doi:10.1073/pnas.1804597116. CONFIRMED — authors, venue, X-learner formalization exact.
2. Nie X., Wager S. "Quasi-oracle estimation of heterogeneous treatment effects." Biometrika 108(2):299–319 (2021). CONFIRMED — vol/issue/pages and Neyman-orthogonal/quasi-oracle property exact.
3. Wager S., Athey S. "Estimation and Inference of Heterogeneous Treatment Effects using Random Forests." JASA 113(523):1228–1242 (2018). CONFIRMED — exact.
4. Larkin I., Ang D., Steinhart J. et al. "Association Between Academic Medical Center Pharmaceutical Detailing Policies and Physician Prescribing." JAMA 2017;317(17):1785–1795. CONFIRMED — 19 AMCs/5 states, DiD, 6 of 8 classes, generic shift exact.
5. Eisenberg M.D., Stone E.M., Pittell H., McGinty E.E. "The Impact Of Academic Medical Center Policies Restricting Direct-To-Physician Marketing On Opioid Prescribing." Health Affairs 2020;39(6):1002–1010, doi:10.1377/hlthaff.2019.01289. CONFIRMED — finding exact; in-text attribution corrected from a prior mis-citation to "Larkin et al." (fact-check pass, 2026-06-17).
