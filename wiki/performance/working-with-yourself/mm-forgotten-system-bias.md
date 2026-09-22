---
type: reference
created: 2026-09-22
status: active
tags: [working-with-yourself, cognitive-bias, adhd, mental-models]
---

# MM: Forgotten-System Bias

This card names the bias of proposing changes to a working system because the
system has dropped out of salience, not because it has failed. Split out of
[[mm-build-dont-adopt-bias]] on 22 Sep 2026 after two same-week instances showed
a distinct mechanism - that card's driver is the reward of designing; this one's
driver is forgetting. Julian's own diagnosis, same day: "I often suggest system
changes because I have forgotten the current system due to lack of clarity and
usage, rather than a desire to create new systems." Read it whenever a change,
rerouting, merge, or restructure of an existing system, process, or convention
is being proposed.

**One-liner:** A redesign impulse toward a working system is usually forgetting,
not failure - name the failure before touching the design.

**Reach for it when:** proposing (or being asked to help with) a change to an
existing system, process, folder structure, or convention.

## Key Takeaways

- The impulse presents as a reasonable process-improvement question, which is
  why it survives the scrutiny that would catch idle tinkering.
- The tell is the absence of a named failure. Both documented instances
  dissolved within minutes of reading the original design doc.
- The root cause is visibility and usage, not judgement: a system that is not
  seen or exercised stops existing mentally (ADHD-amplified out-of-sight,
  out-of-mind).
- When the answer is "forgotten", the fix is a visibility fix - overview doc,
  register row, hook - never a redesign.

## Principles

- **Forgetting feels like insight.** The re-derived "better" design feels fresh
  precisely because the original reasoning is no longer in view.
- **A system with no named failure is not a redesign candidate.** "I'd do it
  differently today" is not a failure.
- **Salience is a maintenance property.** Systems stay remembered by being used,
  reviewed, and surfaced (registers, overviews, hooks), not by having been well
  designed once.

## Guidelines

- Before engaging any restructure proposal, read the system's design doc (e.g.
  [[taxonomy]], [[prioritization-framework]], the relevant overview) and its
  [[systems-register]] row, then ask out loud: **failing, or forgotten?**
- Require a named, observed failure before any design work starts; an
  executional gap (a sync not run, a step skipped) is fixed by running the
  process, not redesigning it.
- If forgotten: improve visibility (write the missing overview, add the register
  row, wire the hook) and leave the design alone.
- Agent backstop: the `feedback-taxonomy-before-filing` memory instructs Claude
  to run this check before engaging with any structural change.

## Limitations

- Not a ban on redesign. A named, observed failure legitimately reopens design -
  the 28 Aug 2026 prioritisation fix was exactly that: evidenced failure
  (sprints breaking on variable work), then redesign.
- Sibling: [[mm-build-dont-adopt-bias]] covers the neighbouring failure,
  building *new* systems for the design reward and abandoning them. This card
  fires on *changing existing* systems.

## Detail

Self-contained pending a detail article; the evidence table below is the
primary record. Row in [[biases-index]]. Countermeasure infrastructure:
[[systems-register]] and whole-system overviews such as [[mental-models-system]].

## Evidence

| Date | Event | Lesson in action | Source |
|------|-------|-------------------|--------|
| 2026-09-22 | While homing the new [[mental-models-system]] overview, nearly collapsed the service-design/system-design taxonomy into a single folder. The trigger was vocabulary salience (recent conversations about "systems" made the all-encompassing usage feel right), not any failure of the taxonomy; neither Julian nor the agent had re-read [[taxonomy]] (May 2026), which already answered the filing question, including a when-in-doubt default. Reading it ended the restructure in minutes | The redesign pull fired at a moment of forgetting, not at a point of failure: the adopted system was working, it had simply dropped out of salience. Read the estate (taxonomy, register, indexes) before restructuring anything | Live session, 22 Sep 2026; paired memory `feedback-taxonomy-before-filing` |
| 2026-09-22 | Second impulse in three days, caught same day: proposed rerouting funnel tech-debt items from the Portfolio backlog to the BAU Kanban. The 28 Aug Project Classes design in [[prioritization-framework]] (signed off by Julian) already answered it - his own classifying test routes discretionary tech debt through the funnel, and BAU is defined as obliged-work-only. The only real defect was executional: eight funnel rows awaiting a `/jira-sync`. The counter worked live: failing-or-forgotten was asked before any restructure work started, and the answer was "forgotten" | The impulse recurs whenever a system's design rationale has dropped out of salience, and it presents as a process-improvement question. The counter is cheap and now twice-proven: read the design doc first, then require a named failure | Live session, 22 Sep 2026 |
