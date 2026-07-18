---
type: index
created: 2026-06-09
---

# Generic System Design

> Architecture and principles shared across all harnesses accessing the Obsidian Vault.

These documents apply regardless of which harness (Claude, Google CLI, OpenCode, etc.) is in use. Harness-specific implementations may differ, but the underlying principles, folder structure, and conventions are universal.

## Articles

- [[agent-instruction-architecture|Agent Instruction Architecture]] - the three-layer instruction model: `AGENTS.md` (canonical universal rules), agent wrappers (`CLAUDE.md` + future Codex/OpenCode files), and this wiki (deep doctrine). Where any new operating rule belongs.
- [[system-design-principles|System Design Principles]] — AI OS architecture, two-layer model, working memory, and design principles
- [[documentation-conventions|Documentation Conventions]] — The single reference for how wiki content is written, structured, foldered, and linked: dual audience, visual-first, the human-navigation vs LLM-flatness balance, the state-folder model (`_wip`/`_reference`/`_on-hold`/`_archived`), bare-wikilink convention, and the current-position surfaces (project Status block + the engagement-strategy doc). Absorbed the former Wiki Folder Structure doc on 2026-06-16.
- [[jira-system-design|Jira System Design]] - Jira project structure, field mappings, labels, story points, cron expressions, and sync conventions. Harness-agnostic design; the current sync automation is Claude skills, but any harness could implement against it.
- [[multi-agent-protocol|Multi-Agent Protocol]] - Model roles, the research-review-write pipeline (Opus → Fable → write), output file conventions, source document integrity, handoff discipline, and the confirmation-amplification bias guard
