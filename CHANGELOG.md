# Changelog

## Unreleased

### Ruflo Patterns

Adopted 5 patterns from AI research to improve the core commands.

**`/review` — Adaptive Multi-Lens Review:**
- Auto-detects change type + scope + confidence before reviewing
- Selects lenses based on type (small fix, feature, codebase, plan, docs, config)
- Runs parallel sub-reviews for multi-lens reviews
- New severity: 🚫 Block / ⚠️ Warn / 💡 Suggest (replaces CRITICAL/HIGH/MEDIUM/LOW)
- Finding IDs (R1, R2...) — say "fix R2 and R5" to approve specific fixes
- Two-layer output: scannable summary at top, detailed findings by lens below
- "What Claude Missed" self-check when fixing issues not in the review report

**`/pair-debug` — New Command:**
- Focused debugging partner (not a teacher — that's `/learning-opportunity`)
- Logs-first habit: always starts with "check the logs"
- Repro contract: gathers expected vs actual, error text, environment
- Hypothesis + check IDs (H1/H2, C1/C2) — user picks which check to run

**`/create-plan` — Parallelization Tags:**
- Steps tagged `[parallel]` or `[sequential]` with deliverables and dependencies
- Optional Goal State section for features with 3+ steps

**`/execute` — Parallel Execution:**
- Pre-flight check: lists files per agent, downgrades to sequential if overlap
- User confirmation before spawning parallel work
- Integration checkpoint after parallel steps complete

**Compaction:**
- `CLAUDE_AUTOCOMPACT_PCT_OVERRIDE` set to 65% in `.claude/settings.json`

---

### Breaking: CLAUDE.md Split

Toolkit instructions have moved out of `CLAUDE.md` into `.claude/rules/toolkit.md`.

**What changed:**
- `CLAUDE.md` is now a short, project-specific template (your project info, preferences)
- `.claude/rules/toolkit.md` contains all toolkit rules (workflow, commands, git guidance, permissions)
- `toolkit.md` is auto-loaded by Claude Code and always updated when you re-run setup
- `CLAUDE.md` is never overwritten — it's yours to customize

**What existing users need to do:**
1. Re-run setup (`setup-claude-toolkit .` or `bash /path/to/setup.sh`)
2. Move any project-specific info from your old `CLAUDE.md` into the new `CLAUDE.md` template
3. Delete your old `CLAUDE.md` and re-run setup if you want a fresh template

**Why:** Previously, toolkit updates couldn't reach existing users because `CLAUDE.md` was skipped if it existed. Now, toolkit rules update automatically via `toolkit.md`, and your project info stays safe in `CLAUDE.md`.

### New Features

- **LESSONS.md** — Track what you learn across sessions. Created on first setup, never overwritten.
- **Staff Engineer Check** in `/review` — Adds a production-readiness lens: "What would you push back on?"
- **Outcomes section** in `/create-plan` — Record what actually happened vs. what was planned
- **"When to Stop"** in `/execute` — Stop and re-plan on critical blockers instead of pushing through
- **Subagent Strategy** — Guidance for Claude to use subagents for research and parallelize independent work

### Fixes

- **`/document` command** — Now aware of LESSONS.md and CHANGELOG.md. Includes file ownership guidance (won't edit `toolkit.md`). Clarifies what goes where: README for features, CLAUDE.md for project info, CHANGELOG for user-facing changes, LESSONS for learnings.
