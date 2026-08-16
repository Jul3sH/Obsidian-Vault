---
type: reference
created: 2026-08-15
updated: 2026-08-16
status: active
tags: [working-with-genai]
---

# Working With GenAI: Mental Models

This is the recall layer for this folder. Each model uses the standard six-slot
mental-model format (One-liner, Reach for it when, Principles, Guidelines,
Limitations, Detail) defined in `documentation-conventions.md`, compressed so the
set can be held in your head. It exists because the detail articles are too long to
hold, and re-deriving them from scratch costs far more than reading them. Read it
before starting substantial AI work; when a statement needs justifying, follow the
Detail link to the article that carries the evidence. **If a card and its article
ever disagree, the article wins and the card gets corrected.**

## The chain

**Verification decides what is possible, routing decides the architecture, steering
configures it.**

| Model | Answers | Detail |
|---|---|---|
| **Verification** | Is verifying the work cheaper than generating it, and by what means | [[verification-bottleneck]] |
| **Routing** | Chat, one agent, several agents, or by hand | [[routing-work-to-agents]] |
| **Steering** | How the chosen thing is made to behave | No article yet, see [[#Steering]] |

They are in that order on purpose. Verification looks like the last step and is
actually the first.

---

## Verification

**One-liner:** Generation scaled and verification did not.

**Reach for it when:** you are about to increase the volume of AI output you are
answerable for.

**Principles:**

- **The test is comparative: is verifying cheaper than generating?** Not "is this
  verifiable", which almost everything is at some price. The community names: the
  **asymmetry of verification** (Jason Wei), measured as the
  **generation-verification gap**.
- **The gap you pay is the residual** left for human judgement after the
  deterministic and eval layers have caught what they can. Building those layers is
  how the gap is shrunk, not overhead.
- **An eval only counts if it can fail independently.** Different model, different
  source information (free, and the one people skip), or ground truth. An eval
  sharing the worker's model and context certifies the error.
- **Reliability is what breaks you, not unreliability.** A long run of good output
  is the condition under which you stop checking; the failure mode is believing you
  are still checking after you have stopped.
- **A check is built, not resolved upon.** "I'll review it" is an intention, and it
  degrades under exactly the volume that created the need for it.

Every check is one of three forms, or a layering of them:

| Form                | Catches                                                                   | Fails when                                                                 |
| ------------------- | ------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| **Deterministic**   | Mechanical. Does it run, does it reconcile, do the citations resolve.     | There is nothing to assert against, or the question needs meaning.         |
| **Agent eval**      | Semantic, at volume. On brief, self-consistent, claim actually supported. | It shares the worker's model or its information, so it confirms the error. |
| **Human judgement** | Whether it is the right thing at all, whether the framing is acceptable.  | Volume. It degrades quietly, not loudly.                                   |

**Guidelines:**

- Layer the forms cheapest first; spend judgement only where it discriminates.
- Keep attention sub-linear to volume: clickable citations so you verify three of
  thirty, output structured so a wrong answer looks wrong, sample rather than sweep.
- Design the verification first and the architecture falls out, not the other way
  round.
- The full tactics in leverage order: [[verification-tactics]].

**Limitations:** taste work - no external criterion to check against, so the
judgement *is* the output - has no gap to shrink. No tactic or architecture helps;
the judgement stays human.

**Detail:** [[verification-bottleneck]], [[verification-tactics]]

---

## Routing

**One-liner:** Pick the lightest tool that still leaves you a result you can
inspect.

**Reach for it when:** deciding how to run a piece of work, before building any
setup.

**Principles:**

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

**Guidelines:**

- Walk the four-question ladder in order; the first two failures point at a simpler
  tool, the last two take AI off the table, so design around those.
- Chat is not the weak answer, it is the clean one: landing there means you avoided
  building anything.
- Several agents is a width dial, not a setting: three named roles at one end, a
  workflow over hundreds at the other, and the checkability bar rises with the
  width.
- Setup templates per verdict: [[routing-work-prompts]].

**Limitations:** the model has no lever for blast radius (cheap-to-check and
catastrophic scores like cheap-to-check and trivial), intrinsic check cost (one
output can still be hard to verify), or latency and cost. Hold those yourself.

**Detail:** [[routing-work-to-agents]], [[routing-work-prompts]]

---

## Steering

**One-liner:** An instruction is not a guarantee.

**Reach for it when:** routing has chosen the architecture and you are configuring
how it behaves.

**Principles:**

- **An instruction is not a guarantee.** Claude follows a written instruction most
  of the time and fails under pressure, in long sessions, or on a prompt injection.
  If something must not happen, a sentence is the wrong tool. *"The model choosing
  to run a formatter is different from the formatter running automatically."*
- **Everything always-loaded costs context always.** Each mechanism trades context
  cost against authority; facts earn permanent residence, procedures and
  constraints load on demand.
- **Subagents buy isolation, not just parallelism.** Their instructions never enter
  the parent conversation and only the final message returns: routing's
  independence, seen as a mechanism.
- **Dynamic workflows are subagents scaled up** - tens to hundreds of agents, the
  plan held in script variables. A width dial inside one routing verdict, not a new
  verdict, and verification's gate binds hardest there.

**Guidelines:**

Match the mechanism to what you are installing:

| What you are installing | Mechanism |
|---|---|
| A **fact** that must always be in context | `CLAUDE.md`, root or subdirectory |
| A **procedure**, run the same way each time | Skill |
| A **constraint** that binds only certain paths | Rule, path-scoped |
| Something that **must happen**, every time, without judgement | Hook |
| An **isolated side task** whose middle you do not want to see | Subagent |

**Limitations:** steering shapes behaviour, not capability - which model and how
much effort are separate dials it cannot reach. And its mechanisms are
harness-specific and perishable: the principles above outlive any particular
mechanism table.

**Detail:** no wiki article yet;
[Steering Claude Code](https://claude.com/blog/steering-claude-code-skills-hooks-rules-subagents-and-more)
is the source.

---

## If you remember nothing else

The three one-liners, in chain order: **generation scaled and verification did
not**, so **pick the lightest tool that still leaves you a result you can
inspect**, and once picked, remember **an instruction is not a guarantee**.
