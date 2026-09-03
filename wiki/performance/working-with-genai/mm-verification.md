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

**Position in the chain:** second. Work types classifies and hands over its
default check; verification tests whether that check holds here, and vetoes the
run if it does not. The check is still designed before the run, never after -
verification looks like the last step and comes at the start. Full chain:
[[genai-task-workflow]].

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

## Evidence

| Date | Event | Lesson in action | Source |
|------|-------|-------------------|--------|
| 2026-08-23 | A team of AI agents wrote 9 wiki articles, each one checked by a second AI. But the final agent - the one that combined everything at the end and wrote two extra files and an index - ran after the checking was done, so its output was never checked by anyone. One of its files contained a false claim, and it nearly got my sign-off | When AI builds something in stages, every stage that writes content needs its own checker. The final pull-it-together stage is the one that gets missed, because it runs after the checking feels finished. Decide who checks each output before the run starts, not after | AGENTS.md (Adversarial Coverage rule), [[log-2026-Q3]] |
| 2026-08-10 | The Ty proposal went through three separate review rounds before sending, each by a different reviewer. Each round caught something the others missed: one found the deal had no exit for Ty if month 1 failed, one flagged a "fatal" problem that turned out to be false when checked, and the outside research round found an exposure neither of the others saw | Different reviewers catch different problems - one reviewer, however good, only sees one angle. For anything that matters, run more than one independent review, and check the reviewers' claims too: one "fatal" finding was itself wrong | [[tti-role]], [[tti-ty-engagement-proposal-codex-review-2026-08-09]] |
