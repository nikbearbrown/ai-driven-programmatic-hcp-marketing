# Chapter 9 — Brand Association as a Measurable Outcome

## 1. Chapter overview

Chapter 8 measured lift — the short-run change in scripts. This chapter measures the thing underneath the scripts: durable brand association, the physician's standing mental rule that "for *this* kind of patient, Brand X is my default." That rule, not unaided recall of the name, is the strongest signal of pharma brand equity, and it is harder to measure than a campaign click. By the end of this chapter you will be able to explain the brand-formation loop and why the association node is where marketing content actually acts; operationalize association into measurable outcomes using both explicit instruments (surveys, conjoint/discrete-choice experiments) and computational ones (the Implicit Association Test, word-embedding association tests such as WEAT); design a study that detects whether a content variant shifts *durable* association rather than a transient recall bump, with a control and a delayed re-measurement; and reason honestly about two genuinely open questions this chapter refuses to settle — whether brand equity tracks clinical value, and whether the computational instruments are valid for a drug brand at all. This is the brand half of the book's lift-versus-brand spine, escalated from the definitions of Chapter 2 to the design of measurement.

## 2. Learning objectives

By the end of this chapter you will be able to:

1. **(Understand)** Explain the brand-formation loop and the strongest equity signal — the physician remembering the patient type, not the brand name.
2. **(Apply)** Operationalize association and quality-label outcomes (message association, perceived efficacy/safety, patient-archetype ownership, share of mind) into measurable designs.
3. **(Create / Part B)** Design a study testing whether a content variant shifts quality association — survey-based and/or embedding/implicit-association-based — with a control and a delayed post-test.
4. **(Evaluate)** Distinguish a durable association shift from a transient recall bump.

## 3. Opening case — the physician who praises the data but never switches

A physician tells a market-research interviewer, without hesitation, that Brand X has "the best efficacy data in the class." Ask the claims record a different question and you get a different answer: through three generic entries, this physician has not once switched a stable patient onto Brand X. The *stated* association — an efficacy belief, reported on demand — and the *behavioral* association — what the physician actually does at the moment of choice for a stable patient — point in opposite directions.

This is the chapter's whole problem in one person. Which association is real? The survey answer is cheap to give and may reflect a remembered talking point rather than a decision rule. The behavior is expensive and revealing, but it is downstream of formulary, habit, and patient mix as well as belief. If a brand team had measured only the survey, it would have booked equity that does not exist. If it had measured only the scripts, it would have missed a belief that might convert a *new* patient even though it never moves a stable one. Measuring durable quality association means designing instruments that can tell these apart — and knowing which instruments are trustworthy. That is what the rest of the chapter builds.

## 4. Core sections

### 4.1 Pharma brand equity is remembering the patient type

The strongest equity signal in pharma is not unaided recall of "Brand X." It is a durable mental rule (grounded in `pantry/pharma-brand-measurement-synthesis.md` §3, §5):

> For this patient profile, in this disease state, after this prior therapy, Brand X is my default.

This is more constrained than the consumer-goods identity statement "I wear Calvin Klein," and far more valuable, because it predicts repeat prescribing at the exact moment of choice. The pharma brand funnel is not awareness → purchase → loyalty; it is awareness → clinical belief → trial → prescribing habit → patient persistence, with the buyer, user, payer, and decision-maker split across physician, patient, insurer, and institution. Consumer-goods brand theory (mental availability, salience, reach) applies to the salience layer but not to the clinical gates — label, guidelines, payer access, prior authorization, risk tolerance — that govern whether a remembered preference becomes a prescription.

### 4.2 The brand-formation loop: where content acts

Brand association is the load-bearing node in a longer loop (synthesis §3): clinical evidence and label → KOL interpretation and guideline discussion → detailing, CME, and congress presence → **HCP mental association ("Brand X is for this kind of patient")** → first patient trial → observed outcome and access experience → repeat prescribing or abandonment → habit, loyalty, advocacy, or switching. Everything downstream of the association node — NBRx, loyalty deciles, persistence — is a *behavioral consequence* of the association. Marketing content acts *at* the association node. That is exactly why this is the outcome to measure when you want to know whether content built equity: the scripts are the lagging proof, but the association is the mechanism.

There is independent evidence that promotion is associated with prescribing — a systematic review in *Annals of Internal Medicine* found industry payments associated with increased prescribing of the paying company's drug and more branded prescribing, and a *JAMA Internal Medicine* study linked payments to higher brand-name statin prescribing `[verify both citations against primary sources]`. The evidence is stronger for association and behavioral influence than for clean causal proof of brand-identity formation — which is the gap this chapter's measurement designs are meant to narrow.

### 4.3 The attitudinal toolkit: what HCPs say

The explicit, self-report layer is the workhorse of commercial brand tracking. The standard battery (synthesis §1):

- **Unaided (spontaneous) recall** — names the brand without prompting; indexes top-of-mind salience.
- **Aided awareness** — recognizes the brand when prompted. The unaided→aided gap signals how much exposure is needed to embed the brand.
- **Favorability, familiarity, message association, perceived efficacy/safety, prescribing intent, NPS-style advocacy, share of mind** — the custom-survey and syndicated-panel staples (Kantar-, Ipsos-, M3/Medscape-, IQVIA/DRG-style trackers).
- **Patient-selection criteria** — notable because launch trackers already capture "for which patient." This *is* the thesis construct — the patient-type rule — already living inside commercial trackers.

Two honesty notes. Attitudinal measures are self-reported and can overstate actual prescribing — the opening-case physician is the warning. And "share of mind," while ubiquitous in industry, has no citable academic formula; flag it as an industry term, not a standardized construct `[verify any precise proprietary tracker formula]`.

### 4.4 Two paradigms: explicit and implicit

The chapter contrasts two ways of measuring association.

**Explicit / attitudinal** — surveys and conjoint — capture what HCPs *say*. The most rigorous explicit instrument is the **conjoint or discrete-choice experiment (DCE)**, governed by ISPOR good-research-practice standards. By presenting physicians with profiles that vary attributes — efficacy, safety, dosing, cost, reimbursement — and including *brand name as an attribute alongside identical clinical specs*, a DCE isolates the **pure brand premium**: the utility a physician assigns to the name net of efficacy and safety. A 2024–2025 DCE of roughly 1,047 Chinese physicians did exactly this for brand-name versus certified-generic prescribing `[verify the brand part-worth magnitude against the primary source, PMC11806230]`.

**Implicit / computational** — the Implicit Association Test (IAT) and word-embedding association — aim at automatic associations a physician may not self-report. The pedagogical payoff is that these can diverge from the explicit measures: a content variant might shift *implicit* association before (or without) shifting survey answers, and might shift recall transiently without shifting durable association at all. Designing both instruments for the same association, then predicting where they will diverge, is the sharpest exercise in this chapter.

### 4.5 The computational instruments — and their contested validity

**The Implicit Association Test (IAT).** Greenwald, McGhee, and Schwartz (1998) introduced reaction-time sorting as an index of automatic associations below survey-reportable awareness. It is the substrate for "implicit brand attitude" claims. But its predictive validity is genuinely contested, and this chapter teaches that fight honestly rather than adopting the instrument as an oracle. Greenwald et al.'s 2009 meta-analysis (122 reports, ~14,900 subjects) reported a mean predictive correlation of about $r \approx .274$; Oswald et al. (2013) found much weaker prediction, an aggregate around $r \approx .148$ and as low as ~$.07$ for some microbehaviors with confidence intervals spanning zero — no better than explicit measures — and test-retest reliability is mediocre (~$r \approx .5$ in adults) `[verify effect sizes against primary PDFs]`. Treat the IAT as "a popular instrument with a real validity fight," not as proof.

There is a sharper gap specific to this book's construct. The IAT is heavily used in healthcare to measure *clinician implicit bias toward patient groups* — a systematic review (FitzGerald & Hurst, 2017) found 15 of 17 HCP-bias studies used it — but **no published study uses an IAT to measure a physician's implicit attitude toward a specific drug brand.** That is a genuine gap, and it is flagged as an open question here, not asserted as a result [open question — see pantry §G].

**Word-embedding association (WEAT).** The Word-Embedding Association Test (Caliskan, Bryson & Narayanan, 2017, *Science*) is "an IAT you run on text": it measures the differential cosine similarity between target word sets and attribute sets, and Caliskan et al. showed embeddings reproduce human IAT associations. Biomedical embeddings are a plausible substrate — word2vec trained on roughly 16 million PubMed abstracts has recovered drug–disease relations via cosine similarity, validated against MeSH and DrugBank `[verify, PMC8519453]`. You can therefore *propose* a brand-association WEAT: let X = Brand X tokens, Y = competitor tokens, A = patient-archetype descriptors, B = other patients, over a CME or clinical-literature corpus; the differential cosine association becomes a computational measure of "Brand X is for THIS patient." Critically, this is a **proposal built from component-wise validated parts, not an existing cited result.** No published brand-versus-patient-archetype WEAT on CME text exists. Present it as a design to test, not a finding to cite [open question — see pantry §G].

### 4.6 Durable versus transient: the measurement that separates them

The single methodological lesson of this chapter: one post-exposure survey cannot tell durable association from a transient bump. The persistence literature (Haugtvedt & Petty) shows that high-elaboration, central-route attitude change persists while peripheral-route change — driven by repetition or a credible source rather than deep processing — decays toward baseline `[verify Haugtvedt & Petty citation]`. Mere-exposure effects (Zajonc) build favorability through repetition but are not uniformly durable. So a campaign that produces an immediate spike in aided recall and favorability may have built nothing lasting.

The design implication is concrete: you need a **delayed re-measurement and a decay curve**, not a single post-test. Durable association shows a roughly flat decay curve across a delayed post-test; transient association shows an immediate bump decaying to baseline. Without the delayed measurement, the two are indistinguishable — and brand teams routinely book the bump as equity.

## 5. Worked example — designing an association instrument

**Process.** Take a content variant — say, a CME-style piece framing Brand X around a specific patient archetype — and design a study to test whether it shifts *durable* quality association. Build it on three pillars. (1) **A control:** randomize physicians to the variant or to a neutral control content, so any association shift is measured against a comparable group (this is the brand-side analog of Chapter 8's holdout — a favorability shift without a control is a lift claim without a holdout). (2) **Two instruments for the same construct:** an explicit measure (a short DCE or survey isolating the patient-type association and the brand premium) and a computational measure (a WEAT-style cosine association on a corpus the physicians engaged with, *flagged as exploratory*). (3) **A delayed post-test:** measure immediately after exposure *and* after a defined delay, and plot the decay curve.

**Lesson.** This design — control, dual instruments, delayed re-measurement — is the reusable **association instrument** the chapter trains. It can detect the four outcomes that a one-shot survey collapses into one: durable explicit shift, transient explicit bump, implicit shift without explicit shift, and no shift at all. Predicting *where* the explicit and implicit measures diverge is itself a finding about how the content worked (central versus peripheral route).

**Limit.** Every instrument here has a soft floor. The DCE measures stated choice, not actual prescribing, and is subject to hypothetical bias. The WEAT rests on the embedding corpus and on a method whose application to a drug brand is unvalidated — a cosine number is a signal, not ground truth. The IAT's predictive validity is contested. And the decay curve needs enough delay and enough physicians to distinguish a flat line from a slow decline. The honest readout names the durability question it answered and the validity caveats it could not resolve.

## 6. Common misconceptions

- **"Brand equity equals awareness."** The strongest pharma equity is the durable patient-type rule, which is behavioral and durable — not a recall score.
- **"A favorability spike right after the campaign proves equity was built."** One post-exposure measurement cannot distinguish durable central-route change from a decaying peripheral bump; you need a delayed re-test.
- **"The physician's stated efficacy belief is their real association."** Stated and behavioral association can diverge sharply — the opening case is the proof.
- **"An IAT or WEAT result is objective ground truth."** Both are signals with contested or unvalidated status for this use; treat a cosine or a reaction-time difference as evidence to weigh, not proof.
- **"A brand-association study doesn't need a control."** It does, for the same reason a lift study does — a shift measured without a comparison group is uninterpretable.
- **"Brand equity must track clinical value."** Whether it does is an open empirical question, not a given (Section 7).

## 7. Evidence check and Compliance and welfare check

**Evidence check.** *Independent / settled:* the brand-formation loop and the attitudinal toolkit (grounded in the pharma brand-measurement synthesis); the mechanics of conjoint/DCE (ISPOR practices); the IAT mechanism (Greenwald et al. 1998); and the WEAT method (Caliskan et al. 2017) are established. *Contested:* the IAT's predictive validity is sharply disputed (Greenwald 2009 ~$.274$ versus Oswald 2013 ~$.148$), and "md-IAT valid for brands" rests largely on proponents/vendors `[contested — see pantry]`. *Open questions, not findings — flagged, not asserted:* (1) **no published IAT measures physician implicit attitude toward a drug brand**; (2) **no published brand-versus-patient-archetype WEAT on CME text exists** — it is a proposal built from validated components; (3) **no study correlates brand equity with ICER clinical-value score** — existing evidence links *price* (not equity) to value, and shows divergence (Wouters et al. 2021 found net prices exceeded the $100k/QALY value-based price for ~81% of drugs) `[verify all three as open per pantry §G]`. *Vendor-generated:* tracker construct *definitions* are reliable; proprietary formulas and "share of mind" lack a citable academic standard.

**Compliance and welfare check.** This is where the book's patient-welfare gate becomes measurable. The central tension (synthesis §6): brand equity can look commercially successful while being socially inefficient if it preserves use of a higher-priced brand where a clinically equivalent cheaper option exists. The high-impact open question — **does brand equity predict prescribing persistence after controlling for ICER clinical-value score?** — *is* the welfare check in measurable form. An uncorrelated finding would say the durable association the industry optimizes is commercial memory, not clinical value [brand-equity-vs-clinical-value: open empirical question — see pantry §G; ICER threshold ranges are ICER's stated values, themselves contested in health economics]. On compliance: any HCP-facing content tested here is subject to MLR review and FDA fair-balance requirements, and an instrument that measures "perceived efficacy" must not itself become a vehicle for off-label or unbalanced framing. Implicit-measurement of clinician attitudes also carries its own ethical weight — the IAT literature in healthcare is about *bias toward patients*, and repurposing it toward brand persuasion deserves explicit scrutiny. Flag for medical, legal, and regulatory review; the Fellow does not adjudicate.

## 8. Exercises

1. **(Understand)** Explain why a single post-exposure favorability survey cannot distinguish a durable association shift from a transient recall bump, and state the one design element that resolves it.
2. **(Apply)** Take the opening-case physician (praises the data, never switches a stable patient). Specify two measurements — one explicit, one behavioral — that would reveal the divergence, and state what each one would and would not tell you.
3. **(Apply+ / Create / Part B)** For your own research thread, design an **association instrument**: a content-variant study with a control, an explicit measure and a computational measure of the *same* association, and a delayed post-test. Predict where the two instruments will diverge and why.
4. **(Produce)** Draft a one-page proposal for the brand-equity-versus-ICER study (Chapter 13, Track B): the hypothesis, the public datasets (Open Payments, Part D, ICER), the outcome, and — explicitly — why a null result would be a high-impact finding. Label every uncertain construct as open per the evidence check.

## 9. Five-part AI block

**When to use AI here.** Use an LLM to draft survey and DCE items, to build a WEAT pipeline (assemble word sets, compute cosine associations) on a CME/literature corpus, and to summarize the IAT validity debate so you know which papers to read.

**When NOT to use AI here.** Do not let an LLM declare an association "durable," "real," or "validated." It will treat a WEAT cosine or an IAT score as ground truth, and it cannot tell you whether the instrument is valid for a drug brand — the very thing this chapter flags as unestablished. It will also fabricate a citation for a "brand IAT study" that does not exist; that gap is real and must be preserved, not papered over.

**LLM exercise.** Prompt an LLM to "find published studies measuring physician implicit attitudes toward a specific drug brand using an IAT." Then verify: the honest answer is that none exist. Treat any citation it returns as a hallucination to be checked against PubMed — this is a live demonstration of the fluency trap.

**CLI exercise.** Using biomedical word embeddings (or a corpus you embed), compute a WEAT-style differential cosine association between a brand token set and a patient-archetype attribute set versus a competitor. Report the number *with* the caveat that the method's application to a drug brand is unvalidated.

**AI validation.** For three claims an LLM makes about IAT or WEAT validity, locate the primary source and confirm or correct the effect size and the strength of the claim. Log whether the model overstated validity (a common failure) and correct it.

## 10. AI Use Disclosure

If you used an LLM, disclose where, and name the judgment it could not make: *whether a measured association is durable and clinically meaningful, and whether the instrument is valid for a drug brand at all.* Those calls require reading the contested validity literature and confronting the three flagged gaps — work the model cannot do for you and will, if unchecked, paper over.

## 11. What would change my mind

The chapter holds three positions open rather than asserting them, so what would change my mind is symmetrical with what would *close* each open question. (1) On the brand IAT gap: a published, peer-reviewed study measuring physician implicit attitudes toward a specific drug brand with adequate reliability would convert the gap into a method. (2) On the WEAT construct: a validated brand-versus-patient-archetype WEAT, benchmarked against behavioral prescribing, would move it from proposal to instrument. (3) On brand-equity-versus-clinical-value: a well-identified study showing durable equity *does* track ICER value would refute the "commercial memory, not clinical value" worry; a null would confirm it. The stance is evidence-first — these are flagged as open precisely so the evidence, when it arrives, can settle them.

## 12. Still puzzling

The deepest puzzle is whether durable brand association and clinical value are even correlated. The evidence we have links *price* to ICER value and finds frequent divergence, but no one has tested whether the *equity* — the physician's patient-type rule — tracks value once clinical score is controlled. If it does not, then the most valuable asset in pharma marketing is, by construction, partly decoupled from patient benefit. That is not an indictment; it is an untested, testable, and consequential claim — exactly the kind a Fellow can put on public data.

## 13. Summary

You can now explain why pharma brand equity is the physician's durable patient-type rule rather than name recall, and why the association node is where content acts in the brand-formation loop. You can operationalize association with explicit instruments (surveys, conjoint/DCE isolating the brand premium) and computational ones (IAT, WEAT), and you can reason honestly about their contested or unestablished validity. You can design an association instrument — control, dual instruments, delayed post-test — that separates durable shift from transient bump, the chapter's core measurement skill. And you can name the three open questions this chapter refuses to settle, holding them as flagged agenda items rather than assertions. The brand half of the spine is now measurable. The next chapters turn the toolkit you have built — ensembles, MoE audits, uplift, brand instruments — into a repeatable lab.

## 14. Key terms

- **Brand equity (pharma):** the durable mental rule that for a given patient type, Brand X is the physician's default — the strongest equity signal.
- **Brand-formation loop:** evidence → KOL/guidelines → detailing/CME → HCP association → trial → outcome → repeat/abandon → habit/loyalty, with content acting at the association node.
- **Attitudinal toolkit:** unaided/aided awareness, favorability, message association, perceived efficacy/safety, prescribing intent, share of mind — self-reported and prone to overstatement.
- **Conjoint / discrete-choice experiment (DCE):** an explicit choice task that, by including brand as an attribute over identical clinical specs, isolates the pure brand premium.
- **Implicit Association Test (IAT):** a reaction-time measure of automatic associations; widely used, predictive validity contested; no published drug-brand application.
- **WEAT (word-embedding association test):** "an IAT on text," measuring differential cosine association between word sets; a validated method whose brand-archetype application is a proposal, not a result.
- **Durable vs. transient association:** durable shows a flat decay curve on delayed re-test; transient bumps then decays — distinguishable only with a delayed measurement.
- **Brand-equity-vs-ICER question:** the open, testable question of whether durable equity tracks clinical value after controlling for ICER score — the welfare check in measurable form.

## 15. Bridge

You now hold the full toolkit: a baseline ensemble, an audit for routing-model claims, an incrementality design, and an instrument for durable association. Much of the work each one requires — scanning literature, mapping claims to evidence, mining CME corpora, drafting instruments — invites a large language model. The next chapter asks the question that governs all of it: where do LLMs genuinely help a Fellow's research, and where do they fluently lie? We will start, fittingly, with an LLM "evidence summary" that cites a study which does not say what it claims.

## 16. Further reading

- Greenwald, A. G., McGhee, D. E., & Schwartz, J. L. K. (1998). *Measuring individual differences in implicit cognition: The Implicit Association Test.* The IAT's origin. `[verify cite]`
- Oswald, F. L., et al. (2013). *Predicting ethnic and racial discrimination: A meta-analysis of IAT criterion studies.* The skeptical counterweight on IAT predictive validity. `[verify cite]`
- Caliskan, A., Bryson, J. J., & Narayanan, A. (2017). *Semantics derived automatically from language corpora contain human-like biases.* Science. The WEAT method. `[verify cite]`
- FitzGerald, C., & Hurst, S. (2017). *Implicit bias in healthcare professionals: a systematic review.* BMC Medical Ethics. Establishes the IAT's heavy use for clinician–patient bias and the absence of brand applications. `[verify cite]`
- ICER. *Value Assessment Framework — cost-effectiveness, the QALY, and the evLYG.* The clinical-value benchmark for the brand-equity-vs-value question; threshold ranges are ICER's stated values. `[verify]`
- `pantry/pharma-brand-measurement-synthesis.md` — the in-pantry synthesis this chapter restructures (NBRx, loyalty deciles, the brand-formation loop, the patient-welfare gap), plus the open-question flags in the Chapter 9 notes §G.

---

## Prompts

*No figures have been generated for this chapter yet.*
*Run the Cowork enrichment pass to populate this section.*
