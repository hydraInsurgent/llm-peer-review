# Code Review Task

Be thorough but concise.

## CRITICAL RULES

1. **REPORT ONLY** - Do NOT make any changes or edits to files
2. **Wait for approval** - Only fix things after I say "fix it"
3. **Explain simply** - I'm a PM learning to code, use plain English

## How to Review

Read the changed files. Then pick one of two modes:

**Small change** (1-2 files, ~20 lines or less): Review in a single pass. No sub-agents needed.

**Bigger change** (3+ files or significant logic): Run three focused sub-agents in parallel using the Agent tool, then combine their results:

| Sub-agent | What it checks |
|-----------|----------------|
| **Security** | Auth checks, input validation, secrets exposure, injection risks |
| **Code Quality** | Naming, duplication, complexity, pattern consistency |
| **Logic** | Edge cases, off-by-ones, missing error handling, wrong assumptions |

Each sub-agent should use the severity scale and Finding ID format below.

## Severity Levels

- 🚫 **Block** — Will break the app. Must fix before merging.
- ⚠️ **Warn** — Should fix before shipping. Risk of bugs or tech debt.
- 💡 **Suggest** — Nice to have. Improves quality but not urgent.

## Finding IDs

Every finding gets a unique ID: **R1**, **R2**, **R3**, etc. This lets the user say "fix R2 and R5" to approve specific fixes.

## Output Format

### Top Issues (scannable summary)
```
🚫 2 Blocks: R1 (file:line — one-line description), R3 (file:line — one-line description)
⚠️ 1 Warn: R2 (file:line — one-line description)
💡 1 Suggest: R4 (file:line — one-line description)
```

### ✅ Looks Good
- [What's working well — 2-3 items]

### 🔍 Findings

- **R1** 🚫 `file:line` — [Issue description in plain English]
  - **Why:** [Why this matters]
  - **Fix direction:** [What to change — not the exact code, just the approach]

- **R2** ⚠️ `file:line` — [Issue description]
  - **Why:** [Why this matters]
  - **Fix direction:** [Approach]

### 🏗️ Staff Engineer Check

After the standard review, step back and evaluate as a staff engineer:
- **Right approach?** — Is the overall design sound, not just the code?
- **Shortcuts to clean up?** — Anything that works now but needs fixing before production?
- **What would you push back on?** — What would a senior engineer flag before merging?

### 📊 Summary
- Files reviewed: X
- Blocks: X | Warns: X | Suggests: X

## REMEMBER: Report issues only. Do NOT edit any files until I approve.
