---
type: article
updated: 2026-06-08
---

# Memory Operations: Store, Inject, Recall

> *The three operations that govern memory in the AI OS. Every memory decision is one of these three.*

For the memory file types, format, and loading rule, see [[_index|Memory]].

## The Three Operations

| Operation | Question it answers | Trigger | Examples |
|-----------|--------------------|---------|----------|
| **Store** | What do we keep, and where? | New durable knowledge emerges | Lessons stay filed under their workstream; `## Key Takeaways` distilled into the principles register; `user.md` gains a new persistent fact |
| **Inject** | What loads unconditionally, every session? | Session start, no query needed | `user.md`; the Tier 1 principles register; `CLAUDE.md` rules |
| **Recall** | What gets retrieved on demand for the situation at hand? | A live situation or query, semantically matched | The full lessons-learned docs, fetched via `_index` navigation when depth is needed |

**Inject is proactive; Recall is reactive.** Inject pays a fixed context cost every session to guarantee presence. Recall pays nothing until needed but risks missing the relevant item. The craft is deciding which knowledge is hot enough to deserve injection, and leaving the rest to recall.

## Worked Example: Principles & Lessons Learned

The lessons-learned corpus (~38 docs: career office-politics, the Personal MBA folders in performance, plus relationships and wellbeing) is fundamentally a **recall** problem: "I'm in a situation, surface what I've learned that applies." The design answers it by splitting recall across two tiers:

- **Tier 1 - Principles register (Inject).** Each lesson doc's `## Key Takeaways` is distilled into a single register of one-line principles, workstream-tagged, each backlinking to its source doc. Small enough to load every session. Because the headline lessons are always present, the model never has to *fetch* them: the hot path becomes injection.
- **Tier 2 - Full lesson docs (Recall).** The articles stay where they are (mostly already consolidated under `wiki/performance/` Personal MBA folders). Retrieved on demand via `_index` navigation when the depth, rationale, or Personal Log evidence is needed - one hop down the backlink from the Tier 1 entry.

**Storage decision:** lessons stay filed by workstream, not relocated. Domain-specific strategy (office politics) belongs in its domain; only generic-effectiveness lessons live in performance, which the taxonomy already enforces.

**Why no vector DB (yet).** At ~38 docs the hand-curated `_index` descriptions plus `[[wikilinks]]` already form a semantic retrieval layer that is more precise than embedding similarity, with no embedding pipeline, chunking, or re-embed-on-edit drift. Revisit only when the corpus passes ~100-150 docs, or when the model is observed systematically missing relevant cross-folder lessons. At that point, embed Tier 2 only; Tier 1 stays in context.

## Key Takeaways

- Memory has three operations: **Store** (what to keep and where), **Inject** (always-on context), **Recall** (on-demand retrieval).
- Inject is proactive and pays a fixed cost; Recall is reactive and risks missing items. Promote knowledge to Inject only when it is hot enough to justify the cost.
- A recall problem can be partly solved by converting the hot path into injection - this is what the two-tier principles-and-lessons design does.
- Keep lessons filed by workstream (Store); distill their Key Takeaways into an always-on register (Inject); leave full docs for on-demand retrieval (Recall).
- No vector DB until the corpus outgrows the hand-curated index (~100-150 docs); then embed the recall tier only.
