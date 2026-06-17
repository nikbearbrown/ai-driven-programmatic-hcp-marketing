# CAJAL Figure Report — Chapter 12: Research Design and Public Data for Marketing Science
_Mode: /scan silent · 2026-06-16 · source: chapters/12-research-design-public-data.md_

## Density recommendation

This chapter is the strongest MC + comparison material in the set: four identification strategies, the TWFE-vs-Callaway-Sant'Anna mechanism, and a four-dataset stack. Recommended density: **5 figures**. The chapter carries three author stubs (fundamental-counterfactual problem; staggered-adoption forbidden-comparison; public-data stack table) — all three confirmed. Two additions: the four-strategy decision tree (the chapter literally calls the choice "a short tree") and a 2×2 DiD double-differencing mechanism figure. Hold at five. RDD and IV are mechanism-rich but verbal-argument designs (continuity assumption, exclusion restriction) that resist clean static depiction without baked text; keep them in prose and let the decision tree (Figure 5) carry their selection logic. Do not chart ICER thresholds ($50k / $175k per QALY) or first-stage F≥10 as figures — they are stated cutoffs, contested/[verify], and belong inline.

## Figures

---

FIGURE 1 — The fundamental problem of causal inference (missing counterfactual) · Critical · Structural / before-after · VG
BLOCK 1 ILLUSTRAE PASTE:
Draw two parallel horizontal timelines for a single physician, stacked one above the other and aligned on the same time axis. The upper timeline represents world A, in which the physician received heavy detailing, and it is drawn as a solid continuous line ending in an observed outcome marker — a filled node. The lower timeline represents world B, in which the same physician received no detailing, and it is drawn as a dashed, faded line ending in a hollow, ghosted outcome marker to signal that this outcome is unobserved and missing. Between the two endpoint markers, draw a short vertical connector with a single-headed arrow indicating that the causal effect is the difference between the observed world-A outcome and the missing world-B outcome. Color the observed world-A line and its filled node in dominant blue, and render the world-B line, its hollow node, and its region in a neutral gray to mark it as the absent counterfactual. The composition must make unmistakable that one of the two worlds is observed and solid while the other is missing and ghosted, and that the causal effect is the gap between them.

BLOCK 2 FULL SCOPE:
- [S] single-col 89mm / 300DPI / vector / textbook.
- [C] One physician, two potential worlds: World A (heavy detailing, observed, solid, filled outcome node); World B (no detailing, unobserved, dashed, hollow node). Causal effect = World A outcome − World B outcome. Every design = an argument to impute World B from other observable units [inferred caption, not drawn].
- [O] Two parallel horizontal timelines on shared time axis. Solid (A) above, dashed (B) below. Vertical difference connector with single-headed arrow between the two endpoint nodes.
- [P] Flat vector, white bg. World A line + filled node = #0072B2 (dominant/observed); World B line + hollow node = neutral gray (missing). Difference connector = #000000. 1pt strokes; dashed = standard dash, not hand-drawn.
- [E] No baked text, no shadows, no third world/timeline, no population of other physicians drawn (imputation lives in caption), no human figures, no 3D, no red-green.

BLOCK 3 NEGATIVE PROMPT:
text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

FIGURE 2 — Difference-in-differences double-differencing · Critical · Structural / before-after · VG
BLOCK 1 ILLUSTRAE PASTE:
Draw a line plot with a horizontal time axis spanning a pre-period and a post-period separated by a vertical event line marking when treatment occurs. Draw two trend lines: an upper or lower control-group line that continues at a steady slope straight through the event with no break, and a treated-group line that runs parallel to the control before the event then bends away from its prior path after the event. Crucially, draw a dashed continuation of the treated line extending along its pre-event slope into the post-period — the counterfactual path the treated group would have followed under the parallel-trends assumption. The vertical gap in the post-period between the dashed counterfactual continuation and the actual treated line is the causal effect; mark it with a short bracketed vertical span. Color the control line in anchor blue, the actual treated line in a dominant tone, and the dashed counterfactual continuation in neutral gray. Before the event the treated and control lines must visibly move in parallel; after the event the treated line must diverge from its own dashed counterfactual, and that divergence span is the estimate.

BLOCK 2 FULL SCOPE:
- [S] single-col 89mm / 300DPI / vector / textbook.
- [C] Two groups (treated, control) across pre/post split by event line. Parallel pre-trends. Dashed counterfactual = treated group's pre-slope extended (parallel-trends assumption). Causal effect = vertical gap between actual treated post-path and dashed counterfactual. Functional-form caveat (levels vs logs) [caption only].
- [O] Time-axis line plot. Vertical event line. 3 lines: control (solid), treated (solid, bends post-event), counterfactual (dashed, continues pre-slope). Bracketed vertical span = effect.
- [P] Flat vector, white bg. Control = #56B4E9 (anchor); treated = #0072B2 (dominant); counterfactual continuation = neutral gray dashed; effect bracket = #000000. 1pt strokes.
- [E] No baked text/axis numbers, no shadows, no confidence bands, no third treated cohort (this is the clean 2×2; staggered case is Figure 3), no y-axis-from-zero requirement (this is a trend plot, not a bar — note for renderer), no red-green.

BLOCK 3 NEGATIVE PROMPT:
text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

FIGURE 3 — Staggered adoption: forbidden vs clean comparisons · Critical · Structural / process · VG / MC
BLOCK 1 ILLUSTRAE PASTE:
Draw a three-panel figure arranged left to right. In the left panel, draw four horizontal unit timelines on a shared time axis: three treated units whose lines change state — shifting color from untreated to treated — at three different adoption dates spread across the span, plus one never-treated unit whose line stays a single untreated state throughout. In the center panel, illustrate the forbidden comparison: draw an arrow from an early-treated unit, already shifted to its treated state, pointing to a later-treated unit as if serving as its control, and mark this arrow as invalid with a perpendicular stop-bar to signal it is a forbidden comparison. In the right panel, illustrate the clean comparison: draw arrows from each treated cohort pointing only to not-yet-treated and never-treated units, all valid single-headed arrows with no stop-bars. Color treated-state segments in a dominant tone, untreated and never-treated segments in neutral gray, the forbidden-comparison arrow and its stop-bar in blocking orange-vermillion, and the clean-comparison arrows in active green. The three panels must read as a progression from setup, to the error, to the correct fix.

BLOCK 2 FULL SCOPE:
- [S] full-width / 120–140mm (three panels) / 300DPI / vector / textbook.
- [C] Left: 3 units adopting at 3 dates (e.g. 2006/2009/2012) + 1 never-treated. Center: TWFE forbidden comparison — already-treated unit used as control for later-treated (Goodman-Bacon 2021). Right: Callaway–Sant'Anna — each cohort compared only to not-yet-treated + never-treated. de Chaisemartin–D'Haultfœuille / Sun–Abraham / Borusyak [caption, alternatives].
- [O] Three panels L→R. Panel 1: 4 horizontal unit timelines, state-change markers. Panel 2: one ⊣-barred forbidden arrow. Panel 3: clean single-headed arrows (→) to valid controls only.
- [P] Flat vector, white bg. Treated segments = #0072B2 (dominant); untreated/never-treated = neutral gray; forbidden arrow + stop-bar = #D55E00 (blocking); clean arrows = #009E73 (active). 1pt strokes.
- [E] No baked text/year labels (use position on shared axis), no shadows, no more than 4 units (≤6–8 components), no estimator math, no dual-headed arrows, no red-green pairing.

BLOCK 3 NEGATIVE PROMPT:
text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

FIGURE 4 — The public-data stack · Important · Structural / comparison · VG
BLOCK 1 ILLUSTRAE PASTE:
Draw four horizontal dataset bands stacked vertically, each band representing one public dataset: Open Payments, Medicare Part D Prescriber, Medicaid State Drug Utilization Data, and ICER value assessments. Within the composition, visually encode each dataset's role in a study by drawing connector lines that show how they combine: a connector from the Open Payments band to the Part D and SDUD bands representing the promotion dose joining to the prescribing outcome, and a connector from the ICER band to those outcome bands representing the clinical-value covariate that makes findings welfare-relevant. Render the Open Payments band — the promotion dose — in a secondary tone, the two outcome-panel bands (Part D and SDUD) in anchor blue, and the ICER band — the value covariate — in a composite tone to mark its distinct welfare role. On each band, place a small caution marker indicating that the dataset carries a critical limit that must be stated in any brief. The composition must communicate that these datasets are interchangeable commodities that only become a contribution when joined by an identification design, so the connectors between them carry the meaning.

BLOCK 2 FULL SCOPE:
- [S] full-width / 120mm / 300DPI / vector / textbook (table-like density).
- [C] Four datasets: Open Payments (promotion dose, 2013–present, free, association-grade alone); Part D Prescriber PUF (prescribing outcome by NPI, ~2yr lag, no NBRx, Medicare-only); Medicaid SDUD (state×time panel, no physician identity); ICER (clinical value covariate, $50k/$175k per QALY [verify], free PDFs). Each carries a critical limit (caution marker). [Coverage dates/access are factual; thresholds contested.]
- [O] Four stacked bands. Connectors: Open Payments → Part D + SDUD (dose→outcome); ICER → outcome bands (covariate). Small caution glyph per band.
- [P] Flat vector, white bg. Open Payments = #E69F00 (secondary/dose); Part D + SDUD = #56B4E9 (anchor/outcome); ICER = #CC79A7 (composite/welfare); caution glyphs = #D55E00 (blocking) outline. 1pt strokes. Connectors single-headed (→) or plain joins.
- [E] No baked text (this complements, does not replace, the prose stack table), no shadows, no fifth dataset, no rendered dollar thresholds, no DUA/coverage-date numerals baked in, no red-green.

BLOCK 3 NEGATIVE PROMPT:
text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

FIGURE 5 — Identification-strategy decision tree · Important · Process / decision · MC
BLOCK 1 ILLUSTRAE PASTE:
Draw a decision tree flowing top to bottom, beginning from a single entry node and branching through a sequence of yes-or-no decision diamonds, each routing to a terminal design node. The first diamond asks whether a policy was adopted at different times across units; a yes routes to a terminal node for staggered difference-in-differences with Callaway-Sant'Anna. A no flows down to a second diamond asking whether a single dated shock hit one group and not another; a yes routes to a terminal node for two-by-two difference-in-differences. A no flows to a third diamond asking whether a sharp eligibility or spending cutoff exists; a yes routes to a terminal node for regression discontinuity. A no flows to a final diamond asking whether an exogenous shifter of exposure exists with a defensible exclusion restriction; a yes routes to a terminal node for instrumental variables. Use single-headed arrows throughout, render the decision diamonds in a uniform anchor tone, and render the four terminal design nodes in active green. The tree must read as a clean cascade where each failed condition flows down to the next test, ending in exactly one of four design recommendations.

BLOCK 2 FULL SCOPE:
- [S] single-col 89mm (or 120mm if four terminals crowd) / 300DPI / vector / textbook.
- [C] Four sequential conditions → four designs: staggered adoption → staggered DiD (Callaway–Sant'Anna, event-study, not-yet/never-treated controls); single dated shock → 2×2 DiD/event study (parallel-trends defense); sharp cutoff → RDD (density check); exogenous shifter + defensible exclusion → IV (first-stage F reported). Each design also requires: identifying assumption + falsifying diagnostic + Ladder ceiling ~L3 [caption].
- [O] Top-down tree. 4 decision diamonds in cascade (yes→terminal, no→next diamond). 4 terminal design nodes. Single-headed arrows (→).
- [P] Flat vector, white bg. Decision diamonds = #56B4E9 (anchor); terminal design nodes = #009E73 (active). 1pt strokes.
- [E] No baked question/design text, no shadows, no fifth branch, no Ladder-level numerals baked, no dual-headed arrows, no crossing paths (clean cascade), no 3D.

BLOCK 3 NEGATIVE PROMPT:
text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

### Supplementary (named, not specced to full blocks)
- **RDD threshold jump** · Supplementary · VG. A running-variable x-axis with a smooth outcome function and a sharp vertical jump at the cutoff (Part D donut hole / LIS income cutoff), plus a small density-smoothness inset (McCrary test). Mechanism-clear but overlaps Figure 5's selection logic; elevate only if RDD gets its own worked example. If rendered: jump = #D55E00, smooth fit = #0072B2, cutoff line = #000000.
- **IV three-condition triad** · Supplementary · VG. Z → treatment → outcome path with the blocked Z→outcome direct path (⊣ stop-bar = exclusion restriction) and a relevance marker (first-stage F). Risk: reduces to a textbook DAG that needs baked text to be legible; recommend prose + caption over a standalone figure.

## Video candidate pass

**Status:** Recommended (one candidate)
**Candidate:** The staggered-adoption TWFE-failure mechanism — how the two-way fixed-effects estimator recruits already-treated units as controls for later-treated units, and how Callaway–Sant'Anna repairs it by restricting to clean controls (the content of Figure 3, animated).
**Criterion:** Transition mechanism is the learning target and the transformation is sub-observable in a static frame — the *why* of the bias (forbidden comparison forming, then being removed) is a dynamic the chapter calls "wrong by math," and the reader must see the bad comparison get drawn, then deleted, then replaced.
**Reason:** This is the chapter's most consequential and most counterintuitive claim ("invalidated a generation of published estimates"). Figure 3 freezes three states; the animation shows the forbidden comparison *forming* as the early cohort's treatment effect contaminates the control, then the Callaway–Sant'Anna correction *swapping in* only not-yet-treated and never-treated controls. The recoloring/rerouting across time is the mechanism.
**Suggested format:** ~25–35s. Units adopt treatment one cohort at a time on a shared timeline; a forbidden arrow snaps from an already-treated unit to a later one (flash #D55E00 + stop-bar), then dissolves; clean arrows (#009E73) reroute to valid controls only; the biased coefficient visibly shifts toward the correct estimate. Okabe-Ito only; no baked narration. Recommend, do not auto-select — confirm one-video-per-chapter budget against Chapters 10 and 11 so three adjacent chapters do not all ship animations.
