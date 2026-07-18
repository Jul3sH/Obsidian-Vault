---
name: Prospecting
category: cold-email-outreach
---

# Prospecting

**Job to be done:** Find and build a list of verified contacts to reach out to.

## Inputs
- ICP criteria (job title, industry, company size, revenue, location, seniority)
- Company domain names
- LinkedIn profile URLs
- Names + company domains (for targeted lookup)

## Outputs
- Verified email addresses
- Contact profiles (name, title, company, LinkedIn URL)
- Company firmographics (size, industry, funding, tech stack)
- Phone numbers (where required)

## Key Capabilities to Evaluate
- **Database size** — how many contacts/companies indexed
- **Filter depth** — how granular the ICP filters are (65+ filters vs. 10)
- **Accuracy / verification rate** — what % of emails are deliverable
- **LinkedIn integration** — native extension or API-based
- **Intent / buying signals** — job changes, funding, tech stack changes
- **Bulk processing** — can it handle 10K+ rows in one batch
- **Multi-provider waterfall** — chain multiple data sources for higher hit rate
- **API access** — needed for automation pipelines
- **Credit model** — pay per result vs. subscription seats

## Vendors in This Category

**Primary**: Snov.io, Apollo, Clay, HubSpot, Prospeo, SalesQL, ProxyCurl, Lix

**Specialist (LinkedIn-native)**: LinkedIn Sales Navigator, ZoomInfo, Cognism

## Seniority & Location Filtering — Apollo vs. Alternatives

For finding senior employees (directors, VPs, C-Suite) in specific geographies (e.g., directors in Hong Kong):

### Apollo ✓ **Best for All-in-One**
- **65+ filters** including seniority level (Owner, Founder, C-Suite, VP, Director, Manager, Entry, Intern)
- **Job title search** with Boolean operators (AND, OR, NOT)
- **Location** filters (country, region, city)
- **Email addresses included** (verified)
- **Outreach automation** built-in
- **Cost**: $79/mo (Professional minimum for 3+ mailboxes)

### LinkedIn Sales Navigator △ **Best for LinkedIn-Native Data**
- **50+ advanced filters** on LinkedIn directly
- **Seniority level filter** (Director, VP, C-level, etc.)
- **Real-time data** from LinkedIn activity
- **Job change signals** ("Recently changed jobs")
- **No email addresses** — requires separate tool
- **No CRM or automation** — requires separate sequencer
- **Cost**: ~$99/mo

### SalesQL △ **Budget Alternative**
- LinkedIn Chrome extension
- Can bulk extract from LinkedIn search results
- Cheaper than Sales Navigator
- **Cost**: $39/mo

### Clay ✓ **Best for Multi-Source**
- Waterfall enrichment from 150+ providers
- Apollo integration built-in
- Can pull from LinkedIn Sales Navigator
- Custom workflows for complex filtering
- **Cost**: Usage-based (variable)

**Recommendation**: For "Managing Directors in Hong Kong" use case:
- **Best single tool**: Apollo Professional ($79/mo) — filters + emails + automation
- **Best LinkedIn accuracy**: LinkedIn Sales Navigator ($99/mo) + separate email tool
- **Budget option**: Apollo Basic ($49/mo) + Apollo reverse lookup (if it includes seniority, TBD)

## Key Takeaways
- Apollo and Clay offer the deepest ICP filter sets and intent signals
- Prospeo and Lix specialise in high-accuracy LinkedIn-sourced emails
- ProxyCurl offers the deepest LinkedIn profile scraping via API
- SalesQL is strong for reverse email → LinkedIn URL lookups
- Snov.io is the best all-in-one (prospecting + verification + outreach) at a single subscription
