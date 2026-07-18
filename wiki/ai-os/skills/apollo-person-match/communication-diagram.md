# Apollo Person Match — Communication Diagram

tags: [technical, skills, apollo-person-match, architecture, diagrams]

> *Interactive HTML/SVG diagram showing all network flows, credential loading, and communication stages for the Apollo Person Match skill on Julian's Hong Kong Mac setup.*

---

## Purpose

This diagram visualises the complete communication architecture of the Apollo Person Match skill, including:
- **Credential loading flow**: How API keys are loaded from disk into the environment
- **Two communication stages**: Python Scripts → Apollo API (direct), Python Scripts → Google Sheets (direct)
- **No VPN required**: Apollo API and Google Sheets are both accessible directly from Hong Kong
- **Data flow**: name + email in → linkedin_url, title, company, phone out

---

## How to Use / Reproduce

### View the diagram:
1. Copy the full HTML code below into a new file named `apollo-diagram.html`
2. Open the file in any web browser (no server required)

### Edit the diagram:
- SVG is embedded directly in the HTML — use a text editor to modify coordinates, colors, or labels
- CSS styles are in the `<style>` block at the top
- SVG drawing code starts after the `<!-- DIAGRAM SVG -->` comment

---

## Key Differences vs LinkedIn Enrichment Diagram

| Aspect | Apollo Person Match | LinkedIn Enrichment |
|--------|--------------------|--------------------|
| VPN needed | No — all direct | Yes — Anthropic via VPN |
| External services | 2 (Apollo, Sheets) | 3 (RapidAPI, Anthropic, Sheets) |
| Credentials | APOLLO_API_KEY, GOOGLE_SERVICE_ACCOUNT_JSON | RAPIDAPI_KEY, ANTHROPIC_API_KEY, GOOGLE_SERVICE_ACCOUNT_JSON |
| API calls per lead | 1 (Apollo /people/match) | 4 (RapidAPI) + 2 (Anthropic LLM) |
| VPN complexity | None | Reverse bypass rule required |

---

## Full HTML Source

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Apollo Person Match — Communication Flow</title>
<style>
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body { font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif; background: #0f1117; color: #e2e8f0; min-height: 100vh; padding: 32px; }
  h1 { font-size: 20px; font-weight: 600; margin-bottom: 6px; color: #f8fafc; }
  .subtitle { font-size: 13px; color: #64748b; margin-bottom: 28px; }
  .legend { display: flex; gap: 20px; margin-bottom: 32px; flex-wrap: wrap; }
  .legend-item { display: flex; align-items: center; gap: 8px; font-size: 12px; color: #94a3b8; }
  .legend-dot { width: 12px; height: 12px; border-radius: 50%; flex-shrink: 0; }
  .section-title { font-size: 13px; font-weight: 700; letter-spacing: 0.07em; text-transform: uppercase; color: #64748b; margin: 36px 0 14px; }
  table { width: 100%; border-collapse: collapse; font-size: 12px; }
  th { text-align: left; padding: 8px 12px; color: #64748b; font-size: 11px; font-weight: 700; text-transform: uppercase; letter-spacing: 0.06em; border-bottom: 1px solid #1e293b; white-space: nowrap; }
  td { padding: 10px 12px; border-bottom: 1px solid #1e293b; vertical-align: top; line-height: 1.6; }
  tr:last-child td { border-bottom: none; }
  tr:hover td { background: rgba(255,255,255,0.02); }
  code { background: #1e293b; border: 1px solid #334155; padding: 1px 6px; border-radius: 4px; font-size: 11px; font-family: "SF Mono", Monaco, monospace; color: #93c5fd; white-space: nowrap; }
  .tag { display: inline-block; font-size: 10px; font-weight: 700; padding: 2px 7px; border-radius: 99px; white-space: nowrap; }
  .tag-green  { background: #16a34a; color: #fff; }
  .tag-amber  { background: #d97706; color: #fff; }
  .tag-blue   { background: #0284c7; color: #fff; }
  .tag-purple { background: #7c3aed; color: #fff; }
  .dim  { color: #475569; font-size: 11px; }
  .proto { color: #f59e0b; font-weight: 600; }
  .port  { color: #38bdf8; font-weight: 600; }
  .auth  { color: #a78bfa; }
  .why   { color: #94a3b8; font-size: 11px; line-height: 1.6; }
</style>
</head>
<body>

<h1>Apollo Person Match — Communication Flow</h1>
<p class="subtitle">Julian's Mac (Hong Kong) · Direct connections only — no VPN required for this skill</p>

<div class="legend">
  <div class="legend-item"><div class="legend-dot" style="background:#16a34a"></div> Works correctly (direct)</div>
  <div class="legend-item"><div class="legend-dot" style="background:#65a30d"></div> Google Sheets (direct)</div>
  <div class="legend-item"><div class="legend-dot" style="background:#06b6d4"></div> Credential flow</div>
</div>

<!-- DIAGRAM SVG -->
<svg viewBox="0 0 980 590" xmlns="http://www.w3.org/2000/svg"
     style="width:100%;max-width:1100px;display:block;margin-bottom:8px;border-radius:14px;background:#0f1117;">

  <defs>
    <marker id="ag"    markerWidth="7" markerHeight="7" refX="5" refY="3" orient="auto"><path d="M0,0 L0,6 L7,3 z" fill="#16a34a"/></marker>
    <marker id="al"    markerWidth="7" markerHeight="7" refX="5" refY="3" orient="auto"><path d="M0,0 L0,6 L7,3 z" fill="#65a30d"/></marker>
    <marker id="acyan" markerWidth="7" markerHeight="7" refX="5" refY="3" orient="auto"><path d="M0,0 L0,6 L7,3 z" fill="#06b6d4"/></marker>
    <marker id="agrey" markerWidth="7" markerHeight="7" refX="5" refY="3" orient="auto"><path d="M0,0 L0,6 L7,3 z" fill="#94a3b8"/></marker>
  </defs>

  <!-- ══ MAC BOX ══ -->
  <rect x="18" y="18" width="318" height="504" rx="14" fill="#1e293b" stroke="#334155" stroke-width="1.5"/>
  <text x="36" y="44" fill="#64748b" font-size="10" font-weight="700" font-family="system-ui" letter-spacing="1.2">🖥  JULIAN'S MAC — HONG KONG</text>

  <!-- ══ CREDENTIAL LOADING SECTION ══ -->
  <text x="36" y="70" fill="#64748b" font-size="9" font-weight="700" font-family="system-ui" letter-spacing="1.2">CREDENTIAL LOADING  ·  STARTUP</text>

  <!-- credentials.json -->
  <rect x="44" y="80" width="268" height="72" rx="8" fill="#111827" stroke="#374151" stroke-width="1"/>
  <text x="68" y="98" fill="#9ca3af" font-size="11" font-weight="600" font-family="system-ui">~/.leadgen/credentials.json  🔐</text>
  <text x="68" y="113" fill="#475569" font-size="9" font-family="system-ui">APOLLO_API_KEY · GOOGLE_SERVICE_ACCOUNT_JSON</text>
  <text x="68" y="125" fill="#475569" font-size="9" font-family="system-ui">SHEETS_AUTH_METHOD</text>
  <text x="68" y="138" fill="#6b7280" font-size="8" font-family="system-ui">chmod 600 (owner only)</text>

  <!-- Arrow: credentials.json → credentials.py -->
  <path d="M 178,152 L 178,174" fill="none" stroke="#06b6d4" stroke-width="2" marker-end="url(#acyan)"/>
  <rect x="220" y="150" width="140" height="32" rx="4" fill="#0d1a25" opacity="0.95"/>
  <text x="290" y="161" fill="#06b6d4" font-size="8" font-weight="700" font-family="system-ui" text-anchor="middle">Read JSON file</text>
  <text x="290" y="173" fill="#06b6d4" font-size="8" font-family="system-ui" text-anchor="middle" opacity="0.7">Check for required keys</text>

  <!-- credentials.py -->
  <rect x="44" y="174" width="268" height="76" rx="8" fill="#1a1a2e" stroke="#06b6d4" stroke-width="1.5"/>
  <text x="68" y="194" fill="#22d3ee" font-size="11" font-weight="600" font-family="system-ui">credentials.py  ·  CredentialManager.load()</text>
  <text x="68" y="209" fill="#475569" font-size="9" font-family="system-ui">1. Check os.environ for existing values</text>
  <text x="68" y="221" fill="#475569" font-size="9" font-family="system-ui">2. Load missing keys from JSON file</text>
  <text x="68" y="233" fill="#475569" font-size="9" font-family="system-ui">3. Inject into os.environ (called at script start)</text>

  <!-- Arrow: credentials.py → os.environ -->
  <path d="M 178,250 L 178,272" fill="none" stroke="#06b6d4" stroke-width="2" marker-end="url(#acyan)"/>
  <rect x="220" y="248" width="140" height="32" rx="4" fill="#0d1a25" opacity="0.95"/>
  <text x="290" y="259" fill="#06b6d4" font-size="8" font-weight="700" font-family="system-ui" text-anchor="middle">Inject into environment</text>
  <text x="290" y="271" fill="#06b6d4" font-size="8" font-family="system-ui" text-anchor="middle" opacity="0.7">Available to script at startup</text>

  <!-- os.environ -->
  <rect x="44" y="272" width="268" height="68" rx="8" fill="#0f2a1a" stroke="#10b981" stroke-width="1.5"/>
  <text x="68" y="290" fill="#86efac" font-size="11" font-weight="600" font-family="system-ui">os.environ  (Shell Variables)</text>
  <text x="68" y="305" fill="#475569" font-size="9" font-family="system-ui">APOLLO_API_KEY · GOOGLE_SERVICE_ACCOUNT_JSON</text>
  <text x="68" y="318" fill="#475569" font-size="9" font-family="system-ui">SHEETS_AUTH_METHOD</text>

  <!-- Divider -->
  <line x1="30" y1="356" x2="336" y2="356" stroke="#334155" stroke-width="1"/>

  <!-- apollo_person_match.py -->
  <rect x="44" y="368" width="268" height="130" rx="8" fill="#1a1a2e" stroke="#7c3aed" stroke-width="1.5"/>
  <text x="68" y="390" fill="#c4b5fd" font-size="12" font-weight="600" font-family="system-ui">apollo_person_match.py  🐍</text>
  <text x="68" y="406" fill="#64748b" font-size="10" font-family="system-ui">HTTPS · Port 443 · APOLLO_API_KEY auth</text>
  <text x="68" y="419" fill="#22c55e" font-size="9" font-family="system-ui">All traffic DIRECT — no VPN needed ✓</text>
  <line x1="44" y1="427" x2="312" y2="427" stroke="#2a2a4a" stroke-width="1"/>
  <text x="68" y="441" fill="#475569" font-size="9" font-family="system-ui">Reads name + email from Sheet (pending rows).</text>
  <text x="68" y="453" fill="#475569" font-size="9" font-family="system-ui">POSTs to /people/match with name + email.</text>
  <text x="68" y="465" fill="#475569" font-size="9" font-family="system-ui">Parses: linkedin_url, title, org, phone.</text>
  <text x="68" y="477" fill="#475569" font-size="9" font-family="system-ui">Writes results + match_status back to Sheet.</text>
  <text x="68" y="489" fill="#475569" font-size="9" font-family="system-ui">Rate: 0.5s sleep · 60s backoff on 429.</text>

  <!-- ══ RIGHT PANEL ══ -->

  <!-- Apollo API -->
  <rect x="614" y="48" width="348" height="172" rx="10" fill="#0a1f0a" stroke="#16a34a" stroke-width="1.5"/>
  <text x="642" y="74" fill="#86efac" font-size="13" font-weight="600" font-family="system-ui">Apollo API  🔍</text>
  <text x="642" y="90" fill="#64748b" font-size="10" font-family="system-ui">api.apollo.io · HTTPS · Port 443</text>
  <text x="642" y="104" fill="#64748b" font-size="10" font-family="system-ui">POST /api/v1/people/match</text>
  <text x="642" y="118" fill="#64748b" font-size="10" font-family="system-ui">Header: x-api-key · Body: name + email</text>
  <text x="642" y="132" fill="#22c55e" font-size="9" font-family="system-ui">Direct from HK — no VPN block · 1 credit/call</text>
  <line x1="614" y1="140" x2="962" y2="140" stroke="#0a1f0a" stroke-width="1" opacity="0.6"/>
  <text x="642" y="152" fill="#1e4620" font-size="9" font-family="system-ui">Returns: linkedin_url, title, organization,</text>
  <text x="642" y="164" fill="#1e4620" font-size="9" font-family="system-ui">corporate_phone, mobile_phone, first_name, last_name.</text>
  <text x="642" y="176" fill="#1e4620" font-size="9" font-family="system-ui">Match rate ~80–90% with name + email input.</text>
  <text x="642" y="188" fill="#1e4620" font-size="9" font-family="system-ui">Status: matched / no_linkedin / failed.</text>
  <rect x="884" y="56" width="66" height="18" rx="9" fill="#16a34a"/>
  <text x="917" y="69" fill="white" font-size="10" font-weight="700" font-family="system-ui" text-anchor="middle">WORKS ✓</text>

  <!-- Google Sheets API -->
  <rect x="614" y="358" width="348" height="122" rx="10" fill="#1a2a0f" stroke="#65a30d" stroke-width="1.5"/>
  <text x="642" y="382" fill="#bef264" font-size="13" font-weight="600" font-family="system-ui">Google Sheets API  📊</text>
  <text x="642" y="398" fill="#64748b" font-size="10" font-family="system-ui">sheets.googleapis.com · HTTPS · Port 443</text>
  <text x="642" y="412" fill="#64748b" font-size="10" font-family="system-ui">Service Account JWT · GET + PUT /v4/spreadsheets/...</text>
  <text x="642" y="426" fill="#475569" font-size="9" font-family="system-ui">Bypasses VPN · Google tolerates direct HK traffic</text>
  <line x1="614" y1="434" x2="962" y2="434" stroke="#1a2a0f" stroke-width="1" opacity="0.6"/>
  <text x="642" y="446" fill="#2d4020" font-size="9" font-family="system-ui">Reads pending rows (name + email). Writes back</text>
  <text x="642" y="458" fill="#2d4020" font-size="9" font-family="system-ui">linkedin_url, title, company, phone, match_status.</text>
  <rect x="884" y="366" width="66" height="18" rx="9" fill="#65a30d"/>
  <text x="917" y="379" fill="white" font-size="10" font-weight="700" font-family="system-ui" text-anchor="middle">WORKS ✓</text>

  <!-- ══ CREDENTIAL ARROWS ══ -->
  <!-- os.environ → Apollo API (APOLLO_API_KEY) -->
  <path d="M 312,290 Q 500,190 612,110" fill="none" stroke="#06b6d4" stroke-width="1.5" stroke-dasharray="4,3" opacity="0.6" marker-end="url(#acyan)"/>
  <text x="415" y="195" fill="#06b6d4" font-size="8" font-weight="600" font-family="system-ui" opacity="0.8">APOLLO_API_KEY</text>

  <!-- os.environ → Google Sheets (GOOGLE_SERVICE_ACCOUNT_JSON) -->
  <path d="M 312,330 Q 500,370 612,400" fill="none" stroke="#06b6d4" stroke-width="1.5" stroke-dasharray="4,3" opacity="0.6" marker-end="url(#acyan)"/>
  <text x="392" y="393" fill="#06b6d4" font-size="8" font-weight="600" font-family="system-ui" opacity="0.8">GOOGLE_SERVICE_ACCOUNT_JSON</text>

  <!-- ══ STAGE ARROWS ══ -->

  <!-- Stage 1: apollo_person_match.py ↔ Apollo API (direct) -->
  <path d="M 314,415 Q 462,290 612,128" fill="none" stroke="#16a34a" stroke-width="2" marker-end="url(#ag)"/>
  <path d="M 612,144 Q 462,307 314,432" fill="none" stroke="#16a34a" stroke-width="1.5" stroke-dasharray="5,3" opacity="0.7" marker-end="url(#ag)"/>
  <circle cx="326" cy="422" r="10" fill="#16a34a"/>
  <text x="326" y="426" fill="white" font-size="9" font-weight="700" font-family="system-ui" text-anchor="middle">1</text>
  <rect x="392" y="254" width="140" height="32" rx="4" fill="#050e09" opacity="0.95"/>
  <text x="462" y="265" fill="#16a34a" font-size="8" font-weight="700" font-family="system-ui" text-anchor="middle">→ :443  HTTPS · direct</text>
  <text x="462" y="277" fill="#16a34a" font-size="8" font-family="system-ui" text-anchor="middle" opacity="0.65">← :49152–65535  ephemeral</text>

  <!-- Stage 2: apollo_person_match.py ↔ Google Sheets (direct) -->
  <path d="M 314,456 Q 462,442 612,428" fill="none" stroke="#65a30d" stroke-width="2" marker-end="url(#al)"/>
  <path d="M 612,442 Q 462,458 314,470" fill="none" stroke="#65a30d" stroke-width="1.5" stroke-dasharray="5,3" opacity="0.7" marker-end="url(#al)"/>
  <circle cx="326" cy="463" r="10" fill="#4d7c0f"/>
  <text x="326" y="467" fill="white" font-size="9" font-weight="700" font-family="system-ui" text-anchor="middle">2</text>
  <rect x="392" y="496" width="140" height="32" rx="4" fill="#060c04" opacity="0.95"/>
  <text x="462" y="507" fill="#65a30d" font-size="8" font-weight="700" font-family="system-ui" text-anchor="middle">→ :443  HTTPS · direct</text>
  <text x="462" y="519" fill="#65a30d" font-size="8" font-family="system-ui" text-anchor="middle" opacity="0.65">← :49152–65535  ephemeral</text>

  <!-- Arrow direction legend -->
  <rect x="340" y="558" width="300" height="26" rx="6" fill="#1e293b" opacity="0.8"/>
  <line x1="356" y1="571" x2="386" y2="571" stroke="#94a3b8" stroke-width="1.5" marker-end="url(#agrey)"/>
  <text x="393" y="575" fill="#94a3b8" font-size="9" font-family="system-ui">outbound  (client → :443)</text>
  <line x1="496" y1="571" x2="526" y2="571" stroke="#94a3b8" stroke-width="1.5" stroke-dasharray="4,3" marker-end="url(#agrey)"/>
  <text x="533" y="575" fill="#94a3b8" font-size="9" font-family="system-ui">return  (← :ephem)</text>

</svg>

<!-- CREDENTIAL TABLE -->
<p class="section-title">Credential Management Workflow</p>
<table>
  <thead>
    <tr>
      <th>Credential</th>
      <th>Source</th>
      <th>Loading</th>
      <th>Used By</th>
      <th>Purpose</th>
      <th>Security</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>APOLLO_API_KEY</code></td>
      <td><code>~/.leadgen/credentials.json</code></td>
      <td>credentials.py @ script start<br><span class="dim">injected into os.environ</span></td>
      <td>apollo_person_match.py</td>
      <td class="why">Authenticates POST requests to Apollo /people/match. Passed as <code>x-api-key</code> header. Each call costs 1 Apollo credit and returns matched person data including linkedin_url.</td>
      <td><span class="tag tag-amber">SECRET</span><br>chmod 600</td>
    </tr>
    <tr>
      <td><code>GOOGLE_SERVICE_ACCOUNT_JSON</code></td>
      <td><code>~/.leadgen/credentials.json</code> (path ref)</td>
      <td>credentials.py @ script start<br><span class="dim">file path injected into os.environ</span></td>
      <td>gsheets_store.py</td>
      <td class="why">Service account JWT file for Google Sheets API authentication. Loaded by gspread to generate Bearer tokens. Enables reading pending rows (name + email) and writing back match results (linkedin_url, title, company, phone, match_status).</td>
      <td><span class="tag tag-amber">SECRET</span><br>chmod 600<br>File-based</td>
    </tr>
    <tr>
      <td><code>SHEETS_AUTH_METHOD</code></td>
      <td><code>~/.leadgen/credentials.json</code></td>
      <td>credentials.py @ script start<br><span class="dim">injected into os.environ</span></td>
      <td>gsheets_store.py</td>
      <td class="why">Determines which Google Sheets auth method to use: "service_account" or "oauth". Currently set to "service_account".</td>
      <td><span class="tag tag-green">NOT SECRET</span><br>chmod 600<br>Config value</td>
    </tr>
  </tbody>
</table>

<!-- COMMUNICATION FLOWS TABLE -->
<p class="section-title">Communication Flows — Full Detail</p>
<table>
  <thead>
    <tr>
      <th>Stage</th>
      <th>From</th>
      <th>To</th>
      <th>Protocol</th>
      <th>Port</th>
      <th>Auth</th>
      <th>Route</th>
      <th>Why this communication exists</th>
      <th>Status</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>1</strong></td>
      <td>apollo_person_match.py</td>
      <td><code>api.apollo.io</code><br><span class="dim">POST /api/v1/people/match</span></td>
      <td><span class="proto">HTTPS / TLS 1.3</span></td>
      <td><span class="port">443</span></td>
      <td><span class="auth">x-api-key header</span></td>
      <td>Direct — no VPN<br><span class="dim">Apollo not blocked in HK</span></td>
      <td class="why">Core enrichment call. For each pending row, the script sends name + email to Apollo's people/match endpoint. Apollo searches its database and returns a matched person object containing linkedin_url, title, organization, phone numbers. Costs 1 credit per call. 0.5s sleep between calls to respect rate limits; 60s backoff on HTTP 429.</td>
      <td><span class="tag tag-green">WORKS ✓</span></td>
    </tr>
    <tr>
      <td><strong>2</strong></td>
      <td>gsheets_store.py</td>
      <td><code>sheets.googleapis.com</code><br><span class="dim">GET + PUT /v4/spreadsheets/{id}/values</span></td>
      <td><span class="proto">HTTPS / TLS 1.3</span></td>
      <td><span class="port">443</span></td>
      <td><span class="auth">Service Account JWT<br>Bearer token</span></td>
      <td>Direct — no VPN<br><span class="dim">Google tolerates HK direct</span></td>
      <td class="why">Google Sheets is the pipeline's data store. The script reads it at the start to get pending rows (name + email, match_status = "pending"), then writes results back after each Apollo call: linkedin_url, title, organization, mobile_phone, corporate_phone, and match_status ("matched" / "no_linkedin" / "failed").</td>
      <td><span class="tag tag-green">WORKS ✓</span></td>
    </tr>
  </tbody>
</table>

<!-- CREDENTIAL LOADING PROCESS -->
<p class="section-title">Credential Loading Process</p>
<table>
  <thead>
    <tr>
      <th>Step</th>
      <th>Component</th>
      <th>Action</th>
      <th>Condition</th>
      <th>Result</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>1</strong></td>
      <td><code>credentials.py</code><br>CredentialManager.load(required=[])</td>
      <td>Called at script startup<br><span class="dim">before any API calls</span></td>
      <td>Always runs when script imports credentials module</td>
      <td>Reads ~/.leadgen/credentials.json from disk (chmod 600)</td>
    </tr>
    <tr>
      <td><strong>2</strong></td>
      <td><code>credentials.py</code><br>Check existing env</td>
      <td>For each required key, check if already in <code>os.environ</code></td>
      <td>User can pre-set via shell (export APOLLO_API_KEY=...)</td>
      <td>Skip loading if already present; allows manual override</td>
    </tr>
    <tr>
      <td><strong>3</strong></td>
      <td><code>credentials.py</code><br>Load from file</td>
      <td>For missing keys, load value from credentials.json</td>
      <td>Key exists in JSON file</td>
      <td>Inject into <code>os.environ[key] = value</code></td>
    </tr>
    <tr>
      <td><strong>4</strong></td>
      <td><code>credentials.py</code><br>Prompt if missing</td>
      <td>If key not in env AND not in file, prompt user</td>
      <td>First-time setup (key doesn't exist anywhere)</td>
      <td>User enters value → saved to credentials.json (chmod 600) → injected into os.environ</td>
    </tr>
    <tr>
      <td><strong>5</strong></td>
      <td><code>apollo_person_match.py</code></td>
      <td>Read credentials from environment</td>
      <td>After CredentialManager.load() completes</td>
      <td><code>os.environ.get("APOLLO_API_KEY")</code> → value used in x-api-key header</td>
    </tr>
    <tr>
      <td><strong>6</strong></td>
      <td><code>apollo_person_match.py</code></td>
      <td>Make Apollo API call with credentials</td>
      <td>Credentials injected into request headers</td>
      <td><code>headers = {"x-api-key": os.environ["APOLLO_API_KEY"]}</code> → Stage 1 request</td>
    </tr>
    <tr>
      <td><strong>7</strong></td>
      <td><code>gsheets_store.py</code></td>
      <td>Load Google service account file</td>
      <td>Path from <code>os.environ["GOOGLE_SERVICE_ACCOUNT_JSON"]</code></td>
      <td>gspread library reads JWT file → generates Bearer token → Stage 2 request</td>
    </tr>
  </tbody>
</table>

<!-- API ENDPOINT REFERENCE -->
<p class="section-title">API Endpoint Reference</p>
<table>
  <thead>
    <tr><th>Call</th><th>Method</th><th>Endpoint</th><th>Key Headers / Body</th><th>Cost</th></tr>
  </thead>
  <tbody>
    <tr>
      <td>Person match</td>
      <td><span class="tag tag-purple">POST</span></td>
      <td><code>https://api.apollo.io/api/v1/people/match</code></td>
      <td><code>x-api-key</code> · body: <code>{"name": "...", "email": "...", "reveal_personal_emails": false, "reveal_phone_number": false}</code></td>
      <td>1 credit</td>
    </tr>
    <tr>
      <td>Sheet read</td>
      <td><span class="tag tag-blue">GET</span></td>
      <td><code>https://sheets.googleapis.com/v4/spreadsheets/{id}/values/{range}</code></td>
      <td>Bearer JWT (service account)</td>
      <td>free</td>
    </tr>
    <tr>
      <td>Sheet write</td>
      <td><span class="tag tag-amber">PUT</span></td>
      <td><code>https://sheets.googleapis.com/v4/spreadsheets/{id}/values/{range}</code></td>
      <td>Bearer JWT (service account)</td>
      <td>free</td>
    </tr>
  </tbody>
</table>

</body>
</html>
```

---

## Notes

- **No VPN complexity** — unlike the LinkedIn enrichment skill, Apollo Person Match runs with entirely direct connections. No ExpressVPN configuration required.
- **No external dependencies** — the HTML file is self-contained (all CSS and SVG inline)
- **Dark theme** — consistent with the LinkedIn enrichment VPN diagram
- **Browser compatibility** — works in all modern browsers (Chrome, Safari, Firefox, Edge)

---

## Version History

- **2026-04-29**: Initial version. Direct-connection architecture, 2 stages (Apollo + Sheets), credential loading flow, full supporting tables.
