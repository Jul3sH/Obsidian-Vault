---
type: reference
updated: 2026-08-01
concept: product-evaluation
product: ClaudeClaw Business OS
---

# ClaudeClaw, Scored Against the Four Pillars

> *How the ClaudeClaw memory system scores on **Capture, Storage, Injection, Recall**. Scoring only. For how it is built (tables, functions, decay factors), see [[claudeclaw-memory-system]]. Model: [[memory-pillars]].*

> [!note] Status: reference, not an adopted design
> An assessment of someone else's product against the four-pillar model. Nothing here is running in this vault.

Source: [[claudeclaw-memory-system]], verified against `claudeclaw-os/src` on 2026-07-25.

## Key Takeaways

- **The only system assessed so far with genuine *triggered* injection.** `buildMemoryContext` runs **every turn**, assembling context live from six layers. That is trigger option 3, the deterministic one.
- **Aggressively curated capture.** An LLM extraction agent scores each turn and **discards anything below importance 0.5**. Most exchanges are never stored.
- **Layered on form**, like MemSearch: synthesised `memories` for retrieval, verbatim `conversation_log` underneath for exact recall.
- **It has a retention *policy*, not just a retention *setting*:** importance-tiered daily salience decay, with pinning as an exemption.
- **It is actually in use.** Contrast [[pillars-agentic-os]], which has better storage infrastructure and is "built but never ingested".

---

## Scorecard

| Pillar | Sub-type | ClaudeClaw |
|---|---|---|
| **Capture** | Continuous / boundary | **Continuous** - `ingestConversationTurn` fires after each turn |
| **Storage** | Kind of claim | **Undifferentiated** - no canonical/behavioural split; `importance` and `pinned` are the only value signals |
| **Storage** | Form | **Layered** - synthesised `memories` (summary, entities, topics) over verbatim `conversation_log` |
| **Storage** | Retention | **Curated, with a decay policy** - hard filter at importance < 0.5, then importance-tiered daily salience decay |
| **Injection** | Scheduled / triggered | **Triggered** - `buildMemoryContext` runs every turn, six layers |
| **Recall** | Write-time / query-time | **Query-time** - embedding cosine similarity (> 0.3, top 5), FTS5/LIKE keyword fallback |

## Capture

An LLM "memory extraction agent" runs after each turn and returns `summary`, `importance` (0-1), `entities`, `topics`.

- **The bar is deliberately high.** The source doc states "most exchanges are skipped" and applies a **hard filter: `importance < 0.5` is discarded**.
- `importance >= 0.8` fires a callback offering the user a **pin**, exempting the memory from decay.
- Separately, `conversation_log` retains the full turn log regardless, so nothing is lost even when extraction compresses it away.

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

Query-time hybrid: embeddings (Google `embedding-001`) with cosine similarity, and an FTS5 mirror kept in sync by triggers as keyword fallback when embeddings are unavailable.

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
- [[pillars-agentic-os]] - the contrast: better storage, no injection, never ingested
- [[memory-claudeclaw-vs-agentic-os]] - the existing head-to-head comparison
