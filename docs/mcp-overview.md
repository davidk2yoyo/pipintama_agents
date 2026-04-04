# Pipintama Boards MCP

## Purpose

Pipintama Boards exposes a hosted MCP server so agents can create and retrieve visual boards without needing access to the product codebase or the private VPS internals.

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

### `list_board_modes`

Return the supported board types and when to use each one.

### `create_board`

Create a board from user text and return a hosted viewer URL.

Input shape:

```json
{
  "workspace_id": "cmndiuyll0002s601xdikq182",
  "title": "Launch Workflow",
  "board_type": "flowchart",
  "source_text": "Capture request. Validate inputs. Generate board. Return hosted URL.",
  "visibility": "shared"
}
```

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

## Board modes

- `mindmap`: concepts, brainstorming, topic exploration
- `flowchart`: processes, approvals, branching logic
- `kanban`: tasks grouped by stage or status
- `architecture`: systems, services, integrations, dependencies

## Visibility guidance

- default to `shared`
- use `public` only when the user explicitly wants an open link
- use `private` only when the workflow requires restricted access

## Output guidance

Prefer returning:

1. the hosted viewer link
2. the PNG export URL when the channel benefits from an image
3. one short sentence explaining what the board contains

Avoid returning raw JSON unless the user asks for it explicitly.

## Safety metadata

The hosted MCP publishes tool annotations so clients can reason about safer defaults:

- `readOnlyHint`
- `destructiveHint`
- `idempotentHint`
- `openWorldHint`
