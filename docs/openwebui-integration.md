# OpenWebUI Integration Notes

OpenWebUI currently works better with Pipintama through `OpenAPI` than through its experimental MCP path.

## Use this endpoint

- `https://api.pipintama.com/openapi.json`

Authenticate with:

- `Authorization: Bearer <PIPINTAMA_API_KEY>`

## Recommended split

- `OpenClaw` and `Claude Code`: use the hosted MCP endpoint
- `OpenWebUI`: use the OpenAPI adapter

## OpenWebUI setup

1. Open `Settings`
2. Open `Integrations`
3. Open `Manage Tool Servers`
4. Add a new connection
5. Use:
   - `Type`: `OpenAPI`
   - `Name`: `Pipintama`
   - `Description`: `Pipintama Boards and Charts`
   - `URL`: `https://api.pipintama.com/openapi.json`
   - `Auth`: `Bearer`
   - `API Key`: your Pipintama API key
6. Save the connection

## What this gives you

Boards:

- `GET /openapi/boards/modes`
- `POST /openapi/boards/create`
- `GET /openapi/boards/{boardId}`
- `POST /openapi/boards/update`
- `POST /openapi/boards/share`
- `POST /openapi/boards/export-png`

Charts:

- `GET /openapi/charts/modes`
- `POST /openapi/charts/create`
- `GET /openapi/charts/{chartId}`
- `POST /openapi/charts/update`
- `POST /openapi/charts/share`
- `POST /openapi/charts/export-png`

## Workspace rule

Do not force `workspaceId` unless the user explicitly provides one.

The authenticated Pipintama API key determines the workspace automatically.

## Skill routing guidance

Use `Boards` for:

- mindmaps
- flowcharts
- kanban boards
- architecture diagrams
- structured visual planning

Use `Charts` for:

- line charts
- bar charts
- pie charts
- radar charts
- trends
- category comparison
- distributions

## Troubleshooting

- If OpenWebUI MCP says it is trying to connect to an `openAPI tool server`, use the OpenAPI path instead of the MCP path.
- If the request returns `401`, verify the Bearer API key.
- If a board or chart does not show in `/platform`, confirm the request used the API key from that user's workspace.
