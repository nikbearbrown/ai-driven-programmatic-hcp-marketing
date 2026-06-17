# Chapter 2 — Lift vs. Brand: The Two Dependent Variables
*Winning refills while losing decisions — and why the dashboard won't tell you.*

A brand team I want you to picture is in a good mood. Their cardiovascular drug — mature, several years on market — is posting healthy total prescription numbers. The dashboard is green. Refills are strong. The install base is loyal. By every metric on the wall, they are winning.

Then one analyst pulls a different cut of the same data. Among prescriptions written for patients *new to the brand* — people deciding, right now, what to start — the brand is down twenty percent year over year. New patients are going to competitors. The strong top line is the sound of an existing base refilling decisions already made; the *new* decisions are being quietly lost.

This is the failure mode the entire chapter turns on. The team was watching the wrong number. Total volume was a lagging measure of decisions from the past; it can stay green on refill inertia for a year or more while the brand's actual competitive position erodes underneath. The phrase worth carrying: **winning refills, losing decisions.** Whether you would have caught this depends entirely on whether you knew that "is the brand doing well?" hides two fundamentally different questions — and that each question demands its own metric, its own study design, and its own time horizon.

---

Start with the split, because everything else in this book routes through it.

**Lift** is the *incremental* change in prescriptions caused by a specific exposure. It is a short-horizon, campaign-attribution question: did this ad cause more prescriptions than would have happened anyway? The operative word is *incremental* — not "did scripts go up," but "did scripts go up *because of this*, above the counterfactual where the exposure never happened?" Lift is inherently a causal claim, which means it demands a control: a group of physicians who were *not* exposed, against which you can compare those who were.

**Brand** is a different animal entirely. Brand asks whether the drug has become the physician's durable mental and clinical default for a particular kind of patient — and whether that default persists, survives competitive challenge, survives loss of exclusivity, and sustains a price premium. It is a longitudinal construct: you cannot see it in ninety days because it is not an event, it is a state. Brand measurement asks "is this physician thinking about Brand X when a certain patient walks through the door?" not "did this email cause a script last Tuesday?"

The tempting misconception is that these are the same thing measured at different time scales — that brand is just lift that lasts. This is wrong, and it is wrong in a precise way. They are different *constructs* that require different *designs*. Lift needs a control or holdout group — the study is causal. Brand needs longitudinal measurement of durable association — the study is observational and stretched across months. And they come apart in both directions. A campaign can produce lift with zero brand formation: one-time trial prescriptions that never repeat. Brand can grow with no measurable campaign lift at all: a guideline change, or word diffusing through key opinion leaders who never saw your email. Understanding why is understanding why you need two chapters later in this book — one on incrementality methods (Chapter 8), one on brand equity study design (Chapter 9).

---

Now the vocabulary, because you cannot think clearly about either question without it.

Prescription counting looks simpler than it is. Three metrics dominate the field, and they measure three genuinely different things that happen to involve the same product.

**TRx — Total Rx** — is every prescription dispensed: new starts plus refills. It is the number on the wall, the headline in the quarterly business review, and it is *lagging*. TRx can look healthy on refill inertia while the brand ages, because a script written today for a patient who started two years ago counts identically to a fresh clinical decision. The number has no memory of when the decision was made.

**NRx — New Rx** — captures newly *written* prescriptions, excluding refills. Better, but still imperfect. NRx can include a patient who has been on the brand for months and is simply getting a new script from the same physician at a routine visit. It blends old relationships with new ones.

**NBRx — New-to-Brand Rx** — is where the signal lives. This metric looks *backward* across the patient's full therapy history, over a longitudinal window, and counts only prescriptions where the patient is genuinely new to the brand. It catches the decision at the moment it is made. NBRx has subtypes worth knowing: therapy-naïve new-to-market patients; switch-from-competitor; restart-after-lapse; add-on. Each tells you something different about where the brand is winning.

The opening case is now readable in metric terms. The team had flat-to-rising TRx — old decisions refilling — and NBRx down twenty percent. Every new patient was going to a competitor, but the refill stream was masking it. TRx is a lagging measure of decisions already locked in; NBRx is the leading indicator of the decisions being made *right now*. The moment you see strong TRx and falling NBRx together, you are looking at a brand that is aging in place while the market moves past it. Paradoxically, that is exactly the moment a brand team should worry most — when the dashboard still looks green.

<!-- → [TABLE: Three-column comparison of TRx, NRx, NBRx — rows: what it counts, lag characteristics, what it misses, when to use it as primary metric] -->

One technical note worth flagging. The major claims-data vendors — IQVIA foremost among them — describe their NBRx methodology as a "gold standard" with roughly 93% coverage of outpatient prescriptions before projection adjustments. These are the vendors' own characterizations of their own products, not independent validation. The metric definition is industry-standardized and uncontroversial; the specific coverage claims are product positioning and should be read accordingly. [verify the 93% figure as a current IQVIA self-description before publication]

---

Volume is not the whole story. *Who* prescribes and whether their patients *stay* matter at least as much.

**New patient starts** are the flow of newly-treated patients — closely related to NBRx, and similarly forward-looking. **Persistence** (sometimes called adherence, or measured as DOT, days of therapy) asks whether those started patients stay on the drug over subsequent fills. A campaign that wins trials but loses persistence has built nothing durable: you have generated first prescriptions that never refill, which shows up as NBRx without the matching TRx.

**Loyalty deciles** segment the universe of eligible prescribers in a therapeutic class by prescribing volume. Decile 10 is the highest-volume prescribers, decile 1 the lowest, non-writers fall outside the ranking. The metric is widely used for targeting; it is also widely misused.

Here is the trap. Sophisticated brand teams go one step further than raw volume and compute *brand share within each physician's eligible patient pool*: Brand X prescriptions divided by all prescriptions that physician writes for the category. This yields a behavioral map that raw deciles cannot see. Consider two cardiologists. Dr. X is decile 10 — enormous prescribing volume — but only 5% brand share: ninety-five percent of her eligible patients are going to competitors. Dr. Y is decile 5 — half the volume — but 60% brand share. A naive targeting model that ranks physicians by predicted prescribing would rank Dr. Y higher. It is targeting the physician who is already largely won. Dr. X is the larger opportunity; there is far more prescribing left to convert.

<!-- → [CHART: 2x2 scatter plot — x-axis: brand share within category (0–100%), y-axis: decile rank (1–10); quadrants labeled: "already won," "high headroom," "low priority," "efficiently converted"; points colored by opportunity tier] -->

That trap has a deeper version that will return in Chapter 8. A model that predicts *who will prescribe* is not a model that predicts *whom you can change*. Targeting the physicians most likely to prescribe anyway, then measuring their response, systematically *overstates* your lift estimate — because many of those prescriptions were going to happen with or without your intervention. The headroom concept here is the first piece of the instrumentality problem. Keeping that distinction sharp — "likely to prescribe" versus "moveable" — is half of what Chapter 8 is about.

---

Lift the lens from individual prescribers to the market, and two more constructs enter.

**Share of Voice (SOV)**, or detail share, is the brand's fraction of total promotional presence in a therapeutic market: its share of rep calls, digital impressions, speaker programs, journal ads, congress presence, everything. It measures how loud you are.

**Share of Mind (SOM)** is the brand's share of *physician mental availability* — recall, association, prescribing intent. It measures whether the noise landed. The industry shorthand **SOMi → SOMa** captures a claimed dynamic: share-of-mind-*intent* (what physicians say they think and intend to prescribe) is claimed to *lead* share-of-mind-*actual* — actual prescribing market share — with a lag.

There is a rule of thumb borrowed from fast-moving consumer goods: if SOV exceeds SOM, the brand tends to grow; if SOV is below SOM, it tends to shrink. The misconception is to treat this as a law in pharma. It is, at best, a leading indicator hedged by gates that do not exist in consumer goods: the FDA label, clinical guidelines, payer access, prior authorization, safety signals, institutional prescribing pathways. Mental availability ideas from the Ehrenberg-Bass tradition apply to salience and reach, but far less to *evidence-gated* prescribing decisions.

Picture a brand with 30% SOV and 15% SOM. Consumer-goods logic predicts growth — you are twice as loud as you are remembered, so memory should catch up. But if the brand sits on Tier-3 formulary behind step therapy, the growth may never materialize. The gate, not the voice, is binding. Shouting louder helps only if the door is not locked by the formulary.

The SOMi → SOMa leading-indicator claim deserves to be flagged explicitly. It is asserted qualitatively across the industry — vendors will tell you that higher brand equity predicts market-share growth — but as of this writing, it is not rigorously tested on linked survey-plus-claims data. [verify; treat as a vendor hypothesis, not an established finding] The statement that "higher brand equity is predictive of market-share growth" appears in vendor materials with no published test attached. Whether mind-share actually predicts share growth with a lag is a tractable research question. It is also exactly the kind of study a Fellow could run on available data, which is why Chapter 13 returns to it.

---

Now the deepest idea in the chapter, and the one most worth resisting the easy version of.

Pharma brand equity is not awareness. In consumer goods, brand is partly identity expression — I wear this because of who I am. In pharma, the construct is more constrained and, if it exists in the way the industry believes, more valuable: *for this patient profile, in this disease state, after this prior therapy, Brand X is my default.* Equity is the durable pattern in which a physician mentally associates a drug with a specific patient archetype — a patient type and clinical situation — and then repeatedly prescribes it for that type without deliberating from scratch each time.

The strongest equity signal is not the physician remembering the brand. It is the physician remembering the *patient type* and the brand coming along automatically.

This is why aided or unaided brand awareness is a misleading surrogate for equity. Awareness is necessary but nowhere close to sufficient. Consider a physician who says, sincerely, "Brand X has the best efficacy data in its class," but who has never once switched a stable patient through three successive generic entries. Strong stated awareness; weak behavioral equity. Behavioral equity shows up in the data as high brand share across a physician's eligible patients — not in a recall survey, which captures what physicians say they believe, not what they do when the chart is in front of them.

Keep one distinction sharp, because the evidence does not support collapsing it. The evidence that marketing builds durable brand *identity* is weaker than the evidence for marketing's association with prescribing behavior. The synthesis underlying this book is explicit: the evidence is "stronger for association and behavioral influence than for clean causal proof of brand identity." Do not let "brand equity" smuggle in a causal claim the data does not support. [contested — see pantry: brand equity vs. clinical value is an open empirical question]

And here is the contested edge: whether brand equity tracks clinical value at all — whether the drugs with the strongest physician loyalty are also the drugs with the strongest evidence base — is not settled. A BMJ-linked analysis argued that the most-promoted drugs were less likely than top-selling drugs to be effective, safe, affordable, novel, or genuine advances; a 2023 study reported that 68% of the most-advertised drugs have low added clinical benefit. [verify both figures against primary sources before publication] Whether these patterns hold robustly, and what they imply for the commercial machine, is an open question the book does not close. Brand equity may be correlated with clinical value, uncorrelated, or negatively correlated. That is testable against ICER value scores in the final projects of Chapter 13, and the chapter seeds it without asserting a direction.

<!-- → [TABLE: Comparison of brand equity in FMCG vs. pharma — rows: what equity means, how it is measured, whether identity or archetype ownership, the failure mode of measuring it wrong] -->

---

Here is how the concepts connect in practice.

Take the worked example from the opening: a brand director says "our goal next year is to grow share," and asks you to make that measurable with a defined failure mode.

First instinct: use TRx. Dead end. We just saw TRx stay green while a brand lost every new decision.

Second instinct: use NRx — "growth" sounds like new prescriptions. Better, but NRx still blends existing-brand patients getting new scripts with genuinely new decisions.

The right answer: **NBRx** as the primary outcome — new-to-brand prescriptions, the cleanest read on decisions being made now. But a metric without a named failure mode is a trap in waiting. NBRx's failure mode is trial without persistence: you can win a burst of new starts that never refill, posting strong NBRx while building no durable base. So you pair the primary metric with a guardrail: NBRx *and* persistence over the following two to three fills.

"Grow share" becomes: *increase NBRx year over year, with persistence held at or above current levels.* A vague commercial goal converted into a measurable outcome with an explicit failure mode the metric alone would miss.

The limit of this exercise is important to name. This mapping tells you *what to measure*; it does not tell you whether your campaign *caused* the NBRx you observe. NBRx going up is consistent with a great campaign, a competitor's stumble, a guideline change, or seasonal noise. Causation is the lift question, and it needs a control group you do not get from a dashboard. That is precisely why Chapter 8 exists.

---

One patient-welfare note that belongs here before the chapter closes.

The welfare risk in metric work is metric capture: optimizing NBRx and share without ever measuring whether the new starts were clinically appropriate. Commercial measurement sees commercial KPIs well — NBRx, switch-ins, share of voice — and patient-welfare KPIs poorly: real-world outcomes, clinical appropriateness, total cost of care. For every project in this book, the welfare question is: *does this metric, optimized hard, reward anything a patient would not want?* Winning new decisions is good for the brand. Whether those decisions were the right drug, for the right patients, at the right time — the commercial metric never asks.

<!-- → [INFOGRAPHIC: Decision tree for choosing a primary outcome metric given a commercial goal — branches: Is the question about causation or association? Short or long horizon? Individual prescriber or market-level? Outputs: lift metric with control, brand metric with longitudinal design, guardrail pairing] -->

---

The central claim of this chapter is falsifiable and worth stating as such. If a large linked dataset showed that TRx and NBRx move together so tightly that the distinction makes no practical difference to brand decisions, the "winning refills, losing decisions" framing would be substantially weakened — and the insistence on NBRx as the leading indicator would need revision. Separately, if a rigorous test on linked survey-plus-claims data showed that share-of-mind-intent does *not* predict subsequent share growth, the entire SOMi → SOMa concept would need to be demoted from "leading indicator" to "interesting but non-predictive attitude data."

These are open questions. They are more interesting as open questions.

---

**Five-part AI exercise block**

**When to use AI.** Use an LLM to draft definitions, generate candidate failure modes for a metric, or restate a vague commercial goal as several alternative measurable outcomes you can then choose among. Good for breadth and first drafts.

**When NOT to use AI.** Do not let an LLM decide *whether your thread is a lift or a brand question*, or *whether brand equity tracks clinical value* — the first requires understanding your specific intervention's causal structure, the second is a contested empirical question the model will happily answer with false confidence.

**LLM exercise (copy-paste prompt):**
> "I have a pharma commercial goal: [STATE GOAL]. Propose three different primary outcome metrics it could map to (choose from TRx, NRx, NBRx, persistence/DOT, loyalty-decile movement, share of voice, share of mind). For each, state (a) what it measures, (b) its single most important failure mode, and (c) a guardrail metric that would catch that failure. Then tell me which metrics make this a *lift* question and which make it a *brand* question. Do not assert that any metric reflects patient benefit."

**CLI exercise.** From a public prescriber dataset (e.g., a Medicare Part D Prescriber file you will use heavily in Chapter 12), use the command line to compute, for a single drug, the count of prescribers and total claims by year, then the year-over-year change. Write one sentence on why this Part-D-derived number is closer to a TRx-style lagging measure than an NBRx leading measure, and what you would need to approximate NBRx.

**AI Validation exercise.** Ask an LLM to summarize the relationship between share of voice and share of mind in pharma. Then check its answer against this chapter: did it state the SOV > SOM rule as a *law* (wrong for pharma) or as a *leading indicator gated by formulary/label/guidelines* (right)? Write one sentence correcting it if it overstated the rule, and note that this is exactly the SOMi → SOMa claim the chapter flags as unvalidated.

**AI Use Disclosure**

*Write two sentences naming what an AI tool did in your work for this chapter and the one judgment it could not make. For example: "I used an LLM to brainstorm candidate metrics and failure modes for my goal; I decided myself that my thread is a brand question rather than a lift question, because the AI could not tell whether my intervention's value lies in causing one extra script or in shifting the durable default for a patient type."*

---

**What Would Change My Mind**

The central claim of this chapter is that lift and brand are genuinely distinct constructs requiring distinct measurement, and that NBRx — not TRx — is the leading indicator of brand health. A study showing that, in a large linked dataset, TRx and NBRx move together so tightly that the distinction makes no practical difference to brand decisions would substantially weaken the "winning refills, losing decisions" framing and the insistence on NBRx. Separately, if a rigorous test on linked survey-plus-claims data showed that share-of-mind-intent does *not* predict subsequent share growth, the entire SOMi → SOMa leading-indicator concept — and the brand-measurement practices built on it — would need to be demoted from "leading indicator" to "interesting but non-predictive attitude data."

**Still Puzzling**

- Does brand equity, measured properly, track clinical value (ICER scores) at all — and if it is uncorrelated or negatively correlated, what does that say about what the commercial machine is actually optimizing? (Seeds Chapters 9 and 13.)
- The evidence for marketing building durable brand *identity* is weaker than for association with prescribing. Is durable identity even separable from "repeated exposure plus inertia," or is "brand equity" partly a story we tell about persistence we cannot otherwise explain?
- At loss of exclusivity, small-molecule brand equity usually collapses but specialty/biologic equity often persists — is the persistent part really *brand belief*, or is it service infrastructure (patient support, hubs, biosimilar friction) wearing brand's clothing? (Seeds the Chapter 13 LOE natural-experiment thread.)

---

## Exercises

**Warm-up**

1. *(Factual recall — metric definitions)* Define TRx, NRx, and NBRx so precisely that you could explain to a brand manager why a brand can post record TRx in the same quarter its NBRx falls. Write two sentences; use a numerical example.
   *What this tests: whether you can hold the three metrics distinct and articulate what each misses.*

2. *(Factual recall — lift vs. brand)* State in one sentence the study design difference between a lift study and a brand study — why does lift require a control group and brand require a longitudinal design?
   *What this tests: the core structural distinction between causal and longitudinal measurement.*

3. *(Factual recall — SOM/SOV)* Name the SOV > SOM rule, state one reason it may not hold in pharma, and give the name for the claimed dynamic between intent share-of-mind and actual market share.
   *What this tests: vocabulary and the limits of importing FMCG concepts into regulated markets.*

**Application**

4. *(Apply to a new scenario)* A brand manager reports that a digital campaign drove a 40% increase in email open rates and a 25% increase in content clicks, and concludes "the message worked." Identify the surrogate, explain why engagement is a misleading stand-in for scripts or belief, and name two metrics you would demand instead — and what each could still fail to show.
   *What this tests: surrogate vs. outcome, and the double failure-mode structure.*

5. *(Apply segmentation logic)* Dr. A is a decile-9 prescriber with 8% brand share in the category. Dr. B is a decile-5 prescriber with 55% brand share. Which is the larger targeting opportunity and why? What additional information would sharpen your answer?
   *What this tests: conversion headroom vs. raw volume, and the seed of the instrumentality problem.*

6. *(Apply metric mapping)* A brand director says: "We want to defend our position in the market during the upcoming LOE window." Map this goal to a primary metric and a guardrail, and name the failure mode the primary metric alone would miss.
   *What this tests: translating a strategic intent into a measurable outcome with explicit failure conditions.*

**Synthesis**

7. *(Combine lift and brand concepts)* A colleague argues that NBRx is both the right lift metric and the right brand metric, so running one study that tracks NBRx solves both problems. Construct the strongest possible argument against this position, drawing on the structural distinction between the two constructs.
   *What this tests: whether you can hold both constructs and their design requirements in tension simultaneously.*

8. *(Synthesize across vocabulary)* A brand is posting strong NBRx but poor persistence. Share of voice is 35% versus a competitor at 40%. Share-of-mind surveys show 60% recall. Classify the brand's situation on each axis — lift opportunity, brand equity health, SOV/SOM position — and recommend one diagnostic study and one metric to add to the dashboard.
   *What this tests: integrating all five concept areas into a coherent situational read.*

**Challenge**

9. *(Open-ended — design a study)* The chapter flags SOMi → SOMa — the claim that share-of-mind-intent predicts future market share with a lag — as unvalidated on linked survey-plus-claims data. Sketch a study design (in one paragraph) that would test this claim. What data would you need? What is the hardest methodological problem? What result would falsify the claim?
   *What this tests: converting a flagged hypothesis into a tractable research design, and identifying its empirical breaking point.*
