---
name: load-workspace
description: Use when the user says "load workspace", "understand this workspace", "read the workspace AGENTS.md", or asks Codex to orient itself in a workspace before doing project work. Reads the current directory's AGENTS.md and uses it to understand multi-repo layout, project purpose, conventions, and next-step context.
---

# Load Workspace

When this skill triggers, orient Codex to the workspace before doing other work.

## Workflow

1. Identify the current workspace root from the active working directory.
2. Read `AGENTS.md` in the current directory first.
3. If it is missing, search upward from the current directory for the nearest `AGENTS.md`.
4. If that is still missing, use `rg --files -g AGENTS.md` from the workspace root to find candidates and read the most relevant one. If multiple seem equally relevant, summarize the candidates and ask which one governs the workspace.
5. Parse the file for:
   - project purpose and high-level product/domain context
   - repository list, paths, and ownership boundaries
   - how repos relate to each other
   - setup, build, test, and run commands
   - branch, commit, PR, review, release, or deployment conventions
   - architecture, security, secret-handling, and data-safety rules
   - external systems, credentials, or environment assumptions
6. If the workspace has multiple repos, inspect only lightweight signals needed to verify the map:
   - repo directories exist
   - each repo's current branch and dirty/clean status
   - obvious package/build files when commands or stack are unclear
7. Report a concise workspace brief:
   - what the workspace is for
   - repos/modules found and what each appears to do
   - important rules Codex must follow
   - available commands or unknowns
   - any risks before making changes

## Behavior

- Treat `AGENTS.md` as authoritative for the workspace unless a deeper file in the target repo overrides it.
- Do not make code changes during workspace loading unless the user explicitly asks.
- Do not run heavy installs, builds, migrations, or tests while loading context.
- Do not expose secrets. If `AGENTS.md` references credentials, summarize the access pattern without printing secret values.
- If later work targets a specific repo, check whether that repo has its own `AGENTS.md` and merge those instructions with the workspace-level context.

## Output Shape

Keep the final brief compact and useful:

```markdown
**Workspace Loaded**
<one-sentence project summary>

**Repos**
- `<path>`: <role/status>

**Rules**
- <important instruction>

**Commands**
- <known command or "not specified">

**Open Questions**
- <only if needed>
```
