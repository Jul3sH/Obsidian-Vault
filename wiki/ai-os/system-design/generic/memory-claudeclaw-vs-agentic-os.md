---
type: reference
created: 2026-07-25
tags: [ai-os, system-design, memory, claudeclaw, agentic-os, comparison]
---

# Memory: ClaudeClaw vs. agentic-os

> *Both systems bolt a memory layer onto Claude Code, but they diverge on substrate, timing, and dependency. Open this to understand why the ClaudeClaw bot remembers you day-to-day while the agentic-os brain sits empty. Verified against both codebases on 2026-07-25.*

They share a shape — atomic memories + semantic recall + a consolidation/insight layer — but the engineering differs at every layer. Deep-dives: [[claudeclaw-memory-system|ClaudeClaw Memory System]] and [[session-transcripts-and-memory|Session Transcripts & the Memory Layer]].

---

## Side by side

| Dimension | ClaudeClaw | agentic-os |
|---|---|---|
| **Substrate** | SQLite (`claudeclaw.db`) + FTS5 | Markdown `MEMORY.md` + `.aos.md` logs + PGLite/pgvector |
| **Capture** | LLM extraction agent per turn; `importance ≥ 0.5` filter; automatic | Stop hook promotes to `MEMORY.md` + summarizes each turn to `.aos.md` |
| **Embeddings** | Google `embedding-001` (needs `GOOGLE_API_KEY`, external) | pgvector in PGLite (local, no external dependency) |
| **Recall** | `buildMemoryContext` — 6 layers, every turn | 3-tier: snapshot → vector/keyword → rerank → cited answer |
| **Injection timing** | **Live, every turn** (dynamic retrieval) | **Frozen snapshot at SessionStart** + on-demand recall |
| **Decay/ranking** | Daily exponential decay by importance; pinned exempt | Reranker: `half_life_days=14`, authority weights, recency floor |
| **Consolidation** | LLM clusters memories → one insight, stored | "Dreaming" promotes recurring daily notes to long-term |
| **Verbatim source** | `conversation_log` (in the DB) + `raw_text` per memory | External raw JSONL transcripts + `.aos.md` summaries |
| **Scoping** | Per-agent + shared tier (`agent_id`, `shared`) | Visibility: private/client/team/system (+ hosted RLS) |
| **Citations** | Topic/importance tags; not source-cited | Cites source/line/date (GBrain-inspired) |
| **Dependency** | External embeddings API | Fully local by design |
| **Status** | **Live & populated** (3 memories, 2 consolidations, 134 log rows) | **Empty** — built but never ingested |

---

## The three differences that matter

**1. Injection timing — dynamic vs. frozen.** ClaudeClaw retrieves semantically and injects a fresh `[Memory context]` block **every turn**, tuned to the current message. agentic-os loads a **frozen `MEMORY.md` snapshot once at session start** (the Hermes pattern) and only searches the vector store on demand. ClaudeClaw is more responsive per-message; agentic-os is cheaper and more stable within a session but staler mid-session.

**2. Dependency — external vs. local.** ClaudeClaw's semantic layer **depends on Google's embedding API** (falls back to FTS5 keyword if the key/API is unavailable). agentic-os **deliberately chose local PGLite** specifically to avoid an external dependency (and to get Windows support + per-user scoping). So ClaudeClaw carries exactly the external dependency the agentic-os design set out to eliminate.

**3. Reality — one runs, one doesn't.** ClaudeClaw's memory is **live and populated** and is what actually remembers you across Telegram sessions. agentic-os's memory is **fully built but never ingested** — the stores are empty because the back-catalogue import has not been run. Day-to-day, the memory you rely on is ClaudeClaw's.

---

## Verbatim recall contrast

- **ClaudeClaw** keeps verbatim inside the DB: `conversation_log` (full turns) + `raw_text` on each memory, retrievable via the keyword-triggered history-recall layer.
- **agentic-os** has no in-store verbatim tier; it leans on the external Claude Code JSONL transcripts (see [[session-transcripts-and-memory]]), which are unindexed. This is the L4 gap noted there — neither system has a MemPalace-style structured verbatim archive.

---

## See Also
- [[claudeclaw-memory-system|ClaudeClaw Memory System]] — the full ClaudeClaw mechanics
- [[session-transcripts-and-memory|Session Transcripts & the Memory Layer]] — the agentic-os side + transcripts
- [[claudeclaw-vs-agentic-os|ClaudeClaw vs. agentic-os]] — the broader system comparison
- [[pointer-vs-copy|Pointer vs. Copy]]
