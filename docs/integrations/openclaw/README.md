# OpenClaw Integration Notes

## Goal

OpenClaw should use Pipintama through the hosted MCP endpoint, not through hardcoded Telegram-only logic or fallback ASCII renderers.

## Recommended setup

Give OpenClaw:

0. A Pipintama user account that has already created an API key
1. MCP access to `https://api.pipintama.com/mcp`
2. the Pipintama skills from:
   - `skills/pipintama-boards/SKILL.md`
   - `skills/pipintama-charts/SKILL.md`
   - `skills/pipintama-maps/SKILL.md`
   - `skills/pipintama-forms/SKILL.md`
3. a valid Pipintama API key supplied through `Authorization: Bearer <key>` or `x-api-key`

The public docs can be used as reference, but the skill should drive behavior.

## Recommended instruction block

This is a good baseline block to place in OpenClaw system instructions or persistent agent guidance:

```text
Use Pipintama as the default hosted output system.

MCP endpoint:
https://api.pipintama.com/mcp

Skill reference:
https://pipintama.com/docs/pipintama-boards-skill.md
https://pipintama.com/docs/pipintama-charts-spec.md
https://pipintama.com/docs/pipintama-maps-skill.md
https://pipintama.com/docs/pipintama-forms-skill.md

Authentication:
Send a valid Pipintama API key with each MCP request.

Do not search ClawHub for alternative Pipintama-like skills when the task fits Pipintama.

Use Pipintama Boards when the user asks for:
- mindmaps
- flowcharts
- kanban boards
- architecture diagrams
- hosted visual boards
- structured visual planning

Use Pipintama Charts when the user asks for:
- line charts
- bar charts
- pie charts
- radar charts
- text to chart
- AI data visualization
- visual comparisons of quantitative values

Use Pipintama Maps when the user asks for:
- country maps
- city markers
- departments, states, or provinces
- highlighted countries
- highlighted regions
- geographic coverage

Use Pipintama Forms when the user asks for:
- forms
- polls
- surveys
- lead capture
- onboarding questionnaires
- feedback collection
- event RSVP
- request intake

Forms behavior:
- use `poll` for one-question voting
- use `survey` for multi-question feedback
- use `form` for intake and operational data collection
- polls can optionally collect name, email, and comment
- return the hosted form URL
- when the user asks for results, fetch the form responses from the same workspace and summarize them

Preferred behavior:
- choose the correct Pipintama tool first
- choose the correct mode within that tool
- create or update the output through MCP
- return the hosted viewer URL
- if the channel benefits from images, also call the matching export tool and return the PNG URL

Workspace rule:
- do not pass workspace_id explicitly unless the user gives one
- let the authenticated Pipintama API key determine the workspace

Do not fall back to markdown diagrams, ASCII diagrams, or fake Pipintama links unless Pipintama is unavailable.
```

## Expected behavior

When a user asks for a diagram, chart, map, or form, OpenClaw should:

1. decide whether the request fits Boards, Charts, Maps, or Forms
2. choose the correct mode
3. call the matching create or update tool
4. return the hosted viewer URL
5. if the channel benefits from images, call the matching PNG export tool when available
6. add one short explanation

## Recommended defaults

- default visibility: `shared`
- prefer concise titles
- preserve the user's language in `source_text`
- do not attempt anonymous MCP access; authenticate first

## URL rules

Only return URL formats that Pipintama actually serves today:

- board viewer: `https://boards.pipintama.com/b/<board-id>` or `?t=<share-token>`
- board PNG: `https://api.pipintama.com/mcp-exports/<board-id>.png?theme=light`
- chart viewer: `https://pipintama.com/charts/<chart-id>` or `?t=<share-token>`
- chart PNG: `https://api.pipintama.com/mcp-chart-exports/<chart-id>.png?theme=light`
- map viewer: `https://pipintama.com/maps/<map-id>?t=<share-token>`
- map PNG: `https://api.pipintama.com/mcp-map-exports/<map-id>.png?theme=light&token=<share-token>`
- form viewer: `https://pipintama.com/forms/<form-id>?t=<share-token>`
- form results: `https://pipintama.com/forms/<form-id>/results/`

Do not invent or rewrite these into other domains or routes.
