# API Skill Troubleshooting — Isolation Testing & Environment Gotchas

tags: [technical, api, troubleshooting, skills, testing]

> *Reference for debugging API-based Claude skills. Captures environment-specific failure modes discovered during the LinkedIn enrichment skill build (April 2026) that Claude would not know without this context.*

---

## Key Takeaways

- **Always check billing before debugging code.** Zero API credits produce errors that look like code bugs.
- **Test each external API independently with curl before running any script.**
- **Julian's environment has known VPN routing quirks** — understand which APIs route through VPN and which bypass it before testing.
- **Not all third-party APIs index all data** — test with known-good data before testing your actual targets.
- **Error messages from orchestration scripts are often misleading** — they report a pipeline failure, not which component failed.

---

## Julian's Environment — Known Gotchas

These are environment-specific facts that affect testing of any API-based skill:

### VPN (ExpressVPN — Hong Kong)
- **Anthropic API (160.79.104.0/21) is blocked in Hong Kong** without VPN — Claude Code and all Anthropic API calls require VPN.
- **RapidAPI blocks VPN exit node IPs** — shared VPN exit IPs are flagged as proxy/bot traffic. RapidAPI calls must bypass the VPN.
- **Configuration:** Reverse IP bypass rule — all traffic routes through VPN *except* anything not in the 160.79.104.0/21 range. This means only Anthropic traffic goes through the tunnel; everything else exits direct.
- **Consequence:** When testing a new skill, be aware that different external APIs will behave differently depending on whether they're VPN-routed or not.

### Known Routing by API
| API | Route | Reason |
|-----|-------|---------|
| Anthropic API | Through VPN | HK network block |
| RapidAPI | Direct (bypass VPN) | VPN IPs blocked by RapidAPI |
| Google Sheets | Direct (bypass VPN) | Google tolerates HK direct |
| Apollo API | Direct (bypass VPN) | Assumed — verify on first use |

### Credentials
- All API keys stored in `~/.leadgen/credentials.json` (chmod 600)
- Loaded at script start by `credentials.py` CredentialManager
- Keys: `RAPIDAPI_KEY`, `ANTHROPIC_API_KEY`, `APOLLO_API_KEY`, `GOOGLE_SERVICE_ACCOUNT_JSON`, `SHEETS_AUTH_METHOD`

---

## Pre-Flight Checklist — Run Before Any Debugging

When a skill fails or before first testing a new skill:

| Step | Check | Why |
|------|-------|-----|
| 1 | `~/.leadgen/credentials.json` has all required keys | Missing keys cause silent failures |
| 2 | Check billing/quota on **every** paid API in the pipeline | Zero credits look like code bugs |
| 3 | curl test each external API independently | Confirms auth and connectivity before running any code |
| 4 | Test with known-good data (not actual targets) | Data coverage gaps can mimic API failures |
| 5 | Confirm VPN routing for each API | Wrong routing causes 400/403 errors |
| 6 | Run full pipeline end-to-end | Integration failures only visible end-to-end |

---

## Isolation Testing — Layer by Layer

Test from the bottom up. Resolve each layer before moving to the next.

```
Layer 1: Credentials     → does ~/.leadgen/credentials.json have the key?
Layer 2: Billing/Quota   → is the API account funded and within quota?
Layer 3: Network/VPN     → is the API reachable from this machine?
Layer 4: Authentication  → does the API key authenticate successfully?
Layer 5: Data            → does the target data exist and is it accessible?
Layer 6: Code            → does the Python script call the API correctly?
Layer 7: Integration     → does the full pipeline run end-to-end?
```

Most debugging sessions fail because they start at Layer 6 and work backwards. Start at Layer 1.

### How to Test Each Layer

**Layer 1 — Credentials:**  
Check the JSON file exists and contains the required key. Do this before anything else.

**Layer 2 — Billing/Quota:**  
Log in to each API provider dashboard and verify: active subscription, credits remaining, monthly quota not exceeded. For RapidAPI, check the specific endpoint's plan limits. For Anthropic, check the billing page directly.

**Layer 3 — Network:**  
Try the API from a browser or with the VPN toggled. If it works with VPN off but not on (or vice versa), the issue is routing, not credentials.

**Layer 4 — Authentication:**  
Use curl to call the API with the key explicitly. A 401 means bad key; 403 can mean bad key, IP block, or plan restriction.

**Layer 5 — Data:**  
Test with a known-good data point (a well-known public profile, a test record) before using your actual targets. Fresh LinkedIn Scraper, for example, only indexes profiles it has previously crawled — not every LinkedIn profile is accessible.

**Layer 6 — Code:**  
Run the Python script against the known-good data from Layer 5. If Layer 5 passed but Layer 6 fails, the bug is in the code.

**Layer 7 — Integration:**  
Run the full pipeline end-to-end with a small batch. Confirm data flows correctly from source (Sheets) through enrichment to destination.

---

## Common Error Patterns

| Error | Likely Layer | First thing to check |
|-------|-------------|----------------------|
| 502 CORS / Network Failure | Network (Layer 3) | VPN on or off? |
| 400 Bad Request | Auth or Data (Layer 4/5) | Is the API key valid? Is the data in the provider's index? |
| 401 Unauthorized | Auth (Layer 4) | Check the API key in credentials.json |
| 403 Forbidden | Auth or Network (Layer 3/4) | VPN IP blocked? Plan doesn't cover this endpoint? |
| 429 Too Many Requests | Quota (Layer 2) | Monthly or per-minute limit hit |
| "credit balance too low" | Billing (Layer 2) | Add credits to the API account |
| Script says "failed" with no detail | Integration (Layer 7) | Run isolation tests — script error masks which component failed |

---

## Lessons Learned — LinkedIn Enrichment Skill (April 2026)

- Spent significant time testing wrong LinkedIn profile IDs (400 errors) when the actual blocker was zero Anthropic billing credits — a Layer 2 issue that should have been caught in the pre-flight check.
- VPN routing needed to be solved before any API testing was meaningful — a Layer 3 issue that blocked everything downstream.
- Fresh LinkedIn Scraper does not index all LinkedIn profiles — test with a generic known-good profile (`jack`) to confirm the API works before testing real targets.
- "Profile enrichment failed" in the script output masked the true cause — only a direct curl test against the Anthropic API revealed the billing error.

See also: [[technology/claude-anthropic/_index|Claude & Anthropic]] for Claude Code skill architecture.
