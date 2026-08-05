> **Mirror copy.** Source: `~/.claude/skills/prompt-zero/SKILL.md`. Do not edit here - edit the source and re-mirror.

---
name: prompt-zero
description: Interviews Julian so HE writes the grounding brief ("Prompt Zero") in his own words before a significant piece of work starts, then writes it as a `## Prompt Zero` section in the deliverable file. Trigger on "/prompt-zero" or "prompt zero"; and automatically whenever substantive work on a deliverable is about to begin and that deliverable file has no `## Prompt Zero` section (this is the AGENTS.md Deliverable-First Step 2 gate). ALSO trigger mid-work when the work has drifted off the brief - "is this still in scope", "this is getting big", or when the current activity cannot be traced back to the stated Outcome. Do NOT trigger for routine system operations (compiling, logging, mirroring, index updates), quick factual questions, or work Julian has flagged as exploratory.
---

# prompt-zero

**An interviewer, not a writer.** A brief only grounds a model if the words are Julian's. A model-drafted brief grounds the model in its own guesses, which is the exact failure this skill exists to stop. Refusing to draft his answers is the skill, not a limitation of it.

The output is not a prompt to paste. It is a section in the deliverable file that every future session reads before touching the work.

## First: which path?

| Situation | Path |
|---|---|
| Deliverable has no `## Prompt Zero` and work is about to start | **Write** |
| Section exists and the work looks off-brief | **Drift** |
| No deliverable file exists at all | **Stop.** Run `/define-user-story`, `/define-enabler` or `/define-task` first. There is no Prompt Zero without a deliverable. |
| Routine ops, quick question, flagged exploratory | Stand down. Say nothing. |

Find the deliverable by grepping `wiki/deliverables/` for the name or the `jira-key`.

## Write path

**Waiver check first.** Read `size` from the deliverable frontmatter.
- **Size 1** (1-4h, up to half a day): offer the waiver *once* - "Size 1, up to half a day. Waive Prompt Zero?" If waived, write the section as `Waived [date] - size 1, [his one-line reason].` and stop. A waiver is logged, never silent.
- **Size 2+** (5h and above): no waiver. If he pushes back, the answer is that he set this gate himself and the override belongs in the section as a dated line, not in a conversation.

**Then interview. One question at a time. Wait for a real answer before the next.**

| # | Ask | What it stops |
|---|---|---|
| 1 | When this is done, what exists that did not before? One sentence. | Work with no object |
| 2 | Done by when, and what actually happens if it slips? | No deadline, no commitment |
| 3 | Name three things this is NOT. What will you be tempted to expand into? | Scope creep |
| 4 | How will you know it is good enough to stop? Something checkable. | Research loops, perfectionism |
| 5 | Is that level of detail warranted for that outcome? Would half of it still work? | Overanalysis |
| 6 | What are you assuming that, if wrong, makes this work useless? Which is cheapest to test first? | Load-bearing assumptions |
| 7 | Hard boundaries: format, length, audience, budget, tools, what must not change. | Silent constraint discovery at the end |
| 8 | What must I *not* do? Name the specific model behaviour you will regret. | The standing instruction |

Read the eight answers back as the drafted section. He confirms or edits. Then write it into the deliverable file above `## Links`.

### Rules for the interview

- **Never draft an answer for him.** If he says "you write it", refuse once and offer probes or an example from an unrelated domain instead. Ownership is the entire mechanism.
- **A feeling is not an answer.** "I want it to be good" fails Q4. Push once for something checkable, then accept what he gives.
- **Ten minutes, hard cap.** A ceremony that overruns is a ceremony that gets skipped. If he stalls on a question, write "unresolved" and move on rather than losing the whole session.
- **One screen.** If the section runs past ~40 lines it graduates to `wiki/deliverables/[name]-prompt-zero.md` and the section becomes a one-line link.
- Q5 and Q6 are the [[overanalysis-check]] and assumption-audit obligations discharged at the right moment. Do not also run them separately later in the same work.

### Section format

```markdown
## Prompt Zero
*Written [date] by Julian. Read this before working on this deliverable.*

- **Outcome:**
- **Done by:** [date] · **If it slips:**
- **Non-goals:** 1. 2. 3.
- **Good enough when:**
- **Depth warranted:**
- **Assumptions (cheapest test first):**
- **Constraints:**
- **Do not:**
```

## Drift path

Re-read the section, then answer three questions in three lines:

1. Is the current activity traceable to the **Outcome**?
2. Has anything from **Non-goals** crept in?
3. Is **Good enough when** already met?

Output a single verdict line: **IN BRIEF** or **DRIFTED: [which test failed]**. Amending the brief mid-work is allowed, but the amendment is appended and dated, never a silent rewrite of what he originally wrote. A brief that quietly becomes whatever the work turned into grounds nothing.

## Rules

- Minimal friction. Never volunteer analysis, never expand the eight questions, never fire on routine ops.
- Julian is the principal. If he overrides the gate, comply, and write the override into the section as a dated line so the record shows work started ungrounded.
- The one thing to say when he wants to skip it: *the model will fill every gap you leave, and it will fill them with the average of the internet.*

## Related

`wiki/ai-os/skills/prompt-zero/SKILL.md` (mirror) · AGENTS.md § Deliverable-First Working Rule (Step 2 is the gate that fires this) · `/standup` (backstop: catches work started without a brief) · [[systems-register]] SYS-3 · the `feedback-overanalysis-check` and `feedback-assumption-audit` memories.
