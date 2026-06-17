# Chapter 10 — LLMs for Commercial Research and Content Intelligence
*Fluency is not accuracy. Treating the gap seriously is the whole skill.*

A Fellow is asked to assemble a one-page evidence summary on whether point-of-care digital messaging lifts new patient starts. They prompt a capable LLM: *"Summarize the peer-reviewed evidence that EHR-embedded promotional messaging increases new prescriptions, with citations."* Ninety seconds later they have four clean paragraphs, five citations with author names, journals, years, and DOIs. It reads like a literature review a postdoc would be proud of.

Two of the five citations do not exist. A third is a real paper — correct authors, correct journal, resolving DOI — but it studied medication adherence reminders sent to patients, not promotional messaging to physicians, and its finding was null.

That third citation is the one that matters most. A reviewer who spot-checks will click the link, see a real paper, see a real journal, and move on. The fabrications are easy to catch once you look. The real-but-wrong citation survives looking. It only fails when you read it.

This is the failure mode the chapter is built around. The Fellow did nothing exotic. They used the tool the way the vendor demo showed it. The defect is not in the asking. It is in treating the answer as finished.

The legal profession learned this failure in public. In *Mata v. Avianca, Inc.* (S.D.N.Y. 2023), attorneys filed a brief citing six entirely fictitious cases ChatGPT had generated, complete with fabricated quotations and fake citations. Judge Castel sanctioned the two attorneys and their firm $5,000 under Rule 11. The court was explicit that the sin was not using AI — it was using it as a substitute for verification. In a pharma claims library, the analog is a fabricated or misattributed efficacy reference flowing into promotional content, where it becomes a substantiation defect the FDA is currently penalizing.

The chapter teaches you to use an LLM as a research instrument — to scan literature, map content to approved claims, triage message variants — while running every output through a validation step that catches what the model gets confidently wrong. The discipline here is not anti-AI. It is the opposite of the vendor posture you audited in Chapter 4. Instead of trusting a fluent claim because it sounds authoritative, you will treat fluency as a warning light.

---

## The useful-draft / trustworthy-claim distinction

An LLM is excellent at producing a *useful draft*: a fluent, plausibly sourced literature summary, a claims-library mapping, a set of message variants. A useful draft becomes a *trustworthy claim* only after every atomic assertion in it has been verified against a real, correctly attributed source and has cleared expert review. The whole chapter operationalizes the gap between those two states.

The mistake is not generating the draft. It is shipping the draft as though generation and verification were the same act.

This is worth stating flatly because the tool actively encourages the confusion. The draft *looks* finished. It has the surface features — citations, hedged language, section structure, confident register — that we use as proxies for "someone did the work." The Fellow's job is to stop reading those surface features as evidence of work. They are evidence that the model is very good at producing surface features.

![Two-stage pipeline: an LLM generates a draft, a validation harness sits between, and only after it does the draft become a trustworthy claim; a labeled gap separates generation from verification.](images/10-llms-for-commercial-research-fig-01.png)

*Figure 10.1 — Generation and verification are different acts*

<!-- → [DIAGRAM: Two-stage pipeline — "LLM generates draft" on the left, arrow to "Validation harness" in the middle, arrow to "Trustworthy claim" on the right. A large gap labeled "the gap this chapter operationalizes" separates left from right. Caption: "Generation and verification are different acts. The harness is what fills the gap."] -->

---

## The fluency trap

LLM output reads as authoritative regardless of accuracy. Human-like fluency and a confident register project credibility even when the content is fabricated. This is the **fluency trap**: the better the prose, the harder it is to disbelieve. And the model's prose is uniformly good — it does not hesitate or hedge the way a human expert does when they are on thin ice.

Human experts project uncertainty through surface behavior. They say "I'm not sure about this one." They add caveats. They recommend checking. The model does not. It produces the same confident paragraph whether the underlying claim is well-established or entirely invented. Confidence is decoupled from correctness in a way it rarely is for a human, and the decoupling is invisible in the text.

For a commercial research workflow under content-volume pressure, this is exactly backwards from what you want. The cues you instinctively use to judge reliability — fluency, structure, citation density — are the ones the model produces for free.

---

## Automation bias and the trust trap

People over-rely on automated systems — the well-documented phenomenon of automation bias — and the effect is strongest precisely when the system appears competent and users are trying to save time, a description of almost every MLR and research workflow under deadline. [verify — unconfirmed: the specific survey source (arXiv 2509.08010) and its exact wording were not confirmed in this pass, though automation bias / over-reliance on automation is a long-established finding in the human-factors literature.] Worse, the reliance compounds. As exposure to quick, authoritative answers increases, willingness to question them decreases. Call it the **trust trap**. The defense cannot be a one-time act of vigilance. It has to be structural — a harness that runs whether or not the Fellow happens to feel skeptical that day.

---

## Where LLMs genuinely help

The skepticism above is not a reason to avoid the tool. It is a reason to point it at tasks where a wrong draft is cheap to catch.

**Literature scanning** — surfacing candidate papers and claims *as drafts to verify*, not as findings. The model proposes; the Fellow disposes.

**Claims-library mapping** — linking generated content to pre-approved claims and flagging incomplete claims or missing references before human MLR review. This is already a mature pharma use case in products like Veeva PromoMats content tooling and Indegene's Regulated Content Orchestrator, though capabilities are vendor-reported and should be verified. [verify current product capabilities against primary sources]

**Creative and message variation** — generating and triaging message variants for human selection, where the cost of a bad draft is low and the savings in time are high.

**Mechanical MLR pre-checks** — decomposing content into claims, charts, and references, linking each to an approved source, and flagging gaps for a human reviewer.

The common thread across every productive use: the LLM does *mechanical* work — generating, decomposing, linking, flagging — and a human does the *judgment*. The moment you ask the model to make the judgment ("is this claim true?", "does this satisfy fair balance?"), you have left the safe zone.

---

## How LLMs fail, with rates

The failure modes are not mysterious. They are measured.

**Hallucinated and misattributed citations.** A peer-reviewed study (Chelli et al., "Hallucination Rates and Reference Accuracy of ChatGPT and Bard for Systematic Reviews," *JMIR* 2024;26:e53164) found GPT-3.5 produced 39.6% non-existent references, GPT-4 a lower 28.6%, and Bard 91.4%. The directional finding is robust: GPT-4-class models hallucinated fewer references than GPT-3.5. (Secondary summaries circulate other figures, e.g., ~55% for GPT-3.5 versus ~18–20% for GPT-4-class models; [verify — those particular numbers come from other write-ups and were not confirmed against a primary source here].)

Two things about those rates are load-bearing.

First, topic familiarity drives fabrication in the wrong direction. Hallucination is *highest where the literature is thinnest* — exactly the rare-disease and niche-indication territory where pharma research is hardest and the stakes feel highest. One experimental study found about 6% fabricated references for a well-studied condition (major depressive disorder) versus roughly 28–29% for less-studied conditions (binge eating disorder and body dysmorphic disorder) — and as high as 46% for a specialized review on a less-common topic (Linardon et al., "Influence of Topic Familiarity and Prompt Specificity on Citation Fabrication in Mental Health Research Using Large Language Models," *JMIR Mental Health* 2025; PMC12658395). The lesson is counterintuitive: **trust the model less, not more, exactly where you most want help.**

Second, "real" does not mean "accurate." Some genuine citations carry bibliographic errors — wrong or invalid DOIs, or mismatched details that survive a casual check because the journal and authors are real. This is the opening-case failure: a resolving link is not a verified claim.

![Bar chart comparing LLM citation-fabrication rate for a well-studied condition (about 6 percent) against niche conditions (about 28 to 29 percent), showing fabrication is highest where the literature is thinnest. Figures are contested and marked verify.](images/10-llms-for-commercial-research-fig-02.png)

*Figure 10.2 — Fabrication is highest where the literature is thinnest (illustrative bars based on Linardon et al., JMIR Mental Health 2025, PMC12658395: ~6% for major depressive disorder vs. ~28–29% for less-studied conditions)*

<!-- → [CHART: Bar chart — hallucination rate by indication type, from PMC12658395 (verify). Bars: well-studied condition (~6%) vs. niche conditions (~28–29%). Caption: "Fabrication is highest where the literature is thinnest — the pharma sweet spot. Trust the model less where you want help most."] -->

**LLM-as-a-judge has limits exactly where you need it.** A tempting fix is to have one LLM grade another's output. Strong judge models reach over 80% agreement with human preferences on general tasks, roughly the level of human-to-human agreement (Zheng et al., "Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena," NeurIPS 2023; arXiv 2306.05685). But that same paper and follow-on work document systematic biases: **position bias** (the order in which options are presented shifts the verdict), **verbosity bias** (longer answers are systematically favored), **self-enhancement bias** (models favor outputs from their own family), and **sycophancy** (models adjust verdicts toward what the user appears to want). Most important for pharma research: agreement between LLM judges and human *experts* is reported to drop substantially — on the order of 60 to 68% — in specialized domains, because the models were tuned toward lay preferences. [verify — unconfirmed: the specific position-bias magnitude (>10 points), the expert-agreement range (60–68%), and the individual arXiv IDs (2410.21819, 2410.02736, 2411.15594) were not confirmed against primary sources in this pass; the Zheng et al. >80% figure and the four named bias types are confirmed from that paper.] Use an LLM judge for triage and ranking. Never for sign-off. Never to approve a claim.

**RAG reduces but does not eliminate the problem.** Retrieval-augmented generation — grounding outputs in retrieved passages — lowers fabrication rates but does not stop them. RAGTruth (Niu et al., "RAGTruth: A Hallucination Corpus for Developing Trustworthy Retrieval-Augmented Language Models," ACL 2024; arXiv 2401.00396) documents LLMs producing claims unsupported by, or outright contradicting, the very passages retrieved for them. Three failure modes survive grounding: *retrieval failure* (the right paper is never fetched), *synthesis hallucination* (the summary overstates what the retrieved text says), and *context misattribution* (a true fact bolted to the wrong source — the opening case, again). RAG is necessary but not sufficient.

---

## The regulatory surface

Generated promotional content lands inside a regulated space. The FDA's fair-balance framework holds that a promotional piece must convey an accurate, non-misleading **net impression** of a product's benefits and risks, evaluated across all elements of the piece as a whole rather than by matching length word-for-word (FDA draft guidance, *Presenting Risk Information in Prescription Drug and Medical Device Promotion*, 2009). A non-deterministic model can hallucinate an unsubstantiated efficacy claim, drift off-label, or generate benefit copy without proportionate risk language. Every one of those is a fair-balance defect. Generated content must pass human MLR review; it cannot bypass it.

Beginning with a September 2025 enforcement push, the FDA sharply escalated promotional enforcement. By legal-tracker counts, the agency issued on the order of 70-plus enforcement letters in 2025 across consumer- and HCP-directed materials, with roughly 64 Untitled Letters and about 10 Warning Letters to drug and biologic manufacturers — and only about five issued before the September action — with priorities including omission of risk information and unsubstantiated claims (counts vary by source and date; e.g., King & Spalding and Covington 2025 year-in-review summaries; the escalation trend is strongly corroborated). Meanwhile, promotional-material production volume reportedly rose roughly 29% year over year in the US in 2025, a vendor-reported figure (Indegene). [verify — the 29% production-volume figure is vendor-reported and not independently confirmed.] That combination — more content, faster production, stricter enforcement — is exactly why the validation step cannot be the thing that gets cut.

---

## The asymmetric-harm argument: why human review is load-bearing

Pull the failures together and a pattern appears. Every automated control degrades in the same place.

Fluency raises confidence where accuracy is lowest. Hallucination is highest in niche indications. The LLM-judge backstop is weakest in expert domains. RAG still lets synthesis errors through. Faithfulness metrics — which score the fraction of atomic claims supported by retrieved context — fail most on complex queries. And the regulator is actively penalizing the defects that result.

There is exactly one control positioned to catch what all the others miss: an expert who is *expected to distrust fluent output*. This is the asymmetric-harm argument. Human review is not a courtesy step at the end. It is the only reliable layer, and it has to be placed where automated confidence is highest and automated reliability is lowest — which, as every failure mode shows, is the same place.

---

## Building the validation harness

The harness is the chapter's named artifact. It is a workflow with four layers — each taught alongside its limits, because a control you trust blindly is just another fluency trap.

**Layer one: citation verification.** Programmatically resolve every reference. Does the work exist? Is the DOI or PMID valid? Does the cited text actually support the claim made? This single layer catches both fabrications and real-but-wrong citations. It is the layer the *Mata* attorneys skipped, and it is non-negotiable.

**Layer two: groundedness scoring.** Decompose the generated answer into atomic claims and score the fraction supported by retrieved context — tools like RAGAS faithfulness metric provide a structured way to do this (docs at ragas.io). *Limit:* faithfulness scoring is moderately effective on simple queries and weak on complex ones. One benchmark reported it failing to score roughly 83.5% of examples in a specific configuration (Cleanlab [config-specific; verify]). Treat it as a triage signal, not a pass/fail oracle.

**Layer three: compliance flag.** Screen generated content for fair-balance gaps, unsubstantiated efficacy language, and off-label drift. Route every flag to MLR or counsel — never auto-approve. This is the hook into Chapter 11's compliance-routing discipline. Dedicated hallucination detectors (RAGTruth-trained models, LettuceDetect, Luna) can sit alongside this layer as a complementary check. None of them replaces layer four.

**Layer four: human-in-the-loop capstone.** The model does the mechanical pre-checks. The expert makes the judgment. By the time content reaches the human, the harness has resolved references, scored groundedness, and surfaced compliance flags — so the human's scarce attention goes to what only a human can decide: is this claim true? Is the signal real? Could the partner defend it to a regulator or an audit committee?

![Vertical four-layer validation harness: citation verification, groundedness scoring, compliance flag, and human capstone, each annotated with what it catches on the left and its limit on the right.](images/10-llms-for-commercial-research-fig-03.png)

*Figure 10.3 — The four-layer validation harness, with each layer's catch and limit*

<!-- → [DIAGRAM: Four-layer pipeline as a vertical stack — citation verification → groundedness scoring → compliance flag → human capstone. For each layer, a "catches" annotation on the left and a "limit" annotation on the right. Caption: "The harness does not make the LLM trustworthy. It makes the LLM useful by removing the errors it hides."] -->

---

## The evidence scan, done with the harness

Return to the opening task — what is the peer-reviewed evidence that point-of-care messaging lifts new patient starts? — and run it through all four layers.

*Generate.* Prompt the LLM for candidate papers with full citations, instructing it to return only references it can attribute and to mark uncertainty. It returns eight candidates.

*Layer one.* Resolve each against PubMed and Crossref. Two fail to resolve — fabricated, drop. One resolves but the abstract describes patient adherence reminders, not physician promotion, finding null — misattributed, drop and note. Five survive.

*Layer two.* For each surviving paper, check that the model's one-line summary matches the abstract's actual finding. One paper described as showing "significant lift" in fact reported a null result for the relevant subgroup — the summary overstated it. Correct the summary, flag the paper as null.

*Layer three.* The draft summary phrased one finding as a benefit claim with no mention of the study's safety caveats. Flag for fair-balance review if any of this language migrates toward promotional use.

*Layer four.* The Fellow reads the four genuinely relevant, correctly summarized papers and concludes: the causal evidence for point-of-care lift is thin and mostly observational. The strong evidence the partner wanted is not there.

The harness did not make the LLM trustworthy. It made the LLM *useful* — it turned a fluent-but-contaminated draft into a smaller, checked, honestly labeled evidence base in a fraction of the time a manual scan would take, while removing exactly the errors a fluent draft hides.

The limit: the harness cannot conjure evidence that does not exist. Its output here is partly a negative result — "the strong evidence you wanted isn't there" — which is itself a finding the lab values. And it cannot, on its own, judge whether the four surviving papers generalize to the partner's context. That is the human's call.

---

## What would change my mind

The chapter's harness design — with citation verification as non-negotiable — would shift if a future model demonstrably resolved and correctly attributed citations at expert-reviewer reliability in niche indications, confirmed by an independent benchmark with no vendor stake in the outcome. Today no such evidence exists. Fabrication is highest exactly where verification matters most, so the harness stays. The position is falsifiable; the evidence does not yet exist to falsify it.

## Still puzzling

Faithfulness metrics fail most on the complex queries that matter most. LLM judges fail most in the expert domains that matter most. Both backstops degrade in the same direction as the task gets harder. Is there an automated check whose reliability rises with task difficulty — or is expert human review structurally the only control with that property? The book's working answer is the latter. But it is genuinely open whether better retrieval architectures or domain-fine-tuned judges could change the calculus.

---

## Exercises

**Warm-up**

1. *(Recall — tests the core distinction)* In your own words, define the difference between a "useful draft" and a "trustworthy claim." Give one concrete example of each from a commercial-research task in pharma. *What this tests: whether you can state the distinction without collapsing it into "AI is good" or "AI is bad."*

2. *(Recall — tests the fluency trap)* Explain why a well-formed citation with a valid DOI is not sufficient evidence that the cited paper supports the claim attached to it. Name the specific failure mode from the chapter's opening case. *What this tests: whether you understand the "real-but-wrong" citation as the more dangerous failure mode.*

3. *(Recall — tests the topic-familiarity effect)* The chapter claims you should trust the model less, not more, in niche indications. Explain the empirical finding that supports this claim and state why it is counterintuitive. *What this tests: whether you can state the finding and its implication without softening it.*

**Application**

4. *(Apply — citation audit)* Take any LLM-generated literature summary with five or more citations. Resolve every citation against PubMed or Crossref. For each, classify it as valid-and-supported, real-but-misattributed, or fabricated. Report the counts. Write one sentence describing the single most dangerous error you found and why it is the most dangerous. *What this tests: whether you can run layer one of the harness on real output.*

5. *(Apply — harness design)* Design the four-layer validation harness for a specific commercial-research task: "generate a one-page evidence summary on whether branded patient support programs improve medication adherence." For each layer, name the tool or check, what it catches, and its documented limit. *What this tests: whether you can operationalize the harness for a task rather than describe it abstractly.*

6. *(Apply — compliance flag)* A generated literature summary includes this sentence: "Three studies demonstrate that EHR-embedded messaging significantly increases new patient starts with no reported safety concerns." Identify every fair-balance and substantiation risk in this sentence. State which flags you would route to MLR counsel and why. *What this tests: whether you can apply the compliance layer to a realistic piece of generated content.*

**Synthesis**

7. *(Synthesize — harness + asymmetric-harm argument)* Connect the four-layer harness to the asymmetric-harm argument. For each layer, state which failure mode it addresses and explain why human review is the only layer that reliably catches what the other three miss. Write this as a one-page memo a data-science lead could use to justify the harness to a partner who wants to cut it. *What this tests: whether you can translate the chapter's argument into a form a skeptical non-technical audience can act on.*

8. *(Synthesize — fluency trap + enforcement context)* Connect the fluency trap to the FDA's 2025 enforcement escalation. Explain the specific mechanism by which AI-accelerated content production under deadline pressure creates the defects (unsubstantiated claims, missing fair balance) the enforcement wave is targeting. *What this tests: whether you can trace the behavioral and structural cause of a regulatory risk.*

**Challenge**

9. *(Challenge — design a benchmark)* Design a study that would let you measure whether a specific LLM, with a specific retrieval configuration, produces citation-verified, correctly attributed summaries at expert-reviewer reliability in a niche pharma indication. Specify: the test set, the evaluation criteria, the ground-truth standard, the measuring party, and the primary threat to validity. You do not need to run it — specify it precisely enough that an independent team could. *What this tests: whether you can articulate the evidence standard that would justify relaxing layer one of the harness.*

---

## Prompts

### Figure 10.1 — Generation and verification are different acts

Generate a single self-contained HTML file (inline CSS, D3 7.9.0 from cdnjs) rendering a left-to-right process diagram with a labeled gap. Three node boxes in a row: "LLM generates draft" (left), "Validation harness" (center), "Trustworthy claim" (right), joined by two arrows pointing right. Between the center and right nodes, draw a wide labeled gap band annotated "the gap this chapter operationalizes." Marks: rectangles (rx=0) for nodes, lines with an arrowhead marker for flow, a dashed bracket for the gap span. Channels: position encodes pipeline order only; no quantitative scales. The left node uses the red accent (the unverified draft); center and right are ink/gray. Use the book CSS variables, no hardcoded hex. Title in EB Garamond, body labels in Inter, source line in caps Inter. Deliverable: one HTML file, role="img" with title/desc, ResizeObserver redraw, prefers-reduced-motion honored. Caption: "Generation and verification are different acts. The harness is what fills the gap."

### Figure 10.2 — Citation-fabrication rate by indication type

Generate a single self-contained HTML file (inline CSS, D3 7.9.0 from cdnjs) rendering a vertical bar chart of two categories on the x-axis: "Well-studied condition" (~6%) and "Niche conditions" (~28–29%, plotted at 28.5). Y-axis is fabrication rate in percent, zero-baseline, domain 0–35. Bars in the single red data series, value-labeled above each bar. Sort by the chart's logical order (well-studied first, niche second), not by value. Add an ALL-CAPS source line: "SOURCE: PMC12658395 — CONTESTED, [VERIFY]." Annotate that figures are contested. margin {top:48,right:40,bottom:56,left:64}; gridlines aria-hidden; tooltip on hover/focus showing the rate. Use book CSS variables, no hardcoded hex; EB Garamond title, Inter body, JetBrains Mono ticks. Deliverable: one HTML file, role="img" with title/desc, ResizeObserver redraw, prefers-reduced-motion honored, inline FALLBACK_DATA literal. Caption: "Fabrication is highest where the literature is thinnest."

### Figure 10.3 — The four-layer validation harness

Generate a single self-contained HTML file (inline CSS, D3 7.9.0 from cdnjs) rendering a vertical stack of four stacked node boxes connected top-to-bottom by down arrows: "Citation verification," "Groundedness scoring," "Compliance flag," "Human capstone." For each layer, place a left-side "catches" annotation and a right-side "limit" annotation aligned to the box. Marks: rectangles (rx=0), arrowhead-marked connector lines, small side text labels. Channels: vertical position encodes pipeline order; left/right text columns carry the catch/limit pairs; no numeric scales. The "Human capstone" box uses the red accent as the load-bearing layer; others ink/gray. Use book CSS variables, no hardcoded hex; EB Garamond title, Inter body, caps Inter source/label line. Deliverable: one HTML file, role="img" with title/desc, ResizeObserver redraw, keyboard-focusable boxes with aria-label, prefers-reduced-motion honored. Caption: "The harness does not make the LLM trustworthy. It makes the LLM useful by removing the errors it hides."

---

## Chapter 10 Exercises: LLMs for Commercial Research and Content Intelligence

**Project:** One Drug, End to End
**This chapter adds:** An LLM scan of your drug's literature and claims, run through the four-layer validation harness — the capstone that catches the fabricated and misattributed citations the whole series has been warning about.

We finish the arc with **Jardiance (empagliflozin)** — branded SGLT2 inhibitor, branded rivals Farxiga and Invokana, generic alternatives metformin and sulfonylureas. Across the series you built a propensity baseline (Ch6), audited a vendor's MoE claim (Ch7), separated persuadables from sure things (Ch8), and measured brand association honestly (Ch9). Every one of those steps generated empirical claims and citations. This chapter's piece: scan the Jardiance literature with an LLM, then run the harness that turns a fluent-but-contaminated draft into a checked, honestly-labeled evidence base. The harness is the natural validator for the entire case.

### Exercise 1 — When to Use AI

1. Prompt an LLM to surface candidate peer-reviewed papers on a Jardiance evidence question (e.g., cardiovascular-outcome or new-patient-start claims) *as drafts to verify*, with full citations and an instruction to mark uncertain references. *Why AI works here:* literature scanning as draft generation — the model proposes, you dispose, and every output is checkable against PubMed/Crossref.
2. Have it decompose a Jardiance promotional paragraph into atomic claims and link each to a candidate approved source. *Why AI works here:* mechanical decomposition — a structured transformation whose output a human MLR reviewer then judges.

**The tell:** you can independently evaluate the output — every citation resolves or it does not; every atomic claim maps to a source you can open.

### Exercise 2 — When NOT to Use AI

1. Do not let the LLM tell you whether the Jardiance evidence is *strong enough to act on*. It produces the same confident paragraph whether a claim is well-established or invented — the fluency trap — and confidence is decoupled from correctness. *Why AI fails here:* hallucination — fabrication is highest exactly in the niche corners where you most want help, and the real-but-wrong citation survives a casual click.
2. Do not let one LLM grade another's Jardiance summary for sign-off. LLM-as-judge agreement with human *experts* drops to roughly 60–68% in specialized domains [verify], with position, verbosity, self-enhancement, and sycophancy biases. *Why AI fails here:* values/ground-truth — fair-balance and substantiation judgments are regulated calls a model cannot certify, and the judge is weakest exactly where the stakes are highest.

**The tell:** if the AI's "this evidence is solid" or "this passes review" is your *reason*, you have failed; if it is a *tool* output you run through citation verification and human MLR, you are fine. **Series connection:** this is a **T7** judgment — hallucinated-citation (fluent-but-wrong) plus missing ground truth. A fabricated or misattributed Jardiance reference flowing into promotional content is a substantiation defect the FDA is actively penalizing. The human capstone owns the "defensible to a regulator?" call.

### Exercise 3 — LLM Exercise

**What you're building this chapter:** a Jardiance evidence summary generated by an LLM and then passed through all four harness layers — citation verification, groundedness scoring, compliance flag, human capstone — producing a smaller, checked, honestly-labeled evidence base (including any negative result).

**Tool:** Claude, run as a **Claude Project**. Persistent drug-context helps because the harness output is the capstone of the entire One Drug case — the Project holds the Jardiance class context, the Chapter 8 incrementality findings, and the Chapter 9 brand caveats, so the literature scan is interpreted against everything you already established rather than from scratch.

**The Prompt:**

```
You are running an LLM literature scan for a running case on one branded drug
carried end to end: Jardiance (empagliflozin), a branded SGLT2 inhibitor with
branded competitors (Farxiga, Invokana) and generic alternatives (metformin,
sulfonylureas).

STEP 1 — GENERATE (useful draft): List up to 8 candidate peer-reviewed references
relevant to this Jardiance evidence question: [PASTE YOUR QUESTION — e.g., "what is
the peer-reviewed evidence on Jardiance's effect on a specific outcome"]. For each,
give author, journal, year, DOI, and a one-line summary of the finding. Return ONLY
references you can attribute; mark any you are unsure of as [uncertain]. Do not
generate a reference you cannot attribute.

STEP 2 — set up the four-layer harness as a checklist I will run:
- Layer 1 (citation verification): every reference resolved against PubMed/Crossref;
  exists? DOI valid? does the cited text support the claim?
- Layer 2 (groundedness): does each one-line summary match the abstract's ACTUAL
  finding (not overstate a null as "significant lift")?
- Layer 3 (compliance flag): does any phrasing read as an unsubstantiated Jardiance
  efficacy/benefit claim with no fair-balance risk language — route to MLR?
- Layer 4 (human capstone): is the SURVIVING evidence strong enough that a partner
  could defend a Jardiance claim to a regulator or audit committee?

Do NOT certify any reference yourself — describe what I must check. Flag every
empirical magnitude as [verify]. It is acceptable and valuable for the honest output
to be a NEGATIVE result ("the strong evidence isn't there").

ADAPTATION: replace Jardiance and its class with your own drug. In ChatGPT or
Gemini, paste your earlier-chapter findings at the top so the scan is interpreted in
context.
```

**What this produces:** a raw LLM draft plus a four-layer harness checklist — the before/after pair that turns a contaminated summary into a checked Jardiance evidence base.

**How to adapt:** swap the drug and your evidence question; in ChatGPT/Gemini re-supply prior findings each session; in a Claude Project, store the case context as Project knowledge. Save the raw output verbatim *before* checking — the before/after comparison is the data.

**Connection to previous chapters:** this harness is the validator the whole series pointed at — it catches the hallucinated citation Chapter 9 warned about (the fake "brand IAT" study), the inflated-lift framing Chapter 8 dismantled, and the unverified vendor claim Chapters 1, 5, and 7 taught you to flag.

**Preview of next chapter:** Chapter 11 takes the compliance flags this harness raises and builds the MLR/counsel routing discipline around them — the harness feeds the governance layer.

### Exercise 4 — CLI Exercise

**What you're building:** layer one of the harness as runnable code — a script that resolves the LLM's Jardiance citation list against Crossref/PubMed and reports survival.

**Tool:** Claude Code (or Cowork) — it can write the resolver, hit the APIs, and emit a structured report. **Skill level:** intermediate (comfortable with HTTP requests and JSON).

**Setup:**
- [ ] The raw citation list from Ex3 saved as `./data/jardiance-citations.txt` (read-only).
- [ ] Python with `requests` (Crossref REST API is keyless; PubMed E-utilities optional).
- [ ] An `./outputs/` folder.

**The Task:**

```
Read ONLY ./data/jardiance-citations.txt (do not modify it). For each citation,
query Crossref (and PubMed if a PMID is present) and return three fields:
  exists (boolean), doi_valid (boolean), abstract_fetched (string or null).
Be polite to the APIs (include a mailto/User-Agent, rate-limit your requests). Do
NOT fabricate a result for any citation that fails to resolve — report it as
exists=false.

Write the per-citation report and a summary count ("N of M citations survived layer
one") to ./outputs/harness-layer1.txt. Do not write anywhere else. Stop when the
file exists, then print it so I can verify the survivors myself.
```

**Expected output:** a per-citation resolution table and a survival count — how many of the LLM's Jardiance references actually exist with valid DOIs.

**What to inspect:** how many citations were fabricated? How many resolved but you will still need to read (real-but-possibly-misattributed)? Did the script invent any "exists=true" it could not confirm?

**If it goes wrong:** if Claude Code marks an unresolved citation as existing (failure), require `exists=false` on any non-200/empty response and re-run; if it hammers the API, add rate-limiting and a contact header.

**CLAUDE.md note:** add `Citation resolvers must report exists=false on any unconfirmed reference — never fabricate a resolution; always include an API contact header and rate-limiting.`

### Exercise 5 — AI Validation Exercise

**What you're validating:** the surviving Jardiance citations from Ex4 — specifically whether the LLM's one-line summary matches each paper's *actual* finding (layer two), and whether any surviving reference is real-but-misattributed.

**Validation type:** groundedness / citation-faithfulness audit — the harness's layer two and the capstone, layer four. **Risk level:** high — because a real-but-wrong Jardiance citation survives a casual click and only fails when read, and a misattributed efficacy reference in promotional content is exactly the substantiation defect the FDA's 2025 enforcement wave targets.

**Setup:** use your Ex3 draft and Ex4 survivor list. For a specific failure to practice on, take a pre-generated summary in which one citation is real but describes a *patient-adherence-reminder* study (null finding) rather than physician promotion — the opening-case failure, ported to Jardiance.

**The Validation Task:**

```
Validation Checklist — Chapter 10 (Jardiance literature harness)

Mark each Pass / Fail / Cannot-determine:
- Correctness: For each surviving citation, does the LLM's one-line summary match
  the abstract's actual finding (no overstating a null as "significant")?
- Completeness: Were all four harness layers run (verification, groundedness,
  compliance flag, human capstone)?
- Scope: Are all magnitudes flagged [verify] and is any negative result reported
  honestly rather than hidden?
- Attribution criterion: Is any surviving reference real-but-misattributed (correct
  journal/authors, wrong topic or reversed finding)?
- Compliance criterion: Is any phrasing an unsubstantiated Jardiance benefit claim
  lacking fair-balance language, routed to MLR?
- Failure-mode check: Look specifically for the hallucinated/misattributed citation
  (fluent-but-wrong: a resolving DOI on a paper that does not support the claim) and
  for missing ground truth (a "strong evidence" verdict with no human capstone
  judgment that a regulator could be satisfied).
```

**What to do with findings:** all Pass — the evidence base is checked and defensible (even if its honest verdict is "the strong evidence isn't there"). One Fail — correct the summary, drop the misattributed citation, route the compliance flag, and re-validate. Multiple Fails — discard the LLM draft as a fluency-trap exhibit and rebuild the evidence base from the survivors you read yourself.

**AI Use Disclosure prompt:** *Write two sentences naming exactly what the AI did and the one judgment it could not make. Example: "I used Claude to draft the Jardiance literature scan and decompose claims; I decided which surviving citations actually supported their claims and whether the evidence was strong enough to defend to a regulator, because no automated layer can make the real-but-misattributed catch or the human capstone call."* (Mandatory.)

**Series connection:** the failure mode is the **hallucinated/misattributed citation** at tier **T7** — the fluency trap in its most consequential form, and the reason the human capstone is the one control in the entire series positioned to catch what every automated layer misses.
