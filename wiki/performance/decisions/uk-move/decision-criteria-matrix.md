---
type: reference
created: 2026-07-13
status: planned
tags: [decision, uk-move, method]
---

# Decision Criteria Matrix (planned)

Planned companion to the UK-move risk register. This doc captures the rationale now so it is not lost. **Build it only after the risk register is complete** (Julian's sequence: finish surfacing/scoring risks first, then transition to the decision matrix).

## Why this exists

Julian wants a **single filterable place** to hold what a decision turns on, per scenario, instead of the analysis being spread across ~15 workspace files. The risk register already does this for the downside (what could go wrong, by scenario, Impact x Probability). This is its sibling for the criteria (how well each scenario delivers what matters).

The pain being solved: "I don't have one place to look. Information is all over the place." The risk register proved the pattern - grab one sheet, filter by scenario, think it through. The decision needs the same.

## The two sibling surfaces

- **Risk register** = downside per scenario. Impact x Probability. Answers *"What could go wrong if I choose X?"*
- **Decision criteria matrix** = criteria per scenario. Weight x Score. Answers *"How well does X deliver what matters?"*
- They feed each other: a big red risk in the register pulls down that scenario's score on the related criterion in the matrix.

## What exists now (and why it is not this)

| What exists | What it does | Why it is not the single decision surface |
|---|---|---|
| "Decision hinges" section in the project | Narrative list of the questions that decide London vs Malvern | Prose, not a scorecard; only 2 of the 3 scenarios; goes stale |
| [[decision-journal]] entry | Records the committed decision + reasoning | A record of what was chosen, not a live side-by-side of the options |
| BRAINED docs (uk-move/ workspace) | The full structured analysis | Deep and correct, but spread across ~15 files - the opposite of "one place I can grab" |
| Financial model / reviews | The cash/runway evidence | One criterion's worth of depth, not the whole decision |

## Proposed structure

Side-by-side (criteria down the side, three scenarios across the top) because it is a small set meant for at-a-glance comparison, unlike the long filterable risk list. Scenarios are the "what we do first" set, same as the risk register: **Stay in HK / Move to London / Move to Malvern.**

| Criterion (workstream) | Weight | Stay HK | Move to London | Move to Malvern |
|---|---|---|---|---|
| Sophia schooling & stability (Wellbeing) | H | | | |
| Sophia autonomy & social world (Wellbeing) | ? | | | |
| Julian's wellbeing / stress (Wellbeing) | ? | | | |
| Family proximity & support - Mum (Relationships) | ? | | | |
| Sophia-mother proximity - Clodagh (Relationships) | ? | | | |
| Partner future - Joanne (Relationships) | ? | | | |
| Search-phase cash burn / run rate (Finance) | H | | | |
| Runway / cashflow resilience - landing pot (Finance) | H | | | |
| Wealth preservation (Finance) | ? | | | |
| Job prospects / lane fit / income (Career) | ? | | | |
| Lifestyle & reversibility (Personal) | ? | | | |
| **Weighted total** | | | | |

Each scored cell carries a one-line rationale. Criteria are ordered by workstream priority (Wellbeing, Relationships, Finance, Career, Personal). The live drivers Julian has already distilled - cash burn, cashflow resilience, and schooling - are weighted High.

## Build plan

- Lives as a **second tab ("Decision Matrix") in the same Google Sheet** as the risk register, so it is in the one file Julian grabs.
- Populated from existing project artifacts only (financial model, job-market report, Sophia profile, reviews) - grounded, no invention.
- Weighted total per scenario is an **indicative** signal, not the decider (same caveat as the risk register totals - do not over-read a number driven partly by how many rows an option has).

## Open questions (resolve at build time)

1. Final criteria set (proposed above; add/cut).
2. Scoring scale: **1-5** (matches the risk register) or **High/Medium/Low**.
3. Weights per criterion (Finance cash-burn/cashflow + Wellbeing schooling flagged heaviest so far).

## Links
- [[uk-relocation-decision]] - the project this serves
- [[uk-move-decision-risk-register-2026-07-12.xlsx|Risk register (.xlsx snapshot)]] + the live Google Sheet (Decision Matrix will be a tab in it)
- [[risk-framework|Risk Framework and Methodology]] - the sibling method for the downside surface
