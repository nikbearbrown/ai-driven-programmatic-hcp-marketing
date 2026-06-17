# CAJAL Figure Report — Chapter 14: From Prototype to Product Decision (The Fellow's Brief)
_Mode: /scan silent · 2026-06-16 · source: chapters/14-prototype-to-product-decision.md_

## Density recommendation

This is a strong process-flowchart and decision-gate chapter. Its spine is a four-stage research-to-product pipeline mapped onto the Evidence Ladder, with a firewall between Stage 1 and Stage 2, feeding a conjunctive five-criterion decision tree whose terminal verdicts are TEST / BUILD / KILL, and inside that tree a patient-welfare gate that holds veto power. The four welfare-trigger patterns are a secondary taxonomy. Recommended density: **4 figures** — one Critical (the conjunctive decision tree with the welfare veto, the chapter's machinery and already author-flagged), one Critical (the four-stage pipeline with the firewall, also author-flagged), one Important (the four welfare-gate trigger patterns), one Supplementary (the verdict-distribution / criterion-pass logic). Both author HTML comments (the four-stage pipeline TABLE and the decision-tree DIAGRAM) are confirmed and extended here. One video candidate is genuinely warranted (the decision tree as a sequential gate-by-gate traversal) — see final section.

## Figures

---

FIGURE 1 — Conjunctive five-criterion decision tree with welfare veto · Critical · Type: decision flowchart · Heuristic: MC + VG

BLOCK 1 ILLUSTRAE PASTE:
Render a top-down decision flowchart beginning at a single root node representing a scored project. From the root, descend through five sequential decision gates, each a diamond, in this fixed order: evidence strength at or above Level 3; magnitude commercially meaningful; compliance risk manageable; patient-welfare gate passed; build cost tractable. Each diamond has a downward pass path that continues to the next gate and a side fail path that exits to a terminal verdict. The failing exits route as the chapter specifies: failing evidence strength exits to a TEST-or-KILL terminal; failing magnitude exits to KILL; failing compliance exits to a TEST terminal marked flag-first; failing the welfare gate exits to a KILL-or-escalate terminal; failing build cost exits to TEST. Passing all five reaches the single BUILD terminal at the bottom. Draw the welfare-gate diamond with a heavier, distinct border to mark its veto authority. Use single-headed arrows on the pass path descending and on each fail path exiting sideways. Single column, flat vector, white background, no baked text.

BLOCK 2 FULL SCOPE:
[S] single-column 89mm, 300DPI, vector, textbook figure (tall orientation).
[C] Five gates in chapter order, all chapter-confirmed: (1) evidence strength ≥L3; (2) magnitude commercially meaningful; (3) compliance risk manageable; (4) patient-welfare gate passed; (5) build cost tractable. Fail routes chapter-confirmed: evidence fail → TEST/KILL; magnitude fail → KILL; compliance fail → TEST (flag first); welfare fail → KILL or escalate; cost fail → TEST. All-pass → BUILD. Conjunctive structure chapter-confirmed ("must pass all of them"). Welfare gate veto/emphasis chapter-confirmed ("welfare gate shown in red to signal veto power").
[O] Vertical spine: root → 5 diamonds top-to-bottom on the pass path → BUILD terminal at bottom. Each diamond emits one sideways fail arrow to a terminal box (TEST, KILL, TEST/KILL, KILL/escalate per the gate). Three terminal types: BUILD, TEST, KILL. Single-headed arrows (→) throughout; no block markers. Welfare diamond emphasized.
[P] flat vector, white bg, Okabe-Ito with hex; pass-path arrows #000000 1pt. Welfare-gate diamond border #D55E00 (blocking/veto) — used instead of literal red to stay Okabe-Ito; other diamonds neutral gray 1pt. BUILD terminal outline #009E73 (active/go), KILL terminals outline #D55E00 (blocking), TEST terminals outline #56B4E9 (anchor/hold). White fills.
[E] Exclude: criterion text or verdict words baked into shapes (TEST/BUILD/KILL distinguished by terminal color and shape, not baked letters); reordering the five gates; collapsing the conjunctive chain into parallel branches (it is sequential AND); literal red fill (use #D55E00 outline for veto); dual-headed arrows; the four welfare trigger patterns (that is Figure 3); the four-stage pipeline (Figure 2); shadows; more than three terminal verdict types.

BLOCK 3 NEGATIVE PROMPT:
reordered gates, parallel branches instead of sequential gates, literal red fill, baked verdict words, baked criterion text, more than five gates, dual-headed arrows, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

FIGURE 2 — Four-stage research-to-product pipeline with the gate-1/gate-2 firewall · Critical · Type: linear staged process with boundary · Heuristic: MC + VG

BLOCK 1 ILLUSTRAE PASTE:
Render a left-to-right pipeline of four stages as four boxes in sequence connected by single-headed arrows. Stage one is open research, owned by the Fellow, on public data, reaching up to Level 3. Stage two is proprietary replication, owned by the partner, running the prospective holdout on internal data, reaching Level 4. Stage three is a working prototype built inside the partner environment, reaching Level 5. Stage four is a monitored, resourced deployment, reaching Level 6. Beneath each stage box, show a small ascending evidence-level indicator so that the level rises across the four stages from a low region under stage one to the top region under stage four. Draw one prominent vertical boundary line between stage one and stage two to mark the firewall — the point where ownership transfers from Fellow to partner and where public data ends and proprietary data begins. Give stage one a distinct color to mark it as the Fellow's sole stage and the other three a shared partner color. Single column, flat vector, white background, no baked text.

BLOCK 2 FULL SCOPE:
[S] single-column 89mm, 300DPI, vector, textbook figure (landscape-leaning).
[C] Four stages chapter-confirmed: 1 open research / Fellow / public data / L0–L3; 2 proprietary replication / partner / holdout on internal data / L4; 3 prototype / partner / client context / L5; 4 resourced feature / partner / monitored deployment / L6. Firewall between Stage 1 and Stage 2 chapter-confirmed ("firewall indicated between Stages 1 and 2"; "the Fellow's job ends at the gate-1-to-gate-2 handoff"). Rising evidence level across stages chapter-confirmed.
[O] Four boxes left→right, single-headed connector arrows between them. Vertical firewall rule between box 1 and box 2 (⊣ / hard boundary, full height). Small ascending level bars beneath each box (L≤3, L4, L5, L6) — a four-step staircase, y-baseline at zero. Ownership shown by box color (Fellow vs partner).
[P] flat vector, white bg, Okabe-Ito with hex; connector arrows #000000 1pt. Stage 1 box outline #0072B2 (Fellow / dominant); Stages 2–4 box outlines #E69F00 (partner / secondary). Firewall rule #D55E00 (blocking boundary). Level staircase bars neutral gray, baseline from zero. White fills.
[E] Exclude: stage names, owner names, or level numbers baked as text (rendered in the companion table at line 24, not in art); more or fewer than four stages; firewall placed anywhere but between 1 and 2; descending or flat level indicator (must rise); dual-headed arrows; the decision tree (Figure 1); shadows; staircase bars not anchored to a zero baseline.
[NOTE: author flagged this as a TABLE at line 24; this figure is the schematic-art companion showing sequence + firewall + rising ladder, which the table alone cannot convey spatially.]

BLOCK 3 NEGATIVE PROMPT:
firewall in wrong position, descending level indicator, baked stage names, baked level numbers, more than four stages, floating level bars not anchored to zero, dual-headed arrows, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

FIGURE 3 — The four patient-welfare gate trigger patterns · Important · Type: 2×2 taxonomy of trigger cases · Heuristic: VG

BLOCK 1 ILLUSTRAE PASTE:
Render a two-by-two grid of four equal cells, each cell representing one pattern that triggers the patient-welfare gate. The four patterns are: suppression of clinically appropriate generic substitution, the coupon case; targeting physician susceptibility rather than patient need, the proxy case; moving prescribing of low-clinical-value drugs, the ICER-mismatch case; and intensifying embedded messaging in the safety-alert layer, the EHR case. Give each cell a simple flat geometric glyph that distinguishes the four mechanisms — for example a divergence motif for generic suppression, a targeting motif for susceptibility, a low-value indicator for the ICER mismatch, and a layered-overlap motif for the safety-alert intensification — keeping every glyph in the same flat line style with no realism. Enclose the four cells in a single outer boundary and give the whole grid one shared accent color to signal that all four feed the same gate and all four can veto a commercially positive result. Single column, flat vector, white background, no baked text.

BLOCK 2 FULL SCOPE:
[S] single-column 89mm, 300DPI, vector, textbook figure.
[C] Four trigger patterns chapter-confirmed and explicitly enumerated: (1) suppression of clinically appropriate generic substitution (coupon case); (2) targeting physician susceptibility rather than patient need (proxy case); (3) moving prescribing of low-clinical-value drugs (ICER-mismatch case); (4) intensifying EHR-embedded messaging in the safety-alert layer (the opening case). All four named in the welfare-gate section.
[O] 2×2 grid, four equal cells, one outer boundary. Each cell holds one abstract flat glyph keyed to its mechanism [glyph designs inferred — chapter names mechanisms, not icons]. No arrows between cells (these are parallel triggers, not a sequence). Shared accent to bind them to one gate.
[P] flat vector, white bg, Okabe-Ito with hex; cell borders and glyphs #D55E00 (blocking — these are veto triggers), 1pt. Outer boundary #000000 1pt. White fills.
[E] Exclude: pattern names or case labels baked as text; more or fewer than four cells; arrows implying sequence/ranking among the four; photorealistic icons; the decision tree; the pipeline; shadows; any implication that one trigger outranks another (they are co-equal). Mark glyph choices "[inferred]" — the chapter specifies mechanisms, not iconography.

BLOCK 3 NEGATIVE PROMPT:
sequence arrows between cells, ranked or numbered cells, more than four cells, baked pattern names, photorealistic icons, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

FIGURE 4 — Conjunctive criteria: any single fail blocks BUILD · Supplementary · Type: logic strip / AND-gate schematic · Heuristic: VG

BLOCK 1 ILLUSTRAE PASTE:
Render a horizontal strip of five aligned criterion cells representing the five conjunctive decision criteria, all feeding rightward into a single convergence point that represents the BUILD outcome. The five cells are evidence strength, magnitude, compliance risk, the patient-welfare gate, and build cost. Draw a single-headed connector from each cell to the convergence node to show that all five must hold for the convergence to resolve to BUILD. To depict the conjunctive rule, show one of the five cells in a failed state with its connector terminating in a blocking perpendicular bar before the convergence, so the reader sees that one failure alone prevents BUILD and diverts to a non-BUILD outcome. Keep the four passing cells in an active state and the single failing cell in a blocking state, with the convergence node neutral until all inputs pass. Align all five cells on a common baseline and keep spacing uniform. Single column, flat vector, white background, no baked text.

BLOCK 2 FULL SCOPE:
[S] single-column 89mm, 300DPI, vector, textbook figure.
[C] Five conjunctive criteria chapter-confirmed: evidence strength, lift/association magnitude, compliance risk, patient-welfare gate, build cost. Conjunctive logic chapter-confirmed ("must pass all of them to reach BUILD. Failing any one produces a TEST or a KILL"). The illustrative single-fail-blocks-BUILD case is a teaching depiction of that rule [the specific failing cell shown is inferred / illustrative — any of the five could be the failing one].
[O] Five cells in a row, each → a central convergence node (AND-gate semantics). Four connectors pass (→), one connector blocked (⊣ perpendicular bar before the node). Convergence node = BUILD, shown neutral/ungated because one input failed. Common baseline, uniform spacing.
[P] flat vector, white bg, Okabe-Ito with hex; passing cells outline #009E73 (active), the one failing cell outline #D55E00 (blocking), convergence node neutral gray. Connectors #000000 1pt; block bar #D55E00.
[E] Exclude: criterion names baked as text; more or fewer than five cells; showing BUILD as resolved/green while a cell fails (the node must read un-resolved); implying the failing cell is always the same specific criterion (mark illustrative); the full decision tree (Figure 1 covers routing); shadows. Mark the chosen failing cell "[inferred / illustrative]".

BLOCK 3 NEGATIVE PROMPT:
resolved BUILD node while a criterion fails, more than five cells, baked criterion names, all cells passing, triangle block instead of perpendicular bar, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Video candidate pass

**Status: Recommended (one candidate).**

- **Candidate:** Figure 1 — the conjunctive five-criterion decision tree — as a gate-by-gate sequential traversal.
- **Criterion met:** ≥3 sequential causal stages where the *sequence and the early-exit logic are themselves the learning target*. The chapter's core teaching is that the criteria are conjunctive and ordered, that a project can exit at any gate, and — critically — that the welfare gate can veto a commercially positive project that has already passed earlier gates. That "you can be winning and still get killed at gate 4" dynamic is a transition the reader benefits from watching unfold, not just reading.
- **Reason:** Static Figure 1 shows the topology; the video shows the *traversal* — a project token descending the pass path, surviving evidence/magnitude/compliance, then hitting the welfare gate and diverting to KILL/escalate despite prior passes. This dramatizes the conjunctive rule and the veto in a way the static tree cannot, and it directly answers the chapter's "Still Puzzling" tension about who holds the veto.
- **Suggested format:** 15–25s flat-vector animated walkthrough. A single marker enters at root; each diamond resolves pass (continues down) with a brief hold; at the welfare gate, show two alternative endings — one where it passes to BUILD, one where it vetoes to KILL/escalate — so the veto's override power is explicit. Okabe-Ito only; welfare diamond in #D55E00. No narration text baked into frames.
- **Recommendation:** Worth producing if a video budget exists for this book; it is the single highest-value motion asset across Chapters 13–14. Recommend, do not auto-select — confirm budget before committing.
