# thesis-structure-review

Structural reviewer for science/engineering theses (理工系卒業論文). Invoked as a slash command with a thesis file path:

```
/thesis-structure-review ./thesis/main.tex
```

The skill reads the file (PDF / LaTeX / Markdown), extracts the table of contents, and grades the thesis against a standard 6-chapter template — paying special attention to the **logical parallelism** that should run through Theory / Method / Result / Discussion (e.g. *baseline → proposed*, *simple case → general case*). It reports in the thesis's own language and cites concrete chapter/section numbers and quotations for every finding.

**Scope:** structure and logic only — it does *not* judge whether the science or math is correct.

See [`SKILL.md`](./SKILL.md) for the full reviewer instructions and output format.
