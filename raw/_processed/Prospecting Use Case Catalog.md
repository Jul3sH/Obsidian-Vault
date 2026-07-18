
---

## Extended Prospecting Comparison: All 9 Products

## Legend

- ✓ = Strong / Native support
    
- △ = Supported but limited or indirect
    
- — = Not supported or no equivalent found
    

---

## Bucket 1: Lead Sourcing (Web/Social Capture)

|#|Use Case|Snov.io|Apollo|Clay|HubSpot|Prospeo|SalesQL|ProxyCurl|Lix|
|---|---|---|---|---|---|---|---|---|---|
|1|LinkedIn lead capture (extension or native)|✓ — LI Prospect Finder extension|✓ — Chrome extension|△ — via CSV/URL import + enrichment|△ — Prospecting Agent uses LinkedIn data indirectly|△ — no dedicated extension, but API can enrich LinkedIn URLs|✓ — core product: Chrome extension extracts from LinkedIn + Sales Navigator|△ — API returns LinkedIn profile data from LinkedIn URLs, no browser extension|✓ — Chrome extension exports LinkedIn search results to CSV/Excel with enriched data|
|2|Web page / Google results lead capture|✓ — Email Finder extension|✓ — Chrome extension|✓ — Claygent AI agent scrapes any web page|—|△ — API-based, not browser capture|—|✓ — scrapes full LinkedIn profiles from any LinkedIn URL via API|—|
|3|Browser extension for on-the-fly prospect capture|✓ — Email Finder + Email Tracker extensions|✓ — Prospecting + Gmail + Salesforce extensions|△ — Claygent runs in-browser as table action|—|✓ — Chrome extension (40+ data points per contact, verified email + mobile)|✓ — Chrome extension (1-click extraction from LinkedIn)|—|✓ — Chrome extension (export LinkedIn to CSV/Excel)|
|4|Gmail contact sync to prospect records|✓ — Prospect sync from Gmail|✓ — Gmail extension included|—|△ — native Gmail-CRM integration|—|—|—|—|
|5|Lead capture from website visitors (inbound)|—|✓ — Inbound add-on: Website Visitors, up to 50K companies/month|—|✓ — Enterprise: website visitor tracking|—|—|—|—|
|6|Reverse email → LinkedIn URL lookup|△ — indirect via domain search|△ — enrichment can return LinkedIn URL|✓ — via enrichment providers|△ — via Breeze Intelligence enrichment|△ — reverse person search available via API|✓ — core use case: reverse email lookup returns name, title, company, LinkedIn|✓ — Reverse Work Email Lookup endpoint returns LinkedIn URL|✓ — Reverse email lookup returns LinkedIn URL as core output|

---

## Bucket 2: Bulk Lead Lookup (Structured Data → Emails/Contacts)

|#|Use Case|Snov.io|Apollo|Clay|HubSpot|Prospeo|SalesQL|ProxyCurl|Lix|
|---|---|---|---|---|---|---|---|---|---|
|7|Single email search (name → email)|✓ — Email Search|✓ — credit-based email credits|✓ — via 150+ data providers|△ — Breeze Intelligence (credit-based)|✓ — core product: 98% accuracy, proprietary infrastructure|✓ — works on LinkedIn + Sales Navigator|— — no email finding; LinkedIn profile scraping only|△ — Email Finder included in credits, but secondary to export|
|8|Bulk email search (spreadsheet names/domains → emails)|✓ — Bulk Email Search, Bulk Domain Search|✓ — CSV import/export, up to 10K record selection|✓ — CSV upload into tables, multi-provider waterfall|△ — enrich segment (max 100/batch)|✓ — bulk list upload with verification + phone lookup|✓ — CSV Enrichment: upload names + company info or LinkedIn URLs|— — no email finding|△ — batch export from LinkedIn searches via extension|
|9|Domain search (one domain → all employee emails)|✓ — Domain Search|✓ — advanced filters + company search|✓ — via enrichment providers|—|✓ — company domain search returns contacts|—|△ — can get employee listing from a company LinkedIn page|—|
|10|Phone number enrichment|—|✓ — 8 credits per verified phone|✓ — Launch plan includes phone enrichment|✓ — Breeze Intelligence adds direct dials|✓ — 125M+ verified mobile numbers, triple-verified|—|✓ — personal contact number lookup endpoint|△ — not a standard output|
|11|CRM/API data enrichment (upload list → enrich)|✓ — Email Finder API, Data Enrichment API|✓ — CSV, CRM & API Data Enrichment + Waterfall|✓ — 150+ providers, API-native, bring your own keys|✓ — Breeze Intelligence, API, native CRM|✓ — Enrich Person API (real-time), Enrich Company API|✓ — CSV Enrichment, Enrich API, CRM push (Salesforce, HubSpot, Pipedrive)|✓ — Person Profile API, Company Profile API, search API|✓ — Realtime API (LinkedIn profile data, org data)|
|12|Skip previously saved / dedup|✓ — Skip saved feature|△ — CRM handles dedup|✓ — exclude companies/people from search on Launch+|✓ — native CRM dedup|—|—|—|—|
|13|Multi-provider waterfall (try A, B, C until match)|—|✓ — Waterfall Enrichment|✓ — foundational feature across all plans|—|—|—|—|—|
|14|Bulk enrichment (enrich 10K+ rows in one go)|✓ — Bulk Domain Search + API|✓ — up to 10,000 record selection (Org plan)|✓ — Enterprise: unlimited rows, bulk enrichment|Limited — 100/batch|—|△ — CSV enrichment handles lists|✓ — batch profile enrichment via API|—|

---

## Bucket 3: Account Intelligence (Company Research, ICP, Enrichment, Signals)

|#|Use Case|Snov.io|Apollo|Clay|HubSpot|Prospeo|SalesQL|ProxyCurl|Lix|
|---|---|---|---|---|---|---|---|---|---|
|15|Database search by ICP filters (title, industry, revenue, size, location)|✓ — Database Search, 50M+ profiles, ICP filters|✓ — 65+ filters, intent topics, advanced filters|✓ — 150+ providers, granular filters, custom data|△ — lead scoring + custom properties, Prospecting Agent uses ICP|✓ — Person Search API: 30+ filters (country, title, seniority, company size, intent, technographics), 300M+ profiles|✓ — AI-powered search: describe profile, AI generates matching leads; B2B database 200M+ contacts|✓ — Person Search + Company Search endpoints with filters; returns full enriched profiles|✓ — People API, Companies API, Jobs API; filter by industry, location, company size|
|16|Company/firmographic database access|✓ — 50M+ company profiles|✓ — proprietary database|✓ — 150+ providers aggregated|✓ — Breeze Intelligence (Clearbit-powered)|✓ — company data via API search|△ — basic company info via LinkedIn|✓ — Company Profile API: size, industry, funding, employees, tech stack, org charts|✓ — Companies API: industry, locations, logos, size|
|17|Intent / buying signals (company news, funding, tech changes)|—|✓ — Intent Topics & Intent Filters (6–12 topics)|✓ — Job changes, promotions, new hires, company news, social, web intent, automated via webhooks|✓ — Prospecting Agent monitors funding, job postings, tech changes, website visits, email opens|—|—|△ — indirect via profile data freshness, LinkedIn company updates|△ — job search data shows hiring signals|
|18|People & company lookalikes|—|✓ — People & Company Lookalikes (BETA)|△ — can build via custom filters in tables|—|—|—|—|—|
|19|CRM-based enrichment (sync + auto-enrich CRM records)|—|✓ — CRM sync + enrich on import|✓ — Growth plan: auto-sync and enrich CRM|✓ — native CRM, Breeze auto-enriches records|△ — via API integration|✓ — push leads to Salesforce, HubSpot, Pipedrive; batch enrich|—|—|
|20|AI-powered prospect research (autonomous)|—|✓ — AI Research, AI Filter, AI Lead Scoring|✓ — Claygent AI agent for custom web research|✓ — Prospecting Agent (Breeze AI): autonomous research + email generation|△ — API-based search, not autonomous agent|✓ — AI-powered search: describe profile → AI finds leads|—|—|
|21|Lead scoring / prioritization|—|✓ — AI Lead Scoring|△ — via signals + custom formulas in tables|✓ — Rules-based (Pro) + Predictive (Enterprise, AI)|—|—|—|—|
|22|Bulk enrichment (enrich 10K+ rows in one go)|✓ — Bulk Domain Search + API|✓ — up to 10,000 selection (Org)|✓ — Enterprise: unlimited rows with Audiences|Limited — 100/batch|—|△ — CSV enrichment|✓ — batch API|△ — bulk export from searches|
|23|Full LinkedIn profile scraping (education, skills, publications)|—|△ — enrichment basics only|—|—|—|△ — via LinkedIn extension|✓ — deepest LinkedIn profile scraping: employment, education, skills, interests, certifications, publications, languages|△ — profile data but less depth than ProxyCurl|
|24|Company → all employee listing|—|✓ — via company page view in extension|—|—|—|—|✓ — Employee Listing API returns all employees for a company|△ — Companies API returns org info but not full employee roster|
|25|Technographic data (tech stack detection)|—|✓ — tech stack filter|✓ — via enrichment providers|△ — via enrichment|—|—|△ — limited tech data in company profiles|—|
|26|Hiring signals (job postings, headcount growth)|—|✓ — intent signals cover hiring|✓ — track job changes, new hires via signals|△ — job postings detected by Prospecting Agent|✓ — search API includes hiring signals|△ — job posting data available|✓ — job postings retrieval via API|✓ — Jobs API returns LinkedIn job postings|

---

## Summary by Product (Prospecting Strength by Bucket)

|Product|Lead Sourcing|Bulk Lead Lookup|Account Intelligence|
|---|---|---|---|
|**Snov.io**|Strong — extensions for LinkedIn + web + Gmail sync|Strong — bulk email/domain search, API, 50M+ profiles|Weak — has company database and ICP filters, but no intent signals, AI research, lead scoring|
|**Apollo**|Moderate — Chrome extension, inbound visitor tracking|Strong — credits-based bulk lookup, waterfall enrichment, CSV/CRM/API|Strong — intent signals, AI research, lookalikes, lead scoring, multi-source waterfall|
|**Clay**|Moderate — Claygent web scraping, no social extensions|Very Strong — 150+ data providers, waterfall, any structured data, tables|Very Strong — signals, custom data, webhook automation, AI agent, unlimited flexibility|
|**HubSpot**|Weak — no social/web capture extensions; relies on inbound + CRM|Moderate — native CRM enrichment, Prospecting Agent research, 100-record batch limit|Strong — Breeze Intelligence, Prospecting Agent, predictive scoring, signal monitoring, native CRM context|
|**Prospeo**|Moderate — Chrome extension (40+ data points), API-based search|Strong — bulk email search with verification, phone lookup, API enrichment|Moderate — 300M+ profiles, 30+ search filters, intent and technographic signals, but no autonomous AI or lookalikes|
|**SalesQL**|Strong — core LinkedIn Chrome extension, Sales Navigator support|Moderate — CSV enrichment, CRM push, LinkedIn URL bulk enrichment|Moderate — AI-powered search for lead discovery, 200M+ contacts, but weak on signals and company intelligence|
|**ProxyCurl**|Weak — API-only, no browser extension|Moderate — batch API enrichment, employee listing, LinkedIn URL input|Moderate — full LinkedIn profile scraping, company profiles with funding/tech stack, search endpoints, but no intent signals or AI|
|**Lix**|Strong — LinkedIn Chrome extension (export search to CSV with enriched emails)|Moderate — bulk export from LinkedIn searches, email credits, realtime API|Moderate — People/Companies/Jobs APIs with filters, hiring signals via Jobs API, org data, but limited compared to Clay/Apollo|

---

## Caveats: Data Sources and Accuracy

|Product|Source Type|Details|
|---|---|---|

|Product|Source Type|Details|
|---|---|---|
|**Snov.io**|**Browser — direct from pricing page**|All features read directly from `snov.io/pricing`. Accurate and current.|
|**Apollo.io**|**Browser — direct from pricing page**|All features read directly from `apollo.io/pricing`. Credit details and tiers are from the live page.|
|**Clay**|**Browser — direct from pricing page**|All features read directly from `clay.com/pricing`. Provider count and plan limits are from the live page.|
|**HubSpot**|**Mixed — browser + web search**|HubSpot's pricing page does not show detailed prospecting features. Features were gathered from the HubSpot prospecting product page, HubSpot Knowledge Base, Spring 2026 Spotlight announcement, and reputable third-party HubSpot analysis sites. Data is accurate but some granular detail (e.g., exact enrichment batch limits, credit costs) is inferred from public analysis.|
|**Prospeo**|**Web search only**|Did not open the manual pricing page. All Prospeo features (98% accuracy, 300M+ profiles, 125M+ mobile numbers, Chrome extension, bulk processing, Person/Company Search API, technographic + intent signals, reverse person search) were gathered from Prospeo's own marketing pages and third-party reviews found via web search. Prospeo's own guides explicitly describe these capabilities. May not reflect latest pricing changes.|
|**SalesQL**|**Web search only**|Did not open the manual pricing page. Features (LinkedIn + Sales Navigator Chrome extension, CSV enrichment, AI-powered search, 200M+ contacts, CRM push, reverse email lookup, phone numbers) were gathered from SalesQL's website, third-party reviews (SalesForge, GetApp, SyncGTM), and their features marketing pages. SalesQL positions as LinkedIn-first, which is accurately reflected.|
|**ProxyCurl**|**Web search only**|Did not open the manual pricing page. Features (Person Profile API, Company Profile API, Search endpoints, Employee Listing API, Job Postings API, LinkedIn profile scraping with education/skills/publications, personal contact number lookup, reverse email lookup) were gathered from ProxyCurl's own blog, YouTube demo, and third-party comparison sites (NinjaPear, Conversion Gems, Slashdot). ProxyCurl is API-only with no browser extension — this is accurate.|
|**Lix**|**Web search only**|Did not open the manual pricing page. Features (LinkedIn Chrome extension, CSV/Excel export, 98% email validation, People/Companies/Jobs APIs, realtime org data, hiring signals, 10K leads/day export) were gathered from Lix's pricing page via search, Software Advice, Capterra, and third-party reviews (Puzzle Inbox, ColdIQ, Derrick comparison). Lix is LinkedIn-native and extension-first — this is accurate.|
|**"Basic Proxy" / "Curl"**|**Not applicable — no such products**|There is no prospecting tool called "Basic Proxy" or "Curl." In our previous catalog, you had **ProxyCurl** (nubela.co) — this is the tool. "Basic Proxy" appeared as a pricing tier name in HasData's documentation[prospeo](https://prospeo.io/s/hasdata-pricing-reviews-pros-and-cons), and "curl" is the HTTP command-line utility used in API examples[nubela](https://nubela.co/blog/best-data-enrichment-tools/). I treated ProxyCurl as the product you meant.|

**Key takeaway on accuracy:** Snov.io, Apollo, and Clay are the most reliable (direct from live pricing pages). Prospeo, SalesQL, ProxyCurl, and Lix were all sourced from web search (marketing pages, third-party reviews, and blog posts) — their features are accurately described but pricing and plan limits may have changed since the sources were published. HubSpot