| Feature                    | Trail     | Starter   | Pro S     | Pro M     | Pro L     | Ultra     |
| -------------------------- | --------- | --------- | --------- | --------- | --------- | --------- |
| Email Search               | 50        | 1,000     | 5,000     | 20,000    | 50,000    | 100,000   |
| Bulk Email Search          | 1,000     | 5,000     | 20,000    | 50,000    | 100,000   | —         |
| Domain Search              | 50        | 1,000     | 5,000     | 20,000    | 50,000    | 100,000   |
| Bulk Domain Search         | 1,000     | 5,000     | 20,000    | 50,000    | 100,000   | —         |
| LinkedIn Search            | 1,000     | 5,000     | 20,000    | 50,000    | 100,000   | —         |
| Database Search            | 50        | 1,000     | 5,000     | 20,000    | 50,000    | 100,000   |
| Email Finder (Chrome ext.) | 50        | 1,000     | 5,000     | 20,000    | 50,000    | 100,000   |
| LI Prospect Finder (ext.)  | 50        | 1,000     | 5,000     | 20,000    | 50,000    | 100,000   |
| Prospect sync from Gmail   | —         | Yes       | Yes       | Yes       | Yes       | Yes       |
| Storage (prospects)        | Unlimited | Unlimited | Unlimited | Unlimited | Unlimited | Unlimited |
| Email Tracker (ext.)       | Unlimited | Unlimited | Unlimited | Unlimited | Unlimited | Unlimited |

## Snov.io Email Finder Capabilities — Detailed Reference

## 1. Email Search (Single Lookup)

|Field|Details|
|---|---|
|**What it does**|Finds a verified business email address for a single prospect by matching their name against a company domain.[snov](https://snov.io/email-finder)|
|**Inputs required**|Prospect first name, last name, and company domain (e.g., `John Doe`, `acme.com`).|
|**Outputs returned**|Verified email address, verification status (`valid`, `not_valid`, `unknown`), and additional deliverability checks.|
|**Platform**|Web app, Chrome extension, API.[snov](https://snov.io/email-finder-api)|
|**Credit cost**|1 credit per found valid or unknown email; 0 if not valid.[snov](https://snov.io/knowledgebase/how-to-enrich-your-data-via-snov-io-api/)|
|**Best use case**|Quick lookup when you know the person's name and the company they work at.|

---

## 2. Bulk Email Search

|Field|Details|
|---|---|
|**What it does**|Finds verified emails in bulk from a list of prospect names and company domains. Turns a messy spreadsheet into a clean lead list.[snov](https://snov.io/bulk-email-finder)|
|**Inputs required**|CSV file with columns: `first_name`, `last_name`, `domain` (company domain).|
|**Outputs returned**|List of verified email addresses exportable as CSV/XLSX/TXT, or directly added to Snov.io prospect lists for campaign launch.[snov](https://snov.io/bulk-email-finder)|
|**Platform**|Web app (Bulk Email Finder tool), API.[snov](https://snov.io/api)|
|**Credit cost**|1 credit per prospect with valid/unknown email; 0 if not valid.[snov](https://snov.io/knowledgebase/how-to-enrich-your-data-via-snov-io-api/)|
|**Best use case**|You have a spreadsheet of known contacts (names + domains) and need to find all their work emails in one pass.|

---

## 3. Domain Search

|Field|Details|
|---|---|
|**What it does**|Finds all email addresses and prospect profiles associated with a specific company domain. Returns both employee emails and generic/department emails.[snov](https://snov.io/knowledgebase/how-to-use-domain-search-api/)|
|**Inputs required**|A single domain name (e.g., `stripe.com`).|
|**Outputs returned**|All discovered emails on the domain — employee emails with names/titles, plus generic emails like `admin@domain.com`, `help@domain.com`.[snov](https://snov.io/api) Paid accounts get prospect profiles (name, title, company).|
|**Platform**|Web app, API (`/v2/domain-search/prospects/start` and `/v2/domain-search/domain-emails/start`).[snov](https://snov.io/knowledgebase/how-to-use-domain-search-api/)|
|**Credit cost**|1 credit per domain search; 1 credit per saved prospect with valid/unknown email.[youtube](https://www.youtube.com/watch?v=FJUlprql7Jw)|
|**Best use case**|You want to map out an entire company's contacts before an outreach campaign.|

---

## 4. Bulk Domain Search

|Field|Details|
|---|---|
|**What it does**|Finds prospects and emails across a large list of company domains in a single batch operation. Processes up to 20,000 domains (or 100,000 prospects/day on higher plans).[snov](https://snov.io/b2b-lead-finder)|
|**Inputs required**|List of domain names (up to 20,000 per job), or CSV file of domains.|
|**Outputs returned**|Prospect profiles and email addresses for every domain in the list, delivered via webhook or API result endpoint.[snov](https://snov.io/api)|
|**Platform**|Web app, API.|
|**Credit cost**|1 credit per prospect with valid/unknown email found.|
|**Best use case**|You have a list of target companies and want to discover decision-makers at all of them at scale.|

---

## 5. LinkedIn Search

|Field|Details|
|---|---|
|**What it does**|Discovers verified email addresses and enriched prospect data from LinkedIn search results, company employee lists, event attendee lists, and Sales Navigator.[snov](https://snov.io/blog/best-linkedin-chrome-extensions/)|
|**Inputs required**|Either: (a) search filters (job title, company, location, industry), (b) a pasted LinkedIn search URL, or (c) a TXT/CSV file with LinkedIn profile URLs.|
|**Outputs returned**|Verified email addresses + enriched data: name, job title, company, location, industry, LinkedIn URL.snov+1|
|**Platform**|Chrome extension (LI Prospect Finder), Web app LinkedIn search, API (`/v2/li-profiles-by-urls/start`).[customerthink](https://customerthink.com/snov-io-launches-data-enrichment-api-after-powering-500m-leads-per-year/)|
|**Credit cost**|1 credit per URL with provided enrichment data.[snov](https://snov.io/knowledgebase/how-to-enrich-your-data-via-snov-io-api/)|
|**Best use case**|You are building a prospect list from LinkedIn — searching by role, company, or scraping attendees from events. Works with Sales Navigator.|

---

## 6. Database Search

|Field|Details|
|---|---|
|**What it does**|Searches Snov.io's 500M+ B2B contact database for prospects matching your Ideal Customer Profile (ICP). Supports both AI natural-language queries and traditional filter-based search.[snov](https://snov.io/b2b-lead-finder)|
|**Inputs required**|Filter-based: job title, management level (C-Level, VP, Director, Manager, Staff), department (Engineering, Sales, Marketing, etc.), location, industry, company size, revenue. Or: natural language description of ICP.[snov](https://snov.io/knowledgebase/how-to-find-prospects-with-database-search/)|
|**Outputs returned**|Pre-verified leads with name, job title, company, verified email address, LinkedIn profile URL.[snov](https://snov.io/knowledgebase/how-to-find-prospects-with-database-search/)|
|**Platform**|Web app (Database Search page), API.[snov](https://snov.io/knowledgebase/how-to-find-prospects-with-database-search/)|
|**Credit cost**|1 credit per saved prospect with valid/unknown email.|
|**Best use case**|You don't have a list yet — you're starting from a profile of who your ideal customer is, and need to discover them from scratch.|

---

## 7. Email Finder Chrome Extension

|Field|Details|
|---|---|
|**What it does**|Scans any webpage you're visiting and extracts associated email addresses. Works on company websites, Google search result pages, and more. Saves contacts directly to Snov.io lists.snov+1|
|**Inputs required**|None — just navigate to a website or Google search results page, click the extension icon, and it scans the page automatically.|
|**Outputs returned**|List of employee and department emails found on the page, with prospect names and titles where available. Saved to your Snov.io account / prospect lists.[galadon](https://galadon.com/snov-io-extension)|
|**Platform**|Chrome browser extension.[snov](https://snov.io/extension)|
|**Credit cost**|50 free lookups/month on free plan; paid plans get their plan's email search quota.[snov](https://snov.io/extension)|
|**Best use case**|You're browsing company websites or searching on Google and want to grab contacts in real-time without switching tools.|

---

## 8. LI Prospect Finder Chrome Extension

|Field|Details|
|---|---|
|**What it does**|Extracts verified emails and enriched LinkedIn profile data from any LinkedIn page — search results, individual profiles, company employee lists, event attendee lists, and Sales Navigator.snov+1|
|**Inputs required**|Navigate to LinkedIn, apply your search filters or go to a profile/company/event page, then click the extension icon.|
|**Outputs returned**|Per prospect: verified email, LinkedIn URL, full name, job title, company details, location, industry.[snov](https://snov.io/knowledgebase/how-to-use-li-prospect-finder-chrome-extension/)|
|**Platform**|Chrome browser extension.[snov](https://snov.io/knowledgebase/how-to-install-li-prospect-finder-chrome-extension/)|
|**Credit cost**|1 credit per prospect found with valid/unknown email.[snov](https://snov.io/knowledgebase/how-to-enrich-your-data-via-snov-io-api/)|
|**Best use case**|You are doing outbound prospecting directly on LinkedIn and want to build a lead list in one click from search results or company pages. Supports bulk extraction across multiple search result pages.[snov](https://snov.io/blog/best-linkedin-chrome-extensions/)|

---

## 9. Prospect Sync from Gmail

|Field|Details|
|---|---|
|**What it does**|Automatically syncs contacts and email interactions from Gmail into your Snov.io account and CRM timeline. Every contact you've emailed gets saved as a prospect with full history.[snov](https://snov.io/knowledgebase/how-email-tracker-syncs-with-snov-io-app/)|
|**Inputs required**|Gmail account connected to Snov.io (requires OAuth permissions: view/send email, view email metadata). Enable "Sync to CRM" toggle in the Email Tracker extension popup.[snov](https://snov.io/knowledgebase/how-email-tracker-syncs-with-snov-io-app/)|
|**Outputs returned**|Contacts are saved to a Snov.io prospect list with: full name, email address, sent emails, open/click/reply statistics, and prospect replies — all displayed in a timeline view per contact.[snov](https://snov.io/knowledgebase/how-email-tracker-syncs-with-snov-io-app/)|
|**Platform**|Chrome browser extension (Email Tracker) + Snov.io web app.[snov](https://snov.io/knowledgebase/how-email-tracker-syncs-with-snov-io-app/)|
|**Credit cost**|No credits consumed — this is a sync/integration feature, available on paid plans (Starter+).[snov](https://snov.io/knowledgebase/how-email-tracker-syncs-with-snov-io-app/)|
|**Best use case**|You're already emailing people in Gmail and want those interactions automatically logged and synced to your Snov.io CRM for tracking and follow-up.|

---

## 10. Email Tracker Chrome Extension

|Field|Details|
|---|---|
|**What it does**|Tracks email opens, link clicks, and replies for emails sent from Gmail. Adds invisible tracking pixels for opens and tags links for click tracking. Displays stats directly in your Gmail interface.[snov](https://snov.io/blog/how-to-track-outgoing-emails-in-gmail-with-snovio-email-tracker/)|
|**Inputs required**|Install extension, log into Snov.io account, activate on a Gmail account. No additional input — runs automatically on outgoing Gmail messages.[snov](https://snov.io/knowledgebase/how-to-track-your-outgoing-emails-inside-your-gmail-account/)|
|**Outputs returned**|Per-email statistics: open count, click count, reply detection, timestamps. Available in Gmail sidebar and synced to Snov.io CRM timeline.snov+1|
|**Platform**|Chrome browser extension.[chromewebstore.google](https://chromewebstore.google.com/detail/unlimited-email-tracker-b/gojogohjgpelafgaeejgelmplndppifh?hl=en)|
|**Credit cost**|Free (unlimited tracking).|
|**Best use case**|You want to know when a prospect opens your email or clicks a link, so you can time follow-ups effectively.|

---

## 11. Email Finder API

|Field|Details|
|---|---|
|**What it does**|Programmatic access to Snov.io's email finding database. Supports domain search, single email search, URL-based prospect search, profile lookup by email, and email count queries.[snov](https://snov.io/email-finder-api)|
|**Inputs required**|Depends on endpoint. Common inputs: `domain`, `first_name`, `last_name`, `url`, `email`. Auth via Bearer token. Webhooks optional for async results.[snov](https://snov.io/api)|
|**Outputs returned**|Verified email addresses, prospect profiles, verification status, pagination metadata (`task_hash`, `total_count`, `next`).[snov](https://snov.io/api)|
|**Platform**|REST API (`api.snov.io`).|
|**Credit cost**|1 credit per valid/unknown email found.|
|**Best use case**|You're building an integration, automating lead enrichment in a pipeline, or using Snov.io data from within another application.|

---

## 12. Data Enrichment API

|Field|Details|
|---|---|

|Field|Details|
|---|---|
|**What it does**|Enriches existing data with fresh B2B information via five enrichment methods: Company→Domain, Name+Domain→Email, Email Verification, LinkedIn URL→Profile, Email→Profile.[snov](https://snov.io/knowledgebase/how-to-enrich-your-data-via-snov-io-api/)|
|**Inputs required**|Varies by method:[snov](https://snov.io/knowledgebase/how-to-enrich-your-data-via-snov-io-api/)  <br>- Company to Domain: `names[]` (company names)  <br>- Email Finder: `rows[]` with `first_name`, `last_name`, `domain`  <br>- Email Verifier: `emails[]`  <br>- LinkedIn URL to Profile: `urls[]` (LinkedIn URLs)  <br>- Email to Profile: `email`|
|**Outputs returned**|Enriched B2B data: domains, verified emails with status, full profiles (name, title, industry, location, company details). Results delivered via webhook or polling the `/result` endpoint.[snov](https://snov.io/knowledgebase/how-to-enrich-your-data-via-snov-io-api/)|
|**Platform**|REST API (`api.snov.io/v2/...`).|
|**Credit cost**|1 credit per record returned with enrichment data; 0 if no data found.[snov](https://snov.io/knowledgebase/how-to-enrich-your-data-via-snov-io-api/)|
|**Best use case**|You have partial data (e.g., just company names or LinkedIn URLs) and need to expand it into full prospect records for outreach.|

---

## Summary: Which Tool for Which Job

|Scenario|Best Tool(s)|
|---|---|
|I know a person's name + company|Email Search (single) or Bulk Email Search (many)|
|I have a list of target companies|Domain Search or Bulk Domain Search|
|I'm prospecting on LinkedIn|LI Prospect Finder extension + LinkedIn Search|
|I'm starting from scratch with an ICP|Database Search|
|I'm browsing websites / Google|Email Finder Chrome Extension|
|I'm browsing LinkedIn pages|LI Prospect Finder Chrome Extension|
|I want Gmail interactions auto-logged|Prospect Sync from Gmail + Email Tracker|
|I'm building an integration or automation|Email Finder API + Data Enrichment API|
|I need verification status only|Email Verifier (in the Verification section)|

All data sourced from Snov.io's product pages, knowledgebase, and API documentation.snov+4