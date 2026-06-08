---
name: claude-review
description: Use when the user explicitly asks Codex to use Claude Code for code review, PR review, security review, or a second-opinion review. Trigger phrases include "claude review", "use claude to review", "ask claude code to review this", and "get a claude agent review".
---

# Claude Review

Run Claude Code as a second-opinion reviewer. Codex stays in review stance and leads with findings.

## Steps

1. Determine the review range:
   - Uncommitted changes: `git diff HEAD`
   - Branch changes: `git diff origin/main...HEAD` or the repository's base branch
2. Run:

```bash
claude -p "[constructed review prompt]"
```

3. Ask Claude Code to return findings grouped by severity with file and line references, plus missing tests and security concerns.
4. Independently sanity-check the highest-risk findings before presenting them.
5. Final response order: findings first, open questions, then brief summary.

## Prompt Requirements

Tell Claude Code to focus on correctness bugs, regressions, security issues, data loss, race conditions, and missing tests. Style-only comments should be omitted unless they hide a real maintainability risk.

