# VPN Communication Diagram — Interactive Visualization

tags: [technical, skills, linkedin-enrichment, architecture, vpn, diagrams]

> *Interactive HTML/SVG diagram showing all network flows, VPN routing, credential loading, and communication stages for the LinkedIn enrichment skill on Julian's Hong Kong Mac setup.*

---

## Purpose

This diagram visualizes the complete communication architecture of the LinkedIn enrichment skill, including:
- **Credential loading flow**: How API keys are loaded from disk into the environment
- **VPN tunnel lifecycle**: Stage 1 (ExpressVPN) before any API calls
- **Four communication stages**: Claude Code → Anthropic (via VPN), Python Scripts → RapidAPI (direct), Python Scripts → Anthropic (via VPN), Python Scripts → Google Sheets (direct)
- **Network isolation**: Visual separation of local client (left), VPN tunnel, and remote services (right)
- **VPN routing rules**: Which traffic goes through the tunnel vs. direct to the internet

The diagram includes:
- Interactive SVG with stage badges and flow labels
- Credential management workflow table
- Full communication flow details (protocol, port, auth, route)
- Credential loading step-by-step process
- API endpoint reference (RapidAPI, Anthropic, Google Sheets)

---

## How to Use / Reproduce

### View the diagram:
1. Copy the full HTML code below into a new file named `vpn-diagram.html`
2. Open the file in any web browser (no server required)
3. Zoom/pan the SVG diagram with mouse wheel and drag

### Edit the diagram:
- The SVG is embedded directly in the HTML — use a text editor to modify coordinates, colors, labels, or add new elements
- CSS styles are in the `<style>` block at the top
- SVG drawing code starts after the `<!-- ═════════════════════════════════════════════════════════ DIAGRAM SVG -->` comment

### Common edits:
- **Change colors**: Update hex codes in `fill=`, `stroke=`, and SVG `<marker>` definitions
- **Move boxes**: Adjust `x=`, `y=`, `width=`, `height=` attributes on `<rect>` elements
- **Edit labels**: Update `<text>` element content and `text-anchor`, `x=`, `y=` positioning
- **Add flows**: Duplicate a `<path>` element block and adjust `d=` (path definition) and `marker-end=` attributes

---

## Key Sections Explained

### Credential Loading (Top section)
Three components flow downward:
1. **~/.leadgen/credentials.json** — JSON file on disk with API keys (chmod 600)
2. **credentials.py** — CredentialManager loads and checks keys
3. **os.environ** — Injected shell variables available to running scripts

Flow descriptions clarify each arrow:
- "Read JSON file" + "Check for required keys"
- "Inject into environment" + "Available to script at startup"

### VPN Tunnel Boundary (Orange dashed box)
Only **ExpressVPN Engine** and **Claude Code** are inside the tunnel. **Python Scripts** are outside because they need to bypass the VPN for RapidAPI (RapidAPI blocks VPN exit node IPs).

### Communication Stages
- **Stage 1**: ExpressVPN Client ↔ VPN Exit Node (UDP 1194 Lightway tunnel, always-on)
- **Stage 2**: Claude Code ↔ Anthropic API (via VPN — blocked in HK)
- **Stage 3a**: Python Scripts ↔ RapidAPI (direct — VPN would be blocked)
- **Stage 3b**: Python Scripts ↔ Anthropic API (via VPN — same reason as Stage 2)
- **Stage 4**: Python Scripts ↔ Google Sheets (direct — Google tolerates HK direct)

### VPN ROUTED Boundary (Right panel, orange dashed box)
Mirrors the left panel's VPN tunnel. Wraps both VPN Exit Node and Anthropic API to show that traffic routed through the tunnel emerges from here.

---

## Full HTML Source

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>VPN Communication Flow — Ports & Protocols</title>
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
  .tag-red    { background: #dc2626; color: #fff; }
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

<h1>VPN Communication Flow — Ports, Protocols & Stages</h1>
<p class="subtitle">Julian's Mac (Hong Kong) · ExpressVPN with 160.79.104.0/21 bypass-exclusion rule</p>

<div class="legend">
  <div class="legend-item"><div class="legend-dot" style="background:#16a34a"></div> Works correctly</div>
  <div class="legend-item"><div class="legend-dot" style="background:#d97706"></div> Through VPN</div>
  <div class="legend-item"><div class="legend-dot" style="background:#0284c7"></div> Hosted remotely</div>
</div>

<!-- ═══════════════════════════════════════════════════════ DIAGRAM SVG -->
<svg viewBox="0 0 980 900" xmlns="http://www.w3.org/2000/svg"
     style="width:100%;max-width:1100px;display:block;margin-bottom:8px;border-radius:14px;background:#0f1117;">

  <defs>
    <marker id="ag"    markerWidth="7" markerHeight="7" refX="5" refY="3" orient="auto"><path d="M0,0 L0,6 L7,3 z" fill="#16a34a"/></marker>
    <marker id="ay"    markerWidth="7" markerHeight="7" refX="5" refY="3" orient="auto"><path d="M0,0 L0,6 L7,3 z" fill="#ca8a04"/></marker>
    <marker id="al"    markerWidth="7" markerHeight="7" refX="5" refY="3" orient="auto"><path d="M0,0 L0,6 L7,3 z" fill="#65a30d"/></marker>
    <marker id="ap"    markerWidth="7" markerHeight="7" refX="5" refY="3" orient="auto"><path d="M0,0 L0,6 L7,3 z" fill="#c4b5fd"/></marker>
    <marker id="acyan" markerWidth="7" markerHeight="7" refX="5" refY="3" orient="auto"><path d="M0,0 L0,6 L7,3 z" fill="#06b6d4"/></marker>
    <marker id="agrey" markerWidth="7" markerHeight="7" refX="5" refY="3" orient="auto"><path d="M0,0 L0,6 L7,3 z" fill="#94a3b8"/></marker>
  </defs>

  <!-- ══ MAC BOX ══ -->
  <rect x="18" y="18" width="318" height="706" rx="14" fill="#1e293b" stroke="#334155" stroke-width="1.5"/>
  <text x="36" y="44" fill="#64748b" font-size="10" font-weight="700" font-family="system-ui" letter-spacing="1.2">🖥  JULIAN'S MAC — HONG KONG</text>

  <!-- ══ CREDENTIAL LOADING SECTION ══ -->
  <text x="36" y="70" fill="#64748b" font-size="9" font-weight="700" font-family="system-ui" letter-spacing="1.2">CREDENTIAL LOADING  ·  STARTUP</text>

  <!-- credentials.json file box -->
  <rect x="44" y="80" width="268" height="72" rx="8" fill="#111827" stroke="#374151" stroke-width="1"/>
  <text x="68" y="98" fill="#9ca3af" font-size="11" font-weight="600" font-family="system-ui">~/.leadgen/credentials.json  🔐</text>
  <text x="68" y="113" fill="#475569" font-size="9" font-family="system-ui">RAPIDAPI_KEY · ANTHROPIC_API_KEY</text>
  <text x="68" y="125" fill="#475569" font-size="9" font-family="system-ui">SHEETS_AUTH_METHOD · GOOGLE_SERVICE_ACCOUNT_JSON</text>
  <text x="68" y="138" fill="#6b7280" font-size="8" font-family="system-ui">chmod 600 (owner only)</text>

  <!-- Arrow: credentials.json → credentials.py -->
  <path d="M 178,152 L 178,174" fill="none" stroke="#06b6d4" stroke-width="2" marker-end="url(#acyan)"/>
  <!-- Label -->
  <rect x="220" y="150" width="140" height="32" rx="4" fill="#0d1a25" opacity="0.95"/>
  <text x="290" y="161" fill="#06b6d4" font-size="8" font-weight="700" font-family="system-ui" text-anchor="middle">Read JSON file</text>
  <text x="290" y="173" fill="#06b6d4" font-size="8" font-family="system-ui" text-anchor="middle" opacity="0.7">Check for required keys</text>

  <!-- credentials.py loader box -->
  <rect x="44" y="174" width="268" height="76" rx="8" fill="#1a1a2e" stroke="#06b6d4" stroke-width="1.5"/>
  <text x="68" y="194" fill="#22d3ee" font-size="11" font-weight="600" font-family="system-ui">credentials.py  ·  CredentialManager.load()</text>
  <text x="68" y="209" fill="#475569" font-size="9" font-family="system-ui">1. Check os.environ for existing values</text>
  <text x="68" y="221" fill="#475569" font-size="9" font-family="system-ui">2. Load missing keys from JSON file</text>
  <text x="68" y="233" fill="#475569" font-size="9" font-family="system-ui">3. Inject into os.environ (called at script start)</text>

  <!-- Arrow: credentials.py → os.environ -->
  <path d="M 178,250 L 178,272" fill="none" stroke="#06b6d4" stroke-width="2" marker-end="url(#acyan)"/>
  <!-- Label -->
  <rect x="220" y="248" width="140" height="32" rx="4" fill="#0d1a25" opacity="0.95"/>
  <text x="290" y="259" fill="#06b6d4" font-size="8" font-weight="700" font-family="system-ui" text-anchor="middle">Inject into environment</text>
  <text x="290" y="271" fill="#06b6d4" font-size="8" font-family="system-ui" text-anchor="middle" opacity="0.7">Available to script at startup</text>

  <!-- os.environ box -->
  <rect x="44" y="272" width="268" height="68" rx="8" fill="#0f2a1a" stroke="#10b981" stroke-width="1.5"/>
  <text x="68" y="290" fill="#86efac" font-size="11" font-weight="600" font-family="system-ui">os.environ  (Shell Variables)</text>
  <text x="68" y="305" fill="#475569" font-size="9" font-family="system-ui">RAPIDAPI_KEY · ANTHROPIC_API_KEY</text>
  <text x="68" y="318" fill="#475569" font-size="9" font-family="system-ui">GOOGLE_SERVICE_ACCOUNT_JSON · SHEETS_AUTH_METHOD</text>

  <!-- Divider -->
  <line x1="30" y1="356" x2="336" y2="356" stroke="#334155" stroke-width="1"/>

  <!-- VPN BUBBLE — covers only ExpressVPN Engine + Claude Code -->
  <rect x="30" y="368" width="294" height="214" rx="10" fill="rgba(245,158,11,0.05)" stroke="#f59e0b" stroke-width="1.5" stroke-dasharray="6,4"/>
  <text x="44" y="386" fill="#f59e0b" font-size="9" font-weight="700" font-family="system-ui" letter-spacing="1.2">EXPRESSVPN TUNNEL  ·  LIGHTWAY / UDP 1194</text>

  <!-- ExpressVPN Engine box (Stage 1) -->
  <rect x="44" y="368" width="268" height="96" rx="8" fill="#1a1400" stroke="#ca8a04" stroke-width="1.5"/>
  <text x="68" y="388" fill="#fbbf24" font-size="12" font-weight="700" font-family="system-ui">ExpressVPN Engine</text>
  <text x="68" y="404" fill="#64748b" font-size="10" font-family="system-ui">Lightway · UDP 1194 (fallback TCP 443)</text>
  <text x="68" y="417" fill="#64748b" font-size="10" font-family="system-ui">Bypass rule: all IPs EXCEPT 160.79.104.0/21</text>
  <line x1="44" y1="425" x2="312" y2="425" stroke="#1a1400" stroke-width="1" opacity="0.6"/>
  <text x="68" y="438" fill="#475569" font-size="9" font-family="system-ui">Routes only Anthropic-bound traffic through the tunnel.</text>
  <text x="68" y="450" fill="#475569" font-size="9" font-family="system-ui">Everything else exits directly to the internet.</text>

  <!-- Claude Code box -->
  <rect x="44" y="470" width="268" height="108" rx="8" fill="#1e3a5f" stroke="#2563eb" stroke-width="1.5"/>
  <text x="68" y="492" fill="#93c5fd" font-size="13" font-weight="600" font-family="system-ui">Claude Code  🤖</text>
  <text x="68" y="508" fill="#64748b" font-size="10" font-family="system-ui">HTTPS · Port 443 · x-api-key auth</text>
  <text x="68" y="521" fill="#475569" font-size="9" font-family="system-ui">Routed THROUGH VPN (160.79.104.0/21)</text>
  <line x1="44" y1="529" x2="312" y2="529" stroke="#1e3a5f" stroke-width="1" opacity="0.6"/>
  <text x="68" y="542" fill="#475569" font-size="9" font-family="system-ui">The AI assistant interface. Sends your messages to</text>
  <text x="68" y="554" fill="#475569" font-size="9" font-family="system-ui">Anthropic and coordinates all skill/tool execution.</text>

  <!-- Python Scripts box (reads from os.environ) -->
  <rect x="44" y="584" width="268" height="120" rx="8" fill="#1a1a2e" stroke="#7c3aed" stroke-width="1.5"/>
  <text x="68" y="606" fill="#c4b5fd" font-size="13" font-weight="600" font-family="system-ui">Python Scripts  🐍</text>
  <text x="68" y="622" fill="#64748b" font-size="10" font-family="system-ui">HTTPS · Port 443 · RapidAPI + Anthropic auth</text>
  <text x="68" y="635" fill="#22c55e" font-size="9" font-family="system-ui">Non-Anthropic traffic BYPASSES VPN → goes direct</text>
  <line x1="44" y1="643" x2="312" y2="643" stroke="#1a1a2e" stroke-width="1" opacity="0.6"/>
  <text x="68" y="656" fill="#475569" font-size="9" font-family="system-ui">Reads RAPIDAPI_KEY, ANTHROPIC_API_KEY from env.</text>
  <text x="68" y="668" fill="#475569" font-size="9" font-family="system-ui">Fetches LinkedIn data, summarises with Haiku,</text>
  <text x="68" y="680" fill="#475569" font-size="9" font-family="system-ui">writes to Sheets. VPN for Anthropic; direct otherwise.</text>


  <!-- ══ RIGHT PANEL: External Services ══ -->

  <!-- VPN Exit Node (Stage 1) -->
  <rect x="614" y="342" width="348" height="100" rx="10" fill="#1a1400" stroke="#ca8a04" stroke-width="1.5"/>
  <text x="642" y="366" fill="#fbbf24" font-size="13" font-weight="600" font-family="system-ui">VPN Exit Node  (ExpressVPN Server)</text>
  <text x="642" y="382" fill="#64748b" font-size="10" font-family="system-ui">Lightway / UDP 1194 · Shared server IP</text>
  <text x="642" y="396" fill="#475569" font-size="9" font-family="system-ui">Only receives 160.79.104.0/21 traffic now</text>
  <line x1="614" y1="404" x2="962" y2="404" stroke="#1a1400" stroke-width="1" opacity="0.6"/>
  <text x="642" y="416" fill="#3d3010" font-size="9" font-family="system-ui">Acts as a proxy so Anthropic traffic appears to originate</text>
  <text x="642" y="428" fill="#3d3010" font-size="9" font-family="system-ui">outside Hong Kong, bypassing the regional block.</text>

  <!-- VPN ROUTED bubble — wraps VPN Exit Node + Anthropic API (mirrors left panel) -->
  <rect x="606" y="334" width="364" height="262" rx="12" fill="rgba(245,158,11,0.05)" stroke="#f59e0b" stroke-width="1.5" stroke-dasharray="6,4"/>
  <text x="622" y="350" fill="#f59e0b" font-size="9" font-weight="700" font-family="system-ui" letter-spacing="1.2">VPN ROUTED  ·  160.79.104.0/21</text>
  <rect x="614" y="460" width="348" height="120" rx="10" fill="#0f2a1a" stroke="#16a34a" stroke-width="1.5"/>
  <text x="642" y="486" fill="#86efac" font-size="13" font-weight="600" font-family="system-ui">Anthropic API  🧠</text>
  <text x="642" y="502" fill="#64748b" font-size="10" font-family="system-ui">api.anthropic.com · HTTPS · Port 443</text>
  <text x="642" y="516" fill="#64748b" font-size="10" font-family="system-ui">POST /v1/messages · Header: x-api-key</text>
  <text x="642" y="530" fill="#475569" font-size="9" font-family="system-ui">IP: 160.79.104.0/21 · Blocked in HK without VPN</text>
  <line x1="614" y1="538" x2="962" y2="538" stroke="#0f2a1a" stroke-width="1" opacity="0.6"/>
  <text x="642" y="550" fill="#375d47" font-size="9" font-family="system-ui">The Claude AI model endpoint. Receives prompts and</text>
  <text x="642" y="562" fill="#375d47" font-size="9" font-family="system-ui">returns generated text — used by both Claude Code and scripts.</text>
  <rect x="892" y="468" width="58" height="18" rx="9" fill="#16a34a"/>
  <text x="921" y="481" fill="white" font-size="10" font-weight="700" font-family="system-ui" text-anchor="middle">WORKS ✓</text>

  <!-- RapidAPI -->
  <rect x="614" y="598" width="348" height="128" rx="10" fill="#1a0f0f" stroke="#7c3aed" stroke-width="1.5"/>
  <text x="642" y="622" fill="#c4b5fd" font-size="13" font-weight="600" font-family="system-ui">RapidAPI — Fresh LinkedIn Scraper  ⚡</text>
  <text x="642" y="638" fill="#64748b" font-size="10" font-family="system-ui">fresh-linkedin-scraper-api.p.rapidapi.com</text>
  <text x="642" y="652" fill="#64748b" font-size="10" font-family="system-ui">HTTPS · Port 443 · GET /api/v1/user/...</text>
  <text x="642" y="666" fill="#64748b" font-size="10" font-family="system-ui">Headers: x-rapidapi-key · x-rapidapi-host</text>
  <text x="642" y="680" fill="#22c55e" font-size="9" font-family="system-ui">Was blocked via VPN · Now direct ✓  (4 credits/lead)</text>
  <line x1="614" y1="688" x2="962" y2="688" stroke="#1a0f0f" stroke-width="1" opacity="0.6"/>
  <text x="642" y="700" fill="#3d2d4a" font-size="9" font-family="system-ui">Scrapes public LinkedIn profiles. Returns profile info,</text>
  <text x="642" y="712" fill="#3d2d4a" font-size="9" font-family="system-ui">work history, education and recent posts as JSON.</text>
  <rect x="888" y="606" width="62" height="18" rx="9" fill="#16a34a"/>
  <text x="919" y="619" fill="white" font-size="10" font-weight="700" font-family="system-ui" text-anchor="middle">FIXED ✓</text>

  <!-- Google Sheets -->
  <rect x="614" y="744" width="348" height="110" rx="10" fill="#1a2a0f" stroke="#65a30d" stroke-width="1.5"/>
  <text x="642" y="768" fill="#bef264" font-size="13" font-weight="600" font-family="system-ui">Google Sheets API  📊</text>
  <text x="642" y="784" fill="#64748b" font-size="10" font-family="system-ui">sheets.googleapis.com · HTTPS · Port 443</text>
  <text x="642" y="798" fill="#64748b" font-size="10" font-family="system-ui">Service Account JWT · GET + PUT /v4/spreadsheets/...</text>
  <text x="642" y="812" fill="#475569" font-size="9" font-family="system-ui">Bypasses VPN · Google tolerates direct HK traffic</text>
  <line x1="614" y1="820" x2="962" y2="820" stroke="#1a2a0f" stroke-width="1" opacity="0.6"/>
  <text x="642" y="832" fill="#2d4020" font-size="9" font-family="system-ui">Stores the lead list. Script reads rows pending enrichment</text>
  <text x="642" y="844" fill="#2d4020" font-size="9" font-family="system-ui">and writes summaries and status flags back when done.</text>
  <rect x="888" y="752" width="62" height="18" rx="9" fill="#65a30d"/>
  <text x="919" y="765" fill="white" font-size="10" font-weight="700" font-family="system-ui" text-anchor="middle">WORKS ✓</text>


  <!-- ══ CREDENTIAL LOADING ARROWS ══ -->
  <!-- Arrow from os.environ to Python Scripts (right side) -->
  <path d="M 312,306 L 614,644" fill="none" stroke="#06b6d4" stroke-width="1.5" stroke-dasharray="4,3" opacity="0.6" marker-end="url(#acyan)"/>
  <text x="450" y="478" fill="#06b6d4" font-size="8" font-weight="600" font-family="system-ui" opacity="0.8">RAPIDAPI_KEY, ANTHROPIC_API_KEY</text>

  <!-- Arrow from os.environ to Google Sheets (right side) -->
  <path d="M 312,306 L 614,799" fill="none" stroke="#06b6d4" stroke-width="1.5" stroke-dasharray="4,3" opacity="0.6" marker-end="url(#acyan)"/>
  <text x="450" y="562" fill="#06b6d4" font-size="8" font-weight="600" font-family="system-ui" opacity="0.8">GOOGLE_SERVICE_ACCOUNT_JSON</text>

  <!-- ══ ARROWS — BIDIRECTIONAL with Stage Badges ══
       Solid path  = outbound (client initiates, dst :443)
       Dashed path = return   (server responds, dst :ephem 49152-65535)
       Forward paths offset -7px, return paths offset +7px vertically
  -->

  <!-- ─── Stage 2: Claude Code ↔ Anthropic API (via VPN) ─── -->
  <!-- outbound → :443 -->
  <path d="M 314,501 Q 463,485 612,469" fill="none" stroke="#16a34a" stroke-width="2" marker-end="url(#ag)"/>
  <!-- return ← :ephem -->
  <path d="M 612,483 Q 463,499 314,515" fill="none" stroke="#16a34a" stroke-width="1.5" stroke-dasharray="5,3" opacity="0.7" marker-end="url(#ag)"/>
  <!-- Stage badge -->
  <circle cx="326" cy="508" r="10" fill="#16a34a"/>
  <text x="326" y="512" fill="white" font-size="9" font-weight="700" font-family="system-ui" text-anchor="middle">2</text>
  <!-- Labels -->
  <rect x="400" y="470" width="126" height="32" rx="4" fill="#050e09" opacity="0.95"/>
  <text x="463" y="481" fill="#16a34a" font-size="8" font-weight="700" font-family="system-ui" text-anchor="middle">→ :443  HTTPS · via VPN</text>
  <text x="463" y="493" fill="#16a34a" font-size="8" font-family="system-ui" text-anchor="middle" opacity="0.65">← :49152–65535  ephemeral</text>

  <!-- ─── Stage 3a: Python Scripts ↔ RapidAPI (direct) ─── -->
  <!-- outbound → :443 -->
  <path d="M 314,623 Q 463,615 612,607" fill="none" stroke="#c4b5fd" stroke-width="2" marker-end="url(#ap)"/>
  <!-- return ← :ephem -->
  <path d="M 612,621 Q 463,629 314,637" fill="none" stroke="#c4b5fd" stroke-width="1.5" stroke-dasharray="5,3" opacity="0.7" marker-end="url(#ap)"/>
  <!-- Stage badge -->
  <circle cx="326" cy="630" r="10" fill="#7c3aed"/>
  <text x="326" y="634" fill="white" font-size="8" font-weight="700" font-family="system-ui" text-anchor="middle">3a</text>
  <!-- Labels -->
  <rect x="400" y="602" width="126" height="32" rx="4" fill="#0d0a18" opacity="0.95"/>
  <text x="463" y="613" fill="#c4b5fd" font-size="8" font-weight="700" font-family="system-ui" text-anchor="middle">→ :443  HTTPS · direct</text>
  <text x="463" y="625" fill="#c4b5fd" font-size="8" font-family="system-ui" text-anchor="middle" opacity="0.65">← :49152–65535  ephemeral</text>

  <!-- ─── Stage 3b: Python Scripts ↔ Anthropic API LLM (via VPN) ─── -->
  <!-- outbound → :443 -->
  <path d="M 314,648 Q 420,580 612,510" fill="none" stroke="#16a34a" stroke-width="1.5" stroke-dasharray="3,3" opacity="0.65" marker-end="url(#ag)"/>
  <!-- return ← :ephem -->
  <path d="M 612,524 Q 420,596 314,662" fill="none" stroke="#16a34a" stroke-width="1.2" stroke-dasharray="2,4" opacity="0.45" marker-end="url(#ag)"/>
  <!-- Stage badge -->
  <circle cx="326" cy="652" r="9" fill="#166534" stroke="#16a34a" stroke-width="1"/>
  <text x="326" y="656" fill="#86efac" font-size="7" font-weight="700" font-family="system-ui" text-anchor="middle">3b</text>
  <!-- Label at curve midpoint -->
  <rect x="390" y="548" width="126" height="32" rx="4" fill="#050e09" opacity="0.95"/>
  <text x="453" y="559" fill="#16a34a" font-size="8" font-weight="700" font-family="system-ui" text-anchor="middle">→ :443  HTTPS · via VPN</text>
  <text x="453" y="571" fill="#16a34a" font-size="8" font-family="system-ui" text-anchor="middle" opacity="0.65">← :49152–65535  ephemeral</text>

  <!-- ─── Stage 4: Python Scripts ↔ Google Sheets API (direct) ─── -->
  <!-- outbound → :443 -->
  <path d="M 314,665 Q 463,704 612,743" fill="none" stroke="#65a30d" stroke-width="2" marker-end="url(#al)"/>
  <!-- return ← :ephem -->
  <path d="M 612,757 Q 463,718 314,679" fill="none" stroke="#65a30d" stroke-width="1.5" stroke-dasharray="5,3" opacity="0.7" marker-end="url(#al)"/>
  <!-- Stage badge -->
  <circle cx="326" cy="672" r="10" fill="#4d7c0f"/>
  <text x="326" y="676" fill="white" font-size="9" font-weight="700" font-family="system-ui" text-anchor="middle">4</text>
  <!-- Labels -->
  <rect x="400" y="698" width="126" height="32" rx="4" fill="#060c04" opacity="0.95"/>
  <text x="463" y="709" fill="#65a30d" font-size="8" font-weight="700" font-family="system-ui" text-anchor="middle">→ :443  HTTPS · direct</text>
  <text x="463" y="721" fill="#65a30d" font-size="8" font-family="system-ui" text-anchor="middle" opacity="0.65">← :49152–65535  ephemeral</text>


  <!-- ─── Stage 1: VPN Client ↔ VPN Exit Node (UDP tunnel) ─── -->
  <!-- outbound → :1194 UDP -->
  <path d="M 314,408 Q 463,375 612,342" fill="none" stroke="#ca8a04" stroke-width="2" marker-end="url(#ay)"/>
  <!-- return ← :ephem UDP -->
  <path d="M 612,356 Q 463,389 314,422" fill="none" stroke="#ca8a04" stroke-width="1.5" stroke-dasharray="5,3" opacity="0.7" marker-end="url(#ay)"/>
  <!-- Stage badge -->
  <circle cx="326" cy="415" r="10" fill="#92400e"/>
  <text x="326" y="419" fill="white" font-size="9" font-weight="700" font-family="system-ui" text-anchor="middle">1</text>
  <!-- Labels -->
  <rect x="400" y="310" width="130" height="32" rx="4" fill="#100c00" opacity="0.95"/>
  <text x="465" y="321" fill="#ca8a04" font-size="8" font-weight="700" font-family="system-ui" text-anchor="middle">→ UDP :1194  Lightway tunnel</text>
  <text x="465" y="333" fill="#ca8a04" font-size="8" font-family="system-ui" text-anchor="middle" opacity="0.65">← UDP :ephem  tunnel response</text>

  <!-- Arrow direction legend (bottom centre) -->
  <rect x="340" y="868" width="300" height="26" rx="6" fill="#1e293b" opacity="0.8"/>
  <line x1="356" y1="881" x2="386" y2="881" stroke="#94a3b8" stroke-width="1.5" marker-end="url(#agrey)"/>
  <text x="393" y="885" fill="#94a3b8" font-size="9" font-family="system-ui">outbound  (client → :443)</text>
  <line x1="496" y1="881" x2="526" y2="881" stroke="#94a3b8" stroke-width="1.5" stroke-dasharray="4,3" marker-end="url(#agrey)"/>
  <text x="533" y="885" fill="#94a3b8" font-size="9" font-family="system-ui">return  (← :ephem)</text>

</svg>

<!-- ═══════════════════════════════ CREDENTIAL TABLE -->
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
      <td><code>RAPIDAPI_KEY</code></td>
      <td><code>~/.leadgen/credentials.json</code></td>
      <td>credentials.py @ script start<br><span class="dim">injected into os.environ</span></td>
      <td>Python Scripts<br><span class="dim">linkedin_enricher.py</span></td>
      <td class="why">Authenticates requests to RapidAPI Fresh LinkedIn Scraper endpoint. Passed as <code>x-rapidapi-key</code> header in GET requests for profile, experience, education, posts.</td>
      <td><span class="tag tag-amber">SECRET</span><br>chmod 600<br>Hidden in env</td>
    </tr>
    <tr>
      <td><code>ANTHROPIC_API_KEY</code></td>
      <td><code>~/.leadgen/credentials.json</code></td>
      <td>credentials.py @ script start<br><span class="dim">injected into os.environ</span></td>
      <td>Python Scripts<br><span class="dim">linkedin_enricher.py</span><br>Claude Code<br><span class="dim">API calls</span></td>
      <td class="why">Authenticates requests to Anthropic API for Claude Haiku LLM summarization (Stage 3b). Python script sends raw LinkedIn data and receives profile/posts summaries.</td>
      <td><span class="tag tag-amber">SECRET</span><br>chmod 600<br>Routed via VPN</td>
    </tr>
    <tr>
      <td><code>GOOGLE_SERVICE_ACCOUNT_JSON</code></td>
      <td><code>~/.leadgen/credentials.json</code> (path ref)</td>
      <td>credentials.py @ script start<br><span class="dim">file path injected into os.environ</span></td>
      <td>Python Scripts<br><span class="dim">gsheets_store.py</span></td>
      <td class="why">Service account JWT file for Google Sheets API authentication. Loaded at runtime by gspread library to generate Bearer tokens. Enables reading pending lead rows and writing enrichment results.</td>
      <td><span class="tag tag-amber">SECRET</span><br>chmod 600<br>File-based</td>
    </tr>
    <tr>
      <td><code>SHEETS_AUTH_METHOD</code></td>
      <td><code>~/.leadgen/credentials.json</code></td>
      <td>credentials.py @ script start<br><span class="dim">injected into os.environ</span></td>
      <td>Python Scripts<br><span class="dim">gsheets_store.py</span></td>
      <td class="why">Determines which Google Sheets auth method to use: "service_account" or "oauth". Currently set to "service_account" which loads the JWT file.</td>
      <td><span class="tag tag-green">NOT SECRET</span><br>chmod 600<br>Config value</td>
    </tr>
  </tbody>
</table>

<!-- ═════════════════════════════════ DETAILED FLOW TABLE -->
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
      <td>ExpressVPN Client</td>
      <td>VPN Exit Node<br><span class="dim">ExpressVPN server</span></td>
      <td><span class="proto">Lightway (WireGuard-based)</span></td>
      <td><span class="port">UDP 1194<br><span class="dim">fallback TCP 443</span></span></td>
      <td><span class="auth">Certificate + shared key</span></td>
      <td>VPN tunnel only<br><span class="dim">Only 160.79.104.0/21</span></td>
      <td class="why">This is established first — before any other communication can occur. Anthropic's IP range (160.79.104.0/21) is blocked in Hong Kong, so a persistent tunnel is opened to an ExpressVPN exit node in another country. Lightway uses UDP 1194 for speed; it falls back to TCP 443 if UDP is blocked. All non-Anthropic traffic bypasses this tunnel via the IP exclusion rule.</td>
      <td><span class="tag tag-amber">FIRST ✓</span></td>
    </tr>
    <tr>
      <td><strong>2</strong></td>
      <td>Claude Code</td>
      <td><code>api.anthropic.com</code><br><span class="dim">160.79.104.0/21</span></td>
      <td><span class="proto">HTTPS / TLS 1.3</span></td>
      <td><span class="port">443</span></td>
      <td><span class="auth">x-api-key header</span></td>
      <td>Through VPN<br><span class="dim">Lightway · UDP 1194</span></td>
      <td class="why">Once the VPN tunnel (Stage 1) is up, Claude Code can reach Anthropic. Every user message is sent here and the AI response comes back through the same tunnel. Port 443 is the only port Anthropic accepts; the VPN carries it because the destination IP is blocked in Hong Kong.</td>
      <td><span class="tag tag-green">WORKS ✓</span></td>
    </tr>
    <tr>
      <td><strong>3a</strong></td>
      <td>Python Script<br><span class="dim">linkedin_enricher.py</span></td>
      <td><code>fresh-linkedin-scraper-api.p.rapidapi.com</code><br><span class="dim">GET /api/v1/user/profile, /experience, /educations, /posts</span></td>
      <td><span class="proto">HTTPS / TLS 1.3</span></td>
      <td><span class="port">443</span></td>
      <td><span class="auth">x-rapidapi-key<br>x-rapidapi-host headers</span></td>
      <td>Direct — bypasses VPN<br><span class="dim">All non-Anthropic IPs</span></td>
      <td class="why">The script fetches raw LinkedIn data for each lead — profile, work history, education and recent posts. Four separate API calls per lead (4 credits total). Traffic goes direct because VPN exit node IPs were being blocked by RapidAPI; the IP exclusion rule now sends this straight to the internet.</td>
      <td><span class="tag tag-green">FIXED ✓</span></td>
    </tr>
    <tr>
      <td><strong>3b</strong></td>
      <td>Python Script<br><span class="dim">linkedin_enricher.py</span></td>
      <td><code>api.anthropic.com</code><br><span class="dim">POST /v1/messages — Claude Haiku 4.5</span></td>
      <td><span class="proto">HTTPS / TLS 1.3</span></td>
      <td><span class="port">443</span></td>
      <td><span class="auth">x-api-key header</span></td>
      <td>Through VPN<br><span class="dim">160.79.104.0/21</span></td>
      <td class="why">After fetching the raw LinkedIn data, the script sends it to Claude Haiku to generate a human-readable profile summary and posts narrative for cold email outreach. Same API endpoint as Stage 2, called programmatically. Routed through the VPN tunnel established in Stage 1.</td>
      <td><span class="tag tag-green">WORKS ✓</span></td>
    </tr>
    <tr>
      <td><strong>4</strong></td>
      <td>Python Script<br><span class="dim">gsheets_store.py</span></td>
      <td><code>sheets.googleapis.com</code><br><span class="dim">GET + PUT /v4/spreadsheets/{id}/values</span></td>
      <td><span class="proto">HTTPS / TLS 1.3</span></td>
      <td><span class="port">443</span></td>
      <td><span class="auth">Service Account JWT<br>or OAuth2 token</span></td>
      <td>Direct — bypasses VPN<br><span class="dim">Google tolerates HK direct</span></td>
      <td class="why">Google Sheets is the pipeline's data store. The script reads it at the start to find pending rows, then writes the generated summaries and status flags back after each lead is enriched. Google's API only operates over HTTPS/443 and tolerates direct connections from Hong Kong.</td>
      <td><span class="tag tag-green">WORKS ✓</span></td>
    </tr>
  </tbody>
</table>

<!-- ═════════════════════════════════ CREDENTIAL LOADING PROCESS -->
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
      <td>User can pre-set via shell (export RAPIDAPI_KEY=...)</td>
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
      <td>Python Scripts<br><code>linkedin_enricher.py</code></td>
      <td>Read credentials from environment</td>
      <td>After CredentialManager.load() completes</td>
      <td><code>os.environ.get("RAPIDAPI_KEY")</code> → returns value for API headers</td>
    </tr>
    <tr>
      <td><strong>6</strong></td>
      <td>Python Scripts<br><code>linkedin_enricher.py</code></td>
      <td>Make API calls with credentials</td>
      <td>Credentials injected into request headers</td>
      <td><code>headers = {"x-rapidapi-key": os.environ["RAPIDAPI_KEY"]}</code> → Stage 3a request</td>
    </tr>
    <tr>
      <td><strong>7</strong></td>
      <td>Python Scripts<br><code>gsheets_store.py</code></td>
      <td>Load Google service account file</td>
      <td>Path from <code>os.environ["GOOGLE_SERVICE_ACCOUNT_JSON"]</code></td>
      <td>gspread library reads JWT file → generates Bearer token → Stage 4 request</td>
    </tr>
  </tbody>
</table>

<!-- ═════════════════════════════════ ENDPOINT REFERENCE -->
<p class="section-title">API Endpoint Reference</p>
<table>
  <thead>
    <tr><th>Call</th><th>Method</th><th>Endpoint</th><th>Key Headers / Params</th><th>Cost</th></tr>
  </thead>
  <tbody>
    <tr>
      <td>Profile fetch</td>
      <td><span class="tag tag-blue">GET</span></td>
      <td><code>/api/v1/user/profile?username=X</code></td>
      <td><code>x-rapidapi-key</code> · <code>x-rapidapi-host</code></td>
      <td>1 credit</td>
    </tr>
    <tr>
      <td>Experience fetch</td>
      <td><span class="tag tag-blue">GET</span></td>
      <td><code>/api/v1/user/experience?username=X</code></td>
      <td><code>x-rapidapi-key</code> · <code>x-rapidapi-host</code></td>
      <td>1 credit</td>
    </tr>
    <tr>
      <td>Education fetch</td>
      <td><span class="tag tag-blue">GET</span></td>
      <td><code>/api/v1/user/educations?username=X</code></td>
      <td><code>x-rapidapi-key</code> · <code>x-rapidapi-host</code></td>
      <td>1 credit</td>
    </tr>
    <tr>
      <td>Posts fetch</td>
      <td><span class="tag tag-blue">GET</span></td>
      <td><code>/api/v1/user/posts?username=X</code></td>
      <td><code>x-rapidapi-key</code> · <code>x-rapidapi-host</code></td>
      <td>1 credit</td>
    </tr>
    <tr>
      <td>LLM summary</td>
      <td><span class="tag tag-purple">POST</span></td>
      <td><code>https://api.anthropic.com/v1/messages</code></td>
      <td><code>x-api-key</code> · <code>anthropic-version: 2023-06-01</code> · model: claude-haiku-4-5</td>
      <td>~$0.001</td>
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

- **No external dependencies** — the HTML file is self-contained (all CSS and SVG inline)
- **Dark theme** — optimized for viewing in a dark terminal or night mode
- **Responsive SVG** — scales to fill the browser window while maintaining aspect ratio
- **Browser compatibility** — works in all modern browsers (Chrome, Safari, Firefox, Edge)

---

## Version History

- **2026-04-29**: Initial version. Complete architecture diagram with credential loading flow, VPN tunnel boundaries, 4 communication stages, and supporting tables.
