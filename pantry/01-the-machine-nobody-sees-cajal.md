# CAJAL Figure Report — Chapter 01: The Machine Nobody Sees
_Mode: /scan silent · 2026-06-16 · source: chapters/01-the-machine-nobody-sees.md_

## Density recommendation
6 figures, Mixed density — the chapter alternates structural anomalies (split agency, identity primitive) with multi-step mechanisms (interoperability rails, the closed loop) and one clean quasi-experimental quantitative result, so it needs a blend of systems diagrams, comparison tables, a sequence diagram, and one bar chart.

## Figures

---

FIGURE 1 — The split-agency structure that breaks consumer sovereignty · Priority: Critical · Type: Systems diagram · Heuristic: VG

BLOCK 1 — ILLUSTRAE PASTE BLOCK:
Create a flat vector systems diagram, single-column 89mm width at 300 DPI, showing the four-party structure of the pharmaceutical transaction. Place four labeled nodes: a prescriber (physician), a patient, a payer (insurer), and an institution (formulary committee or PBM). Draw three distinct flow types between them as separate arrow styles: a decision flow running from prescriber toward the prescription act, a consumption flow from prescription to patient, and a payment flow from payer covering the cost. The defining feature is an asymmetry: the payer's payment arrow has no corresponding return arrow connecting it back to the decision node, and the institution constrains the menu of choices from the side. Render the prescriber node as the primary anchor in sky blue, the absent-feedback payer node in vermillion to mark the missing discipline, the patient and institution in neutral gray and orange. Keep all four nodes on one plane, evenly spaced, with clean orthogonal connectors. Show that the party who pays sits outside the decision loop.

BLOCK 2 — FULL SCOPE:
[S - SPECIFICATION] Single column, 89mm width, 300 DPI, vector, textbook style, white background.
[C - CONTENT] Four nodes confirmed in text: prescriber (decides/writes), patient (consumes/takes), payer (pays majority of cost), institution (constrains menu). Three flows confirmed: decision flow, consumption flow, payment flow. Key confirmed asymmetry: payer's payment arrow has no return arrow to the decision node; payer is "not at the table." Institution role as menu-constraint is confirmed.
[O - ORGANIZATION] Four nodes in a balanced arrangement; arrows typed by function (→ for decision/consumption/payment progression); the missing feedback edge from payer to decision left visibly absent (do not draw a dashed "could-be" arrow unless labeled [inferred]).
[P - PRESENTATION] Flat vector, white bg, Okabe-Ito: prescriber #56B4E9 (primary anchor), payer #D55E00 (the absent-discipline party), patient light gray, institution #E69F00, arrows #000000, uniform 1pt strokes.
[E - EXCLUSIONS] Omit the running-shoes/consumer-sovereignty contrast example; omit dollar figures and the Part D gifts statistic; omit the co-pay card mechanism (its own figure); omit NPI/identity machinery; omit any depiction of the EHR or CDS Hooks; omit the principal-agent textbook framing as on-canvas text; omit drug names.

BLOCK 3 — NEGATIVE PROMPT:
five or more nodes, return arrow from payer to decision, dollar signs, currency symbols, drug packaging, EHR screen, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

FIGURE 2 — Web cookie vs. NPI as identity primitives · Priority: Critical · Type: Comparison panels · Heuristic: VG

BLOCK 1 — ILLUSTRAE PASTE BLOCK:
Create a flat vector side-by-side comparison panel, single-column 89mm width at 300 DPI, contrasting two identity primitives across a shared set of attribute rows. The left panel represents a web cookie; the right panel represents the National Provider Identifier (NPI). Use a shared horizontal axis of five attribute rows aligned across both panels: durability, accuracy, link to behavior, regulatory status, and targeting precision. Render the cookie side as the weaker/probabilistic primitive using neutral gray fills and a frayed or decaying visual weight at the row level, and the NPI side as the deterministic primitive using a solid primary-anchor treatment. Keep the two columns strictly aligned row-for-row so the reader can scan each attribute horizontally. The conceptual point to encode spatially is that the cookie is probabilistic, decaying, and loosely linked, while the NPI is permanent, accurate, and directly tied to prescribing behavior. Leave all cells blank of text; build only the aligned comparison scaffold and the differential visual weight.

BLOCK 2 — FULL SCOPE:
[S - SPECIFICATION] Single column, 89mm width, 300 DPI, vector, textbook style, white background.
[C - CONTENT] Two primitives confirmed: web cookie (probabilistic, decays, gets cleared, loosely maps device→person) vs. NPI (deterministic, permanent, accurate, tied to real prescribing behavior, 10-digit, federal). Five comparison rows confirmed/implied by text: durability, accuracy, link to behavior, regulatory status, targeting precision.
[O - ORGANIZATION] Two vertical panels mapped to a shared 5-row reference axis; horizontal scanning per attribute; no flow arrows.
[P - PRESENTATION] Flat vector, white bg, Okabe-Ito: NPI column #0072B2 (dominant conceptual element, deterministic), cookie column light gray (neutral/weak), 1pt strokes.
[E - EXCLUSIONS] Omit the bid-by-NPI auction mechanic; omit the NPI-list-compilation pipeline; omit the identity graph (Chapter 3 subject); omit any actual cookie data or browser imagery; omit dollar figures; omit drug names; do not bake attribute text into cells.

BLOCK 3 — NEGATIVE PROMPT:
browser windows, actual cookie icons, IP address strings, drug packaging, more than five comparison rows, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

FIGURE 3 — The two clinical interoperability rails commercial messages ride · Priority: Critical · Type: Process flowchart (sequence) · Heuristic: MC

BLOCK 1 — ILLUSTRAE PASTE BLOCK:
Create a flat vector sequence/process flowchart, single-column 89mm width at 300 DPI, showing how a commercial card gets inside the EHR through the CDS Hooks trigger flow. Lay out a single horizontal left-to-right sequence of five stages connected by progression arrows: a physician clinical action, the EHR firing a hook, an external commercial service receiving that hook, the service returning a card, and the card rendering in the EHR sidebar. Above the action stage, mark three discrete trigger events as small parallel entry points feeding the same hook stage (chart opened, order being selected, order being signed). Color the EHR/clinical-rail stages as the structural anchor and the external commercial service stage in a transitional/composite color to mark that a commercial actor has entered a clinical channel. Use uniform single-headed arrows for the forward sequence only. Keep exactly these stages; do not add the SMART on FHIR OAuth handshake as a second track in this figure. Leave all stages unlabeled.

BLOCK 2 — FULL SCOPE:
[S - SPECIFICATION] Single column, 89mm width, 300 DPI, vector, textbook style, white background.
[C - CONTENT] Confirmed CDS Hooks flow: physician action → EHR fires HTTP hook → external service receives hook → service returns card → card renders in EHR sidebar. Confirmed three mature hook triggers: patient-view (chart opened), order-select (order being chosen), order-sign (order about to be signed). Note: figure scoped to CDS Hooks only; SMART on FHIR is a separate figure to respect the 6-8 component limit (named split point).
[O - ORGANIZATION] Horizontal L→R, 5 sequential stages with → progression; three trigger sub-events feed the hook stage as parallel entry points.
[P - PRESENTATION] Flat vector, white bg, Okabe-Ito: EHR/clinical stages #56B4E9 (clinical anchor), external commercial service #CC79A7 (composite/transitional — commercial entering clinical), arrows #000000, 1pt strokes.
[E - EXCLUSIONS] Omit SMART on FHIR / OAuth 2.0 handshake (separate figure); omit the iframe/Hyperspace detail; omit the opening Z87.891 smoking-cessation case walkthrough; omit vendor names (Doceree, OptimizeRx, WebMD); omit point-of-care spend figures; omit the co-pay card step; do not depict a realistic EHR screenshot.

BLOCK 3 — NEGATIVE PROMPT:
realistic EHR screenshot, OAuth token graphics, iframe browser chrome, vendor logos, drug packaging, dual-track parallel diagram, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

_Split point: the SMART on FHIR app-launch sequence (OAuth 2.0 token exchange → context claims → app renders in iframe) is a companion figure. Recommended if the chapter wants both rails depicted; otherwise this CDS Hooks figure carries the core mechanism._

---

FIGURE 4 — Co-pay coupon effect on branded-drug volume, commercial vs. Medicare Advantage · Priority: Critical · Type: Statistical / quantitative (bar chart) · Heuristic: PQ

BLOCK 1 — ILLUSTRAE PASTE BLOCK:
Create a flat vector bar chart, single-column 89mm width at 300 DPI, presenting the estimated effect of co-pay coupon introduction on branded-drug prescribing volume, from the Dafny, Ody, and Schmitt natural experiment. The y-axis represents percent change in quantity of drugs without generic substitutes and must start at zero. Show one primary bar representing the estimated 23 to 25 percent increase in the commercial segment where coupons are permitted, rendered as a single bar or a narrow range band spanning 23 to 25. Show the Medicare Advantage segment, where coupons are federally banned, as the zero/baseline reference. Apply the Proportional Ink Rule strictly: bar height proportional to value, no truncated axis, no 3D. Use the disruptive/negative semantic color for the coupon-driven volume increase to mark it as the suppression-of-substitution effect, and neutral gray for the banned-segment baseline. Leave numerals and axis text off the image; build only the proportioned bars and the zero baseline.

BLOCK 2 — FULL SCOPE:
[S - SPECIFICATION] Single column, 89mm width, 300 DPI, vector, textbook style, white background, y-axis from zero.
[C - CONTENT] Confirmed from Dafny et al. (NBER w29735, AEJ: Policy): commercial segment (coupons permitted) showed a 23-25% increase in quantity of drugs without generic substitutes; Medicare Advantage (coupons federally banned) serves as the quasi-experimental control/baseline. The contrast between segments isolates the coupon effect. [Note: the secondary "8% higher net-of-rebate price" and "49% had a generic equivalent" figures are confirmed in text but belong in separate small charts or annotation, not this bar; the Georgetown "60%" figure is flagged [verify] in source — do not visualize.]
[O - ORGANIZATION] Two-category bar chart on a shared zero-based y-axis; commercial bar shown as a 23-25 range band; MA baseline at/near zero.
[P - PRESENTATION] Flat vector, white bg, Okabe-Ito: commercial coupon effect #D55E00 (suppresses substitution / raises system cost), MA baseline light gray, axis lines #000000, 1pt strokes.
[E - EXCLUSIONS] Omit the 8% net-price and 49%-generic-equivalent figures from this bar (separate treatment); omit the unverified Georgetown 60% figure entirely; omit the co-pay card UI; omit the opening clinical case; omit drug names; no 3D bars, no axis truncation.

BLOCK 3 — NEGATIVE PROMPT:
truncated y-axis, axis not starting at zero, 3D bars, pie chart, line chart, drug packaging, dollar bills, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

FIGURE 5 — The closed commercial loop and the counter-stack nobody built · Priority: Important · Type: Comparison panels (mirror systems diagram) · Heuristic: VG / MC

BLOCK 1 — ILLUSTRAE PASTE BLOCK:
Create a flat vector mirror diagram, single-column 89mm width at 300 DPI, placing two parallel closed loops side by side on a shared central axis. The left loop is the funded commercial system, a closed cycle of five stages: NPI targeting, point-of-care impression, prescription, attribution, and refined targeting feeding back to the start. The right loop is the counter-stack that the same infrastructure could run but does not: comparative-effectiveness data, generic-alternative display, formulary-tier data, patient cost, feeding into the prescribing decision. Render the left commercial loop as a complete, solid, self-reinforcing cycle in the active/operational color. Render the right counter-stack loop in light gray with a clearly unfilled or open quality to signal it is unfunded and hypothetical. Keep both loops to five nodes each, mirrored across the center line so the structural symmetry — same plumbing, only one funded — is immediately legible. Use single-headed progression arrows around each loop. Leave all nodes unlabeled.

BLOCK 2 — FULL SCOPE:
[S - SPECIFICATION] Single column, 89mm width (consider 120mm if mirror feels cramped), 300 DPI, vector, textbook style, white background.
[C - CONTENT] Left loop confirmed: NPI list → bid-time decision/impression → prescription → attribution (via claims) → tighten next NPI list → loop. Right loop confirmed as hypothetical: comparative-effectiveness → generic alternative → formulary tier → patient cost → prescribing decision. Confirmed framing: "the same infrastructure could run both systems; only one is funded." Mark the right loop as [unfunded / does not exist] — not a real operating system.
[O - ORGANIZATION] Two mirrored cycle diagrams across a vertical center axis; closed-loop arrows on both; left solid, right open/gray.
[P - PRESENTATION] Flat vector, white bg, Okabe-Ito: commercial loop #009E73 (active/operational), counter-stack loop light gray (neutral/absent), arrows #000000, 1pt strokes.
[E - EXCLUSIONS] Omit academic-detailing program names (VA, NPS MedicineWise, Therapeutics Initiative); omit the CDS Hooks mechanism detail (Figure 3); omit the attribution-circularity teardown (Chapter 5); omit dollar/spend figures; omit drug names; do not imply the counter-stack exists by rendering it as solid/active.

BLOCK 3 — NEGATIVE PROMPT:
solid filled counter-stack loop, more than five nodes per loop, vendor logos, dollar signs, EHR screenshot, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

FIGURE 6 — Mechanism claims vs. effectiveness claims in a vendor page · Priority: Important · Type: Comparison panels (classification) · Heuristic: VG

BLOCK 1 — ILLUSTRAE PASTE BLOCK:
Create a flat vector two-group classification diagram, single-column 89mm width at 300 DPI, sorting the phrases of a vendor product-page claim into two distinct categories along a shared evidentiary axis. The left group holds mechanism claims — "reaches the right HCP" (an identity-layer claim) and "at the right clinical moment" (a trigger-layer claim). The right group holds the single effectiveness claim — "44% script lift." Place a vertical divider between the groups representing the evidentiary threshold: mechanism claims sit on the credible/plausible side, the effectiveness claim sits on the unverified side requiring a control group. Render the two mechanism claim blocks in the active/plausible color and the lone effectiveness claim block in the contested/unverified color, visibly marked as standing alone on its side to show it is the only claim requiring causal evidence. The effectiveness claim must be encoded as vendor-claimed and contested, not as established fact. Keep to three claim blocks total plus the dividing threshold. Leave all blocks unlabeled.

BLOCK 2 — FULL SCOPE:
[S - SPECIFICATION] Single column, 89mm width, 300 DPI, vector, textbook style, white background.
[C - CONTENT] Confirmed classification: "reaches the right HCP" = identity/mechanism claim (plausible); "at the right clinical moment" = trigger/mechanism claim (plausible); "44% script lift" = effectiveness claim requiring causal evidence, unverified, attribution-circular. FIREWALL NOTE: the 44% lift figure is a vendor-claimed / contested figure (attribution circularity — the platform that served the ad also measured the lift); it must be shown as contested, never as established effect.
[O - ORGANIZATION] Two groups split by a vertical evidentiary-threshold divider; mechanism group (2 blocks) left, effectiveness group (1 block, isolated) right.
[P - PRESENTATION] Flat vector, white bg, Okabe-Ito: mechanism/plausible blocks #009E73, effectiveness/contested block #D55E00 (contested, unverified), divider #000000, 1pt strokes.
[E - EXCLUSIONS] Omit the three-questions framework (KPI/data/evidence) as on-canvas text; omit any "true/false" verdict (the claim is unproven, not false — do not depict an X or checkmark on the effectiveness block); omit vendor name; omit the LLM exercise; omit drug names.

BLOCK 3 — NEGATIVE PROMPT:
checkmark or X marks implying true/false, more than three claim blocks, vendor logos, percentage numerals rendered as effect, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Video candidate pass

FIGURE 1 — Split-agency structure
Status: STATIC SUFFICIENT
Criterion met: none
Reason: A structural anomaly with no temporal transition; the missing feedback edge is best inspected at the reader's own pace.

FIGURE 2 — Cookie vs. NPI comparison
Status: STATIC SUFFICIENT
Criterion met: none
Reason: Side-by-side attribute comparison; no mechanism of change to animate.

FIGURE 3 — CDS Hooks interoperability rail
Status: VIDEO CANDIDATE
Criterion met: Criterion 1 (transition mechanism is the learning target) and Criterion 2 (3+ sequential causal stages)
Reason: The core misconception the chapter fights is "EHR ads are banner ads bolted on"; static panels show the stages but a stepwise animated trace of physician action → hook fires → service returns card → card renders inside the clinical tier makes the "rides the clinical rails" mechanism land in a way arrows only approximate.
Suggested format: short looping animation or narrated walkthrough that lights up each stage in sequence.

FIGURE 4 — Co-pay coupon volume effect
Status: STATIC SUFFICIENT
Criterion met: none
Reason: A two-bar quantitative comparison; motion would add nothing.

FIGURE 5 — Closed loop vs. counter-stack
Status: STATIC SUFFICIENT (borderline)
Criterion met: Criterion 3 partially (cyclical, return-to-start matters)
Reason: The closed self-reinforcing loop is conceptually cyclical, but the learning target is the structural symmetry (same plumbing, one funded), which a static mirror reads more clearly than a spinning animation; reserve the chapter's one video for Figure 3.

FIGURE 6 — Mechanism vs. effectiveness claims
Status: STATIC SUFFICIENT
Criterion met: none
Reason: A classification sort with no transition.

Video candidates identified: 1 (with Figure 5 borderline). Recommended for production: Figure 3 — the CDS Hooks trigger flow, because the chapter's central conceptual correction ("delivered through the clinical interoperability layer, not bolted on") depends on the reader seeing the commercial card arrive through the same plumbing as a safety alert, which animation conveys better than static arrows. Remaining figures are well-served by static treatment.
