## Snov.io Use-Case Based Product Catalog

**Structure:** `I have...` → `I want to...` → **Best tool(s)** → How it works (inputs/outputs). All data sourced from Snov.io product pages, knowledgebase, and API docs.

---

## 1. I have a person's name + company domain → I want their verified email

|Tool|Platform|Inputs|Outputs|When to use|
|---|---|---|---|---|
|**Email Search** (single lookup)|Web app, Chrome ext, API|First name, last name, domain|Verified email + verification status|One-off lookup. You know the person and their company.|
|**Email Finder API** (`/v2/emails-by-domain-by-name`)|REST API|`first_name`, `last_name`, `domain` (up to 10 rows per request)|Verified email + status + deliverability checks|Automating lookups in a script or pipeline.|

**Credit cost:** 1 credit per valid/unknown email found; 0 if not valid.

---

## 2. I have a spreadsheet of names + domains → I want verified emails for all of them

|Tool|Platform|Inputs|Outputs|When to use|
|---|---|---|---|---|
|**Bulk Email Finder**|Web app|CSV with columns: `first_name`, `last_name`, `domain`|List of verified emails; exportable as CSV/XLSX/TXT or directly to Snov.io prospect list|You have a messy spreadsheet of contacts and need clean emails in one pass.|
|**Email Finder API** (bulk)|REST API|`rows[]` array of `{first_name, last_name, domain}` objects (up to 10 per POST, batch multiple)|Verified emails with status per row; delivered via webhook or polling `[web:23]`|Building an automated enrichment pipeline — e.g., enriching CRM contacts programatically.|

**Credit cost:** 1 credit per valid/unknown email.

---

## 3. I have a single company domain → I want all contacts and emails at that company

|Tool|Platform|Inputs|Outputs|When to use|
|---|---|---|---|---|
|**Domain Search**|Web app|A single domain name (e.g., `stripe.com`)|All employee emails on the domain + generic/department emails (`admin@`, `help@`) + prospect profiles (name, title, LinkedIn URL on paid plans)|Mapping out a target account before outreach. You want to see the full org chart of contacts.|
|**Domain Search API** (`/v2/domain-search/prospects/start`)|REST API|`domain` (company website)|Prospect profiles with emails, names, titles; paginated (20 per page); `task_hash` for async retrieval `[web:26]`|Automating account-based prospecting at scale across many domains.|

**Credit cost:** 1 credit per domain search; 1 credit per saved prospect with valid/unknown email.

---

## 4. I have a list of company domains → I want prospects/emails across all of them

|Tool|Platform|Inputs|Outputs|When to use|
|---|---|---|---|---|
|**Bulk Domain Search**|Web app|List of domains (up to 20,000 per job)|Prospect profiles and emails for every domain; delivered via webhook or download|You have a target account list and want to discover decision-makers at scale across all of them.|
|**Domain Search API** (batch multiple domains)|REST API|Multiple `domain` parameters (batch separate requests or loop)|Same as single-domain, but aggregated across all target companies|Building an ABM pipeline. Your script iterates through a list of target accounts.|

**Credit cost:** 1 credit per prospect with valid/unknown email found.

---

## 5. I have a company name → I want their domain (website)

|Tool|Platform|Inputs|Outputs|When to use|
|---|---|---|---|---|
|**Data Enrichment API** — Company to Domain|REST API (`/v2/company-domain-by-name/start`)|`names[]` — company names (up to 10 per request)|Company domain (website) for each name.|You have company names from events, directories, or lists but no websites.|

**Credit cost:** 1 credit per company with found domain.

---

## 6. I have a LinkedIn profile URL → I want their email + full enriched profile

|Tool|Platform|Inputs|Outputs|When to use|
|---|---|---|---|---|
|**Data Enrichment API** — LinkedIn URL to Profile|REST API (`/v2/li-profiles-by-urls/start`)|`urls[]` — LinkedIn profile URLs (up to 10 per request)|Prospect: name, job title, industry, location. Company: name, domain, LinkedIn URL, industry, location. Email if found.|You sourced leads from LinkedIn and need to build outreach-ready records.|
|**LI Prospect Finder (Chrome extension)**|Chrome browser|Navigate to LinkedIn profile → click extension icon|Verified email + name, title, company, location, industry, LinkedIn URL|Browsing LinkedIn manually. One-click enrichment per profile or bulk from search results.|

**Credit cost:** 1 credit per URL with enrichment data returned.

---

## 7. I have a LinkedIn profile URL → I want a full CRM-ready prospect record

|Tool|Platform|Inputs|Outputs|When to use|
|---|---|---|---|---|
|**Data Enrichment API** — LinkedIn URL to Profile (same as above)|REST API|`urls[]`|Name, title, industry, city/country, company name, company domain, company LinkedIn URL, company industry, company location|You're building a prospect database from LinkedIn URLs and need structured fields for your CRM.|

This is the same endpoint but worth calling out separately because the _output_ — a full CRM-ready profile — is the goal, not just the email.

---

## 8. I have a verified email → I want the prospect's full profile (including LinkedIn URL if available)

|Tool|Platform|Inputs|Outputs|When to use|
|---|---|---|---|---|
|**Data Enrichment API** — Email to Profile (`/v1/get-profile-by-email`)|REST API|A single email address|Prospect profile info (name, company, job title, location, industry). LinkedIn URL _may_ be included if in database.|Reverse-enriching an email you already have. First step in a chain.|
|**Chained: get-profile-by-email → Domain Search**|REST API (2-step)|Step 1: email → Step 2: domain + name from step 1|Full profile including LinkedIn URL, if the domain search matches the person|When step 1 doesn't return LinkedIn data. Use name+domain from step 1 to find the full record via domain search.|

**Note:** This is Snov.io's weakest direction. The native reverse lookup exists but LinkedIn URL coverage is not guaranteed.

**Credit cost:** 1 credit if data found; 0 if not.

---

## 9. I have a list of email addresses → I want to know which are valid/deliverable

|Tool|Platform|Inputs|Outputs|When to use|
|---|---|---|---|---|
|**Email Verifier**|Web app|Single email address or bulk upload|Verification status: `valid`, `not_valid`, `unknown`; reasons for unknown (Banned, Catchall, Connection error, Greylisted, Hidden)|Cleaning a list before sending campaigns. Reducing bounce rates.|
|**Email Verifier API** (`/v2/email-verification/start`)|REST API|`emails[]` — email addresses (up to 10 per POST)|Same status data per email; via webhook or polling|Automating list hygiene. Verifying signups in real time. Integrating into form validation.|

**Credit cost:** 1 credit per email checked, regardless of result.

---

## 10. I have an ideal customer profile (ICP) → I want to discover prospects who match it

|Tool|Platform|Inputs|Outputs|When to use|
|---|---|---|---|---|
|**Database Search**|Web app|Filters: job title, management level (C-Level to Staff), department, location, industry, company size, revenue. Or: natural language ICP description|Pre-verified leads with name, job title, company, verified email, LinkedIn URL. Ready for LinkedIn automation.|Starting from zero. You know WHO you want to reach but have no list yet.|
|**AI-powered natural language search** (within Database Search)|Web app|Plain English description of your ICP (e.g., "VPs of Engineering at SaaS companies in the US with 51–200 employees")|Same as above — matched prospects with verified emails and LinkedIn URLs|You don't want to configure filters manually. Describe your ideal customer in plain language.|

**Credit cost:** 1 credit per saved prospect with valid/unknown email.

---

## 11. I have a LinkedIn search URL or specific search criteria → I want emails + enriched data for everyone in the results

|Tool|Platform|Inputs|Outputs|When to use|
|---|---|---|---|---|
|**LinkedIn Search** (web app)|Web app|LinkedIn search URL (pasted), or in-app filters (keyword, company, location, connections degree)|Verified emails + full profiles (name, title, company, location, industry, LinkedIn URL) for all prospects in search results|You already did a filtered search on LinkedIn and want to extract all the contacts from it. Supports Sales Navigator URLs.|
|**LinkedIn Search — Import from file**|Web app|CSV or TXT file with LinkedIn profile URLs (standard or Sales Navigator format)|Same enriched output for each URL in the file|You exported a list of LinkedIn profiles from another tool and want to enrich them in bulk.|
|**LI Prospect Finder (Chrome extension)**|Chrome browser|Navigate to LinkedIn search results → click extension; process multiple pages automatically|Verified email + full enriched profile per prospect; bulk extraction across multiple result pages|You're browsing LinkedIn and want to scrape an entire search results page (or multiple pages) in one click.|

**Credit cost:** 1 credit per prospect with valid/unknown email.

---

## 12. I have a company's website I'm browsing right now → I want all employee emails from that page

|Tool|Platform|Inputs|Outputs|When to use|
|---|---|---|---|---|
|**Email Finder (Chrome extension)**|Chrome browser|Navigate to any company website → click extension icon|All employee and department emails found on the page, with names/titles where available. Saved to Snov.io prospect list.|You're doing account research and want to grab contacts as you browse. Works on any website.|

**Credit cost:** 50 free lookups/month; then plan quota.

---

## 13. I'm browsing Google search results → I want to bulk-extract emails from all the companies shown

|Tool|Platform|Inputs|Outputs|When to use|
|---|---|---|---|---|
|**Email Finder (Chrome extension)** — Google results mode|Chrome browser|Run a Google search (e.g., "SaaS companies San Francisco") → click extension icon|Emails extracted from all search result pages in bulk. Saved to prospect list.|Building a list by searching for companies in a specific industry or location on Google. No need to visit each site.|

**Credit cost:** 50 free lookups/month; then plan quota.

---

## 14. I have a LinkedIn page I'm browsing right now → I want to extract all contacts on that page

|Tool|Platform|Inputs|Outputs|When to use|
|---|---|---|---|---|
|**LI Prospect Finder (Chrome extension)**|Chrome browser|Navigate to LinkedIn search results, company employee list, event attendee list, or Sales Navigator page → click extension icon|Verified emails + enriched profiles for all prospects on the page (name, title, company, location, industry, LinkedIn URL)|Passive prospecting. You're reviewing profiles, company pages, or event lists on LinkedIn and want to capture contacts without manual data entry.|

**Credit cost:** 1 credit per prospect with valid/unknown email.

---

## 15. I have an email address → I want to know when they open/click my emails

|Tool|Platform|Inputs|Outputs|When to use|
|---|---|---|---|---|
|**Email Tracker (Chrome extension)**|Chrome browser|Install extension, activate on a Gmail account, send email to the address|Per-email stats: open count, click count, timestamps, reply detection. Displayed in Gmail sidebar and Snov.io CRM timeline.|You're already emailing someone in Gmail and want to know when they engage, so you can time follow-ups.|
|**Prospect Sync from Gmail**|Chrome extension (Email Tracker) + Snov.io web app|Gmail account connected to Snov.io with "Sync to CRM" enabled|Contacts from Gmail interactions auto-saved as prospects with full timeline: sent emails, opens, clicks, replies, prospect replies|You want ALL your Gmail interactions with prospects automatically logged into Snov.io's CRM for tracking and follow-up.|

**Credit cost:** Free (unlimited tracking). Prospect Sync available on paid plans (Starter+).

---

## 16. I have a verified email → I want to verify it won't bounce before sending

|Tool|Platform|Inputs|Outputs|When to use|
|---|---|---|---|---|
|**Email Verifier**|Web app, Chrome ext, API|A single email or bulk list|Status: `valid`, `not_valid`, `unknown`; detailed reasons for unknown|Last-mile check before adding someone to a campaign. Or cleaning a list pre-import.|

**Credit cost:** 1 credit per email checked.

## 17. Reverse Email Lookup Detail (Row #17 expanded)

**Use Case #17: I have an email address → I want the person's LinkedIn profile URL + company info**

|Product|Platform|What it returns|Coverage / Notes|
|---|---|---|---|
|**Snov.io**|REST API (`/v1/get-profile-by-email`)|Name, company, job title, location. LinkedIn URL _may_ be included.[generect](https://generect.com/blog/apollo-enrichment-api/)|Weakest direction for Snov.io. Profile data returned but LinkedIn URL not guaranteed. Chain with Domain Search for better results.|
|**Prospeo**|Enrich API|Name, title, company, phone, location, job history, skills, firmographics (50+ data points). LinkedIn URL not a primary output.prospeo+1|Strong on general enrichment breadth. 92% match rate, ~$0.01/email, 7-day refresh.[prospeo](https://prospeo.io/s/email-enrichment-api)|
|**SalesQL Basic**|CSV Enrichment (Reverse Email Lookup)|Name, title, company, LinkedIn profile, job title, phone, company.feedback.salesql+1|CSV upload or paste list. Bulk enrichment. Returns LinkedIn URLs as a standard output.|
|**Apollo (People Match)**|REST API (`/api/v1/people/match`)|Name, title, company, LinkedIn URL, location, employment history, org data (industry, revenue, tech stack).[docs.apollo](https://docs.apollo.io/reference/people-enrichment)|Accept email as input identifier. Returns `linkedin_url` in response. Supports waterfall enrichment for broader coverage.[docs.apollo](https://docs.apollo.io/reference/people-enrichment)|
|**ProxyCurl**|Reverse Work Email Lookup Endpoint|Returns closest-match Professional Social Network profile (LinkedIn URL) for a given work email.nubela+1|designed to return closest-match LinkedIn profile. Known limitation: returns false|


Yes — there are several significant use cases that Prospeo, SalesQL, Apollo, ProxyCurl, and Lix cover that Snov.io either doesn't support or supports only weakly. Here are the additional use cases to add to the catalog:

---

## Additional Use Cases (Beyond Snov.io)

## 18. I have an email address → I want a verified mobile/direct-dial phone number

|Product|Platform|What it returns|Notes|
|---|---|---|---|
|**Prospeo**|Enrich API|Verified mobile number + email in one request. 125M+ verified mobile numbers in database.[g2](https://www.g2.com/products/prospeo-io/reviews)|One of Prospeo's key differentiators. Triple-verified phone data.|
|**Apollo**|People Enrichment (`/people/match`)|Personal phone number when `reveal_phone_number=true` + `webhook_url` provided.[dev](https://dev.to/proxycurl/i-built-a-diversity-app-to-pull-employee-composition-of-any-company-5d5)|Delivered asynchronously via webhook.|
|**SalesQL**|Reverse Email Lookup + Enrich API|Phone number as part of full contact enrichment.[nubela](https://nubela.co/blog/how-fresh-is-the-data-from-employee-listing-endpoint-or-the-search-api/)|Returned alongside name, title, company, LinkedIn.|
|**ProxyCurl**|Personal Contact Number Lookup Endpoint|Personal phone number via API.[github](https://github.com/nubelaco/proxycurl-py-linkedin-profile-scraper)|Separate endpoint, not part of reverse email.|
|**Lix**|Reverse Email Lookup API|Phone number not a standard output.[netrows](https://www.netrows.com/blog/best-linkedin-data-api-providers-2026)|—|

**Credit cost varies:** Prospeo ~$0.01/email with phone. Apollo consumes credits per waterfall source.[linkedin](https://www.linkedin.com/posts/adamandrewjeski_prospeo-v2-just-dropped-and-its-completely-activity-7428133913165905921-9boz)

---

## 19. I want to find leads who are actively researching/buying my category RIGHT NOW (intent data)

|Product|What it returns|Notes|
|---|---|---|
|**Prospeo**|Leads filtered by Bombora intent signals across 15,000 topics.prospeo+1|This is Prospeo's strongest differentiator. You can search "VP Sales at SaaS companies actively researching sales engagement tools." 7-day refresh cycle.[prospeo](https://prospeo.io/s/pipeline-generation-using-technographics-and-intent-data)|
|**Apollo**|Limited intent/growth data. Job posting signals available.[youtube](https://www.youtube.com/watch?v=qiIP7V3nbRw)|Not as rich as Prospeo. Good for hiring signals but not Bombora-level intent.|

**No other product in this set does this.** Snov.io, SalesQL, ProxyCurl, Lix — none offer intent data.

---

## 20. I want to find leads based on what technology their company uses (technographics)

|Product|What it returns|Notes|
|---|---|---|
|**Prospeo**|Technographic filters powered by Wappalyzer — filter by tech stack (e.g., "companies using HubSpot").[prospeo](https://prospeo.io/s/pipeline-generation-using-technographics-and-intent-data)|Part of the same 30+ filter system. Layer with intent + growth signals.|
|**Apollo**|Organization search includes `organization_tech_stack` filter.[apollo](https://docs.apollo.io/reference/people-api-search)|Available but less prominent than Prospeo's approach.|

**Snov.io, SalesQL, ProxyCurl, Lix** — no technographic filtering.

---

## 21. I want to find leads who recently changed jobs (job change signals)

|Product|What it returns|Notes|
|---|---|---|
|**Prospeo**|Job change signals with timeframe filters (30/60/90/180/270/365 days). Can filter for promotions only or new company only.[prospeo](https://prospeo.io/api-docs/filters-documentation)|7-day refresh. Critical for sales teams targeting people in new roles.|
|**Apollo**|Available through people search filters.[apollo](https://docs.apollo.io/reference/people-api-search)|Supported but Prospeo's implementation is more prominent.|

**Snov.io, SalesQL, ProxyCurl, Lix** — no dedicated job change signal filtering.

---

## 22. I want to find leads at companies that are growing their headcount (hiring signals)

|Product|What it returns|Notes|
|---|---|---|
|**Prospeo**|Headcount growth signals + live job posting data, all in the same search as verified contacts.[prospeo](https://prospeo.io/s/leads-filter)|Part of the 30+ filter system.|
|**Apollo**|Job Postings endpoint (`/organization-jobs-postings`) returns current job postings per company.[apollo](https://docs.apollo.io/reference/organization-jobs-postings)|Can identify companies with active hiring needs. Department-specific filtering.[youtube](https://www.youtube.com/watch?v=qiIP7V3nbRw)|
|**ProxyCurl**|Job Listings API — fetch all jobs posted by a company on LinkedIn.[dev](https://dev.to/veektor_v/get-a-linkedin-companys-jobs-listings-by-using-proxycurls-jobs-api-16m2)|Includes full job description data per posting.|

**Snov.io, SalesQL, Lix** — no hiring/growth signal filtering.

---

## 23. I have a company LinkedIn URL → I want a full scraped company profile with employee list

|Product|What it returns|Notes|
|---|---|---|
|**ProxyCurl**|Full company profile (funding, tech stack, specialities, employee count). Employee Listing Endpoint returns all current/past employees, filterable by role regex.nubela+1|Most comprehensive LinkedIn company scraping in this set. Supports enrichment per employee. Geographically limited (US, UK, Canada, Israel, Australia, Ireland, NZ, Singapore).|
|**Lix**|Organisation Enrichment: company name, industry, description, website, HQ, employee count, specialties, investment rounds, Crunchbase ID, follower count, Sales Navigator link.[lix-it](https://lix-it.com/blog/linkedin-company-data-api/)|Rich company data. Not as deep as ProxyCurl on employee lists.|
|**Apollo**|Organization Enrichment: company details + job postings.[generect](https://generect.com/blog/apollo-enrichment-api/)|Strong but not LinkedIn-scraped — database-based.|
|**SalesQL**|Limited company data via API.[salesql](https://salesql.com/api)|Not a core strength.|

**Snov.io** — no LinkedIn company scraping or employee listing capability.

---

## 24 I have a company name → I want to find the likely decision-maker for a specific role

|Product|What it returns|Notes|
|---|---|---|
|**ProxyCurl**|Role Lookup Endpoint — finds the likely decision-maker at a company for a given role title.[nubela](https://nubela.co/blog/what-is-proxycurl-api-now-in-2026-im-the-founder/)|Useful for account-based prospecting when you don't know the person's name.|
|**Prospeo**|Search API with role/seniority filters across 300M+ profiles.[prospeo](https://prospeo.io/s/lead-search-engine)|Can narrow to specific role + company.|
|**Apollo**|People Search with title + organization filters.[apollo](https://docs.apollo.io/reference/people-api-search)|Similar capability through database search.|

**Snov.io** — no role-to-person lookup. Lix — not a documented capability. SalesQL — not a core feature.

---

## 25. I have a LinkedIn person URL → I want the full scraped LinkedIn profile (experience, education, skills, publications, languages, recommendations)

|Product|What it returns|Notes|
|---|---|---|

|Product|What it returns|Notes|
|---|---|---|
|**ProxyCurl**|Person Profile Endpoint — full structured LinkedIn profile: experience history, education, languages, certifications, publications, volunteer work, skills, recommendations, connections count, follower count, people also viewed.github+1|This is ProxyCurl's core product. Deepest LinkedIn profile scraping available via API.|
|**Lix**|Profile Enrichment: name, title, company, location, industry, skills from LinkedIn.[lix-it](https://lix-it.com/blog/linkedin-scraping/)|Good but less comprehensive than ProxyCurl.|
|**Apollo**|Enrichment returns basics: name, title, company, LinkedIn URL, location, employment history.[dev](https://dev.to/proxycurl/i-built-a-diversity-app-to-pull-employee-composition-of-any-company-5d5)|Database-based, not scraped — less depth on education/skills/publications.|

**Snov.io** — no full LinkedIn profile scraping. SalesQL, Prospeo — enrich to profile data but not full scraped profile.

---

## 26. I want to search people on LinkedIn with advanced filters (country, past company, title, education)

| Product       | What it returns                                                                                                                                       | Notes                                                            |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| **ProxyCurl** | Person Search Endpoint — search with filters: country, title, past company, current company.nubela+1                                                  | Returns full enriched profiles. Max 10 per page with enrichment. |
| **Lix**       | People Search API — search LinkedIn with filters, export People data in bulk.[lix-it](https://lix-it.com/pages/linkedin-api)                          | 10,000 requests/day. Exports people, companies, jobs data.       |
| **Prospeo**   | Search API — 30+ filters including country, title, seniority, company size, intent, technographics.[prospeo](https://prospeo.io/s/lead-search-engine) | 300M+ profiles.                                                  |

---

## B2B Lead Enrichment Product Catalog — Unified Use Case Index

**Legend:** `✓` = Strong native support | `△` = Supported but limited/weaker | `—` = Not supported or no equivalent found

---

|#|Scenario: I have...|Scenario: I want to...|Snov.io|Prospeo|SalesQL Basic|Apollo (People Match)|ProxyCurl|Lix|
|---|---|---|---|---|---|---|---|---|
|1|Person's name + company domain|Get their verified email|✓|✓|✓|✓|✓|—|
|2|Spreadsheet of names + domains|Get verified emails for all|✓|✓|✓|—|—|—|
|3|Single company domain|Get all contacts + emails at that company|✓|—|—|—|—|—|
|4|List of company domains|Get prospects/emails across all of them|✓|—|—|—|—|—|
|5|Company name (no domain)|Find their website/domain|✓|✓|✓|✓|✓|—|
|6|LinkedIn profile URL|Get their email + full enriched profile|✓|✓|✓|✓|—|—|
|7|LinkedIn profile URL|Build a full CRM-ready prospect record|✓|✓|✓|✓|✓|—|
|8|Verified email address|Get full profile (name, company, LinkedIn if available)|△|✓|✓|✓|✓|✓|
|9|List of email addresses|Check which are valid/deliverable|✓|✓|✓|—|—|—|
|10|Ideal customer profile (ICP)|Discover prospects who match it|✓|✓|—|✓|—|—|
|11|LinkedIn search URL or criteria|Extract emails + enriched data from results|✓|—|—|—|—|—|
|12|Company website I'm browsing|Get all employee emails from that page|✓|—|—|—|—|—|
|13|Google search results for companies|Bulk-extract emails from all companies shown|✓|—|—|—|—|—|
|14|LinkedIn page I'm browsing|Extract all contacts on that page|✓|—|—|—|—|—|
|15|Email address + want engagement data|Track when they open/click/reply|✓|—|—|—|—|—|
|16|Verified email|Verify it won't bounce before sending|✓|✓|✓|—|—|—|
|17|Email address|Get the person's LinkedIn profile URL + company info|△|—|—|✓|✓|✓|
|18|Email address|Get a verified mobile/direct-dial phone number|—|✓|✓|✓|✓|—|
|19|—|Find leads actively researching/buying my category (intent data)|—|✓|—|—|—|—|
|20|—|Find leads based on their company's tech stack (technographics)|—|✓|—|△|—|—|
|21|—|Find leads who recently changed jobs (job change signals)|—|✓|—|△|—|—|
|22|—|Find leads at companies growing headcount (hiring signals)|—|✓|—|✓|✓|—|
|23|Company LinkedIn URL|Get full company profile + employee list from LinkedIn|—|—|—|△|✓|△|
|24|Company name|Find the likely decision-maker for a specific role|—|△|—|△|✓|—|
|25|LinkedIn person URL|Get full scraped LinkedIn profile (experience, education, skills, publications, etc.)|—|△|✓|△|✓|—|
|26|—|Search people on LinkedIn with advanced filters (country, past company, title)|—|△|—|△|✓|✓|

---

## Notes on Select Products

**Prospeo's unique strengths** (rows 19–22): Intent data (Bombora 15,000 topics), technographics (Wappalyzer), job change signals, hiring/headcount growth signals — all searchable within the same 30+ filter system as verified contacts.

**ProxyCurl's unique strengths** (rows 23–25): Deepest LinkedIn scraping available via API — person profiles, company profiles, full employee listings, job listings. Best for building tools that need raw LinkedIn data programmatically.

**Lix's unique strengths** (rows 17, 23, 25, 26): Reverse email → LinkedIn URL is a core product. People search, company search, job search, profile enrichment all via one API. 10,000 requests/day. LinkedIn-native.

**Apollo's coverage** (rows 1–8, 10, 11, 17, 18, 22): Strong on enrichment from its proprietary B2B database. Waterfall enrichment adds coverage. Less depth on LinkedIn scraping but good for email/phone/title/company enrichment at scale.

**SalesQL's coverage** (rows 1–2, 5–9, 17, 18): Focused on reverse email lookup and LinkedIn Chrome extension for quick email/phone discovery. CSV bulk enrichment. Simpler toolset but solid for the core enrichment use cases.

**Snov.io's coverage** (rows 1–16): Strong on forward enrichment (name/domain → email), domain search, Chrome extensions for passive prospecting, and email campaign infrastructure. Weak on reverse enrichment (email → profile/LinkedIn) and has no intent/technographic/hiring signal filtering.