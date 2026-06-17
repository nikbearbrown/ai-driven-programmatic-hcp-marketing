# Chapter 9 — Brand Association as a Measurable Outcome
*Why the physician who praises your data and never prescribes your drug is the most important measurement problem in pharma marketing.*

A physician tells a market-research interviewer, without hesitation, that Brand X has the best efficacy data in the class. No hedging. No uncertainty. The best data. Then you pull her claims record and find that through three generic entries — three opportunities to act on that stated belief — she has not once switched a stable patient onto Brand X.

Which one is real?

This is not a trick question, and it is not a story about a physician who is lying. She may believe every word she said. The stated association — an efficacy belief, reported on demand — and the behavioral association — what she actually does at the moment of choice for a stable patient — are measuring two different things. One is a recalled talking point. The other is a decision rule. They can point in opposite directions, and they frequently do, and if your brand measurement does not account for the difference, you will book equity that does not exist.

That gap is what this chapter is about. Not brand awareness. Not favorability scores. The gap between what a physician says and what that physician does — and the instruments capable of telling them apart.

---

The strongest pharma brand equity signal is not unaided recall of the name. It is a durable mental rule, something like: *for this patient profile, in this disease state, after this prior therapy, Brand X is my default.*

That rule is more constrained than the consumer-goods identity statement "I wear Calvin Klein." It is also far more valuable, because it predicts repeat prescribing at the exact moment of clinical choice — not in a survey room, but at the point where the physician opens a chart, reads the diagnosis, and reaches for a pen. The consumer-goods brand funnel — awareness, consideration, purchase, loyalty — does not describe this. The clinical gates between a remembered preference and a written prescription include label, guidelines, formulary access, prior authorization, the patient's insurance tier, and the physician's risk tolerance. Mental availability is necessary but nowhere near sufficient.

So the thesis construct for this chapter is specific: not "does the physician know Brand X" but "does the physician have a durable patient-type rule that places Brand X as the default for a describable patient." That rule — when it exists, when it is stable, when it persists after exposure ends — is brand equity worth measuring. Everything downstream of it: new-to-brand scripts, loyalty deciles, persistence curves — those are behavioral consequences of the rule. Marketing content acts *at* the rule. If you want to know whether content built equity, measure the rule.

<!-- → [DIAGRAM: The brand-formation loop as a chain — clinical evidence + label → KOL interpretation + guideline discussion → detailing, CME, congress → HCP mental association ("Brand X is for this kind of patient") → first patient trial → observed outcome + access experience → repeat prescribing or abandonment → habit/loyalty/advocacy or switching. Arrow annotation at the association node: "Marketing content acts here." Arrow annotation at NBRx and loyalty: "Behavioral consequences of the rule." Caption: "The association node is the mechanism. Scripts are the lagging proof."] -->

There is independent evidence that promotion is associated with prescribing — a systematic review in the *Annals of Internal Medicine* found industry payments associated with increased prescribing of the paying company's drug and more branded prescribing, and a *JAMA Internal Medicine* study linked payments to higher brand-name statin prescribing. [verify both citations against primary sources.] The evidence is stronger for association and behavioral influence than for clean causal proof of brand-identity formation. That gap is exactly what this chapter's measurement designs are built to narrow.

---

The explicit, self-report layer is the workhorse of commercial brand tracking, and it is worth knowing precisely what it measures and what it does not.

The standard battery runs from simple to complex. **Unaided recall** — name a brand in this class without prompting — indexes top-of-mind salience. **Aided awareness** — do you recognize this name — fills in the floor. The gap between them tells you how much exposure is needed to embed the brand. Then the more interesting measures: favorability, message association ("this brand is associated with reducing cardiovascular risk"), perceived efficacy and safety, prescribing intent, a net-promoter-style advocacy question, and **share of mind** — the estimated fraction of mental real estate in a given category this brand occupies relative to competitors.

Share of mind is ubiquitous in industry and has no citable academic formula. It is an industry term, not a standardized psychometric construct. [verify any precise proprietary tracker formula before citing it as a standard.] The same caveat applies to proprietary tracker instruments from Kantar, Ipsos, M3/Medscape, and IQVIA/DRG: the construct definitions are reliable; the specific computational formulas are proprietary and not externally validated.

One measure in the standard battery is notably precise: **patient-selection criteria** — "for which patient type would you consider this brand." Launch trackers already capture this. It is the thesis construct — the patient-type rule — already living inside commercial measurement. If you want to test whether content shifted the durable association, patient-selection criteria is the explicit instrument to reach for, because it asks directly about the decision rule rather than the name recognition.

The honesty problem with all of these measures is the one the opening case demonstrates. Self-report is cheap. A physician who has heard the efficacy message in twelve detailing calls can reproduce it fluently without ever having built the behavioral habit it is supposed to predict. The question is not whether the survey is capturing something real — it is — but whether that something is the patient-type rule or a remembered talking point. Those can correlate. They can also diverge, as they did in the opening case, and your measurement design needs to be able to tell which one you measured.

---

The instrumental contrast that organizes this chapter is between **explicit** and **implicit** measurement — what physicians say versus the automatic associations they may not be able to report.

The explicit route, taken to its rigorous limit, is the **conjoint or discrete-choice experiment**. Rather than asking a physician what they think of Brand X directly, you present a series of forced choices between physician profiles — drugs described by attributes that vary systematically: efficacy, safety, dosing, cost, reimbursement tier — and you include **brand name as one attribute alongside otherwise identical clinical specifications**. The physician chooses between profiles; the pattern of choices, analyzed by the conjoint model, yields a **part-worth** for each attribute — including the brand name. That part-worth is the pure brand premium: the utility the physician assigns to the name net of the clinical attributes you have held constant.

This is the most rigorous explicit instrument available. It is governed by ISPOR good-research-practice standards for preference studies. It forces an actual trade-off rather than a direct rating. And because brand name varies independently of clinical specs, the premium it estimates is not contaminated by the physician's beliefs about efficacy — it is separated from them by design. A recent discrete-choice study of approximately 1,047 Chinese physicians did exactly this for brand-name versus certified-generic prescribing, isolating the brand part-worth from clinical attributes. [verify the brand part-worth magnitude against the primary source, PMC11806230.]

<!-- → [TABLE: Comparison of explicit measurement instruments. Columns: instrument, what it measures, key strength, key limitation, pharma applicability. Rows: unaided recall (top-of-mind salience; simple, fast; shallow — a recalled talking point, not a decision rule; awareness tracking), aided awareness (recognition; floor measure; minimal diagnostics; same), patient-selection criteria (the patient-type rule; direct construct hit; self-report susceptibility; launch and equity tracking), conjoint/DCE (pure brand premium via forced trade-off; separates name from clinical attributes; expensive, hypothetical bias; brand equity measurement).] -->

The implicit route is more interesting and more contested. The **Implicit Association Test** — Greenwald, McGhee, and Schwartz, 1998 — measures reaction-time latency in a sorting task. The logic: if two concepts are strongly associated in memory, sorting them into the same category is faster than sorting them apart. A positive brand IAT would pair the brand name with positive attributes and a competitor with negative ones, and measure whether the pairing congruent with that association is faster. The result is an index of automatic association that the physician may not self-report.

The IAT's predictive validity is genuinely contested and this chapter teaches that fight rather than adopting the instrument as an oracle. Greenwald et al.'s 2009 meta-analysis of 122 reports found a mean predictive correlation of approximately $r \approx .274$. Oswald et al. (2013) found much weaker prediction — an aggregate around $r \approx .148$, as low as approximately $.07$ for some microbehaviors, with confidence intervals spanning zero — no better than explicit measures — and test-retest reliability is mediocre, around $r \approx .5$ in adults. [verify these effect sizes against primary PDFs.] The honest position is that the IAT is a popular instrument with a real validity fight, not a resolved one.

There is a sharper gap specific to this book's use case. The IAT is heavily used in healthcare to measure clinician implicit bias toward patient groups — a systematic review by FitzGerald and Hurst (2017) found 15 of 17 HCP-bias studies used it — but **no published study uses an IAT to measure a physician's implicit attitude toward a specific drug brand.** [verify this gap holds against current PubMed; open question — see pantry §G.] That is not a minor caveat. The brand-IAT is a plausible instrument built by analogy to a validated application. Whether it produces stable, valid results for a drug brand is unknown. Treat any brand-IAT output as exploratory signal, not ground truth.

---

The computational instrument that sits alongside the IAT is both more tractable and more transparently limited.

The **Word-Embedding Association Test** (WEAT — Caliskan, Bryson, and Narayanan, *Science*, 2017) is, in essence, an IAT run on text. It measures the differential cosine similarity between target word sets and attribute word sets in a trained embedding space. Caliskan et al. showed that embeddings trained on large text corpora reproduce human IAT associations with striking fidelity — the biases in the data become biases in the geometry. The method is validated: the question is what corpus you run it on and what target-attribute pairing you choose.

For a pharma application, the proposal is concrete. Let the target sets be Brand X tokens and competitor tokens. Let the attribute sets be patient-archetype descriptors for the physician's target patient type and descriptors for other patient types. Run the WEAT over a corpus of CME content, journal abstracts, or clinical-platform text. The differential cosine association becomes a computational estimate of "Brand X is associated with this patient type more than the competitor is." Biomedical embeddings have real substrate: word2vec trained on approximately 16 million PubMed abstracts has recovered drug-disease relations via cosine similarity, validated against MeSH and DrugBank. [verify PMC8519453.]

The critical honesty note is this: that substrate validation does not validate the brand-archetype application. The drug-disease cosine result shows that semantic proximity in biomedical text maps onto documented pharmacological relationships. Whether it maps onto physician decision rules — whether the WEAT over a CME corpus predicts what the physician will actually prescribe — is a different question, and no published study has tested it. **The brand-versus-patient-archetype WEAT is a proposal built from validated component parts, not an existing cited result.** [open question — see pantry §G.] A cosine number from this pipeline is a signal to be interpreted, not ground truth to be reported.

<!-- → [DIAGRAM: WEAT setup schematic. Four labeled boxes: Target Set X (Brand X tokens), Target Set Y (competitor tokens), Attribute Set A (patient-archetype descriptors for target patient), Attribute Set B (other patient descriptors). Arrows showing cosine similarity computation between each target and each attribute set. Formula: WEAT score = mean_sim(X, A) − mean_sim(X, B) − [mean_sim(Y, A) − mean_sim(Y, B)]. Caption: "A positive WEAT score indicates Brand X is more associated with the target patient archetype than the competitor. Whether this predicts prescribing is an open question this design would test."] -->

The pedagogical payoff of running both instruments — the DCE and the WEAT — on the same association construct is that they can diverge. A content variant might shift implicit association in the embedding space before shifting DCE part-worths. It might shift explicit patient-selection survey responses without shifting the WEAT at all. Where the instruments agree, you have convergent evidence. Where they diverge, you have a finding about *how* the content worked — whether it changed automatic associations or deliberate clinical preference or neither.

---

The methodological lesson that ties the chapter together is about time.

A single post-exposure measurement cannot distinguish durable association from a transient recall bump. The persistence literature shows that high-elaboration, central-route attitude change — the kind produced by content that genuinely engages the physician's clinical reasoning — persists over time. Peripheral-route change, driven by repetition or source credibility rather than deep processing, decays toward baseline. [verify Haugtvedt and Petty on elaboration and persistence.] Mere-exposure effects build favorability through repetition, but they are not uniformly durable.

A campaign that produces an immediate spike in aided recall and favorability may have built nothing lasting. Brand teams routinely book that spike as equity. The design implication is concrete: you need a **decay curve**, not a single post-test. Measure immediately after exposure, then again after a defined delay — two weeks, four weeks, long enough for peripheral effects to decay. Durable association shows a roughly flat line across both measurements. Transient association shows a bump at the first measurement and a return toward baseline at the second. Without the second measurement, the two patterns look identical.

<!-- → [CHART: Two-line decay chart over three time points (pre-exposure, immediate post, delayed post). Line 1 (durable central-route shift): rises from pre to immediate post, holds flat to delayed post. Line 2 (transient peripheral bump): rises from pre to immediate post, drops back toward pre at delayed post. Both lines start at the same pre-exposure level. Caption: "Only the delayed re-measurement separates durable equity from a recall bump. One post-test cannot distinguish these patterns."] -->

---

Put the pieces together and the study design is clear. Take a content variant — a CME-style piece framing Brand X around a specific patient archetype. Randomize physicians to the variant or to a neutral control. This is the brand-side analog of Chapter 8's holdout: a favorability shift without a control group is as uninterpretable as a script lift without one. Then measure the association three ways. An explicit patient-selection survey or DCE, asking directly whether Brand X belongs with the target patient type. A computational WEAT-style association on the corpus the physicians engaged with, clearly flagged as exploratory. And a delayed post-test, measuring both again after a defined interval.

The study produces four distinguishable outcomes that a one-shot survey collapses into one: a durable explicit shift, a transient explicit bump, an implicit shift without an explicit shift, and no shift at all. Predicting in advance where the explicit and implicit measures will diverge is itself a hypothesis about how the content worked — about whether it engaged central processing or peripheral, about whether the brand-archetype association lives in deliberate clinical reasoning or in automatic association that the physician cannot self-report.

The limit is honest. The DCE measures stated choice, not actual prescribing, and is subject to hypothetical bias. The WEAT rests on a method whose application to a drug brand is unvalidated; a cosine number is a signal, not ground truth. The IAT's predictive validity is contested. The decay curve needs enough physicians and enough delay to distinguish a flat line from a slow decline that the sample size cannot detect. The honest readout names the durability question the design answers and the validity caveats it cannot resolve.

---

There is a deeper open question this chapter holds without settling, because the data to settle it does not yet exist.

Brand equity can look commercially successful while being socially inefficient. If the durable patient-type rule that the industry optimizes — "Brand X for this patient" — is decoupled from the ICER clinical-value score for Brand X, then the most valuable asset in pharma marketing is, by construction, partly commercial memory rather than clinical signal. The evidence we have links *price* to ICER value and finds frequent divergence: a Wouters et al. (2021) analysis found net prices exceeded the $100,000 per QALY value-based benchmark for approximately 81% of drugs assessed. [verify.] But no study has tested whether the *equity* — the physician's durable patient-type rule — tracks clinical value after controlling for ICER score.

That is not an indictment. A durable brand association might track clinical value perfectly — physicians might be building the patient-type rule from genuine efficacy and safety evidence, and the ICER alignment might hold. Or it might not. The question is empirically open, publicly testable with existing data (Open Payments, Part D, ICER assessments), and consequential enough that the honest position is to name it rather than assume either answer.

The opening-case physician, who praises the data and never switches a stable patient, is a single anecdote. The question is whether she represents a failure of brand building or a success — whether the stated association failed to convert because it was superficial, or because the formulary blocked her, or because her stable patients genuinely were not the right profile. Measurement cannot answer that question with one person. It can answer it at scale, with the right instruments and a control group and a delayed post-test. That is what the association instrument the chapter built is designed to do.

**Five-part AI exercise block**

**When to use AI here.** Use an LLM to draft survey items and DCE profiles, to build a WEAT pipeline (assemble word sets, compute cosine associations on a corpus), and to summarize the IAT validity debate so you know which papers to read first.

**When NOT to use AI here.** Do not let an LLM declare an association "durable," "real," or "validated." It will treat a WEAT cosine or an IAT score as ground truth. It will also fabricate a citation for a "brand IAT study" that does not exist — the gap is real and must be preserved, not papered over. And it cannot tell you whether the instrument is valid for a drug brand, which is the central open question of this chapter.

**LLM exercise (copy-paste prompt):**
> "Find published studies measuring physician implicit attitudes toward a specific drug brand using an Implicit Association Test. List the citations with authors, journal, and year." Then go to PubMed and verify each citation it returns. The honest answer is that no such studies exist. Treat any citation the model produces as a hallucination to be checked — this is a live demonstration of the fluency trap applied to a real gap in the literature.

**CLI exercise.** Using biomedical word embeddings (or a corpus you embed), compute a WEAT-style differential cosine association between a brand token set and a patient-archetype attribute set versus a competitor. Report the result with the explicit caveat that the method's application to a drug brand is unvalidated and the cosine number is exploratory signal, not ground truth.

**AI validation.** For three claims an LLM makes about IAT or WEAT validity, locate the primary source and confirm or correct the effect size and the strength of the claim. Log whether the model overstated validity — a common failure — and write one sentence correcting each overstatement.

## AI Use Disclosure

*Write two sentences naming what an AI tool did in your work for this chapter and the one judgment it could not make. For example: "I used an LLM to draft the DCE profiles and to summarize the Greenwald versus Oswald validity debate; I decided myself that the brand-archetype WEAT is a proposal rather than an existing result, because the model was willing to treat the component-wise validation as if it validated the full application — which it does not."*

## What Would Change My Mind

The chapter holds three positions open rather than asserting them, and what would change my mind is symmetrical with what would close each open question. On the brand IAT gap: a published, peer-reviewed study measuring physician implicit attitudes toward a specific drug brand with adequate reliability would convert the gap into a method. On the WEAT construct: a validated brand-versus-patient-archetype WEAT, benchmarked against behavioral prescribing data, would move it from proposal to instrument. On brand equity versus clinical value: a well-identified study showing durable equity tracks ICER value would refute the "commercial memory, not clinical signal" concern; a null result would confirm it. The stance is evidence-first — these are flagged as open precisely so the evidence, when it arrives, can settle them.

## Still Puzzling

The deepest puzzle is whether durable brand association and clinical value are even correlated at the level of physician decision rules. The evidence links price to ICER value and finds frequent divergence, but no one has tested whether the *equity* — the patient-type rule — tracks value once clinical score is controlled. If it does not, then the most valuable asset in pharma marketing is, by construction, partly decoupled from patient benefit. That is not an assertion. It is an untested, testable, and consequential claim — exactly the kind a Fellow can put on public data.

---

## Exercises

**Warm-up**

1. *(Recall — low difficulty) What this tests: the core definition of pharma brand equity.* In two sentences, explain why unaided recall of a brand name is not the strongest signal of pharma brand equity, and state what the strongest signal is. Then explain why the consumer-goods brand funnel (awareness → purchase → loyalty) does not map cleanly onto the pharma prescribing decision.

2. *(Recall — low difficulty) What this tests: the logic of the delayed re-measurement.* Explain why a single post-exposure favorability survey cannot distinguish a durable association shift from a transient recall bump, and state the one design element that resolves the ambiguity. Name the route-of-persuasion distinction (central versus peripheral) that underlies the durability difference.

3. *(Recall — low difficulty) What this tests: the explicit versus implicit instrument contrast.* Define a discrete-choice experiment (DCE) and explain how including brand name as an attribute alongside identical clinical specifications allows it to isolate the pure brand premium. Then explain, in one sentence, what an IAT measures that a DCE cannot.

**Application**

4. *(Apply — medium difficulty) What this tests: diagnosing the divergence in the opening case.* For the opening-case physician (praises the efficacy data, has never switched a stable patient onto Brand X): specify one explicit measurement and one behavioral measurement that would reveal the divergence between her stated and behavioral associations, and state in one sentence what each one would and would not tell you about whether she has built the durable patient-type rule.

5. *(Apply — medium difficulty) What this tests: WEAT design from component parts.* Specify a WEAT design to test whether Brand X is more associated with a target patient archetype than its main competitor, over a CME corpus. Name your target sets (X and Y) and your attribute sets (A and B). State what a positive WEAT score would and would not tell you, and identify the one validation step you would need to move the result from exploratory signal to publishable instrument.

6. *(Apply — medium difficulty) What this tests: decay-curve design and interpretation.* You run a brand association study with an immediate post-test and a four-week delayed post-test. Physician A shows identical patient-selection survey scores at both time points. Physician B shows a strong score immediately after exposure and a score at four weeks that has returned to the pre-exposure baseline. What inference do you draw about each, and what alternative explanation for Physician A's pattern would you need to rule out?

**Synthesis**

7. *(Synthesis — high difficulty) What this tests: designing the full association instrument.* For your own research thread, design an association instrument: a content-variant study with a control, an explicit measure and a computational measure of the *same* association, and a delayed post-test. State your hypothesis about where the two instruments will diverge and why. Then name the one result that would convince you the content shifted durable equity rather than a transient recall bump.

8. *(Synthesis — high difficulty) What this tests: connecting brand equity to patient welfare.* Draft a one-page proposal for a study testing whether durable brand equity — operationalized as physician patient-type rule stability across six months — correlates with ICER clinical-value scores for the same drugs, using Open Payments, Part D, and ICER public data. State the hypothesis, the outcome variable, the main control variables, and — explicitly — why a null result would be a high-impact finding rather than a negative one.

**Challenge**

9. *(Challenge — open-ended) What this tests: reasoning about contested instrument validity.* A brand team proposes using an IAT to measure physician implicit attitudes toward Brand X, citing the Greenwald et al. (2009) meta-analysis as validation. Write a response that: (a) accurately states what the Greenwald meta-analysis found and what Oswald et al. (2013) found in the same literature, (b) identifies the gap specific to drug brands (no published study), and (c) proposes the minimum empirical evidence that would validate the instrument for this application. Do not simply reject the proposal — engage with what validation would require.
