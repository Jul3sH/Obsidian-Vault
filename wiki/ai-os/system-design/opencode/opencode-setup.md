---
type: reference
created: 2026-06-27
tags: [ai-os, system-design, opencode, harness]
---

# OpenCode Setup

> How OpenCode discovers and uses the vault's shared operating layer.

## How OpenCode loads instructions

OpenCode auto-loads the project-root `AGENTS.md` when you open a folder. With the vault as the working directory, it finds and loads vault-root `AGENTS.md` automatically. No configuration needed.

**Important:** if both `AGENTS.md` and `CLAUDE.md` are present (which they are in this vault), OpenCode uses only `AGENTS.md`. The Claude wrapper is cleanly ignored. The full shared operating layer is already in `AGENTS.md`, so OpenCode inherits everything from session start with zero extra setup.

See [[agent-instruction-architecture|Agent Instruction Architecture]] for the full three-layer loading model.

## Discovery precedence (within OpenCode)

| Location | File | Behaviour |
|----------|------|-----------|
| `~/.config/opencode/` (global) | `AGENTS.md` | Global OpenCode-only deltas, applied across all sessions |
| Vault root (project) | `AGENTS.md` | The shared canonical layer - this is the file we maintain |

Project-level instructions are combined with the global file. Both load if both exist.

## OpenCode-specific configuration

- Config file: `~/.config/opencode/opencode.json` - model, keybindings, MCP servers, theme
- Global instruction deltas: `~/.config/opencode/AGENTS.md` - only needed if OpenCode requires a rule no other agent shares

There are currently no OpenCode-specific deltas. If one appears, add it to `~/.config/opencode/AGENTS.md` and document it here.

## Hidden file mirroring

Per the **Hidden File Visibility** rule in `AGENTS.md`, mirror OpenCode's out-of-vault files into this folder (`wiki/ai-os/system-design/opencode/`) so Julian can see them.

Mirror as an exact copy (wrap `.jsonc` and other non-`.md` files in a fenced code block inside a `.md` so they render in Obsidian), update immediately after any change, and confirm to Julian which wiki file maps to which source. **Do not mirror** auth tokens, API keys, logs, generated caches, or session files.

### Mirror map

| Source path (`~/.config/opencode/`) | Wiki mirror (`wiki/ai-os/system-design/opencode/`) | Notes |
|--------------------------------------|-----------------------------------------------------|-------|
| `opencode.jsonc` | [[opencode.jsonc\|opencode.jsonc]] | No secrets to redact |
| `.gitignore` | [[gitignore\|gitignore]] | Stripped leading dot per convention |
| `AGENTS.md` | none | Does not exist yet; document here if created |
| `package.json` | not mirrored | Auto-generated, not authored by Julian (gitignored) |
| `package-lock.json` | not mirrored | Generated cache |
| `node_modules/` | not mirrored | Vendor shipped code

## Critical warning: do not run /init

OpenCode has an `/init` command that scans the repo and generates an `AGENTS.md`. **Do not run `/init` in the vault.** It will overwrite the canonical `AGENTS.md` with auto-generated content, destroying the shared operating layer for all three agents.

## Key Takeaways

- OpenCode works out of the box: open the vault folder in OpenCode and `AGENTS.md` loads automatically
- When `AGENTS.md` and `CLAUDE.md` both exist, OpenCode correctly ignores `CLAUDE.md`
- No wrapper file needed unless a genuine OpenCode-specific rule appears
- Keep OpenCode-only deltas in `~/.config/opencode/AGENTS.md`, not in the vault-root `AGENTS.md`
- Never run `/init` in the vault

## Related

- [[agent-instruction-architecture|Agent Instruction Architecture]] - the full three-layer model
- [[codex-setup|Codex Setup]] - equivalent doc for Codex
