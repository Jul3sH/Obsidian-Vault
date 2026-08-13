---
type: reference
created: 2026-08-13
status: active
tags: [working-with-genai, prompts, routing]
---

# Routing Work: Setup Prompts

These are the four setup templates, one per routing verdict, adapted from Nate B
Jones's One-Minute Test. They exist because [[routing-work-to-agents]] tells you
*where* to send a piece of work and stops there, which leaves the part that actually
determines whether the run is any good. Come here after the verdict, copy the
template for your route, and fill it in before starting the work.

## Key Takeaways

- **The run card is the important one.** It forces the check to be named before the
  run rather than discovered after it, which is the whole discipline in
  [[verification-bottleneck]] reduced to one field.
- **Every template ends in something inspectable.** If you cannot fill in the check
  line, you have the wrong verdict, not a missing sentence.
- **Add roles only when the work demands them.** A named small team beats a swarm.

## Chat

For narrow answer work: the source fits in the prompt, the output is an answer rather
than an action, and you can review it directly.

```
I need help with this task:

[PASTE TASK]

Use only this source material:

[PASTE SOURCE]

Return:
1. The answer
2. Assumptions
3. Anything I should verify before using it
```

The third item is what makes this different from just asking. It converts the model's
hidden uncertainty into a short list you can actually act on, and it costs one line.

## One agent

For one clear goal that needs a tool, folder, or app action, and can still be checked
by one person. The shape to hold: **one goal, one loop, a visible result.**

```
Goal: [one sentence describing the finished outcome]
Done state: [the file, message, decision, booking, or update that exists and can be inspected]
Tools: [only the folder, app, calendar, or API needed for the run]
Cap: [one pass, time limit, or stop condition]
Check: [source, rule, test, calendar state, acceptance note, or human review]
```

The rule this encodes is accountability: never give an agent a vague mission, give it
a finish line and a check. Note that *Done state* and *Check* are different fields
doing different jobs. Done state is how the agent knows to stop; Check is how you
know it was right. An agent can hit its done state perfectly and still be wrong.

**If you cannot fill in the Check line, stop.** That is the checkability gate failing
in the one place the tool does not ask about it, per the single-agent warning in
[[routing-work-to-agents]].

## Several agents

For work too large for one pass that splits cleanly across sources or roles, where
the outputs can be checked against citations, tests, or explicit acceptance rules.
Keep the team small and named.

```
Reader: gathers facts from one source area and cites where each claim came from.
Synth: combines the reader notes into the business output.
Reviewer: checks gaps, source support, and acceptance rules.
Gate: a human approves the reviewed output before it ships or changes anything.
```

Add roles only when the work demands them, and name them after the parts that are
genuinely separate. A weekly deck splits into gather, draft, gap-check, format. A
tool-cost audit splits by source: contracts, invoices, usage, renewals.

Two things carry the weight here. **Citations from the Reader** are what make the
Reviewer's job cheap, so they are not optional decoration. And the **Gate is a human**,
which is the one role that cannot be delegated to another agent without the check
collapsing into the thing it is checking.

## By hand

The verdict the tool calls *Don't bother*. It means do the work yourself rather than
build the apparatus.

No template. Write a short checklist and work through it. Two additions worth making:

- **If taste or strategy is the hard part**, ask one trusted person for a second
  read. That is the check, and a person is the only thing that supplies it.
- **If the task starts recurring**, run the routing questions again with the new
  frequency. Recurrence is one of the two economic bars, so a job that failed once
  can legitimately pass on its third appearance.

## When the verdict surprises you

Jones's own advice, and it is good: look for the input that created the surprise.
Usually one of three things has happened.

- The task is **less checkable** than it felt.
- The **frequency or value does not earn the setup**, and you were about to build
  something for a one-off.
- The work needs **one accountable agent rather than a team**, because you wanted
  parallelism rather than genuinely separate minds.
