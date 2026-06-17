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


| | TRx (Total Rx) | NRx (New Rx) | NBRx (New-to-Brand Rx) |
|---|---|---|---|
| What it counts | Every prescription dispensed — new starts plus refills | Newly written prescriptions, excluding refills | Only prescriptions where the patient is genuinely new to the brand, judged across full therapy history |
| Lag characteristics | Lagging — a refill of a two-year-old decision counts identically to a fresh one | Mixed — fresher than TRx but not anchored to first brand exposure | Leading — captures the decision at the moment it is made |
| What it misses | When the decision was actually made; can stay green on refill inertia | Blends existing-brand patients getting routine new scripts with genuinely new decisions | Persistence — a burst of new starts that never refill |
| When to use it as primary metric | Headline volume / quarterly business review only | A rough new-activity read when NBRx is unavailable | The cleanest read on decisions being made now; pair with a persistence guardrail |

*Table 2.1 — The three prescription-count metrics measure three different things: TRx is a lagging volume number, NBRx is the leading indicator of decisions being made now.*


One technical note worth flagging. The major claims-data vendors — IQVIA foremost among them — describe their NBRx methodology as a "gold standard" with roughly 93% coverage of outpatient prescriptions before projection adjustments. These are the vendors' own characterizations of their own products, not independent validation. The metric definition is industry-standardized and uncontroversial; the specific coverage claims are product positioning and should be read accordingly. [verify the 93% figure as a current IQVIA self-description before publication]

---

Volume is not the whole story. *Who* prescribes and whether their patients *stay* matter at least as much.

**New patient starts** are the flow of newly-treated patients — closely related to NBRx, and similarly forward-looking. **Persistence** (sometimes called adherence, or measured as DOT, days of therapy) asks whether those started patients stay on the drug over subsequent fills. A campaign that wins trials but loses persistence has built nothing durable: you have generated first prescriptions that never refill, which shows up as NBRx without the matching TRx.

**Loyalty deciles** segment the universe of eligible prescribers in a therapeutic class by prescribing volume. Decile 10 is the highest-volume prescribers, decile 1 the lowest, non-writers fall outside the ranking. The metric is widely used for targeting; it is also widely misused.

Here is the trap. Sophisticated brand teams go one step further than raw volume and compute *brand share within each physician's eligible patient pool*: Brand X prescriptions divided by all prescriptions that physician writes for the category. This yields a behavioral map that raw deciles cannot see. Consider two cardiologists. Dr. X is decile 10 — enormous prescribing volume — but only 5% brand share: ninety-five percent of her eligible patients are going to competitors. Dr. Y is decile 5 — half the volume — but 60% brand share. A naive targeting model that ranks physicians by predicted prescribing would rank Dr. Y higher. It is targeting the physician who is already largely won. Dr. X is the larger opportunity; there is far more prescribing left to convert.

![A 2x2 scatter of prescribing decile against brand share within category, showing Dr. X at decile 10 with 5 percent share as high headroom and Dr. Y at decile 5 with 60 percent share as already won.](images/02-lift-vs-brand-fig-01.png)
*Figure 2.1 — Volume is not opportunity: brand share within the eligible pool reveals headroom*

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


| | FMCG (consumer goods) | Pharma |
|---|---|---|
| What equity means | Identity expression — "I buy this because of who I am"; salience and mental availability | The durable default: "for this patient profile, in this disease state, after this prior therapy, Brand X is my default" |
| How it is measured | Aided/unaided awareness, recall, preference surveys | Behavioral: brand share across a physician's eligible patients (awareness is necessary but far from sufficient) |
| Identity or archetype ownership | Identity ownership — the brand stands for a self-image | Archetype ownership — the brand is mentally bound to a specific patient type and clinical situation |
| Failure mode of measuring it wrong | Mistaking reach for preference | Mistaking stated awareness for behavioral equity — a physician who says "best efficacy data" but never switches a stable patient |

*Table 2.2 — Brand equity in pharma is archetype ownership measured behaviorally, not the identity-driven awareness construct imported from consumer goods.*


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

![A decision tree for choosing a primary outcome metric: branching on causation versus association, then horizon and level, into a lift metric with a control, a brand metric with longitudinal design, or NBRx, each paired with a guardrail.](images/02-lift-vs-brand-fig-02.png)
*Figure 2.2 — Choosing a primary outcome metric from a commercial goal*

<!-- → [INFOGRAPHIC: Decision tree for choosing a primary outcome metric given a commercial goal — branches: Is the question about causation or association? Short or long horizon? Individual prescriber or market-level? Outputs: lift metric with control, brand metric with longitudinal design, guardrail pairing] -->

---

The central claim of this chapter is falsifiable and worth stating as such. If a large linked dataset showed that TRx and NBRx move together so tightly that the distinction makes no practical difference to brand decisions, the "winning refills, losing decisions" framing would be substantially weakened — and the insistence on NBRx as the leading indicator would need revision. Separately, if a rigorous test on linked survey-plus-claims data showed that share-of-mind-intent does *not* predict subsequent share growth, the entire SOMi → SOMa concept would need to be demoted from "leading indicator" to "interesting but non-predictive attitude data."

These are open questions. They are more interesting as open questions.

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

---

## Prompts

### Figure 2.1 — Volume is not opportunity: brand share within the eligible pool reveals headroom

Build a 2x2 scatter plot as a single self-contained HTML file using D3 7.9.0 from the cdnjs CDN, inline CSS and inline JS. X-axis = brand share within category, 0–100%, linear; Y-axis = prescribing decile, 1–10, linear. Draw two dashed quadrant dividers (at 50% share and the decile midpoint) splitting the plot region into four labeled quadrants: top-left "high headroom", top-right "already won", bottom-left "low priority", bottom-right "efficiently converted". Plot two named points: Dr. X at decile 10 / 5% share (highlighted red, "huge volume, almost unconverted") and Dr. Y at decile 5 / 60% share (ink, "largely won already"). Each point labeled in place and with a hover tooltip. Plot-region fill light grey, not white. Margins top48 right40 bottom56 left64. Two data marks only; no zero-baseline bar logic. viewBox 700x420. Structural, not aesthetic.

### Figure 2.2 — Choosing a primary outcome metric from a commercial goal

Build a top-down decision tree as a single self-contained HTML file, D3 7.9.0 from cdnjs, inline CSS/JS. Root box "Q1: Causation or association?". Left branch (edge labeled "causation") → red-bordered "LIFT question — needs a control / holdout group" → output box "incremental scripts vs. exposed-minus-control". Right branch (edge labeled "association") → "Q2: Short or long horizon? / individual or market level?" which splits into two leaf boxes: long → "BRAND metric — longitudinal design; brand share, SOMi" and short → "NBRx — decisions now; leading indicator". Below the tree, one full-width ochre-bordered callout: "Always pair the primary metric with a guardrail (e.g. NBRx + persistence over the next 2–3 fills)". Directed arrows between nodes, edge labels off the centerline, hover tooltips per node. viewBox 700x480. Structural flow, not decorative.

---

## Chapter 2 Exercises: Lift vs. Brand

**Project:** One Drug, End to End
**This chapter adds:** Chart your chosen drug's lift-vs-equity profile — its TRx/NBRx split, its loyalty-decile position, and where its brand share reveals headroom versus an already-won base.

### Exercise 1 — When to Use AI

**The judgment:** Three chapter tasks where AI assistance is appropriate.

- *Restating a vague commercial goal as several measurable outcomes* ("grow share" → candidate primary metrics + guardrails). **Why AI works here:** option-generation — you want breadth of candidate metrics before you choose, and you can judge each against the chapter's definitions.
- *Drafting precise definitions of TRx, NRx, NBRx, persistence, loyalty decile* for your drug's class. **Why AI works here:** drafting — these are standardized definitions you can verify against the chapter's Table 2.1.
- *Generating candidate failure modes for a chosen metric* (e.g., NBRx without persistence). **Why AI works here:** pattern-spotting — surfacing the standard ways a metric misleads, which you then confirm apply to your drug.

**The tell:** You are using AI appropriately when you can independently evaluate the output — when you already know what NBRx counts and are just speeding up the write-up.

### Exercise 2 — When NOT to Use AI

**The judgment:** Three tasks here that require your judgment.

- *Deciding whether your drug's question is a lift question or a brand question.* **Why AI fails here:** causal-identification problem — this depends on your specific intervention's causal structure (one extra script vs. a durable shifted default), which the model cannot infer from the metric names.
- *Concluding whether brand equity tracks clinical value for your drug.* **Why AI fails here:** missing ground truth — this is a contested, unsettled empirical question, and the model will answer it with false confidence in whichever direction it last saw.
- *Asserting that SOV > SOM means your drug will grow.* **Why AI fails here:** calibration gap — the FMCG rule of thumb is gated in pharma by formulary, label, and guidelines, and the model tends to state the rule as a law.

**The tell:** You've crossed the line when AI output is your *reason* for a conclusion rather than a tool for reaching one.
**Series connection:** This trains **T5 Causal** judgment — distinguishing "likely to prescribe" from "moveable," which is the difference between a description and a causal claim the data may not support.

### Exercise 3 — LLM Exercise

**What you're building this chapter:** A lift-vs-equity profile for your drug — its primary outcome metric, guardrail, loyalty-decile/brand-share read, and an explicit statement of which questions about it are lift questions and which are brand questions.
**Tool:** Claude. Recommend a **Claude Project** — it can hold your Chapter 1 split-agency map and drug identity so this profile builds directly on it.

**The Prompt:**

```
We are continuing a teaching case study. The drug is a branded SGLT2 inhibitor
for type 2 diabetes, in a class with branded competitors and an older generic
oral antidiabetic as a cheaper substitute. From Chapter 1 we already established
its prescriber set (primary care + endocrinology) and that the payer is the
party absent from the commercial message.

Build a lift-vs-equity profile for this drug, using only the metric framework
below. Use general market knowledge only; invent NO specific numbers and state
NO lift or share figure as fact; mark anything uncertain "[verify]".

1. METRIC TABLE. For this drug, fill a table with rows TRx, NRx, NBRx,
   persistence/DOT, loyalty decile, brand-share-within-eligible-pool. For each:
   what it would tell a brand team about THIS drug, and its single most
   important failure mode.

2. GOAL TRANSLATION. The brand director says "grow share next year." Translate
   that into one primary outcome metric + one guardrail metric, and name the
   failure mode the primary metric alone would miss. Justify why you chose NBRx
   (or argue for another) for THIS drug.

3. HEADROOM READ. Describe the two-physician headroom trap for this drug: a
   high-decile / low-brand-share prescriber vs. a mid-decile / high-brand-share
   prescriber, and which is the larger opportunity and why.

4. LIFT-OR-BRAND SORT. List three questions a team might ask about this drug and
   sort each as a LIFT question (needs a control) or a BRAND question (needs
   longitudinal measurement). Do NOT claim any metric reflects patient benefit.

Output as markdown. End with the one number you would most want to verify before
acting on this profile.
```

**What this produces:** A structured lift-vs-equity profile for your drug, with metric choices, guardrails, a headroom read, and a lift/brand sort.
**How to adapt this prompt:** *For your own drug:* swap the first two sentences (drug, class, substitute) and your Chapter 1 prescriber/payer findings; keep the four-part structure. *For ChatGPT/Gemini:* paste in one message and re-include your Chapter 1 facts since there is no persistent Project. *For a Claude Project:* keep the drug identity and Chapter 1 map in the Project instructions; send only the numbered tasks.
**Connection to previous chapters:** Uses the Chapter 1 split-agency map (prescriber set, absent payer) as the starting context. **Preview of next chapter:** In Chapter 3 you will assemble this drug's synthetic/public prescriber identity graph and propensity vector — the deciles you reason about here become features there.

### Exercise 4 — CLI Exercise

**What you're building this chapter:** A reproducible local computation of prescriber count and total claims by year for your drug from public Part D data, with a written note on why this is a TRx-style lagging measure. · **Tool:** Claude Code (single dataset, scripted summary). · **Skill level:** Intermediate.

**Setup:**
1. Download one year-or-two slice of the public Medicare Part D Prescriber file (you will reuse it heavily in Chapter 12) into `one-drug/data/`.
2. Claude Code installed; Python or DuckDB available.
3. Add a CLAUDE.md rule: "Only compute over the local data file; never invent counts; print the exact filter used."

**The Task:**

```
In one-drug/, using the Part D file already in one-drug/data/, do only this:

1. Write a small script (Python+pandas or DuckDB) that filters to one drug's
   brand name (use the SGLT2 brand you placed in DRUG.txt), and computes, per
   year present in the data: distinct prescriber count and total claim count.
2. Compute the year-over-year change in each.
3. Write ch02-partd-summary.md with the resulting table, the exact drug-name
   filter string used, and a one-paragraph note explaining why this Part-D count
   is closer to a lagging TRx-style measure than an NBRx leading indicator, and
   what additional data you would need to approximate NBRx.

Verification step: print the row count before and after the filter so I can
confirm the filter actually matched rows. Do not modify the raw data file. Stop
after writing ch02-partd-summary.md.
```

**Expected output:** A script, plus `ch02-partd-summary.md` with the per-year table, the filter string, the row-count check, and the TRx-vs-NBRx note.
**What to inspect:** The pre/post-filter row counts — if "after" is zero or implausibly high, the brand-name match is wrong.
**If it goes wrong:** Most likely failure is a brand-name string that matches nothing (formatting/casing in the file) yielding an empty table the model then "explains" anyway. Recovery: inspect distinct brand names in the file for the right spelling and re-filter — don't accept a summary built on zero rows.
**CLAUDE.md / AGENTS.md note:** Add "Every data summary must report the filter string and the pre/post-filter row count."

### Exercise 5 — AI Validation Exercise

**What you're validating:** The lift-vs-equity profile from Exercise 3 (and the metric reasoning behind the Exercise 4 note). · **Validation type:** Reasoning + Structured-data. · **Risk level:** Med — a mislabeled lift/brand sort will misdirect every study design later in the project.

**Setup:** Use your Exercise 3 output as the artifact.

**The Validation Task:**

```
Validation Checklist — Chapter 2 (Lift-vs-Equity Profile)

Mark each Pass / Fail / Cannot-determine with one line of evidence:

- Correctness: Are TRx, NRx, NBRx defined consistently with the chapter (TRx
  lagging, NBRx leading)?
- Completeness: Does every metric row have BOTH a use and a failure mode? Is the
  primary metric paired with a guardrail?
- Scope: Did it avoid asserting any metric reflects patient benefit?
- Chapter-specific 1 (lift vs. brand): Is each sorted question correctly a lift
  question (control needed) or brand question (longitudinal)? Re-derive two
  yourself.
- Chapter-specific 2 (headroom): Is the larger opportunity the high-volume /
  low-share prescriber, not the already-won high-share one?
- Failure-mode check (fluent-but-wrong + attribution circularity): Did it state
  the SOV>SOM rule as a law (wrong), or treat any vendor "lift" figure as causal
  when the same platform would serve and measure it? Flag any number not marked
  [verify].
```

**What to do with your findings:** Pass → adopt the profile. One fail → revise that section and re-run. Multiple/uncertain → redo the lift/brand sort yourself from the chapter's two-ladder logic; this is a "When NOT to Use AI" moment, because the lift/brand call is exactly the judgment the model cannot make for your intervention.
**AI Use Disclosure prompt (mandatory):** Two sentences — what the AI produced (e.g., "drafted the metric table and goal translation") and how you used it, plus one thing it couldn't determine (e.g., "whether my drug's core question is a lift or brand question, which I decided because only I know the intervention's causal structure").
**Series connection:** Trains detection of **attribution circularity** under **T5 Causal** judgment — refusing to read a same-platform "lift" number as a causal effect.
