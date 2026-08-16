---
type: reference
created: 2026-08-16
status: active
tags: [working-with-genai, verification]
---

# Verification Tactics

This is the practical companion to [[verification-bottleneck]]: what to actually do
to shrink the generation-verification gap on real work. It was written when the
question moved from why verification is the constraint to how to scale the amount of
AI work one person can own. It is read before commissioning AI work at any volume;
every tactic in it serves one test, keeping your attention **sub-linear to the
output volume**.

## Key Takeaways

- **Evals scale the checking; deterministic design removes the need for it. Do the
  removing first.** Evals are the middle layer, not the main tool.
- **The gap you pay is the residual** left for human judgement after the cheaper
  layers catch what they can. Building those layers is the work, not overhead on it.
- **A check is built before the run, or it is not a check.** Named after the fact,
  it is an intention, and intentions degrade under exactly the volume that creates
  the need for them.
- **Some work has no gap to shrink.** Where judging is the work, no tactic here
  helps. Route it by hand.

## The four layers, in leverage order

| # | Layer | What it buys | What it costs |
|---|---|---|---|
| 1 | **Deterministic design** | Criteria verified free, forever, never landing on you | Thought at design time |
| 2 | **Check named before the run** | Forces layers 1 and 4 to exist before commissioning | One sentence |
| 3 | **Independent evals** | Semantic checking at volume | Setup, plus independence discipline |
| 4 | **Sub-linear judgement** | Your residual stays flat as volume grows | Output structured for the reader |

## 1. Move criteria into deterministic form

Every criterion made assertable is checked mechanically and never consumes
attention again. The test for membership: could an agent, a script, or a grep check
this with no judgement at all?

- **Citations that resolve.** Require a clickable source for every claim. A link
  works or it does not.
- **Reconciliation to a canonical block.** One authoritative table of numbers; every
  other mention checked against it. Already a steering rule (`AGENTS.md`, Single
  Source of Truth for Project Numbers).
- **Staleness that flags itself.** Status claims carry dates, so an old claim reads
  as old with no memory required. Already a steering rule (`AGENTS.md`, Status
  Claims Must Carry a Date).
- **Formats that validate.** A required section present or absent, frontmatter that
  parses, a table with the agreed columns, a total that sums.

Both existing steering rules were written in response to lived failures, before the
verification vocabulary arrived: the instinct under fire was to make wrongness
self-flagging, not to add reviewers. That instinct is this layer.

## 2. Name the check before the run

The `Check:` field on the one-agent run card in [[routing-work-prompts]] is this
tactic in operational form. One sentence, written before the work is commissioned,
naming which of the three forms will verify it.

- If the line cannot be filled in, the work should not be commissioned at that
  volume. That is [[routing-work-to-agents]]'s gate firing early, which is where it
  is cheap.
- The discipline this buys: layers 1 and 4 get designed at commission time, when
  changing the output's shape is free, rather than discovered at review time, when
  it is not.

## 3. Evals, with independence, or they are worse than nothing

An eval sharing the worker's model, context and blind spot certifies the error
instead of catching it, and adds false confidence while doing so. Independence comes
three ways; at least one is required for the eval to count.

- **Different model.** The multi-model pattern
  ([[ai-os/skills/llm-council/SKILL|llm-council]] is the vault's working example).
- **Different source information.** The eval reads the sources, not the worker's
  summary of them. Free, and the one people skip.
- **Ground truth.** A known-right answer, spec, or historical outcome to compare
  against.

The cheap practical form: **you write acceptance criteria before generation, a
different model grades the output against them.** The criteria cost minutes and do
double duty as the brief.

## 4. Keep your own judgement sub-linear

The residual that reaches you should grow slower than the volume. Designed, not
resolved upon.

- **Sample, do not sweep.** Verify three citations of thirty and trust the pattern;
  a failed sample triggers the full check, not the other way round.
- **Structure output so a wrong answer looks wrong.** The risk register's bold
  scenario sentences are the vault example: a wrong claim in plain speakable form is
  visibly wrong, the same claim buried in a paragraph is not.
- **Push detail downstream.** What you read stays one screen; depth lives in files
  you consult on demand. The length rule is a verification tactic wearing a style
  rule's clothes.

## The counterweight: work with no gap to shrink

Taste work - defined in [[verification-bottleneck]]: no external criterion to check
against, so the judgement is the output - fails the comparative test by definition:
judging which of thirty options is best costs about what generating them costs, so
no volume of generation and no eval layer helps. Product naming, strategic framing,
register and tone. Route it to chat or by hand ([[routing-work-to-agents]]), and if
a second read is needed, a trusted person is the check.

## Relation to the rest of the folder

[[verification-bottleneck]] is why this matters and carries the three forms
canonically. [[routing-work-to-agents]] consumes the check as its gate.
[[mm-verification]] holds the compressed model, and [[mm-routing]] the decision it
feeds.
