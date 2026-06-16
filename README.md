# hk-plugins

The umbrella **Claude Code marketplace** for all of jai's plugins. Add this one marketplace and install any of the plugins below.

This repo is itself the marketplace: `.claude-plugin/marketplace.json` lists every plugin, each living under `plugins/<name>/`.

---

## Install

```bash
# 1. Register this marketplace (once)
/plugin marketplace add HirotoKanda/hk-plugins

# 2. Install whichever plugins you want
/plugin install orchestra@hk-plugins
/plugin install reading-papers@hk-plugins
/plugin install thesis-reviewer@hk-plugins
```

Restart the session (or `/exit` and relaunch) so skills and agents load.

## Plugins

| Plugin | What it does | Notes |
|--------|--------------|-------|
| **orchestra** | `/orchestra` — multi-agent, TDD development. A conductor delegates planning/review to Claude subagents and implementation to ChatGPT Codex through a Plan → Implement → Review → Commit cycle. | Requires the `codex` CLI and the `claude-code-setup` plugin. |
| **reading-papers** | `/reading-papers` — read, summarize & critique a research paper with one unified four-stage method (Triage → Comprehend → Critique → Integrate). Loads a physics toolbox for physics/experimental papers. | — |
| **thesis-reviewer** | `/thesis-structure-review <path>` — grades the structure & logical flow of a science/engineering thesis (理工系卒業論文) against a standard 6-chapter template. Reads PDF/LaTeX/Markdown. | Structure only, never content correctness. |

## Layout

```
hk-plugins/                              <- git repo = marketplace
├── .claude-plugin/marketplace.json      <- lists all plugins below
└── plugins/
    ├── orchestra/                        (skill + 3 agents)
    ├── reading-papers/                   (skill + physics.md)
    └── thesis-reviewer/                  (skill)
```

## Updating a plugin

Edit files under `plugins/<name>/`, bump that plugin's `version` in `plugins/<name>/.claude-plugin/plugin.json`, commit & push, then on each machine:

```
/plugin marketplace update hk-plugins
/plugin update <name>
```

---

*Previously each plugin had its own single-plugin marketplace repo (`orchestra-plugin`, `reading-papers-plugin`). Those are now consolidated here; the old repos are archived.*
