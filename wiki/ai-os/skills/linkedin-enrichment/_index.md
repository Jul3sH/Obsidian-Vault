# LinkedIn Enrichment Skill

tags: [technical, skills, linkedin, api, enrichment]

> *Step 2 of the lead enrichment pipeline. Reads `linkedin_url` populated by the apollo-person-match skill, extracts the username internally, fetches LinkedIn profile and posts via RapidAPI, summarises with Claude Haiku, writes results back to Google Sheets.*

---

## Overview

This skill takes contacts that already have a `linkedin_url` (from the apollo-person-match skill) and enriches them with AI-generated summaries of their LinkedIn profile and recent posts — ready for cold email personalisation. Username extraction from the URL is handled internally by the script — no separate conversion step or column needed.

**Pipeline position:**
```
Google Sheets → apollo-person-match → linkedin-enrichment (this skill)
(name + email)   (linkedin_url)        (profile + posts summaries)
```

---

## Articles in This Section

- [[technology/linkedin-enrichment/architecture|Architecture]] — Pipeline flow, component responsibilities, data flow diagram
- [[technology/linkedin-enrichment/TESTING|TESTING]] — Testing log, isolation tests run, blockers found, pre-flight checklist
- [[technology/linkedin-enrichment/scripts/run_enrichment|run_enrichment.py]] — Orchestration script: reads sheet, dispatches enrichment, writes results
- [[technology/linkedin-enrichment/scripts/linkedin_enricher|linkedin_enricher.py]] — LinkedIn API calls + LLM summarisation
- [[technology/linkedin-enrichment/scripts/gsheets_store|gsheets_store.py]] — Google Sheets read/write layer
- [[technology/linkedin-enrichment/scripts/credentials|credentials.py]] — Shared credential manager (used by all pipeline skills)

---

## Quick Reference

**Run command:**
```bash
python scripts/run_enrichment.py \
  --sheet-id "YOUR_SHEET_ID" \
  --worksheet "Sheet1" \
  --batch-size 2 \
  --provider anthropic \
  --mode both
```

**Credentials required:** `RAPIDAPI_KEY`, `ANTHROPIC_API_KEY`, `GOOGLE_SERVICE_ACCOUNT_JSON`  
**Cost per lead:** 4 RapidAPI credits + ~$0.001 Anthropic Haiku  
**LLM model:** `claude-haiku-4-5-20251001` (hardcoded)

---

## See Also

- [[technology/skill-conventions|Skill Conventions]] — Standard structure for all API-based skills
- [[technology/api-skill-troubleshooting|API Skill Troubleshooting]] — Isolation testing methodology and environment gotchas
