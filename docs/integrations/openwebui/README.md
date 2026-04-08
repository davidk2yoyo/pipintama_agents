# OpenWebUI Integration Notes

OpenWebUI currently works better with Pipintama through `OpenAPI` than through its experimental MCP path.

## Use this endpoint

- `https://api.pipintama.com/openapi.json`

Authenticate with:

- `Authorization: Bearer <PIPINTAMA_API_KEY>`

## Before OpenWebUI setup

1. Create a Pipintama account
2. Generate a Pipintama API key in the platform
3. Use that key in the OpenWebUI tool server config

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
   - `Description`: `Pipintama Boards, Charts, Maps, and Forms`
   - `URL`: `https://api.pipintama.com/openapi.json`
   - `Auth`: `Bearer`
   - `API Key`: your Pipintama API key
6. Save the connection

## Use separate skills

Do not mix all Pipintama behavior into one huge prompt.

Use one instruction block or skill per tool:

- `docs/integrations/openwebui/boards-skill.md`
- `docs/integrations/openwebui/charts-skill.md`
- `docs/integrations/openwebui/maps-skill.md`
- `docs/integrations/openwebui/forms-skill.md`

That reduces fake routes, wrong output formats, and wrong tool selection.

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

Maps:

- `GET /openapi/maps/modes`
- `POST /openapi/maps/create`
- `GET /openapi/maps/{mapId}`
- `POST /openapi/maps/update`
- `POST /openapi/maps/share`
- `POST /openapi/maps/export-png`

Forms:

- `GET /openapi/forms/modes`
- `POST /openapi/forms/create`
- `GET /openapi/forms/{formId}`
- `POST /openapi/forms/update`
- `POST /openapi/forms/share`
- `GET /openapi/forms/{formId}/responses`

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

Use `Maps` for:

- country highlights
- city markers
- departments, states, and provinces
- highlighted regions
- geographic coverage

Use `Forms` for:

- forms
- polls
- surveys
- lead capture
- onboarding and intake
- feedback collection

## Troubleshooting

- If OpenWebUI MCP says it is trying to connect to an `openAPI tool server`, use the OpenAPI path instead of the MCP path.
- If the request returns `401`, verify the Bearer API key.
- If a board, chart, map, or form does not show in `/platform`, confirm the request used the API key from that user's workspace.
- For `Maps`, prefer more structured prompts than Charts. Send `type`, `title`, and explicit fields like `cityNames`, `countryName`, or `regionNames`.
- For `Forms`, remember the pattern is create form -> share form URL -> collect responses -> review results page or `GET /openapi/forms/{formId}/responses`.
