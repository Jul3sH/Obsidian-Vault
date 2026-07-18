---
type: analysis
status: living
created: 2026-07-02
currency: mixed (HKD + GBP)
decision: UK Relocation Decision
tags: [finance, uk-relocation]
---

# UK Move - Financial Model (the "£100k bet")

> The money side of the [[decisions/uk-move/_index|UK relocation decision]]. Reframes the choice as a **bet with a stake and a breakeven probability**, not a lifestyle comparison. Built 2026-07-02 from Julian's 12-month expense history + the [[financial-status-2026-06-22|June 2026 financial status]]. Feeds the [[decisions/decision-journal|Decision Journal]]. The beliefs are tested ([[decisions/uk-move/b1-relationship-belief|B1]], [[decisions/uk-move/b7-lifestyle|B7]]); **this is now the deciding analysis.**

## 0. Canonical Summary: Burn & Runway (SINGLE SOURCE OF TRUTH)

> **In plain English (read this first):** Cost of living is a **wash** - HK and the UK come out about the same, slightly more expensive in London once settled, but **cheaper in London while job-hunting** (the DB flat and Sophia's private school both vanish: own home in London = forgone rent not a rent bill, and UK state school is free). The move also **unlocks the MPF (~£124.5k, otherwise locked until 65), so the runway roughly doubles**. The catch: the MPF is the only private pension, so living off it is spending retirement - which is the whole London-vs-Malvern question (London eats it fast, Malvern preserves it). **The money was never the reason to move or stay - it is neutral. The decision rests on how likely a well-paid HK job really is (low) and the life wanted (Sophia settled, near Mum).**

> **✅ CLARIFIED 14 Jul - tenant treatment is CONDITIONAL on the option (Julian).** The two options are mutually exclusive uses of Cecil Road: **London-direct → live in Cecil Road (Wimbledon), tenants out, no rent income and no rent bill** (only the £213/mo mortgage); **Malvern → tenants stay, Cecil earns +£2,194/mo.** So the London column below (housing = forgone rent) is **correct as modelled**. The overnight [[uk-relocation-fable-consistency-review-2026-07-13|Fable review]] flagged a "DEC-3 collision" because the **RAID register recorded "keep tenants to Aug 2027" as *unconditional*** and said London-direct would need a year of paid London rent - that framing presumes Malvern and is being corrected to conditional. Residual London-direct housing cost = only the short temp-accommodation bridge while tenants serve notice (the £0-6k line in §10), **not** a year of rent. Still to fix: the Stay-HK pot basis (should drop the unbanked £12,475 rebate).

> **This is the authoritative money surface for the UK move. Sections §1-§12 below are the derivation and history that feed it. If any number, in this file or any other, disagrees with this table, THIS TABLE WINS and the other must be corrected to match.** Last reconciled 2026-07-13 from §1, §8-§11 and the [[fable-review-jobdata-2026-07-11|11 Jul Fable red-team]]. Supporting docs: [[uk-vs-hk-income-floor-reconciliation-2026-07-09|income-floor reconciliation]], [[financial-status-2026-07-07|financial status]], [[job-market-analysis|job-market analysis]] (salary inputs).

### The three options at a glance

| | Stay HK (baseline*) | Move: London-direct | Move: Malvern crash-pad interim |
|---|---:|---:|---:|
| **Search-phase net burn/mo** | **~£6,700-7,500** | **~£4,630** | **~£2,450-2,700** |
| Honest / upper end | £7,500 (12-mo mean) | £5,450 (settled, once employed) | £2,700 (top of range) |
| Optimistic floor | £6,700 (6-mo trend) | £4,630 (lean search) | £1,683 (excl. board + car) |
| **Liquid pot at start** | **~£82,500** | **~£50,000** | **~£55,000** |
| MPF pension buffer | **LOCKED to age 65** | +£124,500 on departure | +£124,500 on departure |
| **Liquid-only runway** | **~11-12 mo** | **~11 mo** | **~20-22 mo** |
| Runway incl. MPF | n/a (locked) | ~2.7-3.2 yr | ~5.5-6 yr |
| Pension fallback if search runs long | **None** | Yes (spends retirement) | Yes (largely untouched) |

\*MOVE is already committed (§9), so Stay HK is the superseded baseline, kept for reference. The **live decision is London-direct vs Malvern interim.**
Sources: burn - §1 (HK), §10 UPDATE (London), §9b (Malvern honest); pots - §10 derivation; MPF - §10.

### How each burn is built (auditable)

- **Stay HK ~£6,700-7,500/mo:** full HK outgoings £8,400 (6-mo trend) to £9,200 (12-mo mean) [§1], **less** Cecil Road net rent +£1,730 [§8/§9]. He lives in the DB flat (its cost is already inside the HK burn). No MPF access and no move costs, so it has the largest liquid pot but the weakest *effective* safety, because the pension is locked away.
- **London-direct ~£4,630/mo (search) → £5,450 (settled):** lives in Cecil Road, which he **owns** - so London's housing cost is *forgone rent*, not a rent bill. Search figure is the lean tier; the settled figure adds a cleaner (£460), babysitting (£215) and a car (£225) once life normalises [§10 UPDATE]. Includes the −£970/mo DB-flat rental shortfall [§11].
- **Malvern crash-pad ~£2,450-2,700/mo (search):** lives at Mum's, rents Cecil out (+£2,194). Honest figure adds board ~£500, a car ~£225 (rural, near-essential) and Sophia's interim schooling ~£50 to the £1,683 floor [§9b]. The London crash-pad (~£1,083/mo) is a **cost of earning** - it begins only once a job exists and is paid from salary, not the runway.

### Why London costs more than Malvern (the point that keeps resurfacing)

It is **not** housing. Because Julian owns both homes and both are let in the move scenarios, ongoing housing cost is near-identical: HK-stay net property cash ~£1,172/mo vs London ~£1,231/mo - **~£59/mo apart** [[uk-vs-hk-income-floor-reconciliation-2026-07-09|income-floor reconciliation]]. The London-vs-Malvern gap (~£2,000/mo) is driven by: **forgone Cecil rent** (£2,194 given up by living there instead of letting it), **higher London living costs** for a man + teenager, and **paid help** (cleaner + babysitter) that Mum's presence removes in Malvern. The **car** was the correction that resurfaced most often: it belongs in **both** move scenarios (rural Malvern needs one too), not London only.

### "Is London burn higher than HK?" - the reconciliation

Depends what you strip out, which is why it keeps causing confusion:

| Comparison | Result |
|---|---|
| London total burn (£4,630-5,450) vs **HK total net drain** (£6,700-7,500) | **HK is higher.** London is the cheaper place to live, all-in. |
| London total burn (£4,630-5,450) vs **HK residual** (£4,900 = HK burn *minus* housing £2,900 *minus* tuition £650 [§1]) | **Level.** London settled (£5,450) is slightly above; London lean (£4,630) slightly below. |
| London (£4,630-5,450) vs **Malvern** (£2,450-2,700) | **London is higher** - this is the true "London is more expensive" finding, and it is vs Malvern, not vs HK. |

**So: on total burn London is cheaper than HK; on non-housing lifestyle they are level; London is only "more expensive" relative to Malvern.** Any doc claiming "London > HK" on total burn is using the old £4,550 London figure or comparing against HK residual - correct it against this table.

---

## 1. The real HK burn rate (corrected)

Julian's working assumption was ~100k HKD/month. The 12-month actuals (Jul 2025 - Jun 2026) say it's **lower and falling**:

| Metric | HKD/month |
|---|---:|
| 12-month mean | **92,196** |
| 12-month median | 90,164 |
| First 6 months (Jul-Dec 2025) | 100,452 |
| **Last 6 months (Jan-Jun 2026)** | **83,940** |
| Range | 65,371 - 121,284 |
| **Annualised (12-mo mean)** | **1,106,351 (~£110k @ 10:1)** |

**Findings:**
- The "100k/month" figure was an **overestimate**. Real run-rate is ~92k, and the **recent trend is ~84k** - the expensive months (Aug/Sep/Oct 2025, 108-121k) are behind him; 2026 is calmer (65-98k).
- **Annual burn ≈ 1.1M HKD ≈ £110k.** This is the **stake**: every year spent unemployed in HK betting on a role burns ~1.1M of liquid savings. The "£100k bet" framing holds (it's ~£110k).
- Note the tension with "I live simply in HK": 84-92k/month is **not** a simple-living number. Whatever the root cause (Sophia costs, flat, no contribution from [[../relationships/clodagh|Clodagh]]), the lifestyle he under-uses (see [[decisions/uk-move/b7-lifestyle|B7]]) still costs ~£1k/week.

### HK expense breakdown by category (7 Jul, stated monthly averages)

| Category | HKD/mo |
|---|---:|
| Dining | 10,000 |
| Groceries | 9,000 |
| Beauty | 1,000 |
| Health & fitness | 500 |
| Leisure | 3,000 |
| Travel | 5,000 |
| Bills | 6,000 |
| **Housing** | **29,000** |
| Medical | 1,000 |
| Transport | 3,000 |
| **Tuition** | **6,500** |
| Financial expenses | 800 |
| **Category total** | **74,800** |
| *Actual mean (12-mo)* | *92,196* |
| *Actual trend (6-mo)* | *83,940* |

**Gap (~9-17k HKD/mo):** irregular spending not captured in monthly estimates - holidays, one-off purchases, lumpy school fees. Actuals are more reliable for runway planning; categories are more useful for mapping what survives the move.

**What evaporates in the UK (structural, not lifestyle):**

| | HKD/mo | £/mo |
|---|---:|---:|
| Housing (Cecil Road owned, mortgage in model) | 29,000 | 2,900 |
| Tuition (UK state school is free) | 6,500 | 650 |
| **Total structural saving** | **35,500** | **3,550** |

£3,550/mo (~£42,600/yr) disappears the moment Julian lands in the UK, before any lifestyle adjustment. Residual HK categories at recent trend: ~49k HKD/mo (~£4,900/mo). UK equivalents for those remaining categories will be lower on most lines (groceries, medical on NHS, bills).

## 2. The UK baseline (the alternative's floor)

From [[financial-status-2026-06-22|June 2026 status]]:

- UK property is **cash-flow positive: +£1,814/month** net (≈ +18k HKD/mo) after mortgage, fees, tax provision.
- School free (state system). MPF **~1M HKD unlocks** on leaving HK (one-off liquidity). Interferon continues on the NHS (see [[decisions/uk-move/analysis|A9]]).
- **UK downside is capped.** Living at mum's, property income covering a chunk of costs, near-zero incremental housing → the UK path does not bleed the stake. It trades upside (HK low tax) for **damage limitation + stability**.

## 3. The bet structure

The decision is not "HK vs UK lifestyle." It is:

> **What is P(landing well-paid HK work within the runway), and does the expected prize beat the ~1.1M/yr stake?**

**Two strategies:**

| | STAY & bet (HK) | MOVE (UK controlled) |
|---|---|---|
| Cost | Burn ~1.1M HKD/yr while searching | Near-zero net; property surplus offsets |
| Upside | **Land 1.2-1.8M HKD role @ ~15% tax** → HK wins decisively; pay down flat + fund retirement in ~5 yrs | Steady, lower-tax-disadvantaged; builds the consulting/own-business future he wants |
| Downside | Burn the runway, land nothing, **forced to move anyway** - older, less capital, same UK market (the [[decisions/commitment-avoidance|drift]] failure mode) | Forgoes the HK tax upside; misses the sun (see B7) |

**The prize, quantified.** The HK advantage is *tax*, and it only exists if equivalent income is landed. On a ~1.5M HKD gross role:
- HK (~15% effective) → take-home **~1.275M HKD**
- UK (~45% effective incl. NI at ~£150k) → take-home **~820k HKD**
- **Advantage ≈ 450-525k HKD/year, but only conditional on landing the role in HK.**

## 4. Breakeven probability (the key output)

Instead of guessing P, solve for the P at which staying and moving are financially equal. Illustrative one-year bet (runway ≈ 12 months at ~92k; assumes ~1.1M savings - **to confirm**):

- Expected cost of the HK experiment ≈ (1−P) × 1.1M (full-runway burn, no job) + P × 0.55M (burn until landing mid-year)
- Expected prize ≈ P × ~1.75M (risk-discounted PV of ~5 years of the tax advantage)

Setting them equal:

> **Breakeven P ≈ 45-50%.**

**Interpretation:** staying only pays if Julian's *honest* probability of landing a well-paid HK role within his runway is **roughly a coin-flip or better.** Below that, the controlled UK move is the higher-expected-value choice.

**The gut-check:** given his own stated inputs - **weak HK network**, embarrassment/ADHD-RSD blocking outreach ([[decisions/uk-move/analysis|A1]]), the "old white guy" market concern (B4), and an **emerging-not-specialist** architect profile - is his real P above 50%? If he can't honestly say yes, the model says move.

## 5. The behavioural rider (non-negotiable)

The model exposes that **"Stay HK and drift" is the single worst cell**: it pays the full ~1.1M/yr stake at P≈0, because the networking offensive isn't actually being run. Therefore:

- **Staying is only defensible as an *active, deadlined* bet** - a full-send networking campaign with a drop-dead date and a pre-committed "if no signal by X, I move." Never as a default.
- This is the [[decisions/commitment-avoidance|commitment-avoidance]] trap in financial form: the passive option silently burns £110k/yr while feeling like "not deciding."

## 6. Inputs to sharpen this (optional - the answer likely holds without them)

1. **HK liquid savings balance** → finalises the runway (months = savings ÷ 92k). *(HK account still blank in [[financial-status-2026-06-22|status]].)*
2. **Julian's honest P(well-paid HK work)** → compare against the ~45-50% breakeven. Or accept the breakeven as the target to interrogate.
3. **Realistic HK salary + effective tax** for his actual profile → sharpens the prize (§3).

None of these are likely to move the structural conclusion: **the stake is ~£110k/yr, the downside of staying is unbounded (drift) while the downside of moving is capped, and staying needs a ~50% hit-rate to justify itself.**

## 7. Update (4 Jul): income portability improves the MOVE column

A new insight materially improves the MOVE side: Julian's income-generation is **location-independent**. The live TTI opportunity (via Stephan to Ty) is a **remote, US-aligned consulting engagement** deliverable from anywhere, and *better from a UK base* (London/US timezone beats HK/US). So the MOVE column's income is no longer property-surplus-plus-speculative: it gains a **warm, near-term income bridge** (TTI's default initial six months). This **raises MOVE's expected value, caps its downside further** (the move-and-drift-with-no-income worst case is bridged), and therefore **raises the P(large HK role) that STAY must clear**, since the modest engagement is location-flexible and creates no HK-specific tax advantage. Caveat: TTI is a pitch, not yet landed, and an initial six months is a bridge not the S1 jackpot - but the structural point holds even without TTI, since remote US/UK consulting means moving does not forfeit earning capacity. Full working: [[income-portability]].

## 8. Update (4 Jul, corrected 9 Jul): lower-paid HK roles weaken but do not resolve the model

Julian has now checked the lower end of the HK market. Lower-paid roles available to his profile pay around **100,000 HKD/month gross**. After tax (~15%), net is roughly **85,000 HKD/month**.

**Correction from [[uk-vs-hk-income-floor-reconciliation-2026-07-09]]:** the earlier wording was too pessimistic because it compared HK income against HK burn without consistently offsetting Cecil Road rent. If Julian stays in HK and rents Cecil Road out, the net rent offset is roughly HK$17,360/mo. On that basis, a HK$100k/month gross role is **survivable**, not unlivable: the first-pass spreadsheet shows roughly HK$18k/mo surplus against recent actuals and roughly HK$10k/mo surplus against 12-month mean actuals.

**The narrower structural finding:** HK$100k/month is a weak recovery floor. It may stop or reduce drawdown, but it is not an obviously strong retirement-rebuilding or DB-flat-repair path. It is materially worse than a true senior HK role, but it is not the same as drift.

**Why the burn is where it is - the Clodagh contribution removal.** The burn rate of ~92k/mo (trending 84k) is not primarily lifestyle inflation. It reflects costs that were previously shared: Sophia's schooling, a domestic helper, flat running costs. When [[../relationships/clodagh|Clodagh]] stopped contributing (she chose to leave; now in UK), those costs fell entirely to Julian. This is the structural break: the same HK lifestyle that was financially sustainable with two contributors is not sustainable with one at a non-premium salary.

**What this means for S1:** S1 (HK corporate) should distinguish two HK outcomes:

| HK role level | Read |
|---|---|
| ~HK$100k/mo gross | Survivable with Cecil Road rent offset, but a weak recovery floor. |
| ~HK$125-150k/mo gross | Proper senior recovery path, better able to rebuild safety. |

The model's P(landing) = 30-50% should therefore be read as P(landing a **senior, recovery-quality** HK role), not P(landing any HK job). Julian's own read: the odds of landing at the premium end are low.

**Net effect on the decision:** open pending adversarial review. This correction narrows the UK floor advantage and removes the over-claim that HK$100k/month does not cover life. It does not by itself make HK the better choice, because the role must still be landed in a cooling market and the surplus is thin. The next step is to adversarially review the reconciliation workbook before changing the headline relocation verdict.

## 9. Update (7 Jul): London vs Malvern - the two-scenario burn model

The MOVE direction is now committed. The live decision is **where to land: London vs Malvern** (= the S4-vs-S3 sequencing fork wearing geography). Full decision context: [[decisions/uk-move/_index|workspace]].

**Critical structural fact (corrected 7 Jul): Cecil Road is the London property.** The two scenarios are mutually exclusive uses of the same asset:
- **Malvern:** rent Cecil Road out → **+£2,194/mo take-home**; live at Mum's (the cushion).
- **London:** live in Cecil Road → **£0 rent income, but £0 rent to pay** (owned); only the £213/mo mortgage.

So **London's true cost is the forgone rent, not a new rent bill.** Julian cannot be priced out of London - he already owns the home there. This de-risks the London option versus a rental-market assumption.

### Cecil Road P&L (corrected 7 Jul, from May 26 statement)
| Item | £/mo |
|---|---:|
| Rent charged | 2,500 |
| Management fee (Brinkleys, 10.8% incl VAT) | −270 |
| Rent protection insurance | −36 |
| **Take-home rent** | **2,194** |
| Mortgage payment | −213 |
| Buildings insurance (£550/yr) | −46 |
| Rental income tax (Malvern case, see below) | ~−210 |
| **Net property income (Malvern only)** | **~+1,725** |

**Rental tax (Malvern / unemployed case):** taxable profit = £2,194 × 12 = **£26,328/yr**. Personal allowance (£12,570) shelters the first slice → taxable £13,758 → 20% = **£2,752/yr**; less ~£360/yr mortgage-interest credit → **~£2,400/yr (~£200/mo)**. *Note: higher than Julian's £1-2k estimate, because the £26k rent sits well above the personal allowance so £13.8k is taxed at 20%.* In the **London case there is no rental income and therefore no rental tax** - the house is his home.

### Net monthly burn by scenario (living-cost rows are estimates - to confirm)
| £/mo | Malvern (rent out, at Mum's) | London (live in Cecil Road) |
|---|---:|---:|
| Rent income | +2,194 | 0 |
| Mortgage | −213 | −213 |
| Buildings insurance | −46 | −46 |
| Rental tax | −210 | 0 |
| Board at Mum's | 0 (Mum absorbs; could contribute) | 0 (owned) |
| AI subscriptions (Claude £18 + ChatGPT £20) | −38 | −38 |
| Living costs (est., **re-baselined 7 Jul** - see note) | −2,400 | −3,283 |
| **Sub-total (UK life only)** | **~−713** | **~−3,580** |
| **DB flat rental shortfall (held & let, see §11)** | **−970** | **−970** |
| **Net monthly (cash)** | **~−1,683** | **~−4,550** |

*(Re-baselined 7 Jul after Fable review: the prior London living figure (£2,162) was flagged as 40-60% light vs Julian's HK actuals (residual ~£4,900/mo; §1 documents a HK$9-17k/mo estimate-vs-actual gap). Honest London living for a man + teenager ≈ £3,000-3,500/mo; Malvern ≈ that less council tax/utilities Mum absorbs. **Still an estimate - itemisation is an open item.** Prior arithmetic fix also stands: earlier London sub-total −2,672 double-counted £213.)*

**Read (honest, updated 10 Jul):** Malvern draws ~£1,683/mo cash, London ~£4,550/mo after correcting Cecil Road to Band E council tax and treating the DB letting agency fee as a one-off rather than a recurring monthly cost. **~£1,369/mo of the DB payment is principal (equity), so net-worth burn is that much lower** - Malvern is roughly net-worth-neutral. The London-vs-Malvern delta is ~£2,867/mo. **First year in London ≈ £55k cash + £10-20k one-offs (temp accommodation, shipping, furnishing, DB letting agency fee) ≈ £65-75k.** A 12-18 month search is covered several times over by the runway (below), but plan for the higher number, not the flattering one.

### The runway test (open - gated on HK savings)
Runway = HK liquid savings ÷ London net burn. Every ~£31k funds ~12 months of London search. The ~£100k MPF unlock is a large secondary buffer but is retirement capital, preferably not burned on living costs.

**Decision rule:** if HK liquid savings *alone* cover a realistic search (~12-18 months London burn, £31-47k) with a reserve Julian won't panic below → **London clears.** If not → **Malvern's cushion wins.** TTI bridge (if it lands ~£4-6k/mo for 6 months) covers London burn *entirely* during the search and effectively removes the constraint.

**Still needed:** (1) ~~HK liquid savings - resolved §10~~; (2) confirm Cecil Road suits Julian + Sophia (size, area, school catchment, clubs, transport); (3) TTI firmness; (4) Cecil Road outstanding mortgage balance (to model MPF payoff).

### 9a. The crash-pad interim (de-risking bridge) - added 11 Jul

**The scenario Julian is actually proposing** (was not previously costed). Not "Malvern vs London" as end-states, but **Malvern as an interim de-risking base with a London crash-pad**, then a full London move later:

1. Land in Malvern: rent Cecil out (+£2,194/mo), live at Mum's (rent-free, no bills, no car-on-road). Search from the low-burn base.
2. **Mum looks after Sophia**, which is what makes the commute feasible (removes the sole-parent overnight-care blocker).
3. Take a **London hybrid job** (the [[uk-job-market-remote-hybrid-split-2026-07-11|job data]] shows ~40%+ of London roles are hybrid, so this pool is large and crash-pad-reachable; only the ~1/3 on-site-only London roles are excluded). Commute "TWaT" (Tue/Wed/Thu), crash-pad in London those nights.
4. Once the job is **stable** and at the **end of the education year**, move the family to London full-time (transition to the §9 London P&L: live in Cecil, forgo rent, no crash-pad).

**Crash-pad cost (Julian's estimate, 11 Jul):**
| Item | £/wk | £/mo (×4.33) |
|---|---:|---:|
| Train (Malvern-London return) | ~100 | ~433 |
| Accommodation (3 nights, Mon/Tue-Thu buffer) | ~150 | ~650 |
| **Total crash-pad** | **~250** | **~1,083** |

*(Budgeted at 3 nights in case of a Monday start; 2 nights is often achievable, which would cut it to ~£175/wk / ~£760/mo. Train figure assumes a weekly/flexible fare, not peak walk-up; a season ticket may change it. Estimate - to firm up.)*

**Why this is a de-risking bridge, not just a cost line:**
- **The crash-pad cost is a cost-of-EARNING, incurred only once a job exists.** During the job **search** (no job yet), there is no crash-pad and the burn stays at the Malvern rate (~£1,683/mo cash), not the London rate (~£4,550/mo). This directly mitigates the #1 risk: *large capital moved to the UK, then burning fast with no job.*
- **Once employed**, burn is ~£1,683 + ~£1,083 = **~£2,766/mo**, but a £75-95k+ salary covers that many times over - the position turns strongly cash-positive. The crash-pad is paid out of salary, not runway.
- **Sophia's transition is timed to a school-year boundary** (one clean Malvern-to-London move at year-end), not mid-year, and is cushioned by grandma during the interim. It does still add one extra transition vs London-direct (HK to Malvern to London = two moves vs one) - that residual is the honest cost to weigh against the money de-risk.

**Comparison (search phase, no income):**
| | Malvern-interim (searching) | London-direct (searching) |
|---|---:|---:|
| Monthly cash burn | ~£1,683 | ~£4,550 |
| Months per £31k of runway | ~18 | ~7 |

**Open risks to weigh (for the pending Fable re-review):** the extra Sophia transition; Julian away Tue-Thu (grandma covers, but midweek absence from a teenager); **mum-dependency as a single point of failure** (her health/availability); duration-drift if "stable job + year-end" keeps slipping (needs a pre-committed move-by trigger); and whether target hybrid roles genuinely allow a 2h30 base (most do at 2-3 anchor days).

**Runway comparison:** see the canonical [§0 Burn & Runway summary](#0-canonical-summary-burn--runway-single-source-of-truth) at the top of this file. Headline at the honest burns: London-direct exhausts the ~£50k pot ~month 11 (then into MPF); the Malvern interim runs ~20-22 months on liquid before touching the pension.

### 9b. Fable red-team corrections to §9a (11 Jul) - the honest, hostile numbers

Fable's hostile red-team ([[fable-review-jobdata-2026-07-11]] §10) demoted the interim and corrected §9a's flattering figures. Use these as the planning numbers:

| §9a claim (optimistic) | §9b honest / hostile figure | Why |
|---|---|---|
| Malvern search burn ~£1,683/mo | **~£2,450-2,700/mo** | Adds board at Mum's ~£500 (£0 is neither realistic nor decent for a year), a car ~£225 (rural Malvern, near-essential - the same asymmetry the 10 Jul review caught), and Sophia's interim-schooling ~£50 amortised. Plus a one-off second-move cost not in either figure. |
| Runway edge "~18 vs 7 months per £31k" | **~12-13 vs 7 months** | Follows from the honest burn. Still a real, material advantage - just ~30% smaller than §9a implied. |
| Reachable London hybrid pool ~40% | **~25%** | Once fixed-anchor-day and client-site roles are stripped - and Julian's best-fit lane (SI presales) is customer-facing, so this bites hard. Still far above the 15% resident figure, but the job-access edge is smaller and the search is longer. |
| Crash-pad ~£1,083/mo (train £100 flexible) | Train likely **above** estimate at peak/season-ticket rates; midweek room cost unverified | To firm with real quotes. |
| Transition trigger: "stable job + year-end" | **A slippage engine** | §10.4: the success path itself (a good job landed at ~month 5 + ~6mo to "stable") pushes the exit past the Jul-Aug 2027 window into **summer 2028 (~2yr, Year-10/GCSE-adjacent start)**. Only a hard, signed, tenancy-enforced move-by fixes it. |
| Sophia-midweek: a "residual to accept" | **A design constraint / primary kill-shot** | §10.1 + [[sophia]]: it deletes her non-negotiable bedtime anchor 3 nights/wk and she suppresses distress "for Dad", so the plan is blind to its own largest cost. Needs max 2 fixed nights, guaranteed Thu-Mon presence, a named Malvern secondary attachment, and external monitoring - not a signature. |

Two structural failure modes §9a omitted entirely: **Mum as a single point of failure** with no non-collapsing fallback (month-4 failure forces an emergency London move into a let-out Cecil - worse than any London-direct failure), and the **operational tenancy spine** (funding needs Cecil let; exit needs dated vacant possession, which Renters' Rights / Section 21 abolition may make undeliverable - verify with a letting agent + property solicitor before the interim is admissible).

**Net:** the interim's runway advantage survives hostile costing (still ~£1,900-2,100/mo saved during search, so the money-risk case is real given the tight ~£50-56k pot), but the interim is admissible only in the five-condition hardened form, and is beaten by London-direct if the Sophia/Mum/tenancy conditions cannot all be met or if the pot is topped up (e.g. by banking the rebate).

## 10. Assets, runway, and MPF tax timing (7 Jul)

### Liquid assets

| Asset | HKD | £ (~10:1) | Notes |
|---|---:|---:|---|
| HK savings | 700,000 | 70,000 | Confirmed |
| Tax rebate (anticipated) | 124,748 | 12,475 | Per tax statement |
| **Total liquid** | **824,748** | **~82,500** | |
| MPF pension (Principal + Sun Life) | 1,244,699 | ~124,470 | Confirmed |
| **Total incl. MPF** | | **~206,945** | If withdrawn on departure |

### London runway test

**Julian's decision floor (stated 7 Jul):** never touch the ISAs (~£326.6k, his de-facto pension); never sell either property. The **spendable pot before that floor = non-ISA liquid (£91,869) + MPF (£124,470) = ~£216,339.**

| Scenario | Spendable pot | Cash burn | Runway before floor |
|---|---:|---:|---:|
| **London**, non-ISA liquid only | £91,869 | £4,550/mo | **~20 months** |
| **London**, liquid + MPF | £216,339 | £4,550/mo | **~48 months (~4.0 yrs)** |
| **Malvern**, non-ISA liquid only | £91,869 | £1,683/mo | **~4.5 years** |
| **Malvern**, liquid + MPF | £216,339 | £1,683/mo | **~10.7 years** |

**Result: London still clears comfortably.** Within Julian's own red lines (keep both properties, never touch ISAs), London is funded for **~4 years with zero income** - covering even a long 12-18 month search several times over. Net-worth depletion is slower still (~£1,369/mo of burn is DB principal/equity). Caveats made honest (Fable, 7 Jul): the runway *spends the MPF* (his only private pension → ISAs then carry retirement); real runway is 21 months on liquid until the MPF actually lands (withdrawal has execution + timing risk); the £12,475 tax rebate is anticipated not banked. **The financial question is closed in London's favour, but on ~4 years not ~5; the decision rests on non-financial grounds + execution (school place, tenancy timing).**

> **⚠ UPDATE 2026-07-10 - corrected pot + burn collapse the London liquid runway; London-vs-Malvern REOPENED, leaning Malvern-first.** Two inputs this section rested on have changed, both verifiable:
> - **Landing pot is ~£50-55k liquid, not £91.9k.** Pre-move HK burn + moving one-offs draw it down by departure (planned **end-July**). MPF (£124.5k) still unlocks on leaving, but it is the *only* private pension - spending it is spending retirement.
> - **Honest London burn is ~£5,450/mo settled (£4,630 lean-search), not £4,550.** The old figure omitted a car and realistic paid help: cleaner 8h/wk £460 + babysitting 4h/wk £215 + car £225/mo, at Wimbledon rates. Full working: [[uk-vs-hk-income-floor-reconciliation-2026-07-09]].
>
> **Corrected liquid-only runway (pension preserved):**
>
> | Scenario | Burn/mo | Liquid-only (£50-55k) | Incl. MPF (£175-180k) |
> |---|---:|---:|---:|
> | London settled | £5,450 | **~9-10 mo** | ~2.7 yr |
> | London lean search | £4,630 | **~11-12 mo** | ~3.2 yr |
> | Malvern | £1,683 | **~2.5-2.7 yr** | ~8.6 yr |
>
> **This overturns "London still clears comfortably."** On realistic numbers London funds *under a year* on liquid alone - below a normal 12-18 month search - so London **forces** an early MPF/pension drawdown. Malvern preserves the pension through a multi-year search. The load-bearing reason London beat Malvern on 7 Jul (a ~20-month liquid runway) no longer holds. **London-direct is formally REOPENED** ([[decisions/decision-journal|journal]] 2026-07-10); leaning **Malvern-first** as the risk-mitigating base. The MOVE-to-UK decision itself is unchanged.
> - **Anti-drift design (answers "don't get stuck at Mum's forever"):** Malvern-first is only safe as a *bounded, committed sequence*. The **Cecil Road tenancy length is the structural London-transition trigger** - let it ~12 months and it frees up in exactly a year, at which point Julian moves into his own London home by default; extending the Malvern stay becomes an active, dated, written decision (re-letting Cecil), not a silent slide. The large runway is what *enables* holding out for a good London job rather than being trapped by money.
> - **Conditions to confirm:** remote / West-Corridor job-access works from Malvern (it takes on-site London roles off the table during the search); Sophia's preferred London school realistically reachable on the transition (do not bank it). Pending Fable review.

### Landing-pot derivation (11 Jul) - bridging £91,869 → ~£50-56k

Fable flagged the ~£50-55k landing pot as asserted-not-derived (the single most decision-relevant open number). Bridge from the 7 Jul non-ISA liquid to the pot actually available at departure (planned end-July):

| Component | £ | Note |
|---|---:|---|
| Non-ISA liquid (7 Jul) | 91,869 | HK savings £70,000 + UK current a/c £9,394 + anticipated tax rebate £12,475 |
| − HK tax rebate not yet banked | (12,475) | Anticipated, not received; exclude until it lands. **Swing factor 1** |
| − Pre-move HK burn (mid-Jul → end-Jul departure) | (~6,500) | ~3 weeks at ~£8.5k/mo HK burn; more if departure slips to Aug |
| − Moving one-offs (location-independent) | (~15,000) | Sea freight ~£8-10k + family flights ~£2.5k + DB letting agency fee £1,100 + initial furnishing ~£2-4k. **Swing factor 2** (open item 6, still estimates) |
| − Temp London accommodation (LONDON-DIRECT only) | (0 to −6,000) | Sept-Nov before Cecil frees up; the **Malvern interim avoids this**, so its landing pot is ~£3-6k higher |
| **Landing pot at departure (banked)** | **~£50-57k** | Consistent with the ~£50-55k working figure. Malvern-interim at the top of the range, London-direct at the bottom |

**Two levers move it materially:** **(1)** if the **£12,475 rebate banks before departure**, the pot jumps to **~£62-69k** (chase it - the single cheapest way to firm the London case); **(2)** the moving one-offs are still estimates (open item 6) - a firm shipping quote could move the pot ±£5k.

**What the derived pot means for the decision:** at **~£50-56k the pot does NOT comfortably fund a London-direct search.** Per the canonical [§0 Burn & Runway summary](#0-canonical-summary-burn--runway-single-source-of-truth), London-direct funds only ~11-12 months on liquid (below a normal 12-18 month search → forces an early MPF/pension drawdown), while the Malvern interim funds ~20-22 months on the honest £2,450-2,700 burn. The derived pot sits **above** Fable's ~£45k "interim clearly wins" floor but **below** a comfortable London figure - so **the money-risk axis stays live and the interim's rationale is not dissolved.** The pot derivation confirms, rather than removes, the interim's core advantage. (Note the interim's pot is also slightly *larger*, since it skips the temp-accommodation cost.)

### MPF: rules and timing (CRITICAL - act before departure)

**If Julian stays in HK:** MPF locked until age 65. Cannot access.

**If Julian leaves HK permanently:** can withdraw the full balance as a lump sum.

> **✅ RESOLVED 2026-07-10 - MPF withdrawal does NOT affect HK PR (HK-immigration side only).** Immigration lawyer **John Francois Harvey** (via Justin, 8 Jul WhatsApp): *"MPF withdrawal has no impact on PR status. Just make sure that he shows up every three years."* This clears the feared PR-loss risk on the withdrawal, and confirms HK PR stays live with a visit roughly every 3 years - so HK remains a genuine fallback (the move is more reversible than feared). Underlying rule: a non-Chinese HK permanent resident loses *right of abode* after 36 continuous months of absence but typically retains *right to land* (can still live/work), so a missed visit is not catastrophic. **Two caveats:** (1) this is the HK-PR side ONLY - it says nothing about the **UK-tax** treatment of the withdrawn sum (the tax-timing risk immediately below remains open and is the more expensive mistake); (2) it is a two-line message relayed via a third party - get it in writing from the lawyer directly and confirm which right (abode vs land) is meant.

**Tax timing risk - this is the most time-sensitive financial action in the move:**
- HK has zero capital gains tax. Withdrawal while HK-resident = **tax-free**.
- UK taxes global capital gains from the date of UK tax residency. Withdrawal after arriving in UK permanently = **potentially taxable on the gains element**.
- This is a one-way door: UK tax residency cannot be undone retrospectively.
- **FIG may relax this urgency (see §12):** if Julian qualifies as a new resident, foreign income/gains are UK-exempt for 4 years, which *may* cover an MPF withdrawal made after arrival - but pension lump-sum treatment is specific (UK-HK treaty pension article) and not certainly a "gain." **Do not rely on FIG for the MPF; the safe default remains withdrawing before/early. Confirm with the adviser.**
- **Action required:** initiate MPF withdrawal *before* departing HK permanently. Processing takes time - do not leave this until the day before.
- **Professional advice needed before acting:** the UK-HK double tax treaty treatment of MPF (pension scheme vs investment vehicle) and the precise point UK residency begins affects the exact liability. A one-off tax consultation (~£500) could save a five-figure mistake.

### Cecil Road mortgage (confirmed 7 Jul)

| Field | Value |
|---|---|
| Outstanding balance | £54,264 |
| Type | **Interest-only** (no principal being repaid) |
| Rate | 4.74% variable |
| Monthly payment | £213.08 (pure interest) |
| Term remaining | 7 yr 2 mo (matures ~Sept 2033) |
| **Balloon due at term** | **£54,264** (full principal, interest-only) |

Because it is interest-only, the £213/mo buys nothing but time - the full £54,264 is owed as a lump in 2033 regardless.

### MPF deployment options (post-withdrawal)

1. **Pay off Cecil Road mortgage (£54,264).** Eliminates the £213/mo interest = **£2,556/yr saved, a guaranteed risk-free 4.74% return**, and clears the £54,264 balloon due in 2033. To beat this, keeping the MPF invested must return >4.74% *after* UK CGT (which now bites as a UK resident) - a real hurdle for a guaranteed-vs-risky comparison. Net effect: Malvern position improves materially; **London net burn falls to ~£4,337/mo**, so liquid-only runway is still ~21 months. Caveat: in the Malvern (rent-out) case, paying off loses the ~£511/yr mortgage-interest tax credit, but the £2,556 saving dwarfs it (net +£2,045/yr).
2. **ISA shelter:** the ~£45,700 MPF remainder after payoff → UK ISA at £20,000/yr tax-free.
3. **Keep liquid** as additional job-search buffer alongside the £82,500.

**Recommended approach (validate with tax adviser):** withdraw MPF *before* UK residency → pay off the £54,264 mortgage (clean, guaranteed 4.74%, kills the 2033 balloon) → shelter the ~£45,700 remainder in an ISA → keep the £82,500 liquid for the London search.

## 11. Update (7 Jul): the DB flat (HK home) - hold-and-let

**Correction to earlier speculation:** the DB flat holds **no meaningful equity**. Value ~HK$6M (dropped from the HK$8M paid); mortgage HK$5,893,382 → equity ~HK$107k (~£11k). Julian is down ~HK$3M all-in (price fall + stamp duty + renovation). It is *not* a hidden war chest.

### Rental cash flow (UK-based, let at agent-estimated HK$22,000)
| Item | HKD/mo |
|---|---:|
| Rent in (agent est.; Julian aims for 25,000) | +22,000 |
| Mortgage (HK$12,138 interest + HK$13,689 principal) | −25,827 |
| Discovery Bay Management | −2,054 |
| Rating & Valuation (HK$3,587/qtr) | −1,196 |
| HK Property Tax (~15% on 80% of rent, est.) | ~−2,640 |
| **Net cash out of pocket** | **~−9,717 (~£970/mo)** |

Modelled at **~£970/mo ongoing** in the current burn tables. Julian clarified on 10 Jul that the letting agency fee is **50% of one month's rent**, so HK$11,000 (~£1,100), and is a one-off rather than a recurring ~£60/mo allowance. Confirm with a signed tenancy or agent quote.

### The key reframe
Of the HK$25,827 payment, **HK$13,689 (~£1,369/mo) is principal - equity, not consumption.** Rent (HK$22,000) more than covers *true* carrying costs (interest + fees + tax ≈ HK$18,000), so the ~£970/mo top-up goes into paying down Julian's own mortgage. **Cash cost to runway: real (~£970/mo ongoing, plus a one-off ~£1,100 agency fee). Net-worth cost: roughly nil.**

### Strategy: hold and wait for recovery
Defensible. Rent covers carrying costs; principal builds equity; selling now crystallises the loss at (what Julian believes is) the bottom. Two caveats on record:
1. The ~£970/mo ongoing cash drag, plus the one-off ~£1,100 agency fee, competes with the same liquid pot funding the London search - affordable, but it must stay *in* the model.
2. **"Recovery is expected" is a belief, not a fact.** The HK$3M is sunk; the live question is "is HK$6M best held here vs redeployed?", not "will I get back to HK$8M." Anchoring flagged. **Recommend a defined review trigger (e.g. reassess in 2-3 yrs or on a rate/rent move), not an open-ended wait on hope.** UK CGT may also apply to post-residency gains.

## 12. Update (7 Jul): UK tax on the HK rental - the 4-year FIG regime (researched)

Julian's fear: as a UK resident, the UK would tax the HK rent (~HK$22k/mo) at UK rates *and* deny mortgage-interest offset - potentially "so heavily it doesn't cover the mortgage." **Researched against gov.uk - the fear is largely unfounded for the window that matters.**

- **4-year FIG regime (from 6 Apr 2025):** a "qualifying new resident" pays **zero UK tax on foreign income and gains** for their first 4 UK-resident years. gov.uk explicitly covers **"profits of an overseas property business"** → the HK rent is **UK-tax-free for 4 years.**
- **Eligibility condition (LOAD-BEARING, to confirm):** must have been **non-UK-tax-resident for ≥10 consecutive tax years** before returning. Julian's HK tenure (Telstra, CLSA) far exceeds this - but confirm.
- **Mortgage interest:** cannot be *deducted* from profit (Section 24, since 2020, applies to overseas residential too) but a **20% basic-rate tax credit** applies. Moot during FIG (income exempt).
- **After the 4 years / if ineligible:** rent is UK-taxable, but with **foreign tax credit for HK Property Tax paid** (no double tax, UK-HK treaty) + 20% interest credit + personal allowance if low-income. Realistic worst case (higher-rate, post-FIG) ~£2,900/yr - not catastrophic.
- **Bonus:** FIG also makes **foreign capital gains UK-tax-free for 4 years** → a HK-flat recovery-sale *within* the window is **UK-CGT-free**. Time-limited angle for the hold-for-recovery plan.
- **Caveat:** claiming FIG in a year forfeits that year's personal allowance/CGT exemption - in a jobless year the allowance alone may shelter the rent, so claiming may be unnecessary. Adviser to optimise.
- **Decision impact: location-neutral** (depends on residency, not London vs Malvern) → does **not** change the London-vs-Malvern maths; confirms the modelled DB shortfall (HK-side tax only) carries **no UK tax on top** for 4 years. Removes a feared cost from both scenarios.

## Key Takeaways

- **Burn is ~92k HKD/mo (trending 84k), not 100k** - annual stake ≈ **1.1M HKD ≈ £110k**.
- The decision reduces to **P(well-paid HK work) vs a ~45-50% breakeven**. Above it, stay-and-bet; below it, move.
- **Moving caps the downside; staying's downside is unbounded** (drift burns the stake for nothing).
- Staying is only rational as an **active, deadlined networking bet** - never as drift.
- **London vs Malvern (post-MOVE):** Cecil Road is the London home, so London's cost is *forgone rent* (~£2,600/mo net drawdown), not a rent bill. Malvern is cash-neutral (the cushion). Decision gates on whether HK liquid savings cover a ~12-18 month London search (£31-47k) - see §9.

## Related
- [[decisions/uk-move/_index|UK Relocation Decision workspace]] · [[decisions/decision-journal|Decision Journal]]
- [[decisions/uk-move/analysis|Stage 1 Analysis]] (A1 = P(HK work), the master variable)
- [[decisions/uk-move/b7-lifestyle|B7]] - the lifestyle he under-uses still costs ~£1k/week
- [[financial-status-2026-06-22|June 2026 Financial Status]] · [[finance-workstream|Finance Goals]]
