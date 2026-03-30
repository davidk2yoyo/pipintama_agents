# Pipintama Boards MCP

## Purpose

Pipintama Boards exposes a hosted MCP server so agents can create and retrieve visual boards without needing access to the product codebase or the private VPS internals.

Live endpoint:

- `https://api.pipintama.com/mcp`

Health check:

- `https://api.pipintama.com/mcp-health`

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
2. one short sentence explaining what the board contains

Avoid returning raw JSON unless the user asks for it explicitly.
