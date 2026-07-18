# Stage 2 Decision Framework: Reverse Email Lookup

tags: [technical, lead-enrichment, decision-making, stage-2, reverse-email-lookup]

> *Decision tree for choosing a reverse email lookup service for Stage 2 of the lead enrichment pipeline. All options accept email as input and return a LinkedIn URL. LinkFinder AI is excluded — it is name-based and does not qualify.*

---

## Quick Decision Tree

**Are you already using Apollo for Stage 1 (prospecting)?**
- **Yes** → Use **Apollo People Match API** (Stage 1+2 consolidated; lowest cost at annual billing)
- **No** → Continue below

**Do you need the richest possible data per lookup (title + company + phone + intent signals)?**
- **Yes** → Use **Prospeo** (~$0.01/lookup; 98% email accuracy; returns full B2B profile)
- **No** → Continue below

**Do you want no monthly commitment (pay-per-use only)?**
- **Yes** → Use **ProxyCurl** ($0.003–$0.01/lookup; no minimum)
- **No** → Continue below

**Do you need credit rollover for uneven monthly volume?**
- **Yes** → Use **Lix** ($39–$109/mo; credits roll over; thinner data)
- **No** → Use **SalesQL Basic** ($39/mo; 2,000 credits; clear pricing; URL + title + phone)

---

## Decision Matrix

| Data Needed | Volume | Commitment | Best Choice | Why |
|---|---|---|---|---|
| **URL only** | Any | Pay-per-use | ProxyCurl | No minimum; $0.003–$0.01/lookup; good for testing |
| **URL + core profile (title, company, phone)** | <2,000/mo | Month-to-month | SalesQL Basic | $39/mo; 2,000 credits; $0.02/lookup; clear simple pricing |
| **URL only, credit rollover preferred** | Uneven | Month-to-month | Lix Leads | $39/mo; credits roll over; low data return |
| **Richest data (URL + phone + intent signals)** | Any | No contract | Prospeo | ~$0.01/lookup; 98% accuracy; full B2B profile; best data quality |
| **URL + consolidate with Stage 1** | Any | Annual | Apollo Basic | $49/seat/mo annual; ~$0.002/lookup; best cost if already on Apollo |

---

## Implementation Paths

### Path A: Apollo (Consolidated Stage 1 + 2)
**Best for:** Single platform for prospecting + reverse email lookup; annual budget commitment

**Pipeline:**
1. Upgrade Apollo to Basic or Professional (annual)
2. Build `apollo_person_match.py` — Read email → Call `/people/match` → Write `linkedin_url, title, company, phone` back
3. [[technology/lead-enrichment/linkedin-enrichment/_index|LinkedIn enrichment (Stage 3)]] uses `linkedin_url` as input ✓ (already built)

**Pros:** Lowest per-lookup cost (annual); single platform; returns full contact data in Stage 2
**Cons:** 60–70% email→URL match rate; requires annual commitment for best pricing

### Path B: Prospeo (Best accuracy + richest data)
**Best for:** When match rate matters most; when Stage 2 data enriches Stage 5 email quality

**Pipeline:**
1. Subscribe to Prospeo (no annual commitment)
2. Build `prospeo_match.py` — Read email → Call Prospeo API → Write `linkedin_url, title, company, phone, mobile` back
3. [[technology/lead-enrichment/linkedin-enrichment/_index|LinkedIn enrichment (Stage 3)]] uses `linkedin_url` as input ✓

**Pros:** 98% email accuracy; richest data return (~$0.01/lookup); no contract; best fallback-free match rate
**Cons:** Higher per-lookup cost than Apollo annual; separate tool from Stage 1

### Path C: ProxyCurl (Test / Low volume)
**Best for:** Testing the pipeline before committing to a paid plan; irregular/low volume

**Pipeline:**
1. No subscription — pay per call
2. Build `proxycurl_match.py` — Read email → Call ProxyCurl → Write `linkedin_url` back

**Pros:** No minimum spend; good for testing; developer-friendly API
**Cons:** Thin data return; ~70% estimated accuracy; more expensive per-lookup at scale

### Path D: SalesQL (Mid-volume, simple pricing)
**Best for:** Moderate volume with predictable monthly budget; want URL + phone without complexity

**Pipeline:**
1. Subscribe SalesQL Basic ($39/mo)
2. Build `salesql_match.py` — Read email → Call SalesQL → Write `linkedin_url, title, phone` back

**Pros:** Simple credit pricing; 2,000 credits/mo; returns phone numbers on Basic plan
**Cons:** $0.02/lookup is mid-range; less data than Prospeo

---

## Current Recommendation

**Start with Apollo (if upgrading plan anyway):** Apollo handles Stages 1+2 in one platform at lowest annual cost per lookup. Test actual match rate on your specific lead data.

**If Apollo match rate proves insufficient (<60% on your leads):** Switch Stage 2 to **Prospeo** — 98% email accuracy, richer data return, no annual lock-in. Keep Stage 3 unchanged.

---

---

## See Also

- [[technology/lead-enrichment/cost-comparison|Cost Comparison]] — Full pricing and data return comparison across all 5 services
- [[technology/lead-enrichment/functional-architecture|Functional Architecture]] — Stage 2 in full pipeline context
- [[technology/lead-enrichment/apollo-person-match/_index|Apollo Person Match]] — Apollo skill documentation
- [[technology/lead-enrichment/linkfinder/_index|LinkFinder]] — Name-based tool (not eligible for Stage 2; documented separately)
