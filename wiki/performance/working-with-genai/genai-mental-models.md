---
type: reference
created: 2026-08-15
status: active
tags: [working-with-genai]
---

# Working With GenAI: Mental Models

This is the recall layer for this folder. Each concept is compressed to statements of
the form *this input decides this thing*, with no explanation attached, so the set
fits on one screen and can be held in your head. It exists because the detail
articles are too long to hold, and re-deriving them from scratch costs far more than
reading them. Read it before starting substantial AI work; when a statement needs
justifying, or a case sits on a line and you need the arithmetic, follow the link to
the article that carries the evidence. **If a card and its article ever disagree, the
article wins and the card gets corrected.**

## The chain

**Verification decides what is possible, routing decides the architecture, steering
configures it.**

| Model | Answers | Detail |
|---|---|---|
| **Verification** | Is checking the work cheaper than producing it, and by what means | [[verification-bottleneck]] |
| **Routing** | Chat, one agent, several agents, or by hand | [[routing-work-to-agents]] |
| **Steering** | How the chosen thing is made to behave | No article yet, see [[#Steering]] |

They are in that order on purpose. Verification looks like the last step and is
actually the first.

---

## Verification

This is about checking **the work**, not about deciding where the work goes. Routing
consumes its answer as a gate; the model itself is a fact about generative AI.

**Generation scaled and verification did not.** Producing went up by orders of
magnitude. Confirming it is correct is still one human reading one thing at a time.
Everything below follows from that asymmetry.

**The test is comparative: is checking cheaper than producing?** Not "is this
checkable", which almost everything is at some price. If judging costs about what
generating costs, more agents buy nothing but a larger pile. Taste-only work fails
this by definition, and no architecture repairs it.

**More output is not automatically more value.** Anything that increases the volume
you are answerable for gets costed against the checking it creates, not just the
producing it saves.

Every check is one of three forms, or a layering of them.

| Form | Catches | Fails when |
|---|---|---|
| **Deterministic** | Mechanical. Does it run, does it reconcile, do the citations resolve. | There is nothing to assert against, or the question needs meaning. |
| **Agent eval** | Semantic, at volume. On brief, self-consistent, claim actually supported. | It shares the worker's model or its information, so it confirms the error. |
| **Human judgement** | Whether it is the right thing at all, whether the framing is acceptable. | Volume. It degrades quietly, not loudly. |

Layer them cheapest first, and spend judgement only where it discriminates.
Attention spent on what the first two layers would have caught is attention you no
longer have for the third.

**An eval only counts if it can fail independently.** A different vendor buys model
independence; different source information buys information independence, and that
one is free and the one people skip. An eval sharing the worker's model and context
certifies the error rather than catching it.

**Reliability is what breaks you, not unreliability.** A long run of good output is
the condition under which you stop checking, and fluent uniformly-formatted output
reads as correct whether it is or not. The failure mode is not catching fewer
errors, it is believing you are still checking after you have stopped, while the
record says the work was reviewed.

**So checking has to be built, not resolved upon.** "I'll review it" is an intention
and it degrades under exactly the volume that created the need for it. Keep attention
sub-linear to the volume: clickable citations so you verify three of thirty, output
structured so a wrong answer looks wrong, sample rather than sweep.

**The bridge to routing.** Conventional: pick the architecture, then add
verification. Correct: design the verification, and the architecture falls out. If
checking cannot be made cheap, and a human has to do all of it by hand, multiple
agents are hard to justify whatever else is true of the work.

---

## Routing

| Input | Decides |
|---|---|
| **Size** | Chat or one agent. Nothing else, and only when you are not splitting. |
| **Separation + independence** | Whether the work **wants** splitting. |
| **Verification** | Whether it is **allowed** to split. |
| **Recurrence or value** | Whether it gets built at all. |

Separation and verification answer different questions. One is demand, the other is
permission. You can want a split and be refused one.

| Fail this | You get | What you lose |
|---|---|---|
| Size | Chat | Nothing. Chat was the right tool. |
| Separation | One agent | Nothing. One agent was the right tool. |
| Verification | You do it yourself | All of it. No AI on this job. |
| Economics | You do it yourself, this once | All of it, for now. Do it again and it may qualify. |

The first two point you at a simpler tool and you keep the leverage. The last two
take AI off the table, which is why they are the two worth designing around rather
than discovering.

**Several agents is a width dial, not a setting.** Three named roles you can read sit
at one end; a workflow fanning out over hundreds sits at the other. The checkability
bar rises with the width, because the output you have to trust multiplies while your
attention does not.

**The three rules.** Split on need, not on size. Never split what you cannot check.
Never build what will not repeat or will not matter.

---

## Steering

Routing chose the architecture. Steering is how you make it behave, and the question
it answers is *what kind of thing am I trying to install*.

| What you are installing | Mechanism |
|---|---|
| A **fact** that must always be in context | `CLAUDE.md`, root or subdirectory |
| A **procedure**, run the same way each time | Skill |
| A **constraint** that binds only certain paths | Rule, path-scoped |
| Something that **must happen**, every time, without judgement | Hook |
| An **isolated side task** whose middle you do not want to see | Subagent |

**An instruction is not a guarantee.** The load-bearing rule, and the one that maps
onto verification. Claude follows a written instruction most of the time and fails
under pressure, in long sessions, or on a prompt injection in a file it reads. If
something must not happen, a sentence is the wrong tool: a hook is deterministic and
a sentence is a preference. *"The model choosing to run a formatter is different from
the formatter running automatically."*

**Everything always-loaded costs context always.** Each mechanism trades context cost
against authority. Facts earn permanent residence; procedures and constraints should
load on demand, which is what skills and path-scoped rules buy you.

**Subagents buy isolation, not just parallelism.** Their instructions never enter the
parent conversation and only the final message returns. That is the same property
routing calls independence, which is why *several agents* and *subagents* are the
same decision seen from two ends: routing decides you need minds that cannot see each
other, steering is how you build them.

**Dynamic workflows are subagents scaled up**, orchestrating tens to hundreds of
agents with the plan held in script variables rather than in context. They inherit
routing's verification gate at that width, which is where it binds hardest.

Source: [Steering Claude Code](https://claude.com/blog/steering-claude-code-skills-hooks-rules-subagents-and-more).

---

## If you remember nothing else

**Pick the lightest tool that still leaves you a result you can inspect.** Chat is
not the weak answer, it is the clean one. And if it must happen rather than usually
happen, it is a hook, not a sentence.

Setup templates for each routing verdict: [[routing-work-prompts]].
