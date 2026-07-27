---
type: reference
updated: 2026-07-28
---

# Memory Database Schema

Complete reference for the PGLite/pgvector memory store schema: tables, indexes, scope model, and the no-leak boundary.

## Scope Model

Every memory row carries **four scope columns**:

| Visibility | Who can read it | Required column | Local value |
|------------|-----------------|-----------------|-------------|
| **`private`** | one user | `user_id` | `NULL` (local single-user) |
| **`client`** | within one client workspace | `client_id` | folder slug under `clients/{slug}/` |
| **`team`** | within one team | `team_id` | `NULL` (local install) |
| **`system`** | baseline — everyone in the tenant | (none) | per-tenant baseline |

## Five Core Tables

### `memory_sources`
One row per normalized source document (file, captured session).

| Column | Type | Purpose |
|--------|------|---------|
| `id` | `uuid` | Primary key |
| `source_path` | `text` | File path or source identifier |
| `content_sha256` | `text` | Content hash for change detection |
| `content_date` | `date` | Date from filename (used for recency ranking) |
| `authority_weight` | `float` | Reranking weight from config |
| `team_id`, `client_id`, `user_id`, `visibility` | — | Scope columns |

### `memory_chunks`
One row per embedded chunk. **Scope denormalized from parent source.**

| Column | Type | Purpose |
|--------|------|---------|
| `id` | `uuid` | Primary key |
| `source_id` | `uuid` | Foreign key to memory_sources |
| `content` | `text` | Chunk text |
| `embedding` | `vector(1024)` | BGE-M3 1024-dim L2-normalized vector |
| `chunk_key` | `text` | Stable identity across re-indexes |
| `team_id`, `client_id`, `user_id`, `visibility` | — | Denormalized scope (must match source) |

### `index_jobs`
Work queue for indexer and capture hooks.

### `search_events`
Audit log for every scoped search.

### `schema_migrations`
Migration ledger with version and embed dimension.

## Scope Invariant (The Leak Boundary)

```sql
CHECK (
  (visibility = 'private' AND user_id   IS NOT NULL) OR
  (visibility = 'client'  AND client_id IS NOT NULL) OR
  (visibility = 'team'    AND team_id   IS NOT NULL) OR
  (visibility = 'system')
)
```

Enforced in **application code** (`scope.ts`) before INSERT and in the **database** as a CHECK constraint.

## Indexes

### Vector Index (HNSW + Cosine)

```sql
CREATE INDEX idx_memory_chunks_embedding_hnsw
  ON memory_chunks USING hnsw (embedding vector_cosine_ops)
  WITH (m = 16, ef_construction = 64);
```

- **Type:** HNSW (Hierarchical Navigable Small World)
- **Distance metric:** Cosine
- **Why HNSW?** No training step + good recall on small/cold corpus

### Scope Filter Indexes

```sql
CREATE INDEX idx_memory_chunks_scope
  ON memory_chunks (team_id, visibility, client_id, user_id);
```

## Canonical Search Query

The scope predicate is the single source of truth:

```sql
SELECT c.id, c.source_id, c.content, c.heading, c.source_path,
       (c.embedding <=> $3) AS distance
FROM memory_chunks c
WHERE c.team_id IS NULL            -- catastrophic-default safeguard
  AND c.embedding IS NOT NULL
  AND ( c.visibility = 'system'
     OR c.visibility = 'team'
     OR (c.visibility = 'client'  AND c.client_id = $1)
     OR (c.visibility = 'private' AND c.user_id   = $2) )
ORDER BY c.embedding <=> $3
LIMIT $4;
```

## Reranking Pipeline (Applied in Application Code)

1. **Authority** — source-path-prefix weights from `context/memory-config.json`
2. **Recency** — exponential decay, 14-day half-life, 0.7 floor
3. **Floor-ratio gating** — keep results >= top * 0.3

## PGLite vs Hosted Postgres Compatibility

All features run identically in both engines. The schema is pure SQL, portable across both.

## Related Documentation

- [[agentic-os/memory-system-architecture|Memory System Architecture]] — how indexing and search work
- [[agentic-os/session-capture-and-storage|Session Capture and Storage]] — transcript handling
