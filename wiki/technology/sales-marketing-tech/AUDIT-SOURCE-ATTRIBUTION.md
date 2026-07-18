---
name: Source Attribution Audit — Cold Email Outreach Vendors
description: Comprehensive audit of website source attribution across all 40 vendor files (20 pricing.md + 20 capabilities.md)
category: cold-email-outreach
audit-date: 2026-05-04
---

# Source Attribution Audit — Cold Email Vendors

**Policy:** All pricing.md and capabilities.md files must clearly indicate "source: [URL] (live fetch)" or equivalent to show information was extracted directly from vendor websites.

**Status:** 20 files have website source ✅ | 10 files are estimated ⚠️ | 1 file is sourced from raw input ⚠️ | 20 files lack source attribution ⚠️

---

## Summary by Status

### PRICING.MD — Website Source Status (20 files)

#### ✅ LIVE FETCH — Ready (7 vendors)
Information extracted directly from vendor website. No action needed.

| Vendor | Last Verified | Source URL |
|--------|---------------|-----------|
| Apollo | 2026-05-04 | https://www.apollo.io/pricing + knowledge base |
| Instantly | 2026-05-03 | https://instantly.ai/pricing |
| Lemlist | 2026-05-03 | https://www.lemlist.com/pricing |
| Make | 2026-05-03 | https://www.make.com/en/pricing |
| Prospeo | 2026-05-04 | https://prospeo.io/pricing |
| Saleshandy | 2026-05-03 | https://www.saleshandy.com/pricing/ |
| SalesQL | 2026-05-03 | https://salesql.com/pricing |

#### ⚠️ ESTIMATED — Needs Website Source (10 vendors)
Marked as "estimated from training data" with verification URLs. User must fetch from website and replace.

| Vendor | Last Verified | Current Status | Verification URL |
|--------|---------------|----------------|------------------|
| Claude Code | (undated) | Estimated | https://www.anthropic.com/pricing |
| Clay | (undated) | Estimated | https://www.clay.com/pricing |
| Gumloop | (undated) | Estimated | https://www.gumloop.com/pricing |
| Hermes Agent | (undated) | Estimated | https://hermes-agent.nousresearch.com |
| HubSpot | (undated) | Estimated | https://www.hubspot.com/pricing/sales |
| Lix | (undated) | Estimated | https://lix.it/pricing |
| MillionVerifier | (undated) | Estimated | https://www.millionverifier.com/pricing |
| n8n | (undated) | Estimated | https://n8n.io/pricing/ |
| OpenClaw | (undated) | Estimated | https://openclaw.ai |
| ProxyCurl | (undated) | Estimated | https://nubela.co/proxycurl/pricing |

#### ⚠️ PARTIAL — Needs Clarification (2 vendors)

| Vendor | Last Verified | Current Status | Issue |
|--------|---------------|----------------|-------|
| Fresh LinkedIn Scraper | 2026-05-03 | RapidAPI link | Source is RapidAPI URL (third-party), not primary vendor source |
| Snov.io | 2026-05-03 | `source: raw/SNOV pricing.md` | ⚠️ **CRITICAL GAP**: Sourced from raw file, NOT from snov.io website |

---

### CAPABILITIES.MD — Source Attribution Status (20 files)

#### ⚠️ ALL 20 FILES LACK SOURCE ATTRIBUTION
None of the capabilities.md files have a "source:" line in frontmatter indicating they were extracted from vendor websites.

| Vendor | Has Source Line | Action Required |
|--------|-----------------|-----------------|
| Apollo | ✗ | Add source: [website] |
| Claude Code | ✗ | Add source: [website] |
| Clay | ✗ | Add source: [website] |
| Fresh LinkedIn Scraper | ✗ | Add source: [website] |
| Gumloop | ✗ | Add source: [website] |
| Hermes Agent | ✗ | Add source: [website] |
| HubSpot | ✗ | Add source: [website] |
| Instantly | ✗ | Add source: [website] |
| Lemlist | ✗ | Add source: [website] |
| Lix | ✗ | Add source: [website] |
| Make | ✗ | Add source: [website] |
| MillionVerifier | ✗ | Add source: [website] |
| n8n | ✗ | Add source: [website] |
| OpenAI Codex | ✗ | Add source: [website] |
| OpenClaw | ✗ | Add source: [website] |
| Prospeo | ✗ | Add source: [website] |
| ProxyCurl | ✗ | Add source: [website] |
| Saleshandy | ✗ | Add source: [website] |
| SalesQL | ✗ | Add source: [website] |
| Snov.io | ✗ | Add source: [website] |

---

## Priority Gaps — What User Needs to Provide

### HIGHEST PRIORITY — Critical Data Integrity Issues

**Snov.io — pricing.md ⚠️ CRITICAL**
- Current: `source: raw/SNOV pricing.md`
- Status: Data sourced from raw file, NOT directly from website
- Action: User must fetch pricing from https://snov.io/pricing and replace entire pricing.md with website-sourced data
- Impact: Currently data cannot be verified as accurate from vendor website

### HIGH PRIORITY — All 20 Capabilities Files

**All vendors — capabilities.md (add source attribution)**
- Status: None of the 20 capabilities.md files indicate they were sourced from vendor websites
- Action: When adding/updating capabilities.md for any vendor, include `source:` line in frontmatter
- Format: `source: [vendor website URL] (last accessed [date])` or similar

### MEDIUM PRIORITY — 10 Vendors with Estimated Pricing

These are currently flagged as "estimated from training data" and need replacement with live website data:

1. Claude Code (https://www.anthropic.com/pricing)
2. Clay (https://www.clay.com/pricing)
3. Gumloop (https://www.gumloop.com/pricing)
4. Hermes Agent (https://hermes-agent.nousresearch.com)
5. HubSpot (https://www.hubspot.com/pricing/sales)
6. Lix (https://lix.it/pricing)
7. MillionVerifier (https://www.millionverifier.com/pricing)
8. n8n (https://n8n.io/pricing/)
9. OpenClaw (https://openclaw.ai)
10. ProxyCurl (https://nubela.co/proxycurl/pricing)

### MEDIUM PRIORITY — Fresh LinkedIn Scraper

- Current: `source: https://rapidapi.com/...` (third-party marketplace)
- Issue: Should verify primary vendor source alongside RapidAPI listing
- Action: Check if Fresh LinkedIn Scraper has official docs/pricing page; add as alternate source

---

## Recommended Workflow

1. **User fetches vendor pricing/capabilities** using AI web browser from vendor website
2. **User provides website-sourced information** by pasting into chat
3. **Assistant updates wiki file** with:
   - Replaced data (pricing table, capabilities list)
   - Source attribution line: `source: [URL] (live fetch on [date])` or `source: [URL] (last accessed [date])`
   - Updated `last-verified:` date in frontmatter
4. **Log entry created** in wiki/log-2026-Q2.md documenting the update

---

## File Format Reference

### Pricing.md Frontmatter (with source)
```markdown
---
vendor: [Vendor Name]
last-verified: 2026-05-04
source: https://[vendor].com/pricing (live fetch)
---
```

### Capabilities.md Frontmatter (with source)
```markdown
---
name: [Vendor Name] Capabilities
description: [brief description]
category: cold-email-outreach
source: https://[vendor].com/features (last accessed 2026-05-04)
---
```

---

## Next Steps

1. **Immediate:** User provides website-sourced pricing for **Snov.io** (critical gap)
2. **Next:** User provides website-sourced capabilities for **all 20 vendors** (can be batched)
3. **Ongoing:** Establish cadence for refreshing pricing/capabilities (suggest 60-day cycle per vendor)
