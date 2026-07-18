---
vendor: n8n
last-verified: 2026-05-03
source: estimated from training data — verify at https://n8n.io/pricing/
---

# n8n — Pricing

## Plans

| Plan | Monthly (billed monthly) | Monthly (billed annually) | Notes |
|------|--------------------------|---------------------------|-------|
| Self-hosted Community | $0 | $0 | Open-source, self-hosted, unlimited |
| Starter (cloud) | ~$24/mo | ~$20/mo | 2,500 workflow executions/mo |
| Pro (cloud) | ~$60/mo | ~$50/mo | 10,000 executions/mo |
| Enterprise (cloud) | Custom | Custom | Unlimited + SSO, audit logs |
| Enterprise (self-hosted) | Custom | Custom | License key required |

## Credit / Usage Model

- Cloud plans are metered by **workflow executions** per month; overage charged per additional execution block
- Self-hosted community edition: completely unlimited, no execution caps, no licence fee
- Enterprise self-hosted requires a paid licence for advanced features (SSO, version control, LDAP)

## TCO Notes

- Self-hosted is genuinely free and production-capable; primary cost is hosting (a small VPS ~$5–10/mo is sufficient for moderate workloads)
- Cloud plans are inexpensive but execution caps become a constraint at scale — model your automation frequency before choosing cloud vs. self-host
- For a cold email enrichment pipeline running nightly, self-hosted on a VPS is the lowest TCO option
- n8n's node library is extensive and covers most enrichment APIs (Apollo, Clay webhooks, Google Sheets, HTTP requests) without custom code
