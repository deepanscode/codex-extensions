---
name: claude-debug
description: Use when the user explicitly asks Codex to use Claude Code to investigate or fix a bug. Trigger phrases include "claude debug", "use claude to debug", "ask claude code to fix this bug", and "have a claude agent investigate".
---

# Claude Debug

Delegate bug investigation to Claude Code. Default to diagnosis only unless the user explicitly says to fix or patch.

## Modes

| Mode | Behavior |
|---|---|
| Investigate | Claude Code reads code and explains root cause. Codex verifies no files changed. |
| Fix | Claude Code applies a focused fix. Codex reviews the diff and runs verification. |

## Steps

1. Gather symptoms, reproduction steps, stack traces, recent commits, and likely files.
2. Construct a prompt asking for root cause, execution path, affected files, verification, and prevention.
3. If investigating, include "Do not edit files" in the prompt.
4. Run:

```bash
claude -p "[constructed debug prompt]"
```

5. For investigate mode, verify `git diff --stat` is empty.
6. For fix mode, inspect `git diff`, run tests or a repro command, and summarize the fix.

