---
vendor: Claude Code (Anthropic)
last-verified: 2026-05-03
type: AI coding assistant / agentic tool
---

# Claude Code — Capability Profile

## Use Case Coverage

| Use Case | Rating | Notes |
|----------|--------|-------|
| [[prospecting]] | — | Not a data source; can write scripts to call prospecting APIs |
| [[email-verification]] | — | Not applicable directly |
| [[email-warmup]] | — | Not applicable |
| [[personalisation]] | ✓ | Via MCP: reads prospect data, pulls LinkedIn signals, funding events, hiring data; generates unique first lines per prospect; compresses 4–5 hours of research into 15–30 min; connects to outreach platform via MCP for campaign creation |
| [[campaign-sequence]] | — | Can build campaign logic programmatically; not a sending platform |
| [[inbox-reply-management]] | △ | Gmail MCP reads inbox; classifies emails; drafts replies; requires user-defined rules |

## Vendor Type
AI coding and automation tool. Used to build and orchestrate outreach workflows, not as a sending platform itself.

## Best For
Power users who want AI-generated personalisation at scale by connecting to live prospect signals (LinkedIn, funding, hiring) via MCP tools. Most cost-effective for high-volume icebreaker generation.

## Limitations
- Not a sending platform — must pair with Instantly, Lemlist etc.
- Requires technical setup (MCP configuration, skill files)
- Inbox management (Gmail MCP) is not plug-and-play
- Costs are API-based (Claude Sonnet/Haiku) — need to model usage
