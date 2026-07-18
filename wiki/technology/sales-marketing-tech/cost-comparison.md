# Stage 2 Cost Comparison: Reverse Email Lookup Services

tags: [technical, lead-enrichment, cost-analysis, stage-2, reverse-email-lookup]

> *Per-lookup cost analysis for the 5 reverse email lookup services evaluated for Stage 2 of the pipeline. All use email address as input and return a LinkedIn URL on a successful match.*

**Note:** LinkFinder AI has been excluded — it is name-based, not email-based, and does not qualify as a reverse email lookup service for this pipeline.

---

## Service Comparison Table

| Service | Free Tier | Paid Plans (monthly) | Cost per Successful Lookup | What You Get on a Hit | Typical Use Case |
|---|---|---|---|---|---|
| **Prospeo** | 75 verified emails/mo | From ~$0.01/email (no annual contract) | ~$0.01 | Full B2B profile: name, title, company, LinkedIn URL, direct mobile, technographics, intent signals — 98% email accuracy | Richest data per lookup; best when you need more than just the URL |
| **SalesQL** | 50 credits/mo | Basic $39/mo (2,000 cr); Pro $119/mo (6,000 cr); Ultimate $179/mo (12,000 cr) | ~$0.02 ($39 ÷ 2,000) | Name, title, company, LinkedIn URL; phone on paid plans | Simple credit-based; generous free tier; good for moderate volumes |
| **Apollo.io People Match** | None (API requires paid plan) | Basic $49/seat/mo; Pro $79/seat/mo (annual) | ~$0.002 (annual); ~$0.024 (monthly) | LinkedIn URL + title + company + phone + email — 60–70% email→URL match rate | Best if already using Apollo for Stage 1; consolidates stack |
| **ProxyCurl Reverse Email** | None | Pay-per-use only | ~$0.003–$0.01 | LinkedIn URL + basic profile data — ~70% accuracy (estimated) | Low volume or testing; no monthly commitment |
| **Lix** | 50 email credits + 1,000 rows + 10 API credits | Leads $39/mo (300–1,000 cr); Data Plus $109/mo (500–10,000 cr) | ~$0.04–$0.13 | LinkedIn URL, name, company details — basic identity enrichment; credit rollover | API-driven at lower volume; prefer credit rollover |

---

## Cost at Volume

| Service | 100 lookups/mo | 500 lookups/mo | 1,000 lookups/mo | 5,000 lookups/mo |
|---|---|---|---|---|
| **Prospeo** | ~$1.00 | ~$5.00 | ~$10.00 | ~$50.00 |
| **SalesQL Basic** | $1.95 (plan: $39) | $9.75 (plan: $39) | $19.50 (plan: $39) | $97.50 (plan: $119) |
| **Apollo (annual)** | $0.20 (plan: $49) | $0.98 (plan: $49) | $1.96 (plan: $49) | $9.80 (plan: $49) |
| **Apollo (monthly)** | $2.40 (plan: $59) | $11.88 (plan: $59) | $23.75 (plan: $59) | $118.75 (plan: $59+) |
| **ProxyCurl** | $0.30–$1.00 | $1.50–$5.00 | $3.00–$10.00 | $15.00–$50.00 |
| **Lix Leads** | $4.00–$13.00 (plan: $39) | $20.00–$65.00 (plan: $39–$109) | $40.00–$130.00 (plan: $109) | $200–$650 (plan: $109+) |

---

## Data Return Comparison

| Service | LinkedIn URL | Name | Title | Company | Phone | Email | Intent/Technographic |
|---|---|---|---|---|---|---|---|
| **Prospeo** | ✅ | ✅ | ✅ | ✅ | ✅ (direct mobile) | ✅ (verified) | ✅ |
| **SalesQL** | ✅ | ✅ | ✅ | ✅ | ✅ (paid plans) | — | — |
| **Apollo** | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | — |
| **ProxyCurl** | ✅ | ✅ | — | — | — | — | — |
| **Lix** | ✅ | ✅ | — | ✅ | — | — | — |

---

## Key Insights

### Richest Data Return
**Prospeo** returns the most data per successful lookup — full B2B profile including technographics and intent signals, at ~$0.01/lookup. For this pipeline, richer Stage 2 data means Stage 3 (profile enrichment) and Stage 5 (email creation) have better raw material to work with.

### Best Value at Scale (Annual Commitment)
**Apollo (annual billing)** delivers the lowest per-credit cost (~$0.002) if you're already using Apollo for Stage 1. However, the 60–70% email→URL match rate is lower than Prospeo's 98% email accuracy claim.

### Best for Testing / Low Volume
**ProxyCurl** — no monthly commitment, pay-per-use. Useful for testing the pipeline before committing to a paid plan.

### Credit Rollover
**Lix** offers credit rollover, which is valuable if volume is uneven month-to-month. However, it has the highest per-lookup cost and the thinnest data return.

### Accuracy vs. Cost Trade-off
- Prospeo: 98% email accuracy at $0.01/lookup = $0.0102 per successful match
- Apollo: 60–70% match rate at $0.002/lookup = ~$0.003–$0.0033 per successful match (annual)
- Even with Apollo's lower match rate, its annual per-credit cost still wins on pure cost-per-match — but Prospeo returns significantly richer data on each hit

---

## Recommendation

**Starting point:** Use **Apollo** if already on a paid plan (consolidates Stages 1+2). If Apollo match rate proves insufficient (<60% on actual leads), switch Stage 2 to **Prospeo** for higher accuracy and richer data return at a small cost increase.

**Pure Stage 2 standalone:** **Prospeo** — best accuracy + richest data + no annual commitment.

---

## See Also

- [[technology/lead-enrichment/functional-architecture|Functional Architecture — Stage 2 detail]]
- [[technology/lead-enrichment/decision-framework|Decision Framework — which tool to choose]]
- [[technology/lead-enrichment/apollo-person-match/_index|Apollo Person Match skill]]
