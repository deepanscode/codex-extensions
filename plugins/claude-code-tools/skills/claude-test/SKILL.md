---
name: claude-test
description: Use when the user explicitly asks Codex to use Claude Code to write tests, improve coverage, or run a testing pass. Trigger phrases include "claude test", "use claude to write tests", "ask claude code to add coverage", and "have a claude agent test this".
---

# Claude Test

Use Claude Code to add or improve tests, then run the relevant test suite from Codex.

Use the model and effort shown below unless the user requests an override.

## Steps

1. Detect the test framework and existing test layout.
2. Identify the source files or recent diff that need coverage.
3. Run:

```bash
claude --model claude-opus-5-5 --effort high -p "[constructed test-writing prompt]"
```

4. Review changed test files with `git diff`.
5. Run the appropriate command, such as `npm test`, `npx vitest`, `pytest`, `go test ./...`, or `dotnet test`.
6. Report test files added, scenarios covered, command output summary, and gaps.

## Prompt Requirements

Ask Claude Code to cover happy paths, edge cases, error handling, and regression cases while following existing test style. It should not rewrite production code unless the user explicitly asked for a fix.

