---
vendor: Fresh LinkedIn Scraper API (by SaleLeads, RapidAPI)
last-verified: 2026-05-07
source: https://rapidapi.com/saleleadsdotai-saleleadsdotai-default/api/fresh-linkedin-scraper-api/pricing (verified directly by user, 2026-05-07)
---

# Fresh LinkedIn Scraper API — Pricing

> ✅ **Verified 2026-05-07:** Plan price, request quota, and overage rate confirmed against the live RapidAPI pricing page for the subscribed API (`saleleadsdotai-saleleadsdotai-default`). Previous audit flags from an earlier session (which reviewed a different product — `fresh-linkedin-profile-data`) are retracted.

---

## Confirmed Plans (as of 2026-05-07)

| Plan | Monthly Price | Requests/Month | Overage |
|------|--------------|----------------|---------|
| Basic | Not captured | Not captured | — |
| **PRO** | **$49/mo** | **20,000 requests** | **$0.008 per additional request** |
| Ultra | $199/mo | 100,000 requests | $0.0065 per additional request |
| Mega | $499/mo | 500,000 requests | $0.005 per additional request |

**Terminology note:** The API uses **"requests"** not "credits". Each API call deducts 1 from the monthly request quota, confirmed via `"cost": 1` in every response body.

---

## Active Subscription

| Plan | Monthly | Requests/Month | Overage | Status |
|------|---------|----------------|---------|--------|
| **PRO** | **$49/mo** | **20,000** | $0.008/request | **ACTIVE (subscribed 2026-04-28)** |

> 🎯 **Sunk Cost Note:** Active and paid through 2026-05-28. For TCO calculations, treat as **$0/mo incremental cost** until next billing cycle.

---

## Cost Per Contact

| Endpoint sequence | Requests per contact | Monthly contacts (20,000 quota) |
|------------------|---------------------|--------------------------------|
| Current script (profile + experience + educations + posts) | **4 requests** | **5,000 contacts** |
| Minimal (profile only, no include flags) | 1 request | 20,000 contacts |
| Expanded (+ skills + contact info) | 6 requests | ~3,333 contacts |

**Confirmed:** `"cost": 1` per endpoint call. 4 calls × 1 request = 4 requests per fully enriched contact.

### Gotchas that affect request count
1. **`include_*` flags on `/profile`**: each enabled flag (e.g. `include_experiences`, `include_skills`) adds +1 request to the base 1. The current script does NOT use these flags.
2. **`urn` dependency**: `/profile` must be called first (1 request) to obtain the `urn` needed by the other 3 endpoints. This is already how the script works.
3. **Rate limit**: 20 requests/minute on PRO — caps throughput at ~5 contacts/minute (4 requests × 5 contacts = 20 req/min ceiling).

---

## TCO at Various Volumes

| Contacts/month | Requests needed | Within 20,000 quota? | Overage cost | Total cost (inc. subscription) |
|----------------|----------------|----------------------|-------------|-------------------------------|
| 1,000 | 4,000 | ✓ Yes (20% of quota) | $0 | $49/mo |
| 5,000 | 20,000 | ✓ Yes (100% of quota) | $0 | $49/mo |
| 6,000 | 24,000 | ✗ Over by 4,000 | $32 | $81/mo |
| 10,000 | 40,000 | ✗ Over by 20,000 | $160 | $209/mo |
| 25,000 | 100,000 | ✗ — Ultra plan better | — | $199/mo (switch to Ultra) |

---

## Bandwidth Fee

| Component | Included | Overage |
|-----------|----------|---------|
| Bandwidth | 10,240 MB/month | $0.001 per 1 MB over |

Rarely a limiting factor for LinkedIn profile scraping.

---

## TCO Notes
- PRO plan at $49/mo is sufficient for up to 5,000 fully enriched contacts/month with the current 4-endpoint script
- At 1,000 contacts/month (current volume), only 20% of the quota is used — significant headroom
- Switching to Ultra ($199/mo) only makes sense above ~25,000 contacts/month
- Must be paired with Apollo (~$49/mo) to resolve emails → LinkedIn URLs, and with a sequencer (Lemlist, Instantly) to send
