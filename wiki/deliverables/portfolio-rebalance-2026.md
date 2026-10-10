---
type: deliverable
kind: task
created: 2026-10-10
status: defined
size: TBC
workstream: finance
tags: [deliverable, finance, investments, isa, mpf]
---

# Portfolio Rebalance 2026

## Purpose

The decision on how to reposition Julian's ISAs and MPF against an AI-led stock market crash, and the steps to carry it out. It exists so the choice is made against one written brief and one set of facts before any money moves.

Sections: Status; Prompt Zero; Findings so far; Options on the table; Open checks; Outputs; Time and Token Log; Session Synopsis; Document Log.

## Status

> As of 10 Oct 2026: exploratory analysis done in conversation (8-10 Oct) and captured below. Prompt Zero not yet written, so nothing here is a decision. No money has moved.

Serves Goal 1 in [[finance-workstream]] (automated investment portfolio strategy). Holdings, assumptions, charges and returns: [[investment-holdings]].

## Prompt Zero

*Override, 10 Oct 2026: Julian declined Prompt Zero for this deliverable. In its place, the brief is built through an investment-adviser style fact-find (Claude asks, Julian answers in his own words); his answers are recorded under Fact-find below.*

## Findings so far

All figures from [[investment-holdings]] unless stated. Property values are Julian's estimates, not valuations.

**Whole wealth (approx., HK$10.3 = £1):**

| Asset | Equity | Share |
|-------|--------|-------|
| Cecil Road, London (~£800k less £50k mortgage; based on an £850k asking price nearby, assumed to sell at £800k) | ~£750k | 56% |
| ISA funds (shares) | £321.6k | 24% |
| MPF (HK$1.245M; about 44% shares, 56% bonds, on assumptions) | ~£121k | 9% |
| Cash: HK ~£68k, UK £13.2k after a £3.3k tax bill, ISA cash £14.8k | ~£96k | 7% |
| DB flat, Hong Kong (HK$6.5M less HK$6.0M mortgage) | ~£49k | 4% |
| **Total** | **~£1.34M** | |

- **Spending:** about £3.7k a month (HK$30k + £800), no salary. Cash covers about 22 months.
- **The biggest concentration is property (about 73% of gross assets), not AI.** The DB flat is at 92% loan-to-value, so a 10% fall in Hong Kong prices costs more than its equity.
- **AI/US exposure:** ISA US trackers £233.5k plus about £33k of MPF shares, about £265k in total. Most of the companies at the top of US indexes are AI-linked.
- **Crash test** (US -40%, other markets -30%, illustrative): ISA funds lose about £120k, about 9% of net worth.
- **In past sell-offs, other regions fell with the US** (2022, Apr 2025). Only cash, government bonds and gold have reliably held up. The UK fell least both times.
- **The five active funds trailed their own market's tracker by roughly 13-22 points over five years,** and cost 0.66-1.14% a year against 0.05-0.20% for trackers.
- **ISA rules from 6 Apr 2027 (under 65):** transfers from stocks and shares ISAs to cash ISAs are banned; new cash ISA payments are capped at £12k a year; interest on cash held inside a stocks and shares ISA is charged at 22%. Julian is non-resident, so he cannot add new money at all; transfers are the only route. HMRC laid the regulations before Parliament on 14 Sep 2026.
- **Fidelity:** no charge for switching funds or transferring out. The service fee is 0.20% at £250k or more and 0.35% below; ETFs in an ISA are capped at £90 a year. Funds on the platform are held separately from Fidelity's own assets; the £120k protection limit applies to bank deposits, not funds.

## Options on the table

These are the options discussed, not decisions:

| Option | Money moved | Effect |
|--------|-------------|--------|
| Five lagging active funds + both Santander cash ISAs to a Virgin 1-year fixed cash ISA (4.77%) | £84,195 (£86,717 with the Fidelity cash) | Defensive share of ISAs + MPF rises from 18% to about 34%; earns about £4.0k a year; US exposure unchanged at about 58% |
| Switch the three US trackers to one S&P 500 ETF (VUAG or CSP1) | £233,545 | Fidelity fees fall from about £874 to about £150 a year; slightly more weight in AI-linked giants |
| Reduce the US further (UK tracker, equal-weight S&P 500, global ex-US, gilts, gold) | Open | The only change that reduces AI exposure itself |
| Julian's original target: about 50% defensive | About £160k from the ISAs alone | Costs about £4.8k a year in lost growth if no crash comes (assuming shares beat cash by 3% a year) |

Caution raised: moving only the non-US funds raises the US share of the remaining shares to 94%.

## Open checks

| # | Check | Why it matters |
|---|-------|----------------|
| 1 | Will Virgin open the 4.77% fixed cash ISA for a non-UK resident, by transfer in? If not, use the existing Santander cash ISAs | The main blocker for the cash leg |
| 2 | Virgin early-withdrawal penalty, and whether the 4.77% product accepts transfers | Determines how much cash stays available to buy shares after a crash |
| 3 | Complete the transfers by about Feb 2027 (they can take up to 30 days) | The 6 Apr 2027 ban on transfers into cash ISAs |
| 4 | Confirm the MPF fund mix on eMPF (assumptions A3-A7 in [[investment-holdings]]) | About £121k rests on assumptions |
| 5 | Whether a money market fund held in an ISA counts as cash for the 22% charge | Affects whether a money market fund is usable for cash |
| 6 | Fidelity: whether the 0.20% fee rate applies to the whole balance, and whether a non-resident can buy ETFs | Size of the fee saving |
| 7 | Keep each banking group under £120k (Virgin is part of Nationwide) | Deposit protection |

## Outputs

- [[investment-holdings]] - Holdings register with assumptions, MPF, charges and tracker comparison
- [[investment-holdings-5y-performance.svg]] - Five-year performance chart

## Time and Token Log

| Date | Who | Effort | Notes |
|------|-----|--------|-------|
| 8-10 Oct 2026 | Julian (attended) | TBC | Exploratory session; minutes to be supplied by Julian |
| 8-10 Oct 2026 | Claude (interactive session) | TBC | To be summed from the session transcript at handback |
| 10 Oct 2026 | Claude subagent (fund/ETF charges research) | 85,461 tokens | Verified fund OCFs and ETF TERs |

## Session Synopsis

*Filled at handback: Julian's rating and comments first, then Claude's comment beneath.*

## Document Log

| Date | Change |
|------|--------|
| 10 Oct 2026 | Created from the 8-10 Oct exploratory session; Prompt Zero pending |
