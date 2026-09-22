---
type: reference
created: 2026-09-21
---

# Mental Models System

> **Purpose block.** This is the whole-system overview of the mental-models estate: the one place that shows how the cards, the indexes, the detail articles, and the retrieval machinery fit together. It was created on 21 Sep 2026 after Julian had to reverse-engineer his own system through a session of Q&A - every part was documented, but across five surfaces with the whole stated nowhere. Read it to reorient before adding a card, a bias, or machinery; it maps the system and defines nothing, so each component's own document (linked below) stays authoritative for its rules.

## Key Takeaways

- Every card is a mental model. A bias card is a mental model with extra plumbing; it is a subtype, not a parallel category.
- The system is four tiers: source evidence, evidence rows, six-slot card, detail article. The detail article wins on any disagreement with its card.
- Retrieval is the point. Three paths exist: trigger-fired (the bias-check dispatcher), spaced repetition (session-start hook), and manual reach via the indexes.
- The capture path replaces a lessons-learned register: a new lesson becomes an evidence row on an existing card, or a new card, in the same operation. Nothing is appended to a write-only list.
- Format rules live in [[documentation-conventions]] Part 1. This file is a map, not a second rulebook.

## The four tiers

| Tier | Artefact | Job |
|------|----------|-----|
| 1. Source evidence | The 303 archived lesson files in `raw/_processed/`, plus live session events | The raw record; cited, never edited |
| 2. Evidence rows | Dated rows in a card's Evidence table (Date, Event, Lesson in action, Source) | Prove the pattern with instances; the write-point for new lessons |
| 3. Six-slot card | `mm-*.md`: One-liner, Reach for it when, Principles, Guidelines, Limitations, Detail (Key Takeaways above Principles) | The reach-for layer: recalled under pressure, raised by machinery |
| 4. Detail article | Ordinary wiki article linked from the card's Detail slot | The full framework; wins if it disagrees with the card |

Some cards are self-contained pending a detail article and say so in their Detail slot.

## Taxonomy

⚠ Counts as of 21 Sep 2026: 63 cards.

```
Mental models (63) - all mm-*.md, six-slot
├── Bias cards (17)        patterns that distort
│                          "-bias" filename suffix
│                          row in biases-index (keyed by trigger situation)
│                          covered by a bias-check skill trigger
└── Discipline cards (46)  practices to apply
                           mental-models-index only
```

A bias card and its countermeasure discipline card are separate files that link to each other and never restate each other's content.

## Retrieval paths

| Path | Mechanism | Harness |
|------|-----------|---------|
| Trigger-fired | The [[ai-os/skills/bias-check/SKILL|bias-check]] skill dispatches over [[biases-index]] when a conversation enters a documented trigger situation; [[ai-os/skills/commitment-guard/SKILL|commitment-guard]] and [[ai-os/skills/decision-visualisation-check/SKILL|decision-visualisation-check]] guard their own cards | Claude (agent-fired) |
| Spaced repetition | Session-start hook resurfaces cards created 1 day, 1 week, and 1 month ago for retention | Claude (hook) |
| Manual reach | [[mental-models-index]] (all cards, by workstream) and [[biases-index]] (biases, by trigger situation); cards cross-link bias to countermeasure | Any agent, or Julian directly |

## Capture path (replaces a lessons-learned register)

1. Lesson matches an existing card: add a dated evidence row to that card.
2. Genuinely new pattern: new `mm-*.md` card plus its [[mental-models-index]] row; if a bias, also the [[biases-index]] row and bias-check trigger coverage, all in the same operation.
3. Correction to how an agent should work: feedback memory, not a card.
4. Lesson about AI-routed work: row in [[genai-task-workflow-log]].
5. The weekly `/retro` is the sweep that catches what the moment missed.

## Component map

| Component | Location | Holds |
|-----------|----------|-------|
| Format and naming rules (authoritative) | [[documentation-conventions]] Part 1 | Six-slot format, `mm-`/`MM: ` naming, one-model-one-file, the every-bias-has-a-card rule |
| Card catalogue | [[mental-models-index]] | Every card, by workstream, with one-liners; the two-tier filing test |
| Bias catalogue | [[biases-index]] | The 17 bias cards keyed by firing situation |
| Retrieval machinery | `wiki/ai-os/skills/` (bias-check, commitment-guard, decision-visualisation-check) | Skill definitions mirroring `~/.claude/skills/` |
| Theory (why the system exists) | [[knowledge-and-mental-models]] | Knowledge-as-stock, the activation loop |
| Provenance records | [[mental-models-rebuild]], [[bias-history-review]] | How the set was built from the 303 lesson files and the history scan |
| Accountability | [[systems-register]] row SYS-9 | Whether the system is actually being used |
