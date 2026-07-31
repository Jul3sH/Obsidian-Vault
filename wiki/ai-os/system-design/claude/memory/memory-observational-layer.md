---
type: doctrine
updated: 2026-07-31
authority: analysis-backed
---

# Observational Memory Layer

> *Assessed 2026-07-31. Verdict: not required. Claude Code's JSONL session transcripts already hold the complete observational record, so retrospective behavioural analysis needs a periodic script, not a live capture layer.*

## Key Takeaways

- **The JSONL transcripts are already an observational store.** Every user turn, assistant turn, tool call, tool input, timestamp and session boundary is written to `~/.claude/projects/[project]/*.jsonl`. Nothing needs to be captured live because nothing is being lost.
- **An observational layer would pay a continuous cost to reconstruct what is already on disk for free.** The analysis that produced this article was run entirely from existing files, in one session, with no prior instrumentation.
- **The session-memory case for observational memory did not survive testing.** Two separate hypotheses (procedural agreements lost to context rot; corrections clustering after compaction) were tested against the corpus and both failed.
- **The real gap is aggregate visibility, not recall.** Frequency and distribution facts are invisible from inside any single session, and the wiki cannot hold them by construction: the wiki records what is true, not where effort went.
- **Therefore: a periodic audit script, not a live layer.** Anything else adds a system to maintain, which is itself the pattern the audit exposes.

---

## The question

Does this environment need an observational memory layer: a live capture mechanism that watches sessions and accumulates behavioural patterns over time?

The prior assumption was that strict wiki discipline (a canonical, human-maintained decision layer) had already made such a layer redundant. This article records the test of that assumption.

## Finding: the transcript is the observational store

Claude Code writes a complete JSONL event log per session. For the vault project this was 47 sessions and 24,581 events spanning 2026-05-18 to 2026-07-31, about 100MB.

What is recoverable from it, with no additional instrumentation:

| Signal | Recoverable | Example finding |
|---|---|---|
| Every user turn, with timestamp | Yes | 1,422 clean user turns across 46 active days |
| Every tool call, name and input | Yes | Edit 1,432, Read 815, Bash 772, Write 234 |
| Files written and read, by path | Yes | Per-area effort distribution across the wiki |
| Session and compaction boundaries | Yes | 28 context compactions |
| Skill and slash-command invocations | Yes | 19 skill invocations; `/model` 113 times |
| Turn-level pacing and interrupts | Yes | Median 3.5 tool calls per turn, p90 11, max 90 |

This is the same substrate a live observational layer would build. It exists already, it is complete, and it is queryable at any time.

## What was ruled out

Two hypotheses for why a live layer might still be needed were tested and failed.

**1. Procedural agreements are lost to context rot.**
The proposed mechanism was that agreements made mid-session, not codified in [[AGENTS]] or [[CLAUDE]], drift out of context and get ignored.

Tested against the strongest candidate case in the corpus (2026-07-08, *"why are you creating a structured report before Fable has done its adversarial review, like we agreed?"*). The timeline refutes it: the agreement was made at 15:38, restated by the assistant at 15:43, and challenged at 15:49. The first compaction in that session occurred roughly 19 hours later. The agreement was 11 minutes old and self-restated twice, so it was neither compacted away nor decayed.

That agreement was also not homeless. It is written at [[multi-agent-protocol]] line 51 (*"Fable reviews BEFORE the report is written, not after"*), created 2026-07-09, the day after the correction. The correction caused the doc.

**2. Corrections cluster after compaction.**
Measured correction language in the 15 turns following each of the 28 compactions against baseline: 5.4% versus 2.4%, apparently 2.27x.

The signal is an artefact. Reading the 13 matched turns, roughly 11 are false positives: post-compaction turns are disproportionately context-reloading turns, where reported speech about third parties ("she said", "we agreed", "that was wrong") triggers correction patterns. Stripped of those, the post-compaction rate is not distinguishable from baseline.

**Corollary worth keeping:** the compaction tax is real but it lands on the human, not the assistant. The cost is re-narrating background, not forgotten rules.

## What retrospective analysis surfaced

These are the findings that justified the exercise. All four are aggregate facts, invisible from inside any single session.

**Effort inverts stated priority.** Stated order is Wellbeing, Relationships, Finance, Career, Performance, Personal. Actual wiki edit volume: career 510 (33%), ai-os 379 (24%), relationships 155 (10%), projects 145 (9%), performance 143 (9%), finance 105 (6%), wellbeing 11 (0.7%), personal 6 (0.4%). The top-stated priority received 11 edits; the fourth received 510.

**A quarter of all effort maintains the machine.** `ai-os` is the second-largest area by edit volume despite not being a workstream.

**Skills are built and not adopted.** 19 skill invocations across 47 sessions. Never invoked once: `project-planner`, `goal-planner`, `define-user-story`, `define-enabler`, `sprint-plan`, `standup`, `morning`, `llm-council`, `decision-visualisation-check`. This is the [[feedback-build-dont-adopt]] pattern confirmed in counts rather than prose, and it accounts for much of the 24% above.

**There is a measurable interrupt threshold.** 11 hard "stop" interrupts. Tool runs before the user regains a turn: median 3.5, p90 11, max 90. Interrupts concentrate in the tail, including an explicit cost objection (*"this is not a good usage of credits"*). Nothing in the wiki records this threshold.

**Model routing is decided 113 times without consulting existing doctrine.** `/model` is the most-used command by roughly 50x. A Model roles table already exists at [[multi-agent-protocol]]. This is a wiring problem, not an authoring one: tier-2 doctrine that is never read at the decision point.

## Why an audit, not a layer

- The findings are **retrospective by nature**. None require real-time capture.
- The **data is already complete**. A live layer would duplicate an existing store.
- Adding an always-on system to an environment where system-maintenance is already 24% of effort is precisely the failure mode findings 1 and 3 jointly describe.

Implementation shape: one script, run periodically, output as a dated article under `wiki/ai-os/logs/`. Not a runtime component.

## Caveats

- The corpus begins 2026-05-18; earlier sessions may have rotated out of local storage.
- The separate `claudeclaw-os` project (51 further sessions) was excluded from this analysis.
- Skill counts capture `Skill`-tool and slash-command invocation paths only, so they may undercount.
- JSONL retention is not guaranteed indefinitely. If long-horizon trend analysis is ever wanted, transcript retention becomes the dependency to solve, not capture.

## Related

- [[memory-convention]] - what memory stores and what it must not
- [[memory-operations]] - store, inject, recall; the no-vector-DB rationale
- [[memory-system-explained]] - plain-language ownership view
- [[multi-agent-protocol]] - model roles table and the Fable-before-report rule referenced above
- [[feedback-build-dont-adopt]] - the adoption pattern this analysis confirmed
- [[ai-memory-paradigms]] - generic memory-architecture reference
