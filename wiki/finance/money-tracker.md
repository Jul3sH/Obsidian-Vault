---
type: system
updated: 2026-06-21
status: active
---

# Money Tracker

> *Drop bank statements → categorised spend → maintained budget + monthly variance report. The instrument for [[finance-workstream|Finance Goal #2]] (cash-flow neutrality).*

tags: [finance, tracking]

## Purpose

Replace the bank app's manual ~30 min/month categorisation with a low-overhead, AI-driven pipeline that produces the insights the app won't, and feeds active decisions (HK relocation, [[finance-workstream|cash-flow neutrality goal]]).

## Scope (eco-tested & agreed 2026-06-21)

| In scope | Out of scope (until explicitly requested) |
|----------|-------------------------------------------|
| Categorise statement transactions against a learned map | Real-time alerts (batch only — needs bank-API build) |
| Maintain the budget figures in this wiki | Merchant web-research (best-guess + `?` tag instead) |
| Monthly one-screen variance report + flagged breaches | Multi-account reconciliation |
| Learn new merchants over time (map grows, unknowns shrink) | |

## Workflow

| Step | Who | Action |
|------|-----|--------|
| 1 | Julian | Drop bank statement (paste or file) |
| 2 | Claude | Categorise each line against the map; unknown merchant → best-guess + `?` tag |
| 3 | Claude | Update [[budget\|budget figures]]; produce variance report + breach flags |
| 4 | Julian | ~10 min review: confirm/correct `?` items (map learns from corrections) |

**Breach flag** = on upload, Claude raises any category tracking over budget (e.g. "Dining 80% used, 9 days left"). This is the *insight* substitute for the real-time alert that is out of scope.

## Category Map

Statement transactions map to the **15 top-level categories** from [[budget|the budget]] (each carrying a Non-optional / Discretionary split):

`Housing · Tax · Travel · Tuition · Dining · Groceries · Bills · Health & Fitness · Leisure · Medical · Transport · Shopping · Beauty · Savings & Investments · Financial Expenses`

Charity is tracked but currently HK$0/mo. Variance reports reconcile against the **HSBC account lens (HK$61,738/mo)** — not the full economic total — because at-source items (MPF, mortgage-interest split) never appear in HSBC statements.

The learned **merchant → category** mapping lives below and grows with each statement. Unknown merchant → best-guess + `?` tag for review.

| Merchant pattern | Category | Notes |
|------------------|----------|-------|
| *(populated from first statement)* | | |

## Links

- [[finance-workstream|Finance Workstream]] — Goal #2 depends on this
- [[_index|Finance Index]]
