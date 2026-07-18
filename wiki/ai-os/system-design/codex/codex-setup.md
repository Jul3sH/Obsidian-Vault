---
type: reference
created: 2026-06-27
tags: [ai-os, system-design, codex, harness]
---

# Codex Setup

> How Codex CLI discovers and uses the vault's shared operating layer.

## How Codex loads instructions

Codex auto-loads `AGENTS.md` by walking from the project/git root down to the current working directory. With the vault as the working directory, it finds and loads vault-root `AGENTS.md` automatically. No configuration needed.

Codex never reads `CLAUDE.md`. The full shared operating layer (writing style, knowledge base rules, wiki index structure, Cold Email TCO rules, operations log) is in `AGENTS.md`, so Codex inherits everything from session start with zero extra setup.

See [[agent-instruction-architecture|Agent Instruction Architecture]] for the full three-layer loading model.

## Discovery precedence (within Codex)

| Location | File | Behaviour |
|----------|------|-----------|
| `~/.codex/` (global) | `AGENTS.override.md` | Loaded first if present; use for temporary global overrides |
| `~/.codex/` (global) | `AGENTS.md` | Global Codex-only deltas (only if no override file) |
| Vault root (project) | `AGENTS.md` | The shared canonical layer - this is the file we maintain |

Project-level instructions (closer to cwd) override global defaults. The vault-root `AGENTS.md` is the project-level file.

## Codex-specific configuration

- Config file: `~/.codex/config.toml` - CLI defaults (model, approval mode, etc.)
- Global instruction deltas: `~/.codex/AGENTS.md` - only needed if Codex requires a rule no other agent shares
- Hosted Google connector: [[google-drive-connector]] - installed for Drive, Docs, Sheets, and Slides; currently needs re-authentication

There are currently no Codex-specific deltas. If one appears, add it to `~/.codex/AGENTS.md` and document it here.

## Hidden file mirroring

Per the **Hidden File Visibility** rule in `AGENTS.md`, mirror Codex's out-of-vault files into this folder (`wiki/ai-os/system-design/codex/`) so Julian can see them. Applies to instruction/config files such as:

- `~/.codex/config.toml` (CLI config)
- `~/.codex/AGENTS.md` or `AGENTS.override.md` (global Codex-only deltas, if created)
- any custom prompt / command / instruction files Codex stores under `~/.codex/`

Mirror as an exact copy (wrap `.toml` and other non-`.md` files in a fenced code block inside a `.md` so they render in Obsidian), update immediately after any change, and tell Julian which wiki file maps to which source. **Do not mirror** `~/.codex/auth.json`, API keys, tokens, logs, or session/cache files.

### Current mirror map

| Hidden source | Wiki mirror | Notes |
|---------------|-------------|-------|
| `~/.codex/config.toml` | [[config.toml]] | TOML wrapped in a Markdown code fence for Obsidian rendering |
| `~/.codex/auth.json` | [[auth-json-omitted]] | Omitted: purely secret material |
| `~/.codex/skills/storm-research/SKILL.md` | `wiki/ai-os/system-design/codex/skills/storm-research/SKILL.md` | Exact Markdown mirror of the custom Codex skill instructions |
| `~/.codex/skills/storm-research/agents/openai.yaml` | `wiki/ai-os/system-design/codex/skills/storm-research/agents/openai.yaml.md` | YAML wrapped in a Markdown code fence for Obsidian rendering |
| `~/.codex/skills/storm-research/assets/report-template.html` | `wiki/ai-os/system-design/codex/skills/storm-research/assets/report-template.html.md` | HTML wrapped in a Markdown code fence for Obsidian rendering |

**Out of scope (not mirrored):** `~/.codex/skills/.system/` (OpenAI's shipped/built-in system skills) and any vendor binaries or licence files. Per the Hidden File Visibility rule in `AGENTS.md`, mirror only Julian's own config and custom skills/prompts, not the tool's installation. If Julian later authors his own Codex skills/prompts under `~/.codex/`, mirror those here (stripping any leading dots from folder names).

## Critical warning: do not run /init

Codex has an `/init` command that scans the repo and generates an `AGENTS.md`. **Do not run `/init` in the vault.** It will overwrite the canonical `AGENTS.md` with auto-generated content, destroying the shared operating layer for all three agents.

## Key Takeaways

- Codex works out of the box: open the vault folder in Codex and `AGENTS.md` loads automatically
- No wrapper file needed unless a genuine Codex-specific rule appears
- Keep Codex-only deltas in `~/.codex/AGENTS.md`, not in the vault-root `AGENTS.md`
- Never run `/init` in the vault

## Related

- [[google-drive-connector]] - Hosted Google connector setup and auth status
- [[agent-instruction-architecture|Agent Instruction Architecture]] - the full three-layer model
- [[opencode-setup|OpenCode Setup]] - equivalent doc for OpenCode
