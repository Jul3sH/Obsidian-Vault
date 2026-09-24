---
type: enabler
project: ai-os
workstream: performance
hours: 4h
created: 2026-09-24
status: done
completed: 2026-09-24
retroactive: true
tags: [ai-os, governance, mental-models, hooks, enabler]
---

# GenAI Governance and Recall Repair

> **Retroactive record, not a ceremony.** This work began as an exempt tax question and
> drifted into producing system artefacts. Per [[mm-admission-qualification]] — *"if work
> drifts mid-session from exempt into producing something substantive, re-run the test at
> the point of drift"* and *"if effort on exempt work turns out worth keeping, write a
> retroactive record for the Time and Token Log — a record, not a ceremony."* No upfront
> definition was run and none was owed.

## What triggered it

A long session on [[uktax-srt-fy26-27]] ran entirely from `/Users/julianhart` rather than
the vault. Because the vault is a **child** of that directory and `CLAUDE.md`/`AGENTS.md`
load from the working directory and its **parents**, none of the governance layer loaded.

**One root cause, four symptoms:** no Deliverable-First check, no Prompt Zero gate, no Time
and Token Log, and incorrect frontmatter on a new deliverable. A fifth surfaced separately:
two existing mental models were re-derived from scratch and one existing system duplicated,
because **biases had a recall mechanism and mental models had none.**

## What was built

| Artefact | What it does |
|---|---|
| SessionStart hook (user settings) | Prompts once if the working directory is outside the vault, and warns that vault rules are not in context |
| Work-handback hook (moved project → user, extended) | Asks for attended minutes **and** a Session Synopsis at handback |
| `~/CLAUDE.md` | Backup pointer to vault rules for when the hook does not fire |
| `## Session Synopsis` | New standard section in all three define-* templates + wiki mirrors, with a defined 1–5 rating scale |
| AGENTS.md rule | Session Synopsis governance: Julian rates first, model comments beneath, three non-overlapping slots for synopsis / workflow-log / card |
| [[mm-facts-first]] | New card — every fact arriving mid-analysis invalidates work already done |
| [[mm-confidence-inheritance]] | New card — a conclusion can be no more certain than its weakest input |
| [[mm-verification]] | Three cryptic principles rewritten in plain English |
| `behaviour-check` | `bias-check` renamed and widened into one dispatcher over both [[biases-index]] and [[mental-models-index]] |

## Completion Criteria

- [x] Root cause identified and closed at the mechanism, not the symptom
- [x] Mental models have a recall path equivalent to biases
- [x] Session Synopsis exists in templates, rules and hook, with a defined scale
- [x] All references, wiki mirrors and sync rows updated
- [x] Ops log records the change, the cause, and what was rejected

## Load-Bearing Assumptions

- **Julian will start future sessions from the vault.** The SessionStart hook prompts but
  does not enforce; `~/CLAUDE.md` is the backup if it fails.
- **One dispatcher will not over-fire.** Two separate ones were rejected as certain to
  double-fire on overlapping triggers; the raise cap of two cards per moment is the control.
  If `behaviour-check` becomes noisy, the cap is the thing to tighten first.

---

## Time and Token Log

| Date | Segment | Who | Tokens / Minutes | Notes |
|------|---------|-----|------------------|-------|
| 2026-09-24 | Diagnosis, design and build | Julian attended | 30 min | Self-reported. Steering, naming decisions, and three catches where the model proposed something the wiki already held |
| 2026-09-24 | Interactive session (main thread) | Machine (session) | unmeasured | Shared with the [[uktax-srt-fy26-27]] run; not separable |

## Session Synopsis

**Rating scale — "would you run it this way again?"** 5 yes, unchanged · 4 yes, with a small
adjustment · 3 mixed, got there but the route was wasteful or needed too much steering ·
2 no, right outcome but wrong method · 1 no, should not have been run this way. It rates the
**method**, not the output.

| Date | Rating (1-5) | Julian's read | Model's comment |
|------|--------------|---------------|-----------------|
| 2026-09-24 | **5** | Would run it this way again. | Worth recording honestly: three times in this session I proposed building something the wiki already had — `mm-token-economics` on delegation and context, `genai-task-workflow-log` for lessons, and `mm-admission-qualification` on retroactive records for drifted work. Each was caught by Julian asking me to check rather than by me checking. That is the same failure the session was convened to fix, occurring during the fix, and it is the strongest argument for `behaviour-check` existing. The build itself was sound; the search discipline was not. |

*Lessons do not go here — the mechanical lesson goes to [[genai-task-workflow-log]]; only a lesson durable across runs earns a card in `wiki/performance/working-with-genai/`.*

## Links
- **Project:** [[../projects/ai-os|AI OS]]
- **Triggered by:** [[uktax-srt-fy26-27]]
- **Cards created:** [[mm-facts-first]], [[mm-confidence-inheritance]]
- **Governs:** [[mm-admission-qualification]] (retroactive record rule)
