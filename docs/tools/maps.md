# Pipintama Maps Overview

Pipintama Maps is live on the same hosted platform as Boards and Charts.

## What it does

Maps lets an agent turn text or structured geographic fields into visual outputs such as:

- `country_highlight` for countries and regional groupings
- `city_markers` for cities, branches, stores, offices, and locations
- `region_highlight` for departments, states, and provinces

## When to use Maps

Use Maps when the user asks for:

- a geographic map
- highlighted countries
- marked cities
- departments, states, or provinces
- geographic coverage
- language-region maps such as Spanish-speaking countries

Do not use Maps when the user really needs:

- a process diagram
- a mindmap
- a kanban board
- a quantitative chart

Those belong in `Boards` or `Charts`.

## Shared platform rules

Maps reuses the same Pipintama platform layer:

- workspaces
- API keys
- usage attribution
- hosted MCP access
- PNG exports

## Live MCP tools

- `list_map_modes`
- `create_map`
- `get_map`
- `share_map`
- `set_map_visibility`
- `update_map`
- `export_map_png`

## Output expectation

Agents should prefer returning:

1. `viewer_url`
2. `png_url` when the channel benefits from images
3. one short sentence explaining the map

## Viewer patterns

- `https://pipintama.com/maps/<map-id>?t=<share-token>`

PNG export pattern:

- `https://api.pipintama.com/mcp-map-exports/<map-id>.png?theme=light&token=<share-token>`

## Notes for OpenWebUI

Maps works in OpenWebUI, but city and region requests are more reliable when the model converts them into structured fields such as:

- `type=city_markers`
- `countryName`
- `cityNames`
