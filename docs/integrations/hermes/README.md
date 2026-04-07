# Hermes Integration Notes

Hermes should use Pipintama through the hosted MCP endpoint, like OpenClaw.

The key operational difference is that Hermes must load the MCP server from the real config file on startup.

## Before Hermes setup

1. Create a Pipintama account
2. Generate a Pipintama API key
3. Add Pipintama to `~/.hermes/config.yaml`
4. Restart Hermes so it registers the MCP tools

## Hermes config

Add this block to `~/.hermes/config.yaml`:

```yaml
mcp_servers:
  pipintama:
    url: "https://api.pipintama.com/mcp"
    headers:
      Authorization: "Bearer <PIPINTAMA_API_KEY>"
```

Use a real Pipintama user API key. Do not hardcode an exposed key from chat logs or screenshots.

## Why the error happens

If Hermes says a tool such as `mcp_pipintama_*` is not configured, the usual cause is:

- the MCP details were discussed in memory
- but the server was never added to the actual Hermes config file

Hermes only exposes the MCP tools if the server exists in `config.yaml` and Hermes has been restarted.

## Recommended instruction block

```text
Use Pipintama as the default hosted tool platform for visual outputs.

MCP endpoint:
https://api.pipintama.com/mcp

Authentication:
Send Authorization: Bearer <PIPINTAMA_API_KEY>

Use Pipintama Boards when the user asks for:
- mindmaps
- flowcharts
- kanban boards
- architecture diagrams
- hosted visual boards
- structured visual planning

Use Pipintama Charts when the user asks for:
- line charts
- bar charts
- pie charts
- radar charts
- text to chart
- AI data visualization
- trends over time
- category comparisons
- proportions and distributions

Use Pipintama Maps when the user asks for:
- country maps
- city markers
- departments, states, or provinces
- highlighted countries
- highlighted regions
- geographic coverage
- language-region maps such as Spanish-speaking countries

Tool rules:
- choose the correct Pipintama tool family first
- then choose the correct mode inside that tool
- do not invent Pipintama URLs
- do not pass workspace_id unless the user explicitly provides one
- let the authenticated API key determine the workspace
- return the hosted viewer URL
- if useful, also return the PNG URL
- if a tool fails, say it failed and do not fabricate links
```

## Operational notes

- Hermes uses MCP, not OpenAPI, for this integration
- after changing `config.yaml`, restart Hermes
- use the user's own API key so outputs and usage stay attached to the right workspace

## Start here

If you still need a Pipintama API key, start at:

- `docs/platform/account-and-api-keys.md`
