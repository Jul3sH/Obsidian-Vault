# LinkedIn Enrichment Skill — Testing Log

**Skill:** linkedin-enrichment  
**Date:** April 2026  
**Outcome:** Working end-to-end after resolving 4 distinct blockers  

---

## Overview

This document records the isolation tests run during initial development and debugging of the LinkedIn enrichment skill. Each test is documented with **what** was tested and **why**, so that future debugging of this or similar skills can follow a more direct path.

The core lesson from this session: **we spent significant time debugging data problems (wrong LinkedIn IDs) when the actual blocker was a missing Anthropic API subscription.** Isolation testing identified this, but not early enough. A pre-flight checklist run at the start would have found it in minutes.

---

## The Pipeline Under Test

```
Google Sheets → run_enrichment.py → linkedin_enricher.py → RapidAPI
                                  ↘                      → Anthropic Haiku
                                    gsheets_store.py     → Google Sheets
```

Three external dependencies, each independently capable of failing:
1. **RapidAPI** (Fresh LinkedIn Scraper) — data source
2. **Anthropic API** (Claude Haiku) — summarisation
3. **Google Sheets API** — data store

---

## Tests Run — Chronological

### Test 1 · Web Dashboard Test Against RapidAPI
**What:** Called the RapidAPI endpoint from the RapidAPI web dashboard  
**Why:** To verify the API subscription and key were valid before writing any code  
**Result:** 502 CORS Error / Network Failure  
**Revealed:** Network-level blockage — not an API key problem  
**Next action:** Suspected VPN

---

### Test 2 · VPN Off Test
**What:** Disabled VPN entirely and retested the RapidAPI endpoint  
**Why:** To isolate whether the VPN was causing the connectivity failure  
**Result:** API worked immediately without VPN  
**Revealed:** ExpressVPN exit node IPs were being blocked by RapidAPI (shared IPs flagged as proxy traffic)  
**Next action:** Configure VPN split tunnelling so RapidAPI traffic bypasses the tunnel

---

### Test 3 · VPN Reverse Bypass Rule
**What:** Configured ExpressVPN with a reverse IP bypass rule — route all traffic through VPN *except* IPs outside 160.79.104.0/21 (Anthropic's range)  
**Why:** Needed VPN to reach Anthropic (blocked in Hong Kong) but not for RapidAPI. Standard split tunnelling only supports allow-lists by app, not IP — reverse logic was required.  
**Result:** RapidAPI traffic now exits direct; Anthropic traffic routes through VPN  
**Revealed:** The VPN routing was now correctly partitioned. Network layer resolved.  
**Next action:** Test actual API calls

---

### Test 4 · LinkedIn Profile Accessibility Testing
**What:** Tested multiple real LinkedIn profile IDs against the Fresh LinkedIn Scraper API  
**Why:** To verify that the API could fetch data for our target leads  
**Result:** 400 / 403 errors for all profiles tested (adam-g-hannam-0749885, julianhart-ict, pradeepvhegde)  
**Revealed:** These specific profiles were not indexed in Fresh LinkedIn Scraper's database. Not all LinkedIn profiles are accessible — the scraper only covers profiles it has previously crawled.  
**Time lost:** Significant. We spent too long here, trying different profile IDs, before accepting this was a data coverage issue rather than a code or auth problem.  
**Lesson:** Test with a known-good profile (e.g., a common public figure) to confirm the API works before testing your actual target data.

---

### Test 5 · Direct curl Test Against RapidAPI
**What:** Called the RapidAPI endpoints directly using curl with a known-good profile (`jack`)  
**Why:** To isolate whether the problem was the Python code or the API itself  
**Result:** Successful — full JSON profile response returned  
**Revealed:** RapidAPI was working correctly. The earlier 400 errors were data coverage issues (specific profiles not indexed), not code or auth failures.  
**Next action:** Run the Python script end-to-end

---

### Test 6 · End-to-End Script Run
**What:** Ran `run_enrichment.py` against the Google Sheet  
**Why:** To test the full pipeline with a valid profile  
**Result:** "Profile enrichment failed" errors in output  
**Revealed:** Something in the pipeline was still broken — but unclear which component  
**Next action:** Isolate the Anthropic API call specifically

---

### Test 7 · Direct curl Test Against Anthropic API
**What:** Called the Anthropic API directly using curl  
**Why:** To isolate whether the Anthropic LLM call was the failing component  
**Result:** Failed — error: *"Your credit balance is too low to access the Anthropic API"*  
**Revealed:** **This was the actual root cause.** No billing credits on the Anthropic account. The script had been silently failing at the LLM step all along.  
**Time lost:** This would have been found in minutes had we tested all three external APIs at the start.

---

### Test 8 · Full Pipeline After Adding Anthropic Credits
**What:** Added billing credits to the Anthropic account, re-ran `run_enrichment.py`  
**Why:** To confirm the credit issue was the only remaining blocker  
**Result:** Full pipeline succeeded — profile data fetched, summarised by Haiku, written back to Google Sheets  
**Revealed:** All components were working. The skill was operational.

---

## What Should Have Been Done First — Pre-Flight Checklist

Running these checks at the very start would have collapsed days of debugging into under 30 minutes:

| # | Check | What it catches |
|---|-------|-----------------|
| 1 | Verify credentials file exists and has all keys | Missing API keys |
| 2 | Check billing/quota on **every** paid API | Zero credits, exceeded quota |
| 3 | curl test each external API independently | Auth failures, network blocks |
| 4 | Test with known-good data (not your actual targets) | Data coverage gaps |
| 5 | Test network routing (VPN on vs. off) | VPN IP blocks |
| 6 | Run full pipeline end-to-end | Integration failures |

See `wiki/ai-os/service-design/api-skill-troubleshooting.md` for the generic isolation testing methodology that applies across all skills.

---

## Blockers Summary

| Blocker | Layer | Time Lost | How Found |
|---------|-------|-----------|-----------|
| VPN exit node IPs blocked by RapidAPI | Network | Medium | VPN off test |
| LinkedIn profiles not in scraper database | Data | High | Direct curl with known-good profile |
| RapidAPI monthly quota | Quota | Low | 429 error code |
| Anthropic API — zero billing credits | Billing | High | Direct curl against Anthropic API |

---

## Key Takeaways

- **Test billing before anything else.** A zero-credit API account produces errors that look like code bugs.
- **Test each external API with curl before running the full script.** Isolate each layer independently.
- **Use known-good test data first.** Don't test your actual targets until the API is confirmed working with a safe profile.
- **VPN affects different APIs differently.** RapidAPI blocked VPN exit IPs; Google Sheets did not; Anthropic required VPN (HK block). Understand the routing for each dependency before testing.
- **Error messages lie.** "Profile enrichment failed" did not tell us which component failed — only isolation revealed it was the LLM step.
