---
type: doctrine
updated: 2026-07-31
authority: analysis-backed
---

# Observational Memory Layer

> *Assessed 2026-07-31. Verdict: no observational **capture** layer is required, because the JSONL session transcripts already hold the complete record. A narrow **retrieval** gap does exist over that same material. This article also sets out a transferable five-criteria test for judging the question in any agentic OS.*

## Key Takeaways

- **Separate capture from retrieval before deciding anything.** A vector store is a retrieval technology; it adds nothing to capture. Conflating the two is what produces the wrong engineering choice.
- **The JSONL transcripts are already an observational store.** Every user turn, assistant turn, tool call, tool input, timestamp and session boundary is written to `~/.claude/projects/[project]/*.jsonl`. Nothing needs capturing live because nothing is being lost.
- **An observational capture layer would pay a continuous cost to reconstruct what is already on disk for free.** The analysis behind this article ran entirely from existing files, in one session, with no prior instrumentation.
- **Three session-memory hypotheses were tested and all three failed:** procedural agreements lost to context rot; corrections clustering after compaction; and a human re-narration tax after compaction.
- **The decision hinges on the retrieval-key problem, not on subject matter.** A semantic layer wins specifically when the user remembers the *content* but not the *name or phrasing*, which is where grep fails. Engineering workloads exhibit this strongly, but they do not own it.
- **The retrieval needs here are real but low-frequency and decision-support shaped**, not engineering shaped: provenance of self-stated figures, recall over unstructured pastes, and pre-wiki history.
- **Therefore: index the existing transcripts, do not build a runtime capture-and-embed pipeline.** And run the aggregate audit as a periodic script, since those findings are retrospective by nature.

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

**A third hypothesis was also tested and failed.** The suggestion that compaction shifts cost onto the human, who must re-narrate background afterwards, does not hold either. Mean user turn length in the 10 turns after a compaction is 651 characters against a 1,001-turn baseline of 682, a ratio of **0.95x**. Post-compaction turns are marginally *shorter*, not longer. There is no measurable re-narration tax.

## What retrospective analysis surfaced

These are the findings that justified the exercise. All four are aggregate facts, invisible from inside any single session.

**Effort inverts stated priority.** Stated order is Wellbeing, Relationships, Finance, Career, Performance, Personal. Actual wiki edit volume: career 510 (33%), ai-os 379 (24%), relationships 155 (10%), projects 145 (9%), performance 143 (9%), finance 105 (6%), wellbeing 11 (0.7%), personal 6 (0.4%). The top-stated priority received 11 edits; the fourth received 510.

**A quarter of all effort maintains the machine.** `ai-os` is the second-largest area by edit volume despite not being a workstream.

**Skills are built and not adopted.** 19 skill invocations across 47 sessions. Never invoked once: `project-planner`, `goal-planner`, `define-user-story`, `define-enabler`, `sprint-plan`, `standup`, `morning`, `llm-council`, `decision-visualisation-check`. This is the [[feedback-build-dont-adopt]] pattern confirmed in counts rather than prose, and it accounts for much of the 24% above.

**There is a measurable interrupt threshold.** 11 hard "stop" interrupts. Tool runs before the user regains a turn: median 3.5, p90 11, max 90. Interrupts concentrate in the tail, including an explicit cost objection (*"this is not a good usage of credits"*). Nothing in the wiki records this threshold.

**Model routing is decided 113 times without consulting existing doctrine.** `/model` is the most-used command by roughly 50x. A Model roles table already exists at [[multi-agent-protocol]]. This is a wiring problem, not an authoring one: tier-2 doctrine that is never read at the decision point.

## Capture versus retrieval: the distinction that decides this

The verdict above is about **capture**. It is not a verdict on **retrieval**, and conflating the two produces the wrong engineering decision.

| Axis | Question | Status here |
|---|---|---|
| **Capture** | Does the material exist in durable storage? | **Solved.** 100MB of complete JSONL, no instrumentation needed |
| **Retrieval** | Can you find the right piece of it on demand? | **Not solved.** grep over 100MB of JSONL is genuinely bad |

A semantic (vector) layer is a *retrieval* technology. It adds nothing to capture. So the only defensible reason to build one is a demonstrated retrieval failure over material that is already being captured.

## When a semantic layer is justified: a transferable test

Applicable to any agentic OS, not just this one. A vector store pays for itself only when **all five** hold. The third is the crux.

1. **Volume exceeds browsing capacity.** If a human can scan the file list, they do not need embeddings.
2. **Material is unstructured and untitled at capture time.** No filename, no tag, no link was ever assigned.
3. **The retrieval key is unknown at query time.** The user remembers the *content* but not the *name or phrasing*. This is precisely where grep fails and embeddings win: grep requires you to already know a distinctive string.
4. **The material is not already curated into a canonical store.** Otherwise the layer duplicates an existing index.
5. **Query frequency is high enough to amortise build and maintenance cost.**

**Why generic advice on this topic reads as engineering-flavoured:** software engineering workloads score high on 1, 2 and 3 automatically. Error traces, stack dumps and dead-end approaches are high-volume, never titled, and recalled by symptom rather than by name. That is a *correlation with the criteria*, not a property of engineering itself. The underlying driver is the retrieval-key problem in criterion 3, and non-engineering workloads can exhibit it too.

## Scoring the common use cases against this environment

The five use cases most often cited for observational memory, tested against the corpus:

| Use case | Verdict here | Evidence |
|---|---|---|
| **Vocabulary bridging** over unstructured pastes | **Strong** | 128 pastes over 1,200 chars (10% of turns), largest 16,704. Untitled, untagged, grep-hostile |
| **Cross-tool continuity** across agents | **Real need, misdiagnosed** | The claim that the material "does not exist as files" is false. Codex persists `~/.codex/sessions/`, `session_index.jsonl`, `memories_1.sqlite`. A further 48 Claude sessions sit under `claudeclaw-os`. This is a **federation** problem, not a capture problem, and the fix is far cheaper |
| **Session residue**, rejected options and reasoning | **Partly valid, overstated** | The "0% reaches the vault" claim fails here: [[decision-journal]], the decision register, `uk-move/capture.md` (31 edits) and the Cause-Event-Effect-Response risk register exist specifically to record roads not taken. The gap is only the *unfiled* residue |
| **Negative knowledge**, failures and dead ends | **Weak here** | 119 tool errors across 24,581 events (0.5%). Edits are 98% prose (1,615 markdown vs 29 code/config); Bash is navigation (`cd` 389, `grep` 79, `ls` 61), not build-test-debug. High-value negative knowledge already got written because pain forced it, e.g. the HK VPN routing constraints in [[CLAUDE]] |
| **Temporal queries** | **Already solved** | JSONL carries timestamps and vault-backup commits carry dates. Questions of this exact shape were answered during this analysis, e.g. establishing that `multi-agent-protocol.md` was first written 2026-07-09T11:17 |

**This is not simply an engineering-versus-not split.** Two of the five fail here because this environment is a decision-support workload rather than a build workload, but genuine retrieval needs remain, and they are not engineering-shaped.

## The retrieval use cases that do apply here

Derived from the corpus rather than adapted from a generic list.

- **Provenance of self-stated facts.** 25 instances of the user asking where a figure originated or what they themselves previously stated: *"where's the AR cap come from?"*, *"what did we say the MPF pot is?"*, *"What did I say my ISA investments are currently worth and also what did I say the value of my UK current account is?"* These are decision-support queries, not engineering ones, and they satisfy criterion 3 exactly: the content is remembered, the phrasing is not.
- **Unstructured paste recall.** The 128 large pastes: WhatsApp archives, meeting recaps, salary and job-market dumps, call debriefs. Some are filed into the wiki; the remainder are recoverable only from transcripts.
- **Pre-structure history.** Explicitly requested: *"do you have any visibility of the tasks that I did when I was preparing for my Cisco interview? I think it might have been pre-wiki."* Material predating the current wiki conventions has no canonical home by definition.
- **Cross-agent federation.** Real, but currently low volume (6 Codex session files against 47 Claude ones), and partially addressed already by [[AGENTS]] acting as the deliberate shared layer.

Against the five criteria, these clear 1, 2 and 3 but are marginal on 5: roughly 25 provenance queries across ten weeks is a low amortisation base. That argues for indexing existing transcripts rather than building a runtime capture-and-embed pipeline.

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
