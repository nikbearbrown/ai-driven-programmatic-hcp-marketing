# Chapter 5 — The Evidence Problem

## 1. Overview

This is the chapter the rest of the book leans on. By the end of it you will be able to take any effectiveness claim in pharma HCP marketing and locate it precisely on two axes — *how strong is the study design* and *how independent is the source* — and you will be able to explain, in plain language, why almost every claim you meet is an **association** dressed up as a **causal** fact. You will learn the four mechanisms that make exposure-and-outcome correlations systematically overstate true effect; you will learn a per-channel evidence taxonomy you can grade with; you will see, channel by channel, where the independent evidence is genuinely strong (detailing, meals, academic detailing) and where it is genuinely absent (EHR/point-of-care advertising — the field's largest open validation gap). And you will practice the most transferable skill in the book: reading a document in which *every sentence is literally true and none of it is causal evidence.* A warning the chapter holds itself to: the critical evidence is not automatically better than the industry's. The meal-and-prescribing findings are observational too. We will say so out loud, because a chapter that applies one standard to claims it dislikes and another to claims it likes has no standard at all.

## 2. Learning Objectives

1. **(Analyze)** Evaluate an effectiveness claim against the standard for causal inference — name why association ≠ causation, and identify which of the four overstatement mechanisms is in play.
2. **(Evaluate)** Rate the evidence quality of each major HCP marketing channel using a structured taxonomy combining study-design strength and source independence.
3. **(Create · Part B)** Write the evidence map for your own research thread and select the public dataset you will use — the graded checkpoint for this week.

## 3. Opening Case — The 44% Lift Where Every Sentence Is True

A vendor case study crosses your desk. It is one page, it is well designed, and it claims a **44% script lift** from an AI-driven EHR advertising program. Read it slowly. Here are its sentences, and here is what is true about each.

> *"Physicians exposed to the program prescribed the brand 44% more than physicians who were not exposed."* — **True.** The exposed group did prescribe more. This is a measured fact about two groups.

> *"Exposure was triggered by the relevant diagnosis code in the EHR, ensuring clinical relevance."* — **True.** The trigger fired on the ICD-10 code. The targeting worked as described.

> *"Lift was measured at the NPI level using linked prescribing data."* — **True.** They did link exposure to each physician's actual prescriptions. The measurement is real.

> *"The program targeted high-potential prescribers identified by our predictive model."* — **True — and fatal.** The exposed physicians were *selected because they were already likely to prescribe more.* Their higher prescribing is exactly what the targeting model was built to find.

> *"Measurement and delivery run on a single unified platform for seamless attribution."* — **True — and the second fatal sentence.** The party that served the ad is the party that measured the lift. There is no independent firewall between the commercial interest in a high number and the production of the number.

Every sentence is accurate. The page contains no lie. And the page contains *no causal evidence whatsoever*, because the two fatal sentences describe **selection on the outcome** and **attribution circularity** — two of the four mechanisms that make this kind of association overstate the true effect. The 44% is real as a *difference between groups*; it is unknown as an *effect of the ad*, because we never see what those same high-potential physicians would have prescribed un-exposed.

*(The 44% and all figures in this case are illustrative of vendor-reported ranges and are `[verify]` — they stand for the 4–44% script-lift claims that circulate in this market, none independently validated.)*

That is the skill: seeing truth and non-evidence occupy the same page. Hold onto it. It generalizes to every deck you will ever read.

## 4. Core Sections

### 4.1 Association is not causation — and the four mechanisms that bias it upward

The core distinction is old and simple to state: an **association** is "exposed physicians prescribed more than unexposed physicians"; a **causal** claim is "the exposure *caused* the additional prescribing." The first is a fact about the data. The second is a fact about a counterfactual world — what the *same* physicians would have done un-exposed — which the data, on its own, never shows you (this is the formal core of Chapter 8). The gap between the two is the entire chapter, and it does not close on its own.

Worse, in this market the gap is not random — it leans in one direction. Four mechanisms make the association *systematically overstate* the causal effect, and you should be able to name all four:

1. **Selection / targeting on the outcome.** Platforms target high-propensity prescribers — high deciles, rising NBRx, on-label patient mix. Those physicians were *already* going to prescribe more. Measuring their post-exposure prescribing and crediting the delta to the ad confounds the targeting signal with the treatment effect. (This is the propensity-vs-incrementality inversion you will meet formally in Chapter 8.)

2. **Attribution circularity.** The platform that *serves* the ad also *measures* the lift, using the same NPI-linked infrastructure for both. Targeting and measurement are not independent; there is no firewall between the party with a commercial interest in a high number and the party producing it. As the field synthesis puts it, there is "inherent measurement circularity… no independent academic literature validating the attribution models."

3. **Absence of a control / counterfactual.** "Lift" without a randomized or quasi-randomized holdout is a before/after or exposed/unexposed comparison, not an estimate of the counterfactual. With no control group, there is no way to subtract what would have happened anyway.

4. **Publication / reporting asymmetry.** Vendor case studies report wins; nobody publishes the campaign that did nothing. As §4.4 shows, the same disease afflicts the *peer-reviewed* literature at its source through selective outcome reporting.

Any single mechanism is enough to inflate a number. EHR script-lift claims usually carry all four at once.

### 4.2 The evidence-quality taxonomy — the gradeable artifact

To rate a claim you need a ladder, and a defensible rating uses *two* ladders at once.

**Study-design strength** (descending causal credibility):

> RCT / pre-registered experiment > natural experiment with credible identification (difference-in-differences, regression discontinuity, instrumental variables) > matched observational / propensity-adjusted > unadjusted exposed-vs-unexposed > vendor case study / testimonial.

**Source independence** (descending):

> independent peer-reviewed > government / nonprofit > industry-funded but peer-reviewed > vendor white paper / case study (un-refereed, commercial interest).

A claim's grade is roughly the *minimum* of its two scores — a perfectly designed study reported only in a vendor brochure is still compromised by the conflict, and an independent source reporting an unadjusted before/after is still weak by design. Apply this to the opening case: the 44% claim scores **low on both axes** — unadjusted exposed-vs-unexposed design, vendor-produced. That is the chapter's punchline rendered as a grade.

The taxonomy is also the conceptual seed of the lab's **Evidence Ladder** (Chapter 11), which runs from "interesting claim" (Level 0) to "client-validated incremental impact" (Level 5). Same idea, operationalized for the handoff brief.

### 4.3 The channels, ranked by independent evidence — including where the critique is strong

Now walk the channels. Some pharma tactics have *strong, independent* evidence behind them. Naming those honestly is what gives your skepticism about EHR ads its credibility.

**Detailing (sales-rep visits) — strong independent evidence it works.** The oldest, most-studied tactic. Systematic reviews consistently find that physicians who receive industry information, rep contact, or free samples increase prescribing of the paying company's drugs. The canonical *Annals of Internal Medicine* systematic review finding: physicians' belief that accepting payments will not affect their practice is *not well-founded* — the data show measurable prescribing changes despite self-reported immunity. This is the third-person effect made quantitative: everyone thinks they are immune; the data says no one is. [verify exact author/year of the Annals review before publication.]

**Meals and gifts — strong evidence, with a dose-response — and observational.** DeJong et al., *JAMA Internal Medicine*, 20 June 2016, linked CMS Open Payments to Medicare Part D prescribing for the most-prescribed branded drug in four classes — rosuvastatin (Crestor), nebivolol (Bystolic), olmesartan (Benicar), desvenlafaxine (Pristiq). Across n = 279,669 physicians and 63,524 relevant meal payments (Aug–Dec 2013), receipt of even a *single* industry-sponsored meal (mean value under $20) was associated with higher rates of prescribing the promoted brand, and the rate rose with the number and value of meals — a dose-response. [Verified: jamanetwork.com article 2528290; PubMed 27322350.]

Here is the honesty the chapter requires: **this is observational, association evidence.** Physicians who accept meals may differ systematically from those who do not — in specialty, patient mix, or baseline prescribing — and the study cannot rule that out. The dose-response relationship and the single-meal threshold *strengthen* the causal interpretation; they do not *prove* it. If you would demand a control group from the vendor's 44%, intellectual honesty demands you note the same limit here. The meal finding is *better* evidence than the vendor case study — larger N, independent source, dose-response, peer-reviewed — but it is not gospel, and the book does not pretend it is.

**Academic detailing — strong RCT evidence it works (the counter-model).** Unbiased educational outreach from non-commercial teams: the same high-touch format as pharma detailing, the opposite agenda. A recent systematic review in *JAMA Network Open* (2024/25) examined 118 randomized and non-randomized studies; among the 36 lowest-risk-of-bias studies, 25 (69%) showed significant improvement in at least one prescribing behavior, with a median absolute change of 4.0% in the intended direction. The older 2007 Cochrane meta-analysis of educational outreach visits (69 RCTs) found a median absolute change of about 5.6%. [verify exact authors/year of the JAMA Netw Open review and the Cochrane figure.] The teaching value is sharp: *same channel, opposite funder incentive, rigorous evidence.* The format is a vehicle; the agenda is the variable. Academic detailing is also chronically underfunded relative to commercial detailing (the VA program is the main scaled example).

**A genuine exception — detailing can inform, not only persuade.** A study of Crestor (contraindicated in elderly and Asian patients) found detailing *reduced* prescribing to contraindicated patients — evidence the informative function is real. But it is bundled in the same visit as the persuasive function. Pharma funds detailing to raise scripts; the safety benefit is real but incidental. [verify citation.]

**EHR / point-of-care advertising — the evidence gap (this chapter's center of gravity).** The fastest-growing channel with the thinnest independent evidence. Vendor-reported script lifts span 4–44% depending on therapy and channel; OptimizeRx reports 19–25% from NPI-level analysis; a vendor breakdown cites roughly 11.9% (informational messages, 8 programs) and 11.5% (brand plus savings offer, 27 programs). [All figures vendor-sourced, un-refereed, `[verify]`.] When you search for *independent, peer-reviewed* evidence on this channel, you find almost exclusively vendor marketing pages — which is itself the finding. **No independent, peer-reviewed study validates the causal attribution behind these numbers, and no peer-reviewed study has assessed whether EHR-embedded ads produce clinically appropriate versus inappropriate prescribing.** This is the single largest open validation gap in the field, and it is where the gap in the *evidence* and the gap in the *regulation* coincide (see §7).

### 4.4 The evidence base is contaminated at its source

You might hope to escape vendor circularity by retreating to the peer-reviewed literature. Partly you can — that is what §4.3's independent findings are for. But the literature itself is not clean where industry controls trial design, analysis, and publication.

The canonical case is **GlaxoSmithKline Study 329** (paroxetine/Paxil in adolescents). The published report claimed paroxetine was "generally effective" for adolescent depression. The conclusion came from *post-hoc outcome switching*: the pre-specified primary outcomes were negative, and the positive conclusion was assembled afterward from secondary measures. The drug was ineffective and carried suicidality risk in the studied population. The paper was not corrected or retracted for years, and prescribing continued in the interim. (A 2015 RIAT re-analysis in the *BMJ*, Le Noury et al., restored the original data and reversed the conclusion. [verify citation.])

The pattern generalizes. In the antidepressant literature, an estimated 98% of positive trials were published versus 48% of negative ones; correcting for publication bias plus outcome switching collapsed an apparent 2-to-1 efficacy signal — "the drugs still work, but perhaps half as well as you believed." And only about 31% of medical meta-analyses even check for publication bias [verify — from *Science Fictions*, Ritchie]. The lesson for the Fellow: the problem is not only the vendor case study. The evidence base is contaminated at its source wherever the funded party controls the pipeline. Skepticism is not anti-industry; it is the price of admission to *any* claim, including the ones critical of industry.

## 5. Worked Example — Mapping the Evidence of One Tactic

**Task.** You are asked: "Is our EHR co-pay-message program worth expanding?" Build the evidence map.

**Step 1 — name the dependent variable.** Is this a *lift* claim (incremental scripts) or a *brand* claim (durable association)? The program's stated goal is more scripts: it is a **lift** claim, so it requires a control group. (You cannot grade evidence until you know which variable it asserts to move — Chapter 2.)

**Step 2 — find the best available evidence and grade it on both axes.** The vendor supplies a 19% NPI-level lift figure. Design strength: unadjusted exposed-vs-unexposed → low. Source independence: vendor-produced → low. Grade = min(low, low) = **weak**. There is no independent peer-reviewed estimate to set beside it.

**Step 3 — name the mechanisms.** Which of the four are present? Selection on the outcome (targets high-propensity prescribers): yes. Attribution circularity (same platform serves and measures): yes. No control: yes. Publication asymmetry (you only see the wins): yes. All four — the maximal-bias case.

**A dead end I went down.** My first move was to look for an *adjusted* version of the vendor number — surely a propensity-matched comparison would rescue it. It would help, but it would not solve the problem: matching on observed propensity cannot remove selection on the *unobserved* reasons a physician was targeted, and it does nothing about attribution circularity. The dead end taught the real lesson: *no amount of post-hoc adjustment substitutes for a control group held out before exposure.* That is why Chapter 8 exists.

**The lesson.** The evidence map's honest output is: "best available evidence is weak (vendor, unadjusted, all four bias mechanisms present); no independent estimate exists; the question is unresolved and a holdout study is required to resolve it."

**The limit.** The evidence map tells you *how much you know* (here: little, with confidence). It does not tell you the *true effect*. It can point precisely at the absence of evidence — and naming an absence precisely is itself a result a product team can act on. It cannot manufacture a number to fill the gap, and it must not.

## 6. Common Misconceptions

- **"The ad was followed by more scripts, so the ad caused more scripts."** Sequence is not causation; the targeted physicians were already prescribing more. This is the wedge into Chapter 8.
- **"A peer-reviewed number is automatically trustworthy."** Not where the funded party controls trial design, analysis, and publication (Study 329).
- **"Critical findings are stronger than industry findings."** Not automatically. The meal-and-prescribing evidence is observational; it is good evidence, not proof. Apply one standard to both sides.
- **"More precision in the lift number means more credibility."** A precisely measured association from a circular, uncontrolled design is precisely the wrong number.
- **"If there's no independent evidence, the effect must be small/fake."** Absence of evidence is not evidence of absence. The honest claim is "unknown," which is different from "zero."

## 7. Evidence Check & Compliance and Patient-Welfare Check

**Evidence check — independent vs. vendor-generated vs. observational vs. contested:**
- *Independent, strong:* detailing changes prescribing (multiple systematic reviews); academic detailing improves evidence-based prescribing (Cochrane 2007; JAMA Netw Open 2024/25, RCT-inclusive); generic bioequivalence (FDA review of >2,000 pharmacokinetic trials — branded preference is largely marketing-driven) [verify trial count].
- *Independent but observational (state the limit):* the meals/Open-Payments dose-response (DeJong et al., JAMA Intern Med 2016) — association, not proof; physicians who take meals may differ from those who do not.
- *Vendor-generated (label, never cite as evidence):* all EHR/POC script-lift figures (4–44%; 19–25%; 11.9%/11.5%). The search for independent corroboration returns vendor pages — corroborating the gap, not the claim.
- *Contaminated at source:* industry-controlled trial literature where selective reporting and outcome switching operate (Study 329; antidepressant 98%/48% publication asymmetry).
- *Open gap:* no independent causal estimate of EHR-ad lift, and no independent study of its clinical appropriateness, exists to cite. The chapter points at the absence; it does not fill it.

**Compliance and patient-welfare check:** the EHR/POC channel is where the evidence gap and the *regulatory* gap coincide. The 2025 FDA enforcement wave targeted DTC promotional content but left EHR-integrated advertising in a regulatory gray zone [verify]. That matters for patient welfare specifically because EHR ads are delivered in the same interface layer as drug-interaction and dosage alerts — they borrow the clinical authority of a safety warning while carrying a commercial message, and no independent study has checked whether the resulting prescribing changes are *clinically appropriate*. The patient-welfare gate this chapter raises and cannot close: a measured lift is not a measured benefit. Disclosure alone (the 2010 Sunshine Act) is documented to be necessary but not sufficient — it did not change physician conflict-of-interest behavior — so "it's disclosed" is not a welfare answer either.

## 8. Exercises

1. **(Analyze)** Take the opening case's five sentences. For each, state whether it is true, and if true, whether it is *evidence of causation*. Then name which of the four overstatement mechanisms (if any) each sentence reveals.
2. **(Evaluate)** Grade four claims on both axes (design strength × source independence) and assign each a min-grade: (a) the vendor 44% lift; (b) the DeJong meals study; (c) the academic-detailing JAMA Netw Open review; (d) GSK Study 329 as originally published. Defend each grade in one sentence — and explain why (b) does not get a perfect score.
3. **(Apply+ · Produce · Part B)** Write the **evidence map for your own research thread**: the claim, its dependent variable (lift or brand), the best available evidence with its two-axis grade, the bias mechanisms present, and the honest statement of what is known vs. unknown. Then select the public dataset (Open Payments, Medicare Part D, ICER, or a synthetic substitute) you will use to test it. This is the graded checkpoint.
4. **(Analyze)** Find one *independent* peer-reviewed finding that is critical of pharma marketing and one that is favorable. State the design and source-independence grade of each, and one limitation of each — proving you apply the same standard to both directions.

## 9. The Five-Part AI Block

**When to use AI here.** Use an LLM to *extract and structure* the claims in a long document — pulling every effectiveness sentence into a table and drafting the two-axis grading scaffold. It is a strong first-pass clerk.

**When NOT to use AI here.** Do not let an LLM assign the *final evidence grade* or decide whether a study's design is causal. It will fluently mis-grade — calling a vendor case study "evidence" because it contains numbers, or treating a peer-reviewed label as a guarantee. The grade is the human judgment the chapter trains. Also: LLMs hallucinate citations; never let one supply a study reference you have not opened.

**LLM exercise.** Paste the opening case (or a real vendor case study). Prompt: *"List each factual sentence. For each, state whether it is, on its own, evidence that the ad caused additional prescribing — yes or no — and why. Do not rate the program; rate each sentence's causal status."* Compare the model's verdicts to your own from Exercise 1.

**CLI exercise.** Collect three vendor case-study pages and three independent abstracts as text files. Use `grep -i -E "lift|increase|associated with|caused|n ?= ?[0-9]|p ?< ?0|randomi"` to surface, across all six at once, who uses causal language versus associational language and who reports a sample size or randomization. Tabulate which source type uses which vocabulary.

**AI validation.** For every citation the LLM produced or "confirmed" in the previous steps, open the primary source and verify (a) it exists, (b) it says what was claimed, and (c) the measuring party is independent of the selling party. Record the survival rate. Treat any unverified citation as nonexistent.

## 10. AI Use Disclosure

In drafting this chapter, an LLM helped structure the channel comparison and the two-axis taxonomy; every grade, every causal-vs-associational call, and the honesty caveat on the meals study were set against the primary sources and synthesis files and checked by hand. The judgment no AI could make: **deciding that the meals evidence, though observational, is genuinely stronger than the vendor's 44% — and saying so without applying a double standard.** That calibrated, two-directional skepticism is the human contribution. (Part B standard: name one place where you, not the AI, decided whether a claim was truly evidenced.)

## 11. What Would Change My Mind

The chapter's central claim — that EHR/POC script-lift figures are not causal evidence — would be overturned by a single *independent*, pre-registered, controlled study (randomized holdout, or a credibly identified natural experiment) that estimated the incremental effect of EHR advertising and found the vendor-range effect held up under that design, measured by a party with no commercial stake and no data dependency on the platform. One such study would move the channel from "unknown" toward "evidenced." The claim is falsifiable; today it simply has not been tested that way.

## 12. Still Puzzling

- If EHR-ad lift is real and large, why has no platform commissioned an independent randomized evaluation — is the expected finding worse than the current uncertainty?
- The meals study is observational; the cleanest causal test (randomizing meals) is unethical and impossible. What is the *strongest* identification strategy available for an effect we cannot randomize?
- Publication bias contaminates the literature, yet the literature is still our best independent source. How much should a Fellow discount a peer-reviewed effect size, and on what principled basis?

## 13. Summary

You can now state the difference between association and causation in promotional analytics, and name the four mechanisms — selection on the outcome, attribution circularity, absence of a control, and publication asymmetry — that make industry associations overstate causal effect. You can grade any claim on two axes (design strength × source independence) and take the minimum. You can rank the channels honestly: strong independent evidence for detailing, meals (observational), and academic detailing; a genuine, field-defining *absence* of independent evidence for EHR/point-of-care advertising. And you have practiced reading a document in which every sentence is true and none is causal evidence — the single most transferable skill in this book — while holding yourself to the same standard you hold the vendors to. The evidence map you build for your own thread is this week's deliverable and the foundation of everything in Act Three.

## 14. Key Terms

- **Association vs. causation:** "exposed prescribe more" (a fact about data) vs. "exposure caused more prescribing" (a fact about a counterfactual).
- **Selection on the outcome:** targeting physicians already likely to prescribe, then crediting their prescribing to the ad.
- **Attribution circularity:** the same platform serves the ad and measures the lift, with no independent firewall.
- **Counterfactual / control group:** what the same physicians would have prescribed un-exposed; the thing "lift" without a holdout cannot estimate.
- **Publication / reporting asymmetry:** wins are published, null results are not — at the vendor *and* the peer-reviewed level.
- **Evidence-quality taxonomy:** grading a claim by study-design strength and source independence, taking the minimum.
- **Outcome switching:** reporting post-hoc outcomes as if pre-specified when the pre-specified ones were null (Study 329).
- **Academic detailing:** non-commercial educational outreach in the detailing format with an evidence-based agenda; the RCT-validated counter-model.

## 15. Bridge

You can now grade a claim's evidence and name exactly what is missing. What is most often missing is a credible model and a credible control. Act Two builds the toolkit to supply both — and it starts with the baseline that usually wins: the unglamorous gradient-boosted tree ensemble that every "AI platform" and every "MoE" claim must beat.

## 16. Further Reading

- DeJong, C., et al. "Pharmaceutical Industry–Sponsored Meals and Physician Prescribing Patterns for Medicare Beneficiaries." *JAMA Internal Medicine* 2016;176(8):1114–1122. The dose-response meals finding — and a model of strong *observational* evidence whose limits you should state.
- Ritchie, S. *Science Fictions: How Fraud, Bias, Negligence, and Hype Undermine the Search for Truth* (2020). Publication bias, outcome switching, the antidepressant 98%/48% asymmetry — why the evidence base is contaminated at its source. Load-bearing for §4.4.
- Leigh, A. *Randomistas: How Radical Researchers Are Changing Our World* (2018). Why a control group is the gold standard; the cultural and practical case for RCTs. Bridges directly to Chapter 8.
- Pearl, J., & Mackenzie, D. *The Book of Why: The New Science of Cause and Effect* (2018). Intuition pumps for the central distinction — why correlation, however precise, is not causation.
- Le Noury, J., et al. "Restoring Study 329: efficacy and harms of paroxetine and imipramine in treatment of major depression in adolescence." *BMJ* 2015;351:h4320. The RIAT re-analysis behind §4.4's canonical case. [verify exact citation before use.]

---

## Prompts

*No figures have been generated for this chapter yet.*
*Run the Cowork enrichment pass to populate this section.*
