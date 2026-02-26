# Code Review Task

Perform comprehensive code review. Be thorough but concise.

## CRITICAL RULES

1. **REPORT ONLY** - Do NOT make any changes or edits to files
2. **Wait for approval** - Only fix things after I say "fix it"
3. **Explain simply** - I'm a PM learning to code, use plain English

> **Note:** These checks are opinionated toward a JavaScript/TypeScript web stack. Customize the list below to match your project's language and framework.

## Check For

- **Logging** - No console.log statements, uses proper logger with context
- **Error Handling** - Try-catch for async, centralized handlers, helpful messages
- **TypeScript** - No `any` types, proper interfaces, no @ts-ignore
- **Production Readiness** - No debug statements, no TODOs, no hardcoded secrets
- **React/Hooks** - Effects have cleanup, dependencies complete, no infinite loops
- **Performance** - No unnecessary re-renders, expensive calcs memoized
- **Security** - Auth checked, inputs validated
- **Architecture** - Follows existing patterns, code in correct directory

## Output Format

### ✅ Looks Good
- [Item 1]
- [Item 2]

### ⚠️ Issues Found
- **[Severity]** [File:line] - [Issue description]
  - Fix: [Suggested fix]

### 🏗️ Staff Engineer Check
- **Right approach?** [Assessment]
- **Shortcuts to clean up?** [Assessment]
- **What would you push back on?** [Assessment]

### 📊 Summary
- Files reviewed: X
- Critical issues: X
- Warnings: X

## Severity Levels
- **CRITICAL** - Security, data loss, crashes
- **HIGH** - Bugs, performance issues, bad UX
- **MEDIUM** - Code quality, maintainability
- **LOW** - Style, minor improvements

## Staff Engineer Check

After the standard review, step back and evaluate as a staff engineer would:
- **Right approach?** — Is the overall design/architecture sound, not just the code?
- **Shortcuts to clean up?** — Anything that works now but would need fixing before shipping to production?
- **What would you push back on?** — What would a senior engineer flag before merging this PR?

## REMEMBER: Report issues only. Do NOT edit any files until I approve.
