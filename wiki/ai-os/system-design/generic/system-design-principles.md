---
created: 2026-05-07
type: reference
---

# AI OS — System Design Principles

**Open this document when you want to understand or extend how the AI OS is built.** This covers the architectural decisions behind the system: the two-layer model, the working memory approach, and the conventions for building and documenting new skills.

For how work gets planned, prioritised, and executed — the agile workflow, ceremonies, and sprint rhythm — see [[agile-workflow|Agile Workflow]]. For Jira configuration, see [[jira-system-design|Jira System Design]].

---

## AI OS Architecture

### The two-layer model

The AI OS operates on two layers:

- **Wiki (planning layer):** Source of truth for all strategic decisions — objectives, KRs, WSJF scores, definitions of done, and the rationale behind every prioritisation call. Human-readable, persistent, searchable.
- **Jira (execution layer):** Visual Kanban and sprint board. Populated from the wiki via `/jira-sync`. Provides status tracking, sprint assignment, and board visibility without duplicating planning logic.

Changes are always authored in the wiki and pushed to Jira. Jira manages status, assignees, and sprint membership — none of which flow back to the wiki.

### The two-board separation

Two Jira projects serve fundamentally different purposes:

| Board | Project | Prioritisation | Urgency model |
|-------|---------|---------------|---------------|
| Development Sprints | BWS | WSJF-scored | Cost of delay — continuous, intrinsic |
| BAU Kanban | PERF | Gut-prioritised | Deadline-driven — binary, external |

These reflect two different models of urgency that require different tools. Mixing them on one board would force an artificial choice between WSJF scoring (which doesn't apply to deadline-driven BAU tasks) and gut prioritisation (which systematically undervalues strategic work).

### Working memory model

Three distinct layers determine what context is available during a Claude session:

| Layer | Location | When available | Purpose |
|-------|----------|---------------|---------|
| Always-on context (universal) | `AGENTS.md` | Every session, every agent | Writing style, wiki structure, index doctrine, folder conventions, logging conventions |
| Always-on context (Claude-only) | `CLAUDE.md` | Every Claude session | Imports `AGENTS.md` (`@AGENTS.md`), then adds Claude-specific mechanics: memory, skills, hidden-file mirroring |
| Skill working memory | `~/.claude/skills/[skill]/SKILL.md` | When skill triggers | Operational instructions, tables, field mappings |
| Human reference | `wiki/ai-os/` | When explicitly read | Rationale, audit trail, browsable documentation |

The always-on layer is split so the universal rules live exactly once: `AGENTS.md` is the canonical cross-agent surface (read directly by Codex/OpenCode and imported by Claude Code), and each agent wrapper holds only its own loading-model-specific mechanics. See [[agent-instruction-architecture|Agent Instruction Architecture]] for the full three-layer model and the rule for where new content belongs.

Principles that need to be applied during execution belong in SKILL.md. Principles that exist for human understanding belong in `agile-workflow.md`, `jira-system-design.md`, or this document. Nothing in the wiki is automatically available as working memory: it must be explicitly read via an instruction in `AGENTS.md`, `CLAUDE.md`, or SKILL.md.

---

## Skill Design

### Why every skill has a matching wiki entry

Skills live in `~/.claude/skills/` — a session-tied location that may not persist or be easily navigable. The wiki entry at `wiki/ai-os/skills/[skill-name]/` is the stable, human-readable record of what the skill does and why it was built that way. It also acts as context for future Claude sessions when re-reading the skill is needed.

### Why Python scripts are embedded in Markdown, not stored as .py files in the wiki

Two reasons. First, the wiki is a documentation layer — `.py` files are artefacts, not documentation. Second, embedding code in Markdown allows annotation alongside the code: rationale, edge cases, known gotchas. A `.py` file in the wiki can't be annotated inline without polluting the script itself.

### Why shared files are copied into each skill, not imported across skills

Skills are intentionally self-contained. `credentials.py` and `gsheets_store.py` are copied into every skill's `scripts/` folder rather than imported from a shared location. The trade-off is deliberate: duplication is cheaper than the coupling and fragility that comes from cross-skill imports. If one skill needs a change to a shared file, it makes the change in its own copy without risking other skills.

### Why LLM model names are hardcoded in scripts

Relying on a provider default means the model can change without warning, breaking cost assumptions and output consistency. Hardcoding the model name (e.g. `claude-haiku-4-5-20251001`) makes the cost and capability contract explicit and version-controlled. Use Haiku for data orchestration tasks; Sonnet only when genuine reasoning is required.

### Why every skill requires a TESTING.md

Skills interact with external APIs, VPN routing, and credential stores — all of which can fail silently. A `TESTING.md` that documents what each test isolated, why it was needed, and what it revealed is the pre-flight checklist for future debugging sessions. Without it, the next debugging session starts from scratch.

> Detailed operational conventions (directory structure, credential handling, VPN routing, pre-flight checklist) are in `~/.claude/skills/skill-conventions.md`.

---

## Ad-hoc

*Placeholder for principles that don't yet fit a named category. Promote to a new heading when a cluster forms.*

---

## Key Takeaways

- The wiki is always the source of truth; Jira is the visual execution layer — changes flow one way only
- Two boards reflect two fundamentally different urgency models — mixing them would corrupt both
- SKILL.md is working memory (auto-loaded when skill triggers); wiki docs are human reference (not auto-loaded)
- Skills are self-contained by design — duplication of shared files is cheaper than cross-skill coupling
- Every principle that governs how work is planned, scored, or executed lives in [[agile-workflow|Agile Workflow]] and [[jira-system-design|Jira System Design]]
