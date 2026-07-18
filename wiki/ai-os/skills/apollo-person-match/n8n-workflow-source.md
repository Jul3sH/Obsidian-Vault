# Apollo Person Match — N8N Workflow Source

tags: [technical, apollo-person-match, n8n, source, workflow]

> *Original N8N workflow ("Lead 1") used as reference when building the Apollo Person Match skill. Preserved here for future reference.*

---

## Workflow Overview

**Name:** Lead 1
**ID:** Dbzu6lmK6zWsyyQP
**Status:** Inactive (reference only)

This N8N workflow is the original automated lead generation and enrichment pipeline. It covers all three enrichment stages in a single workflow. Our Python skill reimplements the relevant parts as standalone scripts.

---

## Key Architectural Observations

| Finding | Detail |
|---------|--------|
| Apollo endpoint used | `/api/v1/mixed_people/search` — searches by job title + location |
| Apollo returns | `linkedin_url` (full URL), `id`, `name`, `title` |
| Email retrieval | Second Apollo call to `/api/v1/people/match` using `apollo_id` |
| LinkedIn username extraction | GPT-3.5-turbo strips `https://www.linkedin.com/in/` from `linkedin_url` |
| LinkedIn scraper input | `linkedin_username` (not `linkedin_url`) — passed to RapidAPI |
| Email validation | Separate API: `api.mails.so/v1/validate` |

**Critical insight:** Apollo does NOT return a LinkedIn user ID — it returns the full `linkedin_url`. The username is extracted by stripping the URL prefix. Our Python skill handles this with simple string manipulation, no AI call needed.

---

## Workflow Stages (4 sub-workflows in one file)

### Stage 1: Lead Generation
```
Form submission (Job Title + Location + Number of Leads)
  → Apollo /mixed_people/search
  → Split Out (one item per person)
  → Clean Data (id, name, linkedin_url, title, organization)
  → Add Leads to Google Sheet (all statuses set to "pending")
```

### Stage 2: LinkedIn Username Extraction
```
Google Sheets Trigger (row added)
  → Get Pending Username Row (filter: extract_username_status = "pending")
  → OpenAI GPT-3.5: strip "https://www.linkedin.com/in/" from linkedin_url
  → Add Linkedin Username (write linkedin_username + set status = "finished")
```

### Stage 3: Email Retrieval + Validation
```
Google Sheets Trigger (row added)
  → Get Pending Email Statuses (filter: contacts_scrape_status = "pending")
  → Get Email from Apollo (POST /people/match with apollo_id)
  → Confirm Email Validity (api.mails.so validate)
  → If valid: Add Email Address + set contacts_scrape_status = "finished"
  → If invalid: Mark Invalid Email + set contacts_scrape_status = "invalid_email"
```

### Stage 4: LinkedIn Profile + Posts Enrichment
```
Google Sheets Trigger (row added)
  → Get Pending About and Posts Rows (filter: profile_summary_scrape = "pending")
  → Get About Profile (RapidAPI linkedin-data-api.p.rapidapi.com, param: username)
  → Clean Profile Data (JS: extract headline, education, position, etc.)
  → Stringify + AI Profile Summarizer (GPT-3.5)
  → Update Profile Summary (write to sheet, status = "completed")

Google Sheets Trigger (row added)
  → Get Pending About and Posts Rows (filter: posts_scrape_status = "unscraped")
  → Get Profile Posts (RapidAPI, param: username, start: 0)
  → Clean Posts Data (JS: extract post_1, post_2, post_3 + dates)
  → Stringify + Posts AI Summarizer (GPT-3.5)
  → Update Posts Summary (write to sheet, status = "scraped")

Google Sheets Trigger (row added)
  → Get Completely Enriched Profiles (filter: all 3 statuses complete)
  → Append to Enriched Leads Database (separate Sheet)
```

### Stage 5: Scheduled Retry (every 4 weeks)
```
Schedule Trigger → Reset "failed" profile_summary_scrape rows → back to "pending"
Schedule Trigger → Reset "failed" posts_scrape_status rows → back to "unscraped"
Schedule Trigger → Reset "invalid_email" contacts_scrape_status rows → back to "pending"
```

---

## Google Sheets Schema (from workflow)

| Column | Type | Set by |
|--------|------|--------|
| `apollo_id` | string | Stage 1 — Apollo search |
| `name` | string | Stage 1 — Apollo search |
| `organization` | string | Stage 1 — Apollo search |
| `title` | string | Stage 1 — Apollo search |
| `linkedin_url` | string | Stage 1 — Apollo search |
| `linkedin_username` | string | Stage 2 — OpenAI URL strip |
| `extract_username_status` | string | Stage 2 — pending → finished |
| `email_address` | string | Stage 3 — Apollo people/match |
| `contacts_scrape_status` | string | Stage 3 — pending → finished / invalid_email |
| `about_linkedin_profile` | string | Stage 4 — RapidAPI + GPT-3.5 |
| `profile_summary_scrape` | string | Stage 4 — pending → completed / failed |
| `recent_posts_summary` | string | Stage 4 — RapidAPI + GPT-3.5 |
| `posts_scrape_status` | string | Stage 4 — unscraped → scraped / failed |

---

## Apollo API Calls in This Workflow

### Call 1: Search for Leads
```
POST https://api.apollo.io/api/v1/mixed_people/search
Headers: x-api-key, Cache-Control: no-cache, accept: application/json
Body:
{
  "person_locations": ["{{ Location }}"],
  "person_titles": ["{{ Job Title }}"],
  "page": 1,
  "per_page": {{ Number of Leads }},
  "projection": ["id", "name", "linkedin_url", "title"]
}
```

### Call 2: Get Email by Apollo ID
```
POST https://api.apollo.io/api/v1/people/match
Headers: x-api-key, Cache-Control: no-cache, accept: application/json
Body: { "id": "{{ apollo_id }}" }
Query: reveal_personal_emails=true, reveal_phone_number=false
```

---

## Differences vs Our Python Skill

| Aspect | N8N Workflow | Our Python Skill |
|--------|-------------|-----------------|
| Lead source | Apollo search (title + location) | Apollo match (name + email from Sheet) |
| Apollo endpoint | `/mixed_people/search` | `/people/match` |
| Username extraction | GPT-3.5 (overkill) | Python string strip — `linkedin_url.split('/in/')[-1].strip('/')` |
| AI summarization | OpenAI GPT-3.5 | Anthropic Claude Haiku |
| Orchestration | N8N visual workflow | Python scripts on local Mac |
| Trigger | Form submission / Sheets trigger | Manual run / cron |

---

## Raw JSON

```json
{
  "id": "Dbzu6lmK6zWsyyQP",
  "meta": {
    "instanceId": "2cff59bc4079733bed2846cef09ebd74d667b91742f344a1b849c8c2f8c8dd5a",
    "templateCredsSetupCompleted": true
  },
  "name": "Lead 1",
  "tags": [],
  "nodes": [
    {
      "id": "4cab7c48-1c69-479e-83ce-fe4d3974b5ce",
      "name": "On form submission",
      "type": "n8n-nodes-base.formTrigger",
      "position": [220, 140],
      "webhookId": "28ff6927-5d05-4182-910b-be2381e3b2c4",
      "parameters": {
        "options": {},
        "formTitle": "Leads Search",
        "formFields": {
          "values": [
            {"fieldLabel": "Job Title", "requiredField": true},
            {"fieldLabel": "Location", "requiredField": true},
            {"fieldType": "number", "fieldLabel": "Number of Leads", "requiredField": true}
          ]
        }
      },
      "typeVersion": 2.2
    },
    {
      "id": "e6a3abf6-bb85-4b7e-9498-5490d1d9a3b4",
      "name": "Generate Leads with Apollo.io1",
      "type": "n8n-nodes-base.httpRequest",
      "position": [460, 140],
      "parameters": {
        "url": "https://api.apollo.io/api/v1/mixed_people/search",
        "method": "POST",
        "jsonBody": "{\n  \"person_locations\": [\"{{ $json.Location }}\"],\n  \"person_titles\": [\"{{ $json['Job Title'] }}\"],\n  \"page\": 1,\n  \"per_page\": {{$json['Number of Leads']}},\n  \"projection\": [\"id\", \"name\", \"linkedin_url\", \"title\"]\n}",
        "sendBody": true,
        "sendHeaders": true,
        "specifyBody": "json",
        "headerParameters": {
          "parameters": [
            {"name": "Cache-Control", "value": "no-cache"},
            {"name": "accept", "value": "application/json"},
            {"name": "x-api-key", "value": "\"your-api_key_here\""}
          ]
        }
      },
      "typeVersion": 4.2
    },
    {
      "id": "6851151e-6b2a-42b7-8e0a-729c650da6c4",
      "name": "OpenAI1",
      "type": "@n8n/n8n-nodes-langchain.openAi",
      "position": [740, 380],
      "parameters": {
        "modelId": {"value": "gpt-3.5-turbo"},
        "messages": {
          "values": [
            {"content": "=remove the http or https://www.linkedin.com/in/ from this  {{ $json.linkedin_url }}"}
          ]
        }
      },
      "typeVersion": 1.8
    },
    {
      "id": "ed3b325d-80a5-491a-9f1d-165df1d5b0ec",
      "name": "Get Email from Apollo11",
      "type": "n8n-nodes-base.httpRequest",
      "position": [480, 580],
      "parameters": {
        "url": "https://api.apollo.io/api/v1/people/match",
        "method": "POST",
        "bodyParameters": {
          "parameters": [{"name": "id", "value": "={{ $json.apollo_id }}"}]
        },
        "queryParameters": {
          "parameters": [
            {"name": "reveal_personal_emails", "value": "true"},
            {"name": "reveal_phone_number", "value": "false"}
          ]
        },
        "headerParameters": {
          "parameters": [
            {"name": "Cache-Control", "value": "no-cache"},
            {"name": "accept", "value": "application/json"},
            {"name": "x-api-key", "value": "\"your_api_key\""}
          ]
        }
      },
      "typeVersion": 4.2
    },
    {
      "id": "102398c4-8760-4cc7-8664-293b5de3c460",
      "name": "Get About Profile",
      "type": "n8n-nodes-base.httpRequest",
      "position": [760, 1060],
      "parameters": {
        "url": "https://linkedin-data-api.p.rapidapi.com",
        "queryParameters": {
          "parameters": [{"name": "username", "value": "={{ $json.linkedin_username }}"}]
        },
        "headerParameters": {
          "parameters": [
            {"name": "x-rapidapi-host", "value": "linkedin-data-api.p.rapidapi.com"},
            {"name": "x-rapidapi-key", "value": "faf88fbfc9msh9af1ccc8b3e2f05p11283cjsnc5302b552c5e"}
          ]
        }
      },
      "typeVersion": 4.2
    },
    {
      "id": "f00b7fe0-1bb8-44b9-b19e-cca7576bd7fe",
      "name": "Get Profile Posts",
      "type": "n8n-nodes-base.httpRequest",
      "position": [640, 1900],
      "parameters": {
        "url": "https://linkedin-data-api.p.rapidapi.com/get-profile-posts",
        "queryParameters": {
          "parameters": [
            {"name": "username", "value": "={{ $json.linkedin_username }}"},
            {"name": "start", "value": "0"}
          ]
        },
        "headerParameters": {
          "parameters": [
            {"name": "x-rapidapi-host", "value": "linkedin-data-api.p.rapidapi.com"},
            {"name": "x-rapidapi-key", "value": "faf88fbfc9msh9af1ccc8b3e2f05p11283cjsnc5302b552c5e"}
          ]
        }
      },
      "typeVersion": 4.2
    }
  ]
}
```

*(Full JSON preserved in conversation history. Only key nodes included above for readability.)*
