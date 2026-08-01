---
type: reference
updated: 2026-07-31
authority: analysis-backed
concept: enabler
serves: capture
---

# Observation Layer

> *An enabler for the **Capture** pillar: a mechanism that records what happened during agent sessions into durable storage. It answers "is anything going unrecorded?" It is not a search technology. Model: [[memory-pillars]].*

> [!note] Status: technology theory, not an adopted design
> Reference material on how agent memory systems work. Where one real environment is assessed, it is a worked example to make the model testable.

## Key Takeaways

- **An observation layer captures. It does not retrieve.** Its only job is getting events into durable storage.
- **Never use "observation layer" and "semantic search" interchangeably.** Different pillars, different spend. See the terminology note below.
- **Assess capture before anything downstream.** Retrieval and injection projects cannot proceed over material that was never recorded, and they must not be priced as if capture were missing when it is not.
- **Verdict in the assessed environment: not required.** Claude Code already writes a complete JSONL event log per session. Capture was solved before any layer was proposed.
- **Three hypotheses that would have justified one were tested against a real corpus, and all three failed.**

---

## Terminology note: capture is not retrieval

| | **Observation layer** (this article) | **Semantic search** ([[memory-semantic-search]]) |
|---|---|---|
| Pillar served | **Capture** | **Recall**, and triggered Injection |
| Answers | "Is anything going unrecorded?" | "Can I find what I know is there?" |
| Fails when | Events vanish unlogged | You must know the exact string to grep |
| Output | A durable store | An index over a store |

**The error to watch for: a proposal that argues retrieval benefits in order to justify capture spend.** Phrases like "we would be able to recall past decisions" or "we could surface old error traces" are retrieval arguments. If capture already exists, they justify an index, not a new capture system. Score every claimed benefit onto a pillar before approving anything.

## What counts as an observation layer

Any mechanism whose purpose is to record session activity into durable storage: session transcripts, event logs, tool-call traces, behavioural summaries written at session close, or a live process that watches conversations and extracts patterns.

The defining test is that **it creates a record that did not previously exist**.

Capture is indiscriminate by nature. It does not judge importance; that judgement belongs to the Storage pillar, and specifically to its curated branch. See [[memory-pillars]].

## When an observation layer is justified

1. **Material is genuinely being lost.** Events occur that reach no durable store.
2. **The loss is consequential.** The lost material would change future decisions or behaviour.
3. **No existing store already holds it.** Native transcripts, application logs, or version control frequently already cover this.
4. **Capture cost is lower than reconstruction cost.** If the same insight can be derived retrospectively from existing files, capture is redundant.

## Assessment of one environment, 2026-07-31

**Verdict: not required.** Capture was already complete.

Claude Code writes a full JSONL event log per session to `~/.claude/projects/[project]/*.jsonl`. For the assessed vault this was 47 sessions and 24,581 events spanning 2026-05-18 to 2026-07-31, roughly 100MB.

| Signal | Already captured | Example recovered without instrumentation |
|---|---|---|
| Every user turn, timestamped | Yes | 1,422 clean user turns across 46 active days |
| Every tool call, name and input | Yes | Edit 1,432, Read 815, Bash 772, Write 234 |
| Files read and written, by path | Yes | Per-area effort distribution across the corpus |
| Session and compaction boundaries | Yes | 28 context compactions |
| Skill and command invocations | Yes | 19 skill invocations; `/model` 113 times |
| Turn pacing and interrupts | Yes | Median 3.5 tool calls per turn, p90 11, max 90 |

The analysis producing these numbers ran entirely from existing files in a single session with no prior instrumentation. A capture layer would have duplicated a store that already existed.

## Three hypotheses tested, three failed

Each would have justified a capture layer. None survived contact with the corpus.

**1. Procedural agreements are lost to context rot.**
Proposed mechanism: agreements made mid-session, not codified in an always-loaded rulebook, drift out of context and get ignored.

Tested against the strongest candidate case (a challenge of the form *"why are you doing X before Y, like we agreed?"*). The agreement was made at 15:38, restated by the assistant at 15:43, and challenged at 15:49. The first compaction in that session occurred roughly 19 hours later. The agreement was 11 minutes old and self-restated twice, so it was neither compacted away nor decayed. It was also not undocumented: the rule was written into a protocol doc created the following day. **The correction caused the doc.**

**2. Corrections cluster after compaction.**
Measured correction language in the 15 turns after each of the 28 compactions: 5.4% against a 2.4% baseline, apparently 2.27x. The signal is an artefact. Of the 13 matched turns roughly 11 are false positives, because post-compaction turns are disproportionately context-reloading turns where reported speech about third parties ("she said", "we agreed", "that was wrong") trips correction patterns. Stripped of those, the rate is indistinguishable from baseline.

**3. Compaction imposes a human re-narration tax.**
Proposed mechanism: after compaction the human must re-supply background, shifting cost rather than removing it. Measured: mean user turn length in the 10 turns following a compaction is 651 characters against a 1,001-turn baseline of 682, a ratio of **0.95x**. Post-compaction turns are marginally shorter, not longer. No tax exists.

**Limit of these findings.** All three tests detect *noticed* loss. Corrections require the human to spot that something was dropped; re-narration requires them to re-supply it. Silent loss would produce neither signal. The accurate claim is "no *detectable* harm in this corpus", not "compaction is harmless". Proving the stronger claim needs a designed experiment, not corpus analysis.

## What the capture store is genuinely good for

Capture without retrieval still delivers value, through **aggregate analysis**. These findings are invisible from inside any single session, and a curated knowledge base cannot hold them by construction, because it records what is true, not where effort went.

- **Effort inverted stated priority.** Stated order was Wellbeing, Relationships, Finance, Career, Performance, Personal. Actual edit volume: career 510 (33%), ai-os 379 (24%), relationships 155 (10%), projects 145 (9%), performance 143 (9%), finance 105 (6%), wellbeing 11 (0.7%), personal 6 (0.4%).
- **A quarter of all effort maintained the machine.** The AI-operating-layer folder was the second-largest area by edit volume despite not being a workstream.
- **Skills were built and not adopted.** 19 invocations across 47 sessions, with the entire planning and ceremony stack never invoked once.
- **There is a measurable interrupt threshold.** 11 hard "stop" interrupts, concentrated in the tail of long tool runs, including an explicit cost objection.
- **Model routing was decided 113 times without consulting existing doctrine**, which is a wiring problem rather than an authoring one.

**Implementation shape:** a periodic script over existing transcripts, output as a dated report. Not a runtime component.

## Relationship to the other pillars

**Hard dependency, one direction only.** Recall and Injection depend on capture; capture depends on nothing downstream. Aggregate audit value is delivered by scripted analysis with no index at all.

**Consequence for decision-making:** assess capture first. If it is missing, no retrieval project can proceed. If it is already solved, the only live question is whether retrieval and injection over it justify building anything.

**Synergy:** capture *quality* sets the retrieval *ceiling*. A store carrying timestamps, session ids and tool inputs lets a downstream index filter on metadata before ranking by similarity, which is substantially more precise than similarity alone.

**Trap:** building capture alongside an index when capture is already solved. That doubles the maintenance surface for zero added recall.

For what capture cannot fix, including compaction and context rot, see [[memory-pillars]].

## Caveats

- The assessed corpus begins 2026-05-18; earlier sessions may have rotated out of local storage.
- A separate 48-session project was excluded from the analysis.
- Skill counts capture tool-invocation and slash-command paths only, so they may undercount.
- Transcript retention is not guaranteed indefinitely. For long-horizon trend analysis, **retention** becomes the dependency to solve, not capture.

## Related

- [[memory-pillars]] - the four-pillar model; this enabler serves Capture
- [[memory-semantic-search]] - enabler for Recall and triggered Injection
- [[memory-curated-index]] - enabler for Recall, the manual approach
- [[wiki-vs-openbrain|AI Memory Paradigms]] - write-time versus query-time
