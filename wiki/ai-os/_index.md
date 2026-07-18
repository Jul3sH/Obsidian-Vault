---
type: index
---

# AI OS

> *The operating layer that runs Julian's wiki, workflows, and personal/organisational processes using Claude Code.*

The AI OS is everything that makes the wiki intelligent and executable — skills, service design (workflows and ceremonies), system design (tools, memory, infrastructure), and the conventions that govern how they work. It is distinct from content (career articles, finance notes, etc.) and from plans (epics, projects).

**Rule: all skills go here, regardless of domain.** Even a skill tightly coupled to finance or career lives under `ai-os/skills/`. Workstream indexes cross-link to relevant skills. This is consistent, auditable, and mirrors the operational reality at `~/.claude/skills/`.

**Start here:** [[ai-os/taxonomy|AI OS Taxonomy]] — the filing rule for what belongs in Service Design vs System Design vs Skills.

## Sections

### Service Design
- [[ai-os/service-design/_index|Service Design]] — People and process: agile workflow, ceremonies, prioritisation methodology, operational troubleshooting

### System Design
- [[ai-os/system-design/_index|System Design]] — Tools and infrastructure: architectural principles, Jira integration, skill conventions, mirroring, memory (Claude harness)

### Skills
- [[ai-os/skills/_index|Skills]] — All Claude Code skills (hybrid: SKILL.md = service, scripts/ = system)

### Templates
- [[ai-os/templates/_index|Templates]] — Reusable artifact patterns for producing consistent, well-structured .md files

### Logs
- [[ai-os/logs/log-2026-Q2|Operations Log Q2 2026]] — Append-only record of all compile, refactor, maintenance, and setup operations

## Operational Locations
These are fixed paths that cannot be moved — the wiki documents them but does not host them:
- **Skills:** `~/.claude/skills/[skill-name]/SKILL.md`
- **Memory:** `~/.claude/projects/-Users-julianhart-Obsidian-Vault/memory/`
- **Project settings:** `CLAUDE.md` in the Obsidian Vault root
