# Changelog

## Unreleased

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
