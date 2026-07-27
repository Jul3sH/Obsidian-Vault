---
type: reference
updated: 2026-07-28
---

# Memory System Architecture

Agentic OS replaces the legacy MemSearch semantic memory system with a **PGLite + pgvector store** that runs locally without external dependencies, installs on Windows, and enables scope isolation per user/client/team.

## System Overview

The memory system consists of **four interconnected layers**:

```
Session ends
    ↓
[Session Capture Hook] → Summarize + archive raw transcript
    ↓
[Indexing Pipeline] → Discover files → chunk → embed → store
    ↓
[Database] (PGLite locally or Postgres hosted)
    ↓
[Search & Recall Layer] → Vector + keyword retrieval → scope filter → rerank → return
```

### Layer 1: Session Capture

Fires at every session end (Stop hook):

- **Extract** — pulls the latest user→assistant turn from the session
- **Summarize** — Claude Haiku generates 2-10 bullet summary
- **Append** — writes to daily `context/memory/{YYYY-MM-DD}.aos.md` (machine-owned, indexed)
- **Archive** — copies raw transcript to `context/transcripts/{YYYY-MM-DD}/` (gitignored, not indexed by default)
- **Dedup** — SHA-256 hash of source turn ensures replay is a no-op

### Layer 2: Indexing Pipeline

CLI: `npm run memory:index`

**Flow:**
1. Discover files (`.md`, `.markdown`, `.txt`) from standard roots: `context/memory/`, `context/learnings.md`
2. Skip unchanged files (content SHA-256 check)
3. INSERT/UPSERT into `memory_sources` table
4. Chunk markdown with line metadata, generate stable `chunk_key`
5. Embed chunks (BGE-M3, L2-normalized); reuse embeddings if key unchanged
6. INSERT chunks into `memory_chunks` table
7. Record audit row in `index_jobs` table
8. Prune stale keys

### Layer 3: Database (PGLite locally or Postgres hosted)

**What is PGLite?**
- Lightweight, embedded Postgres database from Electric SQL
- Full Postgres compiled to WebAssembly — not a clone
- In-process like SQLite but with full Postgres capabilities
- Persists to disk: single `data.db` file in `.command-centre/`
- No external dependencies, no cloud accounts needed, works on Windows/Mac/Linux

**What is pgvector?**
- Postgres extension for vector similarity search
- Adds `vector(N)` column type, `<=>` distance operators, HNSW indexing
- Available in both local PGLite and hosted Postgres

### Layer 4: Search & Recall

CLI: `npm run memory:recall`

**Three-rung ladder** (stop at the lowest rung that answers the question):

1. **Search** — hybrid retrieval: BGE-M3 vector search + Postgres full-text keyword search
   ```bash
   npm run memory:recall -- "<query>" --system --json
   ```

2. **Expand** — surrounding source context around a chunk (if search result too short)
   ```bash
   npm run memory:recall -- --expand <chunk-id> --system --json
   ```

3. **Transcript** — raw conversation window behind a chunk (if exact wording needed)
   ```bash
   npm run memory:recall -- --transcript <chunk-id> --system --json
   ```

## Why PGLite + pgvector replaced MemSearch

| Reason | MemSearch | PGLite + pgvector |
|--------|-----------|-------------------|
| **Windows fragility** | Required external account + API key + watcher processes on native Windows | Built-in, no account needed |
| **Heavy infrastructure** | Docker/Milvus + separate Python CLI | Single embedded database, no separate services |
| **Scope isolation** | No concept of scope; everything indexed into one global space | First-class scope columns: `private`, `client`, `team`, `system` with enforced no-leak boundary |
| **Multi-client safety** | Cross-tenant leakage possible | One client never sees another's memory |

## Storage per chunk

~5-6 KB (4 KB vector + 1-2 KB metadata)

**Examples:**
- 6 months light use: 25-30 MB
- 2 years moderate use: 1-1.75 GB
- Negligible laptop impact even at scale

## Embedding Model

**BGE-M3** (Beijing Institute of General Electronic Technology Model 3)
- **Dimension:** 1024 (L2-normalized for cosine distance)
- **Model size:** ~500 MB (downloaded on first setup, cached at `.command-centre/models/`)
- **Distance metric:** Cosine similarity
- **Why BGE-M3:** Strong multilingual support, good semantic richness

## No-Leak Guarantee

**Scope invariant (checked in application code AND enforced by database):**

Every search query filters by this predicate. No-leak tests prove zero cross-tenant leakage with seeded data.

**Only vulnerability:** Raw SQL that omits the scope predicate (code-review rule, not code-enforceable).

## Related Documentation

- [[agentic-os/memory-database-schema|Memory Database Schema]] — tables, indexes, canonical query
- [[agentic-os/session-capture-and-storage|Session Capture and Storage]] — transcript handling and storage
