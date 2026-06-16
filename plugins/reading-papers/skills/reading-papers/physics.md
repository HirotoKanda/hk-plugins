# Physics & Experimental Paper Reflexes

Load alongside the `reading-papers` skill when the paper is physics or a physical-science / lab-experimental paper — not merely any paper with measurements or benchmarks (a CS/ML evaluation does not count). Apply during **Comprehend** (figures, structure) and **Critique** (equations, uncertainty, assumptions). Each bullet is a one-line check; sources at the end. These catch real errors that the general method does not.

## Equations & derivations
- **Units, limits, symmetries** — run all three on every key equation; the goal is to *rule out wrong forms*, not reproduce the right one. [Miller]
- Check **dimensional homogeneity**: both sides, and every term in a sum, share dimensions; a mismatch is proof of an error and shows where it entered. [Miller; Tao]
- The argument of any transcendental function (sin, exp, ln) must be **dimensionless**. [Miller]
- Push a variable to an **extreme** (0, ∞, equal masses) and confirm the result reduces to a formula you already know. [Miller]
- Use **label/particle-swap symmetry**: exchanging identical indices must leave the result invariant — lets you reject wrong forms by inspection. [Miller]
- **Re-derive** the load-bearing steps yourself; that's how you find the hidden assumptions. Skip nasty intermediate algebra on the first pass — authors expect you to fill it in later. [Mermin]
- Before comparing two papers, pin down **conventions**: metric signature (+−−− vs −+++), 2π placement in Fourier transforms, field/state normalization — most apparent discrepancies are pure convention. [Gupta]

## Experimental papers — uncertainty & significance
- Trace the measurement **back to the one raw quantity** actually recorded (counts, a voltage, a field); the headline is only as good as its calibration. [PDG]
- **Statistical vs systematic:** statistical error shrinks as 1/√N, systematic does not — apply the "more-data test" and read which term dominates. [PDG]
- Be skeptical of "more data will confirm it" when the budget is already **systematics-limited** — the next run won't help. [Lyons]
- Tight run-to-run spread ≠ accuracy: systematics shift every repeat the same way and are invisible in the spread (precision ≠ accuracy). [Columbia]
- Never read an **error bar** without its definition — standard deviation vs standard error (σ/√N) vs CI differ by √N and mean different things. [Columbia; PDG]
- Convert significance Z↔p: **3σ ≈ "evidence", 5σ ≈ "discovery"**; read p as P(data this extreme | background only), NOT P(claim is real). [PDG]
- For any bump-hunt or scan, demand the **global (look-elsewhere-corrected)** significance, not the local one. [PDG]
- Know *why* physics uses **5σ**: a buffer against underestimated systematics, look-elsewhere, low prior plausibility, and a history of 3–4σ effects evaporating. [Lyons]
- Look for a **blind analysis** (hidden signal box / offset); if cuts were chosen while the result was visible, suspect tuning-to-expectation. [Klein & Roodman]
- Distinguish a **confidence interval** (frequentist — a property of the procedure) from a **credible interval** (Bayesian — find the prior and any sensitivity check). [PDG]
- For a null result, expect an **upper limit** (90/95% CL); check the method (CLs / Feldman–Cousins) so a downward fluctuation hasn't produced an artificially strong limit. [PDG]

## Theory papers — validity & symmetry
- Find the small/large **dimensionless expansion parameter**, and ask where it stops being small — perturbation series are typically asymptotic, not convergent. [refs]
- Check the **next correction** is genuinely smaller; a finite number of diagrams cannot capture non-perturbative effects (e.g. e^(−1/g²)). [refs]
- For mean-field / large-N results, identify **1/N** as the control parameter; fluctuations aren't negligible near phase transitions or at small N. [refs]
- Take every new formula to a **known limit** (coupling→0, ℏ→0, c→∞) and confirm it reduces correctly; a singular limit means the regimes are physically distinct. [refs]
- Check the result respects the **symmetries / conservation laws / Ward identity** of the theory; surviving gauge dependence in a physical result is an error. [UT Austin]

## Reading figures
- A power law is **straight on log-log** and the slope IS the exponent — read it from log values, and demand 2–3 decades before trusting it. [HyperPhysics; Statistics By Jim]
- **Overlapping error bars ≠ "no difference"** — it depends on whether bars are σ, SEM, or CI; identify the type first. [Cumming]
- Read **reduced χ²**: ≈1 good; ≫1 wrong model or underestimated errors; ≪1 overfit or overestimated errors — a "too-good" fit is suspicious, not a triumph. [reduced-χ²]
- Always look at the **residual plot**, not just χ²: residuals should scatter randomly about zero; any trend or curvature means the fit function is wrong. [Physics 50]
- Demand a **quantity + units on every axis**, and inspect axis ranges for truncation/exaggeration (Tufte's graphical integrity). [Tufte]
- Go to the single most important **figure + caption** first — often ~90% of what matters. [Pizzuto]

## Paper types & ecosystem
- A **PRL Letter** gives the claim and significance only — for derivations and methods go to the **companion long paper** (PRD/PRB/PRA/PRC/PRE). [APS]
- Read the **Supplemental Material** (sample prep, full derivations, tables, code); if a claim only holds via the SM, flag it as a weakness. [APS]
- To enter a new field, read a **review first** (Rev. Mod. Phys. / Physics Reports / Annual Reviews) for the basics and a ready-made reference list. [APS]
- On arXiv, check the **Submission history** (v1, v2, …) and the **journal-ref / DOI** for the published version; cite that if it exists, else the specific arXiv version. [arXiv]
- Trace **forward citations** (ADS / INSPIRE "cited by") to surface follow-ups, **Comments, and refutations** the original paper can't mention. [ADS; INSPIRE]

## The evaluation gauntlet (any flashy claim)
Run the six questions: (1) representative data? (2) blinded? (3) how exceptional vs alternative explanations? (4) ≥5σ? (5) does it actually challenge known physics or just refine it? (6) **independently confirmed** (ATLAS↔CMS, LIGO↔Virgo)? — and weight significance by **prior plausibility** (the 6σ faster-than-light-neutrino result was rightly distrusted because it contradicted relativity). Distinguish "not yet replicated" from "unreplicable." [symmetry magazine]

## Sources
- Miller, *Units, Limits, and Symmetries* (Maryland) — pages.astro.umd.edu/~mcmiller/teaching/astr601f15/lecture01.pdf
- PDG *Review of Particle Physics*, Statistics §40 — pdg.lbl.gov
- Lyons, *Discovering the Significance of 5 sigma* — arXiv:1310.1284
- Klein & Roodman, *Blind Analysis in Nuclear and Particle Physics* (Annu. Rev. Nucl. Part. Sci.)
- Cumming, *Inference by eye* (Stat. Med. 2009); reduced-χ² (Wikipedia); Physics 50 (residual plots)
- Mermin, *What's Wrong with these Equations?* (Physics Today 1989); Simonson & Gouvêa, *How to Read Mathematics*
- APS (PRL / Supplemental Material / Rev. Mod. Phys.) & arXiv (versions, journal-ref) policy pages; NASA ADS; INSPIRE-HEP
- *Six questions physicists ask when evaluating scientific claims*, symmetry magazine; Pizzuto (Wisconsin), *How to Read an Academic Paper*; Gupta (TIFR), *How to write (and read) a paper*
