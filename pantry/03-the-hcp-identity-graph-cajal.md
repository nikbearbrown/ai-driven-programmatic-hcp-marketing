# CAJAL Figure Report — Chapter 03: The HCP Identity Graph and the Targeting Data
_Mode: /scan silent · 2026-06-16 · source: chapters/03-the-hcp-identity-graph.md_

## Density recommendation
6 figures, Mechanistic density — the chapter is dominated by pipelines and mechanisms (de-identification pipeline, Masterfile join, propensity feature vector, claims-lag timeline, omnichannel feedback loop) plus one contested susceptibility-proxy comparison, so it leans heavily on process/systems diagrams with one comparison panel.

## Figures

---

FIGURE 1 — De-identification removes the patient and leaves the prescriber · Priority: Critical · Type: Process flowchart (two-track pipeline) · Heuristic: MC / VG

BLOCK 1 — ILLUSTRAE PASTE BLOCK:
Create a flat vector two-column pipeline diagram, single-column 89mm width at 300 DPI, showing how a single prescription is stripped of patient identity while the prescriber identity survives. Run a horizontal left-to-right pipeline through stages: pharmacy fill, payer processing, broker, pharma buyer, model, and bid. In the upper track, show patient identifiers (name, date of birth, address) being removed at the payer step under Safe Harbor — render these as crossed-out or dropping-away elements that do not continue past the payer. In the lower track, show the National Provider Identifier as a single persistent token that passes intact through every subsequent stage to the bid. The conceptual point to encode is the asymmetry: the patient is erased early, the physician identifier survives end to end. Color the persisting NPI token as the primary structural anchor carried through all stages, and the dropped patient identifiers in the blocking/removal color shown terminating at the payer step. Keep to the six pipeline stages and the two tracks. Leave all text off the image.

BLOCK 2 — FULL SCOPE:
[S - SPECIFICATION] Single column, 89mm width (consider 120mm for the two-track length), 300 DPI, vector, textbook style, white background.
[C - CONTENT] Confirmed: patient fills script → claim flows to payer → payer strips identifiers under Safe Harbor (name, DOB, address removed) → remaining: de-identified patient record, drug, quantity, year-resolved date, and NPI. NPI (10-digit, CMS-assigned, not a patient identifier, not on Safe Harbor list) persists. Confirmed downstream stages: broker, pharma buyer, model, bid. Confirmed output: "NPI wrote 47 statin scripts last month" — anonymous w.r.t. patient, fully identified w.r.t. physician. [NOTE: source caption typo "NCP" should read "NPI".]
[O - ORGANIZATION] Horizontal L→R pipeline; upper track = patient identifiers dropping out at payer (⊣/termination); lower track = NPI persisting (→ through all stages).
[P - PRESENTATION] Flat vector, white bg, Okabe-Ito: persisting NPI token #0072B2 (dominant anchor), dropped patient identifiers #D55E00 (removed/terminated), stage nodes light gray, arrows #000000, 1pt strokes.
[E - EXCLUSIONS] Omit the full 18-identifier Safe Harbor list (only show the 3 named examples as dropping tokens); omit Expert Determination as a parallel route (mention only, separate concern); omit the Masterfile join (Figure 2); omit vendor names; omit drug names beyond a generic token; do not bake field names as legible text.

BLOCK 3 — NEGATIVE PROMPT:
all 18 identifiers listed, legible field-name text, vendor logos, drug packaging, more than six stages, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

FIGURE 2 — The Masterfile join: from anonymous NPI to named prescriber profile · Priority: Critical · Type: Systems diagram · Heuristic: MC / VG

BLOCK 1 — ILLUSTRAE PASTE BLOCK:
Create a flat vector join diagram, single-column 89mm width at 300 DPI, showing how two separate data sources combine on physician identity to produce a sellable prescriber profile. On the left, place two distinct input sources: de-identified prescribing records (NPI-keyed behavior) and the AMA Physician Masterfile (physician identity, name, specialty, affiliation). Draw both flowing into a central join operation linked on physician identity (NPI, historically also DEA number). From the join, draw a single output flowing right: prescriber-level data — a named physician profile with prescribing behavior attached. Render the de-identified prescribing source and the Masterfile source as two separate secondary-colored inputs converging on the join, the join node itself as the composite/transitional element where identity is reattached, and the resolved prescriber profile output as the primary anchor. The point to encode is that neither input alone is commercially useful; the join is what creates the product. Keep to two inputs, one join, one output. Leave all text off the image.

BLOCK 2 — FULL SCOPE:
[S - SPECIFICATION] Single column, 89mm width, 300 DPI, vector, textbook style, white background.
[C - CONTENT] Confirmed: input A = de-identified prescribing records (NPI-keyed); input B = AMA Physician Masterfile (licensed by data-mining firms); join key = physician identity (NPI, historically DEA); output = prescriber-level data (named physician + prescribing behavior + switching pattern). Confirmed model originator IMS Health; successor IQVIA. Confirmed insight: NPI alone is "commercially useless" without the join.
[O - ORGANIZATION] Two inputs (left) → central join node → one output (right); → convergence then → progression.
[P - PRESENTATION] Flat vector, white bg, Okabe-Ito: two inputs #E69F00 (secondary sources), join node #CC79A7 (composite — identity reattached), prescriber-profile output #0072B2 (the product/anchor), arrows #000000, 1pt strokes.
[E - EXCLUSIONS] Omit vendor market-share figures (IQVIA 90%, 11M profiles — these are flagged [verify] self-descriptions, not depictable facts); omit Symphony/Definitive Healthcare as separate nodes; omit the propensity model (Figure 3); omit the de-identification pipeline detail (Figure 1); omit drug/physician names; do not bake field text into nodes.
[FIREWALL NOTE] Do not render IQVIA's ~90% / 11M-profile self-descriptions as established external facts.

BLOCK 3 — NEGATIVE PROMPT:
vendor market-share numerals, multiple competing vendor nodes, legible field text, drug packaging, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

FIGURE 3 — The propensity-model feature vector: four signal sources · Priority: Critical · Type: Systems diagram · Heuristic: MC / VG

BLOCK 1 — ILLUSTRAE PASTE BLOCK:
Create a flat vector input-aggregation diagram, single-column 89mm width at 300 DPI, showing the four kinds of signal that feed a physician propensity model. Place four labeled source groups feeding into a single central model node that outputs a ranked propensity score: claims-derived features (script volume, switching, loyalty decile), identity and affiliation features (specialty, practice setting, geography), behavioral and digital features (journal reads, CME, endemic-platform visits, email opens), and CMS Open Payments history (disclosed industry payments). Draw all four sources converging on the model node, and one output arrow to a ranked list. Visually distinguish the Open Payments source from the other three: render the first three sources in neutral and secondary colors, and the Open Payments source in the contested/flagged color to mark it as the feature that may encode targetability rather than clinical need. Keep to four input groups, one model node, and one ranked output. Leave all text off the image; build only the four-into-one aggregation with the one source visually flagged.

BLOCK 2 — FULL SCOPE:
[S - SPECIFICATION] Single column, 89mm width, 300 DPI, vector, textbook style, white background.
[C - CONTENT] Confirmed four signal sources: (1) claims-derived (script volume by class, switching, restart, refill, patient-mix proxies, loyalty decile); (2) identity/affiliation (specialty, practice setting, geography, health-system membership); (3) behavioral/digital (journal reads, CME, endemic-platform visits, email opens, search); (4) CMS Open Payments history (meals, speaker/consulting fees, Sunshine Act). Confirmed model output: ranked list of NPIs by predicted prescribing. Confirmed central idea: Open Payments encodes receptiveness/targetability, not patient need.
[O - ORGANIZATION] Four sources (arranged around/left) → central model node → ranked-list output; → convergence then → progression.
[P - PRESENTATION] Flat vector, white bg, Okabe-Ito: claims #56B4E9, identity/affiliation #E69F00, behavioral/digital light gray, Open Payments #D55E00 (contested/flagged feature), model node #0072B2, output arrow #000000, 1pt strokes.
[E - EXCLUSIONS] Omit the two-physician susceptibility comparison (Figure 4); omit the claims-lag timeline (Figure 5); omit detailed feature lists as baked text (show grouped sources only); omit drug names.
[FIREWALL NOTE] The susceptibility-proxy construct is the book's flagged position, not established fact ("whether real models weight it heavily is an open empirical question"). Color-flag Open Payments to raise the question; do NOT depict it as a proven discriminatory weighting.

BLOCK 3 — NEGATIVE PROMPT:
proven-weighting depiction, full feature-list text, more than four input groups, drug packaging, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

FIGURE 4 — Two identical physicians, divergent propensity scores · Priority: Important · Type: Comparison panels · Heuristic: VG

BLOCK 1 — ILLUSTRAE PASTE BLOCK:
Create a flat vector side-by-side comparison panel, single-column 89mm width at 300 DPI, contrasting two hypothetical cardiologists who are clinically identical but score differently on a propensity model. Build two aligned columns, Physician A and Physician B, with four shared horizontal rows: specialty, patient-mix proxy for the eligible condition, Open Payments meals over the last three years, and predicted propensity score. Encode that the first three clinical rows are identical between the two physicians (same specialty, same patient mix), while only the Open Payments row differs — Physician A has a multi-year meal history, Physician B has none. Show the resulting propensity-score row diverging: Physician A higher, Physician B lower, despite identical clinical context. Render the matching clinical rows in neutral gray to signal equivalence, the differing Open Payments row in the contested/flagged color, and the diverging score row to mark the consequence. Keep to two columns and four rows. Leave all cell text off the image; build only the aligned scaffold showing three matched rows and one divergent row driving a divergent outcome.

BLOCK 2 — FULL SCOPE:
[S - SPECIFICATION] Single column, 89mm width, 300 DPI, vector, textbook style, white background.
[C - CONTENT] Confirmed: Physician A = high Open Payments meal history (3 years); Physician B = no Open Payments history; both identical patient mix, same specialty, same comorbidity/eligibility. Confirmed result: propensity model may rank A higher — not because A's patients are better candidates but because A has been more moveable by industry contact. Four rows confirmed in source's table call-out: specialty, patient-mix proxy, Open Payments meals (last 3 yrs), predicted propensity score.
[O - ORGANIZATION] Two columns mapped to 4 shared rows; three rows visibly identical, one row (Open Payments) divergent, driving a divergent score row.
[P - PRESENTATION] Flat vector, white bg, Okabe-Ito: matched clinical rows light gray (equivalence), Open Payments row #D55E00 (the flagged differentiator), divergent score row #0072B2, 1pt strokes.
[E - EXCLUSIONS] Omit the four-source feature vector (Figure 3); omit any verdict that the model IS discriminatory (chapter flags this as open); omit drug/physician real names; do not bake row text into cells.
[FIREWALL NOTE] This visualizes the susceptibility-proxy construct, which is contested/flagged, not established. Depict it as a hypothetical illustration of the open question ("a propensity model MAY rank the meal-history physician higher"), never as demonstrated fact.

BLOCK 3 — NEGATIVE PROMPT:
discrimination verdict marks, real physician names, more than four rows, drug packaging, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

FIGURE 5 — The claims-data lag: where targeting error lives · Priority: Important · Type: Timeline / progression · Heuristic: MC

BLOCK 1 — ILLUSTRAE PASTE BLOCK:
Create a flat vector two-track timeline diagram, single-column 89mm width at 300 DPI, contrasting the slow claims-data path against a real-time EHR trigger. On the upper track, lay out the claims-data lag as a horizontal sequence with widening time gaps: prescription written at day zero, pharmacy adjudication at days one to three, payer processing at days seven to fourteen, broker aggregation at days fourteen to thirty, monthly model refresh, then targeting list deployed. On the lower track, lay out a parallel real-time path: clinical event at day zero leading almost immediately to a bid. Align both tracks to a shared horizontal time axis so the reader sees the large gap between event and targeting signal on the upper track versus the near-zero gap on the lower track. Render the slow claims track in neutral gray to mark it as the lagging, error-prone path, and the real-time EHR track in the active color to mark immediacy. The point to encode is that the gap between event and targeting signal is where targeting error lives. Keep to the six claims stages and the two-stage real-time track. Leave all text off the image.

BLOCK 2 — FULL SCOPE:
[S - SPECIFICATION] Single column, 89mm width (consider 120mm for timeline length), 300 DPI, vector, textbook style, white background.
[C - CONTENT] Confirmed claims-lag stages: Rx written (Day 0) → pharmacy adjudication (Day 1-3) → payer processing (Day 7-14) → broker aggregation (Day 14-30) → model refresh (monthly) → targeting list deployed. Confirmed parallel real-time track: clinical event (Day 0) → bid. Confirmed concept: dynamic NPI activation ingests real-time EHR signals to bypass the lag; the event-to-signal gap is where targeting error lives.
[O - ORGANIZATION] Two horizontal tracks on a shared time axis; upper = 6-stage claims lag with growing gaps (→); lower = 2-stage real-time (→); aligned for gap comparison.
[P - PRESENTATION] Flat vector, white bg, Okabe-Ito: claims-lag track light gray (lagging/error-prone), real-time EHR track #009E73 (immediate/active), time axis #000000, 1pt strokes.
[E - EXCLUSIONS] Omit the attribution-error compounding narrative as text (Chapter 8 handoff); omit the PHI-leaving-EHR privacy thread; omit the propensity feature vector (Figure 3); omit vendor names (OptimizeRx/DAAP); omit drug names; do not bake day-range numerals as legible text (encode as spacing).

BLOCK 3 — NEGATIVE PROMPT:
legible day-range numerals, vendor logos, more than six claims stages, drug packaging, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

FIGURE 6 — The identity graph enriched by its own use: omnichannel feedback loop · Priority: Critical · Type: Cycle diagram · Heuristic: MC / VG

BLOCK 1 — ILLUSTRAE PASTE BLOCK:
Create a flat vector circular feedback diagram, single-column 89mm width at 300 DPI, showing how the NPI profile is continuously enriched by the targeting it drives. Place a single NPI profile node at the center. Draw three spokes outward to three activation channels: CRM (rep call logs), endemic media (banner click data), and EHR triggers (prompt responses). For each spoke, draw a return arrow flowing engagement signals back from the channel into the central profile, so each channel both receives targeting and feeds the model. The conceptual point to encode is the closed feedback structure: the profile is not a static dataset queried once but a continuously updating portrait refined by its own activation. Render the central NPI profile as the primary anchor, the three channels as secondary elements, and the return signal arrows as the active/operational color to emphasize the enrichment flow. Keep to one center node and three channels with bidirectional connections. Leave all text off the image; build only the hub-and-spoke cycle with outbound targeting and inbound engagement signals.

BLOCK 2 — FULL SCOPE:
[S - SPECIFICATION] Single column, 89mm width, 300 DPI, vector, textbook style, white background.
[C - CONTENT] Confirmed: central NPI profile; three channels — CRM (Veeva/OCE+/Salesforce, rep call logs), endemic media (Medscape/WebMD/journals, click data), EHR-integrated triggers (prompt responses). Confirmed feedback: every engagement signal (call answered/declined, banner clicked, prompt dismissed) flows back into the profile; the model targeting today is partly built from how the physician responded to being targeted last month. Confirmed framing: omnichannel orchestration; "the graph is enriched by targeting."
[O - ORGANIZATION] Hub-and-spoke cycle: NPI profile center; 3 spokes out (targeting →) and 3 return arrows in (engagement signal → model update); closed-loop semantics where return-to-center is the concept.
[P - PRESENTATION] Flat vector, white bg, Okabe-Ito: NPI profile center #0072B2 (anchor), three channels #E69F00 (secondary), return engagement arrows #009E73 (active enrichment), outbound arrows #000000, 1pt strokes.
[E - EXCLUSIONS] Omit the worked Dr. Martinez next-best-action example as baked text; omit vendor names as labels; omit the Sorrell legal material; omit drug names; do not exceed three channels; do not bake channel text into nodes.

BLOCK 3 — NEGATIVE PROMPT:
more than three channels, vendor logos, legible channel text, drug packaging, text labels, words, gibberish letters, titles, captions, decorative borders, realistic textures, plastic wrap effects, drop shadows, gradient backgrounds, photographic elements, non-standard arrows, dual-headed arrows, hand-drawn styles, sketch lines, human figures (unless explicitly requested), visual clutter, overlapping unaligned paths, fuzzy borders, watermarks, red-green color combinations, rainbow color scales, 3D perspective distortion

---

## Video candidate pass

FIGURE 1 — De-identification pipeline
Status: STATIC SUFFICIENT (borderline)
Criterion met: Criterion 2 partially (sequential stages)
Reason: The patient-drops / NPI-persists asymmetry is the learning target and reads cleanly as a static two-track pipeline; an animation of identifiers falling away could help, but static lets the reader compare the two tracks at leisure.

FIGURE 2 — Masterfile join
Status: STATIC SUFFICIENT
Criterion met: none
Reason: A convergence/join is a structural relationship, not a transition mechanism; static is clearer.

FIGURE 3 — Four-source feature vector
Status: STATIC SUFFICIENT
Criterion met: none
Reason: An aggregation structure; the flagged Open Payments source is best held still for inspection.

FIGURE 4 — Two-physician comparison
Status: STATIC SUFFICIENT
Criterion met: none
Reason: A side-by-side comparison of a contested construct; motion would risk implying the divergence is demonstrated rather than hypothetical.

FIGURE 5 — Claims-data lag timeline
Status: STATIC SUFFICIENT
Criterion met: none (time element alone does not qualify)
Reason: The event-to-signal gap is a spatial comparison of two tracks on a shared axis; static panels map it precisely and allow gap measurement by eye.

FIGURE 6 — Omnichannel feedback loop
Status: VIDEO CANDIDATE
Criterion met: Criterion 3 (cyclical process where return-to-start is the concept)
Reason: The chapter's core claim is that the graph "is not a static dataset queried but a continuously updating portrait enriched by its own use" — the return-to-center enrichment IS the mechanism, and an animated loop showing targeting go out and engagement signals flow back to update the profile conveys the self-reinforcing cycle in a way static return-arrows only suggest.
Suggested format: looping animation showing one cycle of outbound targeting and inbound engagement-signal enrichment.

Video candidates identified: 1 (with Figure 1 borderline). Recommended for production: Figure 6 — the omnichannel feedback loop, because the chapter explicitly contrasts a static database against a self-enriching graph, and only animation makes the "enriched by its own use" cycle viscerally legible. Figure 1 is well-served by static treatment despite its sequential structure, since the patient-drop/NPI-persist asymmetry rewards self-paced comparison over motion.
