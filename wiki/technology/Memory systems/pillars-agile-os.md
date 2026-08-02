---
type: reference
created: 2026-08-02
concept: product-evaluation
product: Agile OS
---

# Agile OS, Scored Against Pillars, Use Cases, and Capabilities

> *How the current Obsidian Vault memory system scores on **Capture, Storage, Injection, Recall**, plus the [[memory-use-cases]] and [[memory-capabilities]] those pillars support. Operational source of truth: [[memory-model-adoption]], [[memory-operations]], [[memory-convention]], [[memory-system-explained]], `AGENTS.md`, and `CLAUDE.md`. Model: [[memory-pillars]].*

> [!note] Status: adopted local system
> This is not an external product review. It is a technology scorecard for the memory system currently running around this Obsidian Vault, described here as Agile OS.

## Key Takeaways

- **Agile OS is an Obsidian-first memory system, not a database-backed memory product.** Its strongest layer is curated markdown: the wiki, indexes, bare wikilinks, project surfaces, and mirrored operational files.
- **It has a clean canonical vs behavioural split.** The wiki stores "is this true?" material; Claude memory stores "does this change how I act?" material.
- **Capture is partly solved by the host and partly by operating discipline.** Claude Code captures JSONL transcripts automatically, but they are inert until read. The real working memory is captured when agents write wiki articles, update indexes, update project surfaces, or create approved behavioural memories.
- **Injection is the binding constraint.** AGENTS and CLAUDE are always-on rulebooks, and Claude is instructed to load `user.md`, but there is no triggered injection, per-turn nudge, vector recall hook, or derived current-project payload.
- **Recall is write-time, transparent, and human-auditable.** The recall layer is `_index.md` navigation, bare wikilinks, and file search. There is no query-time semantic index over the wiki, and no searchable transcript memory layer.
- **The system is excellent for curated knowledge navigation and source-grounded work.** It is weaker for unlocated context discovery, compaction refresh, temporal truth, and cross-agent federation.

---

## Scorecard

| Pillar | Sub-type | Agile OS |
|---|---|---|
| **Capture** | Continuous / periodic / boundary | **Mixed.** Native Claude JSONL transcript capture is continuous, while wiki capture is agent-authored and event-driven by work outputs |
| **Storage** | Kind of claim | **Split canonical and behavioural.** Wiki for facts, decisions, evidence and project state; Claude memory files for user profile, behavioural corrections and hard rules |
| **Storage** | Form | **Curated markdown.** Synthesised at authoring or compile time, with source documents and links retained where relevant |
| **Storage** | Retention | **Curated and manual.** Index discipline, `_archived/`, raw processing, project status surfaces and two-key memory creation; no automated decay |
| **Injection** | Scheduled / triggered | **Scheduled / instruction-loaded only.** `AGENTS.md` and `CLAUDE.md` load by harness; Claude is instructed to load `user.md`; no triggered content injection |
| **Recall** | Write-time / query-time | **Write-time.** Master index, topic indexes, bare wikilinks and file search; no vector index or semantic retrieval layer |

## Use Case and Capability Coverage

| Use case | Capability | Coverage | Why |
|---|---|---|---|
| [[memory-use-cases|Know the user]] | [[memory-capabilities|Identity persistence]] | **Partial** | Claude has `user.md` and behavioural memory; cross-agent identity is weaker because the hidden Claude memory branch is not universal |
| [[memory-use-cases|Resume the work]] | [[memory-capabilities|Critical context availability]] | **Partial** | Project and deliverable state live in the wiki, with status surfaces, but there is no derived current-project payload automatically injected at session start |
| [[memory-use-cases|Survive compaction]] | [[memory-capabilities|Compaction survival]] | **Partial** | Durable wiki files survive, and host transcripts exist, but no `PreCompact` hook or triggered re-injection reasserts critical material mid-session |
| [[memory-use-cases|Preserve reasoning]] | [[memory-capabilities|Working reasoning preservation]] | **Partial** | Reasoning is preserved when written into wiki articles, reviews, project logs or transcripts; there is no deliberate working scratchpad or reasoning checkpoint |
| [[memory-use-cases|Recall old knowledge]] | [[memory-capabilities|Long-term knowledge recall]] | **Strong** | The wiki corpus, master index, topic indexes and bare wikilinks are built for durable knowledge recall |
| [[memory-use-cases|Reconstruct what happened]] | [[memory-capabilities|Episodic recall]] | **Partial** | Claude transcripts and project status logs exist, but transcript recall is not indexed and reconstruction is mostly manual |
| [[memory-use-cases|Keep memory healthy]] | [[memory-capabilities|Retention management]] | **Partial / strong manually** | The vault has index doctrine, `_archived/`, raw processing, and two-key behavioural memory creation, but no automated salience decay, pinning or pruning |
| [[memory-use-cases|Turn patterns into rules]] | [[memory-capabilities|Pattern-to-rule promotion]] | **Strong manually** | User-approved feedback memories, AGENTS updates and skill conventions can promote repeated corrections into durable rules |
| [[memory-use-cases|Find unlocated context]] | [[memory-capabilities|Unlocated context discovery]] | **Weak / partial** | `rg` and agent search can find material, but there is no semantic index and no automatic trigger to search dormant context |
| [[memory-use-cases|Navigate curated knowledge]] | [[memory-capabilities|Curated knowledge navigation]] | **Strong** | This is the system's core strength: master index, topic indexes, one-line descriptions, bare wikilinks and filing discipline |
| [[memory-use-cases|Share memory across agents]] | [[memory-capabilities|Cross-agent memory federation]] | **Partial** | AGENTS and the wiki are shared across agents, but Claude auto-memory is Claude-specific and there is no common memory bus |
| [[memory-use-cases|Keep scopes separate]] | [[memory-capabilities|Scope-isolated recall]] | **Partial** | Filing taxonomy and project/workstream boundaries separate context conceptually, but there are no query-time scope predicates or access controls |
| [[memory-use-cases|Recall what was true then]] | [[memory-capabilities|Temporal fact recall]] | **Weak / partial** | Project logs, file dates and git history can help, but there is no temporal validity model or entity graph |
| [[memory-use-cases|Trace to source]] | [[memory-capabilities|Source-grounded recall]] | **Strong for wiki, partial for transcripts** | Wiki articles preserve links, sources and rationale; raw transcripts exist but are not a normal recall tier |
| [[memory-use-cases|Turn workflows into procedures]] | [[memory-capabilities|Procedural memory generation]] | **Partial** | Skills, AGENTS rules and playbooks can be created from repeated workflows, but this is human-approved and manual rather than generated automatically |

## Capture

Agile OS has two different capture paths, and they should not be confused.

**Host capture is continuous but inert.** Claude Code stores JSONL transcripts automatically outside the vault. This means conversation evidence exists, but it is not automatically memory. It only affects future work when an agent deliberately reads it or when a session outcome is written into the wiki.

**Wiki capture is deliberate.** The working memory system becomes useful when agents create or update:

- wiki articles,
- project and deliverable status surfaces,
- topic indexes,
- raw file processing records,
- skill mirrors,
- Claude behavioural memory mirrors.

This is why the system behaves more like Karpathy's "LLM-maintained wiki" pattern than a passive transcript archive. The captured object is usually a curated markdown artefact, not the raw exchange.

**Behavioural capture uses a two-key process.** Claude can propose a new memory when a persistent behavioural correction is observed, but Julian confirms before it is written, except for explicitly flagged wrong behaviour. That protects the behavioural branch from memory bloat and accidental overreach.

## Storage

Agile OS's strongest design decision is the split between two storage branches:

| Branch | Question it answers | Location | Examples |
|---|---|---|---|
| **Canonical** | Is this true? | `wiki/` | research, decisions, project state, technology reference, source-backed conclusions |
| **Behavioural** | Does this change how the agent acts? | Claude hidden memory path, mirrored into the wiki | `user.md`, `feedback-*.md`, rare hard rules |

The canonical branch is visible, navigable and human-owned in Obsidian. It uses `_index.md` files, `[[wikilinks]]`, project status surfaces, raw processing rules and source-of-truth conventions to keep memory browsable.

The behavioural branch is narrower. It avoids storing project state, research or task context. Those belong in the wiki and are recalled on demand. Behavioural memory stores preferences, recurring corrections and serious hard rules.

Retention is mostly manual but disciplined: index updates, `_archived/` folders, raw inbox processing, mirror maintenance, project status updates and two-key memory creation. There is no salience decay, pinning, duplicate detection, or compression job.

## Injection

Injection is where Agile OS is weakest.

The strong always-on layer is the rulebook:

- `AGENTS.md` is the cross-agent operating layer, loaded directly by Codex and OpenCode and imported by Claude.
- `CLAUDE.md` adds Claude-specific mechanics, including the memory loading rule, skills and hidden-file mirroring.
- Claude is instructed to read `user.md` at session start and load other memory files on demand.

This gives Agile OS a real scheduled injection layer for operating rules. It does not give it strong content injection.

There is no mechanism that:

- derives the current project, blocker and next action into a compact payload,
- injects relevant wiki context every turn,
- nudges the agent to search on `UserPromptSubmit`,
- re-injects critical facts after compaction,
- runs semantic search automatically against dormant context.

The practical consequence is familiar: the store can be excellent and still fail to influence the answer if nothing triggers retrieval.

## Recall

Recall is write-time and curated.

The recall layer is:

- `wiki/_master-index.md`,
- topic `_index.md` files,
- one-line index descriptions,
- bare `[[wikilinks]]`,
- source links inside articles,
- file search with `rg` or equivalent tools.

This is strong when the actor has a plausible starting point: a topic, project, filename, keyword, or linked concept. It is transparent and cheap, and a human can inspect the retrieval structure directly.

It is weaker when the actor remembers only the substance and has no location, keyword or topic hypothesis. That is the unlocated context discovery gap. The current standing decision is not to add a vector index over the wiki corpus until the corpus outgrows curated navigation or repeated misses are observed. The transcript corpus is a separate candidate for semantic indexing because it is large, raw and uncurated.

## What it would and would not solve here

| | |
|---|---|
| **Solves well** | Curated knowledge navigation, long-term knowledge recall, source-grounded wiki work, human auditability, manual pattern-to-rule promotion |
| **Partially solves** | Identity persistence, critical context availability, compaction survival, episodic reconstruction, procedural memory generation |
| **Does not solve well** | Triggered injection, unlocated context discovery at scale, temporal fact recall, cross-agent federation, automated memory health |
| **Next logical builds** | Derived current-context payload, semantic search over JSONL transcripts, triggered injection or at least a per-turn nudge, cross-agent memory federation |

## Related

- [[memory-model-adoption]] - adopted four-pillar frame and current configuration
- [[memory-operations]] - runtime configuration of the memory system here
- [[memory-convention]] - memory file types, format and behavioural branch rules
- [[memory-system-explained]] - ownership view of Claude memory
- [[system-design-principles]] - AI OS working-memory model
- [[memory-pillars]] - the model being applied
- [[memory-use-cases]] - use case catalogue used for the coverage table
- [[memory-capabilities]] - capability catalogue used for the coverage table
- [[memory-features]] - feature catalogue used for implementation examples
- [[memory-challanges]] - challenge catalogue this scorecard helps answer
