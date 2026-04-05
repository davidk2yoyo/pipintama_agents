# Pipintama Boards Overview

Pipintama Boards lets agents turn plain text into hosted visual structures.

## What it does

Boards supports:

- `mindmap` for ideas and hierarchy
- `flowchart` for processes and decisions
- `kanban` for stages and task boards
- `architecture` for systems and services

## When to use Boards

Use Boards when the user asks for:

- a diagram
- a flowchart
- a mindmap
- a kanban board
- an architecture map
- a hosted visual board link

Do not use Boards when the request is mainly quantitative and better represented as a chart.

## Shared platform rules

Boards uses the same Pipintama platform layer as Charts:

- workspaces
- API keys
- usage attribution
- hosted MCP access
- OpenAPI adapter access
- PNG exports

## Live MCP tools

- `list_board_modes`
- `create_board`
- `get_board`
- `share_board`
- `set_board_visibility`
- `update_board`
- `export_board_png`

## Output expectation

Agents should prefer returning:

1. `viewer_url`
2. `png_url` when the channel benefits from images
3. one short sentence explaining the board

## Viewer patterns

- `https://boards.pipintama.com/b/<board-id>`
- `https://boards.pipintama.com/b/<board-id>?t=<share-token>`

PNG export pattern:

- `https://api.pipintama.com/mcp-exports/<board-id>.png?theme=light`

## Public reference

- `https://pipintama.com/docs/tools/boards/`
