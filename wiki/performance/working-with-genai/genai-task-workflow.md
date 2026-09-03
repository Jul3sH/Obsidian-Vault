---
type: reference
created: 2026-09-03
status: active
tags: [working-with-genai, workflow, routing, mental-models]
---

# GenAI Task Workflow

This is the end-to-end workflow for running any piece of work through AI: four
questions, asked in order, each answered by its own mental model. It was created
(3 Sep 2026) because the chain existed only as one-line cross-references inside
the individual models - the machine could piece it together, but a human needs
the whole picture on one page. Read it when starting any substantive piece of AI
work; go down into each model only when its step is the one you are on.

## The chain

**Step 0 - admission (before the chain runs):** decide how much ceremony the work
deserves. Machine-executed, low-blast-radius, single-box work takes the AGENTS.md
Admission Fast Lane (one sitting, admission through execution); everything else
takes the full define ceremony. Admission is Taste work: minimise it, batch it,
never split it across sessions.


| Step | Model | Question it answers | What it hands to the next step |
|---|---|---|---|
| 1 | [[mm-work-types]] | What kind of work is this? | The work type, carrying its default check form |
| 2 | [[mm-verification]] | Does that check actually hold here - cheaper than producing, independent, named before the run? | A check you can afford, or a veto |
| 3 | [[mm-routing]] | Chat, one agent, several agents, or by hand? | The architecture |
| 4 | [[mm-steering]] | How is each agent made to behave once placed? | The configured run |

## How the steps link

- **Admission is Taste work: minimise and batch it.** Only Julian can judge what
  the work is and why, so step 0 spends his judgement deliberately: small, one
  sitting, execution immediately after. Never split admission from execution
  across sessions. (Evidence: the 3 Sep D2 entry in [[genai-task-workflow-log]].)
- **The type carries the check.** Classifying the work (step 1) is a seconds-long
  read, and the type's whole value is that it tells you how the output will be
  checked before anything runs.
- **Verification holds the veto.** Step 2 tests whether the type's default check
  survives this instance. A check that costs as much as the work itself, or an
  eval with no independence, drops the work to chat or by hand regardless of what
  routing might have preferred. This is [[mm-routing]]'s "never split what you
  cannot check" rule, fed from upstream.
- **Routing decides the architecture, including its width.** Several agents is a
  width dial, not a setting - three named roles at one end, a workflow over
  hundreds at the other. The checkability bar rises with the width.
- **The routing/steering boundary:** how many minds and how they relate to each
  other = routing. How each mind is made to behave once placed = steering.

## The feedback loop

Every routed run gets a row in [[genai-task-workflow-log]] - work type, check form, verdict,
outcome, lesson. Before routing new work, the log is checked for similar past
runs; what it accumulates feeds back into these models. Evidence compounds
instead of scattering.

## Companions outside the chain

[[mm-blast-radius]] (assume the wrong call happens - reach for it alongside
routing), [[mm-token-economics]] (what the run costs), [[mm-model-adaptation]]
(after steering, when behaviour still misses).
