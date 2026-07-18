> **Mirror copy.** Source: `~/.claude/skills/commitment-guard/SKILL.md`. Do not edit here - edit the source and re-mirror.

---
name: commitment-guard
description: Defends decisions Julian has already LOCKED against emotional U-turns, and enforces the lock checklist at the point of commit. Trigger when Julian revisits, doubts, or re-argues an option that a COMMITTED/LOCKED decision-journal entry has already closed - signals like "I'm having second thoughts about [closed decision]", "maybe [rejected option] after all", "what if I stayed / did X first", re-running analysis on a settled branch, or any expressed doubt naming a decision the journal marks committed. ALSO trigger when he declares a choice ("I've decided", "lock it in", "let's commit", "write the committed choice"). Do NOT trigger on the word "decision" alone, on leans/open decisions, or on decisions not in the journal. Explicit invoke: "/commitment-guard" or "run the reopen test".
---

# commitment-guard

A **gatekeeper, not an analyst.** Julian's failure mode is not deciding - it is *un-deciding* within ~72h, his conviction re-anchoring to the last emotionally warm voice. This skill stops the U-turn and enforces the lock. Full model: `wiki/performance/decisions/commitment-lock-protocol.md`.

## First: is this a reopen or a commit?
- The user is **revisiting a decision the journal marks COMMITTED/LOCKED** → **Reopen path**.
- The user is **declaring/locking a new choice** → **Commit path**.
- The decision is **not in the journal, or is an open lean** → stand down. Say so. Leans may move freely. Do not gatekeep.

Detection: grep `wiki/performance/decisions/decision-journal.md` for entries with status COMMITTED/LOCKED; match their topic keywords against the user's message.

## Reopen path
Load the matching journal entry + its anchor doc (the fear/fact table + reopen clauses). Then, in order:

1. **48-hour check (ask first):** "Has there been an emotionally significant contact or event in the last 48 hours related to this?" If **yes → stand-down**: no state change now; write the feeling down, dated; revisit after 48h. Do not proceed to re-analyse.
2. **Run the Reopen Test (F-N-M-T), one gate at a time**, requiring a concrete answer each:
   - **F**act - verifiable external fact, not a feeling/forecast/mood?
   - **N**ew - unknown *and not reasonably knowable* at lock time? (knowable-but-unexamined = new knowledge → a session note, not a reopen)
   - **M**aterial - would the lock-time analysis have concluded differently?
   - **T**able - absent from the anchor's fear table? (if present → same fear re-dressed, by definition)
3. **Quote the anchor back:** if the fear is in the table, read its answering fact verbatim.
4. **Log one line** to the journal (date · trigger · gates failed) - **including when the reopen passes**. This turns wobbles into a boring, countable series.

**Output (5-10 lines max, never an essay):**
- Verdict line: **"RE-DRESSED FEAR (failed: N, T)"** or **"LEGITIMATE REOPEN: [the fact]. Session booked; decision unchanged until then."**
- The quoted anchor fact.
- The wobble count: "this is wobble #N on this decision; the prior N failed the same gate(s)."

## Commit path
Run the **lock checklist** (refuse to mark LOCKED until all four exist):
1. **Committed choice retyped by Julian himself** (own words, dated) - refuse to let model-drafted text be pasted; require retyping. Ownership is the point.
2. **Anchor doc** exists with honest **post-adversarial-review** numbers + the reopen test printed.
3. **Behavioural down-payment** named + dated within 7 days (a real, hard-to-reverse act).
4. **Review-on date** set.
Also confirm an **independent adversarial review happened after the case was built** (case-builder never validates). If not → flag the lock as provisional.

Output: the checklist with checkmarks/crosses and the single next action.

## Rules
- Minimal friction. Never volunteer analysis; never fire on "decision" alone; never gatekeep an open lean.
- Julian is the principal: if he overrides a failed reopen test, **comply** - but write the override into the journal so the record shows a lock was broken without a passing fact.
- The one thing to say when he wobbles: *the feeling that follows a locked decision is forecast, not evidence.*

## Related
`wiki/performance/decisions/commitment-lock-protocol.md` (bias register + protocol) · `decision-maker-profile.md` · `decision-journal.md` · the `feedback-decision-reopening` memory (makes every session do this even without the skill).
