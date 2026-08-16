---
type: reference
created: 2026-08-16
status: active
tags: [working-with-genai, verification, mental-models]
---

# MM: Verification

This is the Verification mental model: whether a piece of AI work can be checked
cheaply enough to be worth commissioning, and by what means. It was split out of
the former combined GenAI card so each model stands on its own in the six-slot
format. Read it before increasing the volume of AI output you are answerable for;
the evidence behind every statement is in [[verification-bottleneck]], and the
practical build-out is in [[verification-tactics]].

**One-liner:** Generation scaled and verification did not.

**Reach for it when:** you are about to increase the volume of AI output you are
answerable for.

**Position in the chain:** first. Verification decides what is possible, routing
decides the architecture, steering configures it. Verification looks like the last
step and is actually the first.

## Key Takeaways

- Verifying must be cheaper than generating, or delegation buys you nothing however
  many agents you use.
- The gap you personally pay is the residual left after the cheaper layers catch
  what they can, so building those layers *is* the work.
- An eval that shares the worker's model and context certifies errors rather than
  catching them.
- Reliability, not unreliability, is what stops you checking.

## Principles

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

## Guidelines

- Layer the forms cheapest first; spend judgement only where it discriminates.
- Keep attention sub-linear to volume: clickable citations so you verify three of
  thirty, output structured so a wrong answer looks wrong, sample rather than sweep.
- Design the verification first and the architecture falls out, not the other way
  round.
- The full tactics in leverage order: [[verification-tactics]].

## Limitations

Taste work - no external criterion to check against, so the judgement *is* the
output - has no gap to shrink. No tactic or architecture helps; the judgement stays
human. The model also says nothing about whether work is worth doing at all, only
whether it can be checked once commissioned.

## Detail

[[verification-bottleneck]] (why it matters, the research, the three biases),
[[verification-tactics]] (the four layers in leverage order). If this model and
those articles disagree, the articles win and this file is corrected.
