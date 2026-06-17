# Chapter 13 — The Fellow Research Portfolio (Run One)
*A pre-registered "no" is a result. A literature summary is not.*

A Fellow finishes her first portfolio cycle and brings three things to the lab review. The first is a four-page literature summary on next-best-action models in pharma, well-organized and accurately cited. The second is a slide that says "MoE platforms claim 4–44% script lift" with the range pulled from vendor decks. The third is a notebook she half-built, then abandoned because "the data didn't really let me answer it."

The lab lead reads all three and asks one question: "If I hand any of these to the partner's data-science team on Monday, what would they *do* with it?"

Silence.

The summary is true and useless — it tells the partner what the field already says about itself. The slide repeats a vendor claim the book's entire thesis is built to distrust. The abandoned notebook is the only one that was doing real work, and she killed it for the right instinct (the data wouldn't support the claim) but the wrong reason. She treated "the data won't let me prove the strong version" as failure, when it is itself the finding.

The academic reflex says comprehensive review is value. The lab disagrees. The lab is an external-innovation function. Its only product is reduced uncertainty about where the partner should commit proprietary data and engineering. A paper summary reduces no uncertainty. A reproduced vendor claim reduces no uncertainty — it launders one. The abandoned notebook, rewritten as "here is what public data can and cannot establish about this claim, here is the design that would settle it, and here is the evidence level I reached," reduces a great deal of uncertainty.

This chapter is about producing the third thing on purpose.

---

## The seven-field card

Every project in this portfolio ships the same seven-field card. Part B requires it. The card is not a formality — it is the discipline made structural.

| Field | What it answers |
|---|---|
| **Question** | The falsifiable claim, tied to lift or brand. |
| **Public dataset (+ synthetic fallback)** | What you ran on, and what you'd simulate if access fails. |
| **Identification strategy** | How you impute the missing counterfactual — or why this is a benchmark, not a causal claim. |
| **Success threshold + kill criterion** | Pre-registered: what result would justify a handoff, and what result makes you walk away. |
| **Evidence-Ladder level reached** | The honest ceiling — and why public data caps you there. |
| **Compliance + patient-welfare flags** | MLR / fair-balance / Sunshine / HIPAA exposure, flagged and routed, never adjudicated. |
| **Likely partner owner** | Who on the partner side receives this if it advances. |

Two rules govern every card. First, the kill criterion is pre-registered — you write down what would make you abandon the project *before* you see the result, so that a disappointing finding cannot be quietly relabeled as a success. This is the antidote to the vendor-deck culture the book exists to push against. Second, the Evidence-Ladder ceiling is the firewall made operational. On public data you reach roughly Level 3 — a small offline test that beats a baseline. Levels 4 through 6 require the partner's proprietary data. If your card claims Level 4 on Open Payments and Part D, you have either misunderstood the ladder or broken the firewall.

| Field | What it answers |
|---|---|
| **Question** | The falsifiable claim, tied to lift or brand. |
| **Public dataset (+ synthetic fallback)** | What you ran on, and what you'd simulate if access fails. |
| **Identification strategy** | How you impute the missing counterfactual — or why this is a benchmark, not a causal claim. |
| **Success threshold + kill criterion** | Pre-registered: what result justifies a handoff, and what makes you walk away. |
| **Evidence-Ladder level reached** | The honest ceiling — and why public data caps you there. |
| **Compliance + patient-welfare flags** | MLR / fair-balance / Sunshine / HIPAA exposure, flagged and routed, never adjudicated. |
| **Likely partner owner** | Who on the partner side receives this if it advances. |

*Table 13.1 — The standard portfolio artifact: every Fellow project ships this card*

---

## Track A — Lift and attribution

**The logic.** The field's largest open methodological problem: industry script-lift figures (4 to 44 percent) are all vendor-generated, structurally inflated by attribution circularity (the platform serving the ad also measures the lift) and by selection (targeting concentrates on high-decile prescribers who both get targeted *and* prescribe anyway). The Fellow's job is not to produce a better lift number. It is to show, on public data, how much of a naive estimate is selection, and to specify what a credibly identified estimate would require.

**Three projects in this track.** A1 reconstructs a vendor-style lift estimate using Open Payments as a promotion-dose proxy and Part D as the prescribing outcome, joined on NPI, then re-estimates with a credible design and quantifies the gap. A2 specifies the natural experiment that would identify point-of-care EHR lift — a health-system on/off rollout, for example — and produces a power analysis showing what a real pilot would need; on public data this is design-grade work, which tops out at Level 2, and saying so plainly is the contribution. A3 decomposes observed prescribing change into promotion channels with an honest accounting of what cannot be separated without exposure-level data.

#### Worked project A1 — script-lift attribution audit

**Question.** How much of a vendor-style script-lift estimate is causal, and how much is selection?

**Dataset.** Open Payments (promotion dose per NPI) + Medicare Part D Prescriber (prescribing outcome per NPI), joined on NPI. Synthetic fallback: simulate exposure correlated with a latent prescribing propensity so the true effect is known and the selection inflation can be measured directly.

**Identification.** First, estimate the naive exposed-vs-unexposed difference with no control. Then re-estimate via matching plus a Rosenbaum-style sensitivity analysis, and — where a dated policy shock exists (a gift ban, an academic medical center detailing restriction) — a heterogeneity-robust difference-in-differences (Callaway & Sant'Anna 2021, *Journal of Econometrics* 225(2):200–230). Report the gap between the naive and design-based estimates.

**Success threshold.** A reportable, defensible quantification of selection inflation — the naive lift exceeds the design-based estimate by a margin with a confidence interval around it.

**Kill criterion.** No identifying variation and no credible counterfactual → downgrade to a design memo. Which is still a result: "public data cannot settle this; here is what would."

**Evidence-Ladder level.** L2 to L3.

**Compliance and welfare flags.** The finding that lift is inflated is partner-sensitive but welfare-neutral. Frame as de-risking the partner's own attribution claims, not as an accusation.

**Likely owner.** Measurement analytics.

**The failure mode.** Reporting the matched estimate as "the causal effect." Matching adjusts only for observed confounders; unobserved physician propensity still contaminates the comparison. The honest version reports a residual-confounding sensitivity — "an unobserved confounder of strength Γ would be needed to explain away this effect" — rather than a point claim. A Fellow who writes "we found the true lift is 12%" has reproduced the vendor's sin with better tools.

---

## Track B — Brand and physician identity

**The logic.** Brand equity in pharma is not name awareness. It is the physician remembering the patient type — "for *this* patient, after *this* prior therapy, Brand X is my default." The book's spine asks whether AI-driven promotion builds durable association or buys short-lived engagement. Track B tests that claim. The hard constraint: public data sees behavior well and attitudes poorly. Several B projects must proxy equity from behavioral persistence and label the proxy honestly.

**Four projects.** B1 tests whether share-of-mind predicts later share-of-market with a lag — the industry's central leading-indicator claim, asserted qualitatively but never rigorously tested on linked survey-plus-claims data; this is an open research question, not an established fact. B2 measures how persistent branded-prescribing patterns are across therapeutic classes, operationalizing "habit" and showing where equity is structurally durable. B3 tests whether brand equity or promotion intensity predicts prescribing persistence after controlling for ICER clinical-value score — an uncorrelated finding would be a high-impact policy result. B4 uses generic-entry date as an exogenous shock and estimates how much branded share persists after loss of exclusivity, and whether persistence correlates with pre-LOE equity.

#### Worked project B3 — brand equity versus ICER clinical value

**Question.** Does brand equity or promotion intensity predict prescribing persistence after controlling for independent clinical value?

**Dataset.** ICER reports (clinical-value score, extracted with LLM assistance and validated per Chapter 10's harness) + Part D (branded-share persistence) + Open Payments (promotion intensity).

**Identification.** Persistence regressed on equity and promotion, conditioning on ICER value plus market controls. The headline is the partial association of equity net of value. This is associational by design — flag it. The LOE event-study in B4 is the stronger causal companion.

**Success threshold.** Equity predicts persistence with clinical value held constant → equity functions as commercial memory, not clinical value. A high-impact finding.

**Kill criterion.** The equity effect vanishes once value is controlled, or ICER coverage is too sparse for the drug set to support the regression.

**Evidence-Ladder level.** L2 (associational); L3 when paired with B4's event-study.

**Compliance and welfare flags.** An equity-not-value finding is a patient-welfare finding — the system pays a premium for non-superior drugs. Route the framing carefully.

**The failure mode.** Treating ICER's value score as ground truth. ICER's QALY methodology is contested — disability and equity critiques, industry pushback — and drugs that reach ICER review are a selected set. The most-promoted, most-contested drugs are exactly the ones ICER evaluates. Conditioning on a covariate that is itself selected by the treatment is a trap. The honest version flags the QALY controversy and the selection-into-review problem, and treats ICER as one flagged benchmark among several.

---

## Track C — Model architecture and segmentation

**The logic.** Vendors label tabular targeting stacks "Mixture of Experts." The book's established position from Chapter 7: on medium-sized tabular data, gradient-boosted tree ensembles are state of the art (Grinsztajn, Oyallon & Varoquaux, "Why do tree-based models still outperform deep learning on tabular data?", NeurIPS 2022), and most "MoE" platforms are stacked ensembles relabeled — legitimate ML, but not MoE, and not obviously better than a tuned ensemble. These projects produce benchmark and audit evidence the partner's data-science team can act on directly.

**Three projects.** C1 builds a calibrated XGBoost/LightGBM baseline on a public NPI-propensity task and compares it to a routed model — the TIKTOC worked example. C2 asks whether routing or clustering geometry reveals a stable number of physician archetypes rather than an arbitrary k chosen for a slide template. C3 applies the three architectural criteria and the six buyer questions from Chapter 7 to public vendor "MoE" descriptions and reaches a verdict — pure desk research, no proprietary data, tops out at Level 2.

#### Worked project C1 — ensemble versus routed model on NPI propensity

**Question.** Does a routed, MoE-style model beat a tuned gradient-boosting baseline on an NPI prescribing-propensity task?

**Dataset.** NPI-propensity table built from Medicare Part D Prescriber (two-year-lagged outcome) + CMS Open Payments (promotion-dose features) + NPPES specialty and geography. Synthetic fallback: a simulated NPI feature matrix with known interaction structure, in case join coverage is too thin.

**Identification.** This is a benchmark, not a causal estimate. Both models tuned with equal effort and the same compute budget — logged. Evaluation: out-of-time validation (train on year *t*, test on *t+1*), calibration curves (reliability diagram plus Brier score), and subgroup robustness across specialty and prescribing-decile bands. AUC is reported but is not the headline.

**Success threshold.** The routed model improves out-of-time calibration and holds or improves subgroup robustness, with the gain large enough to matter operationally — not a third-decimal AUC improvement.

**Kill criterion.** No improvement over the tuned tree ensemble, or worse calibration, or a gain too small to justify the routing infrastructure.

**Result (the completed card).** The tuned LightGBM baseline matched the routed model on AUC and beat it on calibration — lower Brier score, better reliability in the tails. Subgroup robustness was equivalent. The routed model added substantial training and inference complexity for no operational gain. Kill criterion met.

**Evidence-Ladder level.** L3 — a small offline test that beats the baseline. Here, the baseline is the winner.

**Compliance and welfare flags.** Minimal. Note for handoff: a "no lift" finding protects the partner from an unjustified architecture investment.

**Likely owner.** Data science.

**Plain-language readout.** "We tested whether the 'mixture-of-experts' model the vendor deck describes would beat a standard, well-tuned model on the kind of physician-targeting task we care about. With equal effort on both, the standard model was as accurate and *better calibrated* — its probability estimates were more trustworthy — at a fraction of the complexity. Recommendation: do not invest engineering in the routed architecture for this task. This 'no' just saved us the build."

**The failure mode.** The rigged benchmark: lovingly tune the fancy routed model, leave the baseline at defaults, and "discover" the fancy model wins. The integrity check is equal tuning effort on both models and calibration reporting, not just AUC. A benchmark where the baseline was sandbagged is worse than no benchmark — it manufactures exactly the false positive the lab exists to prevent. The honest C1, where a well-tuned XGBoost beats or ties the routed model, is a *successful project*.

| Field | C1 entry |
|---|---|
| **Question** | Does a routed, MoE-style model beat a tuned gradient-boosting baseline on an NPI prescribing-propensity task? |
| **Public dataset (+ synthetic fallback)** | Part D Prescriber + Open Payments + NPPES specialty/geography, joined on NPI; synthetic NPI feature matrix with known interaction structure if join coverage is thin. |
| **Identification strategy** | Benchmark, not causal. Both models tuned with equal logged effort; out-of-time validation, calibration (Brier + reliability), subgroup robustness. |
| **Success threshold + kill criterion** | Success: routed model improves out-of-time calibration and holds subgroup robustness with operationally meaningful gain. Kill: no improvement, worse calibration, or gain too small to justify routing. |
| **Evidence-Ladder level reached** | L3 — small offline test; here the baseline wins. |
| **Compliance + patient-welfare flags** | Minimal; a "no lift" finding protects the partner from an unjustified architecture investment. |
| **Likely partner owner** | Data science. |
| **Result** | Tuned LightGBM matched routed model on AUC, beat it on calibration; subgroup robustness equivalent. Kill criterion met. |

*Table 13.2 — A completed portfolio card for a project whose result was "no." The "no" is the deliverable.*

---

## Track D — Privacy, fairness, and accountability

**The logic.** The adversarial track — empirically answerable fairness and welfare questions the field leaves unexamined. It carries the highest partner-framing tension. Frame every project here as collaborative de-risking: you are testing the partner's own claims so the partner does not get caught believing them. Whether and how adversarial these projects can be is a standing blocker that requires partner sign-off before running. [contested — see pantry, Risk 1]

**Three projects.** D1 tests whether propensity and targeting models encode proxies for physician susceptibility — or for protected-correlated attributes — rather than clinical need. Proxy discrimination is a facially neutral feature acting as a stand-in for a protected attribute; whether targeting models do this is unexamined and answerable on public data, though physician-level protected attributes are not in Part D or Open Payments, so this likely relies on area-level proxies and tops out at Level 2. D2 replicates and extends the Dafny–Ody–Schmitt design to estimate how much co-pay coupons suppress generic substitution. D3 produces a normative framework for what monitoring, disclosure, and auditability a deployed targeting system should carry — the direct input to Chapter 14's patient-welfare gate.

#### Worked project D2 — co-pay coupon generic suppression

**Question.** How much do co-pay coupons suppress generic substitution and raise system cost?

**Dataset.** Medicaid State Drug Utilization Data (state × quarter generic versus branded units and spend) + LOE and generic-entry dates. Coupon-legality variation — coupons are banned in Medicare; state rules vary — is the design.

**Identification.** Difference-in-differences with cross-state legality contrast around generic entry — the Dafny–Ody–Schmitt template (Dafny, Ody & Schmitt, "When Discounts Raise Costs: The Effect of Copay Coupons on Generic Utilization," *American Economic Journal: Economic Policy* 9(2):91–123, 2017; NBER WP w22745), which found that coupons raise branded sales by more than 60 percent, entirely by displacing bioequivalent generics; heterogeneity-robust if timing is staggered (Callaway & Sant'Anna 2021, *Journal of Econometrics* 225(2):200–230).

**Success threshold.** A credible, signed estimate of generic-substitution suppression with valid pre-trends — an event-study plot with leads near zero.

**Kill criterion.** No clean legality or timing variation; pre-trends fail.

**Evidence-Ladder level.** L3 — this design is well-precedented.

**Compliance and welfare flags.** High. This directly tests a partner product line (co-pay programs). A suppression finding has clear patient-welfare and policy weight. Secure partner sign-off on framing before running; route any legal characterization to counsel.

**Likely owner.** Compliance and medical-commercial.

**The failure mode.** Ecological inference. Medicaid SDUD is aggregated to NDC × state × quarter — it does not observe individual patients or individual substitution decisions. Reporting "coupons cause patients to stay on the brand" overclaims patient-level behavior from state-level aggregates. The honest version states the estimate at the level the data supports — state-quarter generic share — and explicitly flags that individual substitution is inferred, not observed.

![Evidence Ladder with rungs L0 to L6; the four portfolio tracks plotted by the level public data lets them reach — Track A and Track B span L2 to L3, Track C sits at L3, Track D splits with D1 and D3 at L2 and D2 at L3 — and a red horizontal line above L3 labeled "proprietary data required" marking the public-data ceiling.](../images/13-fellow-research-portfolio-fig-01.png)

*Figure 13.1 — The public-data ceiling is the firewall made visible*

<!-- → [DIAGRAM: Evidence-Ladder with the four tracks placed on it — Track A at L2–L3, Track B at L2–L3, Track C at L3, Track D at L2 (D1/D3) and L3 (D2). Arrow above L3 labeled "proprietary data required." Caption: "The public-data ceiling is the firewall made visible. Claims above the ceiling belong in the partner handoff, not in the portfolio."] -->

---

## What the portfolio is not

Three misconceptions deserve direct statement.

A comprehensive literature review is not a portfolio project. A review summarizes what the field says about itself. A portfolio project tests a claim and reduces uncertainty. The lab grades the second.

If public data cannot prove the strong version, the project did not fail. "Public data establishes X, cannot establish Y, and here is the design that would" is a result — often the most valuable one, because it tells the partner exactly what proprietary work to fund. The A2 design memo, which tops out at Level 2 and says so plainly, is a better artifact than a Level 3 result that quietly overstates its reach.

A negative result did not waste the cycle. The C1 "no lift" outcome saved an engineering budget. The A1 "the lift is mostly selection" outcome stopped the partner believing its own attribution. A pre-registered kill is the portfolio's honesty mechanism, not its failure mode. The discipline is: you write the kill criterion before you see the result, and you apply it without spin after.

---

## What would change my mind

The portfolio's stances are testable and the book holds them open. The claim that public-data lift estimates are mostly selection would require revision if an A1-style audit, run honestly with a credible design, recovered a naive estimate close to the design-based one across multiple drug classes. The claim that routed models do not beat tuned ensembles on tabular NPI tasks would require revision if an equally tuned, calibration-reported C1 benchmark showed a meaningful, reproducible gain. The working assumption that brand equity is often commercial memory rather than clinical value would require revision if B3 and B4 found equity persistence tracking ICER value once selection-into-review is handled. These are falsifiable claims, not positions. The portfolio is how you falsify them.

## Still puzzling

Public data tops out around Level 3. How much of the partner's real uncertainty actually lives below Level 3, where a Fellow can reach it, versus above it, where only proprietary replication can? If most of the uncertainty is above the ceiling, the portfolio's value is in design specification — telling the partner what to fund — rather than in results. That would shift what the lab optimizes for, and it is not yet clear which it is.

For tabular NPI tasks there is no token sequence and no obvious unit of routing. So what would "specialization" mean for a physician-archetype model in C2? Is a "natural N" of physician segments a real structural fact the data is trying to tell you, or an artifact of the clustering objective — a number you chose pretending the data chose it?

---

## Exercises

**Warm-up**

1. *(Recall — tests the portfolio discipline)* For each of the four tracks, write one sentence stating what uncertainty a project in that track reduces for the partner. Then classify these four research artifacts: a four-page summary of next-best-action literature; a DiD estimate of coupon generic-suppression with pre-trends; a vendor lift figure pulled from a deck; a design memo specifying the natural experiment needed to identify EHR lift. *What this tests: whether you can distinguish evidence that reduces uncertainty from evidence that launders it.*

2. *(Recall — tests the kill criterion)* Explain why the kill criterion must be pre-registered before seeing the result. Give one concrete example of what a kill criterion looks like for project A1 and one for project C1. *What this tests: whether you understand the kill criterion as a honesty mechanism, not a failure declaration.*

3. *(Recall — tests the Evidence-Ladder ceiling)* State why public data caps most portfolio projects at Level 3, and name the specific thing that would be required to reach Level 4. Then explain why a project card claiming Level 4 on Open Payments and Part D is a red flag. *What this tests: whether you can apply the firewall operationally rather than abstractly.*

**Application**

4. *(Apply — benchmark integrity)* Take the C1 worked example and rig it: describe exactly what you would change to make the routed model appear to win — tuning asymmetry, metric selection, subgroup cherry-picking. Then write the three integrity checks a reviewer should apply to catch each rig. *What this tests: whether you can spot the failure mode by building it.*

5. *(Apply — seven-field card)* Choose one project from Tracks A, B, or D. Write its full seven-field card, including a pre-registered kill criterion specific enough that, after seeing the result, no honest person could relabel a failure as a success. State the Evidence-Ladder ceiling and justify it from the data's limits. *What this tests: whether you can operationalize the portfolio discipline on a project of your choice.*

6. *(Apply — ecological inference)* The D2 project uses Medicaid SDUD aggregated to NDC × state × quarter. A partner asks: "So patients on the brand are less likely to switch to a generic because of the coupon?" Write the two-sentence correction that states what the data can and cannot establish, and name the specific inference error the partner's question would commit. *What this tests: whether you can apply the ecological-inference caveat precisely in context.*

**Synthesis**

7. *(Synthesize — tracks and the partner)* A partner's data-science team asks which of the four tracks is most worth investing their proprietary data in. Write a one-page recommendation that evaluates each track by: the uncertainty it reduces, the Evidence-Ladder level public data reaches, and what proprietary data would unlock above that ceiling. Do not rank — map. *What this tests: whether you can connect the portfolio's public-data work to a partner's decision about where to spend.*

8. *(Synthesize — failure modes)* The chapter names a characteristic failure mode for each exemplar: calling a matched estimate causal (A1), treating ICER as ground truth (B3), rigging the benchmark (C1), and ecological inference (D2). For each failure mode, state the structural pressure that makes it tempting — the incentive or deadline that pushes a Fellow toward it — and the single integrity check that catches it. *What this tests: whether you understand the failure modes as predictable behavioral patterns, not just technical errors.*

**Challenge**

9. *(Challenge — Part B)* Run one project end to end on public or synthetic data. Produce: (a) the completed seven-field card with a pre-registered kill criterion written before you see any results; (b) the analysis notebook with logged tuning decisions; and (c) a plain-language readout of 150 words or fewer that states what you found, the honest evidence level, and what you recommend the partner do. A defensible "no" earns full marks. Your AI Use Disclosure must name one judgment no automated layer could make for you. *What this tests: whether you can run the full portfolio discipline on a real project and ship the honest result.*

---

## Prompts

### Figure 13.1 — The four tracks on the Evidence Ladder

Build a single self-contained HTML file (inline CSS, no external assets except D3) that renders a vertical "Evidence Ladder" diagram. The y-axis is the evidence level, a discrete ordinal scale with rungs L0 at the bottom through L6 at the top; render each rung as a faint horizontal gridline with a monospace tick label. The x-axis is categorical: four portfolio tracks placed side by side — Track A (Lift), Track B (Brand), Track C (Models), Track D (Ethics/Privacy). Each track is drawn as a vertical span (a thin capsule or bar) covering the levels it can reach on public data: A spans L2–L3, B spans L2–L3, C sits at L3 only, D splits into two markers — D1/D3 at L2 and D2 at L3. Mark each span endpoint with a small node and a short label. Encode level on y (position), track on x (position); use position, not color, as the primary channel. Draw one red horizontal line across the full plot just above the L3 rung, labeled "proprietary data required" — this is the public-data ceiling and the only red element. Add a caption note: "Claims above the ceiling belong in the partner handoff, not in the portfolio." Make each track marker interactive (focusable, tabindex, aria-label). Deliverable: one HTML file using D3 7.9.0 from cdnjs, inline FALLBACK_DATA, light and dark CSS variables, ResizeObserver redraw.

---

## Chapter 13 Exercises: The Fellow Research Portfolio (Run One)

**Project:** One Drug, End to End
**This chapter adds:** You assemble your drug's four-track portfolio as seven-field cards — one per track (Lift, Brand, Models, Ethics/Privacy) — each with a pre-registered kill criterion written before any result, so a disappointing finding cannot be relabeled as a success.

*Worked example throughout: **Cardizem-X**, the branded cardiometabolic drug from Chapters 11–12, now carried into four portfolio cards. Swap in your own drug wherever the notes say so.*

### Exercise 1 — When to Use AI

A pre-registered "no" is a result; a literature summary is not. Use AI for the structural scaffolding of the cards, where you can check the output against the chapter's fixed seven-field template.

1. **Lay out four blank seven-field cards.** Ask an LLM to emit the seven-field card structure (Question, Public dataset + synthetic fallback, Identification strategy, Success threshold + kill criterion, Evidence-Ladder level, Compliance + welfare flags, Likely partner owner) four times, one per track, pre-filled with your drug name and the track logic from Table 13.1. *Why AI works here:* the field set is closed and the track definitions are in the chapter, so a missing or mislabeled field is caught instantly against Table 13.1.
2. **Draft the plain-language readout from a completed card.** Hand the model a finished card and ask for the 150-word readout in the chapter's no-spin register. *Why AI works here:* the readout must restate facts already fixed in the card; you compare sentence-by-sentence against the card and any drift or inflation is visible.

**The tell:** in both tasks you can independently evaluate the output against a fixed template and a completed card — the model fills a known structure, it does not decide what goes in the load-bearing fields.

### Exercise 2 — When NOT to Use AI

1. **Setting the pre-registered kill criterion.** *Why AI fails here:* the kill criterion is the portfolio's honesty mechanism — it must be written before the result and held without spin after. An LLM cannot pre-register on your behalf, and worse, if you paste a result it will quietly relabel a failed threshold as a success ("the effect, while modest, suggests..."), which is exactly the vendor-deck move the chapter exists to push against.
2. **Judging whether your result honestly met or missed the threshold.** *Why AI fails here:* deciding that the equity effect "vanished once value was controlled" (B3's kill) or that the baseline tied the routed model on calibration (C1's kill) is a judgment about whether the signal survived — a real-versus-noise call the model cannot make from the numbers, and one it tends to resolve in the optimistic direction.

**The tell:** AI as *reason* vs. *tool* — if a project is alive because the model framed the result as promising, AI has become the reason; it may only format cards around kill decisions you own. **Series connection:** these are **T7 Wisdom** judgments — the pre-registered kill and the honest threshold call are individual scientific integrity — operating inside a **T6 Collective** discipline, since the portfolio's credibility depends on the whole lab holding the same no-spin standard, not one Fellow's private restraint.

### Exercise 3 — LLM Exercise

**What you're building:** four pre-registered seven-field cards for your drug — one per track — each with a kill criterion fixed before any result and an honest Evidence-Ladder ceiling.

**Tool:** Claude, continuing the **Claude Project** "One Drug — Cardizem-X." Persistent context is doing real work now: the model already holds the drug, class, KPIs, firewall ceiling, and the Chapter 12 identification memo, so it can reuse your loss-of-exclusivity design as the Track B card rather than inventing a new one.

**The Prompt:**

```
Continuing the One Drug project for Cardizem-X (branded cardiometabolic drug, two generics,
one branded competitor, loss of exclusivity ~18 months out). Public data only: Open Payments,
Part D Prescriber PUF, Medicaid SDUD, ICER. Reference "AI-Driven Programmatic HCP Marketing,"
Chapter 13 and its four tracks.

Draft FOUR seven-field portfolio cards for Cardizem-X, one per track:
- Track A (Lift): how much of a vendor-style script-lift estimate for Cardizem-X is selection
  vs. causal (Open Payments dose + Part D outcome, joined on NPI).
- Track B (Brand): does branded-share persistence after loss of exclusivity exceed a no-equity
  baseline once ICER value is controlled (reuse my Chapter 12 loss-of-exclusivity design).
- Track C (Models): does a routed "MoE-style" model beat a tuned gradient-boosting baseline
  on a Cardizem-X NPI-propensity task (benchmark, equal logged tuning, calibration reported).
- Track D (Ethics/Privacy): do co-pay coupons for Cardizem-X suppress generic substitution
  (Medicaid SDUD + coupon-legality variation, Dafny-Ody-Schmitt template).

For EACH card produce all seven fields: Question; Public dataset (+ synthetic fallback);
Identification strategy (or "benchmark, not causal"); Success threshold + PRE-REGISTERED
KILL CRITERION written as if before any result; Evidence-Ladder level reached (public data
caps near L3 — justify); Compliance + patient-welfare flags (flagged and ROUTED, never
adjudicated); Likely partner owner.

CRITICAL: write each kill criterion specifically enough that, after seeing a result, no honest
person could relabel a failure as a success. Do NOT pre-decide whether any threshold was met
— leave the Result field blank for me. Flag uncertain numbers with [verify].
```

**What this produces:** four pre-registered cards for your drug, each with a falsification-proof kill criterion and an honest ceiling — the assembled portfolio Chapter 14 will decide on.

**How to adapt:** swap Cardizem-X and its four track instantiations for your own drug; on ChatGPT or Gemini, paste the four-track definitions from the chapter each session, since they lack the persistent Project that carries them automatically.

**Connection to previous chapters:** Track B reuses the Chapter 12 identification memo; every card's ceiling enforces Chapter 11's firewall; the kill-criterion discipline is the lean-startup validated-learning idea from Chapter 11 made pre-registered.

**Preview of next chapter:** Chapter 14 is the capstone — it takes these four cards, applies the TEST/BUILD/KILL decision and the patient-welfare gate, and assembles the integrated one-drug case study plus partner handoff.

### Exercise 4 — CLI Exercise

**What you're building:** the assembled four-card portfolio for your drug as a coherent multi-file case folder, plus a manifest that checks every card has a non-empty pre-registered kill criterion.

**Tool:** **Cowork** — why: this is multi-file assembly (four cards, a manifest, a portfolio README) across a folder, which is exactly what Cowork's multi-file orchestration is for; a single-thread tool would fight the cross-file consistency check. · **Skill level:** intermediate.

**Setup (3-item checklist):**
- A Cowork session with a `cardizem-x-portfolio/` folder containing `cards/` and an empty `_MANIFEST.md`.
- The four card drafts from Exercise 3 saved as `cards/track-a.md` … `cards/track-d.md`.
- A `CLAUDE.md` line: public/synthetic data only; every card's kill criterion must be present and pre-registered; never write a partner-proprietary value.

**The Task:**

```
In cardizem-x-portfolio/, working across the four files in cards/:
- READ the four track cards in cards/;
- WRITE only _MANIFEST.md and a new cards/_portfolio-readme.md;
- LEAVE the four card files themselves unedited (do not rewrite my kill criteria).

Build _MANIFEST.md as a table with one row per card: track, question, Evidence-Ladder level,
and a PASS/FAIL column "kill criterion present and pre-registered (non-empty, no result-shaped
language)". Build cards/_portfolio-readme.md summarizing the four tracks in two sentences each,
no spin.

STOP after both files are written. If any card's kill criterion is missing or reads like it
was written after a result ("the modest effect suggests..."), mark it FAIL in the manifest and
print which card — do NOT fix the card yourself; assembling is your job, judging the criterion
is mine. VERIFY by opening _MANIFEST.md and confirming four rows with a PASS/FAIL each.
Do not commit or push.
```

**Expected output:** `_MANIFEST.md` with four rows and PASS/FAIL kill-criterion flags, plus `cards/_portfolio-readme.md`.

**What to inspect:** the FAIL rows — these are the cards where the kill criterion is missing or result-shaped, the precise integrity defect the chapter warns about. The fix is yours, not the tool's.

**If it goes wrong:** if Cowork edits a card's kill criterion to "fix" a FAIL, stop it: "do not edit the cards; only flag them in the manifest." Recovery: restore the card from your Exercise 3 draft; nothing was committed.

**CLAUDE.md note:** add "Assembly tools may flag a missing or post-hoc kill criterion but must never rewrite it — relabeling a failed threshold as a success is the failure mode the portfolio exists to prevent."

### Exercise 5 — AI Validation Exercise

**What you're validating:** one completed portfolio card for your drug (with a Result filled in) — checking that the pre-registered kill criterion was applied honestly and not relabeled as a success.

**Validation type:** kill-criterion integrity and benchmark-honesty audit. **Risk level:** high — a relabeled kill ships a false positive to the partner, manufacturing exactly the inflated finding the lab exists to prevent.

**Setup:** use a card from Exercise 3 with a Result you add, or generate a flawed artifact: ask the model to "write the Track C card for Cardizem-X where the routed model tied the baseline on AUC and lost on calibration, but conclude the routed model is promising." Validate that.

**The Validation Task:**

```
Validation Checklist — Chapter 13 (Fellow Research Portfolio)
For the pasted completed card, mark each Pass / Fail / Cannot-determine:

- Correctness: does the stated result actually meet the success threshold, or did it meet the
  kill criterion?
- Completeness: all seven fields present, including a pre-registered kill criterion?
- Scope: public/synthetic data only; Evidence-Ladder level <= 3 and justified?
- Chapter-specific 1 (Kill integrity): does the verdict match the pre-registered criterion, or
  was a failed threshold relabeled as a success?
- Chapter-specific 2 (Benchmark/association honesty): for Track C, equal logged tuning and
  calibration reported (not AUC alone)? For Track A/B, is a matched/conditioned estimate
  honestly flagged as associational rather than called "the causal effect"?
- Failure-mode check: does the card commit KILL-CRITERION-RELABELED-AS-SUCCESS (a "no" dressed
  as a "promising"), a RIGGED BENCHMARK, or MATCHED-ESTIMATE-CALLED-CAUSAL? Is it fluent-but-
  wrong — confident, well-formatted spin over a result that should have killed the project?
- Ground truth: is the result checkable against the pre-registered threshold, or is the ground
  truth (the threshold) missing or vague?
```

**What to do with findings:** all pass — the card advances to the Chapter 14 decision. One fail — restore the honest verdict (a defensible "no" earns full marks) and re-validate. Multiple fails — return to Exercise 3; a card whose kill was relabeled and whose benchmark was rigged is not salvageable, it is the failure mode itself.

**AI Use Disclosure prompt:** *Write two sentences naming what an AI tool did in your Chapter 13 work and the one judgment it could not make — for example, that you used Claude to lay out four seven-field cards and draft the plain-language readouts for Cardizem-X, but you wrote and held each pre-registered kill criterion yourself and decided whether each result honestly met or missed it, because the model would relabel a disappointing finding as promising.* (Mandatory.)

**Series connection:** the failure mode is **kill-criterion-relabeled-as-success**, and the validating judgment is **T7 Wisdom** held to a **T6 Collective** standard — the portfolio is trustworthy only if the whole lab applies the no-spin kill discipline, not one Fellow in private.
