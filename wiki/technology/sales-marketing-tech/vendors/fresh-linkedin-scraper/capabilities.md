---
vendor: Fresh LinkedIn Scraper API (by SaleLeads, RapidAPI)
last-verified: 2026-05-07
source: https://rapidapi.com/saleleadsdotai-saleleadsdotai-default/api/fresh-linkedin-scraper-api (verified directly by user, 2026-05-07)
---

# Fresh LinkedIn Scraper API — Capability Profile

> ✅ **Verified 2026-05-07:** All claims below confirmed against the live RapidAPI page for the subscribed API (`saleleadsdotai-saleleadsdotai-default/api/fresh-linkedin-scraper-api`). Previous audit flags from an earlier session (which reviewed a different product — `fresh-linkedin-profile-data`) are retracted and replaced by this entry.

---

## Use Case Coverage

| Use Case | Rating | Notes |
|----------|--------|-------|
| [[prospecting]] | △ | Returns profile data only — does not find or verify email addresses; no search/filtering for lead generation |
| [[email-verification]] | — | Not applicable |
| [[email-warmup]] | — | Not applicable |
| [[personalisation]] | ✓ | Returns profile summary, work history, education, skills, certifications, posts, and much more — full data for AI-generated icebreakers |
| [[campaign-sequence]] | — | Not applicable |
| [[inbox-reply-management]] | — | Not applicable |

## Vendor Type
Point solution: LinkedIn profile scraping API via RapidAPI (by SaleLeads). Sits upstream of personalisation — provides raw profile data that feeds an AI icebreaker step.

---

## Active Endpoints Used by the Enrichment Script

> All 4 confirmed via RapidAPI playground, 2026-05-07.

| Endpoint | Requests | Parameter | Data returned |
|----------|----------|-----------|---------------|
| `GET /api/v1/user/profile` | 1 | `username` | Headline, about, location, follower count, connection count, current company |
| `GET /api/v1/user/experience` | 1 | `urn` (from profile) | Job history: title, company, dates, description |
| `GET /api/v1/user/educations` | 1 | `urn` (from profile) | School, degree, field of study, years |
| `GET /api/v1/user/posts` | 1 | `urn` (from profile) | Recent post content and engagement |

**Confirmed:** Every endpoint returns `"cost": 1` in the response body.
**Terminology:** The API uses **"requests"** (not "credits") — each call deducts 1 from the monthly request quota.

### ⚠️ Parameter dependency
`/profile` takes `username`. The other 3 endpoints require `urn` (the LinkedIn internal user ID), which is only available in the `/profile` response. The script must call `/profile` first and extract the `urn` before calling `/experience`, `/educations`, or `/posts`.

### ⚠️ Optional include flags on `/profile` (extra cost)
The `/profile` endpoint has optional flags: `include_experiences`, `include_skills`, `include_certifications`, `include_publications`, `include_follower_and_connection_count`. Each enabled flag costs **+1 request** on top of the base 1 request. The current script does not use these flags — it calls separate endpoints for experiences and educations instead.

**Input required:** LinkedIn username (for `/profile`), then `urn` extracted from the profile response for subsequent calls.
**Total cost per contact (current script):** 4 requests

---

## Full Endpoint Catalogue (PRO plan access)

> Source: RapidAPI endpoint list, verified by user 2026-05-07. All endpoints return `"cost": 1`.

### User Profile Data
| Endpoint | Notes |
|----------|-------|
| `GET /api/v1/user/profile` | Core profile — used by script |
| `GET /api/v1/user/posts` | Recent posts — used by script |
| `GET /api/v1/user/comments` | Comments the user has made |
| `GET /api/v1/user/reactions` | Posts the user has reacted to |
| `GET /api/v1/user/videos` | Videos posted by the user |
| `GET /api/v1/user/images` | Images posted by the user |
| `GET /api/v1/user/recommendations` | Recommendations received/given |
| `GET /api/v1/user/save-to-pdf` | Save full profile as PDF |
| `GET /api/v1/user/contact` | Contact info (email, phone if public) |

### User Profile Additional Data
| Endpoint | Notes |
|----------|-------|
| `GET /api/v1/user/about` | About/summary section |
| `GET /api/v1/user/follower-connection` | Follower and connection counts |
| `GET /api/v1/user/experience` | Job history — used by script |
| `GET /api/v1/user/skills` | Skills listed on profile |
| `GET /api/v1/user/educations` | Education history — used by script |
| `GET /api/v1/user/publications` | Published articles/papers |
| `GET /api/v1/user/licenses-certifications` | Licences and certifications |
| `GET /api/v1/user/honors` | Honours and awards |
| `GET /api/v1/user/volunteers` | Volunteer experience |
| `GET /api/v1/user/interests-groups` | Groups the user follows |
| `GET /api/v1/user/interests-companies` | Companies the user follows |

### Company
| Endpoint | Notes |
|----------|-------|
| `GET /api/v1/company/profile` | Company overview |
| `GET /api/v1/company/people` | Employee list |
| `GET /api/v1/company/posts` | Company posts |
| `GET /api/v1/company/jobs` | Active job postings |
| `GET /api/v1/company/job-count` | Number of open jobs |
| `GET /api/v1/company/affiliated-pages` | Affiliated company pages |
| `GET /api/v1/company/associated-members` | Associated member profiles |

### Job
| Endpoint | Notes |
|----------|-------|
| `GET /api/v1/job/search` | Search jobs by keyword/location |
| `GET /api/v1/job/detail` | Detail for a specific job posting |

### Search
| Endpoint | Notes |
|----------|-------|
| `GET /api/v1/search/posts` | Search posts by keyword |
| `GET /api/v1/search/people` | Search people by keyword |
| `GET /api/v1/search/location` | Location lookup |
| `GET /api/v1/search/schools` | School lookup |
| `GET /api/v1/search/industry` | Industry suggestion lookup |

### Group
| Endpoint | Notes |
|----------|-------|
| `GET /api/v1/group/info` | Group overview |
| `GET /api/v1/group/posts` | Posts within a group |

### Post & Ad Library
| Endpoint | Notes |
|----------|-------|
| Post endpoints | Collapsed in UI — full list not captured |
| Ad Library | At least 1 endpoint — full list not captured |

---

## Potentially Useful Endpoints (Not Currently Used)

For cold email personalisation beyond the current 4-endpoint set:

| Endpoint | Requests | Potential use |
|----------|----------|---------------|
| `GET /api/v1/user/skills` | 1 | Add skills to the profile summary prompt for better icebreakers |
| `GET /api/v1/user/licenses-certifications` | 1 | Relevant for professional services ICPs |
| `GET /api/v1/user/contact` | 1 | May surface public email or phone — worth testing |
| `GET /api/v1/user/honors` | 1 | Awards/recognition as a personalisation hook |
| `GET /api/v1/company/profile` | 1 | Company context (size, industry, about) for account-level personalisation |
| `GET /api/v1/company/posts` | 1 | Company content themes — useful for B2B icebreakers |

---

## Limitations
- Requires a LinkedIn username as input — cannot resolve from email alone
- Must pair with a reverse-email-lookup tool (e.g. Apollo) to get LinkedIn URLs/usernames from email lists
- Coverage gaps: profiles not indexed by the scraper return 400/403 errors
- Not a real-time scraper — data freshness depends on the provider's cache
- VPN bypass required in Hong Kong (RapidAPI blocks VPN exit node IPs)
- Rate limit: 20 requests/minute on PRO (≈ 1 contact per 12 seconds at 4 requests/contact)
- Must pair with a campaign tool (Instantly, Lemlist) for sending

## Integration Notes
Used in the [[technology/linkedin-enrichment|LinkedIn Enrichment skill]] pipeline:
```
email list → Apollo (reverse lookup → LinkedIn URL + username) → Fresh LinkedIn Scraper → Claude Haiku (icebreaker) → sequencer
```
