# Apollo Person Match — Architecture & Data Flow

tags: [technical, skills, apollo-person-match, architecture, api]

> *Step 1 of the lead enrichment pipeline. Takes Google Sheet rows with name + email, calls Apollo people/match API, and writes back LinkedIn URL, job title, company, and phone numbers.*

---

## Pipeline Position

```
[Step 1: Apollo Match]  ←→  [Step 2: LinkedIn Enrichment]  ←→  [Step 3: Posts Enrichment]
  This skill              (reads linkedin_url output)        (reads linkedin_username)
  Inputs: name + email                                       (enriches profiles/posts)
  Outputs: linkedin_url, title, company, phone
```

The `linkedin_url` populated here is critical — Step 2 depends on it to extract the LinkedIn username for profile scraping.

---

## Architecture Overview

```
┌─ LOCAL MAC (Hong Kong) ──────────────────────────────┐
│                                                       │
│  ┌──────────────────────────────────────────────┐   │
│  │ Credential Loading (Startup)                 │   │
│  ├──────────────────────────────────────────────┤   │
│  │ ~/.leadgen/credentials.json                  │   │
│  │    ↓ (Read JSON file)                        │   │
│  │ credentials.py → CredentialManager.load()   │   │
│  │    ↓ (Check required keys)                   │   │
│  │ os.environ                                   │   │
│  │    APOLLO_API_KEY                            │   │
│  │    GOOGLE_SERVICE_ACCOUNT_JSON               │   │
│  │    SHEETS_AUTH_METHOD                        │   │
│  └──────────────────────────────────────────────┘   │
│                     ↓                                │
│  ┌──────────────────────────────────────────────┐   │
│  │ Python Script: apollo_person_match.py        │   │
│  ├──────────────────────────────────────────────┤   │
│  │ 1. Read Google Sheets (pending rows)         │   │
│  │ 2. For each row:                             │   │
│  │    - Extract name + email                    │   │
│  │    - Call Apollo /people/match               │   │
│  │    - Parse response (LinkedIn URL, etc.)     │   │
│  │    - Write back to Sheets with status       │   │
│  │ 3. Log results                               │   │
│  │                                              │   │
│  │ Modes: --mode run (default)                  │   │
│  │        --mode stats                          │   │
│  │        --mode reset-failed                   │   │
│  │        --batch-size N (default 10)           │   │
│  └──────────────────────────────────────────────┘   │
│         ↓              ↓              ↓              │
│      [Read]         [Match]        [Write]         │
│                                                    │
└────────────────────────────────────────────────────┘
         ↓                              ↓
┌─ GOOGLE CLOUD ─────────┐  ┌──────────────────────┐
│ Google Sheets API      │  │ Apollo API (Direct)  │
│ sheets.googleapis.com  │  │ api.apollo.io        │
│ (Direct HK traffic OK) │  │ POST /api/v1/people/ │
│                        │  │      people/match    │
│ Service Account JWT    │  │                      │
│ Gets pending rows      │  │ x-api-key header     │
│ Updates status + data  │  │ 1 credit per call    │
└────────────────────────┘  └──────────────────────┘
```

---

## Data Flow: Name + Email → Apollo Match → Sheets Update

```
INPUT ROW (from Sheet)
├─ name: "Julian Hart"
├─ email_address: "julianhart@gmail.com"
└─ match_status: "pending"
        ↓
  API CALL (Apollo /people/match)
  ├─ Request body:
  │  {
  │    "name": "Julian Hart",
  │    "email": "julianhart@gmail.com",
  │    "reveal_personal_emails": false,
  │    "reveal_phone_number": false
  │  }
  │
  │ Cost: 1 Apollo credit
  │ Rate: 0.5s sleep between calls
  │ Backoff: 60s on HTTP 429
  │
  └─ Response: person object (if match found)
        ↓
  PARSE RESPONSE
  ├─ person.first_name → first_name
  ├─ person.last_name → last_name
  ├─ person.title → title
  ├─ person.email → email_address (verify)
  ├─ person.linkedin_url → linkedin_url ⭐ (Step 2 needs this)
  ├─ person.organization.name → organization
  ├─ person.organization.website_url → company_website
  ├─ person.organization.phone → corporate_phone
  └─ person.mobile_phone → mobile_phone
        ↓
  WRITE TO SHEET
  ├─ If linkedin_url found:
  │  └─ match_status: "matched"
  ├─ If person found but no linkedin_url:
  │  └─ match_status: "no_linkedin"
  └─ If no match:
     └─ match_status: "failed"
```

---

## Match Rate & Success Metrics

**Expected Match Rates (Apollo documentation):**
- Name + email together: 80-90% match rate
- LinkedIn URL in response: 60-70% of matched records
- Phone numbers: Varies by data availability

**Status Distribution (typical run):**
- `matched` (has LinkedIn URL): ~55-65%
- `no_linkedin` (found but no URL): ~15-25%
- `failed` (no match): ~10-20%

**Cost per batch:**
- 10 leads = 10 Apollo credits
- 100 leads = 100 credits
- Monthly budget: monitor quota at apollo.io dashboard

---

## Credential & Auth Flow

```
Startup
├─ CredentialManager.load(required=["APOLLO_API_KEY", "SHEETS_AUTH_METHOD", ...])
│
├─ Check os.environ first (allows shell override: export APOLLO_API_KEY=...)
├─ Check ~/.leadgen/credentials.json
├─ Prompt user if missing (first-time setup)
│
└─ os.environ now contains:
   ├─ APOLLO_API_KEY → x-api-key header for Apollo calls
   └─ GOOGLE_SERVICE_ACCOUNT_JSON → JWT for Sheets API

Each API call:
├─ Apollo: headers = {"x-api-key": os.environ["APOLLO_API_KEY"]}
└─ Sheets: gspread reads GOOGLE_SERVICE_ACCOUNT_JSON path → generates Bearer token
```

---

## VPN Routing Assessment

| Service | Block in HK? | Route | Reason |
|---------|-------------|-------|--------|
| Apollo API | No ✓ | Direct | No known HK blocks; publicly accessible |
| Google Sheets | No ✓ | Direct | Google tolerates HK direct traffic |
| Anthropic API (Step 2) | Yes ✗ | Through VPN | 160.79.104.0/21 blocked in HK |

**Implication:** Apollo Person Match runs with **no VPN needed**. VPN only becomes relevant in Step 2 (LinkedIn enrichment) when calling Anthropic API for summarization.

---

## Error Handling & Retry Strategy

| Error | Cause | Handling |
|-------|-------|----------|
| HTTP 401 | Invalid/expired Apollo key | Check credentials.json, rotate key if needed |
| HTTP 403 | Rate limiting or auth failure | 60s backoff, then retry |
| HTTP 429 | Rate limit hit | Sleep 0.5s + exponential backoff (60s) |
| No match returned | Person not in Apollo DB | Write `failed` status, move to next row |
| LinkedIn URL missing | Match found but no LinkedIn | Write `no_linkedin` status |
| Google Sheets quota | Too many API requests | Reduce batch size, add delay between writes |

---

## File Structure

```
~/Downloads/apollo-person-match/scripts/
├── apollo_person_match.py      ← Main orchestrator
│   ├─ Reads pending rows from Sheets
│   ├─ Calls Apollo /people/match
│   ├─ Parses response
│   └─ Writes results back to Sheets
│
├── gsheets_store.py            ← Google Sheets I/O (shared copy)
│   ├─ get_pending_rows()
│   ├─ update_row()
│   └─ write_status()
│
└── credentials.py              ← Credential manager (shared copy)
    ├─ CredentialManager.load()
    ├─ CredentialManager.rotate()
    └─ ~/.leadgen/credentials.json loader
```

---

## Comparison: Apollo vs LinkedIn Enrichment

| Aspect | Apollo (Step 1) | LinkedIn (Step 2) |
|--------|-----------------|------------------|
| Input | name + email | linkedin_username |
| API calls | 1 per lead | 4 per lead (profile, exp, edu, posts) |
| Cost | 1 Apollo credit | 4 RapidAPI credits + Anthropic cost |
| Match rate | 80-90% | 100% (if username valid) |
| Response fields | ~10 | ~50+ nested |
| VPN needed | No | Yes (Anthropic) |
| Processing time | ~10s per lead | ~20-30s per lead |
| Error recovery | Retry failed rows | Manual re-queuing |

---

## Notes

- **HTTP library:** Currently uses `urllib`. May switch to `requests` if 403 errors occur (same issue seen in linkedin-enrichment).
- **Batch size:** Default 10 rows per run (each = 1 credit). Adjust via `--batch-size N`.
- **Sleep between calls:** 0.5s to respect Apollo rate limits.
- **Step 2 dependency:** LinkedIn enrichment expects `linkedin_url` field populated here.
