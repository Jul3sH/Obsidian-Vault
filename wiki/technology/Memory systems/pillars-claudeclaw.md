---
type: reference
updated: 2026-08-01
concept: product-evaluation
product: ClaudeClaw Business OS
---

# ClaudeClaw, Scored Against Pillars, Use Cases, and Capabilities

> *How the ClaudeClaw memory system scores on **Capture, Storage, Injection, Recall**, plus the [[memory-use-cases]] and [[memory-capabilities]] those pillars support. For how it is built (tables, functions, decay factors), see [[claudeclaw-memory-system]]. Model: [[memory-pillars]].*

> [!note] Status: reference, not an adopted design
> An assessment of someone else's product against the four-pillar model. Nothing here is running in this vault.

Source: originally from [[claudeclaw-memory-system]] (verified against `claudeclaw-os/src` on 2026-07-25). Re-verified directly against `/Users/julianhart/claudeclaw-os/src/memory-ingest.ts`, `memory.ts`, and `db.ts` on 2026-08-01. All decay factors and thresholds in the wiki doc checked out exactly (0.99/0.98/0.95 salience decay; importance < 0.5 filter). Three details below were not in the wiki doc.

## Key Takeaways

- **The only system assessed so far with genuine *triggered* injection.** `buildMemoryContext` runs **every turn**, assembling context live from six layers. That is trigger option 4 in [[memory-pillars]], the deterministic content-injecting one, not to be confused with option 3 (a nudge with no content, MemSearch's pattern).
- **Aggressively curated capture.** An LLM extraction agent scores each turn and **discards anything below importance 0.5**. Most exchanges are never stored.
- **Layered on form**, like MemSearch: synthesised `memories` for retrieval, verbatim `conversation_log` underneath for exact recall.
- **It has a retention *policy*, not just a retention *setting*:** importance-tiered daily salience decay, with pinning as an exemption.
- **Capability shape:** strongest on triggered context discovery and memory health; good on reconstruction through `conversation_log`; partial on identity and current-work context because there is no explicit scheduled identity/current-project tier.
- **It is actually in use.** Contrast [[pillars-agentic-os]], which has better storage infrastructure and is "built but never ingested".

---

## Scorecard

| Pillar | Sub-type | ClaudeClaw |
|---|---|---|
| **Capture** | Continuous / periodic / boundary | **Continuous** - `ingestConversationTurn` fires after each turn |
| **Storage** | Kind of claim | **Undifferentiated** - no canonical/behavioural split; `importance` and `pinned` are the only value signals |
| **Storage** | Form | **Layered** - synthesised `memories` (summary, entities, topics) over verbatim `conversation_log` |
| **Storage** | Retention | **Curated, with a decay policy** - hard filter at importance < 0.5, then importance-tiered daily salience decay |
| **Injection** | Scheduled / triggered | **Triggered** - `buildMemoryContext` runs every turn, six layers |
| **Recall** | Write-time / query-time | **Query-time** - embedding cosine similarity (> 0.3, top 5), FTS5/LIKE keyword fallback |

## Use Case and Capability Coverage

| Use case | Capability | Coverage | Why |
|---|---|---|---|
| [[memory-use-cases|Know the user]] | [[memory-capabilities|Identity persistence]] | **Partial** | User-relevant memories can be retrieved per turn, but there is no explicit always-loaded identity tier in the assessed design |
| [[memory-use-cases|Resume the work]] | [[memory-capabilities|Critical context availability]] | **Partial** | Recent high-importance memories and team activity can surface context, but there is no derived current-project payload |
| [[memory-use-cases|Survive compaction]] | [[memory-capabilities|Compaction survival]] | **Strong where capture is continuous** | `buildMemoryContext` re-runs every turn and can re-inject relevant memory; continuous capture avoids the disk-loss problem |
| [[memory-use-cases|Preserve reasoning]] | [[memory-capabilities|Working reasoning preservation]] | **Partial** | `conversation_log` keeps verbatim turns, but the summarised memory layer is aggressively gated by importance |
| [[memory-use-cases|Recall old knowledge]] | [[memory-capabilities|Long-term knowledge recall]] | **Strong** | Query-time embedding recall plus keyword fallback |
| [[memory-use-cases|Reconstruct what happened]] | [[memory-capabilities|Episodic recall]] | **Strong** | The verbatim `conversation_log` layer holds real exchanges even when extraction compresses them away |
| [[memory-use-cases|Keep memory healthy]] | [[memory-capabilities|Retention management]] | **Strong** | Importance gate, duplicate detection, salience decay, and pinning form a real retention policy |
| [[memory-use-cases|Turn patterns into rules]] | [[memory-capabilities|Pattern-to-rule promotion]] | **Partial** | Consolidation derives insights while keeping sources, but this is not the same as promoting standing behavioural rules |
| [[memory-use-cases|Find unlocated context]] | [[memory-capabilities|Unlocated context discovery]] | **Strong** | Per-turn triggered semantic retrieval removes reliance on the human or agent remembering to search |
| [[memory-use-cases|Navigate curated knowledge]] | [[memory-capabilities|Curated knowledge navigation]] | **Missing** | No curated index hierarchy is part of the assessed memory system |
| [[memory-use-cases|Share memory across agents]] | [[memory-capabilities|Cross-agent memory federation]] | **Partial** | Team activity and a shared tier support some cross-agent awareness, but this is not a general multi-tool memory bus |
| [[memory-use-cases|Keep scopes separate]] | [[memory-capabilities|Scope-isolated recall]] | **Strong** | Agent-scoped memories plus an explicit shared tier create a clear isolation model |
| [[memory-use-cases|Recall what was true then]] | [[memory-capabilities|Temporal fact recall]] | **Missing** | No temporal validity model or entity graph was identified |
| [[memory-use-cases|Trace to source]] | [[memory-capabilities|Source-grounded recall]] | **Strong / partial** | `conversation_log` gives source grounding, though normal retrieval first surfaces synthesised memories |
| [[memory-use-cases|Turn workflows into procedures]] | [[memory-capabilities|Procedural memory generation]] | **Missing** | No skill-generation path was identified |

## Capture

An LLM "memory extraction agent" runs after each turn and returns `summary`, `importance` (0-1), `entities`, `topics`.

- **A cheap pre-filter runs before the LLM is even called.** `ingestConversationTurn` returns immediately if the user message is 15 characters or shorter, or starts with `/` (a command) - the extraction model is never invoked for these. Only past that gate does the importance filter apply.
- **The bar is deliberately high.** The extraction prompt states "most exchanges should be skipped" and applies a **hard filter: `importance < 0.5` is discarded**.
- **Semantic duplicate detection at ingest, not just at storage.** Before saving, the candidate memory's embedding is compared by cosine similarity against existing memories for that chat; anything above **0.85 similarity is skipped as a duplicate**. This is a second curation pass beyond the importance threshold.
- `importance >= 0.8` fires a callback offering the user a **pin**, exempting the memory from decay.
- Separately, `conversation_log` retains the full turn log regardless, so nothing is lost even when extraction compresses it away.
- **Resilience detail:** extraction primarily runs via the selected agent provider (Claude), with Gemini as fallback. A quota-aware backoff (5-minute cooldown on `429`) prevents repeated failed calls from spamming logs once a quota wall is hit.

**Consequence worth noting:** the high bar produces a sparse store. At the 2026-07-25 snapshot: **3 memories, 2 consolidations, 134 conversation-log rows.** Curation this aggressive means the synthesised layer is nearly empty while the verbatim layer carries the volume.

## Storage

Five SQLite tables. The two that matter for the model:

- `memories` - the synthesised layer. Carries `embedding`, `importance`, `salience`, `superseded_by`, `pinned`, `shared`.
- `conversation_log` - the verbatim layer, "holds real exchanges even when extraction compressed them away".

**Retention is an active policy, not passive accumulation.** Daily sweep multiplies `salience` by an importance-tiered factor:

| Importance | Daily factor |
|---|---|
| >= 0.8 | x 0.99, fades slowest |
| >= 0.5 | x 0.98 |
| < 0.5 | x 0.95, fades fastest |

`pinned` memories are exempt. This is the most developed retention mechanism among the systems assessed: most either keep everything or prune on a fixed schedule.

## Injection

**This is what distinguishes ClaudeClaw.** The `[Memory context]` block is assembled live, per turn, from up to six layers:

1. **Semantic search** on the current user message (cosine > 0.3, top 5)
2. **Recent high-importance** memories (deduped, top 5)
3. **Consolidation insights** (cosine > 0.3, top 2)
4. **Team activity** from other agents in the last 24h
5. **Conversation history recall**, keyword-triggered on `remember`, `recall`, `yesterday`, `we discussed`
6. **War-room transcript bridge**

Layer 1 is triggered injection in the strict sense: it fires on every turn without the user or the agent deciding to look. Layer 5 is a second, cheaper trigger keyed on intent words.

**A design choice worth stealing:** retrieval deliberately does **not** touch `salience` or `accessed_at`. Only a separate feedback loop (`evaluateMemoryRelevance`) boosts salience, because otherwise "noise retrieved once would stay fresh forever" - a positive-feedback trap. Most retrieval-boosts-relevance designs walk straight into this.

## Recall

Query-time hybrid: embeddings (`gemini-embedding-001`, corrected from "Google embedding-001") with cosine similarity, and an FTS5 mirror kept in sync by triggers as keyword fallback when embeddings are unavailable.

**A seventh context source exists beyond the six documented layers.** `buildMemoryContext` also calls `buildObsidianContext`, appending an Obsidian-vault context block when the agent has one configured (`agentObsidianConfig`). Not covered in [[claudeclaw-memory-system]] and not scored as a separate layer here, since it is vault-reading rather than memory-system behaviour, but worth flagging: the product this scorecard evaluates already bridges into an Obsidian vault, the same substrate this wiki runs on.

**A second synthesis pass exists.** `runConsolidation` clusters unconsolidated memories, has an LLM produce a merged summary plus one key insight, and stores that with its own embedding. So synthesis happens twice: once at ingest, once periodically across memories. That is not a pillar, but it is a real capability the model does not currently name.

## What it would and would not solve here

| | |
|---|---|
| **Would solve** | Injection (triggered). The binding constraint in this environment, and the pillar almost nothing else addresses |
| **Would duplicate** | Capture, already covered by native JSONL |
| **Would add** | Query-time Recall, a genuine gap |
| **Would not fit** | The undifferentiated store. This vault deliberately separates canonical from behavioural; ClaudeClaw does not model that distinction at all |

## Related

- [[claudeclaw-memory-system]] - how it is built: tables, functions, decay factors, known issues
- [[memory-pillars]] - the model being applied
- [[memory-use-cases]] - use case catalogue used for the coverage table
- [[memory-capabilities]] - capability catalogue used for the coverage table
- [[memory-features]] - feature catalogue used for implementation examples
- [[pillars-agentic-os]] - the contrast: better storage, no injection, never ingested
- [[pillars-memsearch]] - the contrast: per-turn nudge rather than true content injection
- [[pillars-mempalace]] - the contrast: no injection at all, but the only one with a compaction-safe capture hook
- [[memory-claudeclaw-vs-agentic-os]] - the existing head-to-head comparison
