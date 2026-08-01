---
type: reference
updated: 2026-08-01
authority: analysis-backed
concept: pillar
pillar: capture
---

# Capture

> *The first pillar of [[memory-pillars|the four-pillar model]]: getting events into a durable record. The capability this pillar enables, once implemented, is called an **Observation Layer** - the ability to look back at what happened, session by session, without gaps. Observation is the outcome of Capture, not a separate technology that produces it.*

> [!note] Status: technology theory, not an adopted design
> Reference material on how agent memory systems work. Where one real environment is assessed, it is a worked example to make the model testable.

## Key Takeaways

- **Capture captures. It does not retrieve.** Its only job is getting events into durable storage before anything is judged, filed, or searched.
- **The capability it enables is called Observation.** A system with working Capture has an Observation Layer: the standing ability to answer "what happened?" for any past session. Observation is not a rival implementation to native transcripts or summarising hooks - it is what having any of them gives you.
- **Never use "Capture" and "Recall" interchangeably**, and never argue for capture spend using a retrieval benefit. See the terminology note below.
- **Three modes, not two: continuous, periodic, boundary.** Plus a separate firing condition, event-triggered, which can layer onto any of the three.
- **Assess capture before anything downstream.** Retrieval and injection cannot proceed over material that was never recorded, and must not be priced as if capture were missing when it is not.
- **Verdict in the assessed environment: not required.** Claude Code already writes a complete JSONL event log per session. Capture, and the Observation capability it produces, existed before any layer was proposed.

---

## Terminology note: Capture is not Recall

| | **Capture** (this article) | **Recall** ([[memory-recall]]) |
|---|---|---|
| Answers | "Is anything going unrecorded?" | "Can I find what I know is there?" |
| Fails when | Events vanish unlogged | You must already know where or how to look |
| Output | A durable store, and the Observation capability that comes with it | An index over a store |

**The error to watch for: a proposal that argues retrieval benefits in order to justify capture spend.** Phrases like "we would be able to recall past decisions" or "we could surface old error traces" are Recall arguments. If capture already exists, they justify an index, not a new capture system. Score every claimed benefit onto its pillar before approving anything.

## What counts as Capture

Any mechanism whose purpose is to record session activity into durable storage: session transcripts, event logs, tool-call traces, behavioural summaries written at a boundary, or a live process that watches conversations and extracts patterns.

The defining test is that **it creates a record that did not previously exist**.

Capture is indiscriminate by nature. It does not judge importance; that judgement belongs to the Storage pillar, and specifically to its curated branch. See [[memory-pillars]].

**The capability, restated:** once any of the above exists, the system has an Observation Layer - it can answer questions about its own past that it could not answer before. Observation is a property of the *outcome*, not a name for one implementation over another.

## When Capture is justified

1. **Material is genuinely being lost.** Events occur that reach no durable store.
2. **The loss is consequential.** The lost material would change future decisions or behaviour.
3. **No existing store already holds it.** Native transcripts, application logs, or version control frequently already cover this.
4. **Capture cost is lower than reconstruction cost.** If the same insight can be derived retrospectively from existing files, capture is redundant.

## Three modes, and a separate firing condition

Capture divides on **granularity**: how often it fires.

| | **Continuous** | **Periodic** | **Boundary** |
|---|---|---|---|
| Fires | Every turn | Every N turns (a fixed interval) | At session end, or another boundary |
| Completeness | Total, verbatim | Total at each checkpoint; nothing since the last one is captured until the next fires | Lossy; usually a summary |
| Cost | Per-turn runtime cost | One cost per interval | One cost per session |
| Risk | Volume; store grows fast | **A gap between checkpoints**: anything since the last one is uncaptured until the next fires | Loses detail the summariser dropped |
| Verified example | Native Claude Code transcripts; ClaudeClaw, agentic-os, MemSearch capture hooks | MemPalace, default every 15 exchanges | Hook-based session-end summarisers generally |

**Periodic is the missing middle case** most models skip: it trades completeness for lower cost than continuous capture, without going as coarse as boundary capture, at the price of a genuine gap between checkpoints.

**A separate question from granularity is *what triggers a firing*: a schedule, or an event.** Event-triggered capture fires in response to something about to happen that would otherwise cause loss, rather than on a fixed cadence. Verified example: MemPalace's `PreCompact` hook, which fires unconditionally, synchronously, immediately before every compaction event, and flushes the transcript into durable storage first. This is not a fourth granularity - it is a firing condition that can be layered onto any of the three modes above, and it is **the only verified structural fix for compaction-caused data loss**. Full analysis: [[memory-pillars]], "Compaction and context rot".

## Capabilities and features across systems

Transposed from the four product scorecards. Everything below is Capture-pillar behaviour, organised by capability rather than by product.

| Capability | Systems | Detail |
|---|---|---|
| **Continuous capture** | ClaudeClaw, agentic-os, MemSearch, native Claude Code transcripts | `Stop` fires per turn in Claude Code; each system's hook captures the last turn on every fire |
| **Periodic capture** | MemPalace | Checkpoints every 15 exchanges (`SAVE_INTERVAL = 15`) via `Stop`, not per-turn |
| **Event-triggered capture (compaction-safe)** | MemPalace | `PreCompact` hook, unconditional, synchronous, always runs regardless of the periodic interval |
| **Importance gating at ingest** | ClaudeClaw | Extraction LLM scores each turn; hard filter discards anything below importance 0.5 |
| **Cheap pre-filter before the extraction model runs at all** | ClaudeClaw | Messages under 15 characters or starting with `/` never reach the LLM |
| **Semantic duplicate detection at ingest** | ClaudeClaw | Cosine similarity > 0.85 against existing memories skips saving, a second curation pass beyond the importance filter |
| **Comprehensive retention (no importance gate)** | MemSearch, MemPalace (default) | Every non-trivial turn is captured; only empty or near-empty transcripts are skipped |
| **Agent-authored capture** (the agent itself decides and writes what to record, via tool calls, rather than an external summariser) | MemPalace (legacy, opt-in mode only) | `Stop` blocks the event and instructs the agent to call memory-write tools itself before finishing, instead of a script summarising on its behalf |
| **Externally-summarised capture** (the default and most common pattern) | ClaudeClaw, agentic-os, MemSearch, MemPalace (default silent mode) | An LLM (often Haiku, cheaper than the main model) or a script summarises the turn; the acting agent is not involved |
| **Verbatim retention alongside a synthesised layer** | ClaudeClaw (`conversation_log`), MemSearch (raw dialogue as last-resort retrieval tier), agentic-os (gitignored, unindexed raw archive) | All three keep a raw layer distinct from the searchable synthesised layer, at different levels of accessibility |
| **Loop-guard against recursive capture** | MemSearch, ClaudeClaw | `stop_hook_active` (or equivalent) checked so a Stop-triggered save cannot itself trigger another save |
| **Content-hash deduplication before indexing** | MemSearch (SHA-256), agentic-os (SHA-256) | Skips re-indexing unchanged content on repeated runs |
| **Resilience: provider fallback plus quota backoff** | ClaudeClaw | Primary extraction via the selected agent provider, Gemini as fallback; a 5-minute cooldown on `429` errors prevents repeated failed calls from flooding logs |
| **Maintenance capture outside the hook chain** | agentic-os | A cron layer (`nightly-memory-index`, `nightly-memory-backup`, `daily-memory-distill`, `weekly-memory-curator`, `weekly-memory-gaps`) runs independently of any session hook, so it continues across headless or scheduled runs |
| **First-run backfill** | agentic-os | `memory-bootstrap-index.js` populates an empty local store once on a fresh clone, so recall works from session one rather than staying dark until the next scheduled index |

## Assessment of one environment, 2026-07-31

**Verdict: not required.** Capture, and the Observation capability it produces, was already complete.

Claude Code writes a full JSONL event log per session to `~/.claude/projects/[project]/*.jsonl`. For the assessed vault this was 47 sessions and 24,581 events spanning 2026-05-18 to 2026-07-31, roughly 100MB.

| Signal | Already captured | Example recovered without instrumentation |
|---|---|---|
| Every user turn, timestamped | Yes | 1,422 clean user turns across 46 active days |
| Every tool call, name and input | Yes | Edit 1,432, Read 815, Bash 772, Write 234 |
| Files read and written, by path | Yes | Per-area effort distribution across the corpus |
| Session and compaction boundaries | Yes | 28 context compactions |
| Skill and command invocations | Yes | 19 skill invocations; `/model` 113 times |
| Turn pacing and interrupts | Yes | Median 3.5 tool calls per turn, p90 11, max 90 |

The analysis producing these numbers ran entirely from existing files in a single session with no prior instrumentation - the Observation capability was already there, unused. A dedicated capture layer would have duplicated a store that already existed.

## Three hypotheses tested, three failed

Each would have justified building a dedicated capture layer. None survived contact with the corpus.

**1. Procedural agreements are lost to context rot.**
Proposed mechanism: agreements made mid-session, not codified in an always-loaded rulebook, drift out of context and get ignored.

Tested against the strongest candidate case (a challenge of the form *"why are you doing X before Y, like we agreed?"*). The agreement was made at 15:38, restated by the assistant at 15:43, and challenged at 15:49. The first compaction in that session occurred roughly 19 hours later. The agreement was 11 minutes old and self-restated twice, so it was neither compacted away nor decayed. It was also not undocumented: the rule was written into a protocol doc created the following day. **The correction caused the doc.**

**2. Corrections cluster after compaction.**
Measured correction language in the 15 turns after each of the 28 compactions: 5.4% against a 2.4% baseline, apparently 2.27x. The signal is an artefact. Of the 13 matched turns roughly 11 are false positives, because post-compaction turns are disproportionately context-reloading turns where reported speech about third parties ("she said", "we agreed", "that was wrong") trips correction patterns. Stripped of those, the rate is indistinguishable from baseline.

**3. Compaction imposes a human re-narration tax.**
Proposed mechanism: after compaction the human must re-supply background, shifting cost rather than removing it. Measured: mean user turn length in the 10 turns following a compaction is 651 characters against a 1,001-turn baseline of 682, a ratio of **0.95x**. Post-compaction turns are marginally shorter, not longer. No tax exists.

**Limit of these findings.** All three tests detect *noticed* loss. Corrections require the human to spot that something was dropped; re-narration requires them to re-supply it. Silent loss would produce neither signal. The accurate claim is "no *detectable* harm in this corpus", not "compaction is harmless". Proving the stronger claim needs a designed experiment, not corpus analysis.

## What the capture store is genuinely good for

Capture without retrieval still delivers value, through **aggregate analysis** - a use of the Observation capability that requires no index at all. These findings are invisible from inside any single session, and a curated knowledge base cannot hold them by construction, because it records what is true, not where effort went.

- **Effort inverted stated priority.** Stated order was Wellbeing, Relationships, Finance, Career, Performance, Personal. Actual edit volume: career 510 (33%), ai-os 379 (24%), relationships 155 (10%), projects 145 (9%), performance 143 (9%), finance 105 (6%), wellbeing 11 (0.7%), personal 6 (0.4%).
- **A quarter of all effort maintained the machine.** The AI-operating-layer folder was the second-largest area by edit volume despite not being a workstream.
- **Skills were built and not adopted.** 19 invocations across 47 sessions, with the entire planning and ceremony stack never invoked once.
- **There is a measurable interrupt threshold.** 11 hard "stop" interrupts, concentrated in the tail of long tool runs, including an explicit cost objection.
- **Model routing was decided 113 times without consulting existing doctrine**, which is a wiring problem rather than an authoring one.

**Implementation shape:** a periodic script over existing transcripts, output as a dated report. Not a runtime component.

## Relationship to the other pillars

**Hard dependency, one direction only.** Recall and Injection depend on Capture; Capture depends on nothing downstream. Aggregate audit value is delivered by scripted analysis with no index at all.

**Consequence for decision-making:** assess Capture first. If it is missing, no Recall or Injection project can proceed. If it is already solved, the only live question is whether Recall and Injection over it justify building anything.

**Synergy:** Capture *quality* sets the Recall *ceiling*. A store carrying timestamps, session ids and tool inputs lets a downstream index filter on metadata before ranking by similarity, which is substantially more precise than similarity alone.

**Trap:** building a dedicated capture mechanism alongside an index when Capture is already solved. That doubles the maintenance surface for zero added recall.

For what Capture cannot fix on its own, including compaction and context rot, see [[memory-pillars]].

## Caveats

- The assessed corpus begins 2026-05-18; earlier sessions may have rotated out of local storage.
- A separate 48-session project was excluded from the analysis.
- Skill counts capture tool-invocation and slash-command paths only, so they may undercount.
- Transcript retention is not guaranteed indefinitely. For long-horizon trend analysis, **retention** becomes the dependency to solve, not capture.

## Related

- [[memory-pillars]] - the four-pillar model overview; the compaction/context-rot analysis that spans Capture and Injection together lives there
- [[memory-storage]] - what Capture feeds into
- [[memory-recall]] - not to be confused with Capture; finds material already captured
- [[memory-injection]] - decides whether captured material reaches context
- [[pillars-claudeclaw]] - [[pillars-agentic-os]] - [[pillars-memsearch]] - [[pillars-mempalace]] - the four product scorecards this capability catalogue is transposed from
- [[wiki-vs-openbrain|AI Memory Paradigms]] - write-time versus query-time
