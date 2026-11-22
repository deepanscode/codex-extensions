---
name: claude-plan
description: Use when the user explicitly asks Codex to use Claude Code to plan, architect, compare approaches, or produce an implementation plan. Trigger phrases include "claude plan", "use claude to plan", "ask claude code to architect", and "get a claude agent plan".
---

# Claude Plan

Run Claude Code as a read-only planning delegate and return the plan to the user.

## Defaults

- CLI: `claude`
- Permission mode: read-only / no edits. If the installed CLI does not expose an exact read-only flag, instruct Claude in the prompt not to modify files and verify with `git diff`.
- Depth: default to a thorough plan; ask for a shorter pass only if the user requested quick/low effort.

Use the model and effort shown below unless the user requests an override.

## Steps

1. Gather context: current directory, branch, recent commits, tech stack files, and relevant paths.
2. Build a prompt that asks Claude Code to analyze the codebase and produce:
   - Summary
   - Approach and rationale
   - Files to create or modify
   - Ordered implementation steps
   - Edge cases
   - Testing strategy
   - Risks and trade-offs
3. Run:

```bash
claude --model claude-opus-5-5 --effort high -p "[constructed planning prompt]"
```

If this CLI accepts a working-directory flag in the installed version, pass the current project path explicitly. Otherwise run the command from the project root.

4. Check `git diff --stat`. If anything changed, stop and report that the delegate unexpectedly modified files.
5. Summarize Claude's plan in Codex's final answer, preserving concrete file paths and risks.

