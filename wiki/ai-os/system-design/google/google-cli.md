---
created: 2026-06-09
type: reference
---

# Google CLI — Gemini Setup & Architecture

## Context: Why Gemini CLI?

Google launched **Antigravity CLI** (`agy`) at Google I/O (May 2026) as a Go-based, multi-agent development architecture to replace Node-based tools. However, server-side geographic restrictions blocked individual account OAuth logins from Hong Kong. Because authentication happens remotely on Google's identity servers during the login handshake, local environment bypasses are completely ineffective for consumer accounts.

To bypass the web-based regional authentication gates, we pivoted to the open-source **Gemini CLI** (`gemini`). By authenticating strictly via a dedicated developer key instead of standard browser OAuth, we established an unblocked terminal agent operating directly within the local directory.

## Strategic Risks & Deprecation Timeline

This setup has a definitive shelf-life due to Google's aggressive consolidation of development tooling:

- **June 18, 2026 Sunset Gate:** Google has officially announced that on this date, Gemini CLI will stop serving requests for consumer Google AI Pro, Ultra, and individual free accounts.
- **API Key Loophole Deprecation:** While enterprise licenses and paid Google Cloud Platform (GCP) API keys are explicitly excluded from this sunset, Google is actively removing standard personal Google AI Studio key authentication from native terminal tools to push users into the Antigravity ecosystem.
- **Workflow Risk:** There is high probability that after June 18, the Gemini CLI binary will refuse to route individual-tier requests or accept consumer API keys entirely.

## Contingency Options (Post-June 18)

1. **Switch to an Enterprise Gateway** — Route the local agent through an explicit, billed Google Cloud Project (GCP) API credential rather than an individual consumer AI Studio key, which unlocks the enterprise onboarding route in Antigravity CLI (`agy`).

2. **Utilize Browser Agent Mode** — Shift workspace tasks to the built-in Gemini sidebar in your editor, setting it to Agent Mode and using the `@workspace` tag to manipulate local files over secure browser channels.

3. **Pivot to an Alternative Framework** — Utilize the exported Google API key inside third-party, open-source CLI orchestration tools (like `aider`) that are agnostic to Google's platform-specific application deprecations.
