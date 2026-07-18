---
updated: 2026-06-20
---

# Active Subscriptions — Sales, Marketing & Tech

> Source of truth for what is currently being paid for. Used by `/tco` to mark sunk costs as $0 incremental. Update whenever a subscription starts, cancels, or renews.

**Monthly total: $85**

---

## Active

| Vendor | Plan | Cost | Renews | Pipeline Stage | Notes |
|--------|------|------|--------|----------------|-------|
| RapidAPI Fresh LinkedIn Scraper | Pro | $49/mo | 28th of each month | Stage 3 - Profile Enrichment | Used by `linkedin-enrichment` skill |
| SalesHandy | Outreach Starter (monthly) | $36/mo | 5th of each month | Stage 6 - Email Sending | Started 2026-06-05. Includes 6,000 emails/mo, 2,000 active prospects (meaning TBC - investigate). Includes TrulyInbox SH Basic Plan free |
| TrulyInbox | SH Basic Plan | $0 (included with SalesHandy) | - | Stage 4 - Domain Warmup | Warm-up started 2026-05-12. Not a separate billing line |

---

## Cancelled / Lapsed

| Vendor | Was Used For | Reason Cancelled | Might Return? |
|--------|-------------|-----------------|---------------|
| SalesQL | Stage 2 - Reverse Email Lookup (email -> linkedin_url) | Not renewed - pipeline direction unclear; didn't want to pay while undecided on enrichment approach | Yes - if apollo-person-match skill proves insufficient |

---

## To Investigate

- SalesHandy "2,000 active prospects" limit - unclear what this caps and whether it constrains the pipeline

## See Also

- [[functional-architecture]] - full 7-stage pipeline with vendor options per stage
- [[vendors/saleshandy/capabilities]] - SalesHandy capabilities detail
- [[vendors/fresh-linkedin-scraper/pricing]] - RapidAPI scraper pricing tiers
- [[ai-os/skills/linkedin-enrichment/_index|linkedin-enrichment skill]] - uses the RapidAPI subscription
