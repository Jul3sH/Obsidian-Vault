---
type: skill-index
created: 2026-05-08
skill-path: ~/.claude/skills/define-enabler/SKILL.md
---

# Define Enabler Skill

Defines a SAFe enabler — technical work that creates the architectural runway for future user stories. Covers four types: Exploration (spike), Architecture, Infrastructure, Compliance. Writes the enabler file to `wiki/projects/` with WSJF scoring and updates the priority queue.

## Trigger phrases
"Define an enabler", "research spike", "I need to set up [X] before I can build [Y]", "technical debt", or when describing work without direct user value but clear downstream unblocking potential.

## What this skill does — and does not do

**Does:**
- Identifies enabler type (Exploration / Architecture / Infrastructure / Compliance)
- Defines technical objective, what the enabler unblocks, and success criteria
- Enforces time-boxing on Exploration spikes (XS–S only)
- Scores the enabler with WSJF, with emphasis on Risk/Opportunity Enablement
- Creates `wiki/projects/[enabler-slug].md`
- Updates `wiki/projects/_index.md` — the WSJF priority queue
- Guards against open-ended spikes, gold-plating, and enablers that unblock nothing

**Does not:**
- Create Jira issues — that is `/jira-sync`'s job
- Define user stories — use `/define-user-story` for user-facing work
- Define projects — use `/project-planner` for that

## Key difference from user stories
Enablers use **Success Criteria** (not Acceptance Criteria) and have a **Technical Objective** (not an As a / I want / So that statement). The file format includes `type: enabler` and `enabler-type:` in the frontmatter.

## Steps
1. **Identify the enabler** — which project, type, technical objective, what it unblocks, success criteria (2–4), Definition of Done
2. **T-shirt size** — guard against XL; enforce XS–S for Exploration spikes
3. **WSJF scoring** — Risk/Opportunity Enablement is the key component; rank in queue context
4. **Write to wiki** — enabler file + index update + log entry
5. **Next steps** — hand off to `/jira-sync`, more stories, or `/sprint-plan`

## Links
- **Skill file:** `~/.claude/skills/define-enabler/SKILL.md`
- **Mirror:** [[SKILL|SKILL.md]]
- **Outputs:** [[../../projects/_index|Projects — WSJF Queue]]
- **Design principles:** [[../../service-design/project-workflow|Project Workflow]] — planning hierarchy and sizing
