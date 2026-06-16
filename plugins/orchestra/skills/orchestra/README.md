# Orchestra — Claude Code + Codex workflow

An adaptation of [ShepAlderson/copilot-orchestra](https://github.com/ShepAlderson/copilot-orchestra) for Claude Code, with the implementation phase delegated to **ChatGPT Codex** via the `codex` CLI instead of running on Copilot's Claude in VS Code Insiders.

## Architecture

```
User -> /orchestra <request>
          |
          v
      CONDUCTOR  (this skill — runs in your main Claude Code session)
       |   ^
       |   | structured returns
       v   |
   +---+---+---+
   |   |   |   |
   v   v   v   v
 PLAN  IMPL  REVIEW   <- subagents, spawned via Agent tool
 (Claude) (Codex) (Claude)
          |
          v
       codex exec --full-auto -C $PWD  <- the actual coding happens here
```

| Role             | Where it lives                                    | Who does the work       |
|------------------|---------------------------------------------------|-------------------------|
| Conductor        | `~/.claude/skills/orchestra/SKILL.md`             | Claude (main session)   |
| Planner          | `~/.claude/agents/orchestra-planner.md`           | Claude subagent         |
| Implementer      | `~/.claude/agents/orchestra-codex-implementer.md` | Claude bridge -> Codex  |
| Reviewer         | `~/.claude/agents/orchestra-reviewer.md`          | Claude subagent         |

## Prerequisites

- **Claude Code** (any recent version with `Agent` tool + custom skills).
- **`codex` CLI** installed and authenticated.
  - Check: `codex --version`
  - Auth: `codex login` (one-time, opens browser).
- **Git workspace.** The cycle assumes commits between phases. For non-git workspaces, the conductor will offer to `git init`.
- **`claude-code-setup` plugin** enabled. The conductor auto-invokes its `claude-automation-recommender` skill during pre-flight to detect your test/lint/format commands and existing automations. Install:
  ```
  /plugin install claude-code-setup@claude-plugins-official
  ```
  If it's missing, `/orchestra` will stop and tell you to install it before proceeding.

## Usage

`/orchestra` has two modes, decided by whether you pass a request.

### Setup mode — `/orchestra` (no argument)

Run once per project to initialize the Claude Code + Codex environment:

```
/orchestra
```

The conductor will: check `codex`/git, auto-invoke `claude-code-setup` to detect your test/lint/format commands and recommend installable plugins (presented at a **consent gate** before any `claude plugin install … --scope user` — this gate runs in setup mode too, not just run mode), save the snapshot to `plans/orchestra-context.md`, and write a managed **orchestra-enabled** block into your project's `CLAUDE.md`. That block is what makes future complex tasks route through orchestra automatically — Claude reads `CLAUDE.md` and steers multi-step / multi-file work through the workflow. Setup then stops; it does not plan or implement. (Plugin installs need a session restart to activate.)

### Run mode — `/orchestra <request>`

```
/orchestra <one-line description of the change you want>
```

The conductor will:

1. **Pre-flight** (`codex --version`, git state, **clean tree required**), reusing `plans/orchestra-context.md` if setup already created it (otherwise it runs the scan + plugin gate now).
2. **Plan phase** — delegate research to the planner (handed the context snapshot), draft a 3–10 phase TDD plan, present it, and **pause for your approval**.
3. **Implement-Review-Commit cycle** per phase:
   - Implementer constructs a phase brief and runs `codex exec --full-auto -C $PWD`.
   - Reviewer reads the uncommitted diff, runs tests, returns APPROVED / NEEDS_REVISION / FAILED.
   - On approval, the conductor writes a phase-complete file and a commit message, then **pauses for you to commit**.
4. **Plan completion** — final summary file under `plans/`.

You stay in control at three pause points: plan approval, each phase commit, and the final close-out — plus a conditional consent gate if any plugins are recommended for installation.

## Files written under your project

- `plans/orchestra-context.md` — the project snapshot from `claude-code-setup` (test/lint/format commands, conventions, existing automations, recommended plugins, and which were installed/declined). Project-level and reused across runs.
- `CLAUDE.md` — a managed, delimited orchestra-enabled guidance block (setup mode; updated in place on re-run)
- `plans/<task-name>-plan.md` — the approved plan
- `plans/<task-name>-phase-<N>-complete.md` — per-phase record (one per phase)
- `plans/<task-name>-complete.md` — final report

Add `plans/` to `.gitignore` if you don't want them tracked.

## Codex invocation details

The implementer subagent calls codex like this (via Bash):

```bash
cat <<'CODEX_BRIEF' | codex exec --full-auto -C "$PWD" -
... phase brief, TDD protocol, scope constraints ...
CODEX_BRIEF
```

Flags:
- `--full-auto` — sandbox `workspace-write` + automatic command execution. Codex can edit files and run tests inside the workspace without prompting, but cannot escape it.
- `-C "$PWD"` — pin Codex's working root to the conductor's cwd.
- Phase brief on **stdin** (not as a quoted argument) — phase briefs are long and shell-escaping them is fragile.

We deliberately do **not** use `--dangerously-bypass-approvals-and-sandbox`. If you ever find Codex blocked on something it should be allowed to do, prefer a narrower fix (`--add-dir` for additional writable dirs, `--config` overrides) over removing the sandbox.

## What this is NOT

- **Not a one-to-one port** of copilot-orchestra. The VS Code Insiders chat-modes UI doesn't exist in Claude Code; pause points use Claude Code's natural end-of-turn waiting instead of a chat-mode handoff.
- **Not a multi-implementer setup.** This wiring picks Codex as the *sole* implementer. Claude plans and reviews; Codex codes. If you want parallel implementers or second-opinion reviews, that's a different topology — easy to add later by editing the conductor's Phase 2A delegation.
- **Not autonomous past pause points.** The user must approve the plan, commit each phase, and close out the run. By design.

## Customizing

- **Different test command per phase?** Mention it in the plan; the conductor passes it down to the implementer.
- **Non-TDD work** (docs, configs, exploratory spike)? The plan-style-guide insists on TDD; for non-TDD work you can either say so up front so the conductor relaxes the protocol, or use a different workflow.
- **Different Codex model?** Edit `orchestra-codex-implementer.md` and add `-m <model>` to the `codex exec` invocation, or set it in `~/.codex/config.toml`.
- **Want Claude as backup implementer too?** Edit the implementer agent to fall through to direct `Edit`/`Write` if `codex` returns FAILED twice. Currently it just reports failure and lets the conductor escalate to you.

## Credits

Workflow design adapted from Shep Alderson's [copilot-orchestra](https://github.com/ShepAlderson/copilot-orchestra) (MIT-style architecture — the agent personas, TDD cycle, plan style, and pause-point discipline are all his). The Codex bridge and the Claude Code packaging are local additions.
