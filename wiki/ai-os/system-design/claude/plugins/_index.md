---
type: index
created: 2026-06-29
---

# Claude Code Plugins

> Third-party and custom plugins installed into the Claude Code harness. Plugins
> are extensions used from inside the Claude environment (they add skills,
> agents, commands, and hooks), so they are documented here under Claude System
> Design rather than in wiki/technology/.

Vendor plugin source files are **not** mirrored into the wiki (per the
[[hidden-file-sync|Hidden File Visibility rule]], shipped/vendor product files
are excluded). Each article below documents the plugin and Julian's
configuration of it, not its source.

## Plugins

- [[codex-plugin|Codex Plugin (OpenAI)]] — Bridges to OpenAI's Codex CLI (GPT-5/Codex) for delegated coding, diagnosis, and review; install/auth state and the stop-review-gate decision.
