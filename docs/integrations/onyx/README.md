# Onyx Integration Notes

## Status

Validated.

The reliable path in Onyx was:

1. create a focused OpenAPI action for Pipintama Charts or Pipintama Boards
2. authenticate it with a real Pipintama API key
3. create an Onyx agent
4. enable the Pipintama action for that agent
5. chat with that agent

## Before Onyx setup

1. Create a Pipintama account
2. Generate a Pipintama API key
3. Use that key in the Onyx action auth step

## What worked

- Charts through Onyx OpenAPI action
- Boards through Onyx OpenAPI action
- Hosted viewer URLs returned in chat
- PNG URLs returned in chat

## Forms and Maps note

Forms and Maps should follow the same focused OpenAPI-action pattern in Onyx:

- create a focused OpenAPI action for that one tool family
- authenticate it with a real Pipintama API key
- enable it on the target agent

Use that path instead of assuming one giant mixed action will route well.

## Important behavior

Connecting the Pipintama MCP server in Onyx can expose tools and action discovery, but that alone did not guarantee successful chat execution.

The validated path was agent-level OpenAPI actions.

## Recommended setup

For each tool family:

- create a focused OpenAPI action
- avoid one giant mixed spec if you can keep it narrower
- authenticate with:
  - `Authorization: Bearer <PIPINTAMA_API_KEY>`
- create an Onyx agent
- enable the Pipintama action for that agent

## OpenAPI schema definitions

Use separate schema definitions for each tool family.

- Charts schema:
  - `docs/integrations/onyx/onyx-charts-openapi.json`
  - `https://pipintama.com/docs/pipintama-onyx-charts-openapi.json`
- Boards schema:
  - `docs/integrations/onyx/onyx-boards-openapi.json`
  - `https://pipintama.com/docs/pipintama-onyx-boards-openapi.json`

## Recommended scope

Use separate actions or at least clearly separated tool families:

- `Pipintama Charts`
- `Pipintama Boards`

That keeps the action surface easier for the agent to use correctly.

For Forms, the same principle applies:

- use a focused Forms action if you want polls, surveys, intake forms, and response reading
- keep response collection and response reading in the same workspace

## Workspace rule

Do not force old demo workspace IDs.

Let the authenticated Pipintama API key determine the workspace automatically.

## Live endpoints used

- OpenAPI spec: `https://api.pipintama.com/openapi.json`
- Boards viewer: `https://boards.pipintama.com`
- Charts viewer pattern: `https://pipintama.com/charts/<chart-id>`

## Expected outputs

Onyx should return:

1. hosted viewer URL
2. PNG URL when useful
3. one short explanation

## Example result

For charts:

- viewer: `https://pipintama.com/charts/<chart-id>?t=<share-token>`
- png: `https://api.pipintama.com/mcp-chart-exports/<chart-id>.png?theme=light&token=<share-token>`

For boards:

- viewer: `https://boards.pipintama.com/b/<board-id>?t=<share-token>`
- png: `https://api.pipintama.com/mcp-exports/<board-id>.png?theme=light&token=<share-token>`
