---
type: reference
updated: 2026-06-30
---

# Project Priorities

The WSJF-ranked queue of all Projects, with flow status. This is
the single source of truth for Project sequencing and the basis for Jira
Portfolio Kanban sync.

**Jira sync direction:** the wiki is authoritative for ranking, scope, and
sizing - changes here (via `/project-planner`) push to Jira via `/jira-sync`.
Reordering or moving cards on the Portfolio Kanban board is reconciled back
via `/jira-pull`, which updates the Flow column below. Run `/jira-pull` first
if cards may have moved on the board since the last pull.

| Project | Workstream | Objective | WSJF | T-shirt | Flow |
|---------|-----------|-----------|------|---------|------|
| [[uk-relocation-decision\|UK Relocation Decision]] | Personal | Have a committed decision on whether to stay in HK or relocate to the UK, locked before the 12 July trip | 6.0 | S | implementing |
| [[tti-role\|TTI Role]] | Career | Secure a full-time role at TTI that funds my current Hong Kong lifestyle | 6.0 | S | implementing |
| [[genai-sa-market-validation\|GenAI SA: Go/No-Go Validation]] | Career | Reach a recruiter-validated go/no-go decision on whether a GenAI SA pivot will materially improve employability | 4.5 | XS | ready |
| [[clsa-second-interview\|CLSA — Second Interview (Deputy CIO)]] | Career | Interview prep for the operationally-focused Deputy CIO: scope doc, AIOps/NetAI research, curated stories, flashcards. **Deadline-driven (interview possibly this week) - scheduled now despite WSJF position.** | 3.8 | M | ready |
| [[automated-linkedin-networking\|Automated LinkedIn Networking]] | Career | Build and warm a LinkedIn pipeline of relevant industry contacts ahead of the brand/KPI foundation | 2.2 | M | ready |
| [[cold-outreach-real-estate\|Cold Outreach — Real Estate]] | Career | Prove I can generate qualified leads at <HK$1,000/lead to unlock a partnership income stream | — | XL | implementing |
| [[job-search-pipeline\|Job Search Pipeline]] | Career | Standing top-of-funnel pipeline — trawling, screening, and cold applications; active opportunities spin out as separate projects | — | S | implementing |
| [[agile-claw-mvp\|Agile Claw MVP]] | Performance | Validate that HK enterprises will pay a commercially viable rate for AI OS consulting | — | L | funnel |
| [[clsa-role\|CLSA — First Interview (Head of Network Services)]] | Career | First-interview stage: rec, resume tailoring, first-interview prep — delivered and earned a second interview | 7.0 | S | done |
