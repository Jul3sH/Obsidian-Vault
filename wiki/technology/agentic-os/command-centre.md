---
type: reference
updated: 2026-07-28
---

# Command Centre Dashboard

The web-based dashboard and CLI hub for Agentic OS. A Next.js application that provides a UI dashboard (`localhost:3000`) and CLI commands for memory management, task tracking, and system operations.

## What is Command Centre?

**Command Centre** is the operational heart of Agentic OS:
- Web dashboard at `http://localhost:3000` (task board, Kanban view, GSD project management)
- CLI runtime for all memory and data operations
- Memory store bootstrap and migrations
- Session import and transcription
- Next.js application built on Node.js

**Location:** `~/agentic-os/command-centre/`

## Launching Command Centre

**First run (with bootstrap):**
```bash
bash scripts/centre.sh                   # macOS/Linux
powershell -File scripts\centre.ps1      # Windows
```

**After first setup:**
```bash
centre                                   # shortcut (added to shell profile)
```

The `centre` command:
1. Reuses saved launcher state
2. Repairs missing bootstrap files silently
3. Starts the Next.js dev server
4. Opens `http://localhost:3000` in browser

## Dashboard Features

- **Task Board** — Create, assign, track tasks; mark status (backlog, in-progress, done)
- **Kanban View** — Visual workflow across states; drag-and-drop task management
- **GSD Project Management** — Structured project execution, phase planning, verification checkpoints
- **Dashboard** — Agentic OS health status, memory index status, recent sessions

## Memory CLI Commands

All commands run from `command-centre/`:

```bash
npm run memory:index                     # Index context/memory/
npm run memory:recall -- "<query>"       # Three-rung recall ladder
npm run memory:expand -- <chunk-id>      # Surrounding context
npm run memory:transcript -- <chunk-id>  # Raw conversation window
npm run memory:backup                    # Create .tar.gz backup
npm run memory:restore -- <file> --yes   # Restore from backup
npm run memory:import-sessions           # Import Claude Code history
npm run memory:reindex                   # Rebuild index from sources
npm run memory:status                    # Show memory store status
```

## Database Operations

All commands run against the local PGLite database (`.command-centre/data.db`) by default. If `MEMORY_DATABASE_URL` is set, they switch to hosted Postgres automatically.

**Bootstrap (first setup):**
```bash
npm run memory:bootstrap                 # Creates data.db, applies migrations
npm run memory:status                    # Verify bootstrap succeeded
```

## Storage

**Local PGLite database:**
- File: `.command-centre/data.db`
- Size: ~4 KB (schema only) → grows as you add memory
- Typical: 25-30 MB (6 months light use) → 1-2 GB (2 years moderate use)

## Related Documentation

- [[agentic-os/memory-system-architecture|Memory System Architecture]] — indexing, search, capture
- [[agentic-os/memory-database-schema|Memory Database Schema]] — tables, indexes, scope model
- [[agentic-os/session-capture-and-storage|Session Capture and Storage]] — transcript handling
