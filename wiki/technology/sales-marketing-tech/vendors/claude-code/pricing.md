---
vendor: Claude (Anthropic API)
last-verified: 2026-05-03
source: estimated from training data — verify at https://www.anthropic.com/pricing
---

# Claude (Anthropic API) — Pricing

## Plans

| Model | Input (per 1M tokens) | Output (per 1M tokens) | Notes |
|-------|----------------------|------------------------|-------|
| Claude Haiku 3 | ~$0.25 | ~$1.25 | Fastest, cheapest; good for summarisation |
| Claude Haiku 3.5 | ~$0.80 | ~$4.00 | Improved reasoning over Haiku 3 |
| Claude Sonnet 3.5 | ~$3.00 | ~$15.00 | Balanced capability/cost |
| Claude Sonnet 3.7 | ~$3.00 | ~$15.00 | Extended thinking available |
| Claude Opus 4 | ~$15.00 | ~$75.00 | Highest capability |

> Prices are per million tokens. Prompt caching discounts apply (cache writes ~25% premium; cache hits ~90% discount on input tokens). Verify current model availability and pricing at https://www.anthropic.com/pricing.

## Credit / Usage Model

- Pure pay-as-you-go; no monthly minimum on the API
- Billed per token (input + output separately)
- Prompt caching: frequently reused context (system prompts, document chunks) cached automatically; cache hits billed at ~10% of normal input rate
- Batch API available for async workloads at ~50% discount vs. real-time API

## TCO Notes

- For a cold email enrichment pipeline (profile summarisation), Claude Haiku is the cost-optimal choice — a 500-token summary costs ~$0.000125 per contact
- At 10,000 contacts/mo with Haiku 3: estimated ~$1.25–$2.50/mo for AI summarisation — negligible vs. data sourcing costs
- VPN required to access Anthropic API from Hong Kong (160.79.104.0/21 range); configure reverse bypass so RapidAPI traffic bypasses VPN — see [[ai-os/skills/linkedin-enrichment/architecture|linkedin-enrichment architecture]]
- Prompt caching on shared system prompts across a batch can reduce effective input cost significantly for high-volume pipelines
