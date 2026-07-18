---
vendor: Hermes Agent (Nous Research)
last-verified: 2026-05-03
source: estimated from training data — verify at https://hermes-agent.nousresearch.com
---

# Hermes Agent (Nous Research) — Pricing

## Plans

| Plan | Cost | Notes |
|------|------|-------|
| Self-hosted (open-source) | $0 | Apache 2.0 / open weights licence |
| Cloud API (if available) | Unknown | Verify at vendor site |

> Hermes is Nous Research's open-weight LLM series (Hermes 2, Hermes 3, etc.), fine-tuned for instruction following, tool use, and agentic tasks. As of training data cutoff, no managed cloud service was publicly available — the primary access mode is self-hosting.

## Credit / Usage Model

- Self-hosted: no credits, no metering — cost is compute only
- If accessed via third-party inference providers (e.g. Together AI, Fireworks, OpenRouter): metered per token at provider rates (~$0.20–$0.90 per million tokens depending on model size and provider)
- Verify whether Nous Research has launched a first-party API at https://hermes-agent.nousresearch.com

## TCO Notes

- Self-hosting requires GPU infrastructure; a 7B model runs on a single consumer GPU (RTX 3090/4090), 70B requires multi-GPU or cloud instance
- For low-to-medium volume agentic workflows, third-party inference APIs offer a managed middle ground without self-hosting overhead
- Hermes 3 (70B) is competitive with GPT-4o-mini for structured output and tool-use tasks — relevant for enrichment pipelines
- Zero licence cost makes it attractive for privacy-sensitive workflows where data should not leave your infrastructure
