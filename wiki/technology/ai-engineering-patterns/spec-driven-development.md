---
type: reference
created: 2026-08-23
updated: 2026-08-23
---

# Spec-Driven Development

> This article is the routing reference for spec-driven development (SDD), one of nine
> patterns in the AI engineering patterns catalog. It exists so that someone deciding how
> to attack a piece of AI-assisted build work can tell quickly whether writing a spec
> first is the right move, or whether it is ceremony that will slow the work down. Read
> the "Reach For It When" section to route; read the rest only if the pattern applies.

## Key Takeaways

- SDD inverts the usual relationship: the written spec is the source of truth and the
  code is the output, rather than the spec being scaffolding thrown away once coding
  starts.
- Reach for it when the diff will be too large to review, not when the task is merely
  long. Size alone is not the trigger; unreviewability is.
- The workflow is the product: constitution, specify, plan, tasks, implement, with a
  human review gate between phases.
- Enforcement stopped being convention-only in 2026. Spec Kit 1.0 (21 Aug 2026) ships
  `/speckit.analyze` and `/speckit.converge`, which check code against the spec and
  append gap tasks until it converges.
- Static specs go stale. Choose a living-spec tool for codebases that move fast, or
  accept that the spec becomes archaeology within weeks.

## What It Is

Spec-driven development treats a structured, written specification as the artefact an AI
coding agent implements against. Rather than prompting an agent to "build the feature"
and reviewing whatever it produces, you write requirements and acceptance criteria
first, decompose them into a plan and then discrete tasks, and only then let the agent
write code. The specification is versioned in the repository alongside the code, usually
as plain Markdown, and review happens at the intent layer where it is cheap rather than
at the diff layer where it is not.

## Reach For It When

Route work here when **any** of these hold:

- **The diff will be unreviewable.** The implementation will span many files or hundreds
  of lines, and you know you will rubber-stamp the pull request rather than read it. The
  spec is what you review instead.
- **You know the outcome but not the precise acceptance criteria.** The problem and
  solution shape are settled; what is missing is a rigorous statement of "done."
  Writing the spec is what forces that statement out of you.
- **Greenfield feature work needing traceability.** Someone will later ask which
  requirement a given piece of code serves, and you want a mapping rather than a guess.
- **A human must approve intent before code exists.** Regulated work, shared codebases,
  or anything where "the agent already built it" would be an expensive thing to unwind.
- **Multi-step implementation with real sequencing.** Tasks have dependencies and doing
  them out of order wastes work.

Do **not** route here when:

- The change is small, local, and reviewable in one sitting. Write it.
- The problem or solution shape itself is still unknown, not just the acceptance
  criteria. Prototype first, spec second.
- The spec would take longer to write than the code would take to write twice.

The routing test in one line: **would you rather review the intent or the diff?** If the
diff, skip this pattern.

## Core Techniques

| Technique | What it does | When to use it |
|---|---|---|
| **Spec-first workflow** | Writes structured requirements and acceptance criteria before any code generation | Default entry point; locks intent before the agent can drift from it |
| **Plan-then-execute with gates** | Decomposes spec into plan, then tasks, then implementation, with human review between phases | Multi-step work where an early wrong turn is expensive to unwind |
| **EARS notation** | Constrains requirements to five templates ("WHEN [trigger] the system SHALL [response]") so criteria are unambiguous enough for an agent to self-check | When acceptance criteria must be machine-checkable, not prose |
| **Cross-artefact consistency check** | Read-only analysis catching conflicts between spec, plan and tasks before implementation starts | Before running the agent, on any spec written over more than one sitting |
| **Convergence loop** | Compares finished code against the spec, appends any gaps as new tasks, repeats until clean | Post-implementation, as the automated substitute for a careful human re-read |
| **Agent hooks / test gates** | Event-driven automations that fire on file save or create, running tests tied to the spec | Enforcing that implementation matches spec continuously rather than at merge |
| **Living vs static specs** | Living specs are refreshed against the code as it changes; static specs are write-once | Living for long-lived codebases, static for one-shot features |
| **Requirement-to-task traceability** | Maps each generated task back to a specific requirement line | Audit, coverage checks, and answering "why does this code exist" later |

## Use Cases & Examples

- **GitHub Spec Kit** - MIT-licensed Python CLI, first released 2 Sep 2025, reached
  v1.0.0 on 21 Aug 2026 (v1.0.1 the same day) with roughly 131k GitHub stars. Runs
  entirely in plain Markdown across 30+ coding agents (Claude Code, Copilot, Cursor,
  Windsurf, Codex CLI) through a nine-command loop: `constitution`, `specify`, `clarify`,
  `plan`, `checklist`, `tasks`, `analyze`, `implement`, `converge`. Only `specify` is
  mandatory before planning. `converge` is append-only: it never edits or deletes code,
  it only adds tasks. The project traces its framing to research by John Lam that GitHub
  built on.
- **Amazon Kiro** - Agentic IDE built on Code OSS (so VS Code settings and Open VSX
  plugins carry over), now also available as a CLI and web surface. Turns a prompt into
  `requirements.md` with EARS-notation acceptance criteria, a `design.md`, and a
  dependency-sequenced `tasks.md`. Runs on Amazon Bedrock, with a model picker that
  changes often (Claude, GPT and open-weight options have all appeared); check Kiro's
  own model changelog rather than trusting a fixed list here. Adds Agent Hooks: event-driven
  automations firing on file save or create. Its specs stay synced with the evolving
  codebase, though the sync is requested rather than automatic (you author code and ask
  Kiro to update the specs).
- **OpenSpec** - Lightweight brownfield-first option, MIT-licensed, shipped as the npm
  package `@fission-ai/openspec` by Fission AI. Proposal-first workflow with delta
  markers, so you can capture the state of an existing system without a full spec
  rewrite. Works with 20+ coding assistants, no API key and no MCP server required.

## Anti-Patterns

- **Spec as a one-time document with no enforcement.** If nothing checks the code against
  the spec, the agent will drift and nobody will notice. Use the convergence or analysis
  commands, or a test gate. This was the standing criticism of Spec Kit through early
  2026 and is the specific thing v1.0 addressed; if your tool has no equivalent, you are
  the enforcement mechanism and you must actually re-read.
- **Static specs on a fast-moving codebase.** Write-once specs rot quickly. Within weeks
  they describe a system that no longer exists, which is worse than no spec because
  people trust them.
- **Speccing an exploration.** If you do not know what you want, the spec encodes a guess
  and the agent implements the guess faithfully. Prototype first.
- **Ceremony inflation.** Running the full nine-command loop on a two-file change costs
  more than it saves. Most of the commands are optional by design; use the ones that earn
  their place.
- **Proprietary lock-in taken accidentally.** Kiro trades portability for tighter
  spec-to-code integration inside AWS. That is a real trade, not simply a downside, but
  it should be a decision rather than a default.
- **Confusing a spec with a prompt.** A spec that reads as instructions to a model rather
  than as a description of the system will not survive being read by a human reviewer,
  which was the whole point.

## Mental Models

[[mm-verification]] - the spec is the check you build when the diff is too large to
inspect; the convergence loop is verification automated.

[[mm-routing]] - "would you rather review the intent or the diff" is a routing question,
and SDD is the answer when the diff fails the checkability bar.

[[mm-steering]] - the constitution and spec are the steering surface, set before the run
rather than corrected during it.

## State of Practice

As of Aug 2026 this remains a young category, but less unsettled than it was six months
ago. Spec Kit hitting 1.0.0 on 21 Aug 2026 with automated drift detection (`analyze` plus
`converge`) is the first credible answer to the "nothing enforces the spec" criticism,
which through early 2026 was the pattern's main weakness. Kiro has moved from an
AWS-specific IDE experiment to a multi-surface product (IDE, CLI, web, GovCloud regions).

Key tools as of Aug 2026: **GitHub Spec Kit** (agent-agnostic, Markdown, greenfield),
**Amazon Kiro** (integrated IDE, EARS, living specs, AWS-bound), **OpenSpec**
(lightweight, brownfield, delta-tracked). No single tool dominates and the enforcement
question is still being answered differently by each, so treat tool choice as reversible
and expect the shape of the pattern to keep moving.

## Links

[[context-engineering]], [[evals]], [[orchestration]], [[observability]]
