> Mirror copy. Source: `~/.codex/config.toml`. No secrets present (auth lives in `~/.codex/auth.json`, which is omitted).

```toml
model = "gpt-5.5"
model_reasoning_effort = "medium"


notify = ["/Users/julianhart/.codex/computer-use/Codex Computer Use.app/Contents/SharedSupport/SkyComputerUseClient.app/Contents/MacOS/SkyComputerUseClient", "turn-ended"]

[marketplaces.openai-bundled]
last_updated = "2026-07-03T03:54:56Z"
source_type = "local"
source = "/Users/julianhart/.codex/.tmp/bundled-marketplaces/openai-bundled"

[marketplaces.openai-primary-runtime]
last_updated = "2026-07-03T04:30:28Z"
source_type = "local"
source = "/Users/julianhart/.cache/codex-runtimes/codex-primary-runtime/plugins/openai-primary-runtime"

[plugins."documents@openai-primary-runtime"]
enabled = true

[plugins."spreadsheets@openai-primary-runtime"]
enabled = true

[plugins."presentations@openai-primary-runtime"]
enabled = true

[plugins."computer-use@openai-bundled"]
enabled = true

[plugins."pdf@openai-primary-runtime"]
enabled = true

[plugins."template-creator@openai-primary-runtime"]
enabled = true

[plugins."browser@openai-bundled"]
enabled = true

[projects."/Users/julianhart/Documents/Codex/2026-06-06/what-subscription-do-i-current-y"]
trust_level = "trusted"

[projects."/"]
trust_level = "trusted"

[projects."/Users/julianhart/Obsidian Vault"]
trust_level = "trusted"

[tool_suggest]
disabled_tools = [{ type = "plugin", id = "google-drive@openai-curated" }]

[desktop]
ambient-suggestions-enabled = false
conversationDetailMode = "STEPS_PROSE"
followUpQueueMode = "queue"

[features]
js_repl = false

[mcp_servers.node_repl]
command = "/Applications/Codex.app/Contents/Resources/cua_node/bin/node_repl"
startup_timeout_sec = 120.0

[mcp_servers.node_repl.env]
BROWSER_USE_AVAILABLE_BACKENDS = "chrome,iab"
BROWSER_USE_CODEX_APP_BUILD_FLAVOR = "prod"
BROWSER_USE_CODEX_APP_VERSION = "26.623.61825"
CODEX_CLI_PATH = "/Applications/Codex.app/Contents/Resources/codex"
CODEX_HOME = "/Users/julianhart/.codex"
NODE_REPL_INSTRUCTIONS_USE_CASE_BROWSER = "Control the in-app browser in conjunction with the Browser Plugin."
NODE_REPL_INSTRUCTIONS_USE_CASE_CHROME = "Control the Chrome browser in conjunction with the Chrome Plugin. Prefer this method of controlling Chrome over alternatives (such as Computer Use) unless the user explicitly mentions an alternative."
NODE_REPL_NATIVE_PIPE_CONNECT_TIMEOUT_MS = "1000"
NODE_REPL_NODE_MODULE_DIRS = "/Applications/Codex.app/Contents/Resources/cua_node/lib/node_modules"
NODE_REPL_NODE_PATH = "/Applications/Codex.app/Contents/Resources/cua_node/bin/node"
NODE_REPL_TRUSTED_BROWSER_CLIENT_SHA256S = "a05cdd282c2717f076e11bc0e94b7b20e1fc4759dbe28440bd1c734953606a56"
NODE_REPL_TRUSTED_CODE_PATHS = "/Users/julianhart/.codex"
```
