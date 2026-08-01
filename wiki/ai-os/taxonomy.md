---
type: reference
created: 2026-05-20
---

# AI OS Taxonomy

**Open this when you need to decide where a new AI OS document belongs.** This is the canonical filing rule for everything under `wiki/ai-os/`.

---

## The Four Categories

### Service Design
**People and process.** Operational workflows, agile workflows, implementation workflows, strategy, prioritisation methodology, ceremonies, and the rules that govern how work flows through the system.

If it describes *what people do* or *how processes run*, it goes here.

**Location:** [[service-design/_index|wiki/ai-os/service-design/]]

### System Design
**Tools and infrastructure.** The architecture of the tools that support the people and processes — system principles, integration design (Jira, APIs), file conventions, mirroring rules, build standards, and the Claude harness (memory system).

If it describes *how the supporting tools are constructed or maintained*, it goes here.

**Location:** [[system-design/_index|wiki/ai-os/system-design/]]

### Templates
**Reusable artifact patterns.** Fill-in-the-blank scaffolds for producing consistent, well-structured `.md` files — prompt templates, document templates, and other repeatable output patterns. Templates are neither process documentation nor infrastructure documentation; they are output patterns.

If it is a reusable scaffold for producing a specific type of artifact, it goes here.

**Location:** [[templates/_index|wiki/ai-os/templates/]]

### Skills (Hybrid)
**Process bundled with implementation.** Skills are a deliberate hybrid: the `SKILL.md` file is service design (the process Claude follows) and the `scripts/` directory is system design (the code that executes it). They are kept together because a skill is a *unit of deployment*, not a document — separating them would make skills harder to audit and would break parity with the operational reality at `~/.claude/skills/`.

**Location:** [[skills/_index|wiki/ai-os/skills/]]

---

## Gate 0: Is this AI OS at all?

Apply this **before** the filing test below. AI OS holds the operating layer *actually
in use here*. Generic knowledge about how a class of system works is reference
material and belongs in `wiki/technology/`.

> **Would this document still be true if this entire environment were deleted and
> rebuilt from scratch?**
>
> - Yes, it describes how a kind of system works → **`wiki/technology/`**
> - No, it describes what is actually running → **`wiki/ai-os/`**

### Worked example: memory

Memory content splits across both indexes, which makes it the clearest illustration.

| Document | Home | Reasoning |
|---|---|---|
| `memory-pillars`, `memory-capture`, `memory-storage`, `memory-injection`, `memory-recall`, `memory-curated-index`, `memory-semantic-search`, `wiki-vs-openbrain` | `technology/Memory systems/` | The four-pillar model, its enabler technologies, vendor comparisons and decision tests. True regardless of what runs here |
| `memory-model-adoption` | `ai-os/system-design/generic/` | The **decision** to adopt the four-pillar frame. A decision record, not a copy of the model |
| `memory-convention`, `memory-operations`, `memory-system-explained` | `ai-os/system-design/claude/memory/` | Describe the memory system actually in use, its types, format and loading rules |
| `user.md`, `MEMORY.md`, `feedback-*.md`, `project-*.md` | `ai-os/system-design/claude/memory/` | Mirrors of live hidden files. These **are** the running system |

### Hard constraint: mirrors never move

Any file mirroring a hidden source (skills, memory, harness config) is **pinned** to
the mirror path defined in its harness mirror map. It is never refiled by a taxonomy
decision, because the mirror path is what makes an otherwise invisible file
discoverable in Obsidian. If a mirror looks misfiled, mirrors are exempt; the mirror
does not move. See the Hidden File Visibility rule in `AGENTS.md`.

The same holds for the auto-memory files themselves. They stay in AI OS not because
of their subject matter but because they are live operating state, not reference.

---

## The Filing Test

Once Gate 0 has placed a document inside AI OS, ask:

> **Is this about people/process/operations, or about the tools that support them?**

- People/process/operations → **Service Design**
- Tools/infrastructure/conventions → **System Design**
- Both, bundled as one unit → **Skill**

### Default Rule

When in doubt, default to **Service Design**. System Design is the smaller, more specific category — reserved for documents that describe infrastructure, architectural principles, or build conventions. Service Design absorbs the long tail of operational and strategic content.

### Edge Cases — Worked Examples

| Document | Category | Reasoning |
|----------|----------|-----------|
| `project-workflow.md` | Service Design | Describes the planning hierarchy and ceremonies — process |
| `wsjf.md` | Service Design | Prioritisation methodology — strategy/process |
| `timebox-planning.md` | Service Design | How timeboxes are planned (DSDM MoSCoW rules) — process |
| `project.md`, `deliverable.md` | Service Design | Definitions of work artefacts and how they are managed — process |
| `portfolio-kanban.md`, `portfolio-backlog.md` | Service Design | Workflow stages and flow management — process |
| `api-skill-troubleshooting.md` | Service Design | Operational troubleshooting workflow — process, not infrastructure |
| `system-design-principles.md` | System Design | Architectural principles for the AI OS itself — infrastructure |
| `jira-system-design.md` | System Design | Jira project configuration and field mappings — tool design |
| `skill-conventions.md` | System Design | How skills are constructed (directory layout, embedded scripts) — build standard |
| `hidden-file-sync.md` | System Design | Mirroring architecture between hidden paths and wiki — infrastructure rule |

---

## Skills as a Hybrid — The Convention

Within `wiki/ai-os/skills/[skill-name]/`:

| File / folder | Layer |
|---------------|-------|
| `SKILL.md` | Service Design — process instructions Claude follows |
| `_index.md` | Service Design — human-readable overview |
| `architecture.md` | System Design — how the skill is built |
| `TESTING.md` | System Design — test methodology and gotchas |
| `scripts/` | System Design — executable code |

The skill *as a whole* is a hybrid unit. Treat it that way — don't try to split it across the two top-level folders.

---

## Why This Taxonomy Exists

Without an explicit filing rule, reference documents accumulate in a single bucket and the difference between "this is how we work" and "this is how the system is built" gets lost. Splitting the two means:

- **Service Design changes** when the way work is planned or prioritised changes — i.e. when we change the *process*
- **System Design changes** when the supporting tools, integrations, or architectural conventions change — i.e. when we change the *infrastructure*

These are different rates of change, different audiences, and (often) different decisions. Keeping them separate makes both easier to navigate and easier to maintain.

---

## Where to File New Documents

- New project/strategic/operational workflow → `service-design/`
- New tool integration design or architectural principle → `system-design/`
- New skill (process + scripts as a unit) → `skills/[skill-name]/`
- New ambiguous reference document → default to `service-design/` unless it clearly describes infrastructure
- New reusable artifact scaffold (prompt template, document template) → `templates/`

If it doesn't fit any of the four categories, flag it — don't add a new category without agreement.

---

## Links

- [[service-design/_index|Service Design]] — workflow, ceremonies, prioritisation, operations
- [[system-design/_index|System Design]] — architecture, integrations, file conventions
- [[skills/_index|Skills]] — the hybrid category
- [[templates/_index|Templates]] — reusable artifact patterns
- [[_index|AI OS Index]]
