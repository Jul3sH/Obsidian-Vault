---
vendor: Apollo.io
last-verified: 2026-05-04
source: https://www.apollo.io/pricing + https://knowledge.apollo.io/hc/en-us/articles/9527776320781-What-Are-Credits (extracted directly from Apollo website, May 4 2026)
---

# Apollo.io — Pricing

## Billing Options
- **Annual billing**: 20% savings (prices below are annual)
- **Monthly billing**: available (no savings stated)
- **Trial**: 14-day free trial on paid plans
- All prices exclude taxes

## Plans

| Plan | Annual/seat/mo | Credits/seat/year | Mailboxes | Free Warmup |
|------|---------------|-------------------|-----------|------------|
| Free | $0 | 900 (granted monthly) | Limited | No (uses credits) |
| Basic | $49 | 30,000 (granted upfront) | 1 mailbox max | 1 free |
| Professional | $79 | 48,000 (granted upfront) | Unlimited Google/Microsoft + 5 SMTP | 1 free |
| Organization | $119 (min 3 seats) | 72,000 (granted upfront) | Unlimited Google/Microsoft + 15 SMTP | 1 free |

## Key Features by Plan

### Basic ($49/seat/mo annual)
- Deliverability Suite & Email Warmup ✓ (flat feature — not credit-based)
- Unlimited Sequences
- AI Research & AI Lead Scoring
- Advanced Filters
- CRM Integrations
- Waterfall Enrichment
- Domain & Mailbox Purchasing
- CSV, CRM & API Data Enrichment
- 6 Intent Topics & Intent Filters
- US Dialer
- 3 Meetings Events

### Professional ($79/seat/mo annual) — Most Popular
- Everything in Basic, plus:
- A/B / A/Z Testing
- Unlimited Gmail & Microsoft Mailboxes + 5 SMTP Mailboxes per user
- Automated Workflows
- Call Recordings & AI Insights (4,000 min)
- Analytics & Pre-built Reports
- 6 Meetings Events

### Organization ($119/seat/mo annual, min 3 seats)
- Everything in Professional, plus:
- 12 Intent Topics
- Custom Reports & Dashboards
- SSO
- 15 SMTP Mailboxes per user
- Call Recordings & AI Insights (8,000 min)

## Add-ons

| Add-on | Monthly (annual billing) | What it covers |
|--------|--------------------------|----------------|
| Inbound | $119/team | Up to 50K website visitors/mo, domain tracking, form enrichment |
| Advanced Dialer | $119/team | International, parallel, power dialer, local presence |

## Credit Usage

| Action | Credits consumed | Notes |
|--------|-----------------|-------|
| Email reveal | 1 credit | — |
| Phone number | 8 credits | — |
| Enrich data | 1–8 credits | Varies by data source; waterfall enrichment costs depend on which source succeeds first |
| AI research | 1 credit per run | — |
| US Dialer | 2 credits per minute | — |
| International Dialer | Varies by region | — |

> Note: Charged once per contact even if Apollo returns multiple numbers.

### Reverse Email Lookup (Email → LinkedIn URL) — Credit Cost

**Critical for TCO:** People Enrichment via email falls under "Enrich data" (1–8 credits). Apollo does NOT publicly specify the exact credit cost for reverse email lookups.

**From Apollo's knowledge base:**
- CSV enrichment, CRM enrichment, job change enrichment, and API enrichment all use credits
- Waterfall enrichment credit use varies by data source and which source succeeds first
- Re-enriching emails/phones costs credits; re-enriching firmographic data does not

**From real-world reports:**
- Email-only enrichment (name + email + company + title): consistently cited at **1 credit per contact**
- Full enrichment (email + phone + firmographics): cited at **5–10 credits per contact**
- Email + basic profile (no phone): estimated at **1 credit per contact**

**For your use case (1,000 contacts/month, email → LinkedIn URL + basic profile):**
- If 1 credit per contact → 1,000 credits/month (40% of Basic 2,500/mo quota) ✓ Feasible
- If 8+ credits per contact → 8,000+ credits/month (exceeds Basic quota) ✗ Infeasible

> ⚠️ Validation required: Contact Apollo support to confirm the exact credit cost of People Enrichment API calls for email-to-LinkedIn enrichment.

### Email Warm-up on Additional Mailboxes — Credit Cost

**From Apollo's knowledge base:**
- Email warmup is free for 1 mailbox on paid plans
- Each additional mailbox requires monthly credits to run warmup
- The exact monthly credit draw per mailbox is NOT specified in Apollo's public docs

**For your use case (3 mailboxes, 2 additional beyond the free one):**
- 1st mailbox warm-up: free ✓
- 2nd & 3rd mailbox warm-up: draws from monthly credit pool, exact amount TBD
- Estimated impact on 2,500/mo quota: low (not quantified in Apollo docs)

> ⚠️ Validation required: Contact Apollo support to confirm the monthly credit cost per additional mailbox for email warmup.

## TCO Notes

### ✓ Correction: Email Warm-up IS included in Apollo

Apollo offers SMTP-based email warmup with managed inbox network (automatic ramping and reply simulation). One mailbox warmup is **free for paid users** (Basic and above). Additional mailboxes beyond the first free one require additional cost (not specified in public docs).

**For 3 domains, plan requirements:**
- **Basic** ($49/mo): 1 mailbox max ✗ **Insufficient** (can only warm up 1 domain)
- **Professional** ($79/mo): unlimited Google/Microsoft + 5 SMTP ✓ **Sufficient** (can warm up 3+ domains)
- 1st mailbox: free warmup ✓
- 2nd & 3rd mailbox: cost TBD (contact Apollo support)

Apollo Professional ($79/mo) is required for 3-domain warm-up. The all-in-one feasibility depends on People Enrichment API credit costs and additional mailbox warmup costs.

### ⚠️ Credit Allocation Conflict — Verify Before Committing

Two conflicting figures found from Apollo's own sources:

| Source | Credits on Basic |
|--------|-----------------|
| Pricing page (May 2026) | 30,000 credits/year (2,500/mo) |
| Knowledge base article (How Do Data Requests Work) | 3,000 export credits/year (~250/mo) |

These may refer to different credit pools (total credits vs. export-specific credits), or one figure may be outdated. **Contact Apollo support to confirm before committing to Basic for 1,000 lookups/month.**

### Reverse Email Lookup Feasibility at 1,000 contacts/month

| Scenario | Credits needed | If 2,500/mo total | If 250/mo export |
|----------|--------------|-------------------|-----------------|
| 1 credit/lookup | 1,000 | ✓ Feasible (40% quota) | ✗ Exceeds quota 4× |
| 3 credits/lookup | 3,000 | ✓ Borderline | ✗ Exceeds quota 12× |
| 8 credits/lookup | 8,000 | ✗ Exceeds quota | ✗ Exceeds quota 32× |

**Critical uncertainties:** 
- If export credits are capped at 250/month, Apollo Basic cannot support 1,000 reverse lookups/month at any credit rate.
- If total credits (2,500/mo) include export credits and can be used for People Enrichment API calls, then 1 credit/lookup is feasible.

### Revised TCO for 1,000 lookups + 3-domain warm-up

**Plan Required: Professional ($79/mo/user) — NOT Basic**
- Reason: Basic only allows 1 mailbox (insufficient for 3 domains)
- Professional allows unlimited Google/Microsoft mailboxes + 5 SMTP (sufficient for 3 domains)

| Item | Cost | Status |
|------|------|--------|
| Reverse email lookups (1,000) | Included in credits | ❓ TBD if 1 credit/lookup |
| 1st mailbox warm-up | Free | ✓ Confirmed |
| 2nd & 3rd mailbox warm-up | Credits from 48,000/year pool | ❓ TBD (exact monthly draw) |
| **Total at Professional ($79/mo)** | $79 + TBD warmup credits | ❓ Pending Apollo clarification |

**To finalize:** Contact Apollo support and ask:
1. Do the 48,000 credits/year on Professional plan include People Enrichment API usage, or are export credits (3,000/year) a separate pool?
2. What is the credit cost for a People Enrichment API call returning email → LinkedIn URL + basic profile?
3. How many credits are consumed monthly for warming up 2 additional mailboxes (beyond the first free mailbox)?

### General Notes
- Per-seat pricing — cost scales linearly with team size
- Phone reveals cost 8 credits each — avoid unless phone numbers are required
- HubSpot/Salesforce integration: Professional and above only
- Email warm-up is relatively new (2024-2025); dedicated tools like Instantly may still be more reliable for high-volume
