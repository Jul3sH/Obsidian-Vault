---
type: index
updated: 2026-05-08
---

# Sales & Marketing Technology

> *Reference library for vendor capabilities, price books, use-case coverage, and pipeline architecture for cold outreach and lead enrichment.*

This section contains **product reference material** — not skills (those live in [[ai-os/skills/_index|AI OS / Skills]]) and not operational process (that lives in [[ai-os/service-design/_index|AI OS / Service Design]]). Use this section to answer "which tool?" and "how much?"

---

## Cold Email Outreach

A structured knowledge base for evaluating and selecting cold email tooling. Covers the full 6-step pipeline from lead prospecting through to inbox management.

### ⚠️ Always Map the Full Pipeline First

Before selecting vendors, map the complete data flow. Use cases have upstream dependencies that must be costed into the TCO:

```
[Email list]
     │
     ▼
Step 1 — Reverse Email Lookup       Email → LinkedIn URL
          Apollo, SalesQL, Prospeo  (existing skill: apollo-person-match)
     │
     ▼
Step 2 — LinkedIn Profile Scraping  LinkedIn URL → profile + posts data
          Fresh LinkedIn Scraper,   (existing skill: linkedin-enrichment)
          ProxyCurl
     │
     ▼
Step 3 — AI Icebreaker Generation   Profile data → personalised copy
          Claude Haiku, Claygent,
          Lemlist AI Variables
     │
     ▼
Step 4 — Domain Warm-up             New sending domains built to reputation
          Instantly, Lemwarm,
          TrulyInbox
     │
     ▼
Step 5 — Campaign Send              Emails sent + follow-up sequences
          Instantly, Lemlist,
          Saleshandy
     │
     ▼
Step 6 — Inbox & Reply Management   Replies triaged, routed, responded to
          Unibox, Lemlist inbox,
          OpenClaw
```

> ✅ Validation: When the user wants "personalised emails using LinkedIn data", always confirm steps 1 and 2 are covered before recommending a sequencer. Existing skills (apollo-person-match, linkedin-enrichment) may already handle these — check before adding cost.

### Reference Documents

| Document | What it covers |
|----------|---------------|
| [[technology/sales-marketing-tech/functional-architecture\|Functional Architecture]] | End-to-end pipeline with 5+ options per stage, pricing, and consolidation strategies |
| [[technology/sales-marketing-tech/use-cases/_index\|Use Cases]] | 6 use case definitions — what job each covers, inputs, outputs, and upstream dependencies |
| [[technology/sales-marketing-tech/vendors/_index\|Vendors]] | 20 vendor directories, each with `capabilities.md` and `pricing.md` |
| [[technology/sales-marketing-tech/domain-strategy\|Domain Strategy]] | Infrastructure: domain count, mailbox configuration, TLD trust tiers |
| [[technology/sales-marketing-tech/cost-comparison\|Cost Comparison]] | Stack-level TCO comparison across recommended configurations |
| [[technology/sales-marketing-tech/decision-framework\|Decision Framework]] | Vendor selection logic by workflow type and volume |
| [[technology/sales-marketing-tech/comparison-snov-vs-saleshandy\|Snov.io vs Saleshandy]] | Detailed head-to-head comparison for starter plans |
| [[technology/sales-marketing-tech/AUDIT-SOURCE-ATTRIBUTION\|Source Attribution Audit]] | Pricing file verification status (live vs estimated) for all 20 vendors |
| [[technology/sales-marketing-tech/pipeline-diagram\|Pipeline Diagram]] | Excalidraw diagram of the 7-stage pipeline with build status and data transformation labels |
| [[technology/sales-marketing-tech/active-subscriptions\|Active Subscriptions]] | Current paid subscriptions ($85/mo), renewal dates, and cancelled/lapsed tools |

### Use Cases

1. [[technology/sales-marketing-tech/use-cases/prospecting\|Prospecting]] — find and build a contact list
2. [[technology/sales-marketing-tech/use-cases/email-verification\|Email Verification]] — validate addresses before sending
3. [[technology/sales-marketing-tech/use-cases/email-warmup\|Email Warm-up & Infrastructure]] — build sender reputation
4. [[technology/sales-marketing-tech/use-cases/personalisation\|Personalisation & Content]] — write content that converts
5. [[technology/sales-marketing-tech/use-cases/campaign-sequence\|Campaign & Sequence Management]] — build and send campaigns
6. [[technology/sales-marketing-tech/use-cases/inbox-reply-management\|Inbox & Reply Management]] — manage replies at scale

### Vendors (20 total)

See [[technology/sales-marketing-tech/vendors/_index|vendors/_index]] for the full directory.

### Maintenance

- Pricing files include a `last-verified` frontmatter date — run `/tco` and it flags any pricing older than 60 days
- To refresh a single vendor: "Refresh pricing for [vendor]" — Claude Code fetches the pricing page and rewrites that vendor's `pricing.md`
- To add a new vendor: create `vendors/[vendor-name]/capabilities.md` and `vendors/[vendor-name]/pricing.md` following the existing format, then add to [[technology/sales-marketing-tech/vendors/_index|vendors/_index]]

---

## Related Skills

| Skill | What it does | Covers pipeline step |
|-------|-------------|---------------------|
| [[ai-os/skills/apollo-person-match/_index\|apollo-person-match]] | Name + email → LinkedIn URL via Apollo API | Step 1 |
| [[ai-os/skills/linkedin-enrichment/_index\|linkedin-enrichment]] | LinkedIn URL → profile + posts summary | Step 2 |
| `/tco` (CLAUDE.md) | Reads this library to produce a ranked TCO comparison for any objective + volume | All steps |
