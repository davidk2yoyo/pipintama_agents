# Pipintama Charts Overview

Pipintama Charts is live on the same hosted MCP stack as Boards.

## What it does

Charts lets an agent turn plain text or structured values into visual outputs such as:

- `line` charts for trends
- `bar` charts for comparisons
- `pie` charts for distribution
- `radar` charts for profile comparison

## When to use Charts

Use Charts when the user asks for:

- a chart from text
- an AI chart generator
- a visual comparison of categories
- trend lines from time or sequence data
- shareable chart images for Telegram, WhatsApp, or similar channels

Do not use Charts when the user really needs:

- a process diagram
- a mindmap
- a kanban board
- a system map

Those belong in `Boards`.

## Shared platform rules

Charts reuses the same Pipintama platform layer as Boards:

- workspaces
- API keys
- usage attribution
- hosted MCP access
- PNG exports
- future OAuth

## Live MCP tools

- `list_chart_modes`
- `create_chart`
- `get_chart`
- `share_chart`
- `set_chart_visibility`
- `update_chart`
- `export_chart_png`

## Output expectation

Agents should prefer returning:

1. `viewer_url`
2. `png_url` when the channel benefits from images
3. one short sentence explaining the chart

## Viewer patterns

- `https://pipintama.com/charts/<chart-id>`
- `https://pipintama.com/charts/<chart-id>?t=<share-token>`

PNG export pattern:

- `https://api.pipintama.com/mcp-chart-exports/<chart-id>.png?theme=light`

## Public reference

- `https://pipintama.com/docs/pipintama-charts-spec.md`
