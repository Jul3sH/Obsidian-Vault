---
type: reference
created: 2026-07-29
tags: [technology, database, postgres, vector-search, ai]
---

# Postgres, pgvector, PGLite and Supabase

> *Four terms that appear together in AI memory system documentation and are easy to conflate. Only one of them is a database engine.*

## The One-Line Answer

**Postgres is the engine. pgvector is a feature you switch on inside it. PGLite and Supabase are just different places that same engine can run.**

Mental model: Postgres is the car. pgvector is a roof rack you bolt on. Supabase, hosted Postgres, and PGLite are whether the car lives in a rented garage, sits in your driveway, or folds up small enough to fit in a drawer. Same car in every case.

## What Each Term Actually Is

| Term | Category | What it does |
|---|---|---|
| **PostgreSQL (Postgres)** | **Database engine** | The actual software. Stores tables, runs queries, enforces constraints. The base thing everything else attaches to |
| **pgvector** | **Extension** (not a database) | Adds a `vector(N)` column type, distance operators (`<=>`), and vector indexes (HNSW) to Postgres. This is what makes semantic similarity search possible |
| **PGLite** | **Packaging of Postgres** | The real Postgres engine compiled to WebAssembly, running embedded in your app as a single `data.db` file. No server, no install, no cloud account |
| **Supabase** | **Hosting platform** | Runs Postgres for you in the cloud, with a dashboard, auth, and APIs layered on top. Still Postgres, just on someone else's server |

## Why pgvector Is Not a Database

This is the distinction that matters most.

- pgvector is a **plugin that bolts onto Postgres.** It cannot run on its own because it has nothing to run *in*.
- Without it, Postgres cannot answer "find the 10 most semantically similar chunks to this query".
- With it installed, an ordinary Postgres table can hold **embeddings** (numeric vectors representing meaning) and be searched by similarity rather than by exact match.
- Concretely, it provides:

| Feature | Purpose |
|---|---|
| `vector(1024)` column type | Stores a 1024-dimensional embedding in a normal table column |
| `<=>` operator | Cosine distance between two vectors, used for "how similar is this?" |
| HNSW index | Hierarchical Navigable Small World index, making similarity search fast without a training step |

## Why PGLite Is Not "Postgres Lite"

The name suggests a cut-down clone. It is not.

- It is **full Postgres compiled to WebAssembly**, not a reimplementation.
- It runs **in-process** like SQLite (no separate server to start or manage) but retains full Postgres capabilities, including extensions such as pgvector.
- It persists to a **single file on disk**, making backup a file copy.
- It works identically on Windows, macOS, and Linux with no external dependencies or accounts.
- Schemas written for PGLite are pure SQL and portable to hosted Postgres unchanged.

## Applied to the AI Memory Systems

Both systems documented in this wiki use **the same engine with the same extension**. They differ only in where the engine runs.

| System | Where Postgres runs | Still Postgres? | pgvector? |
|---|---|---|---|
| **OB1 (OpenBrain)** | Supabase (cloud-hosted), or self-hosted on Kubernetes | Yes | Yes |
| **Agentic OS** | PGLite (embedded locally) by default, hosted Postgres optional | Yes | Yes |

So the frequently quoted contrast of "Supabase or hosted Postgres" versus "PGLite locally" is **a difference of location, not of database kind.** Both are Postgres with vector search enabled.

## Supporting Terms

Concepts that appear alongside these four in AI memory documentation.

| Term | Meaning |
|---|---|
| **Embedding** | A list of numbers representing the meaning of a piece of text, so that similar meanings sit close together in vector space |
| **Embedding model** | The model that produces those numbers. Agentic OS uses BGE-M3 at 1024 dimensions |
| **L2-normalised** | Vectors scaled to unit length, so cosine similarity and distance behave predictably |
| **Cosine distance** | Measures the angle between two vectors. Small angle means similar meaning |
| **Chunk** | A slice of a document, embedded and stored as one searchable row |
| **Hybrid search** | Vector similarity combined with traditional full-text keyword search, so both meaning and exact terms are matched |
| **Reranking** | Reordering raw search hits by additional signals such as source authority or recency |

## Key Takeaways

- **pgvector is not a database.** It is an extension that teaches Postgres to do semantic similarity search.
- **Postgres is the only database engine in the list.** Everything else is either a feature of it or a place to run it.
- **PGLite is genuinely Postgres**, compiled to WebAssembly and embedded as a single local file. Not a lightweight clone.
- **Supabase is managed Postgres hosting**, not a distinct database technology.
- **"Supabase versus PGLite" is a deployment choice, not a database choice.** Cloud versus laptop, same engine either way.
- **Vector search needs three things**: an embedding model to produce vectors, pgvector to store and compare them, and an index (typically HNSW) to make comparison fast.

## Related

- [[openbrain-vs-agentic-os]] - the two systems that use this stack, compared
- [[agentic-os/memory-database-schema|Agentic OS Memory Database Schema]] - a concrete pgvector schema with HNSW indexes and scope constraints
- [[ai-memory-paradigms]] - why these systems are database-backed in the first place
