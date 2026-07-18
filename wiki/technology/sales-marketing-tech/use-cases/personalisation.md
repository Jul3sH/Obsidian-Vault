---
name: Email Personalisation & Content
category: cold-email-outreach
---

# Email Personalisation & Content

**Job to be done:** Create and personalise the email content so it doesn't look like spam and drives higher reply rates.

## Inputs
- Contact profile data (name, title, company, LinkedIn activity, recent news)
- Brief / messaging objective
- Desired tone or persona

## Outputs
- Personalised email copy (icebreaker, body, CTA)
- AI-generated opening lines unique to each prospect
- Dynamic content that changes per recipient
- Multi-language variations

## Key Capabilities to Evaluate
- **Dynamic merge fields** — standard name/company tags plus conditional if/then content
- **AI email generation** — full email written from a brief; how many hours does it save?
- **AI icebreakers / opening lines** — researches each prospect individually for unique first lines
- **Voice / tone cloning** — trains on your email history to match your writing style
- **Spintax / text spinning** — randomises phrasing across sends to avoid ESP pattern detection
- **Visual personalisation** — personalised images (whiteboard with prospect name, logo on mug)
- **Video personalisation** — dynamic video thumbnails per prospect (Sendspark etc.)
- **Multi-language** — auto-generate or translate into prospect's language
- **Fallback handling** — backup content when personalisation data is missing

## ⚠️ Upstream Prerequisites — Required Before This Step

Personalisation **cannot happen without enriched contact data**. If you are starting from an email list, two upstream steps must be completed first:

| Step | Job | Example Tools |
|------|-----|---------------|
| 1. Reverse email lookup | Email address → LinkedIn URL | Apollo, SalesQL, ProxyCurl, Prospeo |
| 2. LinkedIn profile enrichment | LinkedIn URL → profile data (headline, experience, education, posts) | [[technology/cold-email-outreach/vendors/fresh-linkedin-scraper/capabilities\|Fresh LinkedIn Scraper]], ProxyCurl |
| 3. AI icebreaker generation | Profile data → personalised copy | Claude Haiku, Clay Claygent, Lemlist AI Variables |

**Existing implementation in this wiki:**
- [[technology/linkedin-enrichment\|LinkedIn Enrichment skill]] — step 2 (RapidAPI Fresh LinkedIn Scraper → Claude Haiku → Google Sheets)
- [[technology/apollo-person-match\|Apollo Person Match skill]] — step 1 (email → LinkedIn URL via Apollo)

> ✅ Validation check: Before recommending a personalisation vendor, confirm the user has a plan for steps 1 and 2 above. If they only have an email list, steps 1 and 2 must be costed into the TCO.

## Vendors in This Category
Snov.io, Apollo, HubSpot, Instantly, Lemlist, Saleshandy, Clay, n8n, Claude Code, OpenAI Codex, Hermes Agent, OpenClaw

## Key Takeaways
- Lemlist is the only native platform with visual + video personalisation (images, Sendspark, dynamic landing pages)
- Claude Code can generate deeply personalised first lines from live prospect research (LinkedIn, funding, hiring signals) in 15–30 min for a full campaign
- Clay's Claygent generates research-backed personalisation from 150+ enrichment providers
- OpenAI Codex writes replies in your own voice by learning from your Gmail history
- Voice cloning is native only in Lemlist and HubSpot; all AI tools can approximate via system prompt tuning
