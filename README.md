# Pipintama Agents

Public documentation for humans and agents that want to use Pipintama as a hosted tools platform.

Pipintama lets an AI agent turn plain text into useful outputs by calling the right hosted tool:

- `Boards` for diagrams, mindmaps, kanban, and flow structures
- `Charts` for line, bar, pie, and radar visualizations
- future tools for analysis, tables, documents, and structured work

## Live endpoints

- MCP: `https://api.pipintama.com/mcp`
- MCP health: `https://api.pipintama.com/mcp-health`
- Boards viewer: `https://boards.pipintama.com`
- Charts viewer pattern: `https://pipintama.com/charts/<chart-id>`
- Public docs: `https://pipintama.com/docs/`

## Repo structure

- `docs/mcp-overview.md`: shared MCP access and tool surface
- `docs/openclaw-integration.md`: ready-to-paste instructions for OpenClaw-like agents
- `docs/charts-overview.md`: how Charts works and when to use it
- `skills/pipintama-boards/SKILL.md`: agent skill for hosted boards
- `skills/pipintama-charts/SKILL.md`: agent skill for hosted charts

## Tool selection

Use `Boards` when the agent needs:

- a diagram
- a mindmap
- a flowchart
- a kanban board
- an architecture map
- a hosted visual board link

Use `Charts` when the agent needs:

- a line chart
- a bar chart
- a pie chart
- a radar chart
- a visual comparison of quantitative values
- a PNG chart for chat channels

## Authentication

The hosted MCP is not anonymous.

- clients authenticate with a Pipintama API key
- use `Authorization: Bearer <key>` or `x-api-key`
- usage is attributed to the authenticated client and workspace

## Output rules

Agents should prefer returning:

1. a hosted viewer URL
2. a PNG URL when the channel benefits from images
3. one short sentence about what was created

Do not invent unsupported Pipintama URL formats.

## Start here

If you are wiring an agent such as OpenClaw, start with:

- `docs/openclaw-integration.md`

Then load the matching skill:

- `skills/pipintama-boards/SKILL.md`
- `skills/pipintama-charts/SKILL.md`
