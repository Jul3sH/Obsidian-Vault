---
type: reference
created: 2026-09-04
status: active
tags: [finance, airmiles, ba-avios]
---

# BA Avios Redemption

This is the BA Avios scheme reference: how to value an Avios redemption, how
to choose the right point on the Avios-plus-cash slider, and when to redeem
versus pay cash. It was created (4 Sep 2026) from Julian's analysis of a
Hong Kong to Bangkok booking. It is the detail layer behind
[[mm-airmiles-redemption]]: consult it whenever a BA reward flight is being
considered; if this file and the model disagree, this file wins.

## Key Takeaways

- Judge each redemption by the cash fare you avoid, not by the number of
  flights you can spread Avios across. Plan at **1p per Avios**; redeem at 1p+,
  prefer 1.2p+, avoid well below 1p unless flexibility or conserving cash is
  worth more.
- Compare against cash first: if the award's cash co-pay is near or above the
  real cash fare, pay cash and keep the Avios.
- On the slider, value each incremental step; stop once the next increment
  saves less than ~1p per Avios. The maximum-Avios option is frequently poor
  value (0.5-0.8p).
- On the same itinerary, an expensive premium cabin can be a far better
  redemption than cheap Economy.

## Core calculation

Value per Avios = (cash fare you would realistically buy - cash co-pay on the
Avios ticket) / Avios used.

Use the actual comparable fare: same route, dates, cabin, baggage, passenger
count, and fare conditions. Do not compare an Avios booking with an expensive
fully flexible fare you would never actually buy.

| Value achieved | Interpretation | Default action |
|---:|---|---|
| Below 0.8p per Avios | Poor | Pay cash; retain Avios |
| 0.8-1.0p | Acceptable | Use if flexibility or cash-flow saving matters |
| 1.0-1.2p | Good | A sound Avios use |
| 1.2-1.8p | Very good | Prioritise the redemption |
| Above 1.8p | Excellent | Usually a strong use, if the cash alternative is real |

## Choose the slider intelligently

For BA's "Avios + cash" options, assess each **incremental step**, not just
the overall total:

Incremental Avios value = (reduction in cash co-pay) / (extra Avios used).

- Select the point where the next increment of Avios saves cash at **about 1p
  or more per Avios**.
- Stop adding Avios once each additional Avios only reduces the cash payment
  by less than your target value.
- Do not automatically choose the maximum-Avios / lowest-cash option: it
  frequently provides very poor value, sometimes only 0.5-0.8p per Avios.

### Worked examples (Sep 2026, Hong Kong to Bangkok)

| Cabin | Best slider choice | Why |
|---|---:|---|
| Premium Economy | **33,000 Avios + HK$3,427** | The move from 25,400 Avios + HK$4,377 saves HK$950 for 7,600 Avios: about **1.18p per Avios**. Above 33,000 Avios, value fell to roughly 0.51-0.79p per Avios. |
| Economy | **27,500 Avios + HK$1,870** (only if redeeming) | The final move from 21,500 Avios + HK$2,550 saves HK$680 for 6,000 Avios: about **1.07p per Avios**. The 38,500-point option was especially poor at about 0.49p per Avios. |

## Compare against cash first

Before analysing the Avios slider, check whether the **cash co-pay exceeds
the cash ticket price**:

- **Economy example:** cash fare was THB5,500, around HK$1,307. The lowest
  cash Avios option still required HK$1,870 plus Avios. Therefore, pay cash:
  an Avios booking would cost more cash *and* consume Avios.
- **Premium Economy example:** cash fare was THB31,540, around HK$7,494. The
  recommended redemption was 33,000 Avios + HK$3,427, saving about HK$4,067
  and yielding roughly **1.16p per Avios**. This was the clear Avios winner.

For the same itinerary, a relatively expensive premium cabin can therefore be
a far better redemption than cheap Economy. In this example, the cash Premium
Economy upgrade cost roughly HK$6,188, whereas using the chosen Avios options
raised the effective cost by only **5,500 Avios + HK$1,557**.

## When Avios work best

Use Avios selectively rather than spreading them indiscriminately:

- Peak dates, school holidays, weekends, and short-notice travel, when cash
  fares are high.
- Long-haul Premium Economy, business class, or partner-airline awards where
  the cash fare is materially higher than the taxes and carrier charges.
- One-way flights with disproportionately high cash fares.
- Travel where the ability to cancel is valuable.
- Short-haul routes only when the paid fare is expensive enough to justify
  the points.

Usually pay cash for:

- Very cheap Economy fares.
- Redemptions where the cash co-pay is near, equal to, or higher than the
  sale fare.
- Hotel, shopping, and low-value Avios & Money uses, which often return
  materially less than 1p per Avios.
- The highest-Avios slider option where it simply reduces cash at a poor
  exchange rate.

## Flexibility and cancellation

As of Sep 2026: a standard BA Reward Flight is normally cancellable more than
**24 hours before the first flight departs**, with Avios re-credited and the
cash amount refunded less the applicable cancellation/redeposit charge. For
UK-priced bookings, the normal charge is **£35 per person**, or the lower
cash/taxes amount where applicable. Cancelling within 24 hours usually means
losing the Avios. Verify current terms at
[britishairways.com](https://www.britishairways.com/content/the-british-airways-club/avios/spending-avios/reward-flights)
before relying on this.

For an itinerary you may cancel:

- Compare a return award versus two one-way awards.
- A return booking can be cheaper to cancel if you expect to cancel both
  directions.
- Separate one-ways can be useful if you need the freedom to change or cancel
  only one direction.
- Always check the cancellation cost and the cash element before booking;
  flexibility has real value and can justify a slightly lower pence-per-Avios
  result.

## Simple personal rule

1. Value Avios at **1p each** for planning.
2. Check the equivalent cash fare first.
3. Calculate pence-per-Avios using the fare avoided minus the Avios ticket
   cash co-pay.
4. Use the Avios slider only up to the last increment worth around **1p+ per
   Avios**.
5. Pay cash for cheap Economy; reserve Avios for expensive dates, premium
   cabins, or genuinely high cash fares.
6. Treat booking flexibility as a benefit, but do not let it turn an
   otherwise poor redemption into a routine use of points.
