---
type: index
created: 2026-06-09
---

# Claude System Design

> Implementation details and integrations specific to the Claude harness.

This section documents how the Claude harness integrates with the Obsidian Vault, including skill implementation standards, hidden file mirroring, memory conventions, and third-party integrations.

## Articles

- [[skill-conventions|Skill Conventions]] — Standard structure for Claude skills and wiki documentation (mirrored from `~/.claude/skills/skill-conventions.md`)
- [[permissions|Claude Code Permissions]] — How permission prompts are reduced (`/fewer-permission-prompts`), the read-only-first policy, settings-file precedence, and the current project allowlist
- [[hidden-file-sync|Hidden File Sync Checklist]] — Tracks sync status of all hidden skill and memory files mirrored into the wiki
- [[memory/_index|Memory]] — Cross-session memory convention: types, file format, loading rule, and what not to store
- [[notebooklm-tenglin|NotebookLM Tenglin Integration]] — Claude-specific integration with Google NotebookLM; auth model, capabilities, planned use cases, and known risks
- [[plugins/_index|Plugins]] — Third-party and custom Claude Code plugins (extensions adding skills, agents, commands, hooks); currently the OpenAI Codex plugin

> [[jira-system-design|Jira System Design]] moved to [[generic/_index|Generic System Design]] on 2026-06-27: the board design and field mappings are harness-agnostic (any agent could sync), even though the current automation is Claude skills.
