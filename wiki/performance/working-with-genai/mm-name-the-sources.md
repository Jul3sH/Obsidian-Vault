---
type: reference
created: 2026-10-09
status: active
tags: [working-with-genai, steering, sources, mental-models]
---

# MM: Name the Sources

## Purpose

The Name the Sources mental model: before an AI works from a knowledge base, tell it which sources are authoritative, what each is authoritative for, and what is off limits. It exists because a model told only "use the wiki" cannot tell a current record from a superseded or experimental one.

**One-liner:** "Use the wiki" is not a source brief.

**Reach for it when:** you are about to ask a model, a subagent or a second model (such as Codex) to research, draft or review something using facts from the wiki.

**Position in the chain:** part of steering ([[mm-steering]]): it configures what the agent may treat as true. It also sets up verification ([[mm-verification]]): a reviewer can only check claims against sources that were named.

## Key Takeaways

- A knowledge base holds current, superseded, experimental and working records side by side. A model weights them all the same.
- Name three things: the authoritative sources, what each is authoritative for, and what must never be used.
- The brief must travel: a subagent or external reviewer inherits none of your context, so the source list goes into its prompt.

## Principles

- **Authority is not visible from inside a file.** A dated, confident record reads as fact whether it is current or an abandoned experiment. Only the person who wrote the knowledge base knows which is which.
- **Authority is per question, not per file.** A file can be authoritative for dates and wrong on law. Say what each source is authoritative *for*.
- **An exclusion list is as important as an inclusion list.** One plausible wrong source does more damage than a missing right one, because its claim arrives with a citation.
- **A named source list makes review possible.** A reviewer told "check this against the wiki" re-runs the same search with the same blind spots; a reviewer told "check every claim traces to these files" can come back negative.

## Guidelines

- Ask, then propose: the model can suggest candidate sources from the wiki, but the human confirms, cuts and adds.
- Record the confirmed list where the work lives (a deliverable's Prompt Zero, Q8), so later sessions and reviewers read the same list.
- Give a tie-break: when two sources disagree on a fact, which one wins.
- Skip it for quick factual questions; it is for work someone will act on.

## Limitations

It only works if the knowledge base's own status signals are honest: a file marked authoritative that is out of date still misleads. It also adds a question before work starts, so it is wasted on throwaway lookups.

## Detail

The rule: AGENTS.md § Name the Sources. Where the answer is recorded: the `/prompt-zero` skill, Q8. The first worked example: the source table in [[clodagh-consent-letter]].

## Evidence

| Date | Event | Lesson in action | Source |
|------|-------|-------------------|--------|
| 2026-10-09 | A subagent asked to answer an evidence checklist "from the wiki" found the decision journal's "MOVE committed 4 Jul" and reported it as fact. It reached me as a correction of my own account. The journal was an experiment with a decision process, never an authoritative record | Tell the model which files count and which never do. The same day, the letter to Clodagh got a source table with an explicit "never use" row | [[genai-task-workflow-log]] (9 Oct 2026), [[HK-Return-habitual-residency-perplexity]] |

## Document Log

| Date | Change |
|---|---|
| 2026-10-09 | Created at Julian's request from the 9 Oct sourcing error. Not yet adversarially reviewed. |
