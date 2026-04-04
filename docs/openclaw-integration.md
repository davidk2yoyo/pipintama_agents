# OpenClaw Integration Notes

## Goal

OpenClaw should use Pipintama Boards through the hosted MCP endpoint, not through hardcoded Telegram-only logic.

## Recommended setup

Give OpenClaw:

1. MCP access to `https://api.pipintama.com/mcp`
2. the Pipintama Boards skill from `skills/pipintama-boards/SKILL.md`
3. a valid Pipintama API key supplied through `Authorization: Bearer <key>` or `x-api-key`

The public docs can be used as reference, but the skill should drive behavior.

## Recommended instruction block

This is a good baseline block to place in OpenClaw system instructions or persistent agent guidance:

```text
Use Pipintama Boards as the default visual-board system.

MCP endpoint:
https://api.pipintama.com/mcp

Skill reference:
https://pipintama.com/docs/pipintama-boards-skill.md

Authentication:
Send a valid Pipintama API key with each MCP request.

Do not search ClawHub for alternative diagram or mindmap skills when the task fits Pipintama Boards.

Use Pipintama Boards when the user asks for:
- mindmaps
- flowcharts
- kanban boards
- architecture diagrams
- hosted visual boards
- structured visual planning

Preferred behavior:
- choose the correct board mode
- create or update the board through MCP
- return the hosted viewer URL
- if the channel benefits from images, also call export_board_png and return the PNG URL

Workspace rule:
- do not pass workspace_id explicitly unless the user gives one
- let the authenticated Pipintama API key determine the workspace

Do not fall back to markdown diagrams or ASCII diagrams unless Pipintama Boards is unavailable.
```

## Expected behavior

When a user asks for a visual structure, OpenClaw should:

1. decide whether a board is useful
2. choose the correct mode
3. call `create_board` or `update_board`
4. return the hosted viewer URL
5. if the channel benefits from images, call `export_board_png`
6. add one short explanation

## Recommended defaults

- default visibility: `shared`
- prefer concise titles
- preserve the user's language in `source_text`
- do not attempt anonymous MCP access; authenticate first

## Example behavior

User:

```text
Make me a flowchart for our approval process.
```

OpenClaw should choose `flowchart`, call `create_board`, and respond with something like:

```text
I created a flowchart for the approval process:
https://boards.pipintama.com/b/<board-id>?t=<share-token>

It includes intake, validation, and branching for approval vs correction.
```

If the channel benefits from images, OpenClaw should call `export_board_png` and respond with something like:

```text
I created the flowchart and exported a PNG for easy sharing:
Viewer: https://boards.pipintama.com/b/<board-id>?t=<share-token>
PNG: https://api.pipintama.com/mcp-exports/<board-id>.png?theme=light
```

## URL rules

Only return URL formats that Pipintama actually serves today:

- viewer: `https://boards.pipintama.com/b/<board-id>` or `?t=<share-token>`
- PNG: `https://api.pipintama.com/mcp-exports/<board-id>.png?theme=light`

Do not invent or rewrite these into other domains or routes.

Wrong examples:

- `https://pipintama.com/board/<board-id>`
- `https://cdn.pipintama.com/boards/<board-id>/export.png`

## What not to do

- do not ask the user to browse the repo
- do not depend on private VPS details
- do not return raw board JSON first when a hosted link is more useful
- do not make boards public unless the user explicitly asks for that
- do not silently fall back to ASCII or markdown diagrams when Pipintama access is available
- do not fabricate Pipintama URLs that the platform does not serve
