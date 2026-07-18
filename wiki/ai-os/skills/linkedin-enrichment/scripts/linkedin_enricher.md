# linkedin_enricher.py — LinkedIn API + LLM Summarisation

tags: [technical, skills, linkedin, python, api, llm]

> *Core enrichment logic. Calls RapidAPI Fresh LinkedIn Scraper for profile, experience, education, and posts data. Sends cleaned data to Claude Haiku for summarisation. Returns structured results.*

---

## Responsibilities

- Make GET requests to Fresh LinkedIn Scraper API (4 endpoints per lead)
- Clean and structure raw API responses
- Send structured data to LLM for summarisation
- Return results as a dict ready for `gsheets_store.update_row()`
- Handle RapidAPI 429 rate limits (sleep 30s, retry once)

---

## Key Design Decisions

- **`requests` library** used for HTTP (not `urllib`) — more reliable with RapidAPI, easier error handling
- **LLM model hardcoded** as `claude-haiku-4-5-20251001` — prevents accidental use of expensive models
- **LLM provider abstracted** via `call_llm()` — supports anthropic, openai, ollama without changing caller code
- **Cleaning separated from fetching** — `clean_profile()`, `clean_education()`, `clean_posts()` are pure functions, easy to test independently
- **Errors return empty strings + `failed` status** rather than raising — pipeline continues to next row

---

## Source

```python
"""LinkedIn profile and posts enrichment using Fresh LinkedIn Scraper API + LLM summarization."""
import os, json, time, sys
import urllib.request, urllib.error
import requests

# ── Prompts ──────────────────────────────────────────────────────────────────

PROFILE_SUMMARY_PROMPT = """Please summarize the following LinkedIn profile data for a lead I want to cold email. I want to combine this summary with other information about them to send personalized emails, so please make sure you include relevant bits in the summary.

Profile data (headline, recent roles, and expertise):
{profile_string}

Focus on: current role and responsibilities, career trajectory, areas of expertise, anything that would be useful as a cold email hook. Keep it under 3 paragraphs."""

POSTS_SUMMARY_PROMPT = """Below are the most recent posts from a LinkedIn user. Summarize them collectively in no more than two short paragraphs. Focus on capturing the main themes, tone, and any recurring interests or professional concerns.

Avoid listing each post separately — instead, synthesize the information into a narrative that gives a clear idea of what this person is currently focused on or passionate about.

Posts:
{posts_string}

Keep it insightful but brief — no more than 2 concise paragraphs."""

# ── Data cleaners ─────────────────────────────────────────────────────────────

def clean_profile(profile_data: dict, experiences: list, educations: list) -> dict:
    """Extract key fields from Fresh LinkedIn Scraper API responses."""
    top_exp = experiences[:3] if experiences else []
    exp_summary = []
    for exp in top_exp:
        title = exp.get("title", "")
        company = exp.get("company", {}).get("name", "")
        desc = exp.get("description", "")
        if title and company:
            exp_summary.append(f"{title} at {company}")
            if desc:
                exp_summary.append(f"  Description: {desc}")
    return {
        "first_name":  profile_data.get("first_name", ""),
        "last_name":   profile_data.get("last_name", ""),
        "headline":    profile_data.get("headline", ""),
        "location":    f"{profile_data.get('location', {}).get('city', '')}, {profile_data.get('location', {}).get('country', '')}".strip(", "),
        "employment":  " | ".join(exp_summary) if exp_summary else "",
    }

def clean_education(educations: list) -> str:
    """Format education history as JSON string for storage."""
    if not educations:
        return ""
    edu_list = []
    for edu in educations:
        edu_list.append({
            "school":     edu.get("school", ""),
            "degree":     edu.get("degree", ""),
            "start_year": edu.get("date", {}).get("start", ""),
            "end_year":   edu.get("date", {}).get("end", "")
        })
    return json.dumps(edu_list)

def clean_posts(raw_posts: list) -> str:
    """Extract top 5 posts text for LLM summarization."""
    posts_text = []
    for i, post in enumerate((raw_posts or [])[:5], 1):
        text = post.get("text", "").strip()
        if text:
            posts_text.append(f"Post {i}:\n{text}\n")
    return "\n".join(posts_text)

# ── LLM callers ───────────────────────────────────────────────────────────────

def call_llm(prompt: str, provider: str = "anthropic") -> str:
    if provider == "anthropic":
        return _call_anthropic(prompt)
    elif provider == "openai":
        return _call_openai(prompt)
    elif provider == "ollama":
        return _call_ollama(prompt)
    raise ValueError(f"Unknown provider: {provider}")

def _call_anthropic(prompt: str) -> str:
    api_key = os.environ.get("ANTHROPIC_API_KEY")
    if not api_key:
        raise ValueError("ANTHROPIC_API_KEY not set")
    payload = json.dumps({
        "model": "claude-haiku-4-5-20251001",  # hardcoded — do not change without testing cost
        "max_tokens": 512,
        "messages": [{"role": "user", "content": prompt}]
    }).encode()
    req = urllib.request.Request(
        "https://api.anthropic.com/v1/messages",
        data=payload,
        headers={"Content-Type": "application/json",
                 "x-api-key": api_key,
                 "anthropic-version": "2023-06-01"},
        method="POST"
    )
    with urllib.request.urlopen(req, timeout=30) as resp:
        data = json.loads(resp.read())
    return data["content"][0]["text"]

def _call_openai(prompt: str) -> str:
    api_key = os.environ.get("OPENAI_API_KEY")
    if not api_key:
        raise ValueError("OPENAI_API_KEY not set")
    payload = json.dumps({
        "model": "gpt-3.5-turbo",
        "max_tokens": 512,
        "messages": [{"role": "user", "content": prompt}]
    }).encode()
    req = urllib.request.Request(
        "https://api.openai.com/v1/chat/completions",
        data=payload,
        headers={"Content-Type": "application/json",
                 "Authorization": f"Bearer {api_key}"},
        method="POST"
    )
    with urllib.request.urlopen(req, timeout=30) as resp:
        data = json.loads(resp.read())
    return data["choices"][0]["message"]["content"]

def _call_ollama(prompt: str, model: str = "llama3") -> str:
    payload = json.dumps(
        {"model": model, "prompt": prompt, "stream": False}
    ).encode()
    req = urllib.request.Request(
        "http://localhost:11434/api/generate",
        data=payload,
        headers={"Content-Type": "application/json"},
        method="POST"
    )
    with urllib.request.urlopen(req, timeout=60) as resp:
        data = json.loads(resp.read())
    return data.get("response", "")

# ── Main enricher class ────────────────────────────────────────────────────────

class LinkedInEnricher:
    def __init__(self, rapidapi_key: str = None, llm_provider: str = "anthropic"):
        self.api_key = rapidapi_key or os.environ.get("RAPIDAPI_KEY")
        if not self.api_key:
            raise ValueError("RAPIDAPI_KEY not set")
        self.llm_provider = llm_provider
        self._headers = {
            "x-rapidapi-host": "fresh-linkedin-scraper-api.p.rapidapi.com",
            "x-rapidapi-key":  self.api_key,
        }
        self.base_url = "https://fresh-linkedin-scraper-api.p.rapidapi.com/api/v1/user"

    def _get(self, endpoint: str, params: dict) -> dict:
        """Make HTTP GET request to Fresh LinkedIn Scraper API."""
        query = "&".join(f"{k}={v}" for k, v in params.items())
        url = f"{self.base_url}{endpoint}?{query}"
        try:
            resp = requests.get(url, headers=self._headers, timeout=20)
            resp.raise_for_status()
            return resp.json()
        except requests.exceptions.HTTPError as e:
            if e.response.status_code == 429:
                print("RapidAPI rate limit. Sleeping 30s...", file=sys.stderr)
                time.sleep(30)
                resp = requests.get(url, headers=self._headers, timeout=20)
                resp.raise_for_status()
                return resp.json()
            raise

    def enrich_profile(self, linkedin_username: str) -> dict:
        """Fetch LinkedIn profile, experiences, educations and generate AI summary."""
        try:
            profile_resp = self._get("/profile",    {"username": linkedin_username})
            exp_resp     = self._get("/experience", {"username": linkedin_username})
            edu_resp     = self._get("/educations", {"username": linkedin_username})

            profile_data = profile_resp.get("data", {})
            experiences  = exp_resp.get("data", [])
            educations   = edu_resp.get("data", [])

            cleaned     = clean_profile(profile_data, experiences, educations)
            profile_str = json.dumps(cleaned, indent=2)
            summary     = call_llm(
                PROFILE_SUMMARY_PROMPT.format(profile_string=profile_str),
                self.llm_provider
            )
            return {
                "about_linkedin_profile": summary,
                "profile_summary_scrape": "completed",
                "education_history":      clean_education(educations)
            }
        except Exception as e:
            print(f"Profile enrichment failed for {linkedin_username}: {e}", file=sys.stderr)
            return {
                "about_linkedin_profile": "",
                "profile_summary_scrape": "failed",
                "education_history":      ""
            }

    def enrich_posts(self, linkedin_username: str) -> dict:
        """Fetch recent LinkedIn posts and generate AI narrative summary."""
        try:
            raw        = self._get("/posts", {"username": linkedin_username})
            posts_data = raw.get("data", [])
            if not posts_data:
                return {"recent_posts_summary": "", "posts_scrape_status": "failed"}

            posts_str = clean_posts(posts_data)
            if not posts_str.strip():
                return {"recent_posts_summary": "", "posts_scrape_status": "failed"}

            summary = call_llm(
                POSTS_SUMMARY_PROMPT.format(posts_string=posts_str),
                self.llm_provider
            )
            return {"recent_posts_summary": summary, "posts_scrape_status": "scraped"}
        except Exception as e:
            print(f"Posts enrichment failed for {linkedin_username}: {e}", file=sys.stderr)
            return {"recent_posts_summary": "", "posts_scrape_status": "failed"}
```

---

## Notes

- **Not all LinkedIn profiles are indexed** by Fresh LinkedIn Scraper. Test with a known-good profile before testing your actual leads. See [[technology/linkedin-enrichment/TESTING|Testing Log]].
- **DEBUG print statement** on line 163 of the original logs the first 20 chars of the API key to stderr — remove before sharing logs.
- **`requests` vs `urllib`**: The `_get()` method uses `requests`; the LLM callers use `urllib`. This is inconsistent — a future refactor should standardise on `requests`.
