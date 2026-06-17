# Chapter 5 — The Evidence Problem
*Every sentence is true. None of it is evidence.*

A vendor case study crosses your desk. One page, well designed, claiming a **44% script lift** from an AI-driven EHR advertising program. Read it slowly.

> *"Physicians exposed to the program prescribed the brand 44% more than physicians who were not exposed."*

True. The exposed group did prescribe more. This is a measured fact about two groups.

> *"Exposure was triggered by the relevant diagnosis code in the EHR, ensuring clinical relevance."*

True. The trigger fired on the ICD-10 code. The targeting worked as described.

> *"Lift was measured at the NPI level using linked prescribing data."*

True. They linked exposure to each physician's actual prescriptions. The measurement is real.

> *"The program targeted high-potential prescribers identified by our predictive model."*

True — and fatal. The exposed physicians were *selected because they were already likely to prescribe more.* Their higher prescribing is exactly what the targeting model was built to find.

> *"Measurement and delivery run on a single unified platform for seamless attribution."*

True — and the second fatal sentence. The party that served the ad is the party that measured the lift. There is no independent firewall between the commercial interest in a high number and the production of the number.

Every sentence is accurate. The page contains no lie. And the page contains *no causal evidence whatsoever.*

Hold that. It is worth sitting with, because the feeling it produces — mild vertigo, the sense that something went wrong but you cannot quite locate where — is the right feeling. That vertigo is the beginning of scientific literacy in this field. The 44% is real as a *difference between groups.* It is unknown as an *effect of the ad,* because we never see what those same high-potential physicians would have prescribed without the exposure. We see one world. Causation requires comparing it to a world we do not have.

*(The 44% and all figures in this case are illustrative of vendor-reported ranges and are `[verify]` — they stand for the 4–44% script-lift claims that circulate in this market, none independently validated.)*

---

The core distinction is old, and simple to state. An **association** says: exposed physicians prescribed more than unexposed physicians. A **causal claim** says: the exposure *caused* the additional prescribing. The first is a fact about the data. The second is a fact about a counterfactual world — what the *same* physicians would have done un-exposed — which the data, on its own, never shows you.

This is not a philosophical objection. It is a structural one. You cannot see the counterfactual. You can only see one branch of what happened. Every method in Act Two of this book — difference-in-differences, instrumental variables, regression discontinuity, matched holdouts — is an attempt to *reconstruct* the missing branch from things you can observe. But reconstructing something is not the same as having it, and the quality of any causal estimate depends entirely on how credibly the missing branch has been reconstructed.

In pharma marketing, this gap is not symmetric. It does not randomly overstate or understate the true effect. Four mechanisms push it systematically in one direction — upward — and you should be able to name all four cold.

**First: selection on the outcome.** Platforms target high-propensity prescribers — high deciles, rising NBRx, on-label patient mix — because that is how you sell a targeting product. Those physicians were already going to prescribe more. Measuring their post-exposure prescribing and crediting the delta to the ad confounds the targeting signal with the treatment effect. The physicians' prior trajectory is doing the work; the ad is taking the credit.

**Second: attribution circularity.** The platform that serves the ad also measures the lift, using the same NPI-linked infrastructure for both. Targeting and measurement are not independent. There is no firewall between the party with a commercial interest in a high number and the party producing it. This is not a conspiracy; it is a structural conflict that no amount of good intentions resolves. The measurement architecture itself is the problem.

**Third: absence of a control.** "Lift" without a randomized or quasi-randomized holdout is a before/after or exposed/unexposed comparison, not an estimate of the counterfactual. Without a control group, there is no way to subtract what would have happened anyway. You are measuring gross change and calling it net effect.

**Fourth: publication and reporting asymmetry.** Vendor case studies report wins. The campaign that did nothing does not become a case study. The campaign that went negative becomes a quiet quarterly learning. This asymmetry is not unique to vendors — it operates in the peer-reviewed literature too, as we will see — but in the vendor context it is near-total. You are reading a curated sample of the highest outcomes.

Any single mechanism is enough to inflate a number. EHR script-lift claims typically carry all four at once.

<!-- → [DIAGRAM: Four-mechanism diagram — each mechanism as a node feeding into "Observed Lift," with arrows labeled by what each conflates with the true effect; a fifth node for "True Causal Effect" shown as disconnected or estimated only with design controls] -->

---

To grade evidence you need a ladder, and a defensible rating uses two ladders at once.

The first ranks **study-design strength** by causal credibility, from the top down: randomized controlled trial or pre-registered experiment; natural experiment with credible identification (difference-in-differences, regression discontinuity, instrumental variables); matched observational or propensity-adjusted; unadjusted exposed-versus-unexposed; vendor case study or testimonial. Each rung below the top adds uncertainty about the missing counterfactual — either because the assignment to treatment was not random, or because the comparison group is not clean, or because there is no comparison group at all.

The second ranks **source independence**: independent peer-reviewed at the top; government or nonprofit; industry-funded but peer-reviewed; vendor white paper or case study — un-refereed, commercial interest.

A claim's grade is roughly the *minimum* of its two scores. A perfectly designed study reported only in a vendor brochure is compromised by the conflict. An independent source reporting an unadjusted before/after is still weak by design. The minimum-of-two rule matters because it prevents you from being fooled by strength on one axis while missing weakness on the other.

Apply this to the opening case. The 44% claim: design strength is unadjusted exposed-versus-unexposed — low. Source independence is vendor-produced — low. Grade: **weak on both axes.** That is the chapter's punchline rendered as a grade, and the grade is not a judgment call. It follows directly from the design and the source.

<!-- → [TABLE: Evidence-quality taxonomy — rows: study design types (RCT through vendor case study), columns: source independence levels; cells show example claims from this chapter graded at the intersection; the opening case's 44% highlighted in the bottom-left corner] -->

---

Now walk the channels. The field has a habit of speaking as though all pharma marketing operates in an evidentiary vacuum. It does not, and being honest about where the evidence is strong is what gives your skepticism about EHR advertising its credibility.

**Detailing — strong independent evidence it works.** Systematic reviews consistently find that physicians who receive industry information, rep contact, or free samples increase prescribing of the paying company's drugs. The canonical *Annals of Internal Medicine* systematic review documented something particularly sharp: physicians' belief that accepting payments will not affect their prescribing is not well-founded — the data show measurable prescribing changes despite self-reported immunity. This is the third-person effect made quantitative. Everyone thinks they are the exception. The data says no one is. [verify exact author and year of the Annals review before publication]

**Meals and gifts — strong evidence, with a dose-response, and observational.** DeJong et al., *JAMA Internal Medicine*, 2016, linked CMS Open Payments to Medicare Part D prescribing for the most-prescribed branded drug in four classes. Across n = 279,669 physicians and 63,524 relevant meal payments, receipt of even a *single* industry-sponsored meal — mean value under twenty dollars — was associated with higher rates of prescribing the promoted brand, and the rate rose with the number and value of meals. A dose-response relationship. [Verified: JAMA Intern Med 2016;176(8):1114–1122; PubMed 27322350.]

Here is the honesty this chapter requires: **this is observational, association evidence.** Physicians who accept meals may differ systematically from those who do not — in specialty, patient mix, baseline prescribing patterns. The study cannot rule that out. The dose-response relationship and the single-meal threshold strengthen the causal interpretation; they do not prove it. If you would demand a control group from the vendor's 44%, intellectual honesty demands you note the same limit here. The meal finding is *better* evidence than the vendor case study — larger N, independent source, peer-reviewed, dose-response — but it is not proof, and this book does not pretend it is.

A chapter that applies one standard to claims it dislikes and another to claims it likes has no standard at all.

**Academic detailing — strong RCT evidence it works.** The format is identical to pharma detailing — a trained professional visiting a physician in their practice to discuss prescribing. The funder and the agenda are opposite. A systematic review in *JAMA Network Open* examined 118 randomized and non-randomized studies; among the 36 lowest-risk-of-bias studies, 69% showed significant improvement in at least one prescribing behavior, with a median absolute change of 4.0% in the intended direction. The older 2007 Cochrane meta-analysis found a median absolute change of about 5.6% across 69 RCTs. [verify exact authors, year of the JAMA Netw Open review and the Cochrane figure before publication]

The pedagogical point is clean: same channel, opposite funder incentive, rigorous evidence. The channel is a vehicle. The agenda is the variable. Academic detailing is also chronically underfunded relative to commercial detailing — the VA program is the main scaled example — which is a policy observation, not an evidence question.

**EHR and point-of-care advertising — the evidence gap.** The fastest-growing channel with the thinnest independent evidence. Vendor-reported script lifts span 4–44% depending on therapy and channel. OptimizeRx reports 19–25% from NPI-level analysis; one vendor breakdown cites roughly 11.9% from informational messages across eight programs and 11.5% from brand-plus-savings-offer combinations across 27 programs. [All figures vendor-sourced, un-refereed, `[verify]`.]

When you search for *independent, peer-reviewed* evidence on this channel, you find almost exclusively vendor marketing pages. That is itself the finding. No independent, peer-reviewed study validates the causal attribution behind these numbers. No peer-reviewed study has assessed whether EHR-embedded ads produce clinically appropriate versus inappropriate prescribing. This is the single largest open validation gap in the field, and it is where the gap in the evidence and the gap in the regulation coincide.

<!-- → [CHART: Channel evidence strength matrix — x-axis: source independence (low to high), y-axis: study-design strength (low to high); channels plotted as labeled points: detailing (high/high), academic detailing (high/high), meals/DeJong (medium-high/medium), EHR/POC (low/low); quadrant labels explain what each position means for actionability] -->

---

You might hope to escape vendor circularity by retreating to the peer-reviewed literature. Partly you can. But the literature is not clean where industry controls trial design, analysis, and publication.

The canonical case is **GSK Study 329** — paroxetine in adolescents with depression. The published report claimed the drug was "generally effective." The conclusion came from post-hoc outcome switching: the pre-specified primary outcomes were negative, and the positive conclusion was assembled afterward from secondary measures selected after the data were in hand. The drug was ineffective and carried suicidality risk in the studied population. The paper stood uncorrected for years, and prescribing continued. A 2015 RIAT re-analysis in the *BMJ* restored the original data and reversed the conclusion. [Le Noury et al., BMJ 2015;351:h4320 — verify citation before use.]

The pattern generalizes. In the antidepressant literature, an estimated 98% of positive trials were published versus 48% of negative ones. Correcting for publication bias plus outcome switching collapsed an apparent two-to-one efficacy signal — the drugs still work, but perhaps half as well as the unadjusted literature suggested. And only about 31% of medical meta-analyses even check for publication bias. [verify the 31% figure — attributed to Ritchie, *Science Fictions*, 2020]

The lesson: the problem is not only the vendor case study. The evidence base is contaminated at its source wherever the funded party controls the pipeline. Skepticism is not anti-industry. It is the price of admission to *any* claim, including the ones that appear in journals.

---

Here is how the grading works in practice.

A brand team asks: "Is our EHR co-pay-message program worth expanding?" Build the evidence map.

**Step one — name the dependent variable.** Is this a lift claim (incremental scripts) or a brand claim (durable association)? The program's stated goal is more scripts: it is a lift claim, which means it requires a control group. You cannot grade evidence until you know which variable the claim asserts to move.

**Step two — find the best available evidence and grade it on both axes.** The vendor supplies a 19% NPI-level lift figure. Design strength: unadjusted exposed-versus-unexposed. Source independence: vendor-produced. Grade: minimum of low and low — **weak.** There is no independent peer-reviewed estimate to set beside it.

**Step three — name the mechanisms present.** Selection on the outcome: yes, the platform targets high-propensity prescribers. Attribution circularity: yes, the same platform serves and measures. Absence of a control: yes. Publication asymmetry: yes, you are seeing a reported win. All four. The maximal-bias case.

A dead end worth naming. My first instinct was to look for an adjusted version of the vendor number — surely a propensity-matched comparison would rescue it. It would help at the margins. It would not solve the problem. Matching on observed propensity cannot remove selection on the *unobserved* reasons a physician was targeted, and it does nothing about attribution circularity. No amount of post-hoc adjustment substitutes for a control group held out before exposure begins. That is why the holdout exists as a design, not as a post-processing step.

The evidence map's honest output: best available evidence is weak — vendor-generated, unadjusted, all four bias mechanisms present, no independent estimate in existence. The question is unresolved. A holdout study is required to resolve it.

The limit to name: the evidence map tells you how much you know — here, little, with confidence. It does not tell you the true effect. Naming an absence precisely is itself a result a team can act on. It cannot manufacture a number to fill the gap, and it must not.

<!-- → [INFOGRAPHIC: Step-by-step evidence-map construction for the EHR co-pay example — boxes for: (1) name the dependent variable, (2) locate best evidence, (3) grade on two axes, (4) identify mechanisms, (5) state what is known vs. unknown; arrows connecting steps; final output box reads "WEAK — holdout required"] -->

---

The EHR channel sits at the intersection of two gaps — evidence and regulation — and it is worth being precise about what that means for patients.

EHR ads are delivered in the same interface layer as drug-interaction warnings and dosage alerts. They borrow the visual authority of a clinical safety notice while carrying a commercial message. No independent study has examined whether the prescribing changes EHR ads produce are clinically appropriate. A measured lift is not a measured benefit. It is a measured change in physician behavior, and the direction of that change — toward better or worse patient care — is simply unknown.

Disclosure alone has not closed the gap. The 2010 Sunshine Act, which required public reporting of industry payments to physicians, is documented as necessary but not sufficient: disclosure did not substantially change physician conflict-of-interest behavior. "It's disclosed" is not a patient-welfare answer. It is a transparency answer to a different question.

---

**Five-Part AI Exercise Block**

**When to use AI here.** Use an LLM to *extract and structure* the claims in a long document — pulling every effectiveness sentence into a table and drafting the two-axis grading scaffold. It is a strong first-pass clerk for organizing what needs to be graded.

**When NOT to use AI here.** Do not let an LLM assign the final evidence grade or decide whether a study's design is causal. It will fluently mis-grade — calling a vendor case study "evidence" because it contains numbers, or treating a peer-reviewed label as a quality guarantee. The grade is the human judgment this chapter trains. Also: LLMs hallucinate citations. Never let one supply a study reference you have not opened.

**LLM exercise (copy-paste prompt):**
> "Here is a vendor case study: [PASTE TEXT]. List each factual sentence. For each, state whether it is, on its own, evidence that the ad caused additional prescribing — yes or no — and why. Do not rate the program overall; rate each sentence's causal status."

Compare the model's verdicts to your own from the exercises below. Note where it agreed, where it over-credited the vendor, and where it correctly flagged the mechanisms.

**CLI exercise.** Collect three vendor case-study pages and three independent peer-reviewed abstracts as plain-text files. Run:

```bash
grep -i -E "lift|increase|associated with|caused|n ?= ?[0-9]|p ?< ?0|randomi" *.txt
```

Tabulate, across all six files, which source type uses causal language versus associational language, and which reports a sample size or randomization. The vocabulary gap between vendor documents and peer-reviewed abstracts is itself a data point.

**AI validation.** For every citation the LLM produced or "confirmed" in the previous steps, open the primary source and verify: (a) it exists, (b) it says what was claimed, (c) the measuring party is independent of the selling party. Record the survival rate. Treat any unverified citation as nonexistent for the purposes of your evidence map.

**AI Use Disclosure**

*Write two sentences naming what an AI tool did in your work for this chapter and the one judgment it could not make. For example: "I used an LLM to extract and table every effectiveness claim in the vendor materials; I decided myself, against the primary literature, whether the DeJong meals study was genuinely stronger evidence than the vendor's 44% — because the AI could not hold both directions of skepticism simultaneously without defaulting to whichever it saw last."*

---

**What Would Change My Mind**

The chapter's central claim — that EHR/POC script-lift figures are not causal evidence — would be overturned by a single independent, pre-registered, controlled study that estimated the incremental effect of EHR advertising and found the vendor-range effect held up under that design, measured by a party with no commercial stake and no data dependency on the platform. One such study would move the channel from "unknown" toward "evidenced." The claim is falsifiable. Today it simply has not been tested that way.

Separately, if a large-scale audit of propensity-matched versus holdout-measured lift figures showed the two converged within a few percentage points, it would weaken the case against post-hoc matching as a substitute for experimental control. That audit does not yet exist either.

**Still Puzzling**

- If EHR-ad lift is real and large, why has no platform commissioned an independent randomized evaluation? Is the expected finding worse than the current uncertainty — and if so, what does that tell us about who the measurement is for?
- The meals study is observational; the cleanest causal test — randomizing meals — is unethical and impossible. What is the strongest identification strategy available for an effect we cannot randomize?
- Publication bias contaminates the literature, yet the literature is still the best independent source we have. How much should a Fellow discount a peer-reviewed effect size, and on what principled basis?

---

## Exercises

**Warm-up**

1. *(Factual recall — the four mechanisms)* Name the four mechanisms that make promotional associations systematically overstate causal effect. For each, write one sentence explaining what it conflates with the true treatment effect.
   *What this tests: whether you can reproduce the core taxonomy without the text in front of you.*

2. *(Factual recall — the two-axis taxonomy)* Describe the two axes of the evidence-quality taxonomy and explain why the final grade is the minimum of the two scores rather than the average.
   *What this tests: the logic of the grading system, not just its labels.*

3. *(Factual recall — channel evidence)* Rank the four channels covered in this chapter (detailing, meals, academic detailing, EHR/POC advertising) by overall evidence strength. For the highest-ranked, name the design strength and source independence. For the lowest-ranked, name the specific absence that defines the gap.
   *What this tests: retention of the channel-by-channel review and the distinction between weak evidence and absent evidence.*

**Application**

4. *(Apply — grade a claim)* Grade the following four claims on both axes and assign each a min-grade: (a) the vendor 44% lift; (b) the DeJong meals study; (c) the academic-detailing JAMA Network Open review; (d) GSK Study 329 as originally published. Defend each grade in one sentence — and explain why (b) does not receive a perfect score.
   *What this tests: applying the taxonomy in four different directions, including to evidence that is critical of industry.*

5. *(Apply — opening case)* Return to the five sentences of the opening case. For each: state whether it is true, and if true, whether it is evidence of causation. Then name which of the four mechanisms (if any) each sentence reveals.
   *What this tests: the fine-grained skill of separating factual accuracy from causal status — sentence by sentence.*

6. *(Apply — a new claim)* A colleague tells you: "Our rep detailing program must be working — prescribing went up 15% in every territory where we increased call frequency this quarter." Identify the design, the source, the grade on both axes, the mechanism(s) most likely inflating the number, and one piece of additional data that would move the grade upward.
   *What this tests: applying the framework to a claim that is not from a vendor deck — transferring the skill to a new context.*

**Synthesis**

7. *(Synthesize — double standard)* Find one independent peer-reviewed finding that is critical of pharma marketing and one that is favorable to it. State the design and source-independence grade of each, and one limitation of each. The goal is to demonstrate that you apply the same standard in both directions.
   *What this tests: intellectual consistency — whether your skepticism is principled or directional.*

8. *(Synthesize — evidence map for your own thread)* Write the evidence map for your research thread from Chapter 2: the claim, its dependent variable, the best available evidence with its two-axis grade, the bias mechanisms present, and an honest statement of what is known versus unknown. Then name the public dataset you will use to test it.
   *What this tests: integration across Chapter 2 (dependent variable) and Chapter 5 (evidence standard) — the graded checkpoint for this unit.*

**Challenge**

9. *(Open-ended — study design)* The chapter flags the SOMi → SOMa claim and the EHR-ad lift claim as unvalidated on independent data. Choose one. Sketch, in one paragraph, an identification strategy that would provide credible causal evidence — name the design, the data required, the hardest methodological obstacle, and what finding would falsify the claim.
   *What this tests: converting a flagged hypothesis into a tractable research design and identifying its empirical breaking point.*
