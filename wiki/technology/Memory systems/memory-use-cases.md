---
type: reference
created: 2026-08-01
authority: analysis-backed
concept: use-case-catalogue
---

# Memory Use Cases

> *Actor-outcome journeys for agent memory systems. Use cases describe why memory is needed; [[memory-capabilities]] describes the reusable abilities that enable them; [[memory-features]] describes the concrete mechanisms that implement those abilities.*

## Key Takeaways

- **A use case has an actor, trigger or context, goal, and value outcome.** It is not a feature and not an architecture function.
- **Use case names should be memorable.** The name is a short handle; the sentence below carries the actor-outcome detail.
- **Use cases consume capabilities.** One use case may consume several capabilities, and one capability may support several use cases.
- **Features implement the supporting capabilities.** A hook, vector search, index, graph, or recall ladder is implementation, not the use case itself.

## Catalogue

| # | Use case | Use case statement | Primary capabilities | Representative features |
|---|---|---|---|---|
| 1 | **Know the user** | When a new session starts, the AI agent needs to know who it is working with so that the user does not have to re-establish preferences, identity, and working style | [[memory-capabilities|Identity persistence]] | `SessionStart` injection, `USER.md` / `user.md` stores |
| 2 | **Resume the work** | When a new session starts or work resumes, the AI agent needs to know the active project, blockers, and next action so that work resumes from the right place | [[memory-capabilities|Critical context availability]] | Derived critical-context payload, `PROJECT.md` distillation, scheduled snapshot |
| 3 | **Survive compaction** | When context compaction occurs, the AI agent needs critical material to return mid-session so that important facts do not silently disappear | [[memory-capabilities|Compaction survival]] | `PreCompact` hook, triggered context injection, derived critical-context payload |
| 4 | **Preserve reasoning** | When a long analytical session accumulates assumptions, dead ends, and rejected options, the AI agent needs to preserve and re-surface the working reasoning so that later answers do not repeat old paths or drift after context rot | [[memory-capabilities|Working reasoning preservation]] | Working scratchpad, reasoning checkpoint, compaction summary, triggered context refresh |
| 5 | **Recall old knowledge** | When a user or agent needs a fact, decision, or pattern recorded months ago, the system needs to retrieve it so that current work stays consistent with prior knowledge | [[memory-capabilities|Long-term knowledge recall]] | Curated index retrieval, semantic search, vector search, full-text search |
| 6 | **Reconstruct what happened** | When a user asks what happened, why a choice was made, or how a conclusion developed, the system needs to recover past session events so that reasoning and provenance can be inspected | [[memory-capabilities|Episodic recall]], [[memory-capabilities|Source-grounded recall]] | Native JSONL transcripts, transcript rung, closet references |
| 7 | **Keep memory healthy** | When memory grows over time, the system needs to compress, archive, decay, or prune material so that useful memory does not drown in stale material | [[memory-capabilities|Retention management]] | Salience decay, pinning, compression, archiving, importance gates |
| 8 | **Turn patterns into rules** | When repeated observations reveal a stable preference, correction, or workflow, the system needs to promote the pattern into a standing rule so that future sessions improve | [[memory-capabilities|Pattern-to-rule promotion]] | Daily memory distillation, feedback rules, `PROJECT.md` / `USER.md` distillation |
| 9 | **Find unlocated context** | When the user or agent remembers the substance of something but not where it lives, the system needs to find the relevant material so that dormant or poorly filed context can still influence the work | [[memory-capabilities|Unlocated context discovery]] | Semantic search, dense vector search, hybrid search, per-turn retrieval |
| 10 | **Navigate curated knowledge** | When the actor knows the domain or likely topic area, the system needs to navigate a curated knowledge structure so that the right material is found transparently and cheaply | [[memory-capabilities|Curated knowledge navigation]] | Curated index retrieval, `_index.md` hierarchy, bare wikilinks |
| 11 | **Share memory across agents** | When work moves between AI tools, the user's prior context needs to be available across agents so that knowledge is not fragmented by client boundary | [[memory-capabilities|Cross-agent memory federation]] | Shared memory store, MCP memory gateway |
| 12 | **Keep scopes separate** | When multiple clients, agents, or tenants share infrastructure, the system needs to retrieve only permitted memory so that private context does not leak | [[memory-capabilities|Scope-isolated recall]] | Scope predicates, per-agent memory tier, shared memory tier |
| 13 | **Recall what was true then** | When facts change over time, the system needs to answer what was true at a past date so that current truth is not mistaken for historical truth | [[memory-capabilities|Temporal fact recall]] | Temporal entity knowledge graph, validity windows, `mempalace_kg_query` |
| 14 | **Trace to source** | When a retrieved answer matters, the system needs to trace it back to original source material so that the user can verify it | [[memory-capabilities|Source-grounded recall]] | Transcript rung, closet references, source links |
| 15 | **Turn workflows into procedures** | When a workflow recurs, the system needs to turn it into a reusable procedure so that future work is faster and more reliable | [[memory-capabilities|Procedural memory generation]], [[memory-capabilities|Pattern-to-rule promotion]] | Skills from Memory, skill candidates, feedback rules |

## Traceability

```text
Use case -> Capability -> Architecture functions -> Features
```

Example:

| Level | Example |
|---|---|
| Use case | Preserve reasoning |
| Capability | [[memory-capabilities|Working reasoning preservation]] |
| Architecture functions | Capture + Storage + Injection |
| Features | Working scratchpad, reasoning checkpoint, triggered context refresh |

## Related

- [[memory-capabilities]] - reusable abilities that support these use cases
- [[memory-features]] - concrete mechanisms that implement or expose those capabilities
- [[memory-pillars]] - architecture functions underneath the capability model
- [[memory-systems-taxonomy-codex-review-2026-08-01]] - review that prompted this separation
