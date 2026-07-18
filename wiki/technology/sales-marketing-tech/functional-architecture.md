# Lead Generation Pipeline — Functional Architecture

tags: [technical, lead-enrichment, pipeline, architecture]

> *End-to-end pipeline from raw contact list to followed-up cold outreach. 7 functional stages.*

---

## Pipeline Overview

```
[Stage 1]       [Stage 2]        [Stage 3]          [Stage 4]       [Stage 5]         [Stage 6]      [Stage 7]
Lead List   →  LinkedIn URL  →  LinkedIn Profile  →  Domain      →  Email         →  Cold Email  →  Follow-up
(name+email)   Lookup           Enrichment            Warmup          Creation          Sending        Sequences
                (email→URL)      (URL→summary)         (one-off)       (LLM-written)
```

**What's built vs. pending:**
- ✅ Stage 3: LinkedIn enrichment skill (complete)
- 🔧 Stage 2: Apollo Person Match / LinkFinder (in progress)
- ⬜ Stages 1, 4, 5, 6, 7: To be selected and configured

---

## Stage 1: Lead List Creation

### What
A Google Sheet containing one row per prospect with: full name, and a **validated** email address. This is the pipeline's starting point and sole input.

### Why
- Email address (not name) is used as the primary identifier for Stage 2 — names are ambiguous (duplicates, nicknames, initials). A validated email guarantees the address is real before spending credits on enrichment.
- Validation protects email domain reputation by eliminating hard bounces before sending.

### How
Prospects are sourced using a prospecting tool or manual research, then email addresses are verified before they enter the sheet. Each provider validates in slightly different ways (SMTP checks, database cross-reference).

### Options

| # | Tool | What it does | Cost Model | Also Covers | Approximate Cost |
|---|---|---|---|---|---|
| 1 | **Apollo.io** | Search prospects by title/company/location; reveals verified emails | Per email reveal credit | Stages 2, 7 | $49/seat/mo (Basic annual) — 2,500 credits/mo |
| 2 | **LinkedIn Sales Navigator + Hunter.io** | Find prospects on LinkedIn; Hunter finds/validates their email | SalesNav flat + Hunter per verify | — | $99/mo (SalesNav) + $49/mo (Hunter) |
| 3 | **Lusha** | Contact data with verified emails and direct dials; Chrome extension | Per credit (contact reveal) | — | $29-99/mo depending on plan |
| 4 | **Clay** | AI-powered list building; searches LinkedIn, company databases; auto-enriches | Per credit / monthly | Stages 3, 5 | $99/mo (includes enrichment for Stages 3+5) |
| 5 | **HubSpot Sales Hub** | CRM-based prospecting; built-in email validation and lead import | Per contact / monthly flat | Stages 5, 6, 7 | $50/mo (Starter) + email sending fees |

**Note:** The lead list itself can be built once and reused, or continuously appended as new contacts are identified. Integrated tools (Clay, HubSpot) may save cost if you consolidate multiple stages in one platform.

---

## Stage 2: Reverse Email Lookup

### What
Takes the validated email address from Stage 1 and resolves it to a LinkedIn profile URL. This is technically a **reverse email lookup** — using an email address as the identifier to find a person's LinkedIn profile. Output: `linkedin_url` written back to the Google Sheet.

### Why
- Email is the most reliable identifier for person matching. A business email address is nearly unique to one individual and directly resolves to one LinkedIn profile.
- Name-based matching (e.g. "Julian Hart") is unreliable due to duplicates, initials, and name variations — deliberately avoided in this pipeline.
- `linkedin_url` is the required input for Stage 3. Without it, profile enrichment cannot proceed.

### How
API call to a reverse email lookup provider. Request: `{email: "x@company.com"}`. Response: LinkedIn URL + varying additional fields depending on provider. Status written to sheet: `matched`, `no_linkedin`, or `failed`.

### Important: Tool Selection Criteria
Not all tools marketed as "LinkedIn enrichment" support email-as-input. **Name-based tools must be excluded from this stage.** Only providers that explicitly accept an email address and return a LinkedIn URL qualify.

### Options

| Service | Free Tier | Paid Plans (monthly) | Cost per Successful Lookup | What You Get on a Hit | Typical Use Case |
|---|---|---|---|---|---|
| **Prospeo** | 75 verified emails/mo | From ~$0.01/email (no annual contract) | ~$0.01 | Full B2B profile: name, title, company, LinkedIn URL, direct mobile, technographics, intent signals — 98% email accuracy | Richest data return per lookup; best when you need more than just the LinkedIn URL |
| **SalesQL** | 50 credits/mo | Basic $39/mo (2,000 cr); Pro $119/mo (6,000 cr); Ultimate $179/mo (12,000 cr) | ~$0.02 ($39 ÷ 2,000) | Name, title, company details, LinkedIn URL; phone numbers on paid plans — verified business profile | Simple credit-based tool; generous free tier; clear pricing; good for moderate volumes |
| **Apollo.io People Match API** | None (API) | Basic $49/seat/mo; Pro $79/seat/mo (annual) | ~$0.002 (annual); ~$0.024 (monthly) | LinkedIn URL + title + company + phone + email (if matched) — 60–70% match rate for email→URL | Best if already using Apollo for Stage 1; consolidates prospecting + URL lookup in one platform |
| **ProxyCurl Reverse Email** | None | Pay-per-use only | ~$0.003–$0.01 | LinkedIn URL + basic profile data — ~70% accuracy (estimated) | Low-volume or testing; no monthly commitment; good API for developers |
| **Lix** | 50 email credits + 1,000 rows search + 10 API credits | Leads $39/mo (300–1,000 cr); Data Plus $109/mo (500–10,000 cr) | ~$0.04–$0.13 (depending on tier) | LinkedIn URL, name, company details — basic identity enrichment; credit rollover | API-driven lookups at lower volume; prefer credit rollover over monthly expiry |

### Key Distinction
> **LinkFinder AI is name-based, not email-based** — it resolves a LinkedIn URL from a person's name, not their email address. It does not accept email as input and must not be used for this stage. See [[technology/lead-enrichment/linkfinder/_index|LinkFinder documentation]] for its actual use case.

**See also:** [[technology/lead-enrichment/decision-framework|Decision Framework — Stage 2 Tool Selection]]

---

## Stage 3: LinkedIn Profile Enrichment

### What
Fetches LinkedIn profile data (work history, bio, skills, recent activity) for each matched contact and generates an AI summary. Output: `profile_summary` and `recent_posts_summary` written to the Google Sheet.

### Why
- Personalized cold emails that reference a prospect's specific background, recent posts, or career trajectory achieve dramatically higher reply rates (5–10%+) vs. generic templates (<1%).
- AI summarization distills raw LinkedIn data into usable personalization context — ready for email generation in Stage 5.

### How
Python skill: reads `linkedin_url` from sheet → calls LinkedIn scraper API to fetch profile and posts → passes raw data to LLM for summarization → writes summaries back to sheet.

### Options

| # | Tool | What it does | Cost Model | Also Covers | Approximate Cost |
|---|---|---|---|---|---|
| 1 | **RapidAPI Fresh LinkedIn Scraper + Claude Haiku** *(built)* | Scrapes profile + posts; Haiku writes summaries | Per lead | — | ~$0.005/lead (4 RapidAPI credits + $0.001 Haiku) |
| 2 | **ProxyCurl API + LLM** | Cleaner LinkedIn data API; add any LLM for summarization | Per profile endpoint | — | $0.01/profile + LLM cost; better structured data |
| 3 | **Clay** *(integrated)* | No-code enrichment platform; LinkedIn data + AI email writing + lead list building (Stages 1, 3, 5) | Per credit monthly | Stages 1, 5 | $99/mo flat covers Stages 1, 3, 5; per-lead cost ~$0.012 |
| 4 | **Clearbit** | B2B data enrichment; company + person data; best-in-class data quality | Per company + per person | — | $99/mo (Starter) + $50/mo (person data) |
| 5 | **HubSpot Sales Hub** *(integrated)* | Built-in LinkedIn enrichment; auto-syncs profile data into contacts (Stages 1, 3, 5, 6, 7) | Platform flat fee | Stages 1, 5, 6, 7 | $50/mo (Starter); enrichment included |

---

## Stage 4: Email Domain Warming

### What
Gradually ramps up email sending volume from new domains over 2–4 weeks to establish sender reputation with email providers (Gmail, Outlook, etc.).

### Why
- ISPs flag new domains that suddenly send high volumes as spam.
- Warmed domains have significantly lower spam folder placement rates.
- **One-time setup per domain**, then ongoing maintenance to sustain reputation.

### How
Automated tool sends emails between a large network of real mailboxes and marks them as "not spam." Volume increases gradually day by day. Takes 2–4 weeks per domain. Most cold email platforms include this.

### Options

| # | Tool | What it does | Cost Model | Also Covers | Approximate Cost |
|---|---|---|---|---|---|
| 1 | **Instantly.ai** *(included)* | Warmup included in all sending plans; no separate cost if using Instantly for Stage 6 | Included in sending plan | Stages 6, 7 | $0 extra if using Instantly for Stage 6 ($47/mo) |
| 2 | **Smartlead** *(included)* | Same — warmup included in sending plan | Included in sending plan | Stages 6, 7 | $0 extra if using Smartlead for Stage 6 ($39/mo) |
| 3 | **Lemlist** *(included)* | Warmup via Lemwarm; included in paid plans | Included in sending plan | Stages 6, 7 | $0 extra if using Lemlist for Stage 6 ($50/mo) |
| 4 | **Saleshandy** *(included)* | TrulyInbox warmup included with all plans; unlimited email accounts | Included in sending plan | Stages 6, 7 | $0 extra if using Saleshandy for Stage 6 ($36–139/mo) |
| 5 | **Mailreach** *(standalone)* | Dedicated warmup-only tool; works with any SMTP provider | Per mailbox/mo | — | $25/mailbox/mo — use if you want to separate warmup from sending tool |

**Recommendation:** Use the warmup included in whichever platform you choose for Stage 6. Separate warmup tools only make sense if you need SMTP flexibility or are using external SMTP providers.

---

## Stage 5: Personalized Email Creation

### What
Generates a customized cold outreach email for each prospect using their LinkedIn enrichment summaries from Stage 3. Output: a personalized email draft per contact, ready for Stage 6.

### Why
- Mass personalization at scale. Each email should reference something specific to the prospect — their recent role change, a post they wrote, a shared background element.
- LLM-generated personalization is the step that turns a list of enriched contacts into high-converting emails.

### How
Python skill or platform: reads `profile_summary` + `recent_posts_summary` from sheet → passes to LLM with ICP context and email template prompt → outputs subject line + email body per contact.

### Options

| # | Tool | What it does | Cost Model | Also Covers | Approximate Cost |
|---|---|---|---|---|---|
| 1 | **Claude Haiku/Sonnet (custom skill)** | Full control of tone, format, length, ICP prompt; skill reads from sheet and writes draft emails | Per email | — | ~$0.001–0.005/email (Haiku); ~$0.01–0.03/email (Sonnet) |
| 2 | **Clay** *(integrated)* | No-code; combines list building + LinkedIn enrichment + AI email writing (Stages 1, 3, 5) | Per credit monthly | Stages 1, 3 | $99/mo flat covers Stages 1, 3, 5 |
| 3 | **HubSpot Sales Hub** *(integrated)* | Email templates + basic AI personalization; auto-inserts contact fields (Stages 1, 3, 5, 6, 7) | Included in platform | Stages 1, 3, 4, 6, 7 | $50/mo (Starter) |
| 4 | **Instantly AI / Lemlist AI** *(built-in)* | Basic AI personalization built into cold email platform; less control than custom | Included in sending plan | Stages 4, 6, 7 | Included in Stage 6 platform cost — simpler but less flexible |
| 5 | **Outreach / SalesLoft** *(integrated)* | Enterprise sales engagement platform; AI-driven email sequencing and personalization (Stages 5, 6, 7) | Per user / monthly | Stages 6, 7 | $300–500/user/mo — best for enterprise scale |

---

## Stage 6: Cold Outreach Email Sending

### What
Sends the personalized cold emails at scale from warmed domains. Handles SMTP routing, tracking (opens, clicks), bounce management, and compliance (unsubscribe links).

### Why
- The delivery mechanism for the pipeline output.
- Deliverability infrastructure (domain rotation, IP warm-up, spam filter avoidance) is complex — a dedicated platform handles this.

### How
Import contacts (CSV or API) into cold email platform → assign to campaign → platform sends at scheduled times from warmed mailboxes → tracks engagement per contact.

### Options

| # | Tool | Volume | Warmup | Also Covers | Cost | Notes |
|---|---|---|---|---|---|---|
| 1 | **Instantly.ai Growth** | Unlimited emails | Included | Stages 4, 7 | $47/mo (annual) | Market leader; unlimited domains; simple UI |
| 2 | **Smartlead Basic** | Unlimited emails | Included | Stages 4, 7 | $39/mo (annual) | Strong API; good for automation pipelines |
| 3 | **Lemlist Email Pro** | Unlimited emails | Via Lemwarm | Stages 4, 7 | $50/mo (annual) | Most features; LinkedIn automation add-on available |
| 4 | **Saleshandy Starter** | 150k emails/mo | TrulyInbox (7-day) | Stages 4, 7 | $36/user/mo | Unlimited email accounts; AI Co-Pilot for sequences; sender rotation |
| 5 | **HubSpot Sales Hub** *(integrated)* | Unlimited emails | Included | Stages 1, 3, 4, 5, 7 | $50/mo (Starter) | CRM + email + sequences; best for multi-stage consolidation |

---

## Stage 7: Follow-up Outreach

### What
Automated sequence of follow-up emails sent to prospects who have not replied. Typically 2–4 additional touchpoints sent 3–7 days apart after the initial email.

### Why
- Most replies come from follow-ups — 80% of sales require 5+ contacts.
- Automated sequences ensure consistent follow-up without manual effort.
- Conditional logic (e.g., "if opened but no reply, send this variant") improves relevance.

### How
Multi-step email sequences configured within the cold email platform. Each step triggers after a set delay if no reply detected. Can include variants based on engagement signals (opened, clicked).

### Options

| # | Tool | Sequences | Conditions | A/B Testing | Also Covers | Included in |
|---|---|---|---|---|---|---|
| 1 | **Instantly.ai** | Unlimited steps | Yes | Yes | Stages 4, 6 | Stage 6 plan — no extra cost |
| 2 | **Smartlead** | Unlimited steps | Yes | Yes | Stages 4, 6 | Stage 6 plan — no extra cost |
| 3 | **Lemlist** | Unlimited steps | Yes | Yes | Stages 4, 6 | Stage 6 plan — no extra cost |
| 4 | **Saleshandy** | Unlimited steps (AI Co-Pilot) | Yes (sender rotation) | Yes | Stages 4, 6 | Stage 6 plan ($36–139/mo) — included with all plans |
| 5 | **Apollo.io** *(integrated)* | Unlimited steps (paid plans) | Yes | Yes | Stages 1, 2, 6 | If using Apollo for Stages 1+2 ($49/mo) — sequences included, consolidates stack |

---

## Stage Summary Table

| Stage | Purpose | Key Decision | Best-of-Breed (5 options) | Built? |
|---|---|---|---|---|
| 1 — Lead List | Source + validate name + email | Prospecting tool; consolidate with Clay/HubSpot? | Apollo, Hunter, Lusha, **Clay**, **HubSpot** | ⬜ |
| 2 — LinkedIn URL | Email → LinkedIn URL | Reverse email lookup accuracy vs cost | Prospeo, SalesQL, Apollo, ProxyCurl, Lix | 🔧 |
| 3 — Profile Enrichment | URL → profile + posts summary | RapidAPI+Haiku vs Clay vs HubSpot vs Clearbit | RapidAPI, ProxyCurl, **Clay**, Clearbit, **HubSpot** | ✅ |
| 4 — Domain Warmup | New domain reputation building | Platform-included vs standalone | **Instantly**, **Smartlead**, **Lemlist**, **Saleshandy**, Mailreach, **HubSpot** | ⬜ |
| 5 — Email Creation | Profile data → personalized email | Custom skill vs no-code vs platform | Custom Claude, **Clay**, **HubSpot**, **Instantly**/**Lemlist**, **Outreach** | ⬜ |
| 6 — Email Sending | Send cold emails at scale | Cold email platform or CRM? | **Instantly**, **Smartlead**, **Lemlist**, **Saleshandy**, **HubSpot** | ⬜ |
| 7 — Follow-up | Automated reply sequences | Included in sending tool | **Instantly**, **Smartlead**, **Lemlist**, **Saleshandy**, **Apollo**, **HubSpot** | ⬜ |

**Legend:** Bold = integrated tools (cover multiple stages). See "Also Covers" column in each stage for cross-pipeline tools.

---

## Multi-Stage Consolidation Strategies

This architecture lists 5 options per stage. Integrated tools (Clay, HubSpot, Apollo, Outreach) span multiple stages and may offer better TCO than best-of-breed. Three consolidation patterns:

1. **Best-of-Breed:** RapidAPI (Stage 3) + Claude (Stage 5) + Instantly (Stages 4, 6, 7) + Apollo (Stages 1, 2, 7) = cheapest per stage but integration overhead
2. **Clay Consolidation:** Clay (Stages 1, 3, 5) + Apollo (Stages 2, 7) + Instantly (Stages 4, 6) = mid-price, less integration work
3. **HubSpot Full Stack:** HubSpot (Stages 1, 3, 4, 5, 6, 7) + Apollo or Prospeo (Stage 2) = highest all-in-one cost, lowest integration complexity

See TCO calculator for side-by-side cost comparison of each pattern.

---

## See Also

- [[technology/lead-enrichment/cost-comparison|Stage 2 Cost Comparison (Reverse Email Lookup)]]
- [[technology/lead-enrichment/decision-framework|Stage 2 Decision Framework — Which Reverse Email Lookup Tool]]
- **TCO Calculator (Google Sheet):** https://docs.google.com/spreadsheets/d/1sPtYRr_89djclEeZFSDsbrQpi2zABBHQ4BUvPLCO8Qs — v4: All 7 stages (1a, 1b, 2, 3, 4, 5, 6, 7), 6 recommended stacks, cost-per-reply analysis
- **System Diagram (HTML):** `/Users/julianhart/Downloads/lead-gen-pipeline-diagram/index.html` — Interactive visualization of all options and stacks
- [[technology/lead-enrichment/apollo-person-match/_index|Apollo Person Match Skill]]
- [[technology/lead-enrichment/linkedin-enrichment/_index|LinkedIn Enrichment Skill]]
