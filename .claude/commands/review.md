# Code Review Task

Perform an adaptive, multi-lens code review. Be thorough but concise.

## CRITICAL RULES

1. **REPORT ONLY** - Do NOT make any changes or edits to files
2. **Wait for approval** - Only fix things after I say "fix it"
3. **Explain simply** - I'm a PM learning to code, use plain English

> **Note:** These checks are opinionated toward a JavaScript/TypeScript web stack. Customize the lens checks below to match your project's language and framework.

## Step 1: Detect Type + Scope

Before reviewing, classify the change:

```
Detected type: [type from menu below]
Scope: [N files, ~N lines changed]
Confidence: [High / Medium / Low]
```

- If confidence is **Low**, ask one clarifying question before proceeding
- If the user specifies a type (e.g., "review this as a codebase review"), use their override

## Step 2: Select Lenses

Based on detected type, run only the relevant checks:

| Type | Lenses |
|------|--------|
| **Code (small fix, ≤20 lines or 1 file)** | Correctness, Side Effects — single-pass, no sub-agents |
| **Code (small fix touching auth/security/core)** | Correctness, Side Effects, Security — spawns security sub-review |
| **Code (feature, 2-15 files)** | Security, Performance, Code Quality, Logic/Flow |
| **Full codebase (>15 files or explicit)** | Architecture, Consistency, Tech Debt, Security, Performance |
| **Idea/plan** | Feasibility, Scope Creep, Edge Cases, User Impact |
| **Documentation** | Accuracy, Completeness, Clarity |
| **Config/infra** (settings, CI, env) | Correctness, Security, Side Effects |

## Step 3: Run Review

**For multi-lens reviews (3+ lenses):** Run each lens as a parallel sub-review using the Agent tool. Each sub-agent prompt must include: "Provide the 'Why' behind findings so the Lead Engineer can reconcile trade-offs."

**For small reviews (1-2 lenses):** Run as a single pass — no sub-agents needed.

## Step 4: Aggregate Results

After all lenses complete:
1. **De-duplicate** — merge findings that appear in multiple lenses
2. **Normalize severity** — apply the Block/Warn/Suggest scale consistently
3. **Cap findings** — ~3 findings per lens max, unless they are Blocks
4. **Note conflicts** — if lenses disagree (e.g., Performance vs Code Quality), flag the trade-off

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

### 🔍 Findings by Lens

**[Lens Name]**
- **R1** 🚫 `file:line` — [Issue description in plain English]
  - **Why:** [Why this matters]
  - **Fix direction:** [What to change — not the exact code, just the approach]

- **R2** ⚠️ `file:line` — [Issue description]
  - **Why:** [Why this matters]
  - **Fix direction:** [Approach]

*(Repeat for each lens that produced findings)*

### 🏗️ Staff Engineer Check

After the standard review, step back and evaluate as a staff engineer:
- **Right approach?** — Is the overall design sound, not just the code?
- **Shortcuts to clean up?** — Anything that works now but needs fixing before production?
- **What would you push back on?** — What would a senior engineer flag before merging?
- **Trade-off reconciliation** — If lenses conflict (e.g., "Performance suggests X but Code Quality suggests Y"), recommend a path with reasoning: "Given [context], I recommend [Z] because [reasoning]."

### 📊 Summary
- Files reviewed: X
- Blocks: X | Warns: X | Suggests: X

## What Claude Missed (post-review self-check)

When the user asks you to fix something that was NOT in your review report — caught by GPT/Gemini debate, the user's own reading, or any other source — recognize you missed it. **The signal:** you cannot cite a Finding ID for the fix.

**Only trigger for Block or Warn severity issues.** Don't prompt for Suggest-level misses.

When you detect a miss, say:
> "I missed this in my review — I was focused on [X] and didn't check [Y]. Add to LESSONS.md under Mistakes to Avoid? (y/n)"

If the user says yes, write a LESSONS.md entry that captures **why you missed it** (the blindspot reasoning), not just the technical fix.

## REMEMBER: Report issues only. Do NOT edit any files until I approve.
