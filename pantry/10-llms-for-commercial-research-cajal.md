# CAJAL Figure Report — Chapter 10: LLMs for Commercial Research and Content Intelligence
_Mode: /scan silent · 2026-06-16 · source: chapters/10-llms-for-commercial-research.md_

## Density recommendation

This chapter is argument-dense, not data-dense. The conceptual spine is a workflow (generation → validation) with measured failure rates layered on. Recommended density: **4 figures** — two process diagrams (the gap pipeline; the four-layer harness), one quantitative comparison (hallucination by indication type), and one structural/relational figure (the asymmetric-harm convergence). The chapter already carries three author HTML-comment figure stubs; this scan confirms two of them, refines a third, and adds one. Resist over-figuring: the fluency-trap and trust-trap concepts are verbal arguments better left in prose. The LLM-as-judge bias cluster is a legitimate fifth candidate but ranks Supplementary — it competes with the harness figure for the reader's structural attention and is better as a compact named-list in text.

## Figures

---

FIGURE 1 — Useful-draft vs trustworthy-claim pipeline (the gap) · Critical · Process · MC
BLOCK 1 ILLUSTRAE PASTE:
Draw a horizontal two-stage pipeline reading left to right. Place a rounded rectangle on the left labeled as the generation stage, where the language model produces a draft. Draw a solid arrow from it pointing right into a central rounded rectangle representing the validation harness. Draw a second solid arrow from the harness pointing right to a final rounded rectangle on the right representing the trustworthy claim. Between the left rectangle and the central harness, render a visibly wide gap, a deliberate empty horizontal span, that the harness sits inside and bridges. Use a neutral fill for the generation rectangle, a green active fill for the harness, and an anchor-blue fill for the trustworthy-claim endpoint. Show the draft entering the harness carrying small token marks suggesting unverified citations, and the same flow exiting the harness reduced and checked. Keep all three stages on one baseline, evenly weighted, with the arrows as the only horizontal connectors. The composition must make clear that generation and verification are two separate acts and that the harness is the bridge across the gap, not a step inside generation.

BLOCK 2 FULL SCOPE:
- [S] single-col 89mm / 300DPI / vector / textbook.
- [C] Three stages: LLM generates draft; validation harness; trustworthy claim. The "gap this chapter operationalizes" is the named empty span between generation and verification. Draft carries unverified atomic assertions [inferred visual: token marks]; output is reduced/checked.
- [O] Horizontal flow, three nodes on one baseline, two solid single-headed arrows (→). Harness straddles the gap. Reduction shown as fewer marks exiting than entering.
- [P] Flat vector, white bg. Generation = neutral gray; harness = #009E73 (active); trustworthy claim = #56B4E9 (anchor). 1pt strokes.
- [E] No baked text labels, no DOI strings, no human figures, no shadow under nodes, no third intermediate "verification" node duplicating the harness, no dual-headed arrows, no decorative gap fill (gap is empty white).

BLOCK 3 NEGATIVE PROMPT:
text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

FIGURE 2 — Hallucination rate by indication type · Critical · Bar comparison · PQ
BLOCK 1 ILLUSTRAE PASTE:
Draw a simple vertical bar chart with exactly two bars and a y-axis that begins at zero and is scaled in percent. The first bar represents the fabrication rate for a well-studied condition and rises to approximately six percent — a short bar. The second bar represents the fabrication rate for niche conditions and rises to roughly twenty-eight to twenty-nine percent — a tall bar, several times the height of the first. Place the two bars side by side, equal width, with even spacing, baseline aligned to the zero line. Color the short well-studied bar in anchor blue and the tall niche bar in a blocking orange-vermillion to mark it as the high-risk, counterintuitive case. Keep the y-axis a thin neutral line with light horizontal tick guides. Do not add a title, legend, or printed numbers; the relationship is carried by relative bar height alone. The visual claim is that fabrication is highest exactly where the literature is thinnest, so the niche bar must clearly tower over the well-studied bar.

BLOCK 2 FULL SCOPE:
- [S] single-col 89mm / 300DPI / vector / textbook.
- [C] Two categories: well-studied condition ~6%; niche conditions ~28–29%. Source PMC12658395 [verify] — treat magnitudes as contested/approximate. Y-axis from zero, percent scale.
- [O] Two equal-width vertical bars, baseline at zero, light tick guides. Height ratio ~4.5:1 (niche to well-studied).
- [P] Flat vector, white bg. Well-studied = #56B4E9 (anchor); niche = #D55E00 (blocking/high-risk). Y-axis line neutral gray, 1pt.
- [E] No printed values, no title, no legend, no third bar, no GPT-3.5/GPT-4 model-rate bars (different claim — keep separate), no error bars unless source supplies CIs (it does not — omit), no gradient fills.

BLOCK 3 NEGATIVE PROMPT:
text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

FIGURE 3 — The four-layer validation harness (catches / limits) · Critical · Process · MC
BLOCK 1 ILLUSTRAE PASTE:
Draw a vertical stack of four rectangular bands, evenly sized, connected top to bottom by single-headed downward arrows so the flow reads from the first band at the top to the last at the bottom. The top band is citation verification, the second is groundedness scoring, the third is the compliance flag, and the fourth and final band at the bottom is the human capstone. For each of the four bands, attach a small marker on the left edge representing what that layer catches, and a small marker on the right edge representing that layer's limit — so every band has a left catch-marker and a right limit-marker, symmetrically placed. Color the three automated bands — citation verification, groundedness scoring, compliance flag — in a uniform secondary tone, and color the bottom human-capstone band distinctly in active green to mark it as the load-bearing layer. Keep the stack tightly aligned on a shared vertical centerline with the connecting arrows short and straight. The composition must communicate that the three automated layers each have a paired strength and weakness, while the human capstone is the differently-weighted final judge.

BLOCK 2 FULL SCOPE:
- [S] single-col 89mm / 300DPI / vector / textbook.
- [C] Four layers top-to-bottom: citation verification; groundedness scoring; compliance flag; human-in-the-loop capstone. Each automated layer has a "catches" (left) and a "limit" (right) annotation point. Human capstone distinguished as load-bearing.
- [O] Vertical stack, 4 bands, 3 downward single-headed arrows (→ rotated). Left catch-marker + right limit-marker per band. Shared centerline.
- [P] Flat vector, white bg. Three automated bands = #E69F00 (secondary); human capstone = #009E73 (active). Catch-markers neutral; limit-markers #D55E00 (blocking). 1pt strokes.
- [E] No baked text for layer names or catch/limit content, no shadows, no 3D stacking, no funnel taper (bands equal width), no fifth band, no icons inside bands beyond the simple left/right markers.

BLOCK 3 NEGATIVE PROMPT:
text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

FIGURE 4 — Asymmetric-harm convergence: where every control degrades · Important · Structural/relational · VG
BLOCK 1 ILLUSTRAE PASTE:
Draw a convergence diagram in which four separate source nodes on the left each point rightward via single-headed arrows toward one shared target zone on the right. The four left source nodes represent, from top to bottom, fluency raising confidence, hallucination concentrating in niche indications, the LLM-judge backstop weakening in expert domains, and retrieval-augmented synthesis errors surviving. Each of the four arrows converges on a single highlighted region on the right representing the common failure zone — the place where automated reliability is lowest and automated confidence is highest. Inside or beside that shared zone, place one distinct node representing the expert human reviewer, drawn in active green and positioned as the only element that overlaps the failure zone. Render the four source nodes in a uniform neutral tone and the failure zone in a blocking orange-vermillion outline. The four arrows must clearly all terminate at the same region, making the visual claim that independent failure modes all degrade in the same place, and that human review is the single control positioned there.

BLOCK 2 FULL SCOPE:
- [S] single-col 89mm / 300DPI / vector / textbook.
- [C] Four convergent failure modes: fluency↑confidence; hallucination↑ in niche; LLM-judge weakest in expert domains; RAG synthesis errors survive. They converge on one zone (highest automated confidence / lowest automated reliability). One element — expert human reviewer — sits in that zone.
- [O] Four left nodes → one right convergence zone (4 single-headed arrows). Human-reviewer node overlapping the zone. Faithfulness-metric failure could be a 5th source but cap at 4 to stay ≤6–8 components.
- [P] Flat vector, white bg. Source nodes neutral gray; failure zone outline #D55E00 (blocking); human reviewer #009E73 (active). 1pt strokes.
- [E] No baked text, no shadows, no fifth source node (split point: faithfulness-metric degradation named in caption text, not drawn), no regulator/enforcement node (out of figure scope), no dual-headed arrows, no overlapping crossing arrows — fan cleanly into the zone.

BLOCK 3 NEGATIVE PROMPT:
text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

### Supplementary (named, not specced to full blocks)
- **LLM-as-judge bias cluster** (position / verbosity / self-enhancement / sycophancy bias + expert-agreement drop to ~60–68%) · Supplementary · PQ/VG. Strong content but competes with Figure 3 for structural attention; recommend a compact in-text named-list or a small four-icon strip rather than a standalone figure. Split point if elevated: separate the agreement-rate bars (general ~80% vs expert ~60–68%, y from zero) from the four named biases.

## Video candidate pass

**Status:** Recommended (one candidate)
**Candidate:** The evidence scan run through all four harness layers (the worked example: generate → layer 1 → layer 2 → layer 3 → layer 4, with the eight candidates shrinking to four checked papers).
**Criterion:** ≥3 sequential causal stages where the transformation across stages is the learning target — the reader needs to *see* the contaminated draft progressively filtered (8 → drop 2 fabricated → drop 1 misattributed → correct 1 overstated → human verdict). The shrinking/relabeling across stages is sub-observable in a static figure.
**Reason:** A static four-layer figure (Figure 3) shows the *structure*; it cannot show the *attrition dynamic* that is the chapter's payoff ("turned a contaminated draft into a smaller, checked, honestly labeled evidence base"). The progressive drop-and-relabel is the mechanism.
**Suggested format:** ~20–30s stepped animation; one harness layer activates per beat; citation tokens visibly drop out (fabricated), recolor (misattributed/null), and pass through (verified); counter goes 8→5→4. Okabe-Ito only; no narration text baked in. Recommend, do not auto-select — verify production budget against the single-video-per-chapter guideline.
