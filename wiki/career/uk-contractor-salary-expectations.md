---
type: reference
tags: [career, uk-relocation, contracting, ir35, take-home]
created: 2026-09-14
status: complete
status-updated: 2026-09-14
---

> **What this is:** the canonical take-home table for UK contract day rates (inside IR35 via umbrella), plus the billable-days assumptions behind the annual figures.
> **Why it exists:** created 14 Sep 2026 when Julian asked what £600/day actually nets. The take-home rows previously lived inside [[uk-ir35-contracting-feasibility-2026]] and were consolidated here so there is one findable numbers surface.
> **How it is used:** read when evaluating any UK contract rate or comparing contract vs permanent. This file holds the numbers; [[uk-ir35-contracting-feasibility-2026]] holds the IR35 status doctrine and recruiter questions. If any other file quotes these figures and disagrees, this file wins and the other is corrected.

# UK Contractor Salary Expectations

## Key Takeaways

- **£600/day at 225 days nets ~£74.8k** (~£6,200/mo), cash-equivalent to a **~£116k permanent salary**, and ~£16.5k/yr short of the £150k-perm benchmark net (£91.3k).
- **£700/day at 225 days nets ~£83.8k** (~£7,000/mo), cash-equivalent to a **~£136k permanent salary**.
- **~£775/day at 220 days is the cash break-even with £150k permanent**, and still worse after pension, medical, life cover, sick pay, and renewal risk.
- Billable days: **230 is the no-sickness planning case**, **220 allows 10 days for sickness and other buffer**, and **225 is the midpoint used as the base case**, allowing 5 days. All headline figures assume zero bench days between contracts, which is the assumption that actually decides whether contracting works.
- Plan on inside-IR35 economics; outside IR35 is upside, not the base case (doctrine in [[uk-ir35-contracting-feasibility-2026]]).

## Billable Days Ladder

| Planning case | Derivation | Billable days |
|---|---|---:|
| Calendar maximum | 261 weekdays in 2026, less 8 England bank holidays and 20 days annual leave | 233 |
| No-sickness planning case | Calendar maximum rounded down for normal non-billable friction | **230** |
| Conservative case | 230 less 10 days for sickness and other buffer | **220** |
| Base case | Midpoint of 220 and 230, allowing 5 days for sickness and other buffer | **225** |

- **230** = Julian's rounded planning case without an explicit sickness or contingency allowance. The exact 2026 calendar maximum is 233, so 230 already absorbs 3 days of ordinary non-billable friction.
- **225** = base case used in the headline rows below: the midpoint, with 5 further days allowed for sickness and other buffer.
- **220** = conservative case: 10 further days allowed for sickness and other buffer. It is also the market-standard divisor to defend in rate negotiation. Never accept a client-proposed divisor without deriving it - a higher divisor is a rate cut in disguise (rule from [[independent-consulting-pricing]]).
- **~190** = utilisation stress case. All figures above assume back-to-back contracts with zero bench days. As of 14 Sep 2026, unverified contractor-market common knowledge puts realistic multi-year utilisation at 80-90%, i.e. ~175-200 days/yr average; validate via recruiter question 9 (contract length and renewal pattern) in [[uk-ir35-contracting-feasibility-2026]] before relying on anything above 220 as an average.

## £600 a Day at 225 Days

**£600 x 225 = £135,000 assignment income. This is not a £135,000 gross salary when the quoted rate is an umbrella assignment rate.** The umbrella pays employer costs from the assignment income before calculating taxable gross pay.

| Step | Annual amount |
|---|---:|
| Umbrella assignment income | £135,000 |
| Less umbrella margin, employer NI and apprenticeship levy | ~£18,600 |
| Taxable gross pay | **~£116,400** |
| Less income tax | ~£37,300 |
| Less employee NI | ~£4,300 |
| Net cash | **~£74,800** |
| Monthly average | **~£6,230** |

For comparison, a genuine £135,000 gross PAYE salary nets about **£83,300** in 2026/27. The ~£8,500 difference exists because an ordinary employer pays employer NI and other employment costs on top of salary, while an umbrella funds them from the advertised assignment rate.

## Take-Home Table (inside IR35, umbrella)

All rows verified 14 Sep 2026 by a single model that exactly reproduces the rows originally published in [[uk-ir35-contracting-feasibility-2026]] (Jul 2026).

| Day rate | Days | Assignment value | Taxable pay | Net cash | Net /month | ≈ Perm equivalent |
|---:|---:|---:|---:|---:|---:|---:|
| £600 | 220 | £132,000 | ~£113.8k | **~£73.8k** | ~£6,150 | |
| £600 | 225 | £135,000 | ~£116.4k | **~£74.8k** | ~£6,230 | ~£116k |
| £600 | 230 | £138,000 | ~£119.0k | **~£75.8k** | ~£6,320 | |
| £700 | 220 | £154,000 | ~£132.9k | **~£82.2k** | ~£6,850 | |
| £700 | 225 | £157,500 | ~£135.9k | **~£83.8k** | ~£6,980 | ~£136k |
| £700 | 230 | £161,000 | ~£138.9k | **~£85.4k** | ~£7,120 | |
| £775 | 220 | £170,500 | ~£147.1k | **~£89.8k** | ~£7,480 | ≈ £150k |
| £775 | 240 | £186,000 | ~£160.6k | **~£96.9k** | ~£8,070 | |
| £850 | 220 | £187,000 | ~£161.4k | **~£97.3k** | ~£8,110 | |

**Benchmark:** £150k permanent salary ≈ **£91.3k net** (2026/27 PAYE + NI, before employee pension contributions).

**Perm equivalent** = the permanent salary producing the same net cash. It overstates contracting: a permanent package adds pension, medical, life cover, sick pay, income protection, and paid notice that contractor cash only weakly replaces.

## Assumptions

- England PAYE, 2026/27 rates; employee NI category A; personal-allowance taper above £100k (the big bite at these income levels).
- Advertised rate treated as the **umbrella assignment rate**, not taxable PAYE rate - always ask the recruiter which it is.
- Umbrella margin £1,300/yr; employer NI at 15% and apprenticeship levy at 0.5% come out of the assignment pot before taxable pay.
- No pension salary sacrifice. Sacrificing into a pension would materially improve the effective position at these income levels (it unwinds the £100k-£125k taper), if cash flow allows.

## Related

- [[uk-ir35-contracting-feasibility-2026]] - IR35 status doctrine, inside vs outside plausibility, recruiter questions
- [[independent-consulting-pricing]] - divisor doctrine and the worked billable-days calculation (HK context)
- [[uk-150k-feasibility-report]] - the £150k permanent target this is benchmarked against
- [[uk-relocation-project]] - project status surface
