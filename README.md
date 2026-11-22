# Codex Extensions

A local Codex plugin marketplace adapted from `claude-code-extensions`. It includes Claude Code delegation skills, a unified Git platform MCP server with Bitbucket support, dev-workflow guidance, Clean Architecture skills, and 1Password CLI secret handling.

## Plugins

| Plugin | Purpose |
|---|---|
| `claude-code-tools` | Ask Codex to delegate planning, implementation, testing, debugging, and review work to Claude Code using `claude-opus-5-5` at high effort. |
| `gemini-tools` | Delegate the same five tasks to Antigravity CLI (`agy`) using `gemini-4-neon-high` at high effort. |
| `git-platform` | MCP server for GitHub, GitLab, and Bitbucket PRs, pipelines, deployments, and repo operations. |
| `dev-workflow` | Branch naming, commit messages, migration safety, docs/spec/runbook workflows, and pre-PR checks. |
| `clean-architecture` | Layered backend, modular-monolith, route-derived ID, and soft-delete guidance. |
| `1password` | Resolve tokens and environment secrets through the 1Password CLI instead of hardcoding them. |

## Install In Codex

From this repository root:

```bash
codex plugin marketplace add /Users/deepan/Projects/Personal/Tools/codex-extensions/.codex-plugin
```

Then install the plugins in the Codex app or CLI.

## Bitbucket Auth

`git-platform` supports raw env vars and `_CMD` indirection:

```bash
export BITBUCKET_USERNAME='you@example.com'
export BITBUCKET_TOKEN_CMD='op read op://Personal/Bitbucket/token'
```

For a fresh clone, install the MCP dependencies once:

```bash
cd plugins/git-platform
npm install
npm run build
```

## Repository Layout

```text
.codex-plugin/marketplace.json
plugins/
  claude-code-tools/
  git-platform/
  dev-workflow/
  clean-architecture/
  1password/
```
