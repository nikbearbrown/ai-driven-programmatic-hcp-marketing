# TIKTOC Gap Audit

**Source:** `TIKTOC.md`  
**Generated:** 2026-06-16  
**Book directory:** `/Users/bear/Documents/CoWork/bear-textbooks/books/ai-driven-programmatic-hcp-marketing`

---

## Extracted Chapter List

| Week | Slug | Title | Act |
|---:|---|---|---|
| 01 | the-machine-nobody-sees | The Machine Nobody Sees | The System |
| 02 | lift-vs-brand-the-two-dependent-variables | Lift vs. Brand: The Two Dependent Variables | The System |
| 03 | the-hcp-identity-graph-and-the-targeting-data | The HCP Identity Graph and the Targeting Data | The System |
| 04 | what-todays-ai-stack-actually-does-and-claims | What Today's AI Stack Actually Does (and Claims) | The System |
| 05 | the-evidence-problem | The Evidence Problem | The System |
| 06 | ensembles-and-the-tabular-data-advantage | Ensembles and the Tabular-Data Advantage | The Toolkit |
| 07 | mixture-of-experts-and-related-routing-models-and-when-the-word-is-marketing | Mixture of Experts and Related Routing Models (and When the Word Is Marketing) | The Toolkit |
| 08 | uplift-and-incrementality-measuring-real-lift | Uplift and Incrementality: Measuring Real Lift | The Toolkit |
| 09 | brand-association-as-a-measurable-outcome | Brand Association as a Measurable Outcome | The Toolkit |
| 10 | llms-for-commercial-research-and-content-intelligence | LLMs for Commercial Research and Content Intelligence | The Toolkit |
| 11 | the-external-innovation-lab-operating-model-and-the-ip-firewall | The External Innovation Lab Operating Model (and the IP Firewall) | The Lab |
| 12 | research-design-and-public-data-for-marketing-science | Research Design and Public Data for Marketing Science | The Lab |
| 13 | the-fellow-research-portfolio-run-one | The Fellow Research Portfolio (Run One) | The Lab |
| 14 | from-prototype-to-product-decision-the-fellows-brief | From Prototype to Product Decision (The Fellows Brief) | The Lab |

Total: 14 chapters / weeks.

---

## Manuscript Chapter Gap

Current `chapters/` contents:

- `00-frontmatter.md`
- `01-introduction.md`
- `02-chapter-01.md`
- `99-back-matter.md`

Missing or not yet aligned with `TIKTOC.md`:

| Needed file | Status |
|---|---|
| `chapters/01-introduction.md` | Exists, but should be checked against new TIKTOC framing |
| `chapters/02-the-machine-nobody-sees.md` | Missing; old `02-chapter-01.md` should likely be renamed or replaced |
| `chapters/03-lift-vs-brand-the-two-dependent-variables.md` | Missing |
| `chapters/04-the-hcp-identity-graph-and-the-targeting-data.md` | Missing |
| `chapters/05-what-todays-ai-stack-actually-does-and-claims.md` | Missing |
| `chapters/06-the-evidence-problem.md` | Missing |
| `chapters/07-ensembles-and-the-tabular-data-advantage.md` | Missing |
| `chapters/08-mixture-of-experts-and-related-routing-models-and-when-the-word-is-marketing.md` | Missing |
| `chapters/09-uplift-and-incrementality-measuring-real-lift.md` | Missing |
| `chapters/10-brand-association-as-a-measurable-outcome.md` | Missing |
| `chapters/11-llms-for-commercial-research-and-content-intelligence.md` | Missing |
| `chapters/12-the-external-innovation-lab-operating-model-and-the-ip-firewall.md` | Missing |
| `chapters/13-research-design-and-public-data-for-marketing-science.md` | Missing |
| `chapters/14-the-fellow-research-portfolio-run-one.md` | Missing |
| `chapters/15-from-prototype-to-product-decision-the-fellows-brief.md` | Missing |

Note: the file numbering above keeps `01-introduction.md` and starts the TIKTOC Week 1 chapter at `02-...`, matching the current repo pattern. If the build expects Week 1 to be `02`, `book.md` and the chapter manifest should be updated together.

---

## Research Notes Gap

No chapter-specific notes exist yet in the requested `NN-slug_notes.md` format.

Recommended notes files:

| Notes file | Coverage from existing pantry | Gap level |
|---|---|---|
| `01-the-machine-nobody-sees_notes.md` | Partial: `pharma-ai-hcp-marketing-synthesis.md`, `pharma-marketing-evidence-synthesis.md` | Medium |
| `02-lift-vs-brand-the-two-dependent-variables_notes.md` | Strong: `pharma-brand-measurement-synthesis.md` | Low |
| `03-the-hcp-identity-graph-and-the-targeting-data_notes.md` | Partial: `pharma-ai-hcp-marketing-synthesis.md` | Medium |
| `04-what-todays-ai-stack-actually-does-and-claims_notes.md` | Strong but needs verification updates | Medium |
| `05-the-evidence-problem_notes.md` | Partial: `pharma-marketing-evidence-synthesis.md` | Medium |
| `06-ensembles-and-the-tabular-data-advantage_notes.md` | Strong: `moe-vs-ensemble-synthesis.md` | Low |
| `07-mixture-of-experts-and-related-routing-models-and-when-the-word-is-marketing_notes.md` | Strong: `moe-vs-ensemble-synthesis.md` | Low |
| `08-uplift-and-incrementality-measuring-real-lift_notes.md` | Weak: needs causal/uplift-specific research | High |
| `09-brand-association-as-a-measurable-outcome_notes.md` | Strong: `pharma-brand-measurement-synthesis.md`; needs added survey/implicit association sources | Medium |
| `10-llms-for-commercial-research-and-content-intelligence_notes.md` | Weak: needs LLM evaluation/MLR/content research | High |
| `11-the-external-innovation-lab-operating-model-and-the-ip-firewall_notes.md` | Partial: planning docs only | High |
| `12-research-design-and-public-data-for-marketing-science_notes.md` | Weak: needs Open Payments, Part D, ICER, DiD/RDD/IV source work | High |
| `13-the-fellow-research-portfolio-run-one_notes.md` | Partial: `risks.md` and `TIKTOC.md`; needs project-by-project public-data feasibility | High |
| `14-from-prototype-to-product-decision-the-fellows-brief_notes.md` | Partial: planning docs only | High |

---

## Shared Library Scan: Likely Relevant Files

The shared Markdown library at `/Users/bear/Documents/CoWork/bear-textbooks/MD` contains broad supporting material, but little obviously pharma-HCP-specific material.

Most relevant candidates:

| Library file | Likely relevance |
|---|---|
| `math-causal-inference.md` | Chapters 8, 12 |
| `math-causal-inference-mit-press-essential-knowledge-series.md` | Chapters 8, 12 |
| `science-the-book-of-why-the-new-science-of-cause-and-effect.md` | Chapters 8, 12 |
| `ai-applied-causal-inference-powered-by-ml-and-ai.md` | Chapters 8, 12 |
| `math-how-to-measure-anything-finding-the-value-of-intangibles-in-business.md` | Chapters 2, 9, 14 |
| `math-the-art-of-statistics-how-to-learn-from-data.md` | Chapters 5, 8, 12 |
| `math-naked-statistics-stripping-the-dread-from-the-data.md` | Chapters 5, 8, 12 |
| `math-how-to-lie-with-statistics.md` | Chapters 5, 8, 12 |
| `science-calling-bullshit-the-art-of-skepticism-in-a-data-driven-world.md` | Chapters 4, 5, 14 |
| `science-science-fictions-how-fraud-bias-negligence-and-hype-undermine-the-search-for.md` | Chapters 5, 14 |
| `ai-prediction-machines-the-simple-economics-of-artificial-intelligence.md` | Chapters 4, 5, 14 |
| `ai-artificial-intelligence-a-guide-for-thinking-humans.md` | Chapters 4, 10 |
| `ai-the-alignment-problem-machine-learning-and-human-values.md` | Chapters 10, 14 |
| `ai-gigo.md` | Chapters 3, 4, 10 |
| `math-weapons-of-math-destruction-how-big-data-increases-inequality-and-threatens-dem.md` | Chapters 3, 13, 14 |
| `business-data-ism-the-revolution-transforming-decision-making-consumer-behavior-and-al.md` | Chapters 1, 3 |
| `business-the-lean-startup-how-today-s-entrepreneurs-use-continuous-innovation-to-create.md` | Chapters 11, 14 |
| `business-flawless-consulting-4th-edition.md` | Chapters 11, 14 |
| `prompts/peer-review-and-research-paper-development-protocol.md` | Chapters 10, 11, 13 |
| `prompts/branding-tool-pitch-master-prompt-set.md` | Chapters 9, 14 |
| `prompts/brand-identity-strategy-and-style-guide-prompt-set.md` | Chapter 9 |
| `prompts/source-to-textbook-chapter-transformer.md` | Chapter drafting support |

Recommended next step: copy only the top 10-15 library files into `pantry/` with `_lib_` prefixes, then create chapter notes. Avoid copying the broad unrelated matches from `rg`; there are many false positives.

---

## High-Priority Research Gaps

1. **Week 8: Uplift and Incrementality**
   - Needs current uplift modeling references, causal marketing measurement, holdout design, and pharma-specific attribution critique.

2. **Week 10: LLMs for Commercial Research and Content Intelligence**
   - Needs current LLM evaluation, LLM-as-judge limitations, marketing-bias research, regulatory/fair-balance workflow sources.

3. **Week 12: Public Data and Research Design**
   - Needs concrete public dataset documentation: CMS Open Payments, Medicare Part D Prescribers, ICER reports, FDA enforcement data, state policy variation.

4. **Week 13: Fellow Portfolio**
   - Needs feasibility notes for each proposed track: what public data exists, what success threshold is plausible, and what product owner would care.

5. **Act III Partner/IP Firewall**
   - Needs a practical policy memo: what can live in the public repo, what belongs in `private/`, and how Fellows can write pointed critiques without leaking partner IP or creating relationship risk.

---

## Structural Notes

- The new `TIKTOC.md` is stronger than `full-toc-draft.md` because it adds:
  - public-data-only methodology,
  - partner/IP firewall,
  - 14-week course/fellowship structure,
  - assessment points,
  - Part A / Part B research thread,
  - five-part AI exercise blocks,
  - explicit blocker around Graham/partner framing.
- The existing `outline.md`, `architecture.md`, `chapters-spec.md`, and `README.md` still reflect the earlier 12-chapter architecture and should be updated if `TIKTOC.md` is now canonical.
- The current `chapters/02-chapter-01.md` is not aligned with the new chapter slug/title.
