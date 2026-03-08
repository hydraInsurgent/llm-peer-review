# Changelog

## 1.4

- **`/ui-spec` command** - Generate a UI design spec (colors, fonts, accessibility rules) linked to a plan. Picks from curated reference data, outputs a `UI-SPEC-*.md` file, and tags plan steps with `[UI]`.
- **UI reference data** - 15 color palettes with semantic roles, 10 font pairings with Google Fonts imports, and 20 UX guidelines (including 5 accessibility fundamentals). Lives in `.claude/ui-reference/`.
- **`/execute` UI awareness** - When a plan has `[UI]` steps and a linked UI-SPEC, `/execute` applies design system injection (states palette/fonts before writing UI code) and runs a micro-checklist (contrast, spacing, focus states).
- **`/review` design checks** - When a UI-SPEC exists, `/review` adds a Design Review section checking palette compliance, typography, contrast, focus states, touch targets, and responsive behavior.
- **`/create-plan` nudge** - After creating a plan, reminds you to run `/ui-spec` if the plan has UI work.
- **Setup scripts updated** - Both `setup.sh` and `setup.ps1` now copy `.claude/ui-reference/` to target projects.
- **Model updates** - `/ask-gpt` now defaults to GPT-5.4 (was 5.2). `/ask-gemini` now defaults to Gemini 3.1 Pro Preview (was 3 Flash Preview).

---

## 1.2

- **`/review` simplified** — Replaced overengineered 4-step pipeline (type detection, lens lookup, aggregation) with two-mode approach: small changes get a single pass, bigger changes get 3 focused sub-agents (Security, Code Quality, Logic). Removed "What Claude Missed" self-check.
- **Toolkit versioning** — Setup scripts now display version number in banner. VERSION file at repo root.

---

## 1.1

### Ruflo Patterns

Adopted 5 patterns from AI research to improve the core commands.

**`/review` — Simplified Two-Mode Review:**
- Small changes (1-2 files): single-pass review, no sub-agents
- Bigger changes (3+ files): three focused sub-agents in parallel — Security, Code Quality, Logic
- Severity: 🚫 Block / ⚠️ Warn / 💡 Suggest
- Finding IDs (R1, R2...) — say "fix R2 and R5" to approve specific fixes
- Staff Engineer Check for big-picture evaluation

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
- **Staff Engineer Check** in `/review` — Big-picture evaluation: right approach, shortcuts to clean up, what to push back on
- **Outcomes section** in `/create-plan` — Record what actually happened vs. what was planned
- **"When to Stop"** in `/execute` — Stop and re-plan on critical blockers instead of pushing through
- **Subagent Strategy** — Guidance for Claude to use subagents for research and parallelize independent work

### Fixes

- **`/document` command** — Now aware of LESSONS.md and CHANGELOG.md. Includes file ownership guidance (won't edit `toolkit.md`). Clarifies what goes where: README for features, CLAUDE.md for project info, CHANGELOG for user-facing changes, LESSONS for learnings.
