# Chapter 10 — LLMs for Commercial Research and Content Intelligence
*Fluency is not accuracy. Treating the gap seriously is the whole skill.*

A Fellow is asked to assemble a one-page evidence summary on whether point-of-care digital messaging lifts new patient starts. They prompt a capable LLM: *"Summarize the peer-reviewed evidence that EHR-embedded promotional messaging increases new prescriptions, with citations."* Ninety seconds later they have four clean paragraphs, five citations with author names, journals, years, and DOIs. It reads like a literature review a postdoc would be proud of.

Two of the five citations do not exist. A third is a real paper — correct authors, correct journal, resolving DOI — but it studied medication adherence reminders sent to patients, not promotional messaging to physicians, and its finding was null.

That third citation is the one that matters most. A reviewer who spot-checks will click the link, see a real paper, see a real journal, and move on. The fabrications are easy to catch once you look. The real-but-wrong citation survives looking. It only fails when you read it.

This is the failure mode the chapter is built around. The Fellow did nothing exotic. They used the tool the way the vendor demo showed it. The defect is not in the asking. It is in treating the answer as finished.

The legal profession learned this failure in public. In *Mata v. Avianca* (S.D.N.Y. 2023), attorneys filed a brief citing six entirely fictitious cases ChatGPT had generated, complete with fabricated quotations and fake page numbers. They were sanctioned $5,000 under Rule 11. The court was explicit that the sin was not using AI — it was using it as a substitute for verification. In a pharma claims library, the analog is a fabricated or misattributed efficacy reference flowing into promotional content, where it becomes a substantiation defect the FDA is currently penalizing.

The chapter teaches you to use an LLM as a research instrument — to scan literature, map content to approved claims, triage message variants — while running every output through a validation step that catches what the model gets confidently wrong. The discipline here is not anti-AI. It is the opposite of the vendor posture you audited in Chapter 4. Instead of trusting a fluent claim because it sounds authoritative, you will treat fluency as a warning light.

---

## The useful-draft / trustworthy-claim distinction

An LLM is excellent at producing a *useful draft*: a fluent, plausibly sourced literature summary, a claims-library mapping, a set of message variants. A useful draft becomes a *trustworthy claim* only after every atomic assertion in it has been verified against a real, correctly attributed source and has cleared expert review. The whole chapter operationalizes the gap between those two states.

The mistake is not generating the draft. It is shipping the draft as though generation and verification were the same act.

This is worth stating flatly because the tool actively encourages the confusion. The draft *looks* finished. It has the surface features — citations, hedged language, section structure, confident register — that we use as proxies for "someone did the work." The Fellow's job is to stop reading those surface features as evidence of work. They are evidence that the model is very good at producing surface features.

<!-- → [DIAGRAM: Two-stage pipeline — "LLM generates draft" on the left, arrow to "Validation harness" in the middle, arrow to "Trustworthy claim" on the right. A large gap labeled "the gap this chapter operationalizes" separates left from right. Caption: "Generation and verification are different acts. The harness is what fills the gap."] -->

---

## The fluency trap

LLM output reads as authoritative regardless of accuracy. Human-like fluency and a confident register project credibility even when the content is fabricated. This is the **fluency trap**: the better the prose, the harder it is to disbelieve. And the model's prose is uniformly good — it does not hesitate or hedge the way a human expert does when they are on thin ice.

Human experts project uncertainty through surface behavior. They say "I'm not sure about this one." They add caveats. They recommend checking. The model does not. It produces the same confident paragraph whether the underlying claim is well-established or entirely invented. Confidence is decoupled from correctness in a way it rarely is for a human, and the decoupling is invisible in the text.

For a commercial research workflow under content-volume pressure, this is exactly backwards from what you want. The cues you instinctively use to judge reliability — fluency, structure, citation density — are the ones the model produces for free.

---

## Automation bias and the trust trap

People over-rely on automated systems, and the effect is strongest precisely "when the system appears competent and users are trying to save time" — a description of almost every MLR and research workflow under deadline (survey of over-reliance, arXiv 2509.08010 [verify]). Worse, the reliance compounds. As exposure to quick, authoritative answers increases, willingness to question them decreases. Call it the **trust trap**. The defense cannot be a one-time act of vigilance. It has to be structural — a harness that runs whether or not the Fellow happens to feel skeptical that day.

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

**Hallucinated and misattributed citations.** A peer-reviewed study (JMIR 2024, e53164) found GPT-3.5 produced roughly 39.6% non-existent references, with GPT-4-class models substantially better. Secondary summaries circulate figures like 55% fabrication for GPT-3.5 versus 18 to 20% for GPT-4-class models — treat those specific numbers as [verify] against the primary source, but the directional finding is robust: newer models hallucinate less.

Two things about those rates are load-bearing.

First, topic familiarity drives fabrication in the wrong direction. Hallucination is *highest where the literature is thinnest* — exactly the rare-disease and niche-indication territory where pharma research is hardest and the stakes feel highest. One analysis found approximately 6% fabricated references for a well-studied condition (major depressive disorder) versus 28 to 29% for niche conditions like body dysmorphic disorder (PMC12658395 [verify]). The lesson is counterintuitive: **trust the model less, not more, exactly where you most want help.**

Second, "real" does not mean "accurate." A meaningful fraction of genuine citations carry bibliographic errors — wrong or invalid DOIs, mismatched details that survive a casual check because the journal and authors are real [verify primary]. This is the opening-case failure. A resolving link is not a verified claim.

<!-- → [CHART: Bar chart — hallucination rate by indication type, from PMC12658395 (verify). Bars: well-studied condition (~6%) vs. niche conditions (~28–29%). Caption: "Fabrication is highest where the literature is thinnest — the pharma sweet spot. Trust the model less where you want help most."] -->

**LLM-as-a-judge has limits exactly where you need it.** A tempting fix is to have one LLM grade another's output. Strong judge models reach over 80% agreement with human preferences on general tasks, roughly human-to-human level (Zheng et al., MT-Bench / Chatbot Arena, NeurIPS 2023). But the technique carries documented biases: **position bias** (the order in which options are presented shifts the verdict by more than 10 percentage points in pairwise comparisons), **verbosity bias** (longer answers are systematically favored), **self-enhancement bias** (models favor outputs from their own family, arXiv 2410.21819), and **sycophancy** (models adjust verdicts toward what the user appears to want, arXiv 2410.02736). Most important for pharma research: agreement between LLM judges and human *experts* drops to roughly 60 to 68% in specialized domains, because the models were tuned toward lay preferences (survey, arXiv 2411.15594 [verify ranges]). Use an LLM judge for triage and ranking. Never for sign-off. Never to approve a claim.

**RAG reduces but does not eliminate the problem.** Retrieval-augmented generation — grounding outputs in retrieved passages — lowers fabrication rates (RAG survey, arXiv 2506.00054) but does not stop them. RAGTruth (ACL 2024) documents LLMs producing claims unsupported by, or outright contradicting, the very passages retrieved for them. Three failure modes survive grounding: *retrieval failure* (the right paper is never fetched), *synthesis hallucination* (the summary overstates what the retrieved text says), and *context misattribution* (a true fact bolted to the wrong source — the opening case, again). RAG is necessary but not sufficient.

---

## The regulatory surface

Generated promotional content lands inside a regulated space. The FDA's fair-balance requirement holds that risk information must appear with prominence and readability reasonably comparable to benefit information, so that the net impression is not misleading — it governs both content and presentation, and does not require equal length (*Presenting Risk Information in Prescription Drug and Medical Device Promotion*, FDA). A non-deterministic model can hallucinate an unsubstantiated efficacy claim, drift off-label, or generate benefit copy without proportionate risk language. Every one of those is a fair-balance defect. Generated content must pass human MLR review; it cannot bypass it.

Following a September 2025 enforcement push and an accompanying presidential memo, the FDA sharply escalated promotional enforcement — by various counts, on the order of sixty compliance letters in 2025 against roughly five in the period before the September action, with priorities including omission of risk information and unsubstantiated claims (ProPharma; Morgan Lewis — counts approximate; vary by source and date; the escalation trend is well corroborated [verify specifics against primary FDA sources]). Meanwhile promotional-material production volume rose roughly 29% year over year in the US in 2025, vendor-reported (Indegene [verify]). That combination — more content, faster production, stricter enforcement — is exactly why the validation step cannot be the thing that gets cut.

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

**LLM exercise (copy-paste prompt):**

> "Summarize the peer-reviewed evidence that [your chapter's intervention] produces [your chapter's outcome], with full citations — author, journal, year, DOI. For any reference you are not confident about, mark it [uncertain]. Do not generate a reference you cannot attribute."

Save the raw output verbatim before you check anything. The before-and-after comparison is the data.

**CLI exercise.** Write a script that takes the citation list from the LLM exercise and resolves each against Crossref or PubMed, returning three fields per citation: `exists` (boolean), `doi_valid` (boolean), `abstract_fetched` (string or null). This is layer one of your harness. Run it on the raw output and report how many citations survive.

**AI Validation exercise.** For each citation that survives layer one, read the actual abstract and grade whether the LLM's one-line summary matches the paper's actual finding. Count how many "supported" claims were in fact overstated, reversed, or null. That count is your fluency-trap exposure for this task. Record it.

**AI Use Disclosure**

*Write two sentences naming exactly what the AI tool did in your work for this chapter and what judgment you supplied that the AI could not. The Part B standard: name one judgment in your harness that no automated layer could make — specifically, whether the surviving evidence is strong enough that a partner could defend the claim to a regulator or an audit committee.*

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
