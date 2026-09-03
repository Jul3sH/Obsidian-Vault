---
type: reference
created: 2026-08-23
status: active
tags: [working-with-genai, security, mental-models]
---

# MM: Blast Radius

This is the Blast Radius mental model: how much damage a wrong call can do, and
what that fact alone forces you to change about an agent's setup. It was written
to close a gap [[mm-routing]] names in its own Limitations section, that the
routing ladder has no lever for blast radius, so cheap-to-check-and-catastrophic
scores identically to cheap-to-check-and-trivial. Read it before handing an agent
a tool that can delete, spend, send, or publish.

**One-liner:** Assume the wrong call happens, then decide whether you could live
with it.

**Reach for it when:** you are about to give an agent a capability with real-world
reach, or adopt a third party's tool surface.

**Position in the chain:** alongside routing ([[genai-task-workflow]]); blast radius
decides how much reach the result is allowed. It does not choose the architecture,
it bounds it.

## Key Takeaways

- Reversibility, not probability, is the question. A rare irreversible action
  outranks a frequent recoverable one.
- Prevention has no reliable ceiling, so design for containment instead.
- Least privilege is the cheapest control and the most skipped, because the wide
  permission is what made the demo work.
- An approval gate is only a control if the approver actually has enough context
  to refuse.
- Every capability you did not grant is a failure mode you do not have to detect.

## Principles

- **Ask what a wrong call costs before asking how likely it is.** Probability is
  the wrong first question because the mitigations differ: a recoverable error is
  a quality problem and an unrecoverable one is a design problem. The test is
  whether you could undo it cheaply the same day.
- **Prevention is a supplement, containment is the design.** Prompt injection has
  no reliable single fix and the guidance from every serious source is to limit
  what a successful manipulation can reach rather than to try to block every
  attempt. Build as if the filter failed.
- **Least privilege is priced at grant time and paid at incident time.** The wide
  scope is always the convenient one during a build, which is exactly why it
  survives into production. Grant read where write is not required, scope each
  tool to one job, and re-earn anything wider.
- **A gate on an irreversible action is the backstop, not the belt.** Confirmation
  before payments, deletions and outbound sends is what remains when everything
  upstream has failed. It only works if the human is shown what is actually about
  to happen, in terms they can refuse.
- **Someone else's tool surface is your blast radius.** Adopting a third-party
  server or plugin imports its reach and its future versions. A component that was
  safe at review time is not safe at version N+1 by default.

| Wrong call is | Treat it as | Control |
|---|---|---|
| Cheap to undo | A quality problem | Evals, monitoring, fix it later |
| Expensive to undo | A design problem | Narrow the scope, gate the action |
| Impossible to undo | Not the agent's decision | Human approves, or the agent never holds the tool |

## Guidelines

- Enumerate the destructive actions in the tool set first, then design the rest of
  the setup around that short list.
- Prefer removing a capability to guarding it. A tool that is not exposed cannot
  be mis-selected, and needs no gate, no log, and no review.
- Read-only is not automatically safe: an agent that can only read sensitive data
  can still leak it through its output, its logs, or an external model call.
- Pin and re-review anything you did not write, on every version change.
- When the answer is that you cannot bound the damage, that is a verdict, not a
  problem to engineer around: the agent does not get the tool.

## Limitations

The model says nothing about whether the work is worth doing, whether the output
can be checked ([[mm-verification]]), or which architecture runs it
([[mm-routing]]). It also assumes damage is legible: reputational and relational
harm resist the reversibility test, and slow-accumulating harm (a small error
repeated for months) can exceed a single catastrophic one while scoring as
recoverable at each step.

## Detail

[[security-agent-identity]] (the threat model, controls, and identity standards in
full), [[tools-mcp]] (the permissioning and gating layer these judgements land in).
If this model and those articles disagree, the articles win and this file is
corrected.
