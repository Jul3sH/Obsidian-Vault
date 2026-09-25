---
type: review
reviewer: Codex
source: tax-rental-incomes
date: 2026-09-25
authority: adversarial-review
---

This is an independent adversarial review of [[tax-rental-incomes]], checking its arithmetic, tax law and recommendations. It exists to identify corrections before Julian uses the figures for relocation or tax elections; use it alongside the unchanged source, internal only, `send: NEVER`.

| # | Location (section) | Claim in document | Your finding | Direction of error (understates tax / overstates tax / neutral) | Severity (Material / Marginal / Immaterial) | Proposed correction |
|---|---|---|---|---|---|---|
| 1 | §3, §6 | Future exposure remains £6,196; current rates carried forward. | Separate property rates become 22% / 42% / 47% in 2027/28, with a 22% finance-cost reducer. Same-input HK top-up becomes £28,500.40 × 47% - £14,565.60 × 22% - £3,715.824 = **£6,474.932**, not £6,196. Even the no-salary HK-free result ceases to hold: calculation below. [Finance Act 2026][fa26]; [HMRC technical note][future]. | understates tax | Material | Keep 2026/27 examples clearly historical to the intended move. Rebuild §6 using the new rates, and label later years as projections with changing interest, FX and annual rates. |
| 2 | §5, §6, §7, Key Takeaways | FIG only pays above about £100k; never below £75k. | Wrong at the updated rent. At £75k salary, no-claim HK increment is £5,471.296 versus £5,028 allowance cost with FIG: **£443.296 saved**. Break-even other ordinary income is about £72,784, derived below, before other FIG costs. The older HK$25k sensitivity gives a different answer. | overstates tax | Material | Replace the universal threshold with an annual whole-return comparison. Update the sensitivity table to HK$27k and include Cecil profit when specifying other income. |
| 3 | §2.1, §4, §8.5, Key Takeaways | HK interest relief requires 180+ days and conflicts with UK residence; HK tax is unchanged. | Personal Assessment also permits ordinary residence or more than 300 days over two consecutive HK assessment years, one being the election year. The single-year threshold is **more than 180**, not 180+. UK residence does not itself prevent eligibility. The permitted files do not establish the necessary HK facts or total assessable income. [IRD guide][pa]. | overstates tax | Material | Describe £3,716 as Property Tax before any beneficial Personal Assessment election. Check eligibility and recompute HK tax and the corresponding UK credit together. |
| 4 | §5 sale bullet, §8.6 | HK$6M versus HK$8M means a loss, so do not claim FIG in the disposal year. | HK$6M - HK$8M = -HK$2M is not a UK allowable-loss computation. Acquisition and sale require their own sterling exchange rates; former-home relief can disallow all or part of a loss. Those rates, dates, costs and relief history are missing. A loss's usable tax value must also be compared with the income-tax saving sacrificed. [CG78310][fx]; [HS283][prr]. | overstates tax | Material | Remove the automatic no-claim instruction. Compute the allowable sterling loss and compare whole-year outcomes. A rent claim does not automatically exempt a sale gain: identify that gain in a foreign-gain claim. [HS266][fig]. |
| 5 | §5 eligibility, §6 opening | Julian has the qualifying history; 2026/27 is non-resident on a locked position. | The permitted SRT paper §9.2 expressly makes the historical residence claim subject to evidence; §9.7 and its conclusion retain a home-status dependency. Future travel and family facts still matter. Twelve years is consistent with 2025 - 2014 + 1 = 12 tax years, but assertion is not verification. | understates tax | Material | Carry those qualifications into this document. The four-year calendar is correct only conditional on the stated first resident year and evidenced eligibility. |
| 6 | §1 scenario labels, §2.1 | Scenario 1 has no other earnings. | Its working includes £25,778 Cecil profit. HK alone has pre-credit UK tax (£28,500.40 - £12,570) × 20% - £2,913.12 = **£272.96**, not £3,588. Both end at £0 after credit, but the allowance-cost explanation only applies when other taxable income exists. | neutral | Marginal | Label scenario 1 as the incremental HK tax with Cecil already let, or show genuinely standalone scenarios separately from combined cases. |
| 7 | §4, §5 | Reducer capped by property profit; unused carries forward; FIG costs this year's overseas reducer. | The cap also uses adjusted total income, shared across businesses. Carried-forward property losses affect the profit cap. FIG also extinguishes the overseas finance-cost amount carried to the following year; qualifying foreign trading/property losses in a claim year cannot be carried forward, and prior losses can be consumed before FIG relief. [PIM2058][caps]; [RFIG43000][effects]. | understates tax | Marginal | State all caps and distinguish unused finance costs from unused tax credits. Include loss and carry-forward destruction in the election comparison; no opening balances are established in the permitted inputs. |
| 8 | §2.5, §3, Key Takeaways | Banked annual costs; flat does not cost net worth. | The cash/equity identity is correct, conditional on the target rent and listed costs. A monthly mortgage snapshot is not a verified annual interest bill; rates invoices, future owner-paid rates, repairs, voids and actual letting costs are not established. The stated first-year fee alone is HK$13,500 / 12 = HK$1,125 extra monthly cash cost before its UK tax effect. | neutral | Marginal | Call this an illustrative recurring cash surplus before omitted costs, with principal repayment separated. Verify invoices, loan use and actual annual interest; do not present unchanged annual values as settled. |
| 9 | §8.1 | Reducer-before-FTCR is a conservative ordering awaiting confirmation. | It is required: ITA 2007 s27(6) puts double-tax relief after other reductions; TIOPA s36(5)(d) includes other reductions in the attribution calculation. HS263 also removes associated finance costs when removing foreign rent. [s27][order]; [s36][credit]; [HS263][ftcr]. | neutral | Immaterial | Remove the suggestion of an elective ordering. £0 incremental HK tax survives; there is no legitimate extra credit against Cecil tax. |
| 10 | §1, §2.1, §2.3, §2.5 | £2,131 Cecil tax; £5,847 low-income combined; £128 unused HK credit. | Premature rounding: (£25,778 - £12,570) × 20% - £2,556 × 20% = **£2,130.40**; plus £3,715.824 = **£5,846.224**. Unused credit = £3,715.824 - £3,588.64 = **£127.184**. Cash rounding differences are shown below. | overstates tax | Immaterial | Retain precision through the computation and round only final figures. These differences do not change the 2026/27 decisions. |

## Numbers I re-derived

Basis: 2026/27 England rates, sole ownership, full-year letting, no other reliefs or opening losses, and the document's planning FX of HK$10/£1. These are conditional planning calculations, not return-box rounding. UK and overseas property businesses are separate under [PIM4702][overseas]; residential interest uses the restricted relief described in [PIM2054][restriction].

- **HK Property Tax H:** (324,000 - 14,348) × 80% = HK$247,721.60; × 15% = **HK$37,158.24**; / 10 = **£3,715.824**. Agrees with HK$37,158 and £3,716 rounded, provided the rates were owner-paid. Actual management costs and interest are not Property Tax deductions. [IRD Property Tax guide][hk]; [IRD rates example][hkrate].
- **UK HK profit P:** (324,000 - 14,348 - 24,648) / 10 = **£28,500.40**, agreeing with £28,500 rounded. HK finance cost = 12,138 × 12 / 10 = **£14,565.60**; reducer R = 20% × 14,565.60 = **£2,913.12**.
- **Cecil:** 30,000 - 3,240 - 432 - 550 = **£25,778**; reducer D = 20% × 2,556 = **£511.20**. The supporting monthly interest gives 213.08 × 12 = £2,556.96, a £0.96 input difference and £0.192 reducer difference; it changes no material conclusion.
- **Caps:** min(finance cost, adjusted business profit) gives HK £14,565.60 and Cecil £2,556. Their sum £17,121.60 is below both-property adjusted total income: 28,500.40 + 25,778 - 12,570 = **£41,708.40** without salary, or 135,000 + 28,500.40 + 25,778 = **£189,278.40** with salary. Separately, HK-only ATI = £15,930.40 and Cecil-only ATI = £13,208; both exceed their finance costs. Hence full reducers in all four scenarios, no new cap-generated carry-forward. The combined ATI test must precede allocation if binding. [PIM2058][caps].
- **Bands and salary:** PA = max(0, 12,570 - max(0, income - 100,000) / 2). At £135k it is zero. Salary tax = 37,700 × 20% + (125,140 - 37,700) × 40% + (135,000 - 125,140) × 45% = **£46,953**, agreed. Both-property no-salary gross tax = 37,700 × 20% + (41,708.40 - 37,700) × 40% = **£9,143.36**, agreeing with £9,143. [Rates and allowances][rates].

| Scenario or total row | Document: UK / combined | My arithmetic: UK / combined | Agree? |
|---|---|---|---|
| 1: HK increment with Cecil already let | £0 / £3,716 | Pre-credit total = 9,143.36 - 2,913.12 - 511.20 = 5,719.04. HK cap = 5,719.04 - 2,130.40 = 3,588.64. Increment = 3,588.64 - min(3,715.824, 3,588.64) = **£0**; combined = 0 + H = **£3,715.824**. | Yes, with corrected label. |
| 2: HK plus £135k salary | £6,196 / £9,912 | P × 45% - R = 9,912.06; less H = **£6,196.236**; plus H = **£9,912.06**. | Yes, rounded. |
| 3: Cecil alone | £2,131 / £2,131 | (25,778 - 12,570) × 20% - D = **£2,130.40**, both columns. | Disagree by rounding only. |
| 4: Cecil plus £135k salary | £11,089 / £11,089 | 25,778 × 45% - D = **£11,088.90**, both columns. | Yes, rounded. |
| Both, no salary | £2,131 / £5,847 | 5,719.04 - 3,588.64 = **£2,130.40**; plus H = **£5,846.224**. | Disagree by rounding only. |
| Both, £135k salary | £17,285 / £21,001 | 6,196.236 + 11,088.90 = **£17,285.136**; plus H = **£21,000.96**. | Yes, rounded. |
| Both, £135k salary, FIG | Combined £14,805 | UK = **£11,088.90**; plus H = **£14,804.724**. UK reducer D survives; s845D removes the overseas reducer only. | Yes, rounded. |

The credit mechanism agrees with [DTA Article 21(2)(a)][dta] and [TIOPA s36][credit]. Subtracting the same lawful capped credit before the reducers gives 9,143.36 - 3,588.64 - 2,913.12 - 511.20 = £2,130.40 too. Improperly using the full H instead gives £2,003.216, or £127.184 below Cecil-only tax; that is not an alternative permitted by the legislation. HK-only tax also remains zero under the lawful cap: 272.96 - min(H, 272.96) = £0.

**FIG sensitivity check:** at the old HK$25k rent, P25 = (300,000 - 14,348 - 24,648) / 10 = £26,100.40 and H25 = (300,000 - 14,348) × 12% / 10 = £3,427.824. The following increments exclude baseline tax on the other income.

| Other income in §5 | Document: no claim / claim | Re-derived calculation and verdict |
|---|---|---|
| None | £0 / £0 | (26,100.40 - 12,570) × 20% = £2,706.08; capped reducer = 20% × min(14,565.60, 26,100.40, 13,530.40) = £2,706.08; UK £0 either way. No claim is reasonable, but rental tax is tied. |
| £27k UK rental profit | £0 / £2,514 | HK pre-credit increment = 26,100.40 × 20% + 2,830.40 × 20% - R = £2,873.04 < H25, hence £0. Claim cost = 12,570 × 20% = £2,514. No claim, assuming no binding UK reducer cap. The old row does not identify its UK finance cost or whether £27k is gross or profit. |
| £75k salary | £4,100 / £5,000 | 26,100.40 × 40% + 1,100.40 × 20% - R - H25 = **£4,319.296**; claim cost = 12,570 × 40% = **£5,028**. No claim saves 5,028 - 4,319.296 = **£708.704**. £4,100 is understated. |
| £110k salary | £7,700 / £3,000 | 15,140 × 60% + 10,960.40 × 45% - R - H25 = **£7,675.236**; claim cost = (12,570 - 10,000 / 2) × 40% = **£3,028**. Claim saves **£4,647.236**. |
| £150k+ salary | £5,400 / £0 | 26,100.40 × 45% - R - H25 = **£5,404.236**; allowance already zero, claim cost £0. Claim. |

At the new rent and £75k salary: P × 40% + (75,000 + P - 100,000) × 20% - R - H = **£5,471.296** without FIG; less £5,028 claim cost gives **£443.296** saving. Solving the same expression for break-even other income U gives U = 100,000 - P + (5,028 - 0.4P + R + H) / 0.2 = **£72,783.52**; with Cecil profit already present, equivalent salary = 72,783.52 - 25,778 = **£47,005.52**. These thresholds exclude other gains, losses, allowances and reliefs. The §1 no-salary no-claim and £135k claim verdicts survive on its stated inputs.

Eligibility requires ten consecutive non-resident tax years immediately before the first qualifying resident year; the window then spans that year and the next three, without pausing. Annual claims can identify selected sources; overseas property profits qualify, Cecil profits do not. These parts agree with [RFIG44000][eligible], [RFIG42100][claims] and [RFIG45100][qualifying]. Loss of PA and CGT exemption is correctly identified, but “claim costs nothing” assumes those and other sacrificed reliefs have no usable value.

**Cash and future-year cross-checks:**

- §2.5 displayed arithmetic is internally correct: 25,827 + 6,347 - 27,000 = **HK$5,174**; + 5,163 = **HK$10,337**; equity-adjusted changes = 13,689 - 5,174 = **HK$8,515**, and 13,689 - 10,337 = **HK$3,352**. Using unrounded inputs, overhead = (24,648 + 14,348 + 37,158.24) / 12 = HK$6,346.1867; cash shortfall = **HK$5,173.1867**; net-worth increase = 13,689 - 5,173.1867 = **HK$8,515.8133**. UK tax = 6,196.236 × 10 / 12 = HK$5,163.53; resulting cash shortfall = **HK$10,336.7167** and net-worth increase = **HK$3,352.2833**. Principal is equity accumulation, not deductible rental expense.
- Ancillary rounding checks: 9,912.06 / 28,500.40 = **34.78%**; 9,912.06 / 12 = **£826.005**; 2,130.40 / 12 = **£177.533**; 11,088.90 / 12 = **£924.075**; 6,196.236 / 12 = **£516.353**. Four unchanged 2026/27 years give 4 × 6,196.236 = **£24,784.944**, explaining the approximate £25k, but not validating future-year rates. The stated principal-driven annual interest fall is approximately 164,268 × 2.47% = **HK$4,057.42**, conditional on a constant rate.
- At 2027/28 rates, both-property no-salary UK tax = 37,700 × 22% + 4,008.40 × 42% - (14,565.60 + 2,556) × 22% - H = **£2,494.952**. Cecil alone = (25,778 - 12,570 - 2,556) × 22% = **£2,343.44**; HK increment = 2,494.952 - 2,343.44 = **£151.512**. The source's Key Takeaways match §1 apart from rounding, but its universal FIG threshold and future-year extension do not survive.

## Integrity

- Scope: only the four authorised vault files were read; only this new review file was written. Official external sources were used for legal verification.
- Findings: **5 Material / 3 Marginal / 2 Immaterial**.
- Pre-run source SHA-256: `39369cef4f471fdac4e4593b19e8f359c4db4a7d138285e46903751f2d37d74c`.
- Post-run source SHA-256: `39369cef4f471fdac4e4593b19e8f359c4db4a7d138285e46903751f2d37d74c`. **MATCH: source byte-identical.**

## Verdict

As of 25 September 2026, the document is not safe to act on as a tax-election or future-year planning guide. Its 2026/27 headline rental totals are broadly sound, but first correct the post-April-2027 rates, FIG threshold and sale-loss advice, Hong Kong Personal Assessment eligibility, and unsupported residence certainty; then verify actual costs and residence evidence before filing or making elections.

[fa26]: https://www.legislation.gov.uk/ukpga/2026/11/section/7
[future]: https://www.gov.uk/government/publications/changes-to-tax-rates-for-property-savings-and-dividend-income/change-to-tax-rates-for-property-savings-and-dividend-income-technical-note
[pa]: https://www.ird.gov.hk/eng/pdf/pam37e.pdf
[fx]: https://www.gov.uk/hmrc-internal-manuals/capital-gains-manual/cg78310
[prr]: https://www.gov.uk/government/publications/private-residence-relief-hs283-self-assessment-helpsheet/hs283-private-residence-relief-2026
[fig]: https://www.gov.uk/government/publications/foreign-income-and-gains-fig-regime-self-assessment-helpsheet-hs266/hs266-foreign-income-and-gains-fig-regime-2026
[caps]: https://www.gov.uk/hmrc-internal-manuals/property-income-manual/pim2058
[effects]: https://www.gov.uk/hmrc-internal-manuals/residence-and-fig-regime-manual/rfig43000
[order]: https://www.legislation.gov.uk/ukpga/2007/3/section/27
[credit]: https://www.legislation.gov.uk/ukpga/2010/8/section/36
[ftcr]: https://www.gov.uk/government/publications/calculating-foreign-tax-credit-relief-on-income-hs263-self-assessment-helpsheet/relief-for-foreign-tax-paid-2026-hs263
[overseas]: https://www.gov.uk/hmrc-internal-manuals/property-income-manual/pim4702
[restriction]: https://www.gov.uk/hmrc-internal-manuals/property-income-manual/pim2054
[hk]: https://www.ird.gov.hk/eng/pdf/pam54e.pdf
[hkrate]: https://www.ird.gov.hk/eng/faq/pty.htm
[rates]: https://www.gov.uk/income-tax-rates
[dta]: https://www.gov.uk/government/publications/hong-kong-tax-treaties/2010-uk-hong-kong-double-taxation-agreement-in-force
[eligible]: https://www.gov.uk/hmrc-internal-manuals/residence-and-fig-regime-manual/rfig44000
[claims]: https://www.gov.uk/hmrc-internal-manuals/residence-and-fig-regime-manual/rfig42100
[qualifying]: https://www.gov.uk/hmrc-internal-manuals/residence-and-fig-regime-manual/rfig45100
