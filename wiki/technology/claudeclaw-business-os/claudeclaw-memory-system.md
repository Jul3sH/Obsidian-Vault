# ClaudeClaw Memory System

> *How the ClaudeClaw bot remembers across conversations: a SQLite-backed, LLM-extracted, semantically-retrieved memory injected live into every turn. This is the system that produces the `[Memory context]` blocks. Verified against `claudeclaw-os/src` on 2026-07-25.*

Part of [[claudeclaw-business-os-overview|ClaudeClaw Business OS]]. For how this compares to the agentic-os memory layer, see [[memory-claudeclaw-vs-agentic-os|Memory: ClaudeClaw vs. agentic-os]].

---

## Storage (SQLite `store/claudeclaw.db`)

| Table | Role |
|---|---|
| `memories` | The atomic unit. `raw_text` (verbatim exchange), `summary`, `entities[]`, `topics[]`, `connections[]`, `importance` (0–1), `salience` (decays), `embedding` (Google `embedding-001`), `agent_id`, `superseded_by`, `pinned`, `shared`. |
| `memories_fts` | FTS5 mirror kept in sync by triggers (summary/raw_text/entities/topics) — keyword fallback when embeddings are unavailable. |
| `consolidations` | Merged cross-memory insights (`source_ids`, `summary`, `insight`, `embedding`) — the `Insights:` block. |
| `session_summaries` | Per-session summary + `key_decisions` + turn count + cost. |
| `conversation_log` | Full turn log — verbatim history recall (holds real exchanges even when extraction compressed them away). |

---

## Capture (`memory-ingest.ts`)

- After a turn, `ingestConversationTurn` runs an LLM **"memory extraction agent"** (this is the `queue-operation` event seen in raw transcripts). The bar is deliberately HIGH — most exchanges are skipped.
- It returns `summary`, `importance` (0–1), `entities`, `topics`.
- **Hard filter: `importance < 0.5` is discarded.** Only genuinely useful context is saved.
- The memory is embedded (Google `embedding-001`) for semantic search.
- `importance >= 0.8` fires a callback so the user can be offered a **pin**.

---

## Retrieval + injection (`buildMemoryContext`, runs every turn)

The `[Memory context]` block is assembled live, per turn, from up to six layers:

1. **Semantic search** — the user message is embedded; cosine similarity over memory embeddings (threshold > 0.3, top 5), FTS5/LIKE fallback if no embedding. → `Relevant memories:`
2. **Recent high-importance** memories (deduped, top 5).
3. **Consolidation insights** — cosine > 0.3 (top 2), LIKE fallback. → `Insights:`
4. **Team activity** — what other agents did in the last 24h.
5. **Conversation history recall** — triggered by keywords (`remember`, `recall`, `yesterday`, `we discussed`, ...); searches `conversation_log` for verbatim past turns. → `[Conversation history recall]`
6. **War-room transcript bridge** — recent multi-voice meeting lines.

**Key design choice:** retrieval does **not** touch `salience`/`accessed_at`. Only the feedback loop (`evaluateMemoryRelevance`) boosts salience — otherwise noise retrieved once would stay fresh forever (a positive-feedback trap).

---

## Salience decay (`decayMemories`, daily sweep)

Each day, `salience` is multiplied by an importance-tiered factor:

| Importance | Daily factor |
|---|---|
| ≥ 0.8 | × 0.99 (fades slowest) |
| ≥ 0.5 | × 0.98 |
| < 0.5 | × 0.95 (fades fastest) |

`pinned = 1` memories are exempt. Low-value memories decay out; important ones persist. Runs on startup and every 24h.

---

## Consolidation (`runConsolidation`)

Clusters unconsolidated memories, has an LLM produce a merged `summary` + **one key `insight`**, and stores it (with embedding) in `consolidations`. This is the source of the meta-level `Insights:` lines (e.g. the recurring "strategic life management" insight).

---

## Isolation & scoping

- Recall is scoped to the **calling agent + the shared tier** (`agent_id`, `shared = 1`) — fixes the cross-agent "Hive Mind" leak (#95).
- `/keep-shared` opts a multi-agent install back into cross-agent recall (#96); read per-turn, no restart needed.

---

## The nudge

`shouldNudgeMemory` decides when to append `MEMORY_NUDGE_TEXT` — the `[Memory nudge: ...]` line that appears when nothing has been saved to long-term memory in a while.

---

## Known issue: the `checkpoint` command is broken against this schema

The `checkpoint` command documented in `~/.claudeclaw/CLAUDE.md` inserts with columns `(chat_id, content, sector, salience, created_at, accessed_at)`. **The real `memories` schema has no `content` and no `sector` column** (they are `raw_text`/`summary` and `topics`), and `raw_text`/`summary` are `NOT NULL` with no default. As written, the checkpoint insert would fail. Fix: insert `raw_text`, `summary`, `topics`, `importance` using the real column names.

---

## Status (2026-07-25)

Live and populated: 3 memories, 2 consolidations, 134 conversation-log rows. This is the memory system actually in use for the Telegram assistant — unlike the agentic-os layer, which is built but never ingested.

---

## See Also
- [[memory-claudeclaw-vs-agentic-os|Memory: ClaudeClaw vs. agentic-os]]
- [[claudeclaw-business-os-overview|ClaudeClaw Business OS Overview]]
- [[session-transcripts-and-memory|Session Transcripts & the Memory Layer]]
