# Chapter 10 — LLMs for Commercial Research and Content Intelligence (Research Notes)

**Chapter one-line (TIKTOC):** Fellows learn to use LLMs for literature scanning, claims-library mapping, and creative/bias evaluation — with mandatory human validation against the fluency trap. **[METHOD + TEST-DESIGN CHECKPOINT]**

**Spine fit:** Cross-cutting tool, not lift or brand directly — but the discipline (don't trust a fluent output without validating it) governs every measurement claim in both halves. The chapter's named artifact is an *LLM workflow / validation harness*.

**Reuse base:** `pantry/pharma-ai-hcp-marketing-synthesis.md` §4 (MLR acceleration, content generation, the 95%-AI-pilot-failure / governance-not-generation point, FDA 2025 enforcement wave). Library: `_lib_gigo.md` + `_lib_gigo-llm-toc.md` (computational skepticism, hallucinated legal citations), `_lib_prompt-engineering-textbook.md`, `_lib_co-intelligence.md`.

> Sourcing rule: web search returned several **future-dated sources** (2026 arXiv IDs, a Lancet 2026 audit). Headline numbers below are corroborated by clearly-dated 2023–2025 sources; future-dated items are flagged and NOT relied on. See Section G.

---

## A. Conceptual foundations

**1. The useful-draft / trustworthy-claim distinction (the chapter's spine).**
An LLM is excellent at producing a *useful draft* — fluent, plausibly sourced literature summaries, claims-library mappings, message variants. It is NOT trustworthy as the final authority on any factual or promotional claim. A useful draft becomes a trustworthy claim only after **every atomic assertion is verified against a real, correctly-attributed source** and has cleared expert review. The whole chapter operationalizes this gap.

**2. The fluency trap.** LLM output reads as authoritative *regardless of accuracy* — human-like fluency and tone project authority even when content is fabricated. This is why a fluent "evidence summary" is dangerous: confidence is decoupled from correctness. (TechPolicy.Press, "AI Trustwashing": https://www.techpolicy.press/ai-trustwashing-changes-how-consumers-judge-credibility/)

**3. Automation bias / over-reliance.** People over-rely on automated systems, strongest "when the system appears competent and users are trying to save time" — exactly a busy MLR/research workflow under content-volume pressure. Over time the "trust trap" compounds: willingness to question quick authoritative answers decreases as exposure increases. (Over-reliance survey, arXiv 2509.08010: https://arxiv.org/html/2509.08010)

**4. The asymmetric-harm argument for human review (the load-bearing claim).** Human expert review is not a courtesy step; it is the one control that stays reliable exactly where every automated control degrades:
- Fluency raises confidence (A.2)
- Hallucination is *highest* in niche indications (B/D.1)
- The LLM-judge backstop is *weakest* in expert domains (D.2)
- RAG still lets synthesis errors through (D.3)
- Faithfulness metrics miss complex cases (D.5)
- The regulator is *actively penalizing* the resulting defect (D.4)
The only control positioned to catch what all the others miss is an expert *expected to distrust fluent output.*

**5. GIGO framing (from the library).** Computational skepticism is the reliable defense: LLM outputs inherit the structural flaws of their inputs, and scale *amplifies* both the garbage and its consequences. The canonical case study — GPT-4 hallucinating legal citations, traced back to pretraining corpora — is the same failure mode the Fellow must guard against in claims work. (`_lib_gigo-llm-toc.md`, Ch 1.)

---

## B. Domain examples + failure case

**Opening case (from TIKTOC):** An LLM "evidence summary" cites a study that doesn't say what it claims. Two variants of the failure: (a) the cited study is *fabricated* (doesn't exist); (b) the cited study is *real but misrepresented* (wrong DOI, or the paper says something different). Both are routine; (b) is arguably more dangerous because the citation *resolves* and looks legitimate.

**Productive LLM uses in commercial research (where they help):**
- **Literature scanning** — surface candidate papers/claims with provenance, as drafts to verify.
- **Claims-library mapping** — link generated content to pre-approved claims; flag incomplete claims / missing references before human MLR review. (Already a mature pharma use case: Veeva PromoMats Content Agent, late 2025; `pharma-ai-hcp-marketing-synthesis.md` §4.)
- **Creative / message variation + bias evaluation** — generate and triage message variants.
- **Mechanical MLR pre-checks** — decompose content into claims/charts/references, link to approved sources, flag gaps; route to humans for judgment. (Indegene "Regulated Content Orchestrator": https://www.indegene.com/what-we-think/blogs/ai-for-mlr-excellence ; Vodori: https://www.vodori.com/blog/the-future-of-ai-in-medical-legal-and-regulatory-mlr-review)

**Failure case (foreground this): the hallucinated/misattributed citation in a claims library.**
- *Mata v. Avianca* (S.D.N.Y. 2023): attorneys filed a brief citing **six entirely fictitious cases** ChatGPT generated, with fabricated quotations; Judge Castel sanctioned them **$5,000 under Rule 11**. The failure wasn't *using* AI — it was using it as a substitute for verification. (Wikipedia: https://en.wikipedia.org/wiki/Mata_v._Avianca,_Inc. ; Justia Doc. 54: https://law.justia.com/cases/federal/district-courts/new-york/nysdce/1:2022cv01461/575368/54/)
- In a pharma claims library, the analog is a fabricated or misattributed efficacy reference flowing into promotional content — a fair-balance/substantiation defect the FDA is currently penalizing (D.4).

---

## C. Connections

- **To Ch 9 (brand association):** word-embedding association and CME/literature corpus mining are LLM/NLP tasks governed by exactly this validation discipline. A WEAT cosine readout is a "useful draft," not a trustworthy claim, until checked.
- **To Ch 5 (the evidence problem):** Ch 5 teaches association≠causation and rating evidence quality; Ch 10 is the tooling chapter for *doing* that scanning at scale — and the warning that the tool itself fabricates evidence.
- **To Ch 11 (the lab + compliance flags):** AI-generated content is a compliance surface (MLR, fair balance) that gets *flagged and routed to counsel*, never auto-approved. The validation harness is how the lab keeps LLM output on the right side of the firewall and the regulator.
- **To Ch 4 (vendor-claim audit):** the same skepticism applied to vendor "AI/MoE" claims applies to the Fellow's own LLM outputs — don't trust fluency.
- **Checkpoint role:** Ch 10 is the Method + Test-Design checkpoint (100 pts) — the Fellow builds the harness that separates useful draft from trustworthy claim for their own thread.

---

## D. Current state (sourced)

**1. Hallucinated citations — rates.**
- Model generation matters: ~55% of GPT-3.5 citations fabricated vs ~18% for GPT-4 (secondary summary — StudyFinds: https://studyfinds.org/chatgpts-hallucination-problem-fabricated-references/) `[verify against primary]`. GPT-4o: 19.9% of citations fabricated across six simulated lit reviews (same summary).
- Peer-reviewed: JMIR 2024 (e53164) — GPT-3.5 produced ~39.6% non-existent references; GPT-4 substantially better. (https://www.jmir.org/2024/1/e53164)
- **Topic familiarity drives fabrication** (directly relevant to rare-disease/niche pharma): ~6% fabricated for major depressive disorder vs 28% (binge eating disorder), 29% (body dysmorphic disorder). (EurekAlert: https://www.eurekalert.org/news-releases/1106130 ; PMC12658395: https://www.ncbi.nlm.nih.gov/pmc/articles/PMC12658395/)
- "Real ≠ accurate": ~45% of *genuine* citations carried bibliographic errors (commonly wrong/invalid DOIs) per one analysis `[verify primary]`.

**2. LLM-as-a-judge — reliability and limits.**
- Origin: Zheng et al., MT-Bench/Chatbot Arena (NeurIPS 2023) — strong judges (GPT-4) reach >80% agreement with human preferences, ~human-human level. (arXiv 2306.05685: https://arxiv.org/pdf/2306.05685)
- Biases (named in that paper and follow-ups): **position bias** (>10% accuracy swing on order flip in pairwise code judging), **verbosity bias** (longer favored), **self-enhancement/self-preference bias** (favor own model family — arXiv 2410.21819: https://arxiv.org/pdf/2410.21819), **sycophancy** (Justice or Prejudice?, arXiv 2410.02736: https://arxiv.org/pdf/2410.02736).
- **Expert-domain gap (the load-bearing critique):** in specialized fields, LLM-judge↔human-expert agreement drops to ~60–68%, because RLHF tunes models toward *lay* preferences. (Survey, arXiv 2411.15594: https://arxiv.org/html/2411.15594v6 ; CIP "LLM Judges Are Unreliable": https://www.cip.org/blog/llm-judges-are-unreliable) → Use LLM-as-judge for triage/ranking, never sign-off.

**3. RAG for literature scanning.**
- Grounding outputs in retrieved passages reduces (not eliminates) fabrication. (RAG survey, arXiv 2506.00054: https://arxiv.org/html/2506.00054v1)
- **It does not eliminate hallucination:** RAGTruth (ACL 2024) shows LLMs still produce claims unsupported by / contradicting retrieved content. (https://aclanthology.org/2024.acl-long.585/)
- Failure modes for lit review: retrieval failure (right paper not fetched), synthesis hallucination (overstates retrieved content), context misattribution (true fact, wrong source).
- Medical-specific: MIRAGE benchmark (~7,663 clinical/biomedical QA items); clinical RAG evals testing on-prem deployment for privacy (MDPI: https://www.mdpi.com/2079-9292/14/21/4227); self-checking architectures (Self-RAG, FLARE); hallucination detectors (LettuceDetect, arXiv 2502.17125: https://arxiv.org/pdf/2502.17125).

**4. Regulated-content / fair-balance constraints.**
- **FDA fair balance (verified):** risk information must be presented with **prominence and readability reasonably comparable to benefit information** so net impression isn't misleading — governs content *and presentation*; does NOT require equal length. (FDA, Presenting Risk Information guidance: https://www.fda.gov/files/drugs/published/Presenting-Risk-Information-in-Prescription-Drug-and-Medical-Device-Promotion.pdf)
- AI-generated content risk: non-deterministic models can hallucinate unsubstantiated efficacy claims, drift off-label, or generate benefit copy without proportionate risk language — exactly the fair-balance defect. Must pass human MLR, not bypass it. (pharmaphorum: https://pharmaphorum.com/market-access/ai-missing-link-fixing-mlr-or-reason-it-breaks)
- **FDA 2025 enforcement (verified, dated):** after a Sept 9, 2025 crackdown + presidential memo, FDA issued ~60 compliance letters in 2025 (vs ~5 before Sept 9) and 100+ enforcement letters overall; priorities = omission of risk info, unsubstantiated claims (rejecting single-arm/open-label superiority support), misleading spokespersons. (ProPharma: https://www.propharmagroup.com/thought-leadership/fda-crackdown-drug-advertising-key-lessons-2025-compliance-letters ; Morgan Lewis: https://www.morganlewis.com/blogs/asprescribed/2025/09/fda-announces-crackdown-on-dtc-advertising-what-it-means-for-pharma-and-what-comes-next) `[counts approximate — vary by source/date]`
- Volume pressure (why AI is tempting): promotional-material production rose ~29% YoY in US 2025. (Indegene: https://www.indegene.com/what-we-think/reports/future-of-mlr-review)

**5. Building a validation harness.**
- **Citation verification (non-negotiable):** programmatically resolve every reference — work exists, DOI/PMID valid, cited text supports the claim. Catches fabrications AND "real-but-wrong" citations.
- **Groundedness/faithfulness metrics:** RAGAS faithfulness decomposes an answer into atomic claims and scores fraction supported by retrieved context. (RAGAS docs: https://docs.ragas.io/en/stable/concepts/metrics/available_metrics/faithfulness/)
- **Know the limits:** RAGAS faithfulness moderately effective on simple queries, weak on complex ones (one benchmark: failed to score ~83.5% of examples). Not a pass/fail oracle. (Cleanlab: https://cleanlab.ai/blog/rag-tlm-hallucination-benchmarking/)
- **Dedicated detectors** (RAGTruth-trained, LettuceDetect, Luna — arXiv 2406.00975) as a complementary layer.
- **Human-in-the-loop capstone:** AI does mechanical pre-checks; humans do judgment.

**6. Why human review is load-bearing.** Fluency trap + automation bias + trust trap (A.2–A.4). The asymmetric-harm argument (A.4) is the synthesis.

---

## E. Teaching

- **The one-sentence takeaway:** LLMs are powerful *draft generators inside a harness*; they are never the final authority on a factual or promotional claim.
- **Teach with the failure first:** the hallucinated-citation evidence summary (B). Then *Mata v. Avianca* as the cautionary tale — the failure was skipping verification, not using AI.
- **The harness as the artifact:** Fellows build a workflow that (1) verifies every citation, (2) scores groundedness/faithfulness, (3) flags fair-balance/MLR risk, (4) routes to human review. Each layer's *limits* are taught alongside it.
- **The niche-indication warning:** hallucination is highest exactly where pharma research is hardest (rare disease) — so trust *less* where the stakes feel highest.
- **LLM-as-judge nuance:** good for triage/ranking; unreliable as sign-off, *most* unreliable in expert domains. Don't let an LLM judge approve a claim.
- **AI Use Disclosure tie-in:** the chapter trains the judgment named in the book's disclosure rule — which claims are truly evidenced, whether the partner could defend the content to a regulator.
- **Named Fellow artifact:** the *LLM workflow / validation harness* separating useful draft from trustworthy claim.

---

## F. Library files (copied to pantry, prefixed `_lib_`)

- `_lib_gigo.md` + `_lib_gigo-llm-toc.md` — *GIGO: A Crash Course in Data with LLMs* (Patel & Brown). Strongest companion: computational skepticism as the defense; LLM hallucination as the latest GIGO instance; the GPT-4 hallucinated-legal-citation case study; agentic auditors as automated quality sentinels. Directly supports A.5, B, and the harness in D.5/E.
- `_lib_prompt-engineering-textbook.md` — prompt-engineering reference; hallucination + RAG mentions; useful for the "how to prompt for grounded, provenance-bearing output" mechanics.
- `_lib_co-intelligence.md` — *Co-Intelligence* (Mollick). Human+AI collaboration framing, the "centaur"/expert-in-the-loop posture, fluency-vs-accuracy intuition. Good for E (when to use AI / when not).

*Note:* The MD library has no pharma-MLR or fair-balance depth; that comes from the web research (D.4) and `pharma-ai-hcp-marketing-synthesis.md` §4. The GIGO book is the standout library asset for this chapter.

---

## G. Gaps / flags

1. **Future-dated sources — do NOT cite without confirmation.** Search returned a *Lancet* "Fabricated citations" audit and multiple arXiv IDs in the 2601–2605 range, plus 2026 law-firm year-in-reviews. Headline numbers above are corroborated by dated 2023–2025 sources; the "~57 per 10,000 by early 2026" fabrication figure comes from a future-dated source — exclude.
2. **GPT-3.5 55% / GPT-4 18% fabrication figures** from a secondary summary (StudyFinds). Direction corroborated by JMIR 2024 (39.6%), but `[verify]` the exact 55%/18% against the original study.
3. **"~45% of real citations had bibliographic errors"** — from search synthesis; locate the primary study for exact % and population.
4. **"95% of generative AI pilots failing" (MIT)** — widely circulated, frequently mis-cited; `[verify]` the underlying MIT report + methodology before use. (Also appears in `pharma-ai-hcp-marketing-synthesis.md`.)
5. **MT-Bench ">80% agreement"** — solid (primary Zheng 2023). **"60–68% expert-domain agreement"** — from secondary/survey synthesis aggregating multiple studies; cite as a range, not one study.
6. **RAGAS "83.5% no-score" / "0.762 precision"** — benchmark- and config-specific; illustrate limits, not universal RAGAS performance.
7. **FDA 2025 letter counts** ("~60", "100+", "200+") — vary by counting method (compliance vs untitled vs warning) and reporting date. The *trend* (sharp 2025 escalation tied to the Sept 9, 2025 memo) is well-corroborated across major law firms. Attribute any specific count to a single dated source.
8. **Vendor MLR/AI-acceleration figures** (50–60 day cycles, 50–65% reduction) are vendor-reported, not independently audited — flag as such (carried from Ch 11 notes / synthesis §4).
