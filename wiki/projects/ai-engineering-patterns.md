---
workstream: performance
created: 2026-08-17
status: active
flow: implementing
t-shirt: XS
wsjf: 5.5
status-updated: 2026-08-23
por-key: POR-22
jira-key: BWS-61
---

# AI Engineering Patterns

## Status (as of 2026-08-23)

**Position:** As of 23 Aug 2026 (evening): box 1 execution is COMPLETE pending Julian's sign-off. The workflow ran clean: 9 articles drafted from the Perplexity research into `wiki/technology/ai-engineering-patterns/`, every one passed its Codex adversarial check (23 findings raised, all 23 fixed), and the synthesis stage produced the `_index.md`, 2 new mental models ([[mm-blast-radius]], [[mm-adaptation-ladder]]), cross-links, and a technology-index row. Machine cost 2.03M tokens in 11.6 minutes; Julian's attended time so far ~30 min (research stage). Remaining for box 1: Julian reviews the set against the synthesis flags in the deliverable file and signs off (CC4). Target unchanged: all three outputs complete before the possible 1 Sep 2026 TTI start.

**Next action (in order, resume here):**
1. Julian: review the 9 articles and the synthesis flags (recorded in [[ai-engineering-pattern-articles]]), decide the two flagged judgment calls (mm-tool-surface rejection; mm-adaptation-ladder filing location), sign off, and report review minutes for the Time Log.
2. `/define-enabler` for Deliverable 2: task-routing skill + tested evals + wiki mirror + systems-register row (the second 2h box). Same Prompt Zero gate.
3. `/jira-sync` to create the BWS story for Deliverable 1 under Epic BWS-61.

**Waiting on:** Julian's review and sign-off of the 9 articles.

**Detail tier:** see `## Deliverables` below.

## Project Summary File Map

These are the live files that make up this Project's evidence base. The Project page is the hub; domain files stay in their natural homes and are linked here.

| Area | File | Role |
|---|---|---|
| Judgement seed | [[routing-work-to-agents]] | Existing four-question routing ladder; the seed the routing skill extends. |
| Judgement seed | [[mental-models-index]] | Existing mm catalog (verification, routing, steering, token economics, memory pillars) the catalog entries link to. |
| Workstream | [[performance-workstream]] | Objective 1 (Leverage AI, Q4 2026), which this Project serves. |

### Status log (newest first)
| Date | Update |
|------|--------|
| 2026-08-23 | Box 1 workflow executed (wf_649b13a4, 19 agents, 11.6 min, 2.03M tokens, 0 errors): 9 articles drafted and Codex-verified (23/23 findings fixed), _index.md + 2 new mm models ([[mm-blast-radius]], [[mm-adaptation-ladder]]) + cross-links + technology index row created. Research report archived to raw/_processed/ with manifest row. Awaiting Julian sign-off (CC4). |
| 2026-08-23 | Perplexity research delivered (raw/dr-all-areas.md, ~30 min attended, logged). Gap scan verdict: observability is a distinct discipline and becomes Area 8. Perplexity volunteered a ninth area (Model Adaptation: prompting vs RAG vs fine-tuning); Julian accepted it, so the catalog is now 9 articles and completion criteria updated. Ready to launch the workflow. |
| 2026-08-23 | Execution design revised: Perplexity Deep Research replaces the Sonnet research stage (8 prompts written to raw/dr-prompts-ai-engineering-patterns.md; prompt 8 doubles as the gap scan for the eighth area); article template approved (first cut) and recorded in the task file; Opus agents now validate-and-draft. Waiting on Julian to run the prompts. |
| 2026-08-20 | Deliverable 1 defined via `/define-task`: [[ai-engineering-pattern-articles]] (2h, queued). Key decisions: 8 separate pattern files in a new `wiki/technology/ai-engineering-patterns/` folder (no catalog file); fan-out-and-synthesize workflow with per-file Codex verification; original "assembly not research" sizing assumption corrected — research is folded into execution via Sonnet agents. Payoff test passed. |
| 2026-08-18 | POR card created (POR-22, transitioned to Ready) and BWS Epic created (BWS-61) via `/jira-sync`. Keys written back to frontmatter. |
| 2026-08-17 | Definition session closed; numbered resume plan written into Next action (deliverable definition, Jira sync, then the two 2h execution boxes). Resume planned 18 Aug. |
| 2026-08-17 | Project defined and scored (WSJF 5.5, rank 3). Scope merged in the task-routing skill (formerly the separate "AI Task Decomposition Playbook" funnel candidate). POR card pending Atlassian re-auth. |

---

## Objective
Be able to choose the right AI engineering approach for any piece of work and direct it with confidence, in my own AI OS and in the TTI role if secured, backed by a market-aligned patterns catalog and a routing skill that applies it at planning time, in place before the possible 1 Sep 2026 TTI start.

## Outcomes / Outputs
1. **Output — AI Engineering Patterns Catalog:** one succinct entry per pattern area (~8, market-aligned: context engineering, memory, tools/MCP, evals, orchestration/workflow architectures, spec-driven development, security incl. agent identity), each linked to its relevant mental models, with use cases and examples aimed at routing tasks. Chain: Claude drafts, Codex verifies, Julian peer-reviews and signs off. Lives in `wiki/technology/`.
2. **Output — Judgement layer distilled:** new `mm-*` models where a pattern area warrants one (six-slot format, listed in [[mental-models-index]]), plus a "where this applies in my own work" note per area. Same Claude/Codex/Julian chain.
3. **Output — Task-routing skill with tested evals:** a `/decompose`-style skill built from the catalog that works through the right attack shape for a task at planning time; invoked at sprint planning and project definition (adoption forcing-function per [[feedback-build-dont-adopt|build-don't-adopt]]); ships with `evals/` and TESTING evidence like other skills; wiki-mirrored; gets a [[systems-register]] row at creation.

## Future Leverage
Q4 Key Person of Influence content substance (Objective 2), the parked retention method's source material, and AI leverage on TTI-role deliverables if the role lands.

## Existing Leverage
Five existing mm models ([[mm-verification]], [[mm-routing]], [[mm-steering]], [[mm-token-economics]], [[mm-memory-pillars]]), the working-with-genai articles, a taxonomy already agreed in the defining session, the Codex plugin wired for verification, and `/notebooklm` ready for the parked retention output. Assembly and verification work, not research from scratch: this pulled the natural size down to XS.

## Leading Indicators
N/A — XS Project.

## Effort
**T-shirt size:** XS (5-8h), structured as two hard 2h timeboxes (catalog + mental models; routing skill + evals) plus Julian's peer review. The timeboxes are deliberate forcing functions: work stops at the box, remainder is re-scoped rather than overrun.

## WSJF Scoring
| Component | Score | Rationale |
|-----------|-------|-----------|
| Value | 3 | Real but indirect: sharper planning judgement across all AI work. Capped at 3 by the payoff-route rule: the TTI corporate route is not yet secured. Revisit to 5 with a named route if the role lands. |
| Time Criticality | 5 | Named readiness date: in place before the possible 1 Sep 2026 TTI start, the capability's primary application window (role onboarding, when work patterns get set). Useful for routing all work the day it exists. |
| Risk / Opportunity | 3 | What it COULD enable: increases the chances of impressing TTI during a 6-12 month engagement and converting it to a permanent job. Also unblocks the parked retention method and Objective 2 KPI content substance. |
| Job Size | XS = 2 | 5-8h (two 2h boxes + review) |
| **Cost of Delay** | **11** | 3 + 5 + 3 |
| **WSJF** | **5.5** | 11 ÷ 2 |

## Scope
Project-level scope: what's first, what's explicitly out, and the breakdown the deliverables are elaborated from.

**Build first (MVP):** the catalog (Output 1) — the other two outputs consume it.

**Out of scope:** deep-dive articles per pattern area (breadth is the point; depth requests go to the funnel as separate deliverables); the retention/flashcards method (parked, see Funnel below); productising any of this for an external audience (that's Objective 2 territory, later).

**Work breakdown:** each row becomes a deliverable at elaboration time.

| Work | ~Hours |
|------|--------|
| Patterns catalog + mental models + application notes (Claude drafts, Codex verifies) | 2 (hard box) |
| Task-routing skill + evals + wiki mirror + systems-register row | 2 (hard box) |
| Julian peer review and sign-off across all outputs | 1-2 |

## Completed
Nothing completed yet.

## Deliverables
| Deliverable | Hours | Status |
|-------------|-------|--------|
| [[ai-engineering-pattern-articles\|AI Engineering Pattern Articles]] | 2h | queued |

## Funnel
| Item | Intent | Added |
|------|--------|-------|
| Retention method | Ensure the patterns, mental models, and use cases actually stick: periodic triggers or a NotebookLM flashcards integration (via `/notebooklm`). Parked at definition time; promote once the catalog exists. | 2026-08-17 |

## Links
- **Workstream:** [[../performance/_index|performance]] — serves Objective 1 (Leverage AI, Q4 2026) in [[performance-workstream]]
