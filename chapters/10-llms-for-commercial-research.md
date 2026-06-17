# Chapter 10 — LLMs for Commercial Research and Content Intelligence

> **[METHOD + TEST-DESIGN CHECKPOINT]** This chapter is the point in the
> book where you lock the method and test design for your own research
> thread (Part B). The deliverable it trains — a validation harness that
> separates a *useful draft* from a *trustworthy claim* — is the tool you
> will lean on for the rest of the lab.

## 10.1 Chapter overview

By the end of this chapter you will be able to use a large language model (LLM) as a research instrument — to scan literature, map generated content back to approved claims, and triage message variants — while running every output through a validation step that catches what the model gets confidently wrong. The discipline here is not anti-AI. It is the opposite of the vendor posture you audited in Chapter 4: instead of trusting a fluent claim because it sounds authoritative, you will treat fluency as a *warning light*. The chapter's single takeaway is that an LLM is a powerful draft generator inside a harness, and never the final authority on a factual or promotional claim.

## 10.2 Learning objectives

By the end of this chapter you will be able to:

1. **(Apply)** Use an LLM to scan research and map claims to evidence *with provenance* — every assertion carrying a resolvable source.
2. **(Evaluate)** Validate LLM output for hallucinated or misattributed citations, fair-balance and regulatory risk, and fluent-but-wrong analysis.
3. **(Create / Part B)** Build an evaluation harness that separates a "useful draft" from a "trustworthy claim" for your own research thread.

## 10.3 Opening case: the evidence summary that cited a study saying the opposite

A Fellow is asked to assemble a one-page evidence summary on whether point-of-care digital messaging lifts new-patient starts. They prompt a capable LLM: *"Summarize the peer-reviewed evidence that EHR-embedded promotional messaging increases new prescriptions, with citations."* Ninety seconds later they have four clean paragraphs, five citations with author names, journals, years, and DOIs. It reads like a literature review a postdoc would be proud of.

Two of the five citations do not exist. A third is a real paper — correct authors, correct journal — but it studied *medication adherence reminders sent to patients*, not promotional messaging to physicians, and its finding was null. The LLM had stitched a plausible sentence onto a real reference whose DOI *resolves*, which makes it far more dangerous than the two fabrications: a reviewer who spot-checks will click the link, see a real paper, and move on.

This is the failure mode the chapter is built around. The Fellow did nothing exotic. They used the tool the way the vendor demo showed it. The defect is not in the asking; it is in treating the answer as finished. The legal profession learned this in public: in *Mata v. Avianca* (S.D.N.Y. 2023), attorneys filed a brief citing six entirely fictitious cases ChatGPT had generated, complete with fabricated quotations, and were sanctioned $5,000 under Rule 11 (*Mata v. Avianca, Inc.*, Dkt. 54). The court was explicit that the sin was not using AI — it was using it as a substitute for verification. In a pharma claims library, the analog is a fabricated or misattributed efficacy reference flowing into promotional content, where it becomes a substantiation and fair-balance defect the FDA is currently penalizing.

## 10.4 Prerequisites

You should be able to write a basic LLM prompt, read a research abstract, and recall from Chapter 5 the distinction between an *association* claim and a *causal* claim. From Chapter 4 you should carry the habit of asking "what KPI, what data, what evidence" of any assertion — here you turn that skepticism on your *own* AI outputs.

## 10.5 Core sections

### 10.5.1 The useful-draft / trustworthy-claim distinction

An LLM is excellent at producing a *useful draft*: a fluent, plausibly sourced literature summary, a claims-library mapping, a set of message variants. A useful draft becomes a *trustworthy claim* only after every atomic assertion in it has been verified against a real, correctly attributed source and has cleared expert review. The entire chapter operationalizes the gap between those two states. The mistake is not generating the draft; it is shipping the draft as though generation and verification were the same act.

This is worth stating flatly because the tool actively encourages the confusion. The draft *looks* finished. It has the surface features — citations, hedged language, section structure — that we use as proxies for "someone did the work." The Fellow's job is to stop reading those surface features as evidence of work.

### 10.5.2 The fluency trap

LLM output reads as authoritative *regardless of accuracy*. Human-like fluency and a confident register project credibility even when the content is fabricated — confidence is decoupled from correctness in a way it rarely is for a human expert, who usually hedges, hesitates, or signals uncertainty when on thin ice. This is the **fluency trap**: the better the prose, the harder it is to disbelieve, and the model's prose is uniformly good (TechPolicy.Press, "AI Trustwashing" [verify]). For a busy commercial-research workflow under content-volume pressure, this is exactly backwards from what you want — the cues you instinctively trust are the ones the model produces for free.

### 10.5.3 Automation bias and the trust trap

People over-rely on automated systems, and the effect is strongest precisely "when the system appears competent and users are trying to save time" — a fair description of any MLR or research workflow under deadline (over-reliance survey, arXiv 2509.08010 [verify]). Worse, the reliance compounds: as exposure to quick, authoritative answers increases, willingness to question them decreases. Call it the **trust trap**. The defense cannot be a one-time act of vigilance; it has to be a structural step — a harness — that runs whether or not the Fellow happens to feel skeptical that day.

### 10.5.4 Where LLMs genuinely help in commercial research

The skepticism above is not a reason to avoid the tool. It is a reason to point it at tasks where a wrong draft is cheap to catch:

- **Literature scanning** — surfacing candidate papers and claims *as drafts to verify*, not as findings. The model proposes; the Fellow disposes.
- **Claims-library mapping** — linking generated content to pre-approved claims and flagging incomplete claims or missing references *before* human MLR review. This is already a mature pharma use case (e.g., Veeva PromoMats content tooling; Indegene's "Regulated Content Orchestrator"; Vodori — all vendor-reported [verify]).
- **Creative and message variation** — generating and triaging message variants for human selection.
- **Mechanical MLR pre-checks** — decomposing content into claims, charts, and references, linking each to an approved source, and flagging gaps for a human reviewer.

The common thread: in every productive use, the LLM does *mechanical* work — generating, decomposing, linking, flagging — and a human does the *judgment*. The moment you ask the model to make the judgment ("is this claim true?", "is this fair balance?"), you have left the safe zone.

### 10.5.5 How LLMs fail, with rates

The failure modes are not mysterious; they are measured.

**Hallucinated and misattributed citations.** Model generation matters a great deal. A peer-reviewed study (JMIR 2024, e53164) found GPT-3.5 produced roughly 39.6% non-existent references, with GPT-4 substantially better. Secondary summaries report figures like ~55% fabrication for GPT-3.5 versus ~18–20% for GPT-4-class models, but treat those specific numbers as `[verify]` against the primary source. Two findings are robust enough to teach from:

- **Topic familiarity drives fabrication.** Hallucination is *highest where the literature is thinnest* — exactly the rare-disease and niche-indication territory where pharma research is hardest and the stakes feel highest. One analysis found ~6% fabricated references for a well-studied condition (major depressive disorder) versus ~28–29% for niche conditions (binge eating disorder, body dysmorphic disorder) (PMC12658395 [verify]). The lesson is counterintuitive and load-bearing: **trust the model less, not more, exactly where you most want help.**
- **"Real" does not mean "accurate."** A meaningful fraction of *genuine* citations carry bibliographic errors — wrong or invalid DOIs, mismatched details `[verify primary]`. This is the opening-case failure: the citation resolves, so it survives a casual check.

**LLM-as-a-judge has limits exactly where you need it.** A tempting fix is to have one LLM grade another's output. The technique is real — strong judge models (GPT-4-class) reach >80% agreement with human preferences on general tasks, roughly human-to-human level (Zheng et al., MT-Bench / Chatbot Arena, NeurIPS 2023). But it carries documented biases: **position bias** (order of options swings the verdict — over 10% accuracy swing on order flips in pairwise code judging), **verbosity bias** (longer answers favored), **self-enhancement bias** (models favor their own family; arXiv 2410.21819), and **sycophancy** (arXiv 2410.02736). Most important for us, the agreement between LLM judges and *human experts* drops to roughly 60–68% in specialized domains, because the models are tuned toward *lay* preferences (survey, arXiv 2411.15594 — cite as a range, not a single study). So: use an LLM judge for triage and ranking, never for sign-off, and never to approve a claim.

**RAG reduces but does not eliminate the problem.** Retrieval-augmented generation — grounding outputs in retrieved passages — lowers fabrication (RAG survey, arXiv 2506.00054) but does not stop it. RAGTruth (ACL 2024) documents LLMs producing claims unsupported by, or contradicting, the very passages retrieved for them. Three failure modes survive RAG: *retrieval failure* (the right paper is never fetched), *synthesis hallucination* (the answer overstates what the retrieved text says), and *context misattribution* (a true fact bolted to the wrong source — the opening case again).

### 10.5.6 The regulatory surface: fair balance and the 2025 enforcement wave

Generated promotional content lands inside a regulated space. The FDA's fair-balance requirement holds that risk information must be presented with prominence and readability *reasonably comparable* to benefit information so the net impression is not misleading — it governs both content and presentation, and notably does *not* require equal length (FDA, *Presenting Risk Information in Prescription Drug and Medical Device Promotion*). A non-deterministic model can hallucinate an unsubstantiated efficacy claim, drift off-label, or generate benefit copy without proportionate risk language — precisely the fair-balance defect. Generated content must pass human MLR review, not bypass it (pharmaphorum [verify]).

This is not abstract. Following a September 9, 2025 enforcement push and an accompanying presidential memo, the FDA sharply escalated promotional enforcement — by various counts, on the order of sixty compliance letters in 2025 against roughly five before the September action, with priorities including omission of risk information and unsubstantiated claims (ProPharma; Morgan Lewis [counts approximate — vary by source and date; the *trend* is well corroborated]). Meanwhile promotional-material production volume rose roughly 29% year over year in the US in 2025 (Indegene [vendor-reported]) — which is exactly why automating content is tempting and exactly why the validation step cannot be the thing that gets cut.

### 10.5.7 The asymmetric-harm argument: why human review is load-bearing

Pull the failures together and a pattern emerges. Every *automated* control degrades in the same place — and that place is where the work matters most:

- Fluency raises confidence (10.5.2).
- Hallucination is highest in niche indications (10.5.5).
- The LLM-judge backstop is weakest in expert domains (10.5.5).
- RAG still lets synthesis errors through (10.5.5).
- Faithfulness metrics miss complex cases (10.5.8).
- The regulator is *actively* penalizing the resulting defect (10.5.6).

There is exactly one control positioned to catch what all the others miss: an expert who is *expected to distrust fluent output*. That is the asymmetric-harm argument, and it is why human review in this chapter is not a courtesy step at the end. It is the only reliable layer, and it has to be placed where automated confidence is highest and automated reliability is lowest — which is the same place.

### 10.5.8 Building the validation harness

The harness is the chapter's named Fellow artifact. It is a workflow, not a single tool, with four layers — each taught alongside its limits, because a control you trust blindly is just another fluency trap.

1. **Citation verification (non-negotiable).** Programmatically resolve *every* reference: does the work exist, is the DOI/PMID valid, and — critically — does the cited text actually support the claim made? This single layer catches both fabrications and "real-but-wrong" citations. It is the layer the *Mata* attorneys skipped.
2. **Groundedness / faithfulness scoring.** Decompose an answer into atomic claims and score the fraction supported by the retrieved context (e.g., the RAGAS faithfulness metric; docs at ragas.io). *Limit:* faithfulness scoring is moderately effective on simple queries and weak on complex ones — one benchmark reported it failing to score ~83.5% of examples (Cleanlab [config-specific]). It is a triage signal, not a pass/fail oracle.
3. **Compliance flag.** Screen generated content for fair-balance gaps, unsubstantiated efficacy language, and off-label drift, and *route flags to MLR/counsel* — never auto-approve. (This is the hook into Chapter 11's compliance-routing discipline.)
4. **Human-in-the-loop capstone.** The model does the mechanical pre-checks; the expert makes the judgment. By the time content reaches the human, the harness has done the tedious work — resolving references, scoring groundedness, surfacing flags — so the human's scarce attention goes to what only a human can decide: is this claim *true*, is the signal *real*, could the partner *defend* it to a regulator?

Dedicated hallucination detectors (RAGTruth-trained models, LettuceDetect, Luna; e.g., arXiv 2502.17125, 2406.00975) can sit alongside layer 2 as a complementary check. None of them replaces layer 4.

## 10.6 Worked example: scanning the point-of-care evidence base

**Process.** Return to the opening task — *what is the peer-reviewed evidence that point-of-care messaging lifts new starts?* — and do it with the harness.

1. *Generate the draft.* Prompt the LLM for candidate papers with full citations, instructing it to return only references it can attribute and to mark uncertainty. This produces, say, eight candidate citations.
2. *Verify citations (layer 1).* Resolve each against PubMed/Crossref. Two fail to resolve (fabricated — drop). One resolves but, on reading the abstract, studied patient adherence reminders, not physician promotion (misattributed — drop and note). Five survive.
3. *Score groundedness (layer 2).* For each surviving paper, check that the LLM's one-line summary matches the abstract's actual finding. One "showed significant lift" paper in fact reported a null result for the relevant subgroup — the summary overstated it. Correct the summary; flag the paper as null.
4. *Compliance flag (layer 3).* The draft summary phrased one finding as a benefit claim with no mention of the study's safety caveats — flag for fair-balance review if any of this language migrates toward promotional use.
5. *Human judgment (layer 4).* The Fellow reads the four genuinely relevant, correctly summarized papers and concludes: the *causal* evidence for point-of-care lift is thin and mostly observational — consistent with the evidence gap named in Chapter 5.

**Lesson.** The harness did not make the LLM trustworthy. It made the LLM *useful* — it turned a fluent-but-contaminated draft into a smaller, checked, honestly labeled evidence base in a fraction of the time a manual scan would take, while removing exactly the errors a fluent draft hides.

**Limit.** The harness cannot conjure evidence that does not exist. Its output here is partly a *negative* result — "the strong evidence you wanted isn't there" — which is itself a finding the lab values. It also cannot, on its own, judge whether the four surviving papers generalize to the partner's context; that is the human's call, and the AI Use Disclosure must say so.

## 10.7 Common misconceptions

- **"If the citation has a valid DOI, it's fine."** The most dangerous error is a real reference attached to a claim it does not support. A resolving link survives a casual check; only reading the source catches it.
- **"GPT-4-class models don't really hallucinate anymore."** They hallucinate *less*, and *most* in niche indications — the pharma sweet spot. Lower base rate, same catastrophic tail.
- **"I'll just have a second LLM check the first one."** LLM-as-judge is fine for triage and ranking; it is least reliable in expert domains and brings its own biases (position, verbosity, self-preference, sycophancy). It cannot sign off.
- **"RAG fixes hallucination."** It reduces it. Retrieval failure, synthesis overstatement, and misattribution all survive grounding.
- **"Faithfulness score above the threshold means it's verified."** Faithfulness metrics are weak on complex queries and are a triage signal, not proof. They do not replace reading the source.

## 10.8 Evidence check

- **Independent / peer-reviewed:** hallucination rates (JMIR 2024, e53164); topic-familiarity effect (PMC12658395 [verify]); LLM-as-judge baseline and biases (Zheng et al. 2023; arXiv 2410.21819, 2410.02736); RAG limits (RAGTruth, ACL 2024); the *Mata v. Avianca* sanction (court docket).
- **Vendor-reported (treat as directional):** MLR-acceleration and content-volume figures (Indegene, Vodori, Veeva); claims-library tooling capabilities.
- **Approximate / contested:** FDA 2025 enforcement counts (vary by counting method; the escalation trend is well corroborated); the "55%/18%" fabrication split (secondary summary — `[verify]`); "~45% of real citations have bibliographic errors" (`[verify primary]`).
- **Excluded as unverifiable:** several future-dated sources surfaced in scanning (2026-dated arXiv IDs and audits) were *not* relied on; the widely circulated "95% of generative-AI pilots fail" MIT figure is frequently mis-cited and is left `[verify]`.

## 10.9 Compliance and patient-welfare check

Generated promotional content is a live MLR/fair-balance surface: any benefit copy lacking proportionate risk language, any off-label drift, any unsubstantiated efficacy claim is flagged and **routed to medical/legal/regulatory counsel** — this chapter does not adjudicate the law, it models the flag. The patient-welfare stake is direct: a hallucinated efficacy claim that survives review can misinform a prescriber and, downstream, a patient. The harness's compliance layer exists precisely to keep AI speed from outrunning the safety step that protects the patient.

## 10.10 Exercises

1. **(Understand)** In your own words, distinguish a "useful draft" from a "trustworthy claim," and give one example of each from a commercial-research task.
2. **(Apply)** Take any LLM-generated literature summary (five+ citations). Resolve every citation; classify each as *valid-and-supported*, *real-but-misattributed*, or *fabricated*. Report the counts and the single most dangerous error you found.
3. **(Apply+)** Design the four-layer validation harness for a literature-scanning task in your domain. For each layer, name the tool/check, what it catches, and its documented limit.
4. **(Create / Part B — produce)** Build and run the validation harness for *your own research thread*: produce (a) a short LLM-generated evidence draft, (b) the harness output showing what was caught at each layer, and (c) a one-paragraph statement of which judgment in the workflow no AI could make for you.

## 10.11 Five-part AI exercise block

1. **When to use AI:** literature scanning, claims-to-evidence mapping, message-variant generation, mechanical MLR pre-checks — any task where a human can cheaply verify the output and a wrong draft is recoverable.
2. **When NOT to use AI:** as the final authority on whether a factual or promotional claim is true; as the sign-off on fair balance; for anything in a niche indication where you cannot independently verify the literature.
3. **LLM exercise:** prompt a model for "the peer-reviewed evidence that [your thread's intervention] works, with citations." Save the raw output verbatim before you check anything.
4. **CLI / code exercise:** write a script that takes the citation list from #3 and resolves each against Crossref/PubMed, returning exists / DOI-valid / abstract-matches-claim for each. This is layer 1 of your harness.
5. **AI-validation exercise:** for each surviving citation, read the actual abstract and grade whether the LLM's summary matches the finding. Tally how many "supported" claims were in fact overstated or null — this number *is* your fluency-trap exposure.

## 10.12 AI Use Disclosure (Part B)

Your disclosure for this chapter must name at least one judgment in your harness that the AI could not make: which claims are *truly* evidenced (not merely fluently asserted), whether the surviving signal is real, and whether the partner could defend the generated content to a regulator or an audit committee. Naming that judgment is the +5 Part B bonus criterion — and it is the whole point of the chapter.

## 10.13 What would change my mind

If a future model demonstrably resolved and *correctly attributed* citations at expert-reviewer reliability in niche indications — and if an independent, non-vendor benchmark confirmed it — then citation verification could shift from non-negotiable to spot-check. Today no such evidence exists; fabrication is *highest* exactly where verification matters most, so the harness stays.

## 10.14 Still puzzling

Faithfulness metrics fail most on the *complex* queries that matter most, and LLM judges fail most in *expert* domains that matter most. Both backstops degrade in the same direction as the task gets harder. Is there an automated check whose reliability *rises* with task difficulty, or is expert human review structurally the only control with that property? The book's working answer is the latter — but it is the chapter's genuinely open question.

## 10.15 Summary

You can now use an LLM as a research instrument without being captured by it. You can run literature scanning, claims mapping, and content triage through a four-layer harness that verifies every citation, scores groundedness, flags compliance risk, and routes the irreducible judgment to a human. You understand *why* human review is load-bearing — the asymmetric-harm argument — and you can name the fluency trap, automation bias, and the topic-familiarity effect that make fluent AI output most dangerous exactly where you want it most.

## 10.16 Key terms

- **Fluency trap** — the tendency to read confident, well-formed prose as accurate regardless of its actual correctness.
- **Useful draft vs. trustworthy claim** — the distinction between an LLM's fluent output and a claim verified against real, correctly attributed sources and cleared by expert review.
- **Hallucinated / misattributed citation** — a fabricated reference, or a real reference attached to a claim it does not support.
- **LLM-as-a-judge** — using one model to grade another's output; useful for triage, unreliable for sign-off, weakest in expert domains.
- **RAG (retrieval-augmented generation)** — grounding generation in retrieved passages; reduces but does not eliminate hallucination.
- **Faithfulness / groundedness score** — the fraction of an answer's atomic claims supported by retrieved context; a triage signal, not an oracle.
- **Fair balance** — the FDA requirement that risk information appear with prominence comparable to benefit information.
- **Validation harness** — the four-layer workflow (citation verification → groundedness → compliance flag → human capstone) separating useful draft from trustworthy claim.

## 10.17 Bridge

You now have a tool for turning research into checked, provenance-bearing drafts. But a tool is not a process. How does a Fellow turn this — and every other method in the toolkit — into a repeatable lab with a partner, where ideas get scored, compliance-flagged, and handed off or killed? That is the operating model of Chapter 11, and the place where the public-data/IP firewall becomes concrete.

## 10.18 Further reading

- Zheng, L., et al. (2023). *Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena.* NeurIPS 2023 (arXiv 2306.05685). The origin and the honest limits of LLM-as-judge.
- *Mata v. Avianca, Inc.*, No. 1:22-cv-01461 (S.D.N.Y. 2023), Dkt. 54. The cautionary tale: the failure was skipping verification, not using AI.
- JMIR (2024), e53164. Peer-reviewed measurement of fabricated-reference rates across model generations.
- Patel & Brown, *GIGO: A Crash Course in Data with LLMs* (`_lib_gigo-llm-toc.md`). Computational skepticism as the reliable defense; the GPT-4 hallucinated-legal-citation case.
- Mollick, E., *Co-Intelligence* (`_lib_co-intelligence.md`). The expert-in-the-loop / "centaur" posture behind the human-capstone layer.
- FDA, *Presenting Risk Information in Prescription Drug and Medical Device Promotion.* The fair-balance standard the compliance layer screens for.
