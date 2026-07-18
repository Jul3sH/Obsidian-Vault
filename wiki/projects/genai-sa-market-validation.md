---
workstream: career
created: 2026-06-17
status: active
flow: ready
t-shirt: XS
wsjf: 4.5
status-updated: 2026-06-18
por-key: POR-16
jira-key: BWS-10
---

# GenAI SA: Go/No-Go Validation

## Status (as of 2026-06-18)

**Position:** Defined and ranked. Reframed 18 Jun as a go/no-go gate (was "Market Validation & Profile"). Not started.

**Next action:** Run `/define-task` to finish defining the recruiter-validation deliverable, then `/jira-sync`.

**Waiting on:** Nothing.

**Detail tier:** see `## Deliverables` below.

### Status log (newest first)
| Date | Update |
|------|--------|
| 2026-06-18 | Reframed as a go/no-go gate. Profile reposition + market-response outcome moved to Phase 2. Phase 1 now Output-only (research → decision; recruiter validation). Confidence Medium→High; Value 1→3; WSJF 3.5→4.5; ranked #2. Retitled from "Market Validation & Profile". |
| 2026-06-17 | Project defined, scored (WSJF 3.5), added to POR board. Ranked #3 in queue behind TTI Role and Secure Next Role. |

---

## Objective

Reach a recruiter-validated go/no-go decision on whether pivoting toward a GenAI Solution Architect positioning will materially improve my employability — before investing significant development time into it.

## Outcomes / Outputs

1. **Output** — Market research concluded in a go/no-go decision: demand in HK + UK, required skills/experience by seniority, the gap against my current profile, and the employer/outsourcer landscape, driving a documented decision (invest in Phase 2, or treat GenAI SA as a hobby and don't).
2. **Output** — Decision and hypothesis validated with recruiters: their input captured on whether a GenAI SA positioning will materially help my job hunting, confirming or challenging the Output 1 decision.

## Hypothesis

> *"We believe pivoting toward a GenAI Solution Architect positioning will materially improve Julian's employability in HK and UK — leveraging 20+ years of enterprise architecture capital with targeted AI upskilling. We'll know this is worth pursuing when market research and recruiter input converge on a confident 'go' rather than 'this is a hobby that won't move the employment needle'."*

This is the bet the whole gate exists to test. Phase 1 validates it on paper and with recruiters; Phase 2 proves it in the market with real proof of work.

## Confidence

**High** — Phase 1 is Output-only; both outputs (the research-driven decision and the recruiter validation) are within Julian's control. The market-response bet (does the positioning actually generate traction) is deliberately deferred to Phase 2, where it is tested with real proof of work.

## Future Leverage

A confident "go" activates Phase 2 (skills development + proof of work + profile reposition + the market-response outcome). The go/no-go decision itself protects against sinking months into a low-return hobby (Performance Principle 4: Mandatory Value Gate; Career Principle 3: not a hobby dressed up as a business). The GenAI SA niche, if confirmed, also becomes the content engine for Performance Obj 2 (Key Person of Influence) KPI track.

## Existing Leverage

- [[ai-senior-roles]] — role comparison and gap framing already documented from session research (17 Jun 2026); reduces research effort significantly
- Sabbatical AI OS work (tool-using agents, orchestrated workflows) — partial proof of agentic implementation already exists
- TOGAF, CISSP, CTBME credentials — directly match GenAI SA JD requirements

## Leading Indicators

Market research concludes within the first timebox with a clear, defensible provisional verdict — HK and UK demand confirmed (or not), skills gap mapped, and a credible read on whether the positioning is viable — before recruiter validation begins.

## Effort

**T-shirt size:** XS (5–8h)

## WSJF Scoring

| Component | Score | Rationale |
|-----------|-------|-----------|
| Value | 3 | The go/no-go decision has real standalone value: it either greenlights a high-value path or saves months of wasted development on a hobby. Moderate, indirect, but genuine de-risking value (18 Jun reframe). |
| Time Criticality | 3 | Gradual erosion — Q3 job search dependency is real but no hard deadline this month |
| Risk / Opportunity | 3 | Unblocks one initiative — gates the entire Phase 2 investment decision |
| Job Size | XS = 2 | 5–8h; existing leverage (ai-senior-roles.md, sabbatical work) pulls this below S |
| **Cost of Delay** | **9** | 3 + 3 + 3 |
| **WSJF** | **4.5** | 9 ÷ 2 |

**Note on scoring:** Original draft (17 Jun) scored Value=1 because Phase 1 then included only research + profile reposition with no standalone payoff. The 18 Jun reframe makes the go/no-go *decision* the deliverable, which carries real de-risking value (Value=3). RO stays 3 (gates Phase 2). The Value vs RO split still holds — Value = the decision's own worth; RO = what Phase 2 it gates. See [[feedback-wsjf-double-counting]].

## Rough Work Breakdown

1. Market research (Gemini deep research + Perplexity, reviewed by Claude): job listings HK + UK, market/industry reports, employer/outsourcer landscape → provisional go/no-go verdict (~3-5h)
2. Validate the verdict and hypothesis with recruiters: capture their input on whether GenAI SA positioning materially helps Julian's employability (~1-2h)

## Completed

Nothing completed yet.

## Deliverables
| Deliverable | Size | Hours | Status |
|-------------|------|-------|--------|
| [[../deliverables/genai-sa-market-research\|GenAI SA Market Research]] | 2 | 5-8h | queued |
| [[../deliverables/genai-sa-recruiter-validation\|GenAI SA Recruiter Validation]] | 1 | 1-4h | queued (after research) |

## Funnel

| Item | Intent | Added |
|------|--------|-------|
| GenAI SA: Skills & Proof of Work (Phase 2) | Skills development (LLM patterns, RAG, agentic workflows, governance) + ≥1 published proof-of-work artefact + profile reposition (CV + LinkedIn) + LinkedIn publishing track + the market-response outcome (does the repositioned profile generate real traction). Activates on a "go" verdict from this gate. | 2026-06-17 |

## Links

- **Workstream:** [[../career/_index\|Career]]
- [[genai-sa-pivot-strategy]] — living positioning strategy for the GenAI SA target
- [[ai-senior-roles]] — role market analysis and decision rationale (FDE pivot → GenAI SA)
- [[tti-role]] — downstream project this enables
- [[job-search-pipeline]] — downstream pipeline this feeds; [[clsa-role]] and [[tti-role]] — active bounded opportunities
- [[cv/_index]] — master resume (repositioned in Phase 2)
- **Gates (go verdict activates):** Claude Architect (POR-14) — if this project returns "no-go", Claude Architect stays in the funnel as hobby activity and does not enter the active portfolio
