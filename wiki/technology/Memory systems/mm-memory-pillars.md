---
type: reference
created: 2026-08-16
status: active
tags: [technology, memory-systems, mental-models]
---

# MM: Memory Pillars

This is the Memory Pillars mental model: the compressed form of the four-pillar
architecture model in [[memory-pillars]], for recall when assessing, buying, or
building an agent memory system. It was created when the vault's mental models were
standardised into the six-slot format, so the memory domain has the same recall
layer as GenAI and rule-writing. The evidence, sub-type detail, and product
scorings stay in the Memory Systems articles; if this file and [[memory-pillars]]
disagree, that article wins and this file is corrected.

**One-liner:** Memory is four jobs in dependency order, and injection is the one
nobody builds.

**Reach for it when:** assessing, buying, or building any agent memory system, or
diagnosing why one is failing.

## Key Takeaways

- Four jobs in dependency order: **Capture → Storage → Injection → Recall**. Assess
  in order, stop at the first broken pillar.
- Assess each pillar separately: capture is often free from the platform, and a
  bundled assessment prices work that is already paid for.
- Injection is the pillar most systems under-build, and the one whose absence is
  hardest to see.
- Pillars are functions, not technologies or benefits: confusing the levels is the
  domain's standard modelling error.

## Principles

- **Dependency runs one way.** Recall cannot return what Storage never kept;
  Storage cannot keep what Capture never recorded; Injection depends on Recall
  having something to give it.
- **Each pillar has an independent owner.** Capture is frequently given free by the
  platform; the other three are almost always built. That is why they are scored
  separately: a fused model prices a build that is already paid for.
- **Injection is the under-built pillar, and its absence is invisible.** A healthy
  Storage layer makes the whole system look fine while nothing ever triggers a
  lookup.
- **Pillars are functions, not enablers and not capabilities.** Semantic search and
  capture hooks are technologies that *serve* a pillar; "compaction survival" is
  what you *get* when the right pillars work. Naming a design after an enabler and
  filling it with pillar doctrine is the domain's category error.
- **Recall forks into write-time and query-time.** Compile understanding at ingest
  (a curated wiki), or synthesise at query (search over a faithful store). Each
  wins somewhere; the fork is the paradigm debate underneath every product
  comparison.

## Guidelines

- Assess in dependency order and stop early: fixing Recall on top of broken
  Capture is building on sand.
- Name the sub-type, always: "improve Recall (query-time)" is a different piece of
  work from "improve Recall (write-time)". Sub-types per pillar are in the pillar
  articles.
- When a capability is missing, name the pillar *and* sub-type at fault
  ("compaction survival is missing because Injection (triggered) is
  unimplemented"), never the pillar alone.
- Check the Capture mode before buying a compaction fix: continuous capture needs
  only triggered Injection; periodic or boundary capture also needs event-triggered
  Capture, or material is lost twice over.
- Do not pay twice: where the platform's capture is continuous and solved, a
  proposal that includes a capture stage is charging for work already done.

## Limitations

A functional taxonomy only: it answers "what must the system do?", not "what kinds
of memory content exist and what is each tier's injection budget?" - the
complementary question content models like Kashef's six layers answer. The model is
adopted as this environment's reasoning frame, but every product assessment built
on it remains theory: nothing has been chosen or built. And it says nothing about
whether memory is worth building at all - that is routing economics
([[mm-routing]]).

## Detail

[[memory-pillars]] (canonical), then per pillar: [[memory-capture]],
[[memory-storage]], [[memory-injection]], [[memory-recall]]. The paradigm fork:
[[wiki-vs-openbrain|Wiki vs OpenBrain]]. The adoption record:
[[memory-model-adoption]]. Folder reading order:
`wiki/technology/Memory systems/_index.md`.
