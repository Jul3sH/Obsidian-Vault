---
project: cold-outreach-real-estate
workstream: career
size: 2
hours: 5–8h
created: 2026-05-06
status: queued
jira-key: BWS-4
---

# Build Personalised Email Generation Skill

## What this delivers
**Key Result:** KR3 — by end of month 2, the full pipeline is invokable using LLM skills (minimal manual steps).

## Definition of Done
A Claude skill exists for personalised email generation using enriched LinkedIn data. The skill runs end-to-end from a Google Sheet input (enriched contact list) and outputs personalised email copy ready for Saleshandy. LinkedIn enrichment skill is already operational — this is the final automation step in the pipeline.

## Note
LinkedIn enrichment skill is complete and operational. Scope reduced from original L (40h) — only personalised email generation remains. Dependency for Lead Creation story.

## Links
- **Epic:** [[../epics/cold-outreach-real-estate|Cold Outreach — Prove the Real Estate Lead Gen Model]]
- **Workstream:** [[../career/_index|Career]]
- **Related skills:** [[../ai-os/skills/linkedin-enrichment/_index|LinkedIn Enrichment]], [[../ai-os/skills/apollo-person-match/_index|Apollo Person Match]]
