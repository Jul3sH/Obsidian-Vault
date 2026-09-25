---
type: analysis
status: living
created: 2026-09-24
updated: 2026-09-25
decision: UK Relocation Decision
tags: [finance, uk-relocation, tax, hong-kong, rental, fig]
---

# Tax on Rental Incomes

> **What this is.** The tax Julian pays on letting the Discovery Bay flat and Cecil Road if he is UK tax resident: Hong Kong tax, UK tax, how they interact, and what the 4-year FIG regime does.
> **Why it exists.** Closes the item deferred in [[uktax-srt-fy26-27]] §5.11 and §8.8, and replaces the rougher estimate in [[uk-move-financial-model]] §12. Restructured 25 Sep 2026 around Julian's four scenarios.
> **How it is used.** Read §1 for the figures. Read §2 for the working behind each. Read §4 to §5 when deciding, year by year, whether to claim FIG. Not regulated tax advice; adviser items in §8. `send: NEVER`.

**Map:** §1 executive summary · §2 the four scenarios, each broken down · §3 shared inputs · §4 mechanism · §5 FIG regime · §6 next few years · §7 what the earlier analysis got wrong · §8 adviser items · §9 sources.

**Brief, in Julian's words (24 Sep 2026):** *"I would like to understand what tax I will pay on rental earnings in HK if I am a UK resident. I'm not sure whether I can offset the interest payments against my profit. Do I offset the interest, work out my Hong Kong tax, and then the UK taxes above and beyond what Hong Kong did, or do I have to apply UK rules to my Hong Kong earnings? I'd also like to understand the 4-year FIG regime, how it affects me, what the taxation would be with and without it, and how best to use it."* Stands in for Prompt Zero (size 1, waived 24 Sep 2026).

---

## 1. Executive summary

Rent assumed: **HK$324,000 a year (HK$27,000 a month) on the DB flat, £30,000 a year on Cecil Road.** UK resident all year, 2026/27 rates. Figures are per year.

| # | Scenario | HK tax | UK tax | **Combined** | FIG claim? |
|---|---|---:|---:|---:|---|
| 1 | HK flat, no other earnings | £3,716 | **£0** | **£3,716** | No: costs the personal allowance, saves nothing |
| 2 | HK flat, plus £135k salary | £3,716 | **£6,196** | **£9,912** | **Yes:** UK tax falls to £0, combined £3,716 |
| 3 | London flat, no other earnings | n/a | **£2,131** | **£2,131** | n/a (UK income, never covered) |
| 4 | London flat, plus £135k salary | n/a | **£11,089** | **£11,089** | n/a |
| **Total** | **Both properties, no other earnings (1 + 3)** | **£3,716** | **£2,131** | **£5,847** | No claim |
| **Total** | **Both properties, with £135k salary (2 + 4)** | **£3,716** | **£17,285** | **£21,001** | **Yes:** total falls to £14,805 |

- **Properties only:** the HK flat adds nothing to the UK bill; the £2,131 is all Cecil Road.
- **With £135k salary:** the properties cost £17,285 in UK tax (London £11,089 + HK £6,196) because the allowance is gone and all rent is taxed at 45%. FIG removes the £6,196. The salary's own income tax (£46,953) is excluded from these figures.
- **Why the HK flat is free in scenario 1:** the HK tax already paid (£3,716) is credited against the UK tax on that rent (£3,588), and exceeds it.
- **Why it costs £6,196 in scenario 2:** at £135k every pound of rent is taxed at 45%; the two credits cover only £6,629 of the £12,825 UK charge.
- **Cash reality, HK flat at HK$27,000:** about HK$5,200 a month out of pocket before UK tax (HK$10,300 in scenario 2 without FIG). HK$13,689 of that is loan repayment, so net worth rises about HK$8,500 a month before UK tax, HK$3,400 in scenario 2. Detail in §2.5.

---

## 2. The four scenarios, each broken down

### 2.1 Scenario 1: HK flat, no other earnings

**Hong Kong side**
- Rent HK$324,000 less rates HK$14,348 = HK$309,652
- × 80% (flat statutory allowance) = HK$247,722
- × 15% = **HK$37,158 (£3,716)**
- Mortgage interest: not deductible (needs 180+ days in HK)

**UK side**
- HK profit under UK rules: £32,400 − rates £1,435 − fees £2,465 = **£28,500**
- Other income: London profit £25,778 (scenario 3)
- Total income £54,278 − personal allowance £12,570 = £41,708 taxable
- Tax: £37,700 × 20% + £4,008 × 40% = £9,143
- Less interest reducers: London £511, HK £2,913 → £5,719
- UK tax without the HK rent would be £2,131, so **UK tax on the HK rent = £3,588**
- Less HK tax credit, capped at £3,588 → **£0**. £128 of HK tax credit unused

**Result:** combined tax on the HK flat **£3,716**, all paid in Hong Kong.
**FIG:** do not claim. It would forfeit the personal allowance (£2,514 more tax on the London rent) for a saving of nil.

### 2.2 Scenario 2: HK flat, plus £135,000 salary

**Hong Kong side:** unchanged, **£3,716**.

**UK side**
- Salary £135,000 → personal allowance fully tapered (gone above £125,140)
- HK profit £28,500 taxed as top slice at 45% = £12,825
- Less interest reducer £2,913 → £9,912
- Less HK tax credit £3,716 (full, cap not binding) → **£6,196**

**Result:** combined tax on the HK flat **£9,912**, 35% of the £28,500 profit, about £826 a month.
**FIG:** claim. UK tax on the HK rent → £0; the allowance is already lost so the claim costs nothing. Saves £6,196 a year for up to four years. Combined falls to £3,716.

### 2.3 Scenario 3: London flat, no other earnings

- Rent £30,000 − agent £3,240 − rent protection £432 − buildings insurance £550 = **profit £25,778**
- Less personal allowance £12,570 = £13,208 taxable at 20% = £2,642
- Less interest reducer 20% × £2,556 = £511 → **£2,131**

**Result:** **£2,131** a year, £178 a month. This is also the whole UK bill in the no-earnings case (see 2.1).
**FIG:** not available; UK-source income is never covered.

### 2.4 Scenario 4: London flat, plus £135,000 salary

- Profit £25,778, personal allowance gone, taxed at 45% = £11,600
- Less interest reducer £511 → **£11,089**

**Result:** **£11,089** a year, £924 a month.
**Both properties in this case:** London £11,089 + HK £6,196 = **£17,285** UK tax, £21,001 with the HK tax. (The salary's own income tax, £46,953, is on top.)

### 2.5 Cash reality on the HK flat (HK$27,000 rent)

| HK$ per month | Before UK tax | Scenario 2, no FIG | Scenario 2, FIG claimed |
|---|---:|---:|---:|
| Rent in | 27,000 | 27,000 | 27,000 |
| Mortgage (interest 12,138 + loan repayment 13,689) | 25,827 | 25,827 | 25,827 |
| Management fee + rates + HK tax | 6,347 | 6,347 | 6,347 |
| UK tax | 0 | 5,163 | 0 |
| **Cash out of pocket** | **5,174** | **10,337** | **5,174** |
| Of which loan repayment (kept as equity) | 13,689 | 13,689 | 13,689 |
| **Net-worth change, ignoring price moves** | **+8,515** | **+3,352** | **+8,515** |

- The flat costs cash every month but does not cost net worth.
- Corrected 25 Sep 2026: the 24 Sep wording said principal was "part of the shortfall", which was garbled.

---

## 3. Shared inputs

FX 10 HKD = £1 (wiki convention). Banked/Hoped per [[mm-optimism-accounting-bias]].

| Input | Value | Status |
|---|---:|---|
| DB rent | HK$324,000/yr (£32,400) | **Hoped** (Julian's target 25 Sep; agent estimated HK$22,000/mo) |
| DB rates | HK$14,348/yr (£1,435) | Banked ([[financial-status-2026-07-07]]) |
| DB management fee | HK$24,648/yr (£2,465) | Banked |
| DB mortgage interest (2.47% on HK$5.89M) | HK$145,656/yr (£14,566) | Banked; falls ~HK$4k/yr as principal is repaid |
| DB mortgage principal | HK$164,268/yr | Never deductible anywhere |
| DB letting agent fee (50% of one month) | HK$13,500 one-off | Year 1 only, UK-deductible; excluded above |
| Cecil Road rent | £30,000/yr | **Hoped** (Julian's target 25 Sep; May 2026 statement £2,500/mo) |
| Cecil Road expenses (agent 10.8%, rent protection, buildings insurance) | £4,222/yr | Banked ([[uk-move-financial-model]] §9) |
| Cecil Road mortgage interest (interest-only, 4.74%) | £2,556/yr | Banked |
| UK bands 2026/27 | PA £12,570; 20% to £50,270; 40% to £125,140; 45% above; PA tapers £100k to £125,140 | Frozen through 2027/28 |

---

## 4. Mechanism: two full computations, then a credit

| Step | Hong Kong | United Kingdom |
|---|---|---|
| Who taxes | HK, property is there (DTA Art. 6) | UK, worldwide income if resident |
| Base | (rent − rates) × 80%. Nothing else deductible | Rent − fees − rates − insurance − repairs − agent (PIM4702) |
| Mortgage interest | **Not deductible** unless Personal Assessment (180+ days in HK) | **Not deductible** (s272A ITTOIA). Instead a 20% tax reduction, capped at 20% of property profit; unused carries forward |
| Rate | 15% flat | Marginal: 20% / 40% / 45%, with 60% effective between £100k and £125k |
| Double tax | n/a | HK tax paid is a **credit** against UK tax on that income (DTA Art. 21(2)(a)), capped at the UK tax on it |

- The UK does not top up the HK figure. Both run a full computation on the gross rent; HK tax then comes off the UK bill.
- Interest is offset in neither. UK: a 20% credit. HK: nothing, unless 180+ days there, which contradicts UK residence.

---

## 5. The FIG regime and how to use it

- **What:** a qualifying new resident (10+ consecutive non-resident years; Julian has 12) can exempt foreign income and gains in each of the **first four UK-resident tax years** (s845B ITTOIA; RFIG44000). Overseas property income qualifies (RFIG45100). London rent never does.
- **Clock:** runs from the first resident year whether or not you claim. Four consecutive years, no pause. An accidental resident year burns one.
- **Claim:** per year, per source, on the Self Assessment return (RFIG42100). Claiming in year 1 does not commit later years.
- **Cost of claiming:** personal allowance, CGT annual exempt amount, and the overseas interest reducer for that year (RFIG43000, PIM2054).
- **Rule of thumb:** claim only when other UK income is above about **£100k**. Below that the lost allowance costs more than the saving.
- **Sale of the flat:** a gain in a claim year is exempt; a **loss** in a claim year is not allowable. The flat is under water (~HK$6M vs HK$8M cost), so do not claim in a loss-making disposal year.

Sensitivity by salary band (HK$25,000 rent, from the 24 Sep analysis):

| Other UK income | UK tax on HK rent, no claim | With claim | Verdict |
|---|---:|---:|---|
| None | £0 | £0 | No claim |
| £27k UK rent only | £0 | +£2,514 on the UK rent | No claim |
| £75k salary | £4,100 | £5,000 (lost allowance) | No claim |
| £110k salary | £7,700 | £3,000 | Claim, saves £4,600 |
| £150k+ salary | £5,400 | £0 | Claim, saves £5,400 |

---

## 6. The next few years

2026/27 is non-resident on the locked SRT position ([[uktax-srt-fy26-27]]), so the clock has not started. UK tax on the HK rent per year, scenario 2 income:

| Tax year | Resident from 2027/28 | Resident from 2028/29 | Non-resident throughout |
|---|---|---|---|
| 2026/27 | Non-resident: £0 | Non-resident: £0 | £0 |
| 2027/28 | FIG yr 1: £0 (£6,196 without claim) | Non-resident: £0 | £0 |
| 2028/29 to 2030/31 | FIG yrs 2 to 4: £0 | FIG yrs 1 to 3: £0 | £0 |
| 2031/32 | **Full exposure: £6,196** | FIG yr 4: £0 | £0 |
| 2032/33 onward | £6,196 | **Full exposure: £6,196** | £0 |

- FIG is worth about **£25,000 over four years** at scenario 2 income, nothing below about £75k.
- After the window: about £516 a month on top of HK tax. A cost, not a catastrophe; does not decide hold-or-sell alone.
- HK side unchanged by residence: Property Tax due every year the flat is let (BIR60), provisional tax for the following year.

---

## 7. What the earlier analysis got wrong

[[uk-move-financial-model]] §12 (7 Jul 2026) called the fear of UK tax on the HK rent "largely unfounded", worst case ~£2,900/yr. Audit per [[mm-confirmation-amplification-bias]]:

| §12 claim | This note | Lean |
|---|---|---|
| "HK rent is UK-tax-free for 4 years" | Only if you claim, and claiming costs the allowance; at £75k a claim loses money | Toward the wanted answer |
| Worst case post-FIG ~£2,900/yr | £6,196 at £135k and HK$27,000 rent | Understated by ~£3,300 |
| Interest 20% credit, HK tax credit, no double tax | Correct | Neutral |
| In a jobless year claiming may be unnecessary | Correct and stronger: never claim below £75k | Neutral |

Every error leaned the same way.

---

## 8. Adviser items (as of 25 Sep 2026, none yet reviewed by an adviser)

1. **Ordering of the interest reducer against the foreign tax credit.** Moves scenario 1 by about £130 (£128 unused credit on the conservative reading). Immaterial elsewhere.
2. **UK-deductible expenses on the DB flat** beyond fees and rates: insurance, repairs, agent fees. Each £1,000 saves £450 at 45%.
3. **FIG threshold** (~£100k) is a rule of thumb; confirm against actual income before filing.
4. **Pension contributions at £135k** would restore some personal allowance and change scenarios 2 and 4.
5. **Personal Assessment in HK** only if Julian ever spends 180+ days there while letting; conflicts with UK residence.
6. **Capital gains base cost** for the flat (HK$8M plus stamp duty and renovation): evidence now, in case a future sale is a UK-allowable loss.

---

## 9. Sources

- HK Property Tax: [IRD guide](https://www.ird.gov.hk/eng/pdf/pam54e.pdf), [FAQ](https://www.ird.gov.hk/eng/faq/pty.htm)
- HK Personal Assessment: [pam37e](https://www.ird.gov.hk/eng/pdf/pam37e.pdf), [FAQ on election](https://www.ird.gov.hk/eng/faq/pa.htm)
- UK overseas property business: [PIM4702](https://www.gov.uk/hmrc-internal-manuals/property-income-manual/pim4702), [PIM2054](https://www.gov.uk/hmrc-internal-manuals/property-income-manual/pim2054), [PIM2058](https://www.gov.uk/hmrc-internal-manuals/property-income-manual/pim2058)
- FIG regime: [RFIG42100](https://www.gov.uk/hmrc-internal-manuals/residence-and-fig-regime-manual/rfig42100), [RFIG43000](https://www.gov.uk/hmrc-internal-manuals/residence-and-fig-regime-manual/rfig43000), [RFIG44000](https://www.gov.uk/hmrc-internal-manuals/residence-and-fig-regime-manual/rfig44000), [RFIG45100](https://www.gov.uk/hmrc-internal-manuals/residence-and-fig-regime-manual/rfig45100), [HS266 (2026)](https://www.gov.uk/government/publications/foreign-income-and-gains-fig-regime-self-assessment-helpsheet-hs266/hs266-foreign-income-and-gains-fig-regime-2026)
- Treaty: [2010 UK-Hong Kong DTA](https://www.gov.uk/government/publications/hong-kong-tax-treaties/2010-uk-hong-kong-double-taxation-agreement-in-force), Art. 6 and 21(2)(a)
- UK rates 2026/27: [gov.uk](https://www.gov.uk/income-tax-rates)
- Wiki inputs: [[financial-status-2026-07-07]], [[uk-move-financial-model]] §9, §11, §12, [[uktax-srt-fy26-27]] §5.11 and §8.8, [[uk-relocation-cashflows]]

---

## Key Takeaways

- **Two full computations, then a credit.** UK rules on the gross rent; HK tax comes off the UK bill.
- **Interest is offset nowhere.** UK: 20% credit. HK: nothing.
- **HK tax is £3,716 a year at HK$27,000 rent**, whatever the UK does.
- **No salary: the HK flat costs nothing in UK tax**, the London flat £2,131.
- **£135k salary: HK flat £6,196 UK tax, London flat £11,089.** FIG wipes the HK figure for four years; claim.
- **FIG only pays above about £100k of other income.** Never claim below £75k.
