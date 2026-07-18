# Apollo Person Match

tags: [technical, apollo-person-match, skill]

> *Step 1 of the lead enrichment pipeline. Takes name + email from Google Sheets, calls Apollo `/people/match`, writes back LinkedIn URL, title, company, and phone numbers.*

---

## Articles

- [[technology/apollo-person-match/architecture|Architecture]] — Pipeline position, data flow, API details, VPN routing assessment, error handling, and comparison with LinkedIn enrichment
- [[technology/apollo-person-match/communication-diagram|Communication Diagram]] — Interactive HTML/SVG diagram showing credential loading, network flows, and both communication stages (Apollo direct, Sheets direct)
- [[technology/apollo-person-match/n8n-workflow-source|N8N Workflow Source]] — Original N8N workflow ("Lead 1") used as reference; includes key architectural observations and differences vs the Python skill

## Scripts
*(To be documented once scripts are built)*
- `apollo_person_match.py` — Main orchestrator
- `gsheets_store.py` — Google Sheets I/O (shared)
- `credentials.py` — Credential manager (shared)
