---
type: reference
created: 2026-07-29
tags: [technology, agentic-os, ai, memory, architecture, comparison]
---

# OpenBrain (OB1) vs Agentic OS Memory

> *Two database-backed AI memory systems compared: [OB1](https://github.com/NateBJones-Projects/OB1) by Nate B Jones, and the PGLite plus pgvector memory layer inside Agentic OS. Assessed against the framework in [[wiki-vs-openbrain|AI Memory Paradigms]].*

**Headline:** both are **query-time systems** in Jones's own taxonomy. Unlike a Karpathy-style wiki, both store faithfully on ingest and let the AI synthesise when asked. They are architectural cousins. The differences are about *what they are a memory of*, *how data arrives*, and *deployment posture*.

## Shared DNA

- **PostgreSQL plus pgvector** as the substrate in both cases (see [[postgres-pgvector]]).
- **Vector similarity search** as the retrieval primitive, HNSW indexing with cosine distance.
- **Query-time synthesis with the AI as reader**, not a write-time compiled wiki.
- **Own your data, self-hostable**, no mandatory SaaS in the middle.
- **Multi-tenant isolation and provenance** treated as first-class concerns.

## Where They Diverge

| Dimension | OB1 (OpenBrain) | Agentic OS memory |
|---|---|---|
| **What it is memory *of*** | **You**, across every AI tool. A shared brain bus | **The agent's own work.** Claude Code sessions plus project documents |
| **How data arrives** | **Human-curated, multi-source.** Import recipes for ChatGPT, Gmail, Obsidian, X, Instagram, Google Activity, plus Slack and Discord capture bots | **Agent-auto-captured, single-source.** A Stop hook fires at session end, Claude Haiku summarises the turn into `context/memory/{date}.aos.md`, the indexer embeds it |
| **Deployment posture** | **Cloud-first.** Supabase by default, Kubernetes to self-host | **Local-first.** PGLite (Postgres compiled to WebAssembly) as a single `data.db` file, zero external dependencies, Windows-native. Hosted Postgres optional |
| **Access protocol** | **MCP gateway.** Any client plugs in: Claude Desktop, ChatGPT, Claude Code, Cursor | **CLI plus Command Centre dashboard**, native to Claude Code (`npm run memory:recall`) |
| **Schema** | `thoughts` table plus extensible sidecars (provenance, review, use-policy, source-reference, relation, recall-trace, audit) | Five fixed tables: `memory_sources`, `memory_chunks`, `index_jobs`, `search_events`, `schema_migrations` |
| **Search** | Vector search | **Hybrid**: BGE-M3 vector search plus Postgres full-text keyword, reranked by authority weight and recency (14-day half-life, 0.7 floor), with a **three-rung recall ladder** |
| **Isolation model** | Composability and extensions. One user, many tools | **Scope columns** (`private`, `client`, `team`, `system`) with a database CHECK-constraint no-leak boundary. Built for agency multi-client work |
| **Product scope** | A standalone memory **platform** | Memory is **one layer of a wider agent OS**: SOUL.md identity, skills, and brand context |

## The Two Sharpest Distinctions

### 1. Multi-agent bus versus multi-client runtime

The tenancy axis differs, and it is the deepest design split.

- **OB1 is horizontal, across your tools.** One person's brain, many AIs reading and writing through MCP. Its slogan is "Claude, ChatGPT, Cursor, Claude Code, whatever ships next month. One brain. All of them."
- **Agentic OS is vertical, across your clients.** One operator, many isolated client workspaces under `clients/{slug}/`, with leakage prevented in both application code and a database constraint.

These solve different problems. OB1 assumes your risk is fragmentation between tools. Agentic OS assumes your risk is one client seeing another client's data.

### 2. Faithful store versus lossy pre-compile

This is where Jones's own framework bites his neighbour.

- **OB1 is pure OpenBrain.** It stores thoughts faithfully and defers *all* synthesis to query time.
- **Agentic OS performs a small write-time compile.** Haiku turns each session into a 2 to 10 bullet summary *before* it is embedded. What gets retrieved later is the summary, not the conversation.
- That makes Agentic OS a **light hybrid**: a lossy synthesis step at capture feeding a query-time vector store. It buys cheap, dense recall.
- It also walks directly into the editorial nuance-drop trap described in [[wiki-vs-openbrain|AI Memory Paradigms]]. The AI's framing of the session silently becomes the record.
- **Its mitigation is Karpathy's.** Raw transcripts are archived to `context/transcripts/{date}/` (gitignored, not indexed by default) and exposed through the third rung of the recall ladder when exact wording matters.

## The Three-Rung Recall Ladder

Agentic OS has no equivalent in OB1's documented design, and it is a direct answer to the lossy-summary problem. Stop at the lowest rung that answers the question:

| Rung | Command | Returns |
|---|---|---|
| 1. Search | `memory:recall -- "<query>"` | Hybrid vector plus keyword hits, reranked |
| 2. Expand | `memory:recall -- --expand <chunk-id>` | Surrounding source context, when the chunk is too short |
| 3. Transcript | `memory:recall -- --transcript <chunk-id>` | The raw conversation window behind the chunk |

Rung 3 is the escape hatch back to ground truth: the discipline Jones says most wiki adopters fail to maintain, made a single command instead of a habit.

## Positioning in Jones's Taxonomy

| System | Classification |
|---|---|
| **OB1** | Canonical OpenBrain. The structured, faithful, multi-tool store you would put *underneath* a compiled wiki view |
| **Agentic OS** | OpenBrain-shaped but agent-scoped and auto-fed, with a Haiku pre-compile. Closer to self-maintaining session memory than a deliberate knowledge base |
| **Neither** | Provides Karpathy's browsable, cross-referenced, contradiction-flagging artifact. Both would need a graph or compiler layer on top, which is exactly the plugin Jones built for OpenBrain |

## Choosing Between Them

| Choose OB1 when | Choose Agentic OS memory when |
|---|---|
| Multiple AI tools must share one memory | Claude Code is the primary agent |
| You want to import existing history (ChatGPT exports, Gmail, Obsidian, social) | Memory should accumulate automatically from work, with no curation effort |
| Capture should be deliberate and human-curated | You run isolated workspaces for multiple clients and need a hard leak boundary |
| Cloud-hosted and always-available suits you | Local-first, offline-capable, Windows-native matters |
| Memory is the whole product | Memory is one layer under agent identity, skills, and brand context |

## Key Takeaways

- **Both are query-time database systems**, not Karpathy wikis. They are cousins, not opposites.
- **Same substrate**: Postgres plus pgvector in both, differing only in where the Postgres runs.
- **OB1's tenancy axis is tools** (one brain, many AIs). **Agentic OS's is clients** (one operator, isolated workspaces).
- **OB1 stores faithfully; Agentic OS pre-compiles with Haiku** before embedding, making it a light hybrid that trades fidelity for cheap recall.
- **The archived raw transcript plus the third recall rung** is Agentic OS's answer to the lossy-summary risk, and it makes returning to ground truth a command rather than a discipline.
- **Neither gives you a browsable compiled artifact.** Both need a graph layer on top for that.

## Related

- [[wiki-vs-openbrain|AI Memory Paradigms]] - the write-time versus query-time framework
- [[agentic-os/memory-system-architecture|Memory System Architecture]] - the four layers in detail
- [[agentic-os/memory-database-schema|Memory Database Schema]] - tables, scope model, no-leak boundary
- [[agentic-os/session-capture-and-storage|Session Capture and Storage]] - how the Stop hook and transcript archive work
- [[postgres-pgvector]] - what Postgres, pgvector, PGLite, and Supabase each actually are
