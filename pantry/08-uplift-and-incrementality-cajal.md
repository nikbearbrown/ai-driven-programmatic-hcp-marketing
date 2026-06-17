# CAJAL Figure Report — Chapter 8: Uplift and Incrementality
_Mode: /scan silent · 2026-06-16 · source: chapters/08-uplift-and-incrementality.md_

## Density recommendation

This is the most figure-rich of the three chapters. The argument is built on a small number of geometrically vivid concepts, each of which the author has already flagged with a DIAGRAM/CHART/TABLE stub: the propensity-vs-CATE inversion curve, the persuadables 2x2, the Qini/uplift curve, the CATE-estimator taxonomy, and the terminology bridge. The scan confirms all five as figure-worthy and surfaces two net-new: the three-compounding-biases decomposition (the opening case is a three-stage causal-confound story, pure MC) and the holdout/natural-experiment identification design (a before/after structural claim). The PQ heuristic fires hardest on the inversion curve, the Qini curve, and a naive-vs-holdout magnitude contrast.

Recommended density: **6 figures**. This is a High density chapter — the visuals do genuine pedagogical work the prose cannot, because the inversion and the Qini geometry are spatial arguments. FIREWALL note: uplift-vs-propensity, the persuadables/sleeping-dogs quadrants, Qini, the S/T/X/R-learner taxonomy, and holdout design are explicitly named prime figure material; render them. The naive 44% must always be shown as the inflated/contested number, the holdout-corrected gap as the credible one.

## Figures

---

FIGURE 1 — The propensity-vs-incrementality inversion · Critical · Chart (curve) · PQ

BLOCK 1 ILLUSTRAE PASTE:
Render a single two-axis line chart. The horizontal axis is propensity score running from zero at left to one at right; the vertical axis is incremental effect, the conditional average treatment effect, beginning at zero. Plot one smooth curve that is near zero at the low-propensity left tail, rises to a single rounded peak in the middle of the propensity range, then falls back toward zero at the high-propensity right tail — an inverted-U whose maximum sits over the mid-range. Divide the plot into three vertical zones by the curve's shape: a low-propensity left zone, a mid-propensity peak zone, and a high-propensity right zone. Visually emphasize the peak zone as the region of interest using the dominant fill, and render the two tail zones in a muted neutral to signal wasted spend at both ends. The chart must make one point unmistakable: the highest incremental return lives in the middle, not at the high-propensity end where prediction confidence is greatest. Keep the vertical axis origin at zero. Maximum one curve, three zones. Flat vector, white background, single faint baseline.

BLOCK 2 FULL SCOPE:
[S] Single-column 89mm, 300 DPI, vector, conceptual chart.
[C] Confirmed: x = propensity 0→1; y = incremental effect / CATE from zero; inverted-U peaking in the mid persuadable range, near zero at both tails; high-propensity tail = "sure things, wasted spend"; low tail = "lost causes, wasted spend"; middle = "persuadables, the only profitable target." All from the author's DIAGRAM stub and "the inversion."
[O] Inverted-U curve, three zones (low / peak / high). Peak zone → dominant blue (#0072B2) as the profitable region; two tail zones → neutral gray (wasted). Single-headed axis ticks; y from zero.
[P] Flat vector, white background, Okabe-Ito with hex (peak/profitable #0072B2, tail zones neutral gray, curve/axes #000000), 1pt strokes.
[E] Exclude: the three zone labels baked as text (zones carry meaning by color/position); no second curve; no propensity histogram overlay; no annotation sentences; y-axis must not start above zero.

BLOCK 3 NEGATIVE PROMPT:
zone labels as text, second curve, histogram overlay, non-zero y origin, annotation sentences, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

FIGURE 2 — The three compounding biases of naive lift · Critical · Diagram (process/decomposition) · MC

BLOCK 1 ILLUSTRAE PASTE:
Render a horizontal decomposition diagram showing how a single inflated lift number is built from three stacked biases. At the left, place one node representing the naive reported lift. Flowing into it from the right-to-left contribution direction, draw three distinct contributor bands that combine to produce the inflated figure: the first band represents targeting on the outcome, where the treated group was selected because it would prescribe anyway; the second band represents regression to the mean plus secular trend, where high-point selections drift back and an already-growing brand inflates the count; the third band represents attribution circularity, where the platform that served the ad also measured the result on its own data with no independent firewall. Render the three bands as three clearly separated contributing segments converging into the single naive-lift node, each segment a distinct color, sized to read as "three separate sources stacking into one number." Below or beside, show a single small contrasting node representing the honest holdout-corrected effect as a much smaller residual once the three bands are removed. Maximum three bias bands plus two outcome nodes. Flat vector, white background, clean convergence.

BLOCK 2 FULL SCOPE:
[S] Single-column 89mm, 300 DPI, vector, decomposition diagram.
[C] Confirmed: naive lift inflated by three simultaneous biases — (1) targeting on the outcome (treated selected because going to prescribe); (2) regression to mean + secular trend; (3) attribution circularity (server measures own lift, no firewall); holdout-corrected effect is "a fraction of 44%, sometimes inside the noise of zero." All from the opening case.
[O] Three contributor bands → converge into inflated naive-lift node; separate small holdout-corrected residual node for contrast. Three bias bands → three distinct categorical Okabe-Ito hues; inflated node → secondary orange (the contested number); honest residual → green (the credible one). Single-headed convergence arrows.
[P] Flat vector, white background, Okabe-Ito with hex (bias bands #0072B2 / #E69F00 / #CC79A7; inflated node #E69F00 outline emphasis; honest residual #009E73; strokes #000000), 1pt strokes, single-headed arrows.
[E] Exclude: the "44%" numeral baked in (it is illustrative/flagged-for-verify in the chapter — do not hard-code it); no equation; no more than three bias bands; do not render the inflated number as legitimate-green.

BLOCK 3 NEGATIVE PROMPT:
the numeral 44, hard-coded percentages, equations, more than three bias bands, inflated number colored green, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

FIGURE 3 — The persuadables 2x2 · Critical · Diagram (matrix) · VG

BLOCK 1 ILLUSTRAE PASTE:
Render a clean two-by-two matrix. The horizontal axis is "prescribes if treated" with no on the left and yes on the right; the vertical axis is "prescribes if untreated" with yes at top and no at bottom. The four resulting quadrants each carry a distinct meaning conveyed by fill and by two converging targeting arrows: the persuadables quadrant (prescribes if treated, not if untreated) is the single profitable cell and should read as the focal cell using the dominant fill; the sure-things quadrant (prescribes either way) is wasted spend; the lost-causes quadrant (prescribes neither way) is wasted spend; the sleeping-dogs quadrant (treatment reduces the outcome) is the warning cell and should read as the hazard cell using the blocking color. Draw one arrow originating from a "propensity targeting" marker pointing into the sure-things quadrant, and a second arrow from an "uplift targeting" marker pointing into the persuadables quadrant — the two arrows are the chapter's whole argument in one gesture. Keep the matrix square, the axes labeled only by position, and the four quadrants equal-sized. Maximum four quadrants plus two targeting arrows. Flat vector, white background.

BLOCK 2 FULL SCOPE:
[S] Single-column 89mm, 300 DPI, vector, matrix diagram.
[C] Confirmed: axes = prescribes-if-treated × prescribes-if-untreated; persuadables (treated-only, net gain, only profitable group); sure things (either way, wasted + source of inflated lift); lost causes (neither way, wasted); sleeping dogs / do-not-disturbs (treatment reduces outcome, can be harmful); propensity targeting → sure things; uplift targeting → persuadables. All from "If you remember one picture."
[O] Square 2x2; persuadables → dominant blue (#0072B2, focal/profitable); sleeping dogs → blocking #D55E00 (hazard); sure things and lost causes → neutral gray (wasted). Two single-headed targeting arrows: propensity→sure-things, uplift→persuadables; the uplift arrow → green to mark the recommended move.
[P] Flat vector, white background, Okabe-Ito with hex (persuadables #0072B2, sleeping dogs #D55E00, wasted cells neutral gray, uplift arrow #009E73, propensity arrow #E69F00, strokes #000000), 1pt strokes, single-headed arrows.
[E] Exclude: quadrant names baked as text (carried by color + arrow logic); no smiley/frowny icons; no more than two arrows; sleeping-dogs must be visually distinct as a hazard, not just another wasted cell.

BLOCK 3 NEGATIVE PROMPT:
quadrant names as text, emoji, smiley icons, more than two arrows, sleeping-dogs shown as neutral, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

FIGURE 4 — The Qini / uplift curve · Critical · Chart (curve) · PQ

BLOCK 1 ILLUSTRAE PASTE:
Render a single uplift curve chart. The horizontal axis is the fraction of the population targeted, running from zero to one; the vertical axis is cumulative incremental response, beginning at zero. Plot three curves sharing the same origin and the same endpoint. The first is a perfect-model curve that rises steeply at the start and then flattens — it captures all incremental response from the top of the ranking. The second is an actual-model curve that bows moderately above the diagonal. The third is the random-targeting diagonal, a straight line from origin to endpoint. Shade the area between the actual-model curve and the diagonal to represent the Qini coefficient — the summary statistic of uplift targeting quality. Position a subtle knee annotation on the actual curve to convey that persuadables live above the knee and sure things below it. Keep the vertical axis origin at zero, the diagonal mathematically straight, and the three curves clearly distinguishable by line treatment and color. Maximum three curves plus one shaded region. Flat vector, white background.

BLOCK 2 FULL SCOPE:
[S] Single-column 89mm, 300 DPI, vector, quantitative chart.
[C] Confirmed: x = fraction targeted 0→1; y = cumulative incremental response from zero; three curves — perfect (steep then flat), actual (intermediate bow), random (diagonal); shaded area between actual and diagonal = Qini coefficient; "sure things below the knee, persuadables above." All from the author's CHART stub.
[O] Three curves + shaded Qini region. Actual model → dominant blue (#0072B2); perfect model → green (#009E73, the ceiling); random diagonal → neutral gray; Qini shaded region → light blue translucent fill (#56B4E9). y from zero.
[P] Flat vector, white background, Okabe-Ito with hex (actual #0072B2, perfect #009E73, random gray, Qini fill #56B4E9, axes #000000), 1pt strokes.
[E] Exclude: curve labels baked as text; no numeric Qini value (none given); no fourth curve; diagonal must be straight; y origin at zero, not floating.

BLOCK 3 NEGATIVE PROMPT:
curve labels as text, numeric Qini value, fourth curve, curved diagonal, non-zero y origin, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

FIGURE 5 — CATE meta-learner taxonomy · Important · Diagram (structural map) · VG

BLOCK 1 ILLUSTRAE PASTE:
Render a compact structural map of the CATE estimator family showing how each learner is wired, not a text table. Lay out six small estimator modules in two tidy rows. The S-learner: one single model box with a treatment indicator entering as one of its input features, producing one output. The T-learner: two separate model boxes — one fed only treated data, one fed only control data — with a difference node combining their outputs. The X-learner: the same two boxes but with cross-imputation arrows showing each model imputing the missing counterfactual for the other group before differencing. The R-learner: a residualization stage — two small nuisance boxes (propensity, outcome) feeding a residual-on-residual regression node. The causal forest: a small tree-cluster glyph that splits on treatment-effect heterogeneity, ending in leaf nodes each carrying an interval marker. The DR-learner: the propensity box and outcome box both feeding a single combine node with a redundancy indicator showing either-one-correct suffices. Keep each module schematic and minimal; the differences in wiring are the content. Maximum six modules. Flat vector, white background, aligned grid.

BLOCK 2 FULL SCOPE:
[S] Single-column 89mm, 300 DPI, vector, structural taxonomy.
[C] Confirmed: S-learner (one model, treatment as feature); T-learner (two models, difference); X-learner (cross-imputation of counterfactuals, handles imbalance); R-learner (residualize propensity + baseline, regress residual on residual, Neyman-orthogonal); causal forest (splits on treatment-effect heterogeneity, per-leaf CI); DR-learner (consistent if either propensity or outcome model correct). All from the estimator section + the author's TABLE stub.
[O] Six wiring schematics in a 2-row grid. Use neutral consistent fills for model boxes; highlight the *distinguishing wire* of each (treatment-feature in S, the difference node in T, cross-imputation arrows in X, residual node in R, heterogeneity split in forest, redundancy/either-one in DR) in the active green so the eye finds what makes each different. Anchors → light blue.
[P] Flat vector, white background, Okabe-Ito with hex (model boxes neutral gray, distinguishing wire #009E73, nuisance/secondary elements #E69F00, anchors #56B4E9, strokes #000000), 1pt strokes, single-headed arrows.
[E] Exclude: re-drawing the comparison table as text rows (this is the structural complement to the author's TABLE — wiring only); no equations; no "which is best" ranking (the chapter is explicit there is no universal winner); no more than six modules.

BLOCK 3 NEGATIVE PROMPT:
table rows as text, equations, ranking of estimators, best-estimator badge, more than six modules, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

FIGURE 6 — Randomized holdout vs natural experiment: two routes to a counterfactual · Important · Diagram (before/after structural) · VG

BLOCK 1 ILLUSTRAE PASTE:
Render a two-panel diagram of two ways to obtain a counterfactual. The left panel is the randomized holdout: a single high-propensity target list at top, splitting via a randomization node into a large treated group and a smaller withheld holdout group drawn from the same stratum; both groups carry forward through the campaign window to an outcome-comparison node computing treated-mean minus holdout-mean. Emphasize that the split is random and that both groups share the same starting stratum. The right panel is the natural experiment: a timeline with a policy-change shock marker at a fixed date; a treated group (physicians subject to the policy) and a matched control group (neighboring or matched physicians) running in parallel before the shock to convey the parallel-trends assumption, then diverging after the shock, with a difference-in-differences comparison node. Keep both panels on a shared horizontal time baseline so "before vs after" is the structural carrier. Mark the parallel-trends segment before the shock as the load-bearing assumption. Maximum two groups per panel plus comparison nodes. Flat vector, white background.

BLOCK 2 FULL SCOPE:
[S] Single-column 89mm, 300 DPI, vector, structural design diagram.
[C] Confirmed: left = randomized holdout (same high-propensity list, random split, ~15% withheld from same stratum, treated-mean minus holdout-mean over a window with claims-lag accounting); right = natural experiment / diff-in-diff (policy shock at fixed date, treated = affected physicians, control = matched/neighboring, parallel-trends-before assumption, divergence after). All from the holdout section and the AMC-detailing example.
[O] Two panels on shared time baseline. Left: list → random-split node → treated (large) + holdout (small, same stratum) → compare node. Right: timeline with shock marker → parallel pre-trend → post-shock divergence → diff-in-diff node. Treated → dominant blue; holdout/control → secondary orange; the parallel-trends pre-segment and randomization node → green (the identifying move); shock marker → neutral black tick.
[P] Flat vector, white background, Okabe-Ito with hex (treated #0072B2, control/holdout #E69F00, identifying move #009E73, shock marker #000000, anchors #56B4E9, strokes #000000), 1pt strokes, single-headed arrows.
[E] Exclude: numeric counts (2,126 / 24,593 etc. are flagged-for-verify — do not bake in); no map imagery; the parallel-trends segment must be visibly parallel before the shock; no more than two groups per panel.

BLOCK 3 NEGATIVE PROMPT:
specific physician counts, hard-coded numbers, map imagery, non-parallel pre-trend lines, more than two groups per panel, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Video candidate pass

**FIGURE 1 — The propensity-vs-incrementality inversion**
- **Status:** Recommend as video candidate (single, ~1/chapter).
- **Criterion:** Transition mechanism is the learning target. The chapter's spine is a *re-derivation of intuition*: the reader starts believing "target the high-propensity physicians" and must be moved to "target the persuadables in the middle." That shift is a transformation between two mental pictures — the propensity ranking and the incremental-effect curve — which animation can stage as one morphing into the other.
- **Reason:** A static inverted-U asserts the conclusion. A short animation can begin with a monotonically rising propensity curve (the wrong instinct), then sweep across it to reveal the *room to move* shrinking at the high end, collapsing the rising line into the inverted-U where the peak migrates to the middle. Watching the peak slide off the high-propensity tail to the persuadable center makes the inversion felt, not just stated — and the inversion is the one idea the chapter says it is "built on."
- **Suggested format:** 12–16s silent loop, white background, Okabe-Ito; phase 1 rising propensity intuition, phase 2 "room to move" indicator shrinking at the right tail, phase 3 line reshaping into the inverted-U with the peak settling over the mid-range, phase 4 the two tail zones dimming to neutral. No narration text. Recommend; do not auto-select.

_Other strong candidates considered and held as static: the Qini curve (Fig 4) animates well but is a summary statistic, not a mechanism the way the inversion is; the three-biases decomposition (Fig 2) is a stacking story better read static. One video per chapter — the inversion wins._
