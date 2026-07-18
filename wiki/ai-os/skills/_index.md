---
type: index
---

# Skills

> *All Claude Code skills documented here. Operational files live at `~/.claude/skills/`.*

**Rule:** Every skill — regardless of which domain it serves — is documented in this folder. Workstream indexes cross-link here; they do not host skill documentation themselves.

## Active Skills

| Skill | Trigger | Domain |
|-------|---------|--------|
| [[ai-os/skills/goal-planner/_index\|goal-planner]] | Defining quarterly goals, SMART Goals, OKRs | Cross-domain |
| [[ai-os/skills/project-planner/_index\|project-planner]] | Planning initiatives, defining goals, OKRs, WSJF | Cross-domain |
| [[ai-os/skills/jira-sync/_index\|jira-sync]] | "Sync to Jira", "push to Jira", after project-planner sessions | Cross-domain |
| [[ai-os/skills/jira-pull/_index\|jira-pull]] | "jira-pull", "pull from Jira"; Portfolio Kanban board moves; automatic end-of-day HKT pre-check | Cross-domain |
| [[ai-os/skills/sprint-plan/_index\|sprint-plan]] | "Sprint planning", "plan my sprint", `/sprint-plan` | Cross-domain |
| [[ai-os/skills/morning/_index\|morning]] | On-demand `/morning` only (not scheduled) | Cross-domain |
| [[ai-os/skills/standup/_index\|standup]] | End-of-day; automatic 4 PM HKT weekdays; `/standup` | Cross-domain |
| [[ai-os/skills/retro/_index\|retro]] | Weekly; automatic 4 PM HKT Fridays; `/retro` | Cross-domain |
| [[ai-os/skills/linkedin-enrichment/_index\|linkedin-enrichment]] | Enrich leads with LinkedIn data | Outreach |
| [[ai-os/skills/apollo-person-match/_index\|apollo-person-match]] | Match contacts to LinkedIn URLs | Outreach |
| tco | Cold email vendor TCO analysis (defined in CLAUDE.md) | Outreach |
| [[ai-os/skills/llm-council/SKILL\|llm-council]] | "council this", "pressure-test this", "war room this" | Cross-domain |
| [[ai-os/skills/notebooklm-py/SKILL\|notebooklm-py]] | `/notebooklm`, "make flashcards from [topic]", "create a notebook about [topic]" | Performance / Learning |
| [[ai-os/skills/resume-tailor/SKILL\|resume-tailor]] | Tailor resume to JD; "resume tailoring", "JD mapping" | Career |
| [[ai-os/skills/ats-checker/SKILL\|ats-checker]] | Check if resume will pass ATS; "ATS score", "will this get through the bots" | Career |
| [[ai-os/skills/define-task/_index\|define-task]] | "Define a task", "add this as a task" — generic deliverables that aren't a story or enabler | Cross-domain |
| [[ai-os/skills/find-skills/SKILL\|find-skills]] | "Find a skill for X", "is there a skill for X", "how do I do X" — discover and install skills from the ecosystem | Cross-domain |
| [[ai-os/skills/storm-research/SKILL\|storm-research]] | "storm research this", "storm report on X", "STORM briefing on X" — 5-lens multi-perspective HTML research briefing with adversarial citation verification | Cross-domain |
| [[ai-os/skills/commitment-guard/SKILL\|commitment-guard]] | *Reopening* a LOCKED decision (doubt/second-thoughts naming a committed decision), or "lock it in" / "/commitment-guard" — runs the F-N-M-T reopen test + 48h stand-down; defends decisions from emotional U-turns | Decisions |

**Status:** see [[skills-status|Skills Status]] for Active/Parked state.

## Adding a New Skill
1. Build the skill at `~/.claude/skills/[skill-name]/SKILL.md`
2. Create `wiki/ai-os/skills/[skill-name]/_index.md` documenting purpose, architecture, and testing notes
3. Add a row to this index and to [[skills-status|Skills Status]]
4. Cross-link from relevant workstream `_index.md` under a **Tools** section
5. Log the creation in [[ai-os/logs/log-2026-Q2|the operations log]]

## Conventions
Operational conventions (directory structure, credential handling, testing, VPN routing) are in `~/.claude/skills/skill-conventions.md` — loaded by LLMs when creating skills.

Design principles (why skills are structured the way they are) are in [[ai-os/system-design/system-design-principles|System Design Principles]] — § Skill Design.
