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

![Diagram of four bias mechanisms — selection on the outcome, attribution circularity, absence of a control, and publication asymmetry — each feeding arrows into an "Observed Lift" box, with the "True Causal Effect" box sitting apart, reachable only through design controls.](../images/05-the-evidence-problem-fig-01.png)
*Figure 5.1 — Four mechanisms inflate observed lift away from the true causal effect*

<!-- → [DIAGRAM: Four-mechanism diagram — each mechanism as a node feeding into "Observed Lift," with arrows labeled by what each conflates with the true effect; a fifth node for "True Causal Effect" shown as disconnected or estimated only with design controls] -->

---

To grade evidence you need a ladder, and a defensible rating uses two ladders at once.

The first ranks **study-design strength** by causal credibility, from the top down: randomized controlled trial or pre-registered experiment; natural experiment with credible identification (difference-in-differences, regression discontinuity, instrumental variables); matched observational or propensity-adjusted; unadjusted exposed-versus-unexposed; vendor case study or testimonial. Each rung below the top adds uncertainty about the missing counterfactual — either because the assignment to treatment was not random, or because the comparison group is not clean, or because there is no comparison group at all.

The second ranks **source independence**: independent peer-reviewed at the top; government or nonprofit; industry-funded but peer-reviewed; vendor white paper or case study — un-refereed, commercial interest.

A claim's grade is roughly the *minimum* of its two scores. A perfectly designed study reported only in a vendor brochure is compromised by the conflict. An independent source reporting an unadjusted before/after is still weak by design. The minimum-of-two rule matters because it prevents you from being fooled by strength on one axis while missing weakness on the other.

Apply this to the opening case. The 44% claim: design strength is unadjusted exposed-versus-unexposed — low. Source independence is vendor-produced — low. Grade: **weak on both axes.** That is the chapter's punchline rendered as a grade, and the grade is not a judgment call. It follows directly from the design and the source.

| Study design ↓ \ Source independence → | Independent peer-reviewed | Government / nonprofit | Industry-funded, peer-reviewed | Vendor white paper / case study |
|---|---|---|---|---|
| RCT / pre-registered experiment | Academic-detailing RCTs (JAMA Netw Open; Cochrane) — **strongest** | VA academic-detailing program | (rare) | (none in EHR channel) |
| Natural experiment / quasi-random | — | — | — | — |
| Matched / propensity-adjusted | — | — | Some adjusted vendor analyses | Propensity-matched vendor analysis — still no holdout |
| Unadjusted exposed-vs-unexposed | Detailing systematic reviews (association) | — | — | Opening case 19% NPI-level lift |
| Vendor case study / testimonial | — | — | — | **Opening case 44% script lift `[verify]` — weak on both axes** |
| Observational, dose-response | DeJong meals study (JAMA Intern Med 2016) — strong but observational | — | — | — |

*Table 5.1 — Evidence-quality taxonomy. A claim's grade is the minimum of its two axes. The opening case's 44% script lift sits in the weakest corner — un-refereed vendor source crossed with an unadjusted design. The 4–44% vendor script-lift range is `[verify]` and none of it is independently validated. The academic-detailing RCTs are the only top-row independent evidence; the DeJong dose-response is strong but remains association, not proof.*

---

Now walk the channels. The field has a habit of speaking as though all pharma marketing operates in an evidentiary vacuum. It does not, and being honest about where the evidence is strong is what gives your skepticism about EHR advertising its credibility.

**Detailing — strong independent evidence it works.** Systematic reviews consistently find that physicians who receive industry information, rep contact, or free samples increase prescribing of the paying company's drugs. A 2021 systematic review in *Annals of Internal Medicine* (Mitchell et al., *Ann Intern Med* 2021;174(3):353–361; M20-5665) found that of 36 included studies, 30 reported a positive association between industry payments and prescribing in all analyses; the earlier canonical review (Wazana, *JAMA* 2000) reached a similar conclusion across 29 studies. The sharp point documented across this literature: physicians' belief that accepting payments will not affect their prescribing is not well-founded — the data show measurable prescribing changes despite self-reported immunity. This is the third-person effect made quantitative. Everyone thinks they are the exception. The data says no one is.

**Meals and gifts — strong evidence, with a dose-response, and observational.** DeJong et al., *JAMA Internal Medicine*, 2016, linked CMS Open Payments to Medicare Part D prescribing for the most-prescribed branded drug in four classes. Across n = 279,669 physicians and 63,524 relevant meal payments, receipt of even a *single* industry-sponsored meal — mean value under twenty dollars — was associated with higher rates of prescribing the promoted brand, and the rate rose with the number and value of meals. A dose-response relationship. [Verified: JAMA Intern Med 2016;176(8):1114–1122; PubMed 27322350.]

Here is the honesty this chapter requires: **this is observational, association evidence.** Physicians who accept meals may differ systematically from those who do not — in specialty, patient mix, baseline prescribing patterns. The study cannot rule that out. The dose-response relationship and the single-meal threshold strengthen the causal interpretation; they do not prove it. If you would demand a control group from the vendor's 44%, intellectual honesty demands you note the same limit here. The meal finding is *better* evidence than the vendor case study — larger N, independent source, peer-reviewed, dose-response — but it is not proof, and this book does not pretend it is.

A chapter that applies one standard to claims it dislikes and another to claims it likes has no standard at all.

**Academic detailing — strong RCT evidence it works.** The format is identical to pharma detailing — a trained professional visiting a physician in their practice to discuss prescribing. The funder and the agenda are opposite. A 2025 systematic review in *JAMA Network Open* (Rome et al.) examined 118 randomized and non-randomized studies; among the 36 lowest-risk-of-bias studies, 25 (69%) showed significant improvement in at least one prescribing behavior, with a median change of 4.0% in the intended direction. The older Cochrane review of educational outreach visits (O'Brien et al., *Cochrane Database Syst Rev* 2007, Issue 4, CD000409; 69 studies) found a median adjusted risk difference of about 5.6% in compliance with desired practice (4.8% for prescribing specifically).

The pedagogical point is clean: same channel, opposite funder incentive, rigorous evidence. The channel is a vehicle. The agenda is the variable. Academic detailing is also chronically underfunded relative to commercial detailing — the VA program is the main scaled example — which is a policy observation, not an evidence question.

**EHR and point-of-care advertising — the evidence gap.** The fastest-growing channel with the thinnest independent evidence. Vendor-reported script lifts span 4–44% depending on therapy and channel. OptimizeRx reports 19–25% from NPI-level analysis; one vendor breakdown cites roughly 11.9% from informational messages across eight programs and 11.5% from brand-plus-savings-offer combinations across 27 programs. [All figures vendor-sourced, un-refereed, `[verify]`.]

When you search for *independent, peer-reviewed* evidence on this channel, you find almost exclusively vendor marketing pages. That is itself the finding. No independent, peer-reviewed study validates the causal attribution behind these numbers. No peer-reviewed study has assessed whether EHR-embedded ads produce clinically appropriate versus inappropriate prescribing. This is the single largest open validation gap in the field, and it is where the gap in the evidence and the gap in the regulation coincide.

![Scatter matrix with source independence on the x-axis and study-design strength on the y-axis. Detailing and academic detailing sit high/high, the DeJong meals study medium-high/medium, and EHR/point-of-care advertising low/low; quadrant labels explain what each position means for actionability.](../images/05-the-evidence-problem-fig-02.png)
*Figure 5.2 — Channel evidence-strength matrix (vendor EHR figures `[verify]`, plotted as weak)*

<!-- → [CHART: Channel evidence strength matrix — x-axis: source independence (low to high), y-axis: study-design strength (low to high); channels plotted as labeled points: detailing (high/high), academic detailing (high/high), meals/DeJong (medium-high/medium), EHR/POC (low/low); quadrant labels explain what each position means for actionability] -->

---

You might hope to escape vendor circularity by retreating to the peer-reviewed literature. Partly you can. But the literature is not clean where industry controls trial design, analysis, and publication.

The canonical case is **GSK Study 329** — paroxetine in adolescents with depression. The published report claimed the drug was "generally effective." The conclusion came from post-hoc outcome switching: the pre-specified primary outcomes were negative, and the positive conclusion was assembled afterward from secondary measures selected after the data were in hand. The drug was ineffective and carried suicidality risk in the studied population. The paper stood uncorrected for years, and prescribing continued. A 2015 RIAT (Restoring Invisible and Abandoned Trials) re-analysis in the *BMJ* restored the original data and reversed the conclusion, finding neither paroxetine nor high-dose imipramine more effective than placebo and documenting clinically significant harms (Le Noury et al., *BMJ* 2015;351:h4320).

The pattern generalizes. Turner and colleagues, comparing FDA-registered antidepressant trials with the published literature, found that nearly all FDA-positive trials were published (37 of 38), while FDA-negative or -questionable trials were largely either left unpublished or published in a way that conveyed a positive outcome (of 36 such trials, only 3 were published as not-positive); correcting for this selective publication shrank the apparent effect size by roughly a third (Turner et al., *NEJM* 2008;358:252–260). The drugs still work — but less well than the unadjusted literature implied. Publication-bias checking in meta-analyses is also far from universal. [verify — unconfirmed: a specific "~31% of medical meta-analyses check for publication bias" figure (attributed to Ritchie, *Science Fictions*, 2020) did not resolve to a primary source.]

<!-- FACT-CHECK FLAG: UNVERIFIED — see factchecks/05-the-evidence-problem-assertions.md -->

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

![Five-step flowchart building the evidence map for the EHR co-pay example: name the dependent variable, locate best evidence, grade on two axes, identify bias mechanisms, state known versus unknown — arrows connect the steps to a final output box reading "WEAK — holdout required."](../images/05-the-evidence-problem-fig-03.png)
*Figure 5.3 — Evidence-map construction for the EHR co-pay program (output: weak, holdout required)*

<!-- → [INFOGRAPHIC: Step-by-step evidence-map construction for the EHR co-pay example — boxes for: (1) name the dependent variable, (2) locate best evidence, (3) grade on two axes, (4) identify mechanisms, (5) state what is known vs. unknown; arrows connecting steps; final output box reads "WEAK — holdout required"] -->

---

The EHR channel sits at the intersection of two gaps — evidence and regulation — and it is worth being precise about what that means for patients.

EHR ads are delivered in the same interface layer as drug-interaction warnings and dosage alerts. They borrow the visual authority of a clinical safety notice while carrying a commercial message. No independent study has examined whether the prescribing changes EHR ads produce are clinically appropriate. A measured lift is not a measured benefit. It is a measured change in physician behavior, and the direction of that change — toward better or worse patient care — is simply unknown.

Disclosure alone has not closed the gap. The 2010 Sunshine Act, which required public reporting of industry payments to physicians, is documented as necessary but not sufficient: disclosure did not substantially change physician conflict-of-interest behavior. "It's disclosed" is not a patient-welfare answer. It is a transparency answer to a different question.

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

---

## Prompts

### Figure 5.1 — Four mechanisms inflate observed lift away from the true causal effect

Build a single self-contained HTML file using D3 7.9.0 from the cdnjs CDN. Render a left-to-right node-link diagram: four source nodes (selection on the outcome, attribution circularity, absence of a control, publication asymmetry) on the left, each with a labeled arrow flowing into a central "Observed Lift" box. Place a separate "True Causal Effect" node, visually disconnected, reachable only via a dashed "requires design controls" edge. Use ink for structure and red only for the inflation arrows into Observed Lift. Each arrow label states what the mechanism conflates with the true effect. No axes; this is a concept diagram. Interactive: hovering a mechanism node shows a one-line tooltip of what it conflates. Deliverable: one HTML file, inline CSS, CSS-variable theming with light/dark media query, D3 7.9.0 only.

### Figure 5.2 — Channel evidence-strength matrix

Build a single self-contained HTML file using D3 7.9.0 from the cdnjs CDN. Render a 2-D scatter: x-axis source independence (low to high), y-axis study-design strength (low to high), both as ordinal-to-continuous scales. Plot four labeled points: detailing (high/high), academic detailing (high/high, offset to avoid overlap), DeJong meals (medium-high/medium), EHR/point-of-care (low/low). Draw faint quadrant dividers with corner labels explaining actionability. Color points in ink; mark EHR/POC in red as the weak outlier. Caption notes the vendor EHR figures are `[verify]` and plotted as weak, never as fact. Interactive: hovering a point shows channel, both grades, and the key caveat. Deliverable: one HTML file, inline CSS, CSS-variable theming with light/dark media query, D3 7.9.0 only.

### Figure 5.3 — Evidence-map construction for the EHR co-pay program

Build a single self-contained HTML file using D3 7.9.0 from the cdnjs CDN. Render a vertical five-step flowchart: (1) name the dependent variable, (2) locate best evidence, (3) grade on two axes, (4) identify bias mechanisms, (5) state known vs. unknown — each a box with a short result line, arrows connecting top to bottom. Terminate in a red-outlined output box reading "WEAK — holdout required." Use ink for boxes, red only for the final verdict box. Arrowheads on every connector; no label on an arrow centerline. Interactive: clicking a step expands its result detail. Deliverable: one HTML file, inline CSS, CSS-variable theming with light/dark media query, D3 7.9.0 only.

---

## Chapter 5 Exercises: The Evidence Problem

**Project:** One Drug, End to End
**This chapter adds:** Grade the evidence behind your drug's promotional claims using the two-axis evidence taxonomy — producing an honest map of what is known, what is merely asserted, and what gap a holdout would fill.

### Exercise 1 — When to Use AI

**The judgment:** Three chapter tasks where AI assistance is appropriate.

- *Extracting every effectiveness sentence from your drug's vendor materials into a table.* **Why AI works here:** reformatting — pulling claims into a grid, the clerk work before grading.
- *Drafting the two-axis grading scaffold* (design strength × source independence) for each claim. **Why AI works here:** drafting — laying out the structure you then fill with your own grades.
- *Listing which of the four bias mechanisms could apply to each claim.* **Why AI works here:** pattern-spotting — surfacing candidate mechanisms (selection-on-outcome, attribution circularity, no control, publication asymmetry) for you to confirm.

**The tell:** You are using AI appropriately when you can independently evaluate the output — when the final grade remains yours to assign.

### Exercise 2 — When NOT to Use AI

**The judgment:** Three tasks here that require human judgment.

- *Assigning the final evidence grade to a claim.* **Why AI fails here:** calibration gap — the model will call a vendor case study "evidence" because it has numbers, and treat a peer-reviewed label as a quality guarantee.
- *Deciding whether a study's design is genuinely causal for your drug's claim.* **Why AI fails here:** causal-identification problem — distinguishing a counterfactual reconstruction from an exposed/unexposed difference is the exact judgment the chapter trains.
- *Supplying a citation for a study you have not opened.* **Why AI fails here:** hallucination risk — models fabricate plausible references; an unverified citation must be treated as nonexistent.

**The tell:** You've crossed the line when AI output is your *reason* for a conclusion rather than a tool for reaching one.
**Series connection:** This trains **T5 Causal** judgment — refusing to let a measured difference between groups masquerade as a measured effect of the intervention.

### Exercise 3 — LLM Exercise

**What you're building this chapter:** An evidence map for your drug — every promotional claim graded on both axes, with the bias mechanisms named and an honest statement of what is known versus unknown.
**Tool:** Claude. Recommend a **Claude Project** — it can hold the drug identity and your Chapter 4 audited inventory so the evidence map grades the same claims you already inventoried.

**The Prompt:**

```
We are continuing a teaching case study for a branded SGLT2 inhibitor (type 2
diabetes; class has branded competitors and a generic substitute). From Chapter
4 we have an audited inventory of the AI-stack tools and their claims for this
drug.

Build an evidence map for this drug's promotional claims, using the two-ladder
taxonomy. Use only the claim text I give or describe; invent NO study, NO number,
NO citation. If you reference any study, mark it "[verify — open before citing]"
and never present an unopened citation as confirmed.

For each promotional/effectiveness claim about this drug:

1. NAME THE DEPENDENT VARIABLE: is it a LIFT claim (incremental scripts, needs a
   control) or a BRAND claim (durable association, needs longitudinal design)?
2. GRADE ON TWO AXES:
   - design strength (RCT/pre-registered > natural experiment > matched/
     propensity-adjusted > unadjusted exposed-vs-unexposed > vendor case study)
   - source independence (independent peer-reviewed > gov/nonprofit > industry-
     funded peer-reviewed > vendor white paper)
   Then give the MINIMUM-of-two grade.
3. NAME THE BIAS MECHANISMS PRESENT: selection on the outcome, attribution
   circularity, absence of a control, publication asymmetry.
4. STATE KNOWN vs UNKNOWN: one honest sentence on what this claim establishes and
   what it does not.

Do NOT assign a final overall "good/bad" verdict to the drug's marketing — only
grade each claim. Output a markdown table plus, at the end, the single claim most
in need of an independent holdout and one sentence on what that holdout would
compare.
```

**What this produces:** A per-claim evidence map for your drug with two-axis grades, mechanisms, and a holdout recommendation.
**How to adapt this prompt:** *For your own drug:* swap the drug/class line and feed your Chapter 4 claim list; keep the two ladders verbatim. *For ChatGPT/Gemini:* paste in one message; re-state the "no fabricated citations, mark [verify]" rule prominently. *For a Claude Project:* keep the drug identity, the two ladders, and the no-fabrication rule in Project instructions; send only the per-claim task.
**Connection to previous chapters:** Grades the exact claims inventoried in Chapter 4; uses the lift-vs-brand dependent-variable call from Chapter 2. **Preview of next chapter:** This evidence map and the prior chapters' artifacts become the integrated case study and partner handoff the rest of the book assembles.

### Exercise 4 — CLI Exercise

**What you're building this chapter:** A reproducible vocabulary comparison — does your drug's vendor text use causal language while peer-reviewed abstracts use associational language? · **Tool:** Claude Code (grep across mixed source types). · **Skill level:** Beginner/Intermediate.

**Setup:**
1. Save three vendor case-study pages and three independent peer-reviewed abstracts (relevant to your drug or its channel) as plain-text files in `one-drug/evidence/`.
2. Claude Code installed.
3. Add a CLAUDE.md rule: "Tabulate language use per source type; never treat causal vocabulary as proof of causation."

**The Task:**

```
In one-drug/evidence/, with the three vendor files and three peer-reviewed
abstract files, do only this:

1. Run:
   grep -i -E "lift|increase|associated with|caused|n ?= ?[0-9]|p ?< ?0|randomi" *.txt
2. Tabulate, per file and per source type (vendor vs. peer-reviewed): does it use
   CAUSAL language (lift, caused), ASSOCIATIONAL language (associated with), and
   does it report a sample size or randomization?
3. Write ch05-language-gap.md with the table, the grep command, and a one-line
   finding on the vocabulary gap between vendor and peer-reviewed sources for my
   drug's channel.

Do not edit the source files. Verification: list which files matched "randomi" or
"n =" so I can confirm the rigor markers are real, not coincidental. Note clearly
that causal VOCABULARY is not causal EVIDENCE. Stop after writing the markdown.
```

**Expected output:** `ch05-language-gap.md` with the per-source-type language table, the command, the matched rigor markers, and the vocabulary-gap finding.
**What to inspect:** Whether vendor files cluster on causal words with no sample size, while abstracts carry "n =" / "randomi" — and that the not-evidence caveat is present.
**If it goes wrong:** Most likely failure is the model concluding the vendor claims are "weaker science" purely from word frequency, smuggling in a grade the grep cannot support. Recovery: have it report only the counts and the explicit caveat that vocabulary ≠ evidence — the grading is your job, not the regex's.
**CLAUDE.md / AGENTS.md note:** Add "Word-frequency results describe language, not evidence quality; never infer a grade from them."

### Exercise 5 — AI Validation Exercise

**What you're validating:** The evidence map from Exercise 3 — the grades, mechanisms, and especially any citations. · **Validation type:** Factual + Reasoning. · **Risk level:** High — a hallucinated citation or a mis-graded claim would corrupt the partner handoff this map feeds.

**Setup:** Use your Exercise 3 output as the artifact. (If the chapter's lesson needs a specific failure, also hand the model a deliberately over-graded vendor claim and check it catches the inflation.)

**The Validation Task:**

```
Validation Checklist — Chapter 5 (Evidence Map)

Mark each Pass / Fail / Cannot-determine with one line of evidence:

- Correctness: Is each claim's dependent variable (lift vs. brand) correct, and
  does each grade equal the MINIMUM of its two axes (not the average)?
- Completeness: Does every claim have both axis grades, the min-grade, the
  mechanisms present, and a known-vs-unknown line?
- Scope: Did it grade per-claim only, without issuing an overall good/bad verdict
  on the drug's marketing?
- Chapter-specific 1: Is any vendor case study correctly graded WEAK on both axes
  (not credited as "evidence" for having numbers)?
- Chapter-specific 2: Are all four bias mechanisms checked for each lift claim
  where they apply?
- Failure-mode check (fluent-but-wrong + hallucinated citation): Open every cited
  study. Does it exist, say what was claimed, and is the measuring party
  independent of the selling party? Treat any unverifiable citation as
  nonexistent and mark the row Fail.
```

**What to do with your findings:** Pass → use the map in your handoff. One fail → revise that row and re-run. Multiple fails, or any hallucinated citation → grade the claims yourself against the two ladders; this is a "When NOT to Use AI" moment, because the grade and the citation check are the chapter's irreducible human work.
**AI Use Disclosure prompt (mandatory):** Two sentences — what the AI produced (e.g., "extracted and tabled the claims and drafted the grading scaffold") and how you used it, plus one thing it couldn't determine (e.g., "whether the DeJong meals study is genuinely stronger evidence than the vendor's lift figure, which I judged myself, and which citations were real, which I verified by opening each").
**Series connection:** Trains detection of **hallucinated citation** and **fluent-but-wrong grading** under **T5 Causal** judgment — the discipline of treating an unopened source as nonexistent and an exposed/unexposed difference as not-yet-an-effect.

## References (fact-check pass)

1. Mitchell AP, Trivedi NU, Gennarelli RL, et al. Are Financial Payments From the Pharmaceutical Industry Associated With Physician Prescribing? A Systematic Review. Ann Intern Med. 2021;174(3):353–361. https://www.acpjournals.org/doi/10.7326/M20-5665
2. Wazana A. Physicians and the pharmaceutical industry: is a gift ever just a gift? JAMA. 2000;283(3):373–380.
3. DeJong C, Aguilar T, Tseng C, Lin GA, Boscardin WJ, Dudley RA. Pharmaceutical Industry–Sponsored Meals and Physician Prescribing Patterns for Medicare Beneficiaries. JAMA Intern Med. 2016;176(8):1114–1122. https://pubmed.ncbi.nlm.nih.gov/27322350/
4. Rome BN, et al. Academic Detailing Interventions and Evidence-Based Prescribing: A Systematic Review. JAMA Netw Open. 2025;8(1). https://www.ncbi.nlm.nih.gov/pmc/articles/PMC12543401/
5. O'Brien MA, Rogers S, Jamtvedt G, et al. Educational outreach visits: effects on professional practice and health care outcomes. Cochrane Database Syst Rev. 2007;(4):CD000409.
6. Le Noury J, Nardo JM, Healy D, et al. Restoring Study 329: efficacy and harms of paroxetine and imipramine in treatment of major depression in adolescence. BMJ. 2015;351:h4320. https://www.bmj.com/content/351/bmj.h4320
7. Turner EH, Matthews AM, Linardatos E, Tell RA, Rosenthal R. Selective Publication of Antidepressant Trials and Its Influence on Apparent Efficacy. N Engl J Med. 2008;358:252–260. https://www.nejm.org/doi/full/10.1056/NEJMsa065779
