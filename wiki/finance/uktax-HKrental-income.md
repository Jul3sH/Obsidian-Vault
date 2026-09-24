---
type: analysis
status: living
created: 2026-09-24
decision: UK Relocation Decision
tags: [finance, uk-relocation, tax, hong-kong, rental, fig]
---

# UK Tax on Hong Kong Rental Income

> **What this is.** The tax Julian would pay on letting the Discovery Bay flat if he became UK tax resident: Hong Kong tax, UK tax, how the two interact, and what the 4-year FIG regime does to the answer.
> **Why it exists.** Closes the item deferred in [[uktax-srt-fy26-27]] §5.11 and §8.8 ("HK rental treatment deferred as a separate workstream"), and replaces the rougher estimate in [[uk-move-financial-model]] §12.
> **How it is used.** Julian reads it to understand the exposure before any residence decision, and to decide, year by year, whether to claim FIG. Not regulated tax advice; adviser items are listed in §7. `send: NEVER`.

**Map:** §1 answer · §2 the mechanism (two separate computations) · §3 the numbers · §4 the FIG regime and how to use it · §5 the next few years · §6 what the earlier analysis got wrong · §7 adviser items · §8 sources.

**Brief, in Julian's words (24 Sep 2026):** *"I would like to understand what tax I will pay on rental earnings in HK if I am a UK resident. I'm anticipating a rental income of around HK$25,000 a month. I'm not sure whether I can offset the interest payments against my profit. In the UK you're not allowed to do this, but in Hong Kong, if I'm allowed to, do I offset the interest, work out my Hong Kong tax, and then the UK taxes above and beyond what Hong Kong did, or do I have to apply UK rules to my Hong Kong earnings? I'd also like to understand the 4-year FIG regime, how it affects me, what the taxation would be with and without it, scenarios over the next few years, and how best to use it."* No deliverable file exists for this work; this brief stands in for Prompt Zero (size 1, waived 24 Sep 2026).

---

## 1. The answer

- **Hong Kong taxes the rent first, at 15% of 80% of the rent.** About **HK$34,300 a year (£3,430)** at HK$25,000 a month. Mortgage interest is **not** deductible against it for you: the interest deduction only exists under Personal Assessment, which needs 180+ days a year in Hong Kong.
- **The UK then taxes the same rent under UK rules, from scratch.** You do not start from the Hong Kong figure. You recompute profit the UK way (rent less management fees and rates; **interest is not a deduction**), work out UK tax at your marginal rate, then take two reductions: a **20% credit for the mortgage interest** (about £2,900) and a **credit for the Hong Kong tax paid** (about £3,430, capped at the UK tax on that income).
- **What that costs depends almost entirely on your other UK income:**

| Your other UK income | UK tax on the HK rent, no FIG claim | With a FIG claim | What to do |
|---|---:|---:|---|
| None, or Cecil Road rent only | **£0** | £0, but costs £2,500 of allowance on Cecil Road | Do not claim |
| £75k salary | **£4,100** | £5,000 (lost personal allowance) | Do not claim |
| £110k salary | **£7,700** | £3,000 (lost allowance) | Claim, saves £4,600 |
| £150k or £200k salary | **£5,400** | **£0** | Claim, saves £5,400 |

- **FIG is worth roughly £5,000 a year, for four years, and only if you earn £100k+.** Below that the personal allowance you give up is worth more than the tax you save. Above that the allowance has been tapered away already, so claiming is free.
- **Cash reality check:** at HK$25,000 rent the flat is cash-negative by about **HK$6,900 a month** before any UK tax (mortgage HK$25,827 + fees + rates + HK tax). UK tax at £150k with no FIG claim adds about HK$4,500 a month; with a claim it adds nothing. About HK$13,700 of the monthly shortfall is principal repayment, so the net-worth cost is small.

---

## 2. The mechanism: two separate computations, then a credit

| Step | Hong Kong | United Kingdom |
|---|---|---|
| Who taxes | HK, as the property is there (UK-HK DTA Art. 6: "may be taxed in that other Party") | UK, on worldwide income if resident |
| Base | Net assessable value = (rent − rates paid by owner) × 80%. The 20% is a flat allowance for repairs and outgoings; nothing else is deductible | Overseas property business profit, computed "in the same way as a UK property business" (PIM4702): rent − management fees − rates − insurance − repairs − agent fees |
| Mortgage interest | **Not deductible** under Property Tax. Deductible only if you elect Personal Assessment, which needs you to be ordinarily resident in HK or present 180+ days in the year (or 300+ over two years) | **Not deductible** (s272A ITTOIA, applies to overseas lets too). Instead a **tax reduction of 20% × interest**, capped at 20% of the property profit; unused amounts carry forward |
| Rate | 15% flat | Your marginal rate: 20% / 40% / 45%, plus the 60% effective band between £100k and £125k where the personal allowance tapers |
| Double tax | n/a | HK Property Tax paid is a **credit** against UK tax on that income (DTA Art. 21(2)(a)), limited to the UK tax on the HK income. Not a deduction, not a starting point |

**So the direct answer to the brief:** the UK does not "top up" the HK-determined amount. Both jurisdictions run their own full computation on the gross rent; the HK tax then comes off the UK bill. The interest is offset in neither computation. In the UK it becomes a 20% credit; in HK it disappears entirely unless you spend 180+ days there, which is incompatible with the UK-resident premise of this note.

---

## 3. The numbers

**Inputs** (FX 10 HKD = £1, the wiki convention; Banked/Hoped per [[mm-optimism-accounting-bias]]):

| Input | HKD/yr | GBP/yr | Status |
|---|---:|---:|---|
| Rent at HK$25,000/mo | 300,000 | 30,000 | **Hoped** (Julian's target; agent estimated 22,000) |
| Rates (HK$3,587/qtr) | 14,348 | 1,435 | Banked ([[financial-status-2026-07-07]]) |
| DB management fee (HK$2,054/mo) | 24,648 | 2,465 | Banked |
| Mortgage interest (HK$12,138/mo, 2.47% on HK$5.89M) | 145,656 | 14,566 | Banked; falls ~HK$4k/yr as principal is repaid |
| Mortgage principal (HK$13,689/mo) | 164,268 | 16,427 | Never deductible anywhere |
| Letting agent fee (50% of one month) | 12,500 | 1,250 | One-off, year 1 only; deductible in the UK computation, excluded from the steady-state figures below |

**Hong Kong Property Tax:** (300,000 − 14,348) × 80% = 228,522 × 15% = **HK$34,278 (£3,428)**. At HK$22,000 rent: HK$29,958 (£2,996).

**UK computation, no FIG claim, 2026/27 rates (PA £12,570; 20% to £50,270; 40% to £125,140; 45% above):**

| | None / Cecil only | £75k salary | £110k salary | £150k+ salary |
|---|---:|---:|---:|---:|
| HK property profit (30,000 − 1,435 − 2,465) | 26,100 | 26,100 | 26,100 | 26,100 |
| UK tax on that profit at marginal rate | 2,706 → 0 after reducer | 10,440 | 14,016 | 11,745 |
| Less 20% interest reducer | (2,706, capped) | (2,913) | (2,913) | (2,913) |
| Less credit for HK tax | 0 | (3,428) | (3,428) | (3,428) |
| **UK tax attributable to the HK rent** | **0** | **4,099** | **7,675** | **5,404** |
| Total tax on the HK rent, HK + UK | 3,428 (13%) | 7,527 (29%) | 11,103 (43%) | 8,832 (34%) |
| Monthly UK cost | £0 | £342 | £640 | £450 |

Notes on the table:
- "Cecil only" assumes the Malvern case (Cecil Road let at £26,328/yr). The HK rent then sits partly in the 40% band, but the interest reducer plus the HK credit more than cover the marginal UK tax, so the incremental UK cost is nil (the credit is limited to UK tax on the HK income, so it cannot go below nil on a conservative ordering; on a generous ordering it clips £690 off the Cecil Road bill as well). "None" is the London-direct case with no job.
- £110k is the worst band because the HK rent eats the tapered personal allowance (an effective 60% rate).
- At HK$22,000 rent the £150k figure falls to about £4,200.
- Rates and bands are frozen through 2027/28 at least; the figures hold for the years in §5 unless bands change.

**UK computation with a FIG claim:** the HK rent is exempt (UK tax £0), but the claim costs the personal allowance for that year, the CGT annual exempt amount, and the interest reducer for the overseas property (RFIG43000: "will lose their entitlement to relief under section 274A"; any carried-forward relievable amount is set to nil, PIM2054). The cost of the lost allowance: £2,514 at Cecil-only (20% band), £5,028 at £75k (40% band), £3,028 at £110k (partly tapered already), £0 at £125,140+.

---

## 4. The FIG regime and how to use it

- **What it is.** A "qualifying new resident" (10+ consecutive non-resident tax years before arrival; Julian has 12) can claim relief on foreign income and gains in each of the **first four tax years of UK residence** (s845B ITTOIA; RFIG44000). Overseas property income is explicitly qualifying income (RFIG45100). The London rent is UK-source and never covered.
- **The clock runs from the first resident year whether or not you claim.** Four consecutive tax years, no pause.
- **The claim is per year and per source** (RFIG42100): made on the Self Assessment return, quantified, source by source. Claiming in year 1 does not commit you to years 2 to 4. You can claim on the HK rent and nothing else.
- **Rule of thumb for Julian:** claim in a year only if UK income (excluding the HK rent) is above about **£100k**. Below that, do not claim; the ordinary rules already reduce the HK rent's UK tax to between nil and £4,100, and the allowance is worth more.
- **A foreign gain claim covers a sale of the flat** within the window. Today the flat is under water (value ~HK$6M against HK$8M cost plus stamp duty and renovation), so the relevant point is the reverse: a foreign **loss** in a year you claim FIG is **not** allowable (RFIG43000). If a loss might be useful against other UK gains, do not claim in the disposal year. If the flat recovered above cost, a claim in the disposal year exempts the gain.
- **Sophia has her own window**, spent before she has income; not relevant to this note.

---

## 5. The next few years

2026/27 is a non-resident year on the locked SRT position ([[uktax-srt-fy26-27]]), so the FIG clock has not started. Two illustrative sequences, using the £150k band for the UK-resident years (HK rent tax per year, UK side):

| Tax year | Resident from 2027/28 | Resident from 2028/29 | Non-resident throughout |
|---|---|---|---|
| 2026/27 | Non-resident: £0 (HK tax only) | Non-resident: £0 | £0 |
| 2027/28 | FIG yr 1: £0 with claim (£5,400 without) | Non-resident: £0 | £0 |
| 2028/29 | FIG yr 2: £0 | FIG yr 1: £0 | £0 |
| 2029/30 | FIG yr 3: £0 | FIG yr 2: £0 | £0 |
| 2030/31 | FIG yr 4: £0 | FIG yr 3: £0 | £0 |
| 2031/32 | **Full exposure: £5,400/yr** | FIG yr 4: £0 | £0 |
| 2032/33 onward | £5,400/yr | **Full exposure: £5,400/yr** | £0 |

- **The FIG relief on this flat is worth about £20,000 over the four years at a £150k salary**, and nothing at all if income stays under about £75k. That is the whole value of the regime for this asset.
- **After the window,** the exposure at £150k is roughly £450 a month on top of the HK tax, falling slowly as mortgage interest declines and rising if the rent is raised. It is a cost, not a catastrophe, and does not by itself decide whether to hold the flat.
- **An accidental resident year still burns a year of the clock** with nothing to shelter; the SRT document already covers this.
- **Hong Kong side is unchanged by residence:** Property Tax is due every year the flat is let, reported on the individual return (BIR60), with provisional tax for the following year. Notify the IRD of chargeability within four months of the year end if no return is issued.

---

## 6. What the earlier analysis got wrong

[[uk-move-financial-model]] §12 (7 Jul 2026) concluded the fear of UK tax on the HK rent was "largely unfounded" and gave a post-FIG worst case of **~£2,900/yr**. Directional-error audit per [[mm-confirmation-amplification-bias]]:

| §12 claim | This note | Lean |
|---|---|---|
| "HK rent is UK-tax-free for 4 years" | True only if you claim, and claiming costs the personal allowance; at £75k a claim loses money | Toward the wanted answer |
| Worst case post-FIG ~£2,900/yr | £4,100 to £7,700/yr depending on income band; £5,400 at £150k | Toward the wanted answer, understated by £1,200 to £4,800 |
| Interest is a 20% credit, HK tax is a credit, no double tax | Correct | Neutral |
| "In a jobless year the allowance alone may shelter the rent, so claiming may be unnecessary" | Correct, and stronger: at nil to £75k of other income, never claim | Neutral |

Every error leaned the same way. The corrected picture is still not catastrophic, but "largely unfounded" was overstated: with a real UK salary and no claim, the HK rent costs a third to four-tenths of its profit in combined tax.

---

## 7. Adviser items (as of 24 Sep 2026, none yet reviewed by an adviser)

1. **Ordering of the interest reducer against the foreign tax credit** (both are Step 6 tax reductions). Changes the Cecil-only case by up to £690; immaterial elsewhere.
2. **UK-deductible expenses** beyond fees and rates: buildings insurance, repairs, agent fees. Each £1,000 of expense saves £400 to £450 at the top bands.
3. **The FIG claim threshold** above (about £100k) is a rule of thumb from these bands; confirm against actual income in the year before filing.
4. **Personal Assessment in Hong Kong** is only worth exploring if Julian ever spends 180+ days there in a year while still letting the flat. Then HK tax would fall to nil (interest plus basic allowance exceed the net assessable value), but that day pattern conflicts with UK residence.
5. **Capital gains base cost** for the flat (HK$8M plus stamp duty and renovation) should be evidenced now, in case a future sale is a UK-allowable loss.

---

## 8. Sources

- HK Property Tax: [IRD guide to Property Tax](https://www.ird.gov.hk/eng/pdf/pam54e.pdf), [FAQ on Property Tax returns](https://www.ird.gov.hk/eng/faq/pty.htm) (15% of net assessable value; 20% statutory allowance; rates paid by owner deductible; nothing else)
- HK Personal Assessment: [IRD brief guide (pam37e)](https://www.ird.gov.hk/eng/pdf/pam37e.pdf) (interest "on money borrowed for the purpose of producing property income" deductible, capped at that property's net assessable value); [FAQ on election](https://www.ird.gov.hk/eng/faq/pa.htm) (ordinarily resident or temporary resident: 180+ days in the year or 300+ over two years)
- UK overseas property business: [PIM4702](https://www.gov.uk/hmrc-internal-manuals/property-income-manual/pim4702) (computed as a UK property business; foreign tax relieved by credit); [PIM2054](https://www.gov.uk/hmrc-internal-manuals/property-income-manual/pim2054) and [PIM2058](https://www.gov.uk/hmrc-internal-manuals/property-income-manual/pim2058) (finance cost restriction and the 20% reduction, cap, carry-forward; FIG claim sets overseas carried-forward relief to nil)
- FIG regime: [RFIG42100](https://www.gov.uk/hmrc-internal-manuals/residence-and-fig-regime-manual/rfig42100) (claims per year, per source, quantified on the return); [RFIG43000](https://www.gov.uk/hmrc-internal-manuals/residence-and-fig-regime-manual/rfig43000) (loss of personal allowance, AEA, s274A relief, foreign losses); [RFIG44000](https://www.gov.uk/hmrc-internal-manuals/residence-and-fig-regime-manual/rfig44000) (qualifying new resident); [RFIG45100](https://www.gov.uk/hmrc-internal-manuals/residence-and-fig-regime-manual/rfig45100) (overseas property income qualifies); [HS266 (2026)](https://www.gov.uk/government/publications/foreign-income-and-gains-fig-regime-self-assessment-helpsheet-hs266/hs266-foreign-income-and-gains-fig-regime-2026)
- Treaty: [2010 UK-Hong Kong DTA](https://www.gov.uk/government/publications/hong-kong-tax-treaties/2010-uk-hong-kong-double-taxation-agreement-in-force), Art. 6(1) and (3), Art. 21(2)(a)
- UK rates 2026/27: [gov.uk income tax rates](https://www.gov.uk/income-tax-rates)
- Wiki inputs: [[financial-status-2026-07-07]] (mortgage split, fees, rates), [[uk-move-financial-model]] §11 and §12, [[uktax-srt-fy26-27]] §5.11 and §8.8, [[uk-relocation-cashflows]] (salary bands)

---

## Key Takeaways

- **Two full computations, then a credit.** UK rules apply to the gross rent; HK tax comes off the UK bill. The HK figure is never the starting point.
- **Interest is offset nowhere.** UK: a 20% tax credit (about £2,900). HK: nothing, unless you spend 180+ days there.
- **HK tax is about £3,400 a year at HK$25,000 rent.** Fixed, whatever the UK does.
- **UK tax on the HK rent ranges from £0 (no salary) to £7,700 (£110k) to £5,400 (£150k+).** Your salary decides it, not the flat.
- **FIG is a £5,000-a-year switch that only pays above about £100k of other income.** Claim per year, per source; never claim below £75k.
- **After four years the exposure is about £450 a month at £150k.** Real, not ruinous; it does not decide the hold-or-sell question on its own.
