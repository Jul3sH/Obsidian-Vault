---
type: index
created: 2026-06-27
---

# OpenCode System Design

> Implementation details and integrations specific to the OpenCode harness.

OpenCode consumes the shared operating layer by auto-loading the vault-root `AGENTS.md`, the same canonical file Claude imports and Codex reads directly. It needs no per-tool wrapper unless a genuinely OpenCode-specific rule appears. For the cross-harness loading model, see [[agent-instruction-architecture|Agent Instruction Architecture]].

## Articles

- [[opencode-setup|OpenCode Setup]] - How OpenCode discovers `AGENTS.md` in the vault, config locations, where OpenCode-only deltas go, and the `/init` overwrite warning.
- [[opencode.jsonc|opencode.jsonc]] - Mirror of `~/.config/opencode/opencode.jsonc`
- [[gitignore|gitignore]] - Mirror of `~/.config/opencode/.gitignore`
