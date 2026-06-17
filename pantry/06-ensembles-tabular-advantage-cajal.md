# CAJAL Figure Report — Chapter 06: Ensembles and the Tabular-Data Advantage
_Mode: /scan silent · 2026-06-16 · source: chapters/06-ensembles-tabular-advantage.md_

## Density recommendation
For this text I recommend **6 figures using Mechanistic density**. This chapter is dense with prime figure material: the bias-variance-covariance decomposition and its covariance floor (the chapter's central mathematical mechanism), the three ensemble paradigms (bagging/boosting/stacking), the Grinsztajn tree-vs-deep-learning benchmark, the discrimination-vs-calibration distinction, the four-quadrant evaluation checklist, and the claims-lag illusion of lift. The ensemble mechanics and calibration are explicitly flagged as prime figure material. Most are MC (mechanism) figures the reader cannot reconstruct from prose. One firewall note: the Grinsztajn benchmark is a peer-reviewed independent result (NeurIPS 2022 Datasets & Benchmarks) — it may be rendered as established, but the bar-chart figure must be marked as a *qualitative reproduction* `[verify against paper]`, not a re-measurement.

## Figures

---

### FIGURE 1 — The bias-variance-covariance decomposition and the covariance floor · Critical · Mechanism cross-section (three numbered panels) · MC
The chapter's central mathematical mechanism: averaging shrinks variance toward zero but covariance sets an irreducible floor. Three panels show single model → 10-model ensemble → N→∞ floor.

**BLOCK 1 — ILLUSTRAE PASTE BLOCK**
Create a single-column three-panel mechanism figure, 89mm wide at 300 DPI, textbook style, white background. Arrange three equal panels left to right, each showing a stacked vertical bar representing total ensemble error decomposed into components. In panel one, the bar has two stacked segments: a lower bias-squared segment and a larger upper variance segment. In panel two, the variance segment is visibly smaller and a new third covariance segment appears between them, so the total bar is shorter. In panel three, the variance segment has shrunk nearly to nothing while the covariance segment remains substantial, and a horizontal dashed floor line is drawn across at the height of bias-squared plus covariance. Hold the bias-squared segment identical in height across all three panels to show it never changes. Color bias-squared in the neutral anchor tone, variance in the secondary tone, and covariance in the blocking tone to mark it as the limiting term. Leave all segments and the floor line blank and unannotated. Uniform 1pt strokes, flat fills, y-axis from zero, no 3D, no shadows, no gradients, maximum eight components.

**BLOCK 2 — FULL SCOPE**
- **[S]pecification** — Single-column 89mm, 300 DPI, vector, textbook default; y-axis (error) from zero.
- **[C]ontent** — Three confirmed panels: (1) single model error = bias² + variance; (2) 10-model ensemble = bias² + shrunken variance + emerging covariance; (3) N→∞ = bias² + covariance with variance ≈ 0, dashed floor line at bias² + covar. Bias² constant across panels (averaging cannot reduce it — confirmed). All chapter-confirmed from the formula.
- **[O]rganization** — Three numbered panels left→right; stacked-bar decomposition; constant bias² baseline; covariance floor line in panel 3. → progression of N increasing.
- **[P]resentation** — Flat vector, white bg. Bias² #0072B2 (constant anchor); variance #E69F00 (shrinking); covariance #D55E00 (the floor-setting limit). Dashed floor line #000000. 1pt strokes.
- **[E]xclusions** — No formula text rendered as image; no fourth panel; no covariance segment shown shrinking (it must persist); no bias² changing height between panels; no curve-fitting overlay; no 3D bars.

**BLOCK 3 — NEGATIVE PROMPT**
formula text, fourth panel, shrinking covariance segment, changing bias height, curve overlay, 3D bars, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

### FIGURE 2 — Three ways to manufacture ensemble diversity: bagging, boosting, stacking · Critical · Comparison panels · MC
The three canonical ensemble paradigms shown by their structural difference: parallel-independent, sequential-corrective, and meta-learned combination. Sets up the Chapter 7 punchline that "MoE" is often relabeled stacking.

**BLOCK 1 — ILLUSTRAE PASTE BLOCK**
Create a single-column three-panel comparison figure, 89mm wide at 300 DPI, textbook style, white background. In the left panel, draw several identical base-model nodes arranged in parallel, each receiving an independent input and all feeding into a single averaging node — representing bagging. In the middle panel, draw three model nodes arranged in a left-to-right sequence connected by arrows, where each node passes a residual to the next — representing sequential boosting. In the right panel, draw several diverse base-model nodes in a row all feeding upward into a single meta-learner node positioned above them — representing stacking. Use the primary anchor tone for base-model nodes consistently across all three panels, the active tone for the bagging averaging node, the secondary tone for the boosting sequence arrows, and the composite tone for the stacking meta-learner node. Keep the three panels equal in size and clearly separated. Leave all nodes blank and unannotated. Uniform 1pt single-headed arrows, flat fills, no shadows, no gradients, no 3D, maximum eight components per panel.

**BLOCK 2 — FULL SCOPE**
- **[S]pecification** — Single-column 89mm, 300 DPI, vector, textbook default.
- **[C]ontent** — Three confirmed paradigms: (1) bagging — parallel independent models on bootstrap samples → averaging node (Random Forest); (2) boosting — sequential models each fitting predecessor's residuals (XGBoost/LightGBM/CatBoost); (3) stacking — diverse base models → meta-learner on out-of-fold predictions. Structural difference is the content; all chapter-confirmed.
- **[O]rganization** — Three side-by-side panels mapped to a shared "model nodes" vocabulary. Bagging = parallel→average; boosting = sequential chain; stacking = fan-up to meta-learner.
- **[P]resentation** — Flat vector, white bg. Base-model nodes #56B4E9; bagging averager #009E73; boosting sequence arrows #E69F00; stacking meta-learner #CC79A7. 1pt black single-headed arrows.
- **[E]xclusions** — No algorithm names baked in; no math formulas; no more than ~4 base nodes per panel (avoid clutter); no MoE/router depiction (that is Chapter 7); no performance numbers; no dual-headed arrows in the boosting chain.

**BLOCK 3 — NEGATIVE PROMPT**
algorithm names, math formulas, MoE router, performance numbers, more than four base nodes per panel, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

### FIGURE 3 — Trees vs. deep learning on medium tabular data (Grinsztajn et al. 2022) · Important · Statistical / quantitative (ranked bar) · PQ
Reproduces the qualitative structure of the chapter's anchor benchmark: tree-based methods cluster at the top, deep-learning methods scatter lower across 45 datasets. This is the bar any vendor "AI platform" claim must beat. Peer-reviewed independent result — rendered as a `[verify]` qualitative reproduction.

**BLOCK 1 — ILLUSTRAE PASTE BLOCK**
Create a single-column horizontal ranked bar chart, 89mm wide at 300 DPI, textbook style, white background, with the value axis beginning at zero. Plot roughly six to eight horizontal bars sorted by length from longest at the top to shortest at the bottom, representing methods ranked by average normalized performance. Render the top cluster of bars (the longest two or three) in the active/affirming tone to represent tree-based methods, and the lower bars in the secondary tone to represent deep-learning methods, creating a clear visual break between the top tree cluster and the scattered lower deep-learning group. Keep all bars the same height and uniform spacing. Leave all axis values and bar labels blank and unannotated. Flat fills, thin zero-based axis, minimal gridlines, no 3D, no shadows, no gradients, uniform 1pt strokes, maximum eight bars.

**BLOCK 2 — FULL SCOPE**
- **[S]pecification** — Single-column 89mm, 300 DPI, vector, textbook default; value axis from zero (Proportional Ink).
- **[C]ontent** — Ranked methods by average normalized performance across 45 tabular datasets: tree-based methods (gradient-boosted trees, Random Forest) clustered at top; deep-learning methods (e.g., FT-Transformer, SAINT, MLP) lower and scattered. Qualitative structure of Grinsztajn et al. NeurIPS 2022 Figure 1. FIREWALL: this is a *qualitative reproduction* `[verify figure representation against the paper before publication]`, not a re-measured result.
- **[O]rganization** — Horizontal bars sorted descending; visual break separating top tree cluster from lower DL group.
- **[P]resentation** — Flat vector, white bg. Tree-based bars #009E73 (top performers); deep-learning bars #E69F00. Thin zero-based axis. 1pt black.
- **[E]xclusions** — No precise numeric scores (qualitative only); no more than eight bars; no error bars implying exact reproduced statistics; no TabPFN claim of dominance (the chapter marks tabular DL as not-yet-default); no 3D; no truncated axis.

**BLOCK 3 — NEGATIVE PROMPT**
precise score numbers, fabricated error bars, ninth bar, truncated axis, 3D bars, TabPFN dominance marker, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

### FIGURE 4 — Discrimination vs. calibration: same ranking, wrong probabilities · Critical · Comparison panels · VG
The chapter's load-bearing evaluation distinction: a model can rank perfectly (high AUC) yet be systematically miscalibrated, which silently corrupts every spend decision. Shown as a reliability curve against the diagonal.

**BLOCK 1 — ILLUSTRAE PASTE BLOCK**
Create a single-column two-panel comparison figure, 89mm wide at 300 DPI, textbook style, white background. In the left panel, draw a calibration reliability plot: a square with a 45-degree diagonal reference line from bottom-left to top-right, and a second plotted curve that bows consistently below the diagonal to represent an overconfident model whose predicted probabilities exceed observed rates. In the right panel, draw a ranking representation: a series of correctly ordered items from low to high along an axis, showing that the same model ranks perfectly even while miscalibrated. Color the diagonal reference line in neutral gray, the bowed miscalibration curve in the blocking tone to flag the error, and the correctly-ordered ranking elements in the affirming tone to show discrimination is intact. Keep both panels equal size. Leave all axes, curves, and elements blank and unannotated. Uniform 1pt strokes, flat fills, axes from zero, no 3D, no shadows, no gradients, maximum seven components.

**BLOCK 2 — FULL SCOPE**
- **[S]pecification** — Single-column 89mm, 300 DPI, vector, textbook default; calibration axes 0–1.
- **[C]ontent** — Left: reliability curve with 45° perfect-calibration diagonal and an overconfident curve bowing below it (predicted > observed). Right: correctly ordered ranking showing AUC/discrimination intact despite miscalibration. The chapter's confirmed point: high AUC can coexist with severe miscalibration; calibration is co-equal for spend decisions and load-bearing for Chapter 8 CATE. All chapter-confirmed.
- **[O]rganization** — Two panels: calibration (curve vs. diagonal) and discrimination (ordered ranking), sharing the "same model" frame.
- **[P]resentation** — Flat vector, white bg. Diagonal reference gray; miscalibration curve #D55E00; intact ranking #009E73. 1pt black axes.
- **[E]xclusions** — No Brier-score number; no third panel; no multiple curves cluttering the reliability plot (one diagonal + one curve only); no histogram bins unless minimal; no AUC numeric value; no implication miscalibration changes the ranking.

**BLOCK 3 — NEGATIVE PROMPT**
Brier score number, AUC numeric value, multiple reliability curves, third panel, dense histogram bins, ranking-changes-with-calibration implication, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

### FIGURE 5 — The four-quadrant model-evaluation checklist · Important · Hierarchy/taxonomy (2×2 quadrant) · VG
The chapter's named evaluation artifact: discrimination, calibration, temporal validation, subgroup robustness — pass all four to earn the baseline; passing only the first is the common mistake.

**BLOCK 1 — ILLUSTRAE PASTE BLOCK**
Create a single-column 2-by-2 quadrant diagram, 89mm wide at 300 DPI, textbook style, white background. Draw a square divided by one vertical and one horizontal divider into four equal quadrants. Place a small distinct glyph in each quadrant: a ranking/ordering glyph in the first quadrant for discrimination, a curve-against-diagonal glyph in the second for calibration, a split-timeline glyph in the third for temporal validation, and a segmented-groups glyph in the fourth for subgroup robustness. Color all four quadrant glyphs in the primary structural anchor tone to read as equal co-requirements, and tint the four quadrant backgrounds in a neutral light gray. Emphasize the first quadrant's border slightly to mark it as the one most commonly mistaken as sufficient. Keep glyphs simple and schematic. Leave all glyphs and quadrants blank of text and unannotated. Uniform 1pt strokes, flat fills, no 3D, no shadows, no gradients, maximum eight components.

**BLOCK 2 — FULL SCOPE**
- **[S]pecification** — Single-column 89mm, 300 DPI, vector, textbook default.
- **[C]ontent** — Four confirmed quadrants: (1) discrimination (AUC/AUPRC — "can it rank?"); (2) calibration (reliability curve, Brier — "does the probability mean what it says?"); (3) temporal validation (out-of-time split — "does it hold when the future is the future?"); (4) subgroup robustness (specialty/decile/geography — "where does it fail?"). Quadrant 1 marked as commonly-mistaken-as-sufficient. All chapter-confirmed.
- **[O]rganization** — 2×2 equal quadrants, each carrying one schematic glyph; all four co-equal; quadrant 1 border emphasized.
- **[P]resentation** — Flat vector, white bg. Four glyphs #56B4E9 (co-equal anchors); quadrant tints neutral gray; quadrant-1 emphasis border #000000. 1pt strokes.
- **[E]xclusions** — No more than four quadrants; no failure-mode text; no metric formulas; no ranking that implies one quadrant outranks another (they are co-equal); no fifth check; no checkmark icons implying validation.

**BLOCK 3 — NEGATIVE PROMPT**
fifth quadrant, failure-mode text, metric formulas, checkmark icons, hierarchy implying one quadrant dominates, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

### FIGURE 6 — The claims-lag illusion of lift · Important · Timeline / process · MC
The chapter's pharma-specific landmine: a prescription written before a marketing contact but recorded after it gets miscredited as a response. A timeline showing service date vs. recorded date straddling the exposure window.

**BLOCK 1 — ILLUSTRAE PASTE BLOCK**
Create a single-column horizontal timeline diagram, 89mm wide at 300 DPI, textbook style, white background. Draw one horizontal time axis running left to right. Mark a single vertical exposure-contact line near the center, and shade a post-exposure outcome window as a band extending to the right of that line. Draw two horizontal event markers for a single prescription: a service-date marker positioned to the left of the exposure line (when the script was actually written) connected by a horizontal lag arrow to a recorded-date marker that lands inside the post-exposure window to the right. Render the lag arrow distinctly to show the bookkeeping delay carrying a pre-exposure event into the post-exposure window. Color the exposure line and outcome window in the primary anchor tone, the legitimate service-date marker in neutral gray, and the misattributed recorded-date marker and the lag arrow in the blocking tone to flag the artifact. Leave all markers and axis points blank and unannotated. Uniform 1pt single-headed arrows, flat fills, no 3D, no shadows, no gradients, maximum seven components.

**BLOCK 2 — FULL SCOPE**
- **[S]pecification** — Single-column 89mm, 300 DPI, vector, textbook default.
- **[C]ontent** — One time axis; one exposure-contact line; one post-exposure outcome window (right of the line); one prescription with a service date (left of exposure, legitimately pre-existing) and a recorded/adjudicated date (right of exposure, inside the window) connected by a claims-lag arrow. The confirmed mechanism: late-recorded fills written before contact inflate apparent response. All chapter-confirmed.
- **[O]rganization** — Horizontal timeline; exposure line as pivot; lag arrow carries a pre-exposure service date into the post-exposure window. → left-to-right time.
- **[P]resentation** — Flat vector, white bg. Exposure line + outcome window #56B4E9 (window as light tint); service-date marker neutral gray; recorded-date marker + lag arrow #D55E00 (the artifact). 1pt black single-headed arrows.
- **[E]xclusions** — No second prescription cluttering the timeline; no calendar months rendered as text; no payer/pharmacy/broker icons (the lag is one arrow, not a sub-process); no numeric dates; no implication the lift is real; no dual-headed arrows.

**BLOCK 3 — NEGATIVE PROMPT**
second prescription event, calendar month text, payer broker pharmacy icons, numeric dates, real-lift implication, multi-stage lag sub-process, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Video candidate pass

**FIGURE 1 — Bias-variance-covariance floor**
Status: VIDEO CANDIDATE
Criterion met: (1) transition mechanism is the learning target, and (4) transformation below direct observation — the covariance floor *emerges* as N grows, which is a limiting process students must mentally simulate.
Reason: An animation sweeping N from 1 upward, showing variance collapse toward zero while the covariance segment persists and the floor line settles, makes the limit behavior viscerally clear in a way three static panels only sample. Suggested format: looping animation (N-sweep with settling floor line) or interactive slider on N.

**FIGURE 2 — Bagging / boosting / stacking**
Status: STATIC SUFFICIENT
Criterion met: none (structural contrast, not a single transition mechanism)
Reason: Three architecturally distinct topologies compared side by side; learner-controlled inspection beats motion, and boosting's sequence is adequately shown with arrows.

**FIGURE 3 — Grinsztajn benchmark**
Status: STATIC SUFFICIENT
Criterion met: none
Reason: A ranked snapshot read in one glance.

**FIGURE 4 — Discrimination vs. calibration**
Status: STATIC SUFFICIENT
Criterion met: none
Reason: A two-state comparison; the reliability curve and the intact ranking are both static properties.

**FIGURE 5 — Four-quadrant checklist**
Status: STATIC SUFFICIENT
Criterion met: none
Reason: A reference artifact; no transition.

**FIGURE 6 — Claims-lag illusion**
Status: VIDEO CANDIDATE (weak)
Criterion met: (1) transition mechanism is the learning target — the lag *carrying* a pre-exposure event into the post-exposure window.
Reason: A short animation sliding the recorded-date marker rightward along the lag arrow across the exposure line dramatizes the misattribution; but the static timeline already shows the straddle clearly and serves as a returnable reference. Suggested format: short looping animation (marker sliding across the exposure line).

Video candidates identified: 2 (Figure 1, Figure 6 weak). Recommended for production: Figure 1 — the bias-variance-covariance floor, because the covariance floor is the chapter's central mechanism and its emergence as N→∞ is a limiting process that animation conveys far better than three static snapshots. Figure 6 is well-served by static treatment.
