---
project: cold-outreach-real-estate
workstream: career
size: 2
hours: 5–8h
created: 2026-05-18
status: queued
jira-key:
---

# Lead Creation

## Story
> *As a business developer, I want a clean, enriched contact list aligned to the agreed target segment so that I can run personalised outreach via the Email Campaign.*

## Acceptance Criteria
1. Contact list contains a minimum of 2,000 contacts matching the target segment defined by the B2C Risk & Strategy Assessment
2. Every contact has: full name, company, verified email address, LinkedIn URL, and at least one personalisation field (role, company vertical, or recent activity)
3. List is de-duplicated — no contact appears more than once
4. List is imported into Saleshandy and passes validation (bounce rate < 5% on a test send of 50 contacts)
5. Output is stored in the agreed Google Sheet format, ready for the email generation skill

## Definition of Done
A contact list of 2,000+ verified prospects aligned to the strategy defined by the B2C Risk & Strategy Assessment exists in the agreed Google Sheet, enriched with LinkedIn data and at least one personalisation field per contact. The list is de-duplicated, imported into Saleshandy, and has passed deliverability validation. It is ready to hand off to the Email Campaign story with no further data preparation needed.

## Notes
- Blocked by: B2C Risk & Strategy Assessment (segment definition must exist before sourcing begins)
- Saleshandy Starter plan caps at 2,000 active prospects simultaneously; a 3-email sequence to 2,000 = 6,000 sends = exactly the monthly cap — see [[../../technology/sales-marketing-tech/vendors/saleshandy/pricing|Saleshandy Pricing]]
- Enrichment pipeline: Apollo Person Match (Step 1) + LinkedIn Enrichment skill (Step 2) — both operational

## Links
- **Epic:** [[../epics/cold-outreach-real-estate|Cold Outreach — Prove the Real Estate Lead Gen Model]]
- **Workstream:** [[../career/_index|Career]]
- **Blocks:** [[outreach-email-campaign|Email Campaign]]
- **Blocked by:** [[outreach-b2c-risk-assessment|B2C Risk & Strategy Assessment]]
