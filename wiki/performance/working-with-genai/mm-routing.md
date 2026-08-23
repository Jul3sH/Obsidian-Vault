---
type: reference
created: 2026-08-16
status: active
tags: [working-with-genai, routing, mental-models]
---

# MM: Routing

This is the Routing mental model: how to run a given piece of work, choosing
between chat, one agent, several agents, or by hand. It was split out of the former
combined GenAI card so each model stands on its own in the six-slot format. Read it
before setting up any substantial piece of AI work; the four-question ladder, the
arithmetic for borderline cases, and the evidence are in
[[routing-work-to-agents]], and the setup templates per verdict are in
[[routing-work-prompts]].

**One-liner:** Pick the lightest tool that still leaves you a result you can
inspect.

**Reach for it when:** deciding how to run a piece of work, before building any
setup.

**Position in the chain:** second. Verification decides what is possible, routing
decides the architecture, steering configures it.

## Key Takeaways

- Split on need, not on size: volume is a reason for a longer leash, not more
  agents.
- Never split what you cannot check - an unverifiable split is worse than no split.
- Never build what will not repeat or will not matter; either bar alone passes,
  middling at both fails.
- Chat is the clean answer, not the weak one.

## Principles

- **Split on need, not on size.** Big work with nothing to separate is one agent on
  a longer leash; small work that needs separate minds still faces the check.
- **Never split what you cannot check.** Separation is demand, verification is
  permission: you can want a split and be refused one.
- **Never build what will not repeat or will not matter.** Two separate bars,
  either alone passes; middling at both fails.

| Input | Decides |
|---|---|
| **Size** | Chat or one agent. Nothing else, and only when you are not splitting. |
| **Separation + independence** | Whether the work **wants** splitting. |
| **Verification** | Whether it is **allowed** to split. |
| **Recurrence or value** | Whether it gets built at all. |

| Fail this | You get | What you lose |
|---|---|---|
| Size | Chat | Nothing. Chat was the right tool. |
| Separation | One agent | Nothing. One agent was the right tool. |
| Verification | You do it yourself | All of it. No AI on this job. |
| Economics | You do it yourself, this once | All of it, for now. Do it again and it may qualify. |

The first two failures point at a simpler tool and you keep the leverage. The last
two take AI off the table, which is why they are the two worth designing around
rather than discovering.

## Guidelines

- Walk the four-question ladder in order; the first two failures point at a simpler
  tool, the last two take AI off the table, so design around those.
- Chat is not the weak answer, it is the clean one: landing there means you avoided
  building anything.
- Several agents is a width dial, not a setting: three named roles at one end, a
  workflow over hundreds at the other, and the checkability bar rises with the
  width.
- When work lands on *by hand* because you cannot check it, build the check rather
  than shrinking the work. The check is the only input you construct rather than
  observe.
- Setup templates per verdict: [[routing-work-prompts]].

## Limitations

The model has no lever for blast radius (cheap-to-check and catastrophic scores
like cheap-to-check and trivial), intrinsic check cost (one output can still be
hard to verify), or latency and cost. Hold those yourself, or reach for the
companion models: [[mm-blast-radius]] for reach and reversibility,
[[mm-token-economics]] for cost. It also assumes the work
is worth doing: it chooses the architecture, not the objective.

## Detail

[[routing-work-to-agents]] (the ladder, the arithmetic, what the source tool gets
wrong), [[routing-work-prompts]] (setup templates per verdict). If this model and
those articles disagree, the articles win and this file is corrected.
