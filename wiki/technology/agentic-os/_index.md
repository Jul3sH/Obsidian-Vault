---
type: index
updated: 2026-07-28
---

# Agentic OS

> *Turn Claude Code into your Agentic Operating System.*

Agentic OS gives Claude Code personality, memory, and skills so it works like a team member, not a chatbot. It remembers your brand voice, learns your preferences over time, and runs proven methodologies instead of winging it every session.

## Architecture Overview

Agentic OS is built on three interdependent layers:

1. **[[agentic-os/three-layer-architecture|Three-Layer Architecture]]** — Agent Identity (SOUL.md, USER.md, memory), Skills (modular, self-improving capabilities), Brand Context (voice, positioning, ICP, visual identity)
2. **[[agentic-os/memory-system-architecture|Memory System Architecture]]** — Session capture, indexing pipeline, database, search & recall (four interconnected layers)
3. **[[agentic-os/multi-client-architecture|Multi-Client Architecture]]** — Run multiple isolated clients from one install, with full scope isolation per client/team/user

## Core Documentation

### Identity & Personality
- **[[agentic-os/three-layer-architecture|Three-Layer Architecture]]** — SOUL.md (who you are), USER.md (who you're helping), skills, brand context

### Semantic Memory System

The memory system consists of four layers:

1. **[[agentic-os/session-capture-and-storage|Session Capture and Storage]]** — Auto-capture at session end, stored as .aos.md summaries (git-tracked) and raw transcripts (archived locally)
2. **[[agentic-os/memory-system-architecture|Memory System Architecture]]** — Indexing pipeline (discover → chunk → embed), PGLite + pgvector database, hybrid search (vector + keyword), three-rung recall ladder
3. **[[agentic-os/memory-database-schema|Memory Database Schema]]** — Five tables (sources, chunks, index_jobs, search_events, schema_migrations), scope model (private/client/team/system), indexes, no-leak guarantees
4. **[[agentic-os/command-centre-dashboard|Command Centre Dashboard]]** — Web UI and CLI hub for all operations (indexing, search, recall, backup, restore)

### Multi-Client & Isolation

- **[[agentic-os/multi-client-architecture|Multi-Client Architecture]]** — Run multiple isolated clients (`clients/{slug}/`), per-client brand context and memory, scope isolation prevents cross-client leakage

### Comparisons

- **[[openbrain-vs-agentic-os|OpenBrain (OB1) vs Agentic OS Memory]]** - Both are query-time database systems on Postgres plus pgvector. Differences in tenancy axis (multi-tool versus multi-client), capture model (human-curated versus auto-captured with Haiku pre-compile), and deployment posture.
- **[[wiki-vs-openbrain|AI Memory Paradigms: Write-Time vs Query-Time]]** - The framework these comparisons use: when the AI does the hard thinking, at ingest or at query.
- **[[postgres-pgvector|Postgres, pgvector, PGLite and Supabase]]** - What the storage stack terms mean; only Postgres is a database engine.

## Key Facts at a Glance

| Component | Details |
|-----------|---------|
| **Memory backend** | PGLite locally (default) or hosted Postgres |
| **Embedding model** | BGE-M3, 1024-dimensional, L2-normalized |
| **Search type** | Hybrid (vector + full-text keyword), reranked by authority + recency |
| **Storage per chunk** | ~5-6 KB (vector + metadata) |
| **Typical disk usage** | 6 months light use ≈ 25-30 MB; 2 years moderate ≈ 1-2 GB; negligible laptop impact |
| **Scope isolation** | Private (user), client (folder), team (hosted), system (baseline) with enforced no-leak boundary |
| **Update behavior** | Preserves client data, syncs shared skills/hooks, auto-merges changes with manual conflict resolution |
| **Skills** | Core (always installed) + optional (add/remove as needed); self-improving with feedback |
| **Brand context** | Voice, positioning, ICP, visual identity auto-loaded by skills to keep output on-brand |

## Quick Reference

### Memory CLI Commands

```bash
# Index context/memory/ and learnings.md
npm run memory:index -- --visibility system

# Three-rung recall (search → expand → transcript)
npm run memory:recall -- "<query>" --system --json

# Back up and restore
npm run memory:backup
npm run memory:restore -- <file> --yes

# Import Claude Code sessions
npm run memory:import-sessions

# Check status
npm run memory:status
```

### Scope Flags

```bash
--system              # root baseline memory
--client <slug>       # clients/{slug}/ memory (isolated per client)
--team <id>          # team-scoped (hosted multi-team deployments)
--user <id>          # user-scoped (hosted multi-user)
```

## Storage Calculation

| Usage Pattern | Turns/Year | Raw Storage | Laptop Impact |
|---------------|-----------|-------------|---------------|
| Light (1-2 sessions/week) | ~5,000 | 100-175 MB | Negligible |
| Moderate (daily sessions) | ~50,000 | 1-1.75 GB | Minor (<2%) |
| Heavy (multiple daily) | ~200,000 | 4-7 GB | Manageable |
| 5 years heavy use | ~1,000,000 | 20-35 GB | <5% of modern SSD |

**Backup sizes (compressed):**
- 6 months light: 10-20 MB
- 2 years moderate: 50-100 MB
- 5 years heavy: 200-300 MB

## Installation & Launch

**First run:**
```bash
git clone https://<TOKEN>@github.com/simonc602/agentic-os.git
cd agentic-os
bash scripts/centre.sh              # macOS/Linux
# OR
powershell -File scripts\centre.ps1 # Windows
```

**After setup:**
```bash
centre                              # shortcut
```

## Operating Principles (from SOUL.md)

- Be genuinely helpful (no filler)
- Have opinions (recommend with reasoning)
- Be resourceful (check context first)
- Anticipate needs (think owner, not employee)
- Own mistakes (don't hedge)
- Work across domains (not limited to one skill)

## Related Documentation

- **[[technology/claude-anthropic/_index|Claude & Anthropic]]** — Claude Code platform documentation
- **[[technology/claudeclaw-business-os/_index|ClaudeClaw Business OS]]** — Telegram bridge to Claude Code
- **[[ai-os/_index|AI OS]]** — System design, operational layer, skills infrastructure (your specific Claude instance setup)

## Filing Convention

Agentic OS documentation lives here in `wiki/technology/` because it is **generic tool documentation** useful to anyone running Agentic OS.

Operational specifics (your personal Claude setup, hooks, memory configuration) live in `wiki/ai-os/` instead.
