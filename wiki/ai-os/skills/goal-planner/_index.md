---
type: skill-doc
created: 2026-05-21
---

# goal-planner

Defines quarterly goals — SMART Goals or OKRs — and writes them to the
appropriate workstream goals file.

**Trigger:** `/goal-planner`
**Source:** `~/.claude/skills/goal-planner/SKILL.md`
**Writes to:** `wiki/[workstream]/goals.md`

---

## What It Does

Guides the user through a structured goal-setting interview and writes the
output to the wiki. Branches automatically based on workstream:

| Workstream | Framework | Output format |
|-----------|-----------|--------------|
| Career | OKR | Objective + KR table (Score 0.0–1.0) |
| Performance | OKR | Objective + KR table (Score 0.0–1.0) |
| Finance | SMART Goals | Goal row in quarterly table |
| Personal | SMART Goals | Goal row in quarterly table |
| Relationships | SMART Goals | Goal row in quarterly table |
| Wellbeing | SMART Goals | Goal row in quarterly table |

---

## Key Design Principles

- **Max 3 goals/objectives per workstream per quarter** — enforced at the start
- **OKR Objectives** must be inspirational, clear, and memorable (not deliverable-shaped)
- **OKR Key Results** must be value-based (not activity), measurable, and gradable 0.0–1.0
- **SMART goals** must embed all five SMART criteria in the goal statement itself
- **Quarter-aware** — asks which quarter (Q2 current, Q3 next) before writing
- **Epic linking** — optional column links goals to supporting Epics

---

## Key Files

| File | Purpose |
|------|---------|
| `SKILL.md` | Operational skill (mirror of source) |
| `wiki/[workstream]/goals.md` | Output — one per workstream |
| `wiki/ai-os/service-design/workstream-framework.md` | Methodology reference |

---

## Links

- [[SKILL|SKILL.md]] — full skill source
- [[../../../service-design/workstream-framework|Workstream Framework]] — SMART vs OKR rationale
- [[../project-planner/_index|project-planner]] — defines Projects that serve goals
- [[../../../service-design/project-workflow|Project Workflow]] — full planning hierarchy
