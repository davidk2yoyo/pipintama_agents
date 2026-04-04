# Pipintama Charts Overview

Pipintama Charts is the next planned hosted tool after Boards.

## Why it exists

Boards is for structure:

- mindmaps
- flowcharts
- kanban boards
- architecture maps

Charts is for quantitative views:

- comparisons
- trends
- percentages
- multidimensional profiles

## Proposed MVP

Renderer:

- `Chart.js`

Chart types:

- `line`
- `bar`
- `pie`
- `radar`

## Expected MCP Surface

- `list_chart_modes`
- `create_chart`
- `get_chart`
- `update_chart`
- `share_chart`
- `set_chart_visibility`
- `export_chart_png`

## Shared platform rules

Charts should reuse the same Pipintama platform layer as Boards:

- workspaces
- API keys
- usage attribution
- MCP access
- PNG exports
- future OAuth

## Output expectation

Agents should prefer returning:

1. `viewer_url`
2. `png_url` when the channel benefits from images
3. one short sentence explaining the chart

## Public reference

- `https://pipintama.com/docs/pipintama-charts-spec.md`
