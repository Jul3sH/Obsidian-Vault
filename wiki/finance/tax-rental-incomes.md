---
type: analysis
status: living
created: 2026-09-24
updated: 2026-09-25
authority: Codex-reviewed
reviewed: 2026-09-25
decision: UK Relocation Decision
tags: [finance, uk-relocation, tax, hong-kong, rental, fig]
---

# Tax on Rental Incomes

> **What this is.** The tax Julian pays on letting the Discovery Bay flat and Cecil Road if he is UK tax resident: Hong Kong tax, UK tax, how they interact, and what the 4-year FIG regime does.
> **Why it exists.** Closes the item deferred in [[uktax-srt-fy26-27]] §5.11 and §8.8, and replaces the rougher estimate in [[uk-move-financial-model]] §12. Restructured 25 Sep 2026 around Julian's four scenarios. Adversarially reviewed by Codex on 25 Sep 2026; corrections applied the same day (property rates from 2027/28, FIG threshold, sale-loss advice, HK Personal Assessment wording, residence conditionality).
> **How it is used.** Read §1 for the figures. Read §2 for the working behind each. Read §5 when deciding, year by year, whether to claim FIG. Not regulated tax advice; adviser items in §8. `send: NEVER`.

**Map:** §1 executive summary · §2 the four scenarios, each broken down · §3 shared inputs · §4 mechanism · §5 FIG regime · §6 next few years · §7 what the earlier analysis got wrong · §8 adviser items · §9 sources.

**Brief, in Julian's words (24 Sep 2026):** *"I would like to understand what tax I will pay on rental earnings in HK if I am a UK resident. I'm not sure whether I can offset the interest payments against my profit. Do I offset the interest, work out my Hong Kong tax, and then the UK taxes above and beyond what Hong Kong did, or do I have to apply UK rules to my Hong Kong earnings? I'd also like to understand the 4-year FIG regime, how it affects me, what the taxation would be with and without it, and how best to use it."* Stands in for Prompt Zero (size 1, waived 24 Sep 2026).

---

## 1. Executive summary

Rent assumed: **HK$324,000 a year (HK$27,000 a month) on the DB flat, £30,000 a year on Cecil Road.** UK resident all year. Figures are per year, property tax only (the income tax on any salary itself is excluded).

**Two rate bases.** 2026/27 is the year the scenarios were asked for. **From 6 April 2027 property income is taxed at 22% / 42% / 47% instead of 20% / 40% / 45%, and the mortgage interest credit becomes 22%** (Finance Act 2026 s7). Julian's first possible UK-resident year is 2027/28, so **the right-hand columns are the ones to plan on.**

| # | Scenario | HK tax | UK tax 2026/27 | Combined 2026/27 | **UK tax 2027/28+** | **Combined 2027/28+** | FIG claim? |
|---|---|---:|---:|---:|---:|---:|---|
| 1 | HK flat, no salary (Cecil let) | £3,716 | £0 | £3,716 | **£152** | **£3,867** | No: costs the allowance, saves nothing |
| 2 | HK flat, plus £135k salary | £3,716 | £6,196 | £9,912 | **£6,475** | **£10,191** | **Yes:** UK tax to £0, combined £3,716 |
| 3 | London flat, no salary | n/a | £2,131 | £2,131 | **£2,343** | **£2,343** | n/a (UK income, never covered) |
| 4 | London flat, plus £135k salary | n/a | £11,089 | £11,089 | **£11,553** | **£11,553** | n/a |
| **Total** | **Both properties, no salary (1 + 3)** | £3,716 | £2,131 | £5,847 | **£2,495** | **£6,211** | No claim |
| **Total** | **Both properties, £135k salary (2 + 4)** | £3,716 | £17,285 | £21,001 | **£18,028** | **£21,744** | **Yes:** combined falls to £15,269 |

- **No salary:** the HK flat adds almost nothing to the UK bill. The HK tax already paid is credited against the UK tax on that rent and covers it (fully in 2026/27, all but £152 from 2027/28).
- **£135k salary:** every pound of rent is taxed at the top rate (45%, then 47%); the interest and HK tax credits cover about half of it.
- **FIG threshold has moved.** At this rent, claiming pays once other UK income (salary plus Cecil Road profit) exceeds about **£73k**, which is a salary of about **£47k** with Cecil Road let. The earlier "£100k" rule of thumb was wrong at this rent. See §5.
- **Cash reality, HK flat at HK$27,000:** about HK$5,200 a month out of pocket before UK tax (HK$10,600 in scenario 2 without FIG). HK$13,689 of that is loan repayment, so net worth rises about HK$8,500 a month before UK tax, HK$3,100 in scenario 2. Illustrative; detail and omissions in §2.5.

---

## 2. The four scenarios, each broken down

Working shown at 2026/27 rates; the 2027/28 figure follows each result.

### 2.1 Scenario 1: HK flat, no salary (Cecil Road let)

**Hong Kong side**
- Rent HK$324,000 less rates HK$14,348 = HK$309,652
- × 80% (flat statutory allowance) = HK$247,722
- × 15% = **HK$37,158 (£3,716)**
- Mortgage interest: not deductible under Property Tax. Deductible only under a Personal Assessment election (see §4 and §8.4)

**UK side**
- HK profit under UK rules: £32,400 − rates £1,435 − fees £2,465 = **£28,500**
- Other income: Cecil Road profit £25,778 (scenario 3)
- Total income £54,278 − personal allowance £12,570 = £41,708 taxable
- Tax: £37,700 × 20% + £4,008 × 40% = £9,143
- Less interest reducers: Cecil £511, HK £2,913 → £5,719
- UK tax without the HK rent would be £2,131, so **UK tax on the HK rent = £3,588**
- Less HK tax credit, capped at £3,588 → **£0**. £128 of HK tax credit unused

**Result:** combined tax on the HK flat **£3,716**, all paid in Hong Kong.
**From 2027/28:** property bands 22% / 42%, reducer 22%. UK tax on the HK rent £3,867, HK credit £3,716, **UK £152**, combined £3,867.
**FIG:** do not claim. It would forfeit the personal allowance (£2,514 more tax on Cecil Road) for a saving of nil.
*Label note (Codex finding 6): this is the incremental tax on the HK rent with Cecil Road already let. With the HK flat as the only income, UK tax on it is £273 before credit and still £0 after.*

### 2.2 Scenario 2: HK flat, plus £135,000 salary

**Hong Kong side:** unchanged, **£3,716**.

**UK side**
- Salary £135,000 → personal allowance fully tapered (gone above £125,140)
- HK profit £28,500 taxed as top slice at 45% = £12,825
- Less interest reducer £2,913 → £9,912
- Less HK tax credit £3,716 (full, cap not binding) → **£6,196**

**Result:** combined tax on the HK flat **£9,912**, 35% of the £28,500 profit, about £826 a month.
**From 2027/28:** £28,500 × 47% = £13,395, less reducer 22% × £14,566 = £3,204, less HK credit £3,716 → **UK £6,475**, combined £10,191 (£849 a month).
**FIG:** claim. UK tax on the HK rent → £0; the allowance is already lost so the claim costs nothing (subject to §5 on CGT and losses). Saves £6,475 a year for up to four years.

### 2.3 Scenario 3: London flat, no salary

- Rent £30,000 − agent £3,240 − rent protection £432 − buildings insurance £550 = **profit £25,778**
- Less personal allowance £12,570 = £13,208 taxable at 20% = £2,642
- Less interest reducer 20% × £2,556 = £511 → **£2,131**

**Result:** **£2,131** a year, £178 a month. This is also the whole UK bill in the no-salary case (see 2.1).
**From 2027/28:** £13,208 × 22% = £2,906, less reducer 22% × £2,556 = £562 → **£2,343**.
**FIG:** not available; UK-source income is never covered.

### 2.4 Scenario 4: London flat, plus £135,000 salary

- Profit £25,778, personal allowance gone, taxed at 45% = £11,600
- Less interest reducer £511 → **£11,089**

**Result:** **£11,089** a year, £924 a month.
**From 2027/28:** £25,778 × 47% = £12,116, less £562 → **£11,553**.
**Both properties in this case:** UK £17,285 (2026/27) or £18,028 (2027/28+). The salary's own income tax, £46,953, is on top.

### 2.5 Cash reality on the HK flat (HK$27,000 rent, illustrative)

UK tax shown at 2027/28 rates, scenario 2.

| HK$ per month | Before UK tax | Scenario 2, no FIG | Scenario 2, FIG claimed |
|---|---:|---:|---:|
| Rent in | 27,000 | 27,000 | 27,000 |
| Mortgage (interest 12,138 + loan repayment 13,689) | 25,827 | 25,827 | 25,827 |
| Management fee + rates + HK tax | 6,347 | 6,347 | 6,347 |
| UK tax | 0 | 5,396 | 0 |
| **Cash out of pocket** | **5,174** | **10,570** | **5,174** |
| Of which loan repayment (kept as equity) | 13,689 | 13,689 | 13,689 |
| **Net-worth change, ignoring price moves** | **+8,515** | **+3,119** | **+8,515** |

- The flat costs cash every month but does not cost net worth, on these inputs.
- **Omitted:** the year-1 letting agent fee (HK$13,500, about HK$1,125 a month spread over the year), voids, repairs, and any rise in owner-paid rates. The interest figure is a monthly statement snapshot, not a verified annual bill.

---

## 3. Shared inputs

FX 10 HKD = £1 (wiki convention). Banked/Hoped per [[mm-optimism-accounting-bias]].

| Input | Value | Status |
|---|---:|---|
| DB rent | HK$324,000/yr (£32,400) | **Hoped** (Julian's target 25 Sep; agent estimated HK$22,000/mo) |
| DB rates | HK$14,348/yr (£1,435) | Banked ([[financial-status-2026-07-07]]); assumes owner-paid |
| DB management fee | HK$24,648/yr (£2,465) | Banked |
| DB mortgage interest (2.47% on HK$5.89M) | HK$145,656/yr (£14,566) | Banked from a monthly snapshot; falls ~HK$4k/yr as principal is repaid |
| DB mortgage principal | HK$164,268/yr | Never deductible anywhere |
| DB letting agent fee (50% of one month) | HK$13,500 per new tenancy; HK$6,750/yr on a 2-year tenancy | Julian 25 Sep; UK-deductible; excluded from §1 and §2 |
| DB buildings insurance | HK$3,300/yr (HK$275/mo) | Julian 25 Sep; UK-deductible; excluded from §1 and §2 |
| Cecil Road rent | £30,000/yr | **Hoped** (Julian's target 25 Sep; May 2026 statement £2,500/mo) |
| Cecil Road expenses (agent 10.8% = £3,240, rent protection £432, buildings insurance £469) | £4,141/yr | Julian 25 Sep (insurance was £550 in the July P&L); §1 and §2 still use £4,222 |
| Cecil Road council tax when lived in (Merton Band E, single-person discount) | £1,968/yr | Julian 25 Sep; a living cost, never deductible |
| Cecil Road mortgage interest (interest-only, 4.74%) | £2,556/yr | Banked |
| UK bands 2026/27 | PA £12,570; 20% to £50,270; 40% to £125,140; 45% above; PA tapers £100k to £125,140 | gov.uk |
| **UK property rates from 2027/28** | **22% / 42% / 47%; interest reducer 22%**; bands and allowance unchanged | **Finance Act 2026 s7; HMRC technical note** (verified 25 Sep 2026) |

**As of 25 Sep 2026, the §1 and §2 tables use the narrower expense set (DB fees + rates; Cecil £4,222).** With the fuller deductible set logged above (DB £49,046/yr = £4,905; Cecil £4,141), the 2027/28 figures move by less than £500: HK flat at £135k salary **£6,002** (not £6,475), HK flat with no salary **£0** (not £152), Cecil Road at £135k £11,591 (not £11,553), Cecil Road with no salary £2,361 (not £2,343). Re-run the tables when the savings sheet is rebuilt.

---

## 4. Mechanism: two full computations, then a credit

| Step | Hong Kong | United Kingdom |
|---|---|---|
| Who taxes | HK, property is there (DTA Art. 6) | UK, worldwide income if resident |
| Base | (rent − rates) × 80%. Nothing else deductible | Rent − fees − rates − insurance − repairs − agent (PIM4702). UK and overseas lets are separate property businesses |
| Mortgage interest | **Not deductible** under Property Tax. Deductible only under Personal Assessment: ordinarily resident in HK, or more than 180 days in the year, or more than 300 days over two consecutive years | **Not deductible** (s272A ITTOIA). Instead a tax reduction at the property basic rate (20%, **22% from 2027/28**), capped at the lowest of: finance costs, property profit, and adjusted total income; unused carries forward |
| Rate | 15% flat | Marginal. 2026/27: 20% / 40% / 45%. **2027/28+: 22% / 42% / 47%** on property income, plus the 60% effective band between £100k and £125k where the allowance tapers |
| Double tax | n/a | HK tax paid is a **credit** against UK tax on that income (DTA Art. 21(2)(a)), capped at the UK tax on it. The interest reducer is applied first, then the credit (ITA 2007 s27; per Codex review, adviser to confirm) |

- The UK does not top up the HK figure. Both run a full computation on the gross rent; HK tax then comes off the UK bill.
- Interest is offset in neither. UK: a 20% (22%) credit. HK: nothing, unless Personal Assessment applies (§8.4).

---

## 5. The FIG regime and how to use it

- **What:** a qualifying new resident (10+ consecutive non-resident years) can exempt foreign income and gains in each of the **first four UK-resident tax years** (s845B ITTOIA; RFIG44000). Overseas property income qualifies (RFIG45100). London rent never does.
- **Julian's eligibility** rests on 12 consecutive non-resident years (2014/15 to 2025/26), stated in [[uktax-srt-fy26-27]] §9.2 subject to evidence. Not independently verified; the four-year calendar below is conditional on it and on the first resident year being 2027/28.
- **Clock:** runs from the first resident year whether or not you claim. Four consecutive years, no pause. An accidental resident year burns one.
- **Claim mechanics:**
  - Per year, per source, quantified, on that year's Self Assessment return (RFIG42100). Nothing to activate in advance.
  - Decided in arrears, after the year ends. **Not claiming in year 1 does not forfeit years 2 to 4.**
  - A mid-year job start: the whole tax year's income decides whether to claim for that year.
  - **Deadline:** 12 months after the normal 31 January filing date for that year (RFIG42300), so a 2027/28 claim can be made until 31 January 2030. After that the year is gone.
- **Cost of claiming:** the personal allowance, the CGT annual exempt amount, and the overseas interest reducer for that year, including any carried-forward unused finance cost (RFIG43000, PIM2054). Foreign losses in a claim year cannot be carried forward.
- **Rule for Julian at HK$27,000 rent:** claim once other UK income (salary plus Cecil Road profit) is above about **£73k**, which is a salary of about **£47k** with Cecil Road let. Below that the lost allowance costs more than the saving. Roughly the same break-even on 2027/28 rates. Check each year against actual income; do not rely on the threshold.
- **Sale of the flat in a claim year:** a gain can be exempted, but only if the gain is itself identified in a foreign-gain claim; a rent claim does not cover it automatically. A loss in a claim year is not allowable. Whether a sale produces a UK-allowable loss needs a sterling computation at both dates and former-home relief; the HK$6M-versus-HK$8M gap is not that computation (§8.6). Compute before deciding the claim in a disposal year.

Sensitivity at HK$27,000 rent, 2026/27 rates, Cecil Road let (other income = salary + £25,778):

| Salary | UK tax on HK rent, no claim | Cost of claiming (lost allowance) | Verdict |
|---|---:|---:|---|
| None | £0 | £2,514 | No claim |
| £25k | £4,771 | £5,028 | No claim (£257 worse) |
| £47k | £5,028 | £5,028 | Break-even |
| £75k | £9,851 | £4,872 | Claim, saves £4,978 |
| £110k+ | £6,196 | £0 | Claim, saves £6,196 |

£75k is the worst band: the HK rent pushes income through the £100k allowance taper (60% effective rate).

---

## 6. The next few years (projection)

2026/27 is non-resident on the locked SRT position ([[uktax-srt-fy26-27]]), so the clock has not started. UK tax on the HK rent per year, scenario 2 income, 2027/28 property rates. Projection: interest falls about HK$4k a year, FX, rent and bands will move.

| Tax year | Resident from 2027/28 | Resident from 2028/29 | Non-resident throughout |
|---|---|---|---|
| 2026/27 | Non-resident: £0 | Non-resident: £0 | £0 |
| 2027/28 | FIG yr 1: £0 (£6,475 without claim) | Non-resident: £0 | £0 |
| 2028/29 to 2030/31 | FIG yrs 2 to 4: £0 | FIG yrs 1 to 3: £0 | £0 |
| 2031/32 | **Full exposure: ~£6,475** | FIG yr 4: £0 | £0 |
| 2032/33 onward | ~£6,475 | **Full exposure: ~£6,475** | £0 |

- FIG is worth about **£26,000 over four years** at scenario 2 income, nothing below about £47k salary.
- After the window: about £540 a month on top of HK tax. A cost, not a catastrophe; does not decide hold-or-sell alone.
- HK side unchanged by UK residence: Property Tax due every year the flat is let (BIR60), provisional tax for the following year.

---

## 7. What the earlier analysis got wrong

[[uk-move-financial-model]] §12 (7 Jul 2026) called the fear of UK tax on the HK rent "largely unfounded", worst case ~£2,900/yr. Audit per [[mm-confirmation-amplification-bias]]:

| §12 claim | This note | Lean |
|---|---|---|
| "HK rent is UK-tax-free for 4 years" | Only if you claim, and claiming costs the allowance; below about £47k salary a claim loses money | Toward the wanted answer |
| Worst case post-FIG ~£2,900/yr | £6,475 at £135k and HK$27,000 rent on 2027/28 rates | Understated by ~£3,600 |
| Interest 20% credit, HK tax credit, no double tax | Correct (credit rate 22% from 2027/28) | Neutral |
| In a jobless year claiming may be unnecessary | Correct: never claim with no salary | Neutral |

The 24 Sep version of this note also erred toward the wanted answer: it used 2026/27 rates for 2027/28 onward, and its "claim only above £100k" rule was wrong at this rent (Codex review, 25 Sep).

---

## 8. Adviser items (as of 25 Sep 2026, none yet reviewed by an adviser)

1. **Ordering of the interest reducer and the foreign tax credit.** Codex reads ITA 2007 s27 and TIOPA 2010 s36 as requiring reducer first, credit second (the basis used here). Confirm. Moves nothing material.
2. **UK-deductible expenses on the DB flat** beyond fees and rates: insurance, repairs, agent fees. Each £1,000 saves £470 at 47%.
3. **FIG break-even** (~£47k salary with Cecil let) is a rule of thumb from these inputs; confirm against actual income before filing each year.
4. **Personal Assessment in Hong Kong for the 2026/27 HK year of assessment** (1 Apr 2026 to 31 Mar 2027). Julian lived in HK until Sep 2026, so the 300-days-over-two-years test is probably met for that year; an election could cut HK tax on any 2026/27 rent to nil via the interest deduction. Not available in later years unless he spends more than 180 days in HK.
5. **Pension contributions at £135k** would restore some personal allowance and change scenarios 2 and 4.
6. **Capital gains position on the flat:** evidence base cost (HK$8M plus stamp duty and renovation), acquisition-date and sale-date sterling rates, and former-home relief, so a future sale can be assessed as a UK gain or allowable loss before any FIG claim in that year.
7. **FIG eligibility evidence:** the 12 non-resident years (SRT §9.2) should be documented before the first claim.
8. **Opening loss and carry-forward balances** (property losses, unused finance costs): none assumed here; confirm none exist.

---

## 9. Sources

- HK Property Tax: [IRD guide](https://www.ird.gov.hk/eng/pdf/pam54e.pdf), [FAQ](https://www.ird.gov.hk/eng/faq/pty.htm)
- HK Personal Assessment: [pam37e](https://www.ird.gov.hk/eng/pdf/pam37e.pdf), [FAQ on election](https://www.ird.gov.hk/eng/faq/pa.htm)
- UK property rates from 2027/28: [Finance Act 2026 s7](https://www.legislation.gov.uk/ukpga/2026/11/section/7), [HMRC technical note](https://www.gov.uk/government/publications/changes-to-tax-rates-for-property-savings-and-dividend-income/change-to-tax-rates-for-property-savings-and-dividend-income-technical-note)
- UK overseas property business: [PIM4702](https://www.gov.uk/hmrc-internal-manuals/property-income-manual/pim4702), [PIM2054](https://www.gov.uk/hmrc-internal-manuals/property-income-manual/pim2054), [PIM2058](https://www.gov.uk/hmrc-internal-manuals/property-income-manual/pim2058)
- Foreign tax credit: [HS263 (2026)](https://www.gov.uk/government/publications/calculating-foreign-tax-credit-relief-on-income-hs263-self-assessment-helpsheet/relief-for-foreign-tax-paid-2026-hs263), [ITA 2007 s27](https://www.legislation.gov.uk/ukpga/2007/3/section/27), [TIOPA 2010 s36](https://www.legislation.gov.uk/ukpga/2010/8/section/36)
- FIG regime: [RFIG42100](https://www.gov.uk/hmrc-internal-manuals/residence-and-fig-regime-manual/rfig42100), [RFIG42300](https://www.gov.uk/hmrc-internal-manuals/residence-and-fig-regime-manual/rfig42300), [RFIG43000](https://www.gov.uk/hmrc-internal-manuals/residence-and-fig-regime-manual/rfig43000), [RFIG44000](https://www.gov.uk/hmrc-internal-manuals/residence-and-fig-regime-manual/rfig44000), [RFIG45100](https://www.gov.uk/hmrc-internal-manuals/residence-and-fig-regime-manual/rfig45100), [HS266 (2026)](https://www.gov.uk/government/publications/foreign-income-and-gains-fig-regime-self-assessment-helpsheet-hs266/hs266-foreign-income-and-gains-fig-regime-2026)
- Capital gains: [CG78310](https://www.gov.uk/hmrc-internal-manuals/capital-gains-manual/cg78310) (foreign currency), [HS283 (2026)](https://www.gov.uk/government/publications/private-residence-relief-hs283-self-assessment-helpsheet/hs283-private-residence-relief-2026)
- Treaty: [2010 UK-Hong Kong DTA](https://www.gov.uk/government/publications/hong-kong-tax-treaties/2010-uk-hong-kong-double-taxation-agreement-in-force), Art. 6 and 21(2)(a)
- UK rates 2026/27: [gov.uk](https://www.gov.uk/income-tax-rates)
- Wiki inputs: [[financial-status-2026-07-07]], [[uk-move-financial-model]] §9, §11, §12, [[uktax-srt-fy26-27]] §5.11, §6.2, §8.8, §9.2, [[uk-relocation-cashflows]]

---

## Key Takeaways

- **Two full computations, then a credit.** UK rules on the gross rent; HK tax comes off the UK bill.
- **Interest is offset nowhere.** UK: 20% credit, 22% from 2027/28. HK: nothing (unless Personal Assessment, §8.4).
- **HK tax is £3,716 a year at HK$27,000 rent**, whatever the UK does.
- **Plan on 2027/28 rates (22/42/47), not 2026/27.** No salary: HK flat £152 UK tax, London flat £2,343. £135k salary: HK flat £6,475, London flat £11,553.
- **FIG wipes the HK figure for four years. Claim once salary is above about £47k with Cecil Road let**, not £100k. Decide each year in arrears; skipping a year forfeits nothing but the clock runs regardless.
- **After the window: about £540 a month at £135k.** Real, not ruinous; does not decide hold-or-sell alone.
