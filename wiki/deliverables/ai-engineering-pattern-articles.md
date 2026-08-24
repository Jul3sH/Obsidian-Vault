---
type: task
project: ai-engineering-patterns
workstream: performance
hours: 2h
created: 2026-08-20
status: done
jira-key:
value-rationale:
---

# AI Engineering Pattern Articles

> **Purpose block.** This is the definition file for Deliverable 1 of the [[ai-engineering-patterns|AI Engineering Patterns]] Project: 9 pattern-area articles plus supporting mental models, written into `wiki/technology/ai-engineering-patterns/`. It was created on 20 Aug 2026 through the `/define-task` interview so the work enters the backlog scoped, sized, and payoff-tested before execution starts. It is read at execution time (the Execution Approach section is the run plan) and at sign-off (the Completion Criteria are the checklist).

## Prompt Zero
**Waived 20 Aug 2026** (size 1 waiver, permitted at 1-4h). Reason: the grounding brief already exists in Julian's own words from the 19-20 Aug definition session — the payoff, good-enough condition, execution shape, and corrected assumptions below were all stated or approved by him during the `/define-task` interview, so a separate Prompt Zero interview would duplicate them.

## Task Description
Produce 9 market-aligned AI engineering pattern articles (with new mental models where warranted) in a new `wiki/technology/ai-engineering-patterns/` folder, giving Julian a wiki reference for choosing the best engineering pattern for any project or task.

## Completion Criteria
1. 9 pattern-area files exist in `wiki/technology/ai-engineering-patterns/` (context engineering, memory, tools/MCP, evals, orchestration/workflow architectures, spec-driven development, security including agent identity, production observability and drift monitoring, model adaptation), each linked to relevant mental models with use cases and examples, and listed in a new `_index.md` (navigation only, per wiki convention; the collection of 9 files is the catalog, there is no separate catalog file)
2. New `mm-*` files in six-slot format exist for pattern areas that warrant one, and are listed in [[mental-models-index]]
3. A Codex verification pass is complete on each of the 9 files
4. Julian has signed off

## Definition of Done
The `wiki/technology/ai-engineering-patterns/` folder exists containing an `_index.md` and 9 pattern articles, each researched from current (post-2025) practitioner sources, cross-linked to the mental-model catalog, and individually verified by Codex. Any new mental models are filed in the six-slot format and indexed. Julian has read the set and signed off, and can route a task to an engineering pattern by consulting the folder.

## Execution Approach
Agreed 19-20 Aug 2026 in the definition session; revised 23 Aug 2026 (Perplexity replaces the Sonnet research stage; article template agreed). Shape: **fan-out and synthesize** dynamic workflow, with one inline adversarial check per branch (not a panel review of the final result). Fable (session model) coordinates.

- **Research (Julian + Perplexity, before the workflow):** Julian runs ONE single-shot Perplexity Deep Research prompt (in `raw/dr-prompts-ai-engineering-patterns.md`) producing all area reports in one document, saved as `raw/dr-all-areas.md`; per-area fallback prompts exist in the same file for any area that comes back thin. Area 8 of the prompt is the gap scan that selects the eighth pattern area, testing the "right cut" assumption. This is attended time — logged in minutes.
- Pipeline over the 9 pattern areas (was 8; Julian accepted Perplexity's ninth area, Model Adaptation, on 23 Aug 2026 — research already done, one extra parallel branch). Each branch: **Opus agent** (high reasoning effort: validates the Perplexity report — spot-checks claims and currency, flags what does not survive — fills gaps, then drafts the article to the agreed template, linking mental models) → **one Codex adversarial check** of that file, invoked by the workflow agent calling the Codex companion runtime directly via Bash (the `/codex:adversarial-review` slash command is user-invoke-only, but the underlying script is callable).
- **Article template (approved 23 Aug 2026, first cut; becomes the folder convention):** frontmatter → title → purpose block → Key Takeaways → What It Is → Reach For It When (the load-bearing routing section) → Core Techniques (table) → Use Cases & Examples → Anti-Patterns → Mental Models → State of Practice (dated) → Links.
- Final **Opus synthesis stage** (barrier, needs all 9): writes `_index.md`, decides which new `mm-*` models are warranted (cross-area view avoids duplicates), adds cross-links.
- Julian reviews and signs off after the run (workflows take no mid-run input).
- Codex usage bills to the ChatGPT subscription (auth mode: chatgpt, no API key), so the cost risk is throttling, not money. A Codex failure marks that file "unverified, retry later" rather than killing the branch.
- Expected agent count (~20: 9 validate-and-draft, 9 Codex checks, 1 synthesis) exceeds the session's medium workflow size guideline; the task genuinely calls for it.

## Load-Bearing Assumptions
1. **The 9 areas are the right market-aligned cut.** (Resolved 23 Aug 2026: the gap scan confirmed observability as a distinct discipline and surfaced model adaptation; Julian accepted both, settling the cut at 9.)
2. **A single-shot Perplexity Deep Research run, validated by Opus agents, provides sufficient grounding; Julian does no further manual research.** (Revised 23 Aug 2026: originally Sonnet research agents; Perplexity replaced them, and one combined run replaced 8 individual runs — the known risk is thinner per-area depth.) This replaces the Project's original sizing assumption ("material already exists in the wiki, this is assembly work"), which Julian corrected as wrong on 19 Aug 2026. Cheap test: skim the report's weakest-looking area before launching the workflow; the fallback per-area prompts re-run any thin area cheaply.

## Payoff Test
- **Payoff:** This makes Julian better at task routing. The articles and their mental models become a wiki reference he consults when deciding how to attack a piece of work, so he can choose the best engineering pattern for any project or task rather than guessing. Two concrete pieces of work get better because this exists: the task-routing skill (this Project's second deliverable) is built directly from these articles, and sprint planning / project definition improve because that is where routing decisions get made. A third payoff, using these patterns in the TTI role, is recorded as speculative because that role is not yet secured.
- **Silence test:** Passed. Julian confirmed (20 Aug 2026) he would still do this work if he could never tell anyone, so the payoff stands on usefulness, not prestige.
- **Good enough when:** the task-routing skill can be built from the articles alone without going back to do more research, and Julian can manually verify task-routing choices by reading the articles against the mental model he has built.

## Sign-off Review Scope (agreed 23 Aug 2026; the definition future estimates compare against)
Julian's manual verification of a machine-drafted, machine-verified article set is:
1. Full read of the `_index.md` plus a ~30% sample of the articles.
2. Skim of the remainder at Key Takeaways + "Reach For It When" level.
3. An explicit decision on every judgment item the synthesis stage flagged.
4. A glance at newly created mental-model files and at any pre-existing file the run edited.

This scope assumes the two upstream machine passes ran clean (Opus claim validation at draft time, Codex adversarial check per file, all verdicts "verified"). A run arriving with unverified articles or failed branches warrants a wider sample. Record actual review minutes against this scope in the Time Log so future estimates compare like with like.

## Sign-off
**Signed off by Julian, 23 Aug 2026.** All four completion criteria met. Decisions at sign-off: the mm-tool-surface rejection was upheld (covered by [[mm-blast-radius]] plus [[mm-token-economics]]; revisit only if future tool-surface decisions go unguided); [[mm-model-adaptation]] (renamed from mm-adaptation-ladder at review) stays in performance/working-with-genai/. Totals: Julian 65 attended minutes against the 2h box; machine 2,633,750 tokens (2,028,039 Claude workflow + 605,711 Codex across 10 reviews).

## Sign-off Review Flags (from the 23 Aug 2026 workflow run; resolved at CC4 review, see Sign-off)
1. **mm-tool-surface proposal rejected** by the synthesis stage as not distinct (least-privilege half went into [[mm-blast-radius]]; progressive-disclosure half already covered by [[mm-token-economics]]). Overturn if you disagree.
2. **[[mm-model-adaptation]] filing location**: created in performance/working-with-genai per instruction, but by the filing test it arguably belongs in technology/. Decide at review.
3. **Contested claims kept and flagged in-article, not resolved**: RAG vs long-context (no winner), memory vendor benchmarks (self-reports vs independent evals disagree), MCP adoption numbers, the evals/observability boundary.
4. **Perishable facts**: several articles carry Aug 2026 vendor/pricing/context-window facts that age within months. Dated in-line; re-check before any feeds a real decision.
5. The synthesis stage also edited [[mm-routing]]'s Limitations section (its blast-radius gap now points to the new model) and fixed 8 broken sibling links the drafters wrote against wrong slugs.
6. **RESOLVED 23 Aug (later same day):** the synthesis outputs (2 mm files, mm-routing edit, _index) had escaped adversarial review because verification was wired per-branch and synthesis ran after it. A follow-up Codex pass reviewed all four; it found one medium finding (a false claim that frontier closed models are not API-fine-tunable; OpenAI/Azure do offer it), now corrected in both [[mm-model-adaptation]] and the model-adaptation article. A permanent coverage rule was added to AGENTS.md ("Adversarial Coverage of Machine-Drafted Deliverables"). The _index, mm-blast-radius, and the mm-routing edit passed clean.

## Time Log
Machine effort is recorded in tokens (from the workflow run view), Julian's effort in focused minutes (self-reported at each handoff, prompted by the UserPromptSubmit time-log hook). Only Julian's minutes roll up into Actual hrs in the [[estimation-baseline|Estimation Baseline]]; tokens go in that row's Notes.

| Date | Segment | Who | Tokens / Minutes | Notes |
|------|---------|-----|------------------|-------|
| 2026-08-23 | Perplexity Deep Research: single-shot run, Area 8 update, export wrangling | Julian | ~30 min | Report delivered to raw/dr-all-areas.md; 9 areas (ninth accepted into scope) |
| 2026-08-23 | Workflow run wf_649b13a4: 9 draft + 9 Codex-verify + 1 synthesis (19 agents, 0 errors, 11.6 min wall-clock) | Machine (Claude) | 2,028,039 tokens | All 9 articles verified; 23 Codex findings, 23 fixed; 2 mm models created |
| 2026-08-23 | Codex adversarial reviews, 9 threads (gpt-5.5, medium reasoning) | Machine (Codex) | 526,363 tokens | Mined from ~/.codex/logs_2.sqlite per-thread peak total_usage_tokens (42,965 to 86,900 per review); billed to ChatGPT subscription, not counted by the workflow meter |
| 2026-08-23 | Sign-off review, part 1 (step 3 of the review scope) | Julian | 5 min | Review scope steps 1-2 and 4 still open at this point |
| 2026-08-23 | Codex adversarial review of synthesis outputs (2 mm files, mm-routing edit, _index) after coverage gap found | Machine (Codex) | 79,348 tokens | 1 medium finding (false fine-tuning availability claim); fixed in mm-model-adaptation and model-adaptation. Coverage rule added to AGENTS.md |
| 2026-08-23 | Sign-off review, part 2: Codex-fix review (5 min) + mm-blast-radius review (5 min) | Julian | 10 min | Running attended total: 45 min |
| 2026-08-23 | Sign-off review, part 3: scope steps 1-2, index + article sample and skim (15 min, all OK); mm-model-adaptation review (5 min, keep in working-with-genai) | Julian | 20 min | Running attended total: 65 min |
| 2026-08-23 | **Signed off.** Final totals | - | Julian 65 min; machine 2,633,750 tokens | Deliverable complete; rolled into estimation baseline |

## Links
- **Project:** [[../projects/ai-engineering-patterns|AI Engineering Patterns]]
- **Workstream:** [[../performance/_index|performance]]
