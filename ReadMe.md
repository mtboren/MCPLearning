# MCP Learning

Repository of the goodness (example code and learning materials) from exploring the Model Context Protocol (MCP). The codebase includes a simple MCP client and server, utilities, and example chat integrations used while following the MCP introductory course.

## Project layout
- `src/` — main example code and runnable scripts.


This repo was created while working through the "Introduction to Model Context Protocol" course from Anthropic. The course introduces MCP fundamentals, client/server patterns, message formats, and step-by-step examples to help you build MCP-aware applications.

### Course link

- https://anthropic.skilljar.com/introduction-to-model-context-protocol/

## Quick notes
- See `src/README.md` for code-specific notes and run instructions

## MCP Inspector in GitHub Codespaces
To succeed with using MCP Inspector web UI in a GitHub Codespaces container, Matt found that you just need to make a few adjustments:

- Allow the public (non-local) web-based origin of the MCP proxy (codespace-name-6277.app.github.dev, for example) to access the MCP server; do so by prefixing the `mcp dev ...` command with a temporary environment variable `ALLOWED_ORIGINS`
    - Example command (all one line) to set this env var and to start the MCP server (uses the current Codespace name and port-forwarding domain):
        ```bash
        ALLOWED_ORIGINS="https://${CODESPACE_NAME}-6274.${GITHUB_CODESPACES_PORT_FORWARDING_DOMAIN}" uv run mcp dev ./mcp_server.py
        ```
- Make MCP proxy server port accessible (change port "visibility" in the Codespace container):  change the visibility of the forwarded port for the proxy (default `6277`) to `public` (in the `PORTS` tab of the VS Code's Terminal pane)
- Set the `Inspector Proxy Address` value in the Inspector Web UI to the actual value of the address of the Codespace's forwarded port (can find this in the aforementioned `PORTS` tab); ex: `https://my-cool-codespace-46w694q65rc5g69-6277.app.github.dev`
    - ⚠️ **Note**: at the time of writing, you must have _no_ trailing slash on the URL -- using a trailing slash (as copied from the `PORTS` tab) will result in failure for the Inspector web UI to connect to the Inspector proxy
- Set the `Proxy Session Token` value in the Inspector Web UI to the "🔑 Session token" value reported at MCP server startup. Theoretically, adding the `?MCP_PROXY_AUTH_TOKEN=...` query string to the inspector URL will set said proxy session token -- try it out!
- ⚠️ And, of course:  be safe and secure out there -- if there is any concern about privacy / security with temporarily exposing the MCP proxy port publicly, do not doit! You can still use a GitHub Codespace container for the development -- just connect your _local_ VSCode editor to the remote Codespace, then all of the `localhost` / `127.0.0.1` addresses will work as expected and desired. The helpful hints above are for enabling fully-web-based exploration, for if/when that is useful.