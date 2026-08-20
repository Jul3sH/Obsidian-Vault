---
type: task
project: ai-engineering-patterns
workstream: performance
hours: 2h
created: 2026-08-20
status: queued
jira-key:
value-rationale:
---

# AI Engineering Pattern Articles

> **Purpose block.** This is the definition file for Deliverable 1 of the [[ai-engineering-patterns|AI Engineering Patterns]] Project: 8 pattern-area articles plus supporting mental models, written into `wiki/technology/ai-engineering-patterns/`. It was created on 20 Aug 2026 through the `/define-task` interview so the work enters the backlog scoped, sized, and payoff-tested before execution starts. It is read at execution time (the Execution Approach section is the run plan) and at sign-off (the Completion Criteria are the checklist).

## Prompt Zero
**Waived 20 Aug 2026** (size 1 waiver, permitted at 1-4h). Reason: the grounding brief already exists in Julian's own words from the 19-20 Aug definition session — the payoff, good-enough condition, execution shape, and corrected assumptions below were all stated or approved by him during the `/define-task` interview, so a separate Prompt Zero interview would duplicate them.

## Task Description
Produce 8 market-aligned AI engineering pattern articles (with new mental models where warranted) in a new `wiki/technology/ai-engineering-patterns/` folder, giving Julian a wiki reference for choosing the best engineering pattern for any project or task.

## Completion Criteria
1. 8 pattern-area files exist in `wiki/technology/ai-engineering-patterns/` (context engineering, memory, tools/MCP, evals, orchestration/workflow architectures, spec-driven development, security including agent identity, plus one more landed during drafting), each linked to relevant mental models with use cases and examples, and listed in a new `_index.md` (navigation only, per wiki convention; the collection of 8 files is the catalog, there is no separate catalog file)
2. New `mm-*` files in six-slot format exist for pattern areas that warrant one, and are listed in [[mental-models-index]]
3. A Codex verification pass is complete on each of the 8 files
4. Julian has signed off

## Definition of Done
The `wiki/technology/ai-engineering-patterns/` folder exists containing an `_index.md` and 8 pattern articles, each researched from current (post-2025) practitioner sources, cross-linked to the mental-model catalog, and individually verified by Codex. Any new mental models are filed in the six-slot format and indexed. Julian has read the set and signed off, and can route a task to an engineering pattern by consulting the folder.

## Execution Approach
Agreed 19-20 Aug 2026 in the definition session. Shape: **fan-out and synthesize** dynamic workflow, with one inline adversarial check per branch (not a panel review of the final result). Fable (session model) coordinates.

- Pipeline over the 8 pattern areas. Each branch: **Sonnet research agent** (low reasoning effort, tight brief: what "market-aligned" means, post-2025 practitioner sources preferred, fixed output shape) → **Opus draft agent** (high reasoning effort: synthesises the brief into the article, links mental models) → **one Codex adversarial check** of that file, invoked by the workflow agent calling the Codex companion runtime directly via Bash (the `/codex:adversarial-review` slash command is user-invoke-only, but the underlying script is callable).
- Final **Opus synthesis stage** (barrier, needs all 8): writes `_index.md`, decides which new `mm-*` models are warranted (cross-area view avoids duplicates), adds cross-links.
- Julian reviews and signs off after the run (workflows take no mid-run input).
- Codex usage bills to the ChatGPT subscription (auth mode: chatgpt, no API key), so the cost risk is throttling, not money. A Codex failure marks that file "unverified, retry later" rather than killing the branch.
- Expected agent count (~25) exceeds the session's medium workflow size guideline; the task genuinely calls for it.

## Load-Bearing Assumptions
1. **The 8 areas are the right market-aligned cut.** If wrong, the reference misroutes tasks. Cheap test: the research stage's first outputs will expose a missing or mislabelled major area; review them before drafting proceeds.
2. **Sonnet research agents at execution time provide sufficient grounding; Julian does no manual pre-research.** This replaces the Project's original sizing assumption ("material already exists in the wiki, this is assembly work"), which Julian corrected as wrong on 19 Aug 2026: most raw material does not already exist. Cheap test: review the first area's output; if it is shallow, stop the run before burning the other 7 branches.

## Payoff Test
- **Payoff:** This makes Julian better at task routing. The articles and their mental models become a wiki reference he consults when deciding how to attack a piece of work, so he can choose the best engineering pattern for any project or task rather than guessing. Two concrete pieces of work get better because this exists: the task-routing skill (this Project's second deliverable) is built directly from these articles, and sprint planning / project definition improve because that is where routing decisions get made. A third payoff, using these patterns in the TTI role, is recorded as speculative because that role is not yet secured.
- **Silence test:** Passed. Julian confirmed (20 Aug 2026) he would still do this work if he could never tell anyone, so the payoff stands on usefulness, not prestige.
- **Good enough when:** the task-routing skill can be built from the articles alone without going back to do more research, and Julian can manually verify task-routing choices by reading the articles against the mental model he has built.

## Links
- **Project:** [[../projects/ai-engineering-patterns|AI Engineering Patterns]]
- **Workstream:** [[../performance/_index|performance]]
