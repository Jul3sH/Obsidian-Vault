---
name: behaviour-check
description: Raises the relevant card from Julian's documented biases and mental models at the moment it can still change the outcome. Trigger whenever the conversation enters one of these situations - (1) weighing life/career/relationship options or forming a preference; (2) doubt or wobble after a locked/committed decision; (3) starting, scoping or expanding an analysis, register, framework or research task - including any analysis whose answer depends on someone's circumstances, history, assets or intentions; (4) at a send/commit point - finalising a draft, proposal, message or decision; (5) interpreting someone's silence, delay or motives; (6) building or reviewing a financial model, plan or runway figure; (7) reviewing any AI-assisted analysis that supports the answer Julian wanted; (8) designing a new system, process, register or structure, or proposing to change, reroute, merge or restructure an existing one; (9) a reasonable-sounding case forming against doing something uncomfortable or scary, or a sudden convincing reprioritisation away from a feared task; (10) a sudden spike to near-total certainty on a judgement call; (11) deciding whether to hold or continue an asset, project or strategy where already-spent money, time or effort features in the reasoning; (12) choosing what to learn or research; (13) about to state a conclusion as settled, or reading one - especially where the reasoning is sound but a fact behind it was assumed, recalled or single-sourced; (14) deciding how to run a piece of AI work - whether to delegate, how to check it, how much to load into context, or which model to route it to. Also trigger on explicit invoke: "/behaviour-check", "/bias-check", "behaviour check" or "bias check". Do NOT fire on routine system operations (compiling, logging, mirroring, index updates) or quick factual questions.
---

# Behaviour Check

## Purpose

- Julian's documented **biases** live as mm cards indexed in `wiki/performance/biases-index.md`; his **mental models** live as mm cards indexed in `wiki/performance/mental-models-index.md`.
- This skill is the dispatcher that makes both indexes practical: when a conversation enters a situation where a documented bias tends to fire, or where a known method applies, it checks the indexes and raises the matching card at the moment it can still change the outcome.
- Without it, both indexes are reference libraries rather than guardrails. Renamed from `bias-check` on 24 Sep 2026 and widened to cover mental models, after a long session in which two existing mental models were re-derived from scratch and a third system was duplicated because nothing surfaced them.

## The two card types, and how they differ

Both are raised the same way, but they say different things and should be framed differently:

| Type | Index | What the raise means |
|------|-------|----------------------|
| **Bias** | `biases-index.md` | *"Your judgement may be distorted here."* Something about the moment makes a known error likely. |
| **Mental model** | `mental-models-index.md` | *"There is a known method for this."* Prior thinking exists; use it rather than re-deriving. |

## Procedure

1. **Read both indexes.** Open `wiki/performance/biases-index.md` and `wiki/performance/mental-models-index.md` and scan them against the current situation. Read them fresh every time - never from memory - so new cards are picked up automatically.
2. **Match narrowly.** Identify which rows genuinely match what is happening now. Most situations match one or two. Matching four or more means the match is too loose - pick the ones whose wording actually describes the moment.
3. **Check precedence.** Two biases have dedicated skills that own their specific patterns:
   - Reopening a LOCKED decision → hand to `commitment-guard` (run the reopen test); do not duplicate it here.
   - Warming to an option by feel or image → `decision-visualisation-check` owns the both-images intervention.
   If either fires, this skill stays silent on that row.
4. **Raise it briefly.** One short paragraph per card, not a lecture: name it, one line on why this moment matches, the card's one-liner, and the single most relevant guideline. Link the card. Then continue with the work - this is a checkpoint, not a blocker.
5. **Julian overrules freely.** If he says it does not apply, accept it and continue. Log nothing. The skill's job is to make the check happen, not to win it.

## Rules

- **Raise at most two cards per moment**, across both types combined. If more seem to apply, name the strongest match only and mention the indexes exist.
- **Never fire twice on the same card in the same piece of work** unless the situation has materially changed.
- **Biases and mental models compete for the same two slots.** A bias usually outranks a model at a decision point; a model usually outranks a bias when scoping or executing work.
- Read both indexes fresh each time, never from memory.

## Maintenance

- When a row is added to `biases-index.md` or `mental-models-index.md`, check its situation is covered by one of the trigger situations in this skill's description; if not, widen the description in the same operation (this rule is also in `documentation-conventions.md` Part 1).
- Keep this skill and both indexes in lockstep.
- Trigger history: seven situations at creation (19 Sep 2026); widened to twelve on 19 Sep after an artefact-level review found five uncovered bias rows; situation 8 widened 22 Sep to cover changes to existing systems; situations 13 and 14 added 24 Sep with the mental-model widening, covering confidence calibration and AI-work routing decisions.
- `/bias-check` is retained as an invoke alias for muscle memory.
