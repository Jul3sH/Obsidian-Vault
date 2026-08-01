# Claude Code Session Transcripts & the Memory Layer

> *How Claude Code stores raw session history, and how the Agentic OS memory layer consumes it. Captured from a working session on 2026-07-25.*

tags: [technical, claude, anthropic, memory, agentic-os]

This note explains where Claude Code keeps its raw conversation logs, what format they take, and how the Agentic OS memory system (curated memory + back catalogue import) is built on top of them.

---

## Session Transcripts (the raw layer)

- **What they are** — Claude Code's native, append-only log of every session. One file per session. This is default runtime behaviour, **not** anything configured in `CLAUDE.md`. `CLAUDE.md` is context injected into the prompt; it cannot create files. The CLI writes these transcripts regardless, to power `--resume`/`--continue` and rewind.
- **Format** — **JSONL** (JSON Lines): one JSON event per line, not a single JSON document. Parse by streaming line-by-line. Each `user`/`assistant` line carries a full envelope (`cwd`, `gitBranch`, `message`, `timestamp`, `sessionId`, `uuid`, `parentUuid`, `version`, ...). `parentUuid` links events into a tree, which is what enables branching/rewind.
- **Full, not summarized** — the `message.content` holds the complete verbatim text of every user and assistant message, plus full `tool_use` / `tool_result` blocks. Nothing is condensed on write. The only summary that ever appears is a compaction `summary` event in very long sessions, and even then the original turns remain. It is a lossless, replayable record.
- **One turn = several lines** — a turn that calls a tool is split across multiple JSONL lines (assistant text + `tool_use`, then a `user`-role `tool_result` line, then more assistant lines).

### Where they are stored

```
~/.claude/projects/<encoded-cwd>/<session-uuid>.jsonl
```

- The subfolder **name is the working directory**, path-encoded (slashes → dashes), e.g. `-Users-julianhart-Obsidian-Vault`. The name is a **label/mapping only** — the files physically live in the central `~/.claude/` store, one subfolder per project cwd.
- **Not stored inside the project folder.** Transcripts from the Obsidian Vault sessions are **not** in the vault; backing up or syncing the vault would not include them. Renaming/moving the vault starts a fresh subfolder and orphans the old history.
- **Local only** — everything is on the machine, nothing in the cloud.

---

## Storage Footprint (snapshot 2026-07-25)

| Store | Size | What it is |
|---|---|---|
| `~/.claude/projects/*.jsonl` | **103 MB** (136 files) | Raw verbatim transcripts (Claude Code native) |
| `~/.claude/projects/-Users-julianhart-Obsidian-Vault` | **102 MB** (110 files) | ~99% of the total — the actively-used environment |
| agentic-os `context/memory/` | ~0 (0 `.aos.md`) | Summarized memory — **empty, import never run** |
| agentic-os vector store | — | **Does not exist on disk yet** |
| `claudeclaw-os/store/claudeclaw.db` | 640 KB | Separate system: the Telegram assistant's memory |

- The only store that grows large is the **raw transcripts**, and they grow unbounded (nothing prunes them). 103 MB of text is not large in disk terms.
- `command-centre` shows 1.1 GB but that is **948 MB of `node_modules`** (app dependencies), unrelated to memory volume.

---

## The Agentic OS Memory Layer (the consuming layer)

Two distinct surfaces sit on top of the raw transcripts:

- **Curated working memory (`context/MEMORY.md`)** — a small, size-capped (~2,500 char) scratchpad of durable facts/decisions/preferences. A Stop hook promotes worthwhile items into it; it is injected at the **start of the next** session (frozen-snapshot pattern — mid-session writes take effect next session). Maintained by the `meta-memory-write` skill. It is **not** reserved for auto-capture; hooks or the user can write to it, subject to the cap and the frozen-snapshot timing.
- **Full capture + semantic recall** — every turn is summarized into `context/memory/{date}.aos.md` blocks, then chunked and embedded as vectors in a **local PGLite + pgvector** store (originally planned as Memsearch; swapped for local-only, Windows support, and per-user scoping). Recall is three-tier: read the snapshot first, else vector/keyword search → rerank → cited answer (source, line, date) or an honest "nothing found".

### Back catalogue = `memory-import-sessions.cjs`

- The doc's **"back catalogue becomes your brain"** feature **is** the script `command-centre/scripts/memory-import-sessions.cjs`. Same thing, two names.
- It discovers the raw JSONL transcripts under `~/.claude/projects/`, summarizes each session into the `.aos.md` blocks the live hook uses, then indexes them. User-controlled (dry-run / interactive / scriptable), idempotent, dedup-safe.
- **Status:** despite the doc tagging it "coming soon ETA July", the script already exists and is written. But it **has not been run** — hence the empty memory/vector stores above. Running it is the step that populates the searchable memory from existing history.

### Team memory

- Foundation is built: memory is tagged by visibility (`private` / `client` / `team` / `system`), threaded through ~10 scripts; the capture hook already emits `--visibility ... --client ...`; bootstrap branches on local vs hosted Postgres. Open question is completeness/testing (e.g. row-level security on the hosted store), not whether it needs writing from scratch.

---

## Verbatim Recall: MemPalace vs. Raw JSONL

The [Claude Memory Systems](https://docs.google.com/document/d/1d5Xk2G3xoyGUqYV_-vwwZRLjeFRhULrpvQIkGGGdKYQ) doc (Google Doc, external) places verbatim recall at **Level 4**, and documents exactly one system there: **MemPalace** (the "Memory Palace"). Verbatim recall is the strongest case for "just search the JSONL" — because unlike semantic memory, it needs no summarization; the transcripts already hold the exact words losslessly. So why does MemPalace exist?

**Because the JSONL contains the verbatim text but has no way to find it.** MemPalace's value is the index, structure, and entity graph layered on top — not the storage of verbatim text (the JSONL does that too).

**MemPalace design:**
- Nested structure: **Wings** (projects) → **Rooms** (sessions) → **Closets** (topics) → **Drawers** (verbatim text)
- Two stores: **SQL** for entity relationships + **Chroma** vector DB for searchable chunks
- A "dense symbolic dialect" (AA language) to scan thousands of drawers in ~42 ms
- Explicit goal: exact words/decisions **without summarization loss**

**What MemPalace has that raw JSONL lacks:**

| Dimension | Raw JSONL | MemPalace |
|---|---|---|
| Structure | Flat, keyed by session-UUID + cwd; one 8 MB session mixes many topics | Wings→Rooms→Closets→Drawers; topic-addressable |
| Retrieval unit | Verbatim buried in `message.content`, split by `parentUuid`, mixed with tool noise | Pre-segmented topic-coherent "drawers" |
| Index | None — linear byte scan + literal grep | SQL (entity/relationship) + Chroma (semantic vectors) |
| Meaning match | No — "deadline" won't find "decide by Wednesday" | Yes — vector rank + entity join |
| Speed at scale | Re-reads growing 103 MB per query, unindexed | ~42 ms via maintained index |
| Cross-session entities | None — each file an island | SQL links entities across all rooms |
| Durability | Volatile, cwd-keyed, CLI-owned; orphans on vault rename | Owns its store, decoupled |

**Why no documented system points at the JSONL:** (1) it's a *replay log, not a retrieval structure* — to search it you'd have to build MemPalace's index on top anyway, leaving only the choice of copying text vs. storing byte-offset pointers into a volatile foreign format; (2) the ecosystem is deliberately *tool-agnostic* (esp. L6 OpenBrain/Mem0, built to span Claude/ChatGPT/Cursor), and JSONL is Claude-Code-only.

**Neighbours on verbatim:** Claude Mem (L3) stores summaries/observations, not verbatim (lossy). MemSearch (L3) vectorises markdown chunks (lossy on phrasing). OpenBrain/Mem0 (L6) store facts in a portable `thoughts` table (fact-oriented, not a structured verbatim archive). MemPalace is the only one in the doc treating verbatim-with-structure as the goal.

---

## Where agentic-os sits on the 6-level map

From the same doc's tiering (L1 native → L6 universal brain):

- **L1 Native** — uses CLAUDE.md, SOUL.md, USER.md context injection. ✅
- **L2 Structured** — curated size-capped MEMORY.md + daily logs, hook-promoted. ✅
- **L3 Semantic/vector** — local PGLite + pgvector, three-tier retrieval with rerank/authority/recency. ✅ (this is the core)
- **L4 Verbatim** — **not** a MemPalace-style structured verbatim archive; the raw JSONL is the only verbatim source, and it's unindexed. ⚠️ Gap.
- **L5 Research wiki** — the Obsidian vault itself (Karpathy LLM-wiki pattern, knowledge graph). ✅ (separate from the memory pipeline)
- **L6 Universal brain** — foundation present (per-tenant visibility, local-vs-hosted-Postgres branch), not fully realised. 🟡

**Net:** agentic-os is a strong **L2+L3** operational memory with an **L5** wiki alongside, an emerging **L6** scoping layer, and **no dedicated L4** verbatim tier (it leans on raw transcripts for that).

---

## Key Takeaways

- **Raw transcripts are default Claude Code, full and verbatim, stored centrally under `~/.claude/projects/` — never inside the project/vault folder.**
- The Agentic OS memory system is a **pipeline**: raw JSONL → summarized `.aos.md` + vector index. It keeps the raw as the citable source and only summarizes for recall, so it never bloats context.
- **The back catalogue (`import-sessions`) is built but has never run**, so ~103 MB of history sits unremembered and the vector store is empty. Running it is what turns that history into searchable memory.

---

## See Also
- [[claude-code]] — the CLI itself
- [[claude-md-and-memory]] — persistent instructions via CLAUDE.md
- [[claudeclaw-business-os-overview]] — the Telegram assistant system
