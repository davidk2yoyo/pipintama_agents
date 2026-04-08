# Pipintama MCP Overview

Pipintama exposes one hosted MCP endpoint that currently serves `Boards`, `Charts`, `Maps`, and `Forms`.

For clients that behave more reliably with OpenAPI than MCP, Pipintama also exposes:

- `https://api.pipintama.com/openapi.json`

## Purpose

Pipintama exposes a hosted MCP server so agents can create and retrieve visual outputs without needing access to the product codebase or private VPS internals.

Live endpoint:

- `https://api.pipintama.com/mcp`

Health check:

- `https://api.pipintama.com/mcp-health`

## Authentication

The hosted MCP is not anonymous.

- remote clients authenticate with a Pipintama API key
- clients can send it through `Authorization: Bearer <key>` or `x-api-key`
- usage is attributed to the authenticated client id and name
- OAuth is planned later for user-scoped access across multiple Pipintama tools

## Supported tools

### Board tools

### `list_board_modes`

Return the supported board types and when to use each one.

### `create_board`

Create a board from user text and return a hosted viewer URL.

Input shape:

```json
{
  "title": "Launch Workflow",
  "board_type": "flowchart",
  "source_text": "Capture request. Validate inputs. Generate board. Return hosted URL.",
  "visibility": "shared"
}
```

When the MCP request is authenticated with a Pipintama API key, let the platform resolve the workspace from that key. Do not force an older demo `workspace_id` unless the workflow explicitly requires it.

### `get_board`

Fetch board metadata, scene data, and hosted viewer URL.

### `share_board`

Switch a board into shared mode and return the tokenized viewer URL.

### `set_board_visibility`

Change a board to `private`, `shared`, or `public`.

### `update_board`

Refine an existing board without creating a new board id.

Input shape:

```json
{
  "board_id": "cmndns0hn0001o401md5okzju",
  "board_type": "flowchart",
  "source_text": "User submits request. Validate request. If valid, create the board. If invalid, ask for correction.",
  "note": "Tighten the wording and preserve yes/no branching."
}
```

### `export_board_png`

Return a PNG export URL when the channel needs an image as well as a hosted link.

Output shape:

```json
{
  "ok": true,
  "board_id": "cmndns0hn0001o401md5okzju",
  "viewer_url": "https://boards.pipintama.com/b/cmndns0hn0001o401md5okzju",
  "png_url": "https://api.pipintama.com/mcp-exports/cmndns0hn0001o401md5okzju.png?theme=light",
  "theme": "light"
}
```

### Chart tools

### `list_chart_modes`

Return the supported chart types and when to use each one.

### `create_chart`

Create a chart from text or structured values and return a hosted viewer URL.

Input shape:

```json
{
  "title": "Weekly Active Agents",
  "chart_type": "line",
  "source_text": "Mon: 12\nTue: 18\nWed: 15\nThu: 22\nFri: 28",
  "visibility": "shared"
}
```

### `get_chart`

Fetch chart metadata, configuration, and hosted viewer URL.

### `share_chart`

Switch a chart into shared mode and return the tokenized viewer URL.

### `set_chart_visibility`

Change a chart to `private`, `shared`, or `public`.

### `update_chart`

Refine an existing chart without creating a new chart id.

### `export_chart_png`

Return a PNG export URL when the channel needs an image as well as a hosted link.

Output shape:

```json
{
  "ok": true,
  "chart_id": "cmnkxiet60013nu016w086rx2",
  "viewer_url": "https://pipintama.com/charts/cmnkxiet60013nu016w086rx2",
  "png_url": "https://api.pipintama.com/mcp-chart-exports/cmnkxiet60013nu016w086rx2.png?theme=light",
  "theme": "light"
}
```

### Map tools

### `list_map_modes`

Return the supported map types and when to use each one.

### `create_map`

Create a map from structured geography inputs and return a hosted viewer URL.

Input shape:

```json
{
  "title": "Colombia Main Cities",
  "map_type": "city_markers",
  "country_name": "Colombia",
  "city_names": ["Bogotá", "Medellín", "Cali", "Barranquilla", "Cartagena"],
  "visibility": "shared"
}
```

### `get_map`

Fetch map metadata, geometry references, and hosted viewer URL.

### `share_map`

Switch a map into shared mode and return the tokenized viewer URL.

### `set_map_visibility`

Change a map to `private`, `shared`, or `public`.

### `update_map`

Refine an existing map without creating a new map id.

### `export_map_png`

Return a PNG export URL when the channel needs an image as well as a hosted link.

Output shape:

```json
{
  "ok": true,
  "map_id": "cmnmj209w0005nu01qnvzz2cm",
  "viewer_url": "https://pipintama.com/maps/cmnmj209w0005nu01qnvzz2cm?t=<share-token>",
  "png_url": "https://api.pipintama.com/mcp-map-exports/cmnmj209w0005nu01qnvzz2cm.png?theme=light&token=<share-token>",
  "theme": "light"
}
```

### Form tools

### `list_form_modes`

Return the supported form types and when to use each one.

### `create_form`

Create a hosted form, poll, or survey and return a hosted form URL.

Input shape:

```json
{
  "title": "Next Feature Vote",
  "form_type": "poll",
  "source_text": "Question: What should we build next? Options: Forms results dashboard, Docs / invoices, Analysis, Tables.",
  "visibility": "shared",
  "collect_name": true,
  "collect_email": true,
  "collect_comment": true
}
```

### `get_form`

Fetch form metadata, schema, and hosted viewer URL.

### `share_form`

Switch a form into shared mode and return the tokenized viewer URL.

### `set_form_visibility`

Change a form to `private`, `shared`, or `public`.

### `update_form`

Refine an existing form without creating a new form id.

### `list_form_responses`

Fetch responses for an existing form so the agent can summarize votes, comments, or structured answers.

## Board modes

- `mindmap`: concepts, brainstorming, topic exploration
- `flowchart`: processes, approvals, branching logic
- `kanban`: tasks grouped by stage or status
- `architecture`: systems, services, integrations, dependencies

## Chart modes

- `line`: trends over time
- `bar`: category comparison
- `pie`: part-to-whole distribution
- `radar`: multidimensional profile comparison

## Map modes

- `country_highlight`: countries, language groups, highlighted country sets
- `city_markers`: cities, offices, stores, branches, and precise locations
- `region_highlight`: departments, states, and provinces inside a country

## Form modes

- `form`: intake, onboarding, lead capture, and request collection
- `poll`: one-question voting with optional name, email, and comment
- `survey`: multi-question feedback with ratings and text answers

## Visibility guidance

- default to `shared`
- use `public` only when the user explicitly wants an open link
- use `private` only when the workflow requires restricted access

## Output guidance

Prefer returning:

1. the hosted viewer link
2. the PNG export URL when the channel benefits from an image
3. one short sentence explaining what the output contains

Avoid returning raw JSON unless the user asks for it explicitly.

## Safety metadata

The hosted MCP publishes tool annotations so clients can reason about safer defaults:

- `readOnlyHint`
- `destructiveHint`
- `idempotentHint`
- `openWorldHint`
