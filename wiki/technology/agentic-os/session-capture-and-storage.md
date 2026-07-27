---
type: reference
updated: 2026-07-28
---

# Session Capture and Storage

How Agentic OS automatically captures, summarizes, and stores session transcripts; disk space implications; and how it differs from Claude's built-in JSONL transcripts.

## Session Capture Flow

Runs automatically at every session end (Stop hook):

```
Session ends
  ↓
[Stop hook] fire-and-forget
  → Start memory-capture.cjs in detached process (non-blocking)
  ↓
[Extract] last user→assistant turn, remove tool-result noise
  ↓
[Summarize] via Claude Haiku (2-10 third-person bullets, 120s timeout)
  ↓
[Append] to context/memory/{YYYY-MM-DD}.aos.md
  ↓
[Archive raw transcript] to context/transcripts/{YYYY-MM-DD}/
  ↓
[Dedup check] SHA-256 hash of source turn (replay is a no-op)
```

**Fire-and-forget design:** The Stop hook returns immediately, never blocking the agent turn.

## Storage Locations

### Indexed Machine-Owned Summaries

**Path:** `context/memory/{YYYY-MM-DD}.aos.md`

Daily file containing session summaries, one block per turn. Machine-generated and machine-owned. Each block is 2-10 bullets in third-person voice.

**Tracked in git:** Yes. Version-controlled so memory can be rebuilt later with a new model or embedding pipeline.

**Indexed by:** Yes. The indexer includes `context/memory/` by default; these summaries are searchable.

### Raw Transcript Archives

**Path:** `context/transcripts/{YYYY-MM-DD}/`

Raw, complete conversation turns from the session. Not summarized — the full transcript window behind a summary block or a chunk. Used by the "transcript" rung of the recall ladder.

**Tracked in git:** No. Gitignored because large and only used when drilling into a specific transcript via `npm run memory:recall --transcript`

**Indexed by:** No. Raw transcripts are not indexed by default (too noisy).

## Duplicate Transcript Capture: Claude vs Agentic OS

Both systems capture the same turn data, but for different reasons:

| System | Storage | Format | Purpose |
|--------|---------|--------|---------|
| **Claude Code (harness)** | `~/.claude/projects/...` | JSONL | Built-in session logging by Claude |
| **Agentic OS Memory** | `context/transcripts/` | Raw markdown | Local archive for semantic indexing + recall |

**Is this wasteful?** Slightly, but by design. They serve different purposes and the transcripts are text (highly compressible). `context/transcripts/` can be safely pruned if disk space becomes an issue — recall continues to work, just loses the "transcript" rung of the ladder.

## Storage Calculation

### Per-Turn Storage

| Item | Size |
|------|------|
| Raw transcript | 5-15 KB |
| Haiku summary (2-10 bullets) | 0.5-2 KB |
| Indexed chunks + embeddings | 5-6 KB per chunk |
| **Total per turn** | **20-35 KB** |

### Scaling Examples

| Usage Pattern | Turns/Year | Storage | Laptop Impact |
|---------------|-----------|---------|---------------|
| Light (1-2 sessions/week) | ~5,000 | 100-175 MB | Negligible |
| Moderate (daily sessions) | ~50,000 | 1-1.75 GB | Minor (<2%) |
| Heavy (multiple daily) | ~200,000 | 4-7 GB | Manageable |
| 5 years heavy | ~1,000,000 | 20-35 GB | <5% of modern SSD |

### Backup Sizes (Compressed)

- 6 months light use: 10-20 MB
- 2 years moderate use: 50-100 MB
- 5 years heavy use: 200-300 MB

## Configuration

Edit `context/memory-config.json`:

```json
{
  "capture": {
    "summarize": {
      "provider": "claude",
      "model": "claude-3-5-haiku-20241022",
      "timeout_ms": 120000
    }
  }
}
```

**If summarization fails or times out:** Capture writes a bounded fallback summary instead of dropping the turn.

## Deduplication

Each summary block is keyed by SHA-256 hash of the source turn. Re-running the Stop hook with the same turn is a no-op — never appended twice.

## Pruning Transcripts

If disk space becomes an issue:

```bash
rm -rf context/transcripts/*          # safe; loses the "transcript" rung
npm run memory:backup                 # backup first
```

Recall still works; you just can't drill into full-turn context for old searches.

## GitHub Backups

`.aos.md` summaries are tracked in private GitHub backup so memory can be re-indexed if the model changes. Raw transcripts stay local (not pushed).

## Related Documentation

- [[agentic-os/memory-system-architecture|Memory System Architecture]] — capture flow within the system
- [[agentic-os/memory-database-schema|Memory Database Schema]] — tables and scope model
