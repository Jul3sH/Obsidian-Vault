---
type: review
reviewer: Codex
source: UK Relocation savings comparison v3
date: 2026-09-25
authority: adversarial-review
deliverable: savings-v3-review
---

This reviews the v3 relocation savings sheet against Julian's briefing, [[tax-rental-incomes]] and [[tax-rental-incomes-codex-review-2026-09-25]]. It checks whether the revised tax and cashflow calculations support the comparison. Julian and the coordinating agent should use the findings to correct the model before relying on its ten-year figures; internal only, `send: NEVER`.

# Savings v3: Codex Review

**Map:** verdict and findings; all-scenario tax check; cashflow reconciliation; scope.

## Key Takeaways

- **As of 25 Sep 2026: annual property-tax calculations pass on the supplied basis; the ten-year projection does not.** It extends FIG relief past its four-year window.
- At £135k salary, this overstates ten-year London and Malvern savings by **HK$360,156 each (about £36,016)**, holding everything else constant.
- HK salary tax uses an outdated basic allowance. Updating it increases every positive-salary HK scenario's savings by **HK$2,210/year**.
- Tax amounts are hardcoded. The displayed `OK` checks do not validate tax or detect stale amounts after an input change.

## Findings

| Severity | Cells | Finding and direction | Correction |
|---|---|---|---|
| Material | v3 `C6:G11`, `I6:M11`; assumption `B42` | Cumulative formulas multiply row 31 by years, including FIG savings in years 5 to 10. **Overstates UK savings.** | Tie eligibility to the first resident tax year. Use no-FIG tax after expiry. If Y1 is the first qualifying year, cumulative savings = `n × annual savings − max(n−4,0) × (no-FIG tax − tax used)`. |
| Material for reuse | v3 `B21:S22`, `B27:S29`; checks `B12:S12`, `B32:S32` | Salary and property taxes are literals. Changing salary, rent or costs changes cashflow but leaves taxes frozen; `OK` can remain. **Direction depends on the edit.** | Derive taxes from explicit inputs and add an independent tax check. Until then label the workbook a fixed-input snapshot requiring tax recomputation after edits. |
| Marginal | v3 `O21:S21`, `B40` | HK basic allowance is HK$132,000; enacted allowance from 2026/27 is **HK$145,000**. **Understates HK savings by HK$2,210/year** in all five working scenarios. | Salary tax should be **84,850 / 144,350 / 186,850 / 212,350 / 297,350** at the five positive salary bands. Child/single-parent relief remains excluded as instructed. |

The FIG window is the first qualifying UK-resident tax year plus the next three, whether claims are made or not: [HMRC RFIG44000](https://www.gov.uk/hmrc-internal-manuals/residence-and-fig-regime-manual/rfig44000). The HK allowance change was enacted in May 2026: [IRD budget FAQ](https://www.ird.gov.hk/eng/faq/budget2026_27.htm). Neither finding reopens the settled rental-tax review.

**FIG expiry only, using the sheet's rounded amounts:**

| Salary | London ten-year overstatement, HK$ | Malvern ten-year overstatement, HK$ |
|---|---:|---:|
| Zero | 0 | 0 |
| £75k | 5,934 | 287,316 |
| £110k | 314,736 | 360,156 |
| £135k / £150k / £200k | 360,156 | 360,156 |

At £135k, London Y10 falls from **2,272,380 to 1,912,224**; Malvern from **4,655,770 to 4,295,614**. These isolate FIG expiry, not all corrections or a new forecast. If fewer than four eligible years remain at Y1, the overstatement is larger.

## All-scenario tax check

Independent calculation, not a replay of the sheet's checks. Basis: FX 10; UK profit £25,860 when let; HK profit £27,495.40 when let; annual finance costs £2,556 UK and £14,565.60 HK. Salary taxed first, remaining property income at 22/42/47; allowance tapers on total income; 22% finance relief precedes the capped foreign credit. This matches the [HMRC property-tax technical note](https://www.gov.uk/government/publications/changes-to-tax-rates-for-property-savings-and-dividend-income/change-to-tax-rates-for-property-savings-and-dividend-income-technical-note). Finance-cost caps were checked, including the binding adjusted-income cap in London Zero; see [PIM2058](https://www.gov.uk/hmrc-internal-manuals/property-income-manual/pim2058).

**UK property-related tax, HK$, independently derived and rounded to whole dollars:**

| Salary | London no FIG | London FIG | Malvern no FIG | Malvern FIG | HK, no FIG applicable |
|---|---:|---:|---:|---:|---:|
| Zero | 0 | 0 | 23,615 | 51,269 | 23,615 |
| £75k | 51,269 | 50,280 | 201,155 | 153,269 | 23,615 |
| £110k | 82,736 | 30,280 | 198,655 | 138,629 | 23,615 |
| £135k | 60,026 | 0 | 175,945 | 115,919 | 23,615 |
| £150k | 60,026 | 0 | 175,945 | 115,919 | 23,615 |
| £200k | 60,026 | 0 | 175,945 | 115,919 | 23,615 |

All match rows 28 and 29. These are **increments above salary-only UK tax**, including allowance loss; row 29 is not simply tax on rent. In HK scenarios, the calculation assumes UK non-residence and entitlement to the UK personal allowance, as instructed.

- **HK Property Tax:** `(324,000 − 14,348) × 80% × 15% = HK$37,158.24`; row 27 rounds correctly in every let scenario, and is zero when occupied. Basis agrees with [IRD Property Tax instructions](https://www.ird.gov.hk/eng/tax/bir57se_notes.htm).
- **FIG choice:** all row-30 choices correct within eligibility. London Low saves **£98.892**, not a large benefit; Malvern Zero is **£2,765.40 worse** with a claim. London Zero is a tax tie, so no claim is preferable absent another reason.
- **£135k salary:** UK income tax **£46,953**, annualised NI **£4,710.60**, net **£83,336.40**: all correct. NI uses the [published thresholds and rates](https://www.gov.uk/guidance/rates-and-thresholds-for-employers-2026-to-2027). HK tax **189,060** reproduces the old allowance; **186,850** uses the current basic allowance.
- **Annual savings:** all 18 row-31 formulas correctly implement `take-home + (UK rent − UK expenses) × 10 + HK rent − HK expenses − HK Property Tax − UK tax used − living expenses`. No property-income or mortgage-interest double count was found in this bridge.
- **Immaterial precision:** UK NI is HK$4 too high in each £75k/£110k/£150k/£200k UK column because of whole-pound rounding. Actual cashflow interest £213.08/month implies £2,556.96/year, reducing relevant UK property tax by another HK$2.112/year versus the article's £2,556 basis. Neither changes a FIG choice.

## Cashflow reconciliation

The linked source's `Cashflow comparison!E181:G181` is **83,342.3 / 68,296.3 / 62,355.3 HK$/month** (HK / London / Malvern). Multiplying by 12 gives **1,000,107.6 / 819,555.6 / 748,263.6**. V3 uses **1,000,104 / 819,552 / 748,264**: only HK$3.60, HK$3.60 and HK$0.40 differences. Malvern's v3 amount agrees with the live source to whole-dollar rounding.

Both mortgage interest lines and Pine View principal are included once. The obsolete HK$17,330 line is absent. Housing subtotal row 109 is zero, so the property costs shown above it are excluded from living expenses and are picked up separately in v3.

**Source-budget flags to resolve, not silently adjust:**

| Source cells | Issue | Annual savings effect if corrected |
|---|---|---|
| `E92:G92` and `E157:G157` | Professional Wills appears twice at HK$70.8333/month, both counted. Confirm whether one service. | Removing one increases every scenario by **HK$850**. |
| `E135`, `E136` | HK column counts UK Oyster HK$500/month as well as Octopus HK$625/month. Confirm whether the Oyster cost belongs in HK. | Removing Oyster increases HK savings by **HK$6,000**. |
| `F107`, `F109` | UK contents insurance HK$180/month is excluded by the zero housing subtotal and is absent from v3's council-tax/buildings-insurance total. | Restoring this live budget item reduces London savings by **HK$2,160**. Check against the separate HK-contents-labelled `F110` first. |

The briefing's supplied annual property-cost totals were retained, including its known rounding differences and the older article-table mismatch. No input challenge is inferred from those accepted differences.

## Scope and handoff

Reviewed [v3, Sheet1](https://docs.google.com/spreadsheets/d/1TS-ve2WfgcBfNYrEaZCbl-4De_JdqHSqQbm_CdSZojM/edit) `A1:S53` and traced the [Cashflow comparison](https://docs.google.com/spreadsheets/d/1HP-4Gm7TUqftlnCiXFqe34Wpp4torBt3NOZOb9BG4U4/edit?gid=2028208137#gid=2028208137) through row 183. All 18 scenarios were checked; no sampling. Used the supplied briefing, the two tax documents and the relevant [[financial-status-2026-07-07]] inputs. V2 was not reviewed. Neither Google Sheet nor either tax document was edited.

As of 25 Sep 2026: review complete, findings await Julian's adjudication. Correct FIG expiry and the HK basic allowance, make tax recalculation explicit, then resolve the source-budget flags. This checks the stated planning basis, not residence evidence, actual tax returns, future interest/FX or a complete ten-year life forecast. Record: [[savings-v3-review]].
