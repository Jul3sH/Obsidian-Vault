---
vendor: OpenClaw
last-verified: 2026-05-03
type: AI email agent (autonomous)
---

# OpenClaw — Capability Profile

## Use Case Coverage

| Use Case | Rating | Notes |
|----------|--------|-------|
| [[prospecting]] | — | Not a data source |
| [[email-verification]] | — | Not applicable |
| [[email-warmup]] | — | Not applicable |
| [[personalisation]] | ✓ | Agent fills personalisation fields from persistent memory and MCP skills; multi-model routing (Claude, GPT-4, Gemini); spawns sub-agents per task |
| [[campaign-sequence]] | △ | Multi-step follow-up sequences executed autonomously as daemon; A/B testing via agent skills |
| [[inbox-reply-management]] | ✓ | EmailToolkit with TriageEngine (YAML rules); 80–90% of replies handled automatically; dry_run safety mode; human review queue with Slack/email/webhook; auto_reply toggle per category |

## Vendor Type
Autonomous AI email agent. Specialises in inbox triage and reply handling; can execute follow-up sequences as a background daemon.

## Best For
Teams wanting to automate inbox triage at high volume without manual reading. The TriageEngine's YAML-configured rules make it highly customisable for reply handling.

## Limitations
- Not a sending platform (no native campaign builder)
- Pricing and commercial details are limited publicly — newer product
- Setup requires configuring YAML triage rules and MCP skills
- Follow-up sequences are less structured than Instantly or Lemlist
