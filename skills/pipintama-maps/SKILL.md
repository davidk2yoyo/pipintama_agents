---
name: pipintama-maps
description: Create, fetch, share, or update hosted Pipintama Maps through the MCP server. Use when a user needs a geographic map with countries, city markers, departments, states, or provinces, and the right output is a hosted map link or PNG instead of only prose.
---

# Pipintama Maps

Use this skill when the user would benefit from a hosted geographic map instead of only plain text.

Primary MCP endpoint:

- `https://api.pipintama.com/mcp`

Access model:

- this hosted MCP requires a valid Pipintama API key
- clients should provide it through `Authorization: Bearer <key>` or `x-api-key`
- usage is attributed to the authenticated client and workspace

Health check:

- `https://api.pipintama.com/mcp-health`

Primary tools:

- `list_map_modes`
- `create_map`
- `get_map`
- `share_map`
- `set_map_visibility`
- `update_map`
- `export_map_png`

## When to use this skill

Use Maps when the user asks for:

- a country map
- highlighted countries
- a map of cities
- city markers
- departments, states, or provinces
- highlighted regions
- geographic coverage
- language-region maps such as Spanish-speaking countries
- branch, office, or market locations on a map

Do not use Maps when:

- the user needs a chart, board, or form instead of geography
- the answer is only prose and a map adds no value
- the user is asking for a process diagram rather than geographic regions

## Core workflow

1. Understand whether a geographic map is useful.
2. Choose the correct mode: `country_highlight`, `city_markers`, or `region_highlight`.
3. Build a concise map title.
4. Preserve the user intent in structured fields instead of rewriting the task into something unrelated.
5. Default visibility to `shared` unless the user explicitly wants `public` or `private`.
6. Do not pass `workspace_id` unless the user explicitly provides one. Let the authenticated API key determine the workspace.
7. Prefer explicit structured fields when possible, especially for cities and regions.
8. Return the hosted map URL first.
9. Add one short sentence describing what the map shows.

## Mode selection

- `country_highlight`: countries, language groups, highlighted country sets
- `city_markers`: cities, branches, offices, stores, and locations
- `region_highlight`: departments, states, and provinces inside a country

Prefer the simplest correct mode. Do not use `country_highlight` when the real need is to place city markers. Do not use `city_markers` when the user wants administrative regions colored by area.

## Mode-specific rules

### `country_highlight`

Use when:

- the user asks for countries
- the user wants a regional language group
- the user wants to highlight a market footprint at country level

Rules:

- prefer explicit country names or country codes
- keep the title short and region-focused
- use for sets like "Spanish-speaking countries" only when the country list is clear

### `city_markers`

Use when:

- the user asks for cities
- the user wants branches, stores, or office locations
- the output should show precise places instead of shaded regions

Rules:

- if all cities are in one country, send that country explicitly
- send city names as a clear array when possible
- prefer the user’s exact requested city names as labels

### `region_highlight`

Use when:

- the user asks for departments, states, or provinces
- the map should show administrative areas inside one country

Rules:

- send the country explicitly
- send region names when the user names specific regions
- use for cases like "all departments of Colombia" or "highlight Antioquia and Cundinamarca"

## Visibility rules

- default to `shared`
- use `public` only when the user explicitly wants an open link
- use `private` only when the user explicitly asks for restricted access

## Tool usage

### `create_map`

Use this for the first map creation.

Expected inputs:

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

Use this when the user asks to inspect or retrieve an existing map.

### `share_map`

Use this when a map should be opened through a tokenized share link.

### `set_map_visibility`

Use this when the user explicitly asks to make a map private, shared, or public.

### `update_map`

Use this when the user wants to refine an existing map instead of creating a new one.

Typical cases:

- add or remove countries
- add or remove cities
- switch from city markers to region highlights
- refine labels or title
- change visibility

### `export_map_png`

Use this when the user needs an actual image file instead of only a hosted link.

Typical cases:

- Telegram
- WhatsApp
- quick previews in chat
- channels where an image is more useful than a URL alone

## Output format

Default output:

1. hosted map URL
2. one short explanation sentence

If the channel supports images and visual attachments are useful:

1. hosted map URL
2. PNG export URL
3. one short explanation sentence

Good response pattern:

```text
I created the map:
https://pipintama.com/maps/<map-id>?t=<share-token>

It shows the main cities of Colombia as labeled markers.
```

Image-friendly pattern:

```text
I created the map and exported a PNG for easy sharing:
Viewer: https://pipintama.com/maps/<map-id>?t=<share-token>
PNG: https://api.pipintama.com/mcp-map-exports/<map-id>.png?theme=light&token=<share-token>
```

Only use live Pipintama URL patterns.

Valid:

- `https://pipintama.com/maps/<map-id>?t=<share-token>`
- `https://api.pipintama.com/mcp-map-exports/<map-id>.png?theme=light&token=<share-token>`

Invalid:

- `https://pipintama.com/map/<map-id>`
- `https://api.pipintama.com/maps/<map-id>.png`
