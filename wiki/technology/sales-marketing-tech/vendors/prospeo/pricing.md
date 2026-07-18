---
vendor: Prospeo
last-verified: 2026-05-04
source: https://prospeo.io/pricing + https://prospeo.io/s/how-to-reverse-email-lookup
---

# Prospeo — Pricing

## Plans (Annual Billing)

| Plan | Monthly (annual) | Credits/year | Credits/month | Cost/credit |
|------|-----------------|--------------|---------------|-------------|
| Free | $0 | 1,200 | 100 | $0 |
| Starter | $37/mo | 24,000 | 2,000 | ~$0.02 |
| Growth | $74/mo | 60,000 | 5,000 | ~$0.01 |
| Pro | $187/mo | 180,000 | 15,000 | ~$0.01 |

## Credit / Usage Model

- 1 credit = 1 verified business email enrichment
- 10 credits = 1 direct mobile number
- Credits do NOT roll over on renewal
- Chrome extension credits: 100/month free (separate from paid plan credits)

## TCO Notes for Reverse Email Lookup (Email → LinkedIn URL)

### ⚠️ Critical Gap — LinkedIn URL Output NOT Confirmed

Prospeo's reverse email lookup (email-in → profile data-out) returns:
- ✓ Name, job title, company
- ✓ Direct dial phone number
- ✓ 50+ additional data points
- ❌ **LinkedIn URL: NOT explicitly listed in feature documentation**

Source: [prospeo.io/s/how-to-reverse-email-lookup](https://prospeo.io/s/how-to-reverse-email-lookup) — LinkedIn URL is absent from the field list.

> ⚠️ **Ruled out for current workflow**: The pipeline requires email → LinkedIn URL as an output field to feed into the linkedin-enrichment skill. This is unconfirmed for Prospeo. Use free tier (75 lookups/month) to test before committing.

### Prospeo's Primary Direction
Prospeo's core speciality is the **opposite direction**: LinkedIn URL → email (finding verified emails from LinkedIn profiles). Its reverse email lookup is a secondary feature with less documented output fidelity.

### Comparison vs SalesQL at 1,000 lookups/month

| Vendor | Plan | Cost | Credits | LinkedIn URL Output |
|--------|------|------|---------|---------------------|
| Prospeo Starter | $37/mo | $37/mo | 2,000/mo | ❌ Not confirmed |
| SalesQL | $39/mo | $39/mo | 2,000/mo | ✓ Confirmed (LinkedIn-native) |

SalesQL is $2/mo more expensive but has confirmed LinkedIn URL output — strongly preferred for this use case.
