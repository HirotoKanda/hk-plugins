---
name: reading-papers
description: Use when reading, summarizing, evaluating, or critiquing an academic or research paper (PDF, DOI, arXiv, or URL) — including physics/experimental papers — deciding whether a paper is worth deeper reading, or doing a literature survey of an unfamiliar field.
---

# Reading Papers

## Overview

Read a paper in **staged effort**, not start-to-finish — invest depth in proportion to the paper's value. This skill uses **one unified four-stage method**: **Triage → Comprehend → Critique → Integrate**. It fuses Keshav's three-pass method (the triage + critique spine) with Elliott, Beck & DeMarco's "Four i's" (active reading, and the Integrate stage Keshav omits).

Default deliverable: a **summary** (Triage + Comprehend) and a **critique** (Critique), closed by a short **Integrate** note.

Sources: S. Keshav, "How to Read a Paper" (ACM SIGCOMM CCR); C. Elliott, D. Beck & B. DeMarco, "How to Read a Physics Paper — The Four i's" (U. Illinois). For physics/experimental papers, also use `physics.md` (this directory). This skill operationalizes these; it is not a replacement for reading them.

## When to Use

- "Read / summarize / explain / TL;DR this paper"
- "Is this paper worth reading in depth?"
- "Review / critique / evaluate this paper" (requires the Critique stage)
- "Survey the literature on X" (use Literature Survey mode)

**When NOT to use:** writing or revising your own paper; casual blog/news reading.

## Getting the paper

Fetch the actual document — never summarize from memory of the title.
- HTML / abstract pages: WebFetch. (arXiv full text: try `ar5iv.org`; it may redirect to arxiv.org for papers it hasn't rendered. Cross-host redirects are returned to you, not followed — call WebFetch again with the redirect URL.)
- **PDFs (the reliable workhorse):** WebFetch usually can't decode PDF text — but it saves the binary to a local path. Use the **Read tool on that saved path** (renders PDFs page by page, figures and equations included); read multi-page PDFs in chunks. When in doubt, go straight to PDF→Read.
- **Long papers:** a whole-document WebFetch summary can be silently incomplete — it truncates, and may even invent missing numbers. For the Results / key sections of a long paper, go straight to **PDF→Read of the specific pages**; don't trust a summary for load-bearing figures.
- Local file given: Read it directly.

## The method — four stages

| Stage | Effort | Goal | What you do |
|-------|--------|------|-------------|
| **1 · Triage** | 5–10 min | Bird's-eye view; decide whether to continue | Read title, abstract, intro; read section headings; read conclusions; look at figures + captions; glance at references; note authors/affiliations → answer the five C's |
| **2 · Comprehend** | ≤ 1 hr | Grasp content, not every detail | Identify structure (often IMRD); active reading; take notes; scrutinize figures; skip proofs first time |
| **3 · Critique** | 1–5 hr | Full understanding; needed to review | Reconstruct / re-derive the work; rewrite in your own words and check; challenge every assumption |
| **4 · Integrate** | short | Connect & retain | Fit it against what you know; act on it; decide how to track it |

Times are Keshav's originals for human readers; as an agent treat them as **relative effort** (Triage ≪ Comprehend ≪ Critique), not literal clocks. After any stage you may legitimately **stop** (not relevant, outside your area, invalid assumptions).

### Stage 1 — Triage → answer the five C's
1. **Category** — what type? (measurement, analysis of an existing system, prototype, theory, review…)
2. **Context** — related papers; theoretical bases used.
3. **Correctness** — do the assumptions appear valid?
4. **Contributions** — main contributions?
5. **Clarity** — is it well written?

Also weigh the author list/affiliations as a credibility signal, and end with an explicit "study or move on?"

### Stage 2 — Comprehend
Identify the structure (many papers are **IMRD**: Introduction, Methods, Results, Discussion). Read with care but **skip proofs/derivations the first time**. Practice **active reading**: generate questions, then read to answer them, and iterate. **Take notes** and highlight what you don't understand. Scrutinize figures and graphs — axes labeled? error bars / statistical significance? — and cross-check the narrative against the figures and tables. Mark unread references for later. Goal: be able to summarize the main thrust *with supporting evidence* to someone else.

### Stage 3 — Critique
Reconstruct the work from its assumptions, then compare to the paper. Put it aside and **rewrite the key ideas in your own words**, then check against the original for accuracy and emphasis. **Challenge every assumption.** Identify implicit assumptions, missing citations, hidden failings, strong vs weak points, and issues in experimental/analytical technique. Do you agree; is the evidence sufficient? Jot ideas for future work.

**Adapt the reconstruction to the field, and state which you used:** computational/experimental → **virtually re-implement**; theory/math → **re-derive the key result**; qualitative/humanities/social → **reconstruct the argument and chain of evidence** and test whether the conclusions follow. A mixed theory-plus-experiment paper often needs **two at once** — do both and say so.

### Stage 4 — Integrate
How does the paper fit what you already know? Does it **contradict** something you believed, **raise new questions**, or give a **method you could reuse**? Will you need it later — and **how will you track it** (DOI, citation manager, note)? This stage is what turns reading into retained, usable knowledge; Keshav's method omits it.

## Physics & experimental papers

If the paper is physics or a physical-science / lab experiment, **also load `physics.md`** (same directory) and apply its field-specific reflexes during Comprehend and Critique. (A paper that merely has an empirical evaluation — e.g. a CS/ML benchmark study — does *not* count.) The reflexes cover: the units-limits-symmetries check on equations, statistical-vs-systematic uncertainty and significance (3σ/5σ, look-elsewhere), reduced-χ²/residual and log-plot reading, PRL-Letter↔companion-paper and arXiv/Supplemental norms, and the six-question evaluation gauntlet.

## Output format

Default deliverable, in this order:
1. **Header** — title, authors, venue/year, and Category (Triage). State Category here only.
2. **Summary** — the remaining four C's (Context, Correctness, Contributions, Clarity) plus the main thrust with supporting evidence (Triage + Comprehend).
3. **Critique** — strengths, then weaknesses / hidden assumptions / missing citations / methodological issues, with a one-line bottom-line verdict. State which reconstruction adaptation you used here.
4. **Integrate** — 3–4 lines: how it fits the broader context, what it contradicts or opens up, any reusable method, and whether/how it's worth tracking.

If the user only wants a quick read, stop after Triage + the five C's and say so.

## Literature Survey mode

For surveying an unfamiliar field of many papers:
1. Search engine (Google Scholar / Semantic Scholar) + good keywords → find 3–5 **recent** papers; Triage each; read their *related work* sections. If a recent survey exists, use it and stop.
2. Otherwise, find **shared citations and repeated author names** → those are the key papers/researchers; check where those researchers publish → that reveals the top venues.
3. Browse those venues' recent proceedings → high-quality related work. Two stages (Triage→Comprehend) through the resulting set, iterating when a new key citation appears.

Note the venue-prestige bias in steps 2–3: supplement with preprints and cross-disciplinary sources so important non-elite work isn't missed.

## Common mistakes

- Reading linearly front-to-back instead of in stages — wastes time on papers not worth it.
- Skipping the stop/continue decision after a stage.
- Summarizing without ever fetching the paper.
- Giving a summary when the user asked for a review (a review **requires** the Critique stage).
- Applying "re-implement" literally to a non-CS paper instead of adapting it.
- Passive reading — not generating questions first, or not taking notes as you go.
- Stopping at the critique and skipping **Integrate** (how it fits, what's next, how you'll track it).
- For a physics paper, not loading `physics.md` — missing the units / significance / χ² checks that catch real errors.
