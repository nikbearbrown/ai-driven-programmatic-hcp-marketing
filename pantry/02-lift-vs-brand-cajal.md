# CAJAL Figure Report — Chapter 02: Lift vs. Brand: The Two Dependent Variables
_Mode: /scan silent · 2026-06-16 · source: chapters/02-lift-vs-brand.md_

## Density recommendation
6 figures, Mixed density — the chapter is built on conceptual distinctions (lift vs. brand, three Rx metrics, FMCG vs. pharma equity) that need comparison/conceptual figures, plus one genuine 2x2 segmentation scatter and one decision tree, with two contested empirical claims that must be flagged rather than depicted as fact.

## Figures

---

FIGURE 1 — Winning refills while losing decisions: TRx vs. NBRx divergence · Priority: Critical · Type: Statistical / quantitative (paired trend) · Heuristic: PQ

BLOCK 1 — ILLUSTRAE PASTE BLOCK:
Create a flat vector quantitative chart, single-column 89mm width at 300 DPI, showing the opening case in which two prescription metrics for the same brand move in opposite directions over one year. Plot two series on a shared zero-based vertical axis against a horizontal time axis of roughly twelve months: a total-prescription (TRx) series that stays flat-to-rising, and a new-to-brand (NBRx) series that declines about twenty percent year over year. The visual point is the widening gap between a healthy-looking top line and an eroding leading indicator beneath it. Render the TRx series in a neutral/secondary color to mark it as the misleading lagging measure, and the NBRx series in the disruptive/warning color to mark the genuine decline being masked. Shade or otherwise indicate the growing divergence between the two lines. The y-axis must start at zero and bar or line heights must be proportional. Leave all numerals, axis ticks, and legend text off the image; build only the two proportioned series and the divergence region.

BLOCK 2 — FULL SCOPE:
[S - SPECIFICATION] Single column, 89mm width, 300 DPI, vector, textbook style, white background, y-axis from zero.
[C - CONTENT] Confirmed: TRx (total Rx, new + refills) flat-to-rising on refill inertia; NBRx (new-to-brand Rx) down ~20% YoY; the gap is the "winning refills, losing decisions" failure mode. TRx = lagging; NBRx = leading indicator of decisions made now.
[O - ORGANIZATION] Two line/area series over a 12-month horizontal axis on a shared zero-based y-axis; divergence region highlighted.
[P - PRESENTATION] Flat vector, white bg, Okabe-Ito: NBRx (eroding leading signal) #D55E00, TRx (misleading lagging line) light gray, axis #000000, 1pt strokes.
[E - EXCLUSIONS] Omit NRx as a third series (keep to two for clarity); omit the metric-definition table content (Figure 2); omit persistence/DOT; omit dollar figures; omit drug/brand names; no 3D, no truncated axis.

BLOCK 3 — NEGATIVE PROMPT:
third data series, truncated y-axis, axis not starting at zero, 3D, pie chart, drug packaging, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

FIGURE 2 — TRx vs. NRx vs. NBRx: what each metric counts · Priority: Critical · Type: Comparison panels · Heuristic: VG

BLOCK 1 — ILLUSTRAE PASTE BLOCK:
Create a flat vector three-column comparison panel, single-column 89mm width at 300 DPI, distinguishing the three prescription-counting metrics across a shared set of attribute rows. Set up three aligned columns for TRx, NRx, and NBRx, and four shared horizontal rows: what it counts, lag characteristic, what it misses, and when to use it as the primary metric. Use a nested or layered visual to encode that the metrics narrow progressively — TRx is the widest set (new starts plus refills), NRx is a subset (newly written, refills excluded), and NBRx is the tightest, backward-looking subset (patient genuinely new to the brand). Render NBRx as the primary anchor where the signal lives, TRx in neutral gray as the broad lagging measure, NRx as an intermediate secondary color. Keep the three columns strictly row-aligned for horizontal scanning. Leave all cells and headers blank of text; build only the aligned scaffold and the progressive-narrowing visual relationship.

BLOCK 2 — FULL SCOPE:
[S - SPECIFICATION] Single column, 89mm width, 300 DPI, vector, textbook style, white background.
[C - CONTENT] Confirmed: TRx = every Rx dispensed (new + refills), lagging, has no memory of when decision was made; NRx = newly written, excludes refills, still blends old relationships with new; NBRx = backward-looking over a longitudinal window, counts only patients genuinely new to brand, catches the decision at the moment made. Confirmed subset relationship TRx ⊃ NRx ⊃ NBRx. Four comparison rows confirmed in source's own table call-out.
[O - ORGANIZATION] Three columns mapped to 4 shared attribute rows; nested-subset visual (TRx widest → NBRx narrowest); horizontal scanning.
[P - PRESENTATION] Flat vector, white bg, Okabe-Ito: NBRx #0072B2 (where the signal lives), NRx #E69F00 (intermediate), TRx light gray (broad/lagging), 1pt strokes.
[E - EXCLUSIONS] Omit NBRx subtypes (naïve/switch/restart/add-on) from this figure; omit the IQVIA 93%-coverage claim; omit the opening case chart (Figure 1); omit persistence; omit drug names; do not bake row/column text into cells.

BLOCK 3 — NEGATIVE PROMPT:
NBRx subtype breakdown, coverage percentage numerals, more than four rows, drug packaging, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

FIGURE 3 — Decile rank vs. brand share: the targeting-headroom trap · Priority: Critical · Type: Statistical / quantitative (2x2 scatter) · Heuristic: PQ / VG

BLOCK 1 — ILLUSTRAE PASTE BLOCK:
Create a flat vector 2x2 scatter quadrant chart, single-column 89mm width at 300 DPI, mapping prescribers by two dimensions to expose the headroom trap. The horizontal axis is brand share within the physician's eligible category, running zero to one hundred percent; the vertical axis is loyalty-decile rank, running one to ten. Divide the plane into four quadrants and place two illustrative physician points: Dr. X at high decile (10) but low brand share (about 5 percent), sitting in the high-volume/high-headroom region; and Dr. Y at mid decile (5) but high brand share (about 60 percent), sitting in the high-share/low-headroom region. Encode that Dr. X is the larger conversion opportunity (much prescribing left to win) and Dr. Y is largely already won. Color the high-headroom point in the active/opportunity color and the already-won point in neutral gray. Keep to two plotted points and four quadrant regions. Leave axis numerals and quadrant text off the image; build only the axes, quadrant divisions, and the two distinguished points.

BLOCK 2 — FULL SCOPE:
[S - SPECIFICATION] Single column, 89mm width, 300 DPI, vector, textbook style, white background.
[C - CONTENT] Confirmed: x = brand share within category (0-100%); y = loyalty-decile rank (1-10). Dr. X = decile 10, ~5% brand share = high headroom / larger opportunity. Dr. Y = decile 5, ~60% brand share = already largely won. Confirmed insight: a naive volume-ranking model wrongly ranks Dr. Y higher. Quadrant semantics from source: "already won," "high headroom," "low priority," "efficiently converted."
[O - ORGANIZATION] 2x2 quadrant scatter; two labeled points; shared zero-anchored axes.
[P - PRESENTATION] Flat vector, white bg, Okabe-Ito: high-headroom point (Dr. X) #009E73 (opportunity), already-won point (Dr. Y) light gray, axes/quadrant lines #000000, 1pt strokes.
[E - EXCLUSIONS] Omit the instrumentality/"likely vs. moveable" extension text (Chapter 8 handoff); omit more than two example points; omit persistence; omit drug names; do not render quadrant labels as baked text; no 3D.

BLOCK 3 — NEGATIVE PROMPT:
more than two data points, 3D scatter, axis not starting at zero, quadrant text baked in, drug packaging, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

FIGURE 4 — Share of Voice vs. Share of Mind, gated by formulary · Priority: Important · Type: Systems diagram · Heuristic: VG / MC

BLOCK 1 — ILLUSTRAE PASTE BLOCK:
Create a flat vector systems diagram, single-column 89mm width at 300 DPI, showing why the consumer-goods "SOV exceeds SOM predicts growth" rule is gated in pharma. On the left, depict Share of Voice (promotional loudness) as an input flowing rightward toward Share of Mind (physician mental availability), and from there toward an outcome of market-share growth. Between Share of Mind and the growth outcome, place a prominent gate or barrier representing the pharma-specific constraints that do not exist in consumer goods: the FDA label, clinical guidelines, payer access, prior authorization, and formulary tier. Render the SOV-to-SOM flow as active progression, and the gate in the blocking/disruptive color with a blockage symbol indicating it can stop the flow even when voice exceeds mind. Encode the worked case spatially: a strong voice input that is halted at the locked formulary gate, so growth does not materialize. Keep to the input, the intermediate, the gate (as one consolidated barrier), and the outcome. Leave all text off the image.

BLOCK 2 — FULL SCOPE:
[S - SPECIFICATION] Single column, 89mm width, 300 DPI, vector, textbook style, white background.
[C - CONTENT] Confirmed: SOV (share of promotional presence / loudness) → SOM (share of physician mental availability) → market-share growth, BUT gated in pharma by FDA label, clinical guidelines, payer access, prior authorization, formulary tier. Confirmed case: 30% SOV, 15% SOM, but Tier-3 formulary behind step therapy means growth may never materialize — "the gate, not the voice, is binding." Use ⊣ blockage semantics at the gate.
[O - ORGANIZATION] Horizontal L→R flow (SOV → SOM → growth) with a consolidated gate/barrier (⊣) interposed before the growth outcome.
[P - PRESENTATION] Flat vector, white bg, Okabe-Ito: SOV→SOM flow #56B4E9 (primary), gate/barrier #D55E00 (blocking), growth outcome node #009E73, ⊣ blockage in #000000, 1pt strokes.
[E - EXCLUSIONS] Omit the SOMi→SOMa leading-indicator sub-claim (separate, and flagged contested — see Figure 5 note); omit the Ehrenberg-Bass attribution as text; omit numeric SOV/SOM values as baked numerals; omit drug names; keep the five gate constraints consolidated as one barrier, not five separate labeled gates (component-count discipline).
[FIREWALL NOTE] The "SOV>SOM predicts growth" rule is explicitly NOT a law in pharma per the chapter; depict it as a hedged, gated tendency, never as a deterministic rule.

BLOCK 3 — NEGATIVE PROMPT:
five separate labeled gates, deterministic rule depiction, numeric values baked in, drug packaging, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

FIGURE 5 — Brand equity in FMCG vs. pharma · Priority: Important · Type: Comparison panels · Heuristic: VG

BLOCK 1 — ILLUSTRAE PASTE BLOCK:
Create a flat vector side-by-side comparison panel, single-column 89mm width at 300 DPI, contrasting how brand equity works in fast-moving consumer goods versus pharma across a shared set of rows. Build two aligned columns, FMCG on the left and pharma on the right, with four shared horizontal rows: what equity means, how it is measured, whether it rests on identity expression or patient-archetype ownership, and the failure mode of measuring it wrong. Encode the central distinction spatially: FMCG equity centers on identity expression ("I use this because of who I am"), while pharma equity centers on a physician's durable association of a drug with a specific patient archetype and clinical situation, expressed as repeated prescribing without re-deliberation. Render the pharma column as the primary anchor and the FMCG column as a neutral/secondary reference. Keep the two columns strictly row-aligned for horizontal scanning. Leave all cells and headers blank of text; build only the aligned comparison scaffold.

BLOCK 2 — FULL SCOPE:
[S - SPECIFICATION] Single column, 89mm width, 300 DPI, vector, textbook style, white background.
[C - CONTENT] Confirmed: FMCG equity = partly identity expression; pharma equity = durable association of drug with a specific patient archetype + clinical situation, prescribed repeatedly without deliberating from scratch. Confirmed: strongest equity signal = remembering the patient type and the brand following automatically; awareness is necessary but not sufficient; behavioral equity shows as high brand share across eligible patients, not in recall surveys. Four comparison rows confirmed in source's own table call-out.
[O - ORGANIZATION] Two columns mapped to 4 shared attribute rows; horizontal scanning; no flow arrows.
[P - PRESENTATION] Flat vector, white bg, Okabe-Ito: pharma column #0072B2 (dominant conceptual), FMCG column light gray (reference), 1pt strokes.
[E - EXCLUSIONS] Omit the contested brand-equity-vs-clinical-value question (that is a flagged claim, not a depictable fact — keep out of this figure); omit the BMJ/2023 advertising-vs-clinical-benefit statistics; omit loss-of-exclusivity material; omit drug names; do not bake row text into cells.
[FIREWALL NOTE] Do NOT visualize "brand equity tracks clinical value" in any direction — the chapter flags this as an open, contested empirical question. The evidence is "stronger for association/behavioral influence than for clean causal proof of brand identity"; do not let the figure smuggle in a causal identity claim.

BLOCK 3 — NEGATIVE PROMPT:
clinical-value correlation depiction, advertising-vs-benefit statistics, more than four rows, drug packaging, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

FIGURE 6 — Choosing a primary outcome metric: decision tree · Priority: Important · Type: Process flowchart (decision tree) · Heuristic: MC

BLOCK 1 — ILLUSTRAE PASTE BLOCK:
Create a flat vector decision-tree flowchart, single-column 89mm width at 300 DPI, guiding the choice of a primary outcome metric from a commercial goal. Start from a single entry node (the commercial goal) and branch through three sequential binary decision points: is the question about causation or association; is the horizon short or long; is the analysis at the individual-prescriber or market level. Lead the branches to three terminal outputs: a lift metric paired with a control group, a brand metric paired with a longitudinal design, and a guardrail-pairing output (primary metric plus its failure-mode guardrail). Lay the tree top-to-bottom with clean single-headed branch arrows and consistent diamond decision nodes and rectangular outcome nodes. Color the causation/lift path and the association/brand path distinctly so the two study-design families are visually separable, and render the guardrail-pairing output as a transitional/composite element since it attaches to either path. Keep to three decision nodes and three outcome nodes. Leave all node text off the image; build only the branching scaffold.

BLOCK 2 — FULL SCOPE:
[S - SPECIFICATION] Single column, 89mm width, 300 DPI, vector, textbook style, white background.
[C - CONTENT] Confirmed decision branches from source's infographic call-out: causation vs. association; short vs. long horizon; individual prescriber vs. market level. Confirmed outputs: lift metric with control; brand metric with longitudinal design; guardrail pairing. Confirmed worked example logic: "grow share" → NBRx primary + persistence guardrail (this is the embodied path through the tree).
[O - ORGANIZATION] Top-to-bottom decision tree; 3 binary decision nodes (diamonds) → 3 outcome nodes (rectangles); → progression on branches.
[P - PRESENTATION] Flat vector, white bg, Okabe-Ito: lift/causation path #56B4E9, brand/association path #E69F00, guardrail output #CC79A7 (composite/transitional), decision nodes/arrows #000000, 1pt strokes.
[E - EXCLUSIONS] Omit the full worked NBRx+persistence narrative as baked text; omit the metric-capture / patient-welfare note (separate concept); omit more than three decision nodes; omit drug names; do not bake branch-condition text into the diamonds.

BLOCK 3 — NEGATIVE PROMPT:
more than three decision nodes, baked branch-condition text, drug packaging, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Video candidate pass

FIGURE 1 — TRx/NBRx divergence
Status: STATIC SUFFICIENT
Criterion met: none (time element alone does not qualify)
Reason: The divergence over twelve months is fully legible as a static paired-trend chart; the learning target is the gap, not the unfolding, and self-paced inspection serves better.

FIGURE 2 — Three Rx metrics comparison
Status: STATIC SUFFICIENT
Criterion met: none
Reason: A nested-subset comparison; no transition mechanism.

FIGURE 3 — Decile vs. brand-share trap
Status: STATIC SUFFICIENT
Criterion met: none
Reason: A two-point quadrant comparison; static allows careful reading of where each physician sits.

FIGURE 4 — SOV/SOM gated flow
Status: VIDEO CANDIDATE
Criterion met: Criterion 1 (transition mechanism is the learning target)
Reason: The instructional point is that voice flows toward growth but is halted at the formulary gate; an animation showing the SOV signal advancing and then being stopped at the locked gate dramatizes "the gate, not the voice, is binding" better than a static blockage symbol — though a static ⊣ also communicates it adequately.
Suggested format: short looping animation showing the signal advancing and stalling at the gate.

FIGURE 5 — FMCG vs. pharma equity
Status: STATIC SUFFICIENT
Criterion met: none
Reason: A conceptual comparison table; nothing to animate.

FIGURE 6 — Metric-choice decision tree
Status: STATIC SUFFICIENT
Criterion met: none
Reason: A branching decision aid is best inspected statically so the reader can trace any path at their own pace.

Video candidates identified: 1. Recommended for production: Figure 4 — the SOV/SOM gated flow, because the chapter's correction of the imported FMCG "rule" hinges on the reader seeing the promotional signal get blocked at the formulary gate rather than flowing through to growth. This is the chapter's only true transition-mechanism concept; the other five are comparisons, distributions, or decision aids that static treatment serves as well or better.
