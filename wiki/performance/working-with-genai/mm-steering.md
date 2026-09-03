---
type: reference
created: 2026-08-16
status: active
tags: [working-with-genai, steering, mental-models]
---

# MM: Steering

This is the Steering mental model: how an agent is made to behave once
[[mm-routing]] has chosen the architecture. It carries both the model and its
detail, because the mechanism layer comes from Anthropic's
[steering guide](https://claude.com/blog/steering-claude-code-skills-hooks-rules-subagents-and-more)
rather than a separate wiki article. Read it when configuring agent behaviour.
Anthropic's own term for this territory is **steering**.

**One-liner:** An instruction is not a guarantee.

**Reach for it when:** routing has chosen the architecture and you are configuring
how the agent, or fleet of agents, behaves.

**Position in the chain:** fourth. Work types classifies, verification permits,
routing decides the architecture, steering configures it. Full chain:
[[genai-task-workflow]].

## Key Takeaways

- An instruction is not a guarantee: must-happen means a mechanism, not a sentence.
- Match the mechanism to what you are installing: fact, procedure, constraint,
  must-happen, isolated task, identity.
- Always-loaded costs context always; on-demand is free until triggered.
- Persistence is a third axis: cost and authority say nothing about whether an
  instruction is still there after a compaction.
- Steering shapes behaviour, not capability, and it never substitutes for
  verification.

## Principles

- **An instruction is not a guarantee.** An LLM follows instructions
  probabilistically. Anthropic's guide names the failure conditions: under
  pressure, in a long session, in an ambiguous situation, or on a prompt injection
  in a file read during the task. So for anything that absolutely must or must not
  happen, an instruction is the wrong tool and a mechanism is the right one:
  *"The model choosing to run a formatter is different from the formatter running
  automatically."* This is the load-bearing principle; [[mm-rule-layering]] generalises
  it to all rulebooks.
- **Every mechanism trades context cost against authority.** Always-loaded
  instructions (a root instruction file, an output style) carry the most weight and
  cost context on every turn. On-demand mechanisms (skills, path-scoped rules,
  subagents) cost nothing until triggered. Facts earn permanent residence;
  procedures and constraints should load on demand.
- **Persistence is a third axis, independent of the other two.** Cost and authority
  say nothing about whether an instruction is still in context in an hour. Three
  survival mechanisms exist: the harness **re-supplies** it (root instruction files,
  output styles, rebuilt after every compaction), it sits in the **transcript** and
  degrades when compacted (your prompts, skill bodies, tool results), or it is
  **re-triggered** by its own event (hooks, path-scoped rules). The axes do not move
  together: a mechanism can be cheap and low-authority yet permanent, or expensive
  and high-authority yet fragile. A long skill body carries real weight the moment
  it loads and can be gone after the next compaction. Note the vocabulary clash:
  this is *context* persistence, measured in turns, not the knowledge-ageing
  durability of [[mm-rule-layering]], measured in months.
- **Steering shapes behaviour, not capability.** Which model runs and how hard it
  works are separate dials that no steering mechanism can reach. A perfectly
  steered weak configuration is still weak.
- **Subagents buy isolation, not just parallelism.** A subagent's instructions
  never enter the parent conversation, and only its final message returns. That is
  routing's independence requirement implemented as a mechanism: the two are the
  same decision seen from opposite ends. And isolation cuts both ways: the child
  inherits neither your context nor your steering.
- **Dynamic workflows are subagents scaled up.** Tens to hundreds of agents,
  orchestrated with the plan held in script variables rather than in context. A
  width dial inside one routing verdict, not a new verdict, and the verification
  gate binds hardest at that width because output multiplies while attention does
  not.

## Guidelines

⚠ As of 16 Aug 2026, current for Claude Code. This is the fast-ageing row of the
model ([[mm-rule-layering]]): the principles above outlive this table, so on a harness
change, refresh here without reopening them.

Match the mechanism to what you are installing:

| What you are installing | Mechanism | Persistence |
|---|---|---|
| A **fact** that must always be in context | `CLAUDE.md` / `AGENTS.md`, root or subdirectory | Root: re-supplied. Subdirectory: re-triggered, and lost until that directory is touched again |
| A **procedure**, run the same way each time | Skill | Transcript-resident: the body degrades on compaction |
| A **constraint** that binds only certain paths | Rule, path-scoped | Re-triggered by the path |
| Something that **must happen**, every time, without judgement | Hook | Re-triggered by its event |
| An **isolated side task** whose middle you do not want to see | Subagent | Separate context; parent persistence does not apply |
| A **different identity**, not the coding assistant at all | Output style (see caveat below) | Re-supplied |

- Keep procedures out of the always-loaded file: a 30-line procedure in `CLAUDE.md`
  belongs in a skill. The always-loaded file is for facts held all the time.
- Scope rules with paths so they stay out of context during unrelated work.
- "Every time X, always do Y" written as an instruction is the anti-pattern: if it
  must happen reliably, it is a hook.
- Personal preferences go in user-level files, team or project conventions in
  project-level files.
- Output styles replace the default identity: unless `keep-coding-instructions` is
  set, the built-in engineering instructions are removed. Reserve for genuine role
  changes, not for preferences like brevity, which belong in the instruction layer.
- One deliverable's style or scope belongs in the deliverable's own brief (the
  `## Prompt Zero` section), a recurring format in a skill, a place-bound register
  in a path-scoped rule.
- Steer a subagent through its own definition, not through the parent
  conversation: subagents run their own system prompts, so the main session's
  instructions and output style do not follow them.
- If a rule must hold across a whole long session, check its persistence tier and
  not just its authority. Worked example: the public `i-have-adhd` skill puts its
  ruleset in a skill body (transcript-resident), then ships a `SessionStart` hook
  matching `compact` to re-inject it. That buys re-triggered persistence for
  content that is fragile by nature. An always-loaded instruction file would have
  needed no hook at all.

## Limitations

- **Steering cannot reach the capability dials.** Model choice and effort are set
  outside every steering mechanism.
- **The mechanism layer is harness-specific and perishable.** The table above is
  Claude Code's, as dated; the principles are not tied to it.
- **Only the re-supplied tier is compaction-proof, and only textually.** The
  instruction survives intact, but the conversation it was written to govern is
  exactly what got compressed, so behaviour can still drift after a compaction
  while every rule is still in context.
- **Steering does not verify.** A well-steered agent still produces unverified
  output. In the chain, verification decides what is possible and routing decides
  the architecture before steering configures it: good steering is not evidence of
  good work.

## Detail

Source: [Steering Claude Code](https://claude.com/blog/steering-claude-code-skills-hooks-rules-subagents-and-more)
(Anthropic). Companions: [[mm-rule-layering]] (the enforcement principle
generalised to rulebooks), [[mm-routing]] and [[routing-work-to-agents]] (the
decision upstream of this one).
