---
type: index
updated: 2026-05-20
---

# Service Design

> *People and process: operational workflows, project workflow, prioritisation methodology, ceremonies, and the rules that govern how work flows through the system.*

For the taxonomy that decides what belongs here vs. System Design, see [[../taxonomy|AI OS Taxonomy]].

**Filing test:**
> Does this describe what people do, how processes run, or how work is prioritised and planned?
> - **Yes** → file here in `wiki/ai-os/service-design/`
> - **No, it describes the tools/infrastructure** → file in [[../system-design/_index|System Design]]
> - **In doubt** → default to Service Design

## Articles

- [[workstream-framework|Workstream Framework]] — What workstreams are, how they are structured (vision, values, ambitions, directions, goals), the six domains, filing rules, SMART vs OKR split, traceability principle, and how goals connect to Projects
- [[project-workflow|Project Workflow]] — Planning hierarchy, timebox rhythm, ceremony schedule, and operating guardrails
- [[wsjf|WSJF Reference]] — Formula, scoring criteria, Value vs RR/OE distinction, counter-factual questioning, anti-mood-bias check, and rationale
- [[project|Project Reference]] — Project definition, Objective + KR constraints, WSJF scoring at project level, commitment gate, and estimation approach
- [[deliverable|Deliverable Reference]] — User-facing Deliverable and Enabler types, sizing, story points, acceptance/success criteria, and scope discipline
- [[timebox-planning|Timebox Planning (DSDM)]] — MoSCoW prioritisation rules, 60/20/20 capacity split, timebox commitment model, and DSDM/Scrum hybrid process
- [[portfolio-kanban|Portfolio Kanban]] — Workflow stages (funnel → ready → implementing → done), transition triggers, WIP limits, Jira sync, and SAFe mapping
- [[portfolio-backlog|Portfolio Backlog]] — Parked Project candidates across all workstreams not yet gate-qualified; promoted to active Projects via `/project-planner`
- [[planning-hierarchy.excalidraw|Planning Hierarchy (diagram)]] — Visual companion to [[project-workflow|Project Workflow]]: Goals → Projects → Deliverables → Timebox, plus ceremonies and guardrails

- [[api-skill-troubleshooting|API Skill Troubleshooting]] — Isolation testing methodology and environment-specific gotchas (VPN routing, billing checks, curl isolation)
- [[prioritization-framework|Prioritization Framework]] — How to decide what to work on and when: workstream hierarchy, WSJF within workstreams, cross-workstream scheduling rules (draft)
- [[estimation-baseline|Estimation Baseline]] — Estimate vs actuals for every Project (three estimate points: t-shirt, scoped, actual); calibrates future sizing against real history
## Archived

- [[_archived/agile-workflow-retired/_index|Agile Workflow (retired)]] — Frozen verbatim snapshot of the pre-June 2026 Agile vocabulary (Epic/Story/Sprint). Includes vocab map and reinstatement instructions.
