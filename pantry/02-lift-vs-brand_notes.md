# Research Notes: Chapter 02 — Lift vs. Brand: The Two Dependent Variables

**Chapter one-line (TIKTOC):** Fellows learn to decide whether a question is about campaign **lift** (incremental scripts) or **brand formation** (durable "Brand X is for this patient"), and to pick the right metric.

**Opening artifact (TIKTOC):** a brand with healthy TRx but collapsing NBRx — "winning refills, losing decisions."

**Scope of these notes:** campaign lift vs. brand equity; TRx/NRx/NBRx, new starts, persistence, loyalty deciles, share of voice / share of mind; "brand = remembering the patient type."

> **Primary reuse source:** `pantry/pharma-brand-measurement-synthesis.md` is the spine of this chapter — these notes synthesize and source-check it, adding a few external citations. A chapter author should read that file alongside these notes.

---

## A. Conceptual foundations

### A1. The two dependent variables — lift vs. brand
**Explanation.** The whole book routes through this split (TIKTOC names Ch 2 a load-bearing chapter). **Lift** = the *incremental* change in prescriptions caused by a specific exposure — a short-horizon, campaign-attribution question ("did this ad cause more scripts than would have happened anyway?"). **Brand** = a *durable belief-and-behavior* system — whether the drug becomes the physician's default mental/clinical choice for a patient archetype, and whether that choice persists, survives competition and loss-of-exclusivity, and sustains a price premium. Campaign attribution asks "did this exposure generate incremental scripts?"; brand measurement asks "is this drug becoming the default choice for a category of physicians and patients?"
**Common misconception.** "Lift and brand are the same thing measured at different time scales." They are different *constructs* requiring different study designs: lift needs a **control/holdout** (causal, Ch 8); brand needs measurement of **durable association** over time (longitudinal, Ch 9). A campaign can produce lift with zero brand formation (a one-time trial that never repeats) and brand can grow with no measurable campaign lift (guideline change, KOL diffusion).
**Worked example.** Same content variant: (a) lift question — "did exposed NPIs write more new starts than matched unexposed NPIs in the next 90 days?"; (b) brand question — "did exposed physicians durably shift toward associating Brand X with *this* patient type, measured 6–12 months out?"
**Source.** `pantry/pharma-brand-measurement-synthesis.md` (opening framing + Bottom Line); TIKTOC Part 5 arc statement.

### A2. The prescribing-volume metrics: TRx / NRx / NBRx
**Explanation.**
- **TRx (Total Rx):** all prescriptions dispensed (new + refills). Lagging; can look healthy on refill inertia while the brand is aging.
- **NRx (New Rx):** newly written prescriptions (excludes refills) — but still includes patients already on the brand getting a *new* script.
- **NBRx / NBx (New-to-Brand Rx):** prescriptions where the patient is **new to the brand** after a longitudinal lookback across prior therapies. The cleanest read on *current* treatment decisions. Subtypes: new-to-market/therapy-naïve, switch-from-competitor, restart-after-lapse, add-on.
**Common misconception.** "Rising TRx = the brand is winning." TRx can rise on refill persistence (old decisions) while NBRx falls — the chapter's opening case ("winning refills, losing decisions"). NBRx is the leading indicator because it reflects the physician's decision *at the moment of choice* and the marketing team's effort most directly.
**Worked example.** Brand A: TRx flat/up, NBRx down 20% YoY → the install base is refilling but new patients are going to competitors; equity is eroding even though the top-line looks stable. This is precisely when a brand team should worry.
**Source.** `pantry/pharma-brand-measurement-synthesis.md` §2A (IQVIA Brand Analytics subcomponents: NBRx, new-to-market, immediate switch, restart, add-on; IQVIA NBRx as "gold-standard" longitudinal input; ~93% outpatient Rx coverage before projection). External: Definitive Healthcare NBRx glossary (https://www.definitivehc.com/resources/glossary/nbrx); Alpha Sophia NBRx (https://www.alphasophia.com/glossary/nbrx-new-to-brand-prescription) — NBRx reflects marketing more directly than NRx/TRx and signals competitive share capture.

### A3. Persistence, new starts, and prescriber loyalty deciles
**Explanation.** **New patient starts** = the flow of newly-treated patients (closely related to NBRx). **Persistence / adherence / DOT (days of therapy)** = whether started patients stay on. **Loyalty deciles** = segmenting the universe of eligible prescribers in a class by prescribing volume/value (decile 10 = highest, decile 1 = lowest, non-writers = none). Sophisticated teams go beyond volume to **brand share within each physician's eligible patient pool** (Brand X scripts ÷ all eligible category scripts), yielding behavioral segments: non-writer, trialist, occasional writer, loyalist, advocate/KOL.
**Common misconception.** "Target the highest-volume (decile 10) prescribers." Not necessarily — a **decile-10 physician with *low* brand share** may be more valuable than a decile-5 with high share, because the upside (conversion headroom) is bigger. The goal is converting *habit*, not generating one script. (This also seeds the Ch 8 lesson: targeting high-decile responders and measuring their response *inflates* lift estimates.)
**Worked example.** Two cardiologists: Dr. X (decile 10, 5% brand share) vs. Dr. Y (decile 5, 60% brand share). Dr. X is the bigger opportunity. A naïve propensity model that ranks by predicted prescribing would rank Dr. Y higher and miss the conversion upside.
**Source.** `pantry/pharma-brand-measurement-synthesis.md` §2B (decile + brand-share segmentation table). NBRx + predictive-KPI framing: PM360 "Every Metric Tells a Story" (https://pm360online.com/every-metric-tells-a-story/).

### A4. Share of Voice (SOV) vs. Share of Mind (SOM/SOMi→SOMa)
**Explanation.** **SOV / detail share** = the brand's share of *promotional presence* in a market (rep calls, details, speaker programs, emails, digital, journal ads, congress, scientific SOV). **Share of mind (SOM)** = the brand's share of *physician mental availability* (recall, association, prescribing intent). The FMCG rule of thumb: if SOV > SOM, the brand tends to grow; if SOV < SOM, it shrinks. The industry shorthand **SOMi → SOMa** = mind-share (SOM-intent) is claimed to *lead* market-share/SOM-actual with a lag.
**Common misconception.** "SOV is a law of growth like in FMCG." In pharma it is a **leading indicator, not a law** — extra gates intervene: FDA label, clinical guidelines, payer access, prior authorization, safety, institutional pathways. Ehrenberg-Bass mental-availability ideas apply to salience/reach but less to evidence-gated prescribing.
**Worked example.** Brand with SOV 30% but SOM 15% — FMCG logic predicts growth; but if it's blocked on Tier-3 formulary with step therapy, the growth never materializes. The gate, not the voice, is binding.
**Source.** `pantry/pharma-brand-measurement-synthesis.md` §2C (SOV formula; Veeva HCP 360 / CRM-derived SOV) + §5 (pharma vs. FMCG). SOMi→SOMa predictive-validity is **asserted qualitatively in industry but not rigorously tested on linked survey+claims data** (TIKTOC research finding; corroborated only loosely — Inizio "higher brand equity is predictive of market-share growth," https://inizio.com/insights/measuring-brand-equity-a-brands-beating-heart/ — a vendor claim, not a published test).

### A5. "Brand = remembering the patient type" (the core insight)
**Explanation.** Pharma brand equity is **not awareness**. It is the durable pattern where a physician mentally associates a drug with a *patient type / clinical situation / risk profile / treatment-sequence position* and then repeatedly prescribes it. The FMCG version is "I wear Calvin Klein"; the pharma version is: *"For this patient profile, in this disease state, after this prior therapy, Brand X is my default."* More constrained, but far more valuable. Equity is strongest when the physician does not merely remember the *brand* but remembers the *patient type*.
**Common misconception.** "Brand equity = aided/unaided awareness." Awareness is necessary, not sufficient — the strongest equity signal is patient-archetype ownership, which shows up behaviorally as loyalty (high share of eligible patients), not in a recall survey.
**Worked example.** A physician who says "Brand X has the best efficacy data" but has never switched a stable patient through three generic entries — strong *stated* awareness, weak *behavioral* equity. (This is also Ch 9's opening case.)
**Source.** `pantry/pharma-brand-measurement-synthesis.md` §3 (brand-formation loop) + §5; the key line "becomes strongest when the physician … remembers the patient type."

---

## B. Domain examples and cases

- **The TRx-up / NBRx-down brand (opening case).** Mature drug, strong refills, weak new starts — the textbook "winning refills, losing decisions." Demonstrates why TRx alone misleads and NBRx is the leading indicator. (Synthesis §2A.)
- **Decile-10-low-share vs. decile-5-high-share targeting.** Real brand-planning trade-off; shows loyalty deciles need the brand-share dimension, not just volume. (Synthesis §2B.)
- **LOE / generic-entry equity stress test.** At loss of exclusivity, small-molecule equity usually collapses (payer/pharmacy substitution dominates), but persists in specialty, biologic/biosimilar, high-risk, and strong-patient-support markets. Brand equity here is partly *service infrastructure*. (Synthesis §4 table.) This is also a Ch 13 Track B natural experiment (LOE persistence).
- **FAILURE / contested case — equity that doesn't track clinical value.** A BMJ-linked analysis argued the *most-promoted* drugs were *less* likely than top-selling/top-prescribed drugs to be effective, safe, affordable, novel, or genuine advances; a 2023 study found 68% of the most-advertised drugs have low added clinical benefit. The failure mode: brand equity optimized as **commercial memory, not clinical value** — testable against ICER value scores (Ch 9/13 research thread). (Synthesis §6; `pantry/pharma-marketing-evidence-synthesis.md` §4.)

---

## C. Connections and dependencies

- **Prereqs:** Ch 1 (the stack and the split — the metrics describe what the stack optimizes).
- **Unlocks:** Ch 3 (to move either metric you must reach the right HCP — the identity graph); Ch 8 (lift = incrementality, the causal half of this split, escalated to study design); Ch 9 (brand association as a measurable outcome — the *spiral return* on this chapter's brand half, escalated to measurement design); Ch 13 Tracks A (lift/attribution) and B (brand/identity).
- **Load-bearing:** TIKTOC marks Ch 2 as one of three load-bearing chapters — "the lift/brand split everything routes through." Skipping it breaks Act III.
- **Adjacent:** Ch 5 (rating evidence per metric/channel); Ch 14 (the handoff brief asks "lift or brand, and how strong is the evidence").

---

## D. Current state of the field

- **Settled.** TRx/NRx/NBRx, deciles, SOV, persistence are standardized commercial metrics (IQVIA/Symphony/Definitive Healthcare define them consistently). NBRx is widely accepted as the leading decision-indicator. Industry payments are *associated* with increased branded prescribing (Annals of Internal Medicine systematic review; JAMA Internal Medicine statin study) — association, not clean causal proof of *brand identity*.
- **Contested / open.** (1) **SOMi→SOMa predictive validity** — the leading-indicator claim is asserted qualitatively, not tested on linked survey+claims data (TIKTOC's flagged research finding; a tractable Ch 13 study). (2) **Brand equity vs. clinical value** — open empirical question; may be uncorrelated or even negatively correlated (BMJ-linked analysis; testable vs. ICER, Ch 9/13).
- **Last-3-years developments.** AI plugs into the *behavioral + investment* layers first (NBA optimizes engagement/NBRx/call-response; segmentation optimizes decile movement) and sees commercial KPIs well (NBRx, switch-ins, SOV) but patient-welfare KPIs poorly (real-world outcomes, clinical appropriateness, total cost of care). The measurement frontier: connecting commercial brand metrics to patient-centered outcomes. (Synthesis §7.)

---

## E. Teaching considerations

- **Where students stick.** (1) Conflating NRx and NBRx — drill the longitudinal-lookback definition; (2) assuming higher decile = better target — the conversion-headroom flip; (3) treating SOV>SOM as deterministic — the pharma gates break the FMCG law; (4) equating brand with awareness — the "remembers the patient type" reframe is the key unlock.
- **Analogies.** TRx vs. NBRx = "total customers vs. *new* customers this month — a store can have steady foot traffic while every new shopper goes to the competitor." Brand-as-patient-type = "not 'I've heard of this drug' but 'when I see *this exact patient*, my hand reaches for this pad.'" SOV vs. SOM = "shouting louder helps only if the door isn't locked by the formulary."
- **Exercises (match TIKTOC).** Given a stated commercial goal, map it to a primary outcome metric and its failure modes (e.g., "grow share" → NBRx, failure mode = trial without persistence). Evaluate-level: judge when engagement (opens/clicks) is a misleading surrogate for belief/scripts. **Part B:** the Fellow picks their own thread here — a *lift* thread or a *brand* thread (this is the choice point for the whole arc).

---

## F. Library files relevant (copied to `pantry/` as `_lib_*`)

- `_lib_science-calling-bullshit-the-art-of-skepticism-in-a-data-driven-world.md` — surrogate-metric and "number that sounds meaningful but isn't" reasoning; directly supports the "engagement is a misleading surrogate" objective and rating SOV/SOM claims.

*(Ch 2 is overwhelmingly served by `pantry/pharma-brand-measurement-synthesis.md`; the MD library adds only skepticism/metrics-critique support. No pharma-brand-specific library file exists in MD.)*

---

## G. Gaps and flags

- **FLAG (TIKTOC research finding):** SOMi→SOMa leading-indicator claim is *not* rigorously validated on linked survey+claims data. Vendor sources (Inizio) assert predictive validity but cite no published test. Present as a hypothesis to be tested (Ch 13), not a settled fact.
- **CONTESTED (book's position):** "Brand equity tracks clinical value" = open/empirical; testable (ICER vs. equity), may be uncorrelated. Do not assert correlation either way.
- **FLAG:** IQVIA's "~93% outpatient Rx coverage" and "NBRx gold-standard" are IQVIA's own characterizations — accurate as descriptions of their product positioning, but cite them as vendor self-description, not independent validation.
- **GAP:** Clean *causal* evidence that marketing builds durable *brand identity* (vs. association with prescribing) is weaker than the association evidence — the synthesis is explicit that evidence is "stronger for association and behavioral influence than for clean causal proof of brand identity." Keep that distinction sharp.
