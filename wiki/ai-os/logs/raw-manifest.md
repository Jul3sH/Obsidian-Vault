---
type: manifest
created: 2026-06-05
purpose: Track compile status of all raw/ inbox files. Processed files move to raw/_processed/. Pending files stay in raw/ root until compiled.
---

# Raw Inbox Manifest

> Source of truth for what has and has not been compiled from `raw/`. Updated after every compile or batch move. Cross-reference with `log-2026-Q2.md` for detail.

## Convention
- **Processed** - compiled into wiki; file lives in `raw/_processed/`
- **Pending** - not yet compiled; file sits in `raw/` root
- **Duplicate** - redundant copy; moved to `raw/_processed/` with a note

---

## Processed (moved to raw/_processed/)

| File | Destination in wiki | Compile date |
|------|-------------------|--------------|
| Auntie Hil Whatsapp messages.md | relationships/Dad/ (dad-finance-discussions, dad-health-discussions) | 2026-06-01 |
| Codex 5.4 Stephan relationship analysis.md | career/tti/_reference/tti-stephan-relationship-analysis.md | 2026-05-27 |
| Gemini 3.5 flash Summary of Stephan Pudwill conversations.md | career/tti/_reference/tti-stephan-relationship-analysis.md | 2026-05-27 |
| Stephan Pudwill Whatsapp messages.md | career/tti/_reference/tti-stephan-relationship-analysis.md | 2026-05-27 |
| TTI Engagement Timeline.md | career/tti/_reference/engagement-history.md | 2026-05-27 |
| Dad inheritance timeline feb to august 2023.md | relationships/Dad/dad-finance-discussions.md | 2026-06-01 |
| Felix Hart Whatsapp messages.md | relationships/Dad/dad-finance-discussions.md + dad-health-discussions.md | 2026-06-01 |
| Felix Hart Will.md | relationships/Dad/ (wendy-profile, hilary-profile, relationship-dynamics) | 2026-06-01 |
| Felix Health whatsapp messages.md | relationships/Dad/dad-health-discussions.md | 2026-06-03 |
| Felix Health whatsapp messages.txt | DUPLICATE of .md — processed as part of same compile | 2026-06-03 |
| Felix Health whatsapp messages 1.txt | DUPLICATE of .md — processed as part of same compile | 2026-06-03 |
| Wendy Whatsapp messages.md | relationships/Dad/dad-finance-discussions.md + dad-health-discussions.md | 2026-06-01 |
| Wendy evidence of undue influnce.md | relationships/Dad/dad-finance-discussions.md | 2026-06-01 |
| Campaign & Sequence Management.md | technology/sales-marketing-tech/use-cases/campaign-sequence.md | 2026-05-03 |
| Cold Email Outreach skill.md | technology/sales-marketing-tech/ (functional-architecture + skills) | 2026-05-03 |
| Cold email outreach use case categories.md | technology/sales-marketing-tech/use-cases/ | 2026-05-03 |
| Converting a Claude skill into a plugin makes it more likely to be executed.md | technology/claude-anthropic/claude-cowork.md | 2026-04-27 |
| Do options use system 1 and does this introduce more bias.md | performance/the-human-mind/system-1-thinking-and-ai-options.md | 2026-04-21 |
| Email Personalisation & Content.md | technology/sales-marketing-tech/use-cases/personalisation.md | 2026-05-03 |
| Email Verification use case catalog.md | technology/sales-marketing-tech/use-cases/email-verification.md | 2026-05-03 |
| Email warmup use case catalog.md | technology/sales-marketing-tech/use-cases/email-warmup.md | 2026-05-03 |
| Lemlist vs Instantly.ai vs Saleshandy – A Complete Guide for Marketing Leaders in 2026.md | technology/sales-marketing-tech/vendors/ | 2026-04-30 |
| Lesson leaned - context switching.md | performance/working-with-yourself/adhd-aware-work-patterns.md | 2026-04-27 |
| Lessonlearnt1st100 (folder) | performance/ + career/ + wellbeing/ + relationships/ (~280 lessons batch) | 2026-04-21 |
| Lessonlearnt2nd100 (folder) | performance/ + career/ + wellbeing/ + relationships/ (~280 lessons batch) | 2026-04-21 |
| lessonslearnt3rd100 (folder) | performance/ + career/ + wellbeing/ + relationships/ (~280 lessons batch) | 2026-04-21 |
| lessonslearntlast3 (folder) | performance/ + career/ + wellbeing/ + relationships/ (~280 lessons batch) | 2026-04-21 |
| Prospecting Use Case Catalog.md | technology/sales-marketing-tech/use-cases/prospecting.md | 2026-05-03 |
| SNOV email finder.md | technology/sales-marketing-tech/vendors/snov-io/ | 2026-05-03 |
| SNOV pricing.md | technology/sales-marketing-tech/vendors/snov-io/ | 2026-05-03 |
| Snov.io Use-Case Based Product CatalogLead Gen Product Catalog.md | technology/sales-marketing-tech/vendors/snov-io/ | 2026-05-03 |
| Unified inbox and reply management.md | technology/sales-marketing-tech/use-cases/inbox-reply-management.md | 2026-05-03 |
| Use Claude's chat search and memory to build on previous context.md | technology/claude-anthropic/claude-cowork.md | 2026-04-27 |
| apollo-person-match (folder) | ai-os/skills/apollo-person-match/ | 2026-04-29 |
| 150k feasibility report - JH Clarifications.md | career/uk-150k-feasibility-jh-clarifications-2026-07-09.md + career/uk-ir35-contracting-feasibility-2026.md | 2026-07-09 |
| UK versus HK earnings - JH clarifications.md | career/uk-vs-hk-earning-comparison-jh-clarifications-2026-07-09.md | 2026-07-09 |

---

## Pending (in raw/ root — not yet compiled)

| File | Topic | Notes |
|------|-------|-------|
| 2026-05-19 Epic brainstorm.md | Epics / planning | Tiny stub; compile when ready to act on it |
| Stephan email brainstorm.md | TTI / Stephan message | Created 2026-06-05; source for the stephan-whatsapp draft |
| Nate B Jones AI Skill set prompt kit.md | AI skills / prompting | No wiki article found; pending compile |
| Prompt to insert additional Leads into google sheets.md | Leadgen / Google Sheets | No wiki trace; pending compile |
| The-Complete-Guide-to-Building-Skill-for-Claude.pdf | Claude / skill building | No wiki trace; large PDF; pending compile |

---

## How to use this manifest

1. **After every compile:** add a row to the Processed table; move the file to `raw/_processed/`.
2. **To check what is pending:** scan the Pending table.
3. **Do not delete raw files** — move them to `raw/_processed/` so the source material is preserved.
