---
type: reference
created: 2026-08-16
status: active
tags: [the-human-mind, mental-models, rules]
---

# Rule Layering

This is the mental model for classifying any rule, convention, or piece of
knowledge before writing it down, so it gets placed, phrased, and enforced
correctly. It was written when the Principles/Guidelines split in the six-slot
mental-model format needed its own justification, and the justification turned out
to be a general model with three prior sightings in this vault. It is used by
Julian and by any agent whenever a new rule or convention is about to be written,
in the vault or anywhere else.

**One-liner:** Fast learns, slow remembers - and must is not should.

**Reach for it when:** you are about to write down a rule, convention, principle,
or piece of operating knowledge, and need to decide where it lives, how it is
phrased, and how it is enforced.

**Principles:**

- **Knowledge ages at different rates.** Why-shaped claims are grounded in the
  nature of a problem and hold as long as the problem does. How-shaped claims are
  bound to current tools and context, and die when those change. This is pace
  layering (Stewart Brand): healthy systems are layers moving at different speeds,
  where fast layers learn and slow layers remember.
- **Coupling fast to slow makes every refresh reopen settled ground.** When the
  perishable and the durable live in one undifferentiated block, a tooling change
  casts doubt on the understanding next to it, and updating one line means
  re-reading everything. Separated, they rot on different clocks and staleness is
  localised.
- **Authority is a separate axis from durability.** Mandatory (must) versus
  advisory (should) is independent of how fast a rule ages. Conflating the two
  produces advice phrased as law, which teaches readers to ignore "must", and law
  phrased as advice, which gets skipped when it matters.
- **The more mandatory and consequential a rule, the less it can rely on being
  read and obeyed.** An instruction is not a guarantee. Genuinely must-happen
  rules need a mechanism (a gate, a hook, a format that fails visibly), not a
  sentence. This is the steering model's load-bearing rule applied to rulebooks.

The two axes give four cells, each with its own placement and enforcement:

| | **Mandatory (must)** | **Advisory (should)** |
|---|---|---|
| **Durable** (why-shaped) | Hard rules and policies. Live in the always-on layer (AGENTS.md non-negotiables). Phrase as absolutes, state the consequence. | Principles and heuristics. Live in mental models and detail articles. Phrase as invariants, carry the why. |
| **Perishable** (how-shaped) | Current procedure. Live in skills, checklists, hooks. Enforce mechanically where the cost of failure earns it. | Guidelines and current best practice. Live in Guidelines slots and conventions docs. Phrase as advice, expect refresh. |

**Guidelines:**

- Before writing a rule, place it in the 2x2 out loud: does it age, and does it
  bind? The cell tells you where it lives and how it is phrased.
- Keep the rows apart in any artefact: a Principles section and a Guidelines
  section, never one mixed list. Refresh the fast row without reopening the slow
  one.
- Date anything in the perishable row that claims to be current. An undated
  how-claim reads as current forever (the Status Claims rule is this guideline
  applied to documents about themselves).
- For the mandatory-perishable cell, prefer enforcement to prose where failure is
  costly: a hook over an instruction, a required section over a reminder, a
  format whose violation is visible.
- When a rule keeps being violated, check its cell before strengthening its
  wording: advice phrased as law and law enforced as advice are placement errors,
  not discipline errors.

**Limitations:** more layers means more boundaries to police, and a small artefact
can be genuinely monolithic - forcing four cells onto a five-line note is
bureaucracy. The 2x2 classifies rules about *doing*; it says nothing about whether
the rule is right. And cell membership can shift: a durable principle can be
demoted by a paradigm change, so the slow row is slow, not immortal.

**Detail:** [[documentation-conventions|documentation-conventions]] (the
Principles/Guidelines split in the mental-model format is this model applied);
[[genai-mental-models]] (the steering model's "an instruction is not a guarantee"
is the enforcement principle in its home domain); Stewart Brand, *The Clock of the
Long Now*, for pace layering itself.

## Key Takeaways

- Classify before writing: durability (does it age?) x authority (does it bind?).
- Separate the rows so the perishable and the durable rot on different clocks.
- Phrase to the column: absolutes with consequences, or advice with reasons.
- Must-happen rules need mechanisms, not sentences.
