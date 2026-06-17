# CAJAL Figure Report — Chapter 7: Mixture of Experts and Related Routing Models
_Mode: /scan silent · 2026-06-16 · source: chapters/07-mixture-of-experts.md_

## Density recommendation

This chapter is conceptually dense in the architectural-mechanism register but light on numeric distributions. The load-bearing concepts are structural and comparative: the MoE layer mechanism (sparse activation), the two-distinction MoE-vs-stacking contrast, the load-balancing tension, what experts actually specialize in, and the six-question audit. Most existing HTML figure stubs are well-targeted. The PQ heuristic fires in only two places (utilization percentages in the lineage; the Grinsztajn tree-vs-deep benchmark), and one of those (utilization) is a magnitude story worth a clean dot/bar.

Recommended density: **6 figures** (4 already stubbed by the author plus 2 net-new the scan surfaces — the load-balancing tension and the utilization/scale magnitude). This is a Medium-high density chapter: lean toward the Critical/Important figures and let prose carry the lineage list. FIREWALL note: the "genuine MoE vs marketing relabel" distinction is the chapter's spine and must be rendered as a *diagnostic contrast*, never as a settled hierarchy where MoE is "the good one." MoE is shown as the wrong tool for the tabular task; the audit diagnoses mislabeling, not badness.

## Figures

---

FIGURE 1 — Sparse activation in a MoE layer (gating + top-k) · Critical · Diagram · MC

BLOCK 1 ILLUSTRAE PASTE:
Render a single horizontal left-to-right process diagram of one Mixture-of-Experts layer. Begin at the far left with one input node representing a single input x. Draw one arrow from x into a small gating-network box. From the gating box, draw a fan of arrows toward a vertical column of N expert boxes — use eight expert boxes stacked vertically. Show exactly two of the eight expert boxes in the active fill and the remaining six in neutral gray to convey that only k of N experts fire. From the two active experts only, draw arrows converging into a single combine node depicting a weighted sum, and from that node draw one output arrow to a single output node y. Add a thin secondary annotation band beneath the experts contrasting two quantities: total capacity scaling with N versus compute scaling with k, shown as two horizontal magnitude bars of clearly different length. Keep the gating box, expert column, combine node, and output on one clean baseline. Maximum eight expert boxes plus four structural nodes. Use flat vector shapes, white background, single-weight strokes, generous whitespace between the gating fan-out and the convergence so the sparsity is legible at a glance.

BLOCK 2 FULL SCOPE:
[S] Single-column 89mm, 300 DPI, vector, textbook reference figure.
[C] Confirmed: input x; gating network G(x); N experts (N=8 shown); top-k selection (k=2 shown); weighted-sum combination; output y; "capacity scales with N, compute scales with k." All from the formal definition and the author's existing DIAGRAM stub. Eight-expert/top-2 choice is [inferred] illustrative count for legibility, not a claimed configuration.
[O] Horizontal flow x → gate → expert column (2 of 8 active) → weighted-sum combine → y. Secondary magnitude band below: two horizontal bars, capacity (long) vs compute (short). Active experts → green; inactive experts → neutral gray; combine node → composite; input/output anchors → light blue.
[P] Flat vector, white background, Okabe-Ito with hex (active #009E73, inactive neutral gray, combine #CC79A7, anchors #56B4E9, strokes #000000), 1pt strokes, single-headed arrows only.
[E] Exclude: any token/sequence imagery (this is the abstract layer, not the sequence case); no numeric weights on the arrows; no softmax glyphs or math notation baked in; no third magnitude bar; no more than two active experts; no routing lines drawn from inactive experts.

BLOCK 3 NEGATIVE PROMPT:
math equations, softmax symbols, numeric weights, token sequences, more than two active experts, routing arrows from inactive experts, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

FIGURE 2 — MoE vs stacking: the two distinctions that matter · Critical · Diagram (structural contrast) · VG

BLOCK 1 ILLUSTRAE PASTE:
Render a two-panel side-by-side structural comparison. The left panel depicts a genuine Mixture of Experts as one unified system: a single outer boundary enclosing a shared input trunk, a column of three expert sub-networks all drawn at identical width and height to convey shared input-output dimensionality, a gating node inside the same boundary, and a convergence to a single output — with a return arrow looping back across the whole enclosure to signify joint end-to-end training and gradient flow through both gate and experts. The right panel depicts a stacked ensemble as separate frozen artifacts: three visibly different component shapes of different sizes and forms, each sealed by a small lock-style frozen marker, their outputs flowing into a separate downstream aggregator box that sits outside and after them, with no return loop — emphasizing that the components were trained first and combined afterward. Place the two panels on a shared horizontal baseline with a slim central divider. Use the differing expert shapes on the right versus the identical expert shapes on the left as the primary visual carrier of the output-standardization point. Maximum three components per side plus structural nodes. Flat vector, white background, generous interior whitespace.

BLOCK 2 FULL SCOPE:
[S] Single-column 89mm, 300 DPI, vector, comparative reference figure.
[C] Confirmed: left = genuine MoE (shared input-output space, identical expert dimensionality, gating inside one system, joint end-to-end training, gradient return loop); right = stacking (incommensurable component outputs, separately trained then frozen, downstream aggregator translates formats, no joint optimization, no co-adaptation). All directly from "The two distinctions that actually separate MoE from stacking."
[O] Two panels, shared baseline, central divider. Left: enclosed system, three identical experts, gate, single output, full-loop return arrow (training). Right: three differently-shaped frozen components, aggregator after them, forward-only arrows. Joint-training loop → green; frozen markers and aggregator → secondary orange; shared output node → composite; anchors → light blue.
[P] Flat vector, white background, Okabe-Ito with hex (active/joint #009E73, frozen/aggregator #E69F00, output #CC79A7, anchors #56B4E9, strokes #000000), 1pt strokes, single-headed arrows; the training return loop is a single-headed curved arrow, not double-headed.
[E] Exclude: a tabular comparison grid (the author's stub is a TABLE; this figure is the *structural* complement, not a re-drawn table — do not bake table rows/columns as text); no verdict glyphs (no check/X declaring one "better"); no more than three components per side; no labels naming specific algorithms.

BLOCK 3 NEGATIVE PROMPT:
table grids, comparison rows as text, check marks, X marks, verdict symbols, ranking arrows, more than three components per side, identical shapes on the stacking side, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

FIGURE 3 — The load-balancing vs specialization tension · Important · Diagram · VG

BLOCK 1 ILLUSTRAE PASTE:
Render a single conceptual diagram of two opposed forces acting on a router's output distribution. At the center place a horizontal row of six small expert bins. Above the bins, draw one force arrow pressing the distribution toward evenness — depict its target as six bins of equal, uniform height. Below the bins, draw an opposing force arrow pulling toward specialization — depict its target as six bins of deliberately unequal heights, some tall and some short, signifying that experts must see systematically different inputs. Between the two targets, render a third small inset state showing expert collapse: of six bins only one or two are filled and the rest are empty, representing routing that concentrates on a handful of experts. Arrange the three states — uniform (balanced), unequal (specialized), and collapsed — as a clean left-to-right or stacked progression with the two opposing force arrows making the conflict explicit. Keep the opposing arrows on a single shared axis so the tension reads as a tug between two endpoints. Maximum three distribution states plus two force arrows. Flat vector, white background, equal-width bins, baselines from zero.

BLOCK 2 FULL SCOPE:
[S] Single-column 89mm, 300 DPI, vector, conceptual figure.
[C] Confirmed: expert collapse (few experts get most routing); load balancing pushes toward uniform routing; specialization requires non-uniform routing; the two objectives genuinely conflict. Three states (uniform, non-uniform, collapsed) all from "The load-balancing problem." Six-bin count is [inferred] for legibility.
[O] Three small bin-distribution states + two opposing single-headed force arrows on one axis (balance-force vs specialization-force). Balance/uniform target → light blue (neutral anchor); specialization target → secondary orange; collapsed state → blocking orange-red (#D55E00) to flag it as the failure mode. Bin baselines from zero.
[P] Flat vector, white background, Okabe-Ito with hex (uniform #56B4E9, specialized #E69F00, collapse #D55E00, force arrows #000000), 1pt strokes, single-headed arrows.
[E] Exclude: the three named mechanisms (aux loss / noisy top-k / DeepSeek bias) — those are a list, not figure material here, do not bake them as text; no equations; no more than three states; bins must not float (baseline at zero).

BLOCK 3 NEGATIVE PROMPT:
floating bars, non-zero baselines, equations, mechanism names as text, more than three distribution states, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

FIGURE 4 — What experts route on: token-type (sequence) vs the open question (tabular) · Important · Infographic · VG

BLOCK 1 ILLUSTRAE PASTE:
Render a two-panel contrast on a shared baseline. The left panel shows a sequence regime: a horizontal row of discrete token cells of distinguishable kinds flowing upward into a single MoE routing node, with each token kind taking a clearly different route to a different expert — the routes color-coded by token type to convey that routing tracks surface token structure, not topic. The right panel shows a tabular regime: a single physician feature vector drawn as a vertical stack of heterogeneous feature cells flowing toward the same routing node, but the route beyond the node is rendered as a single ambiguous, unresolved branch terminating in a prominent open-question marker rather than clean per-type routes — signifying there is no syntactic structure to route on. Keep the two routing nodes vertically aligned across panels so the architecture is held constant while the input regime changes. Make the left side's multiple distinct routes and the right side's single unresolved route the primary visual contrast. Maximum six token cells left, one feature-vector stack right, one routing node each. Flat vector, white background.

BLOCK 2 FULL SCOPE:
[S] Single-column 89mm, 300 DPI, vector, infographic.
[C] Confirmed: in sequence models, MoE routing specializes on token type / syntactic-computational pattern, not semantic domain; tabular NPI input is a feature vector with no token sequence and no syntactic structure; what it routes on is an open question, "probably not physician archetypes." All from "What experts actually specialize in."
[O] Two panels, aligned routing nodes. Left: tokens → distinct color-coded routes to several experts. Right: feature vector → single unresolved route → open-question marker. Token routes use distinct Okabe-Ito hues (no rainbow ramp — discrete categorical only); the open-question marker → blocking #D55E00 to flag the unresolved/contested status; anchors → light blue.
[P] Flat vector, white background, Okabe-Ito with hex (categorical routes from #0072B2, #E69F00, #009E73, #CC79A7; open-question marker #D55E00; anchors #56B4E9; strokes #000000), 1pt strokes, single-headed arrows.
[E] Exclude: literal letters/words inside token cells (use abstract glyph shapes for token "kinds," not text); no claim that archetypes ARE found (the right panel must read as open/unresolved, not as a discovered result); no more than four distinct route colors; no rainbow scale.

BLOCK 3 NEGATIVE PROMPT:
letters in tokens, words in cells, resolved archetype clusters on the tabular side, more than four route colors, rainbow color scales, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, 3D perspective distortion

---

FIGURE 5 — MoE active-parameter utilization across frontier models · Supplementary · Chart (dot/bar) · PQ

BLOCK 1 ILLUSTRAE PASTE:
Render a horizontal bar chart comparing active-parameter utilization for a small set of named MoE systems, where utilization is the fraction of total parameters active per forward pass. Plot four horizontal bars of equal thickness on a value axis that begins at zero and extends to one hundred percent. Bar one represents a system at roughly twenty-eight percent active (the Mixtral-style case, about thirteen of forty-seven). Bar two represents a system at roughly five and a half percent active (the DeepSeek-V3-style case, thirty-seven of six hundred seventy-one). Order the bars from highest to lowest utilization top to bottom so the dramatic sparsity gradient is immediate. Keep the value axis gridless or with one faint reference line, all bars in a single consistent fill, and the zero origin unmistakable. The visual point is the steep drop toward very low utilization as total capacity grows — capacity scales while compute stays sparse. Maximum four bars. Flat vector, white background, uniform bar color, axis from zero.

BLOCK 2 FULL SCOPE:
[S] Single-column 89mm, 300 DPI, vector, quantitative chart.
[C] Confirmed magnitudes from "The genuine MoE lineage": Mixtral ~13B active of ~47B (~28%); DeepSeek-V3 ~37B active of ~671B (~5.5%). Two data points are firm. If a third/fourth bar is added (Llama 4 / Qwen3) mark "[inferred]" — exact ratios not stated in chapter; prefer to render only the two confirmed bars rather than fabricate ratios.
[O] Horizontal bars, sorted high→low utilization, single value axis 0–100% from zero. Single dominant fill (#0072B2) for all bars; no per-bar color coding (this is one measured quantity). One faint reference line acceptable.
[P] Flat vector, white background, Okabe-Ito with hex (bars #0072B2, axis/strokes #000000), 1pt strokes, bars from zero baseline.
[E] Exclude: any bar whose ratio is not stated in the chapter (do not invent Llama 4 / Qwen3 percentages); no model-name text baked in; no second axis; no 3D bars; no gradient fills; no per-bar rainbow coloring.

BLOCK 3 NEGATIVE PROMPT:
invented data values, fabricated percentages, non-zero baseline, second axis, per-bar rainbow coloring, 3D bars, model names as text, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

FIGURE 6 — The six buyer questions audit (checklist + fast screen) · Important · Infographic · MC

BLOCK 1 ILLUSTRAE PASTE:
Render a vertical decision-checklist infographic of a six-step vendor audit. Stack six numbered question slots top to bottom, each with a yes/no branch indicator to its right that resolves toward one of two terminal outcomes at the bottom: a "stacking / not obviously better" outcome and a "genuine MoE — verify benchmark" outcome. Draw the flow so that a no answer on the structural questions (independent training, no shared output space, no joint routing) channels toward the stacking outcome, and a clean yes-pattern channels toward the genuine-MoE outcome. To the side, render a compact three-item inset box representing the fast screen — three criteria (token-level routing; shared trunk and output space; jointly trained) — with a small rule that three no answers terminate at "not MoE." Keep the six slots evenly spaced on one vertical spine with consistent branch geometry; keep the inset visually subordinate. Maximum six question slots, two terminal outcomes, one three-item inset. Flat vector, white background, aligned spine, generous spacing.

BLOCK 2 FULL SCOPE:
[S] Single-column 89mm, 300 DPI, vector, audit infographic.
[C] Confirmed: six buyer questions (component models; trained jointly/independently; shared interfaces vs aggregator translation; routing learned-joint vs separately assigned; routing-layer-within-one-model vs meta-architecture; performance vs tuned XGBoost on an independent benchmark); fast three-criterion screen (token-level routing? shared trunk+output? jointly trained?); "three no answers = stacking." All from "Six buyer questions."
[O] Vertical six-slot spine with yes/no branch glyphs → two terminal nodes. Stacking terminal → secondary orange (diagnostic, NOT failure-red — stacking may be right); genuine-MoE terminal → green; fast-screen inset → neutral gray box; anchors/branch lines → light blue/black.
[P] Flat vector, white background, Okabe-Ito with hex (genuine-MoE terminal #009E73, stacking terminal #E69F00, inset neutral gray, branches #56B4E9, strokes #000000), 1pt strokes, single-headed arrows.
[E] Exclude: the full question text baked as paragraphs (slots are numbered placeholders, not transcribed sentences); do not color the stacking outcome as a failure/red — it is a neutral diagnostic; no more than six slots; no scoring meter (the screen is a sufficient condition, not a rubric).

BLOCK 3 NEGATIVE PROMPT:
full question sentences as text, paragraph blocks, scoring meters, gauges, stacking outcome shown as failure-red, more than six slots, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Video candidate pass

**FIGURE 1 — Sparse activation in a MoE layer**
- **Status:** Recommend as video candidate (single, ~1/chapter).
- **Criterion:** Sub-observable transformation + transition mechanism is the learning target. The whole conceptual payload of MoE is the *act of routing and selective firing* — which experts light up for a given input, and how capacity decouples from compute. That gating-then-sparse-activation dynamic is precisely a process that a static frame compresses.
- **Reason:** A short animation can show the gating vector forming, the top-k selection zeroing all but two experts, the two experts firing while six stay dark, and the weighted sum assembling — making "capacity scales with N, compute with k" visible as motion rather than asserted in a caption. This is the chapter's foundational mechanism; everything downstream (stacking contrast, specialization, audit) depends on the reader internalizing it.
- **Suggested format:** 12–18s silent loop, white background, Okabe-Ito; phase 1 input enters gate, phase 2 gate scores fan out, phase 3 top-2 selection (six experts dim to gray), phase 4 two experts pulse active and outputs converge to y. No narration text; on-screen motion only. Recommend; do not auto-select.

_No other figure in this chapter meets the video bar — Figures 2, 4, 6 are structural/comparative (better static), Figure 3 is a conceptual tension (static), Figure 5 is a magnitude chart (static)._
