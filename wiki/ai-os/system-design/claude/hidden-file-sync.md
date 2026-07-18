---
type: reference
created: 2026-05-08
updated: 2026-06-20
---

# Hidden File Sync Checklist

> *Every file at a hidden path (`~/.claude/`) must have an exact mirror in the wiki. This checklist tracks sync status.*

**Why this exists:** Skill files and memory files live outside Obsidian at hidden paths. The user cannot see or verify them without this mirror. Claude must update the wiki copy whenever the source changes.

---

## Skill Files

| Skill | Source | Wiki Mirror | Last Synced |
|-------|--------|-------------|-------------|
| ats-checker/references | `~/.claude/skills/ats-checker/references/jd-keyword-extraction.md` | [[../../skills/ats-checker/references/jd-keyword-extraction\|jd-keyword-extraction.md]] | 2026-06-10 (made Step 1 keyword table display mandatory before confirmation question; added Tiering Signal Key for Core/High/Medium classification) |
| goal-planner | `~/.claude/skills/goal-planner/SKILL.md` | [[../../skills/goal-planner/SKILL\|SKILL.md]] | 2026-05-21 |
| storm-research | `~/.claude/skills/storm-research/SKILL.md` | [[../../skills/storm-research/SKILL\|SKILL.md]] | 2026-06-30 (new skill: 5-lens research pipeline with adversarial citation verification, HTML report output) |
| storm-research | `~/.claude/skills/storm-research/report-template.html` | [[../../skills/storm-research/report-template\|report-template.md]] | 2026-06-30 (new) |
| project-planner | `~/.claude/skills/project-planner/SKILL.md` | [[../../skills/project-planner/SKILL\|SKILL.md]] | 2026-06-20 (Review stage removed: Stage Regression `review` row dropped — regression now only targets `funnel` or re-scores in place at `ready`; two trigger-field "moves to Review" references repointed to "moves to Ready". Prior: 2026-06-15 Step 0 restructured into 0.1 Title/Description/Workstream, 0.2 Upstream Hierarchy Check (full home-workstream check incl. Vision/Principles/Values/Ambitions/Directions/OKRs + fixed-order upstream Principles/Vision check + Performance Principles/Values/Ambitions/Directions always checked regardless of hierarchy position), 0.3 Commitment Gate; old Step 1.1 Workstream now redirects to 0.1; Step 0.2 findings format changed — bold label folds in source workstream (e.g. "Relationships Value"), no separate "(upstream — X)" annotation; Step 0.1 description now requires what+why with a gatekeeper check; Step 0.3 Payoff restructured into 4 sub-headings — Goal Alignment Payoff / Lessons Learnt Leverage / Future Leverage / Stated Payoff; Cost of 3 months' inaction now bulleted, one consequence per Payoff item; new Recommendation Default "Adjustment Window" — invite adjustments after every step before proceeding; Step 1.3's old "What This Unlocks" retired (superseded by Step 0.3 Future Leverage); Step 1.4 adds "Existing Leverage" check before sizing; Step 1.5 + Phase 3 wiki template updated with Future Leverage / Existing Leverage sections; Step 0.3 adds Confidence band (High/Med/Low, Outcome payoffs only) as a gate modifier not a WSJF input, carried into Step 1.5 summary + Project file Confidence section; Step 1.4 consults estimation-baseline.md before sizing; Step 3.3b appends a baseline row on Project write; t-shirt scale gains XXS=1 (one consistent Fibonacci scale XXS/XS/S/M/L/XL across all artefact types); deliverables-in-project refactor: Phase 3 template's projects/_index.md header, Detail tier, Links, and Someday-promotion text now point to each Project's own `## Deliverables` section instead of deliverables/_index.md; projects/_index.md split into pure-nav index + new project-priorities.md (WSJF-ranked queue, Jira sync SSOT) — Context section, Step 2.3, Step 3.1 (two header templates), Step 3.3, and Step R5 all repointed accordingly; **also today:** funnel-parking path (Step 0.3 "vague" branch) now also creates a POR board card (Epic, label `funnel`, status `Funnel`) per row, written back to funnel.md's new Jira column — see portfolio-backlog.md "Jira representation"; **also today (2):** `## Someday` renamed to `## Funnel` in the Phase 3 Project file template — now also absorbs former `## Parked Ideas` content (one table for both); new `## Completed` and `## Deliverables` placeholder sections added; Step R4 Stage Regression's preserved-content list updated from "Parked Ideas" to "Funnel"; bau-someday.md eliminated entirely — standalone deliverable ideas now become XXS Project candidates in funnel.md) |
| define-task | `~/.claude/skills/define-task/SKILL.md` | [[../../skills/define-task/SKILL\|SKILL.md]] | 2026-06-30 (Task sizing changed from Fibonacci abstraction to direct hours estimate (e.g. 1h, 2h); split threshold changed from "size 8" to ">8h"; size/story-points references removed from template, log format, and admission gate. Prior: 2026-06-15 Step 4.4 scoped hrs; deliverables-in-project refactor; Funnel rename) |
| jira-pull | `~/.claude/skills/jira-pull/SKILL.md` | [[../../skills/jira-pull/SKILL\|SKILL.md]] | 2026-06-20 (Review stage removed from Column→Flow mapping — Review/Analyzing collapsed into `ready`; added legacy-Review fallback note. Prior: 2026-06-15 Step 0 cheap pre-check; Steps 2/5 repointed to project-priorities.md) |
| jira-sync | `~/.claude/skills/jira-sync/SKILL.md` | [[../../skills/jira-sync/SKILL\|SKILL.md]] | 2026-06-15 (Step 1 repointed from projects/_index.md to project-priorities.md for the list of active Projects; **also today:** Step 3 and Edge Cases updated — skip items in a Project's `## Funnel` section, replacing the former `## Someday` / `wiki/deliverables/bau-someday.md` references, now eliminated) |
| morning | `~/.claude/skills/morning/SKILL.md` | [[../../skills/morning/SKILL\|SKILL.md]] | 2026-05-20 (operating-model→agile-workflow ref) |
| resume-tailor | `~/.claude/skills/resume-tailor/SKILL.md` | [[../../skills/resume-tailor/SKILL\|SKILL.md]] | 2026-06-03 (model-selection gate; final coverage review; anti-skip guardrails; pre-flight Role #1 checkpoint; mandatory Live Working Document — update tracking file after every lock so it never goes stale) |
| resume-tailor/references | `~/.claude/skills/resume-tailor/references/pre-section-template-selection.md` | [[../../skills/resume-tailor/references/pre-section-template-selection\|pre-section-template-selection.md]] | 2026-06-03 |
| resume-tailor/references | `~/.claude/skills/resume-tailor/references/section0-mapping.md` | [[../../skills/resume-tailor/references/section0-mapping\|section0-mapping.md]] | 2026-06-03 |
| resume-tailor/references | `~/.claude/skills/resume-tailor/references/section2-summary.md` | [[../../skills/resume-tailor/references/section2-summary\|section2-summary.md]] | 2026-06-03 (default char limit 545→560 incl. spaces; rationale added: 5 rows × 120 less ~7% wrap buffer) |
| resume-tailor/references | `~/.claude/skills/resume-tailor/references/section3-skills.md` | [[../../skills/resume-tailor/references/section3-skills\|section3-skills.md]] | 2026-06-03 (separate evidenced-vs-JD-demanded judgements; never present master-evidence as JD basis) |
| resume-tailor/references | `~/.claude/skills/resume-tailor/references/section4-responsibilities.md` | [[../../skills/resume-tailor/references/section4-responsibilities\|section4-responsibilities.md]] | 2026-06-03 (responsibilities = scope not outcomes; + "option N" vs "Responsibility 1-3" naming convention) |
| resume-tailor/references | `~/.claude/skills/resume-tailor/references/section5-achievements.md` | [[../../skills/resume-tailor/references/section5-achievements\|section5-achievements.md]] | 2026-06-03 (added "Aligns with chosen responsibilities?" column; + "option N" vs "Achievement 1-3" naming convention) |
| retro | `~/.claude/skills/retro/SKILL.md` | [[../../skills/retro/SKILL\|SKILL.md]] | 2026-06-15 (Step 4: when a completed story closes out its parent Project, fill Actual hrs + variance + learning in estimation-baseline.md) |
| define-enabler | `~/.claude/skills/define-enabler/SKILL.md` | [[../../skills/define-enabler/SKILL\|SKILL.md]] | 2026-06-15 (Step 4.4: add deliverable's hour-equivalent to parent Project's running Scoped hrs in estimation-baseline.md; deliverables-in-project refactor: Steps 1.1b/3.1/4.2 now read/write the Project's own `## Deliverables` section in wiki/projects/[project-slug].md instead of deliverables/_index.md, with `## Standalone Deliverables` in deliverables/_index.md for standalone items; **also today:** `## Someday` references renamed to `## Funnel`; standalone fallback (deleted `wiki/deliverables/bau-someday.md`) replaced with XXS Project candidate rows in `wiki/projects/funnel.md`; evals.json eval 4 updated to match) — 2026-06-25 (frontmatter + intro corrected: "with WSJF scoring" → "sized, not WSJF-scored"; WSJF is Project-level only, matching the existing body text) |
| define-user-story | `~/.claude/skills/define-user-story/SKILL.md` | [[../../skills/define-user-story/SKILL\|SKILL.md]] | 2026-06-15 (Step 4.4: add deliverable's hour-equivalent to parent Project's running Scoped hrs in estimation-baseline.md; deliverables-in-project refactor: Steps 3.1/4.2 and duplicate-check edge case now read/write the Project's own `## Deliverables` section in wiki/projects/[project-slug].md instead of deliverables/_index.md, with `## Standalone Deliverables` in deliverables/_index.md for standalone items; **also today:** `## Someday` references renamed to `## Funnel`; standalone fallback (deleted `wiki/deliverables/bau-someday.md`) replaced with XXS Project candidate rows in `wiki/projects/funnel.md`) — 2026-06-25 (frontmatter + intro corrected: "with WSJF scoring" → "sized, not WSJF-scored"; WSJF is Project-level only, matching the existing body text) |
| sprint-plan | `~/.claude/skills/sprint-plan/SKILL.md` | [[../../skills/sprint-plan/SKILL\|SKILL.md]] | 2026-05-22 (BWS renamed to Agile Sprints) |
| standup | `~/.claude/skills/standup/SKILL.md` | [[../../skills/standup/SKILL\|SKILL.md]] | 2026-05-08 |
| skill-conventions | `~/.claude/skills/skill-conventions.md` | [[skill-conventions\|skill-conventions.md]] | 2026-06-03 (full-folder mirror rule added) |
| notebooklm-py | `~/.claude/skills/notebooklm-py/SKILL.md` | [[../../skills/notebooklm-py/SKILL\|SKILL.md]] | 2026-06-07 |
| notebooklm-py/scripts | `~/.claude/skills/notebooklm-py/scripts/run_notebooklm.py` | [[../../skills/notebooklm-py/scripts/run_notebooklm\|run_notebooklm.md]] | 2026-06-07 |
| notebooklm-py/references | `~/.claude/skills/notebooklm-py/references/TESTING.md` | [[../../skills/notebooklm-py/references/TESTING\|TESTING.md]] | 2026-06-07 |
| llm-council | `~/.claude/skills/llm-council/SKILL.md` | [[../../skills/llm-council/SKILL\|SKILL.md]] | 2026-06-09 (stakes/context-tier gate; nearest-past-failure + behavioural priors + flagged-hypothesis in brief; Root-Cause & Precedent Check in synthesis; peer-review Q4 root-cause-vs-symptom) |
| llm-council | `~/.claude/skills/llm-council/lessons-learned.md` | [[../../skills/llm-council/lessons-learned\|lessons-learned.md]] | 2026-06-09 (new curated improvement loop; L1 = TTI routing-flaw) |
| commitment-guard | `~/.claude/skills/commitment-guard/SKILL.md` | [[../../skills/commitment-guard/SKILL\|SKILL.md]] | 2026-07-07 (new: instruction-only skill; defends LOCKED decisions from emotional U-turns via the F-N-M-T reopen test + 48h stand-down; commit-path lock checklist) |
| decision-visualisation-check | `~/.claude/skills/decision-visualisation-check/SKILL.md` | [[../../skills/decision-visualisation-check/SKILL\|SKILL.md]] | 2026-07-15 (new: instruction-only skill; fires when Julian evaluates life/career/relationship options by feel; asks for full mental image - pleasant + bad-day version - to complete the incomplete frame before it biases the decision; paired with feedback-visual-representation-bias memory and visual-representation-bias article) |

## Plugin Skill Files

| Skill | Source | Wiki Mirror | Last Synced |
|-------|--------|-------------|-------------|
| apollo-person-match | `~/Library/Application Support/Claude/.../skills/apollo-person-match/SKILL.md` | [[../../skills/apollo-person-match/SKILL\|SKILL.md]] | 2026-05-08 |
| linkedin-enrichment | `~/Library/Application Support/Claude/.../skills/linkedin-enrichment/SKILL.md` | [[../../skills/linkedin-enrichment/SKILL\|SKILL.md]] | 2026-05-08 |

## Memory Files

| File | Source | Wiki Mirror | Last Synced |
|------|--------|-------------|-------------|
| MEMORY.md | `~/.claude/projects/.../memory/MEMORY.md` | [[memory/MEMORY\|MEMORY.md]] | 2026-07-07 (added feedback-decision-reopening.md row) |
| feedback-decision-reopening.md | `~/.claude/projects/.../memory/feedback-decision-reopening.md` | [[memory/feedback-decision-reopening\|feedback-decision-reopening.md]] | 2026-07-07 (new: defend LOCKED decisions from emotional U-turns; F-N-M-T reopen test + 48h stand-down; complements feedback-commitment-forcing) |
| feedback-visual-representation-bias.md | `~/.claude/projects/.../memory/feedback-visual-representation-bias.md` | [[memory/feedback-visual-representation-bias\|feedback-visual-representation-bias.md]] | 2026-07-15 (new: Julian builds vivid but incomplete mental images of decision options; pleasant frame crystallises first; ADHD-amplified; ask for full image including bad-day version before the decision biases) |
| feedback-overanalysis-check.md | `~/.claude/projects/.../memory/feedback-overanalysis-check.md` | [[memory/feedback-overanalysis-check\|feedback-overanalysis-check.md]] | 2026-07-16 (new: before large analytical work, ask whether the detail level is warranted; trigger on registers, matrices, scoring frameworks) |
| MEMORY.md | `~/.claude/projects/.../memory/MEMORY.md` | [[memory/MEMORY\|MEMORY.md]] | 2026-07-15 (added feedback-visual-representation-bias.md row; also brought mirror current: was missing wsjf-double-counting, commitment-forcing, decision-reopening rows) |
| user.md | `~/.claude/projects/.../memory/user.md` | [[memory/user\|user.md]] | 2026-07-12 (added Psychological Fingerprint table with 4 traits; added Context Loader trigger table for on-demand deep-file loading; updated Family with Sophia age + UK move detail; removed Active Focus Area as project state; separated Preferences section) |
| projects.md | `~/.claude/projects/.../memory/projects.md` | [[memory/projects\|projects.md]] | 2026-06-30 (CLSA split: First Interview (clsa-role) closed Done; Second Interview (clsa-second-interview, M, WSJF 3.8) added as active, deadline-driven, POR-21) |
| deliverables.md | `~/.claude/projects/.../memory/deliverables.md` | [[memory/deliverables\|deliverables.md]] | 2026-06-09 (renamed from project.md; points to wiki/deliverables/, timebox vocab) |
| feedback-goal-listing-order.md | `~/.claude/projects/.../memory/feedback-goal-listing-order.md` | [[memory/feedback-goal-listing-order\|feedback-goal-listing-order.md]] | 2026-06-12 (new) |

## AGENTS.md Core Framework Sections

| Framework | Source | Wiki Mirror | Last Synced |
|-----------|--------|-------------|-------------|
| Risk Framework & Methodology | `AGENTS.md` - Risk Framework section | [[risk-framework\|risk-framework.md]] | 2026-07-16 (register now covers risks AND opportunities; RISK/OPP col 2 added; Mitigation→Response, Mitigation Description→Response Description; opportunity response types Exploit/Enhance/Accept added; RAG split for threats vs opportunities; column schema updated to 24 cols; workflow updated. Prior: 2026-07-13 initial framework, 2026-07-15 one-row-per-effect + Probability:/Impact: labelling) |

## Config Files

| File | Source | Wiki Mirror | Last Synced |
|------|--------|-------------|-------------|
| settings.json (project) | `<vault>/.claude/settings.json` | [[permissions\|permissions.md]] (allowlist embedded verbatim) | 2026-06-30 (added 10 read-only MCP/Bash entries via /fewer-permission-prompts) |

> **Unmirrored (gap):** global `~/.claude/settings.json` and both `settings.local.json` files are not yet mirrored. Tracked in [[brain-dump]] (Wiki / AI OS).

## How to Verify

1. Open this checklist in Obsidian
2. Click any wiki mirror link — it opens the mirror copy
3. If the "Last Synced" date is older than the most recent session that modified the file, ask Claude to re-sync
