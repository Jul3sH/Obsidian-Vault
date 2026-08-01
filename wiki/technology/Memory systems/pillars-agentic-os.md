---
type: reference
updated: 2026-08-01
concept: product-evaluation
product: Agentic OS
---

# Agentic OS, Scored Against the Four Pillars

> *How the Agentic OS memory layer scores on **Capture, Storage, Injection, Recall**. Scoring only. For how it is built (layers, schema, scope model), see [[agentic-os/memory-system-architecture|Memory System Architecture]] and [[agentic-os/memory-database-schema|Memory Database Schema]]. Model: [[memory-pillars]].*

> [!note] Status: reference, not an adopted design
> An assessment of someone else's product against the four-pillar model. Nothing here is running in this vault.

> [!warning] Corrected 2026-08-01 against source
> The first version of this file was written from the wiki architecture doc alone and got Injection wrong (claimed none exists) and Capture wrong (claimed boundary, not continuous). Corrected against `/Users/julianhart/agentic-os` source: `.claude/settings.json`, the `memory-*.js` hooks, and `cron/jobs/*memory*.md`. See [[feedback-verify-before-writing]].

## Key Takeaways

- **Has scheduled injection, not none.** `load-memory-snapshot.js` fires on `SessionStart` and injects `SOUL.md`, `USER.md`, `MEMORY.md`, and the day's log as `additionalContext`. The gap is narrower than first assessed: it has scheduled injection like Hermes, but **no triggered injection** - nothing wired to `UserPromptSubmit` reads memory.
- **Capture is continuous, not boundary.** The `Stop` hook fires at the end of every agent turn in Claude Code, and `memory-capture.js`'s own comment confirms it captures "the transcript's **last turn**" each time, not a session-level summary.
- **A cron layer exists beyond the four documented layers**: `daily-memory-distill`, `nightly-memory-index`, `nightly-memory-backup`, `weekly-memory-curator`, `weekly-memory-gaps`. None of this appears in [[agentic-os/memory-system-architecture|the architecture doc]].
- **Best-in-class scope isolation:** `private` / `client` / `team` / `system` enforced in both application code and the database, with no-leak tests.
- **"Built but never ingested" now has direct corroboration**, not just the ClaudeClaw doc's claim. `context/MEMORY.md` in the actual repo is empty template scaffolding - the Active Threads, Environment Notes, and Pending Decisions sections are all unpopulated.
- **Revised finding:** this is no longer the clean "best Storage/Recall, zero Injection" case it first appeared to be. It has injection - just the weaker, scheduled kind. The sharper contrast with ClaudeClaw is specifically *triggered* injection, which only ClaudeClaw has.

---

## Scorecard

| Pillar | Sub-type | Agentic OS |
|---|---|---|
| **Capture** | Continuous / boundary | **Continuous** - `Stop` hook fires every turn; `memory-capture.js` captures "the transcript's last turn" each time |
| **Storage** | Kind of claim | **Undifferentiated**, but **scope-partitioned** (`private`/`client`/`team`/`system`) |
| **Storage** | Form | **Synthesised, with an unindexed raw archive** - summaries are indexed; raw transcripts are archived, gitignored, "not indexed by default" |
| **Storage** | Retention | **Comprehensive for summaries**; raw kept but outside the searchable set |
| **Injection** | Scheduled / triggered | **Scheduled only.** `load-memory-snapshot.js` on `SessionStart`; nothing on `UserPromptSubmit` |
| **Recall** | Write-time / query-time | **Query-time**, the most developed here: hybrid BGE-M3 vector plus Postgres full-text, three-rung ladder |

## Capture

Fires on every `Stop` event - which in Claude Code is the end of each agent turn, not session end. `memory-capture.js`'s own comment is unambiguous: *"On every Stop it spawns memory-capture.cjs detached: that captures **the transcript's last turn** as a summarized block... archives the raw transcript, and runs a debounced incremental index into the local PGLite memory store."*

Two further `SessionStart` hooks support capture rather than performing it:
- `memory-bootstrap-index.js` - on a freshly cloned workspace, backfills the empty local PGLite store once from on-disk memory, so recall works from the first session rather than staying dark until the nightly cron catches up.
- `memory-watch-start.js` - starts a live file-watcher so memory edited outside a Claude session becomes searchable without waiting for the next capture.

**A cron layer extends capture and maintenance beyond the hooks**, found in `cron/jobs/` and absent from the architecture doc: `nightly-memory-index`, `nightly-memory-backup`, `daily-memory-distill`, `weekly-memory-curator`, `weekly-memory-gaps`.

**The raw archive is not part of the memory system in practice.** It is gitignored and "not indexed by default", so unlike ClaudeClaw's `conversation_log` it cannot be queried. The verbatim layer exists as backup, not as a retrieval tier.

## Storage

PGLite locally, or hosted Postgres, both with pgvector. Five core tables (`memory_sources`, `memory_chunks`, `index_jobs`, and others - see [[agentic-os/memory-database-schema|the schema doc]]).

**The distinguishing feature is the scope model.** Every row carries a scope of `private`, `client`, `team`, or `system`, and every search filters on it. The invariant is enforced in application code *and* in the database, with no-leak tests against seeded data. The doc names the single remaining vulnerability honestly: raw SQL that omits the scope predicate, which is a code-review rule rather than a code-enforceable one.

That is a genuine capability nothing else assessed has, and it is why this exists at all: it replaced MemSearch specifically for Windows robustness, infrastructure weight, and **scope isolation** (MemSearch has "no concept of scope; everything indexed into one global space").

Storage cost is modest: roughly 5-6 KB per chunk, so ~25-30 MB for six months of light use.

## Injection

**Scheduled, not absent - and this reverses the first version of this file.** `load-memory-snapshot.js` fires on `SessionStart` and reads `context/SOUL.md`, `context/USER.md`, `context/MEMORY.md`, and today's (or yesterday's, as fallback) daily log, then injects them as `additionalContext` - the runtime's own comment says this is so Claude has them "available at session start without needing the user to prompt". This is precisely Simon's frozen-snapshot Injection pillar.

`MEMORY.md` is explicitly labelled a **frozen snapshot** in its own header comment: *"mid-session writes only take effect next session"* - confirming scheduled, not triggered, by the system's own design intent, capped at 2,500 characters.

**What is genuinely missing is triggered injection.** Nothing is wired to `UserPromptSubmit` that reads memory; that event fires only a notification hook and a session-sync hook. So per the trigger hierarchy in [[memory-pillars]], mid-session recall still depends on option 1 (the human asks) or option 2 (the agent decides to invoke the CLI) - the two unreliable rungs. Only ClaudeClaw's `buildMemoryContext`, wired to run on every turn, reaches trigger option 3.

**The "built but never ingested" claim now has independent corroboration.** [[claudeclaw-memory-system]] states it; direct inspection of the repo adds to it - `context/MEMORY.md` in this workspace is the unpopulated template (Active Threads, Environment Notes, Pending Decisions all empty), not a working scratchpad with real content. Sophisticated scheduled-injection infrastructure exists and appears unused in practice, even though it is more complete than the first assessment credited it for.

## Recall

The most developed of any system assessed. A **three-rung ladder**, designed to stop at the lowest rung that answers the question:

1. **Search** - hybrid BGE-M3 vector search plus Postgres full-text keyword search
2. **Expand** - surrounding source context around a chunk, if the result is too short
3. **Transcript** - the raw conversation window behind a chunk, if exact wording is needed

BGE-M3 at 1024 dimensions, L2-normalised for cosine distance, chosen for multilingual strength.

The escalation design is sound: it is the same instinct as MemSearch's tiered retrieval, spending tokens only when a cheaper rung fails.

## What it would and would not solve here

| | |
|---|---|
| **Would add** | Query-time Recall, the strongest implementation assessed. Scheduled Injection, of the kind this environment currently lacks entirely (`user.md` here is fetched by instruction, not injected by a hook - see [[memory-model-adoption]]). Scope isolation, though this environment is single-user so that is unused capability |
| **Would duplicate** | Capture, already covered by native JSONL |
| **Would partially solve** | **Injection - the scheduled half only.** Mid-session triggered recall, the sharper gap measured in [[memory-curated-index]] (11% invocation, 25% autonomous discovery), would still be unaddressed |
| **Cautionary** | Its own track record. More complete infrastructure than first credited, and still recorded as unused in practice |

## Related

- [[agentic-os/memory-system-architecture|Memory System Architecture]] - how it is built: the four layers, PGLite, BGE-M3
- [[agentic-os/memory-database-schema|Memory Database Schema]] - tables, indexes, canonical query
- [[memory-pillars]] - the model being applied
- [[pillars-claudeclaw]] - the contrast: weaker storage, triggered injection, actually in use
- [[memory-claudeclaw-vs-agentic-os]] - the existing head-to-head comparison
