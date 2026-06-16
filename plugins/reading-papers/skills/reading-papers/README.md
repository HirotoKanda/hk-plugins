# reading-papers — skill docs

The `/reading-papers` skill reads a research paper the way a careful researcher does: in **staged effort**, investing depth in proportion to the paper's value, and ending with a critical, connected understanding rather than a flat summary.

## The four-stage method

| Stage | Fuses | Goal → action | Decision |
|-------|-------|---------------|----------|
| **1 · Triage** | Keshav pass 1 + "Importance" | Scan title/abstract/intro/headings/conclusions/figures + authors → answer the **five C's** | stop or go deeper |
| **2 · Comprehend** | pass 2 + "Iteration" | IMRD skim; **active reading** (questions → read to answer → iterate); take notes; scrutinize figures | — |
| **3 · Critique** | pass 3 + "Interpretation" | Reconstruct / re-derive; rewrite in own words then check; challenge every assumption | — |
| **4 · Integrate** | *(new)* | How it fits / contradicts / reusable methods / how you'll track it | — |

**Five C's** (the Triage checklist): Category, Context, Correctness, Contributions, Clarity.

**Pass-3 adaptation** — state which you used: computational/experimental → *virtually re-implement*; theory/math → *re-derive the key result*; qualitative/social → *reconstruct the argument and chain of evidence*. A mixed theory-plus-experiment paper often needs two at once.

## Output format

1. **Header** — title, authors, venue/year, Category.
2. **Summary** — the other four C's + main thrust with supporting evidence.
3. **Critique** — strengths, then weaknesses / hidden assumptions / missing citations / method issues, with a one-line verdict and the adaptation used.
4. **Integrate** — a few lines: fit, contradictions, reusable methods, how to track it.

If you only want a quick read, the skill stops after Triage + the five C's and says so.

## Physics & experimental papers

For physics or lab-experimental papers (not merely any paper with a benchmark), the skill also loads **`physics.md`** and applies its reflexes during Comprehend and Critique — e.g. dimensional homogeneity and limiting-case checks on equations, separating statistical (1/√N) from systematic uncertainty, reading significance (3σ = evidence, 5σ = discovery) and demanding the global/look-elsewhere number, reduced-χ² ≈ 1 and residual-plot checks, log-log slope reading, going from a PRL Letter to its companion long paper, and a six-question evaluation gauntlet (including independent confirmation and prior plausibility).

## Getting the paper

Fetch the real document — never summarize from the title. Prefer HTML; for PDFs, WebFetch usually can't decode the text but saves the binary to a local path, so **Read that path** (renders pages, figures, equations). For long papers, go straight to PDF→Read of the key pages — a whole-document fetch summary can silently truncate or fabricate.

## Literature survey

The skill also has a survey mode: find 3–5 recent papers, mine their related-work and shared citations to surface key authors and venues, then Triage→Comprehend the resulting set — supplementing elite venues with preprints to avoid prestige bias.

## Sources

S. Keshav, *How to Read a Paper*; C. Elliott, D. Beck & B. DeMarco, *How to Read a Physics Paper — The Four i's*. The physics toolbox cites PDG, Lyons, Klein & Roodman, Cumming, Mermin, Simonson & Gouvêa, APS/arXiv policy, and *symmetry* magazine (see `physics.md`).
