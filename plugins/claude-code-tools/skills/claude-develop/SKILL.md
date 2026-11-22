---
name: claude-develop
description: Use when the user explicitly asks Codex to use Claude Code to implement, build, refactor, or edit code. Trigger phrases include "claude develop", "use claude to build", "ask claude code to implement", and "have a claude agent code this".
---

# Claude Develop

Run Claude Code as an implementation delegate, then inspect and verify the resulting changes before reporting back.

Use the model and effort shown below unless the user requests an override.

## Steps

1. Inspect the project enough to give Claude Code precise boundaries: feature request, relevant files, existing patterns, test command, and constraints.
2. Warn the prompt against unrelated refactors, destructive git operations, secret exposure, and AI attribution.
3. Run from the project root:

```bash
claude --model claude-opus-5-5 --effort high -p "[constructed implementation prompt]"
```

4. Inspect results:

```bash
git diff --stat
git diff
```

5. Run the most relevant tests or lint command available. If test setup is unclear, inspect package/tooling files first.
6. Present what Claude changed, what Codex verified, and any remaining risk.

## Prompt Shape

Ask Claude Code to return:

- Summary
- Files changed
- Key decisions
- Tests run
- Known gaps

Tell it to keep edits focused and leave the workspace in a reviewable state.

