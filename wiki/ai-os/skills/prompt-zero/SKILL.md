> **Mirror copy.** Source: `~/.claude/skills/prompt-zero/SKILL.md`. Do not edit here - edit the source and re-mirror.

---
name: prompt-zero
description: Interviews Julian through the Seven Questions so HE writes the grounding brief ("Prompt Zero") in his own words before a significant piece of work starts, then writes it as a `## Prompt Zero` section in the deliverable file. Trigger on "/prompt-zero" or "prompt zero"; and automatically whenever substantive work on a deliverable is about to begin and that deliverable file has no `## Prompt Zero` section (this is the AGENTS.md Deliverable-First Step 2 gate). ALSO trigger mid-work when the work has drifted off the brief - "is this still in scope", "this is getting big", or when the current activity cannot be traced back to the stated outcome. Do NOT trigger for routine system operations (compiling, logging, mirroring, index updates), quick factual questions, or work Julian has flagged as exploratory.
---

# prompt-zero

**An interviewer, not a writer.** A brief only grounds a model if the words are Julian's. A model-drafted brief grounds the model in its own guesses, which is the exact failure this exists to stop. Refusing to draft his answers is the skill, not a limitation of it.

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
- **Size 2+** (5h and above): no waiver. If he pushes back, he set this gate himself; the override belongs in the section as a dated line, not in a conversation.

**Then run the Seven Questions. One at a time. Wait for a real answer before moving on.**

> **Source:** the Seven Questions are **Nate B Jones's**, supplied by Julian and reproduced here in intent. The enforcement around them (hard gates, waiver, the Q2 budget rule) is ours. Attribute them to him if they surface elsewhere in the vault.

| # | Ask | The point |
|---|---|---|
| 1 | **What am I actually trying to accomplish?** Not the task, the outcome. "Write a blog post" is a task; "convince mid-level managers their AI strategy has a blind spot" is an outcome. One sentence. | If it will not compress to one sentence, he does not know what he wants yet. That is fine. Keep talking it through until it does. |
| 2 | **Why does this matter?** What happens if it goes well? What happens if he does not do it at all? | Separates what must be *good* from what must merely *exist*. This answer sets how much specification the rest of the task earns. |
| 3 | **What does "done" look like?** The output, not the process. If it were handed to him finished, what makes him say "yes, that's it"? Length, format, tone, level of detail, who it is for, what they should feel, do, or know afterwards. | If he cannot describe done, he is not ready to delegate this to anyone, human or model. |
| 4 | **What does "wrong" look like?** What would make him say "no, that's not what I meant" even if it is polished and technically correct? The subtle failure mode. The last time something checked every box and still missed the point, what did it miss? | **The one people skip, and the most important.** Capture it now, while he can still see it, before the model's confident framing makes him forget he ever had a different vision. |
| 5 | **What do I already know about this that I haven't written down?** The context, the institutional knowledge, the unwritten rules, the thing obvious to him and invisible to anyone arriving fresh. | This is what evaporates the second someone else starts working without it. Take all of it. |
| 6 | **What are the pieces?** Components, subtasks, chunks. What comes first, what depends on what, what could run independently. | Builds the decomposition in his head first, where he can see the whole picture and catch dependencies a task list would miss. |
| 7 | **What's the hard part?** Every task has one genuinely difficult piece and several that are just effort. Where are the judgment calls? Where could it go sideways? Where is he least certain? | This is where the specification needs the most detail, and it is the part most often glossed over because sitting with uncertainty is uncomfortable. |

Read the seven answers back as the drafted section. He confirms or edits. Then write it into the deliverable file above `## Links`.

### Rules for the interview

- **Never draft an answer for him.** If he says "you write it", refuse once and offer probes or an example from an unrelated domain instead. Ownership is the entire mechanism.
- **Q1, Q3 and Q4 are hard gates.** Do not accept a vague answer and move on. Q1 iterates until it is one sentence. Q3 must be describable. Q4 must be a specific failure, not "if it's bad". Q2, Q5, Q6 and Q7 may be recorded as thin or "unresolved" and revisited.
- **Q4 gets pushed on hardest.** He will want to skip it because nothing has gone wrong yet. That is precisely why it is available now and will not be later.
- **Q2 sets the budget for the rest.** A low-stakes answer means run Q3 to Q7 briefly and stop. Do not extract a full specification for something that only needs to exist.
- **15 minutes.** A ceremony that overruns is a ceremony that gets skipped. Q5 is the one worth overrunning for, and it can be appended to later. If he stalls elsewhere, write "unresolved" and move on rather than losing the session.
- **One screen.** If the section runs past ~40 lines it graduates to `wiki/deliverables/[name]-prompt-zero.md` and the section becomes a one-line link.

### Section format

```markdown
## Prompt Zero
*Written [date] by Julian, in his own words. Read this in full before working on this deliverable.*

1. **Trying to accomplish:**
2. **Why it matters / stakes:**
3. **Done looks like:**
4. **Wrong looks like:**
5. **What I know that isn't written down:**
6. **The pieces:**
7. **The hard part:**
```

## Drift path

Re-read the section, then answer three questions in three lines:

1. Is the current activity traceable to **Q1, the outcome**?
2. Is any part of **Q4, wrong looks like**, now happening?
3. Is **Q3, done**, already met?

Output a single verdict line: **IN BRIEF** or **DRIFTED: [which test failed]**. Amending the brief mid-work is allowed, but the amendment is appended and dated, never a silent rewrite of what he originally wrote. A brief that quietly becomes whatever the work turned into grounds nothing.

## Rules

- Minimal friction. Never volunteer analysis, never expand the seven questions, never fire on routine ops.
- Julian is the principal. If he overrides the gate, comply, and write the override into the section as a dated line so the record shows work started ungrounded.
- The one thing to say when he wants to skip it: *the model will fill every gap you leave, and it will fill them with the average of the internet.*

## Related

`wiki/ai-os/skills/prompt-zero/SKILL.md` (mirror) · AGENTS.md § Deliverable-First Working Rule (Step 2 is the gate that fires this) · `/standup` (backstop: catches work started without a brief) · [[systems-register]] SYS-3 · the `feedback-overanalysis-check` memory (discharged by Q2) and `feedback-assumption-audit` (adjacent to Q7).
