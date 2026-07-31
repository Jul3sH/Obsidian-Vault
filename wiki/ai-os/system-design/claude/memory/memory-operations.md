---
type: article
updated: 2026-07-31
---

# Memory Operations

> *How memory is operated at runtime **in this environment**: what loads every session, what is left to on-demand recall, and the standing decision not to add a vector index over the wiki corpus.*

For the memory file types, format, and loading rule, see [[_index|Memory]].

> [!warning] Framework superseded
> This article previously defined memory as three operations, **Store, Inject, Recall**. That framing is superseded by the four-pillar model (**Capture → Storage → Injection → Recall**) in [[memory-pillars]], which splits capture out of storage and gives each pillar its two sub-types. Use the four-pillar model for any new analysis. This article now covers only how those pillars are **configured here**.

## Current configuration

| Pillar        | How it is configured in this environment                                                                                                                       |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Capture**   | Claude Code JSONL session transcripts. Automatic and complete, but inert: they only become memory when explicitly read                                         |
| **Storage**   | Curated markdown. Memory files at the hidden path (`user.md`, `feedback-*.md`); everything else as wiki articles                                               |
| **Injection** | **Scheduled only.** `user.md` in full plus the `MEMORY.md` index at session start, and the `CLAUDE.md` / `AGENTS.md` rulebook. There is no triggered injection |
| **Recall**    | Hand-curated `_index` navigation plus `[[wikilinks]]`. No vector index                                                                                         |

**Injection is proactive; recall is reactive.** Injection pays a fixed context cost every session to guarantee presence. Recall pays nothing until needed but risks missing the relevant item. The craft is deciding which knowledge is hot enough to deserve injection, and leaving the rest to recall.

**Known gap:** because injection here is scheduled only, nothing pulls relevant material back in mid-session. Recall depends on the human asking for it. See the trigger analysis in [[memory-semantic-search]].

## Worked example: principles and lessons learned

The lessons-learned corpus (~38 docs: career office-politics, the Personal MBA folders in performance, plus relationships and wellbeing) is fundamentally a **recall** problem: "I'm in a situation, surface what I've learned that applies." The design answers it by splitting recall across two tiers:

- **Tier 1 - Principles register (injected).** Each lesson doc's `## Key Takeaways` is distilled into a single register of one-line principles, workstream-tagged, each backlinking to its source doc. Small enough to load every session. Because the headline lessons are always present, the model never has to *fetch* them: the hot path becomes injection.
- **Tier 2 - Full lesson docs (recalled).** The articles stay where they are (mostly already consolidated under `wiki/performance/` Personal MBA folders). Retrieved on demand via `_index` navigation when the depth, rationale, or Personal Log evidence is needed, one hop down the backlink from the Tier 1 entry.

**Storage decision:** lessons stay filed by workstream, not relocated. Domain-specific strategy (office politics) belongs in its domain; only generic-effectiveness lessons live in performance, which the taxonomy already enforces.

## Why no vector index over the wiki corpus (yet)

**Scope note:** this decision concerns the **wiki article corpus**. The separate question of indexing the **JSONL transcript corpus** is assessed in [[memory-semantic-search]] and reaches a different conclusion, because the material has different properties. Do not read one as settling the other.

At ~38 docs the hand-curated `_index` descriptions plus `[[wikilinks]]` already form a semantic retrieval layer that is more precise than embedding similarity, with no embedding pipeline, chunking, or re-embed-on-edit drift.

**Revisit trigger:** when the corpus passes ~100-150 docs, or when the model is observed systematically missing relevant cross-folder lessons. At that point, embed Tier 2 only; Tier 1 stays in context.

Assessed against the five-criteria test in [[memory-semantic-search]], the wiki corpus currently fails criteria 1 (volume is browsable), 2 (articles are titled, tagged and linked) and 4 (already curated into a canonical store). That is why the answer differs from the transcript corpus, which fails none of those.

## Key Takeaways

- The **Store/Inject/Recall** framing is superseded. Use **Capture → Storage → Injection → Recall** ([[memory-pillars]]).
- Injection here is **scheduled only**: `user.md` and the `MEMORY.md` index at session start. Nothing injects mid-session, so recall depends on the human asking.
- Injection is proactive and pays a fixed cost; recall is reactive and risks missing items. Promote knowledge to injection only when it is hot enough to justify the cost.
- A recall problem can be partly solved by converting the hot path into injection. That is what the two-tier principles-and-lessons design does.
- Keep lessons filed by workstream; distill their Key Takeaways into an always-on register; leave full docs for on-demand retrieval.
- **No vector index over the wiki corpus** until it outgrows the hand-curated index (~100-150 docs); then embed the recall tier only. This is a separate question from indexing the transcripts.
