<!--
    book.md
    BOOK DESCRIPTION & HIGH-LEVEL OUTLINE — your planning document.

    This file is for YOU, not the reader. It does not get compiled into
    the EPUB. Use it to think clearly about what the book is before you
    write it, and to keep yourself honest as you draft.

    Update freely as the book takes shape. Earlier versions belong in
    git history, not in this file.
-->

# AI-Driven Programmatic HCP Marketing

**Author:** Nik Bear Brown

---

## One-Sentence Pitch

This book teaches pharma marketing teams and research Fellows how to turn current AI research into testable HCP marketing and brand-measurement experiments that can improve lift, brand association, targeting quality, and patient-centered accountability.

## The Argument

<!-- What does this book claim that isn't already obvious or settled?
     What changes in the reader's head between page one and the end?
     2–4 paragraphs. -->

Pharma commercial AI is moving faster than the evidence base around it. Platforms can now target HCPs by NPI, trigger messages inside clinical workflows, personalize next-best actions, measure script lift, and claim increasingly sophisticated AI architectures. But the hardest questions are still under-researched: which models actually improve incremental prescribing rather than merely predict likely prescribers; which interventions build durable brand association rather than short-lived engagement; and which commercial optimizations create patient value rather than just branded volume.

The central argument of this book is that an external innovation lab can close that gap. Fellows do not need to own production systems to create value. They can scan the latest research, translate it into testable commercial hypotheses, build small prototypes or experimental designs, and hand the best ideas to product and data science teams for resourcing. The Fellow's job is not to ship the platform. The Fellow's job is to reduce uncertainty: identify what is promising, what is hype, what is ethically risky, and what deserves real engineering investment.

The book treats Mixture of Experts, ensembles, uplift modeling, causal inference, brand-equity measurement, LLM evaluation, and HCP journey analytics as tools inside a commercial research program. The point is not to worship new models. The point is to learn which modeling ideas can improve either marketing activation, such as lift and next-best action, or brand formation, such as quality association, patient archetype ownership, and prescriber loyalty.

## The Gap

<!-- Why does this book need to exist? What does it do that no other
     book in the field already does? Name 2–3 books in the same space
     and say briefly how yours differs. -->

Most pharma marketing books explain channels, regulation, brand planning, or sales force strategy. Most AI books explain model families without understanding HCP marketing, claims data, MLR, FDA constraints, payer friction, or brand equity. Most vendor materials claim lift but do not explain independent validation. This book sits in the gap.

It differs from a general healthcare marketing text by focusing on the research-to-product pipeline: how to evaluate emerging AI methods for commercial usefulness. It differs from a machine learning handbook by treating pharma constraints as load-bearing: NPI identity graphs, claims lag, patient privacy, FDA fair balance, MLR review, formulary access, brand measurement, and patient-welfare misalignment. It differs from vendor white papers by asking what a Fellow could independently test before a company commits product resources.

## The Reader

<!-- Who is this book FOR? Be specific — not "anyone interested in X."
     What do they already know? What are they trying to do?
     What will they be able to do after reading it? -->

The primary reader is a Fellow, analyst, product strategist, or commercial innovation researcher embedded near a pharma marketing platform, agency, data provider, or brand team. They know the basics of pharma marketing and have some comfort with data, but they are not expected to be production ML engineers.

After reading, the reader should be able to: map the pharma commercial stack; distinguish campaign lift from brand equity; explain when ensembles, MoE, uplift models, and LLM systems are appropriate; design small research studies that test model value; evaluate vendor claims; and produce product-ready briefs for internal engineering, data science, medical, legal, regulatory, and commercial stakeholders.

## High-Level Outline

<!-- Three to five acts / parts / movements. Not chapters yet — those
     live in outline.md. This is the shape of the argument at altitude. -->

**Part I — The Commercial Machine**
Establishes how pharma marketing actually works: detailing, DTC, NPI identity, claims data, point-of-care messaging, EHR integration, measurement, and the difference between campaign attribution and brand formation.

**Part II — The Model Toolkit**
Builds the AI and measurement vocabulary Fellows need: ensembles, MoE, uplift modeling, causal inference, LLMs, next-best action, brand association measurement, and model evaluation under pharma constraints.

**Part III — The Innovation Lab**
Turns the toolkit into an external lab operating model: research briefs, prototype experiments, handoff criteria, compliance review, product translation, and a portfolio of Fellow projects that could justify company investment.

## Open Questions

<!-- Things you don't yet know how to handle. Update as you draft.
     Don't pretend they're solved. -->

- Which public datasets or synthetic datasets should be used for Fellow prototypes when claims data is unavailable?
- How much technical implementation should the book require versus research design and product translation?
- Should patient-centered outcomes be a core grading criterion for every project, or a dedicated final module?
