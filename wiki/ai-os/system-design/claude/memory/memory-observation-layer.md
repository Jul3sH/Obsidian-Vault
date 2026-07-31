---
type: doctrine
updated: 2026-07-31
authority: analysis-backed
concept: capture
---

# Observation Layer

> *An observation layer is a **capture** mechanism: it records what happened during agent sessions. It answers "is anything going unrecorded?" It is not a search technology. Paired concept: [[memory-semantic-search]].*

## Key Takeaways

- **An observation layer captures. It does not retrieve.** Its job is to ensure events reach durable storage, nothing more.
- **Never use "observation layer" and "semantic search" interchangeably.** They sit on different axes and justify different spend. See the terminology note below.
- **Verdict for this environment: not required.** Claude Code already writes a complete JSONL event log per session. Capture is solved before any layer is built.
- **Three hypotheses that would have justified one were tested against the corpus and all three failed.**
- **Capture is upstream of retrieval.** You cannot search what was never recorded, so capture is assessed first, always.

---

## Terminology note: do not use these terms interchangeably

This is the single most common category error in agentic OS design, and it is expensive.

| | **Observation layer** (this article) | **Semantic search** ([[memory-semantic-search]]) |
|---|---|---|
| Axis | **Capture** | **Retrieval** |
| Answers | "Is anything going unrecorded?" | "Can I find what I know is there?" |
| Fails when | Events vanish unlogged | You must know the exact string to grep |
| Output | A durable store | An index over a store |

The error to watch for: **a proposal that argues retrieval benefits in order to justify capture spend.** Phrases like "we would be able to recall past decisions" or "we could surface old error traces" are retrieval arguments. If capture already exists, they justify an index, not a new capture system. Ask which axis every claimed benefit sits on before approving anything.

## What counts as an observation layer

Any mechanism whose purpose is to record session activity into durable storage: session transcripts, event logs, tool-call traces, behavioural summaries written at session close, or a live process that watches conversations and extracts patterns.

The defining test is that **it creates a record that did not previously exist**.

## When an observation layer is justified

1. **Material is genuinely being lost.** Events occur that reach no durable store.
2. **The loss is consequential.** The lost material would change future decisions or behaviour.
3. **No existing store already holds it.** Native transcripts, application logs, or version control frequently already cover this.
4. **Capture cost is lower than reconstruction cost.** If the same insight can be derived retrospectively from existing files, capture is redundant.

## Assessment for this environment, 2026-07-31

**Verdict: not required.** Capture is already complete.

Claude Code writes a full JSONL event log per session to `~/.claude/projects/[project]/*.jsonl`. For the vault project this was 47 sessions and 24,581 events spanning 2026-05-18 to 2026-07-31, roughly 100MB.

| Signal | Already captured | Example recovered without instrumentation |
|---|---|---|
| Every user turn, timestamped | Yes | 1,422 clean user turns across 46 active days |
| Every tool call, name and input | Yes | Edit 1,432, Read 815, Bash 772, Write 234 |
| Files read and written, by path | Yes | Per-area effort distribution across the wiki |
| Session and compaction boundaries | Yes | 28 context compactions |
| Skill and command invocations | Yes | 19 skill invocations; `/model` 113 times |
| Turn pacing and interrupts | Yes | Median 3.5 tool calls per turn, p90 11, max 90 |

The analysis producing these numbers ran entirely from existing files in a single session with no prior instrumentation. A capture layer would have duplicated a store that already existed.

## Three hypotheses tested, three failed

Each would have justified a capture layer. None survived contact with the corpus.

**1. Procedural agreements are lost to context rot.**
Proposed mechanism: agreements made mid-session, not codified in [[AGENTS]] or [[CLAUDE]], drift out of context and get ignored.

Tested against the strongest candidate case (2026-07-08, *"why are you creating a structured report before Fable has done its adversarial review, like we agreed?"*). The agreement was made at 15:38, restated by the assistant at 15:43, and challenged at 15:49. The first compaction in that session occurred roughly 19 hours later. The agreement was 11 minutes old and self-restated twice, so it was neither compacted away nor decayed. It was also not homeless: the rule is written at [[multi-agent-protocol]] line 51, created 2026-07-09, the day after the correction. The correction caused the doc.

**2. Corrections cluster after compaction.**
Measured correction language in the 15 turns after each of the 28 compactions: 5.4% against a 2.4% baseline, apparently 2.27x. The signal is an artefact. Of the 13 matched turns roughly 11 are false positives, because post-compaction turns are disproportionately context-reloading turns where reported speech about third parties ("she said", "we agreed", "that was wrong") trips correction patterns. Stripped of those, the rate is indistinguishable from baseline.

**3. Compaction imposes a human re-narration tax.**
Proposed mechanism: after compaction the human must re-supply background, shifting cost rather than removing it. Measured: mean user turn length in the 10 turns following a compaction is 651 characters against a 1,001-turn baseline of 682, a ratio of **0.95x**. Post-compaction turns are marginally shorter, not longer. No tax exists.

## What the capture store is genuinely good for

Capture without retrieval still delivers value, through **aggregate analysis**. These findings are invisible from inside any single session and the wiki cannot hold them by construction, because the wiki records what is true, not where effort went.

- **Effort inverts stated priority.** Stated order is Wellbeing, Relationships, Finance, Career, Performance, Personal. Actual edit volume: career 510 (33%), ai-os 379 (24%), relationships 155 (10%), projects 145 (9%), performance 143 (9%), finance 105 (6%), wellbeing 11 (0.7%), personal 6 (0.4%).
- **A quarter of all effort maintains the machine.** `ai-os` is the second-largest area despite not being a workstream.
- **Skills are built and not adopted.** 19 invocations across 47 sessions. Never invoked once: `project-planner`, `goal-planner`, `define-user-story`, `define-enabler`, `sprint-plan`, `standup`, `morning`, `llm-council`. This is [[feedback-build-dont-adopt]] confirmed in counts.
- **There is a measurable interrupt threshold.** 11 hard "stop" interrupts, concentrated in the tail of long tool runs, including an explicit cost objection.
- **Model routing is decided 113 times without consulting existing doctrine.** A Model roles table already exists at [[multi-agent-protocol]]. This is a wiring problem, not an authoring one.

**Implementation shape:** a periodic script over existing transcripts, output as a dated article under `wiki/ai-os/logs/`. Not a runtime component.

## Relationship to semantic search

**Hard dependency, one direction only.**

- [[memory-semantic-search]] **depends on** this layer. You cannot embed what was never recorded. Capture is upstream; retrieval is downstream.
- This layer does **not** depend on semantic search. Aggregate audit value is delivered by scripted analysis alone.

**Consequence for decision-making:** always assess capture first. If capture is missing, a semantic search project cannot proceed. If capture is already solved, as it is here, the only remaining question is whether retrieval over it justifies an index.

**Synergy:** capture *quality* sets the retrieval *ceiling*. Because the JSONL carries timestamps, session ids and tool inputs, any future index can filter on metadata before ranking by similarity, which is substantially more precise than similarity alone.

**Trap:** building both at once. Where capture is already solved, adding an observation layer beside an index doubles the maintenance surface for zero added recall.

## Caveats

- The corpus begins 2026-05-18; earlier sessions may have rotated out of local storage.
- The separate `claudeclaw-os` project (48 further sessions) was excluded from this analysis.
- Skill counts capture `Skill`-tool and slash-command paths only, so they may undercount.
- JSONL retention is not guaranteed indefinitely. For long-horizon trend analysis, transcript *retention* becomes the dependency to solve, not capture.

## Related

- [[memory-semantic-search]] - the paired retrieval concept; read both before deciding
- [[memory-convention]] - what memory stores and what it must not
- [[memory-operations]] - store, inject, recall; the no-vector-DB rationale
- [[multi-agent-protocol]] - model roles table and the Fable-before-report rule
- [[feedback-build-dont-adopt]] - the adoption pattern this analysis confirmed
- [[ai-memory-paradigms]] - generic memory-architecture reference
