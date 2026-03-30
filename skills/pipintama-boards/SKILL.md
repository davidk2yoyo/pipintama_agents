---
name: pipintama-boards
description: Use when an agent should create, fetch, share, or change visibility for Pipintama Boards through the hosted MCP server. Covers board-mode selection, visibility defaults, and the expected response style when returning hosted board links to users.
---

# Pipintama Boards

Use this skill when the user would benefit from a hosted visual board instead of only plain text.

Primary MCP endpoint:

- `https://api.pipintama.com/mcp`

Health check:

- `https://api.pipintama.com/mcp-health`

Primary tools:

- `list_board_modes`
- `create_board`
- `get_board`
- `share_board`
- `set_board_visibility`

Default workspace for demos:

- `cmndiuyll0002s601xdikq182`

## When To Use Boards

Use Boards when the user asks for:

- a mind map
- a flowchart
- a task board or kanban
- an architecture map
- a hosted diagram they can open or share

Do not use Boards when:

- the user only wants prose
- the answer is a short factual reply
- the visual structure would not add value

## Mode Selection

- `mindmap`: concept exploration, brainstorming, clustering ideas
- `flowchart`: processes, approvals, decisions, yes/no branching
- `kanban`: tasks grouped by stage, backlog/doing/review/done planning
- `architecture`: services, databases, integrations, gateways, system maps

Prefer the simplest correct mode. Do not use `architecture` for a human workflow. Do not use `kanban` for a concept breakdown.

## Visibility Rules

- default to `shared`
- use `public` only when the user explicitly wants an open link
- use `private` only when the user explicitly asks for restricted access

If a board needs to be shareable and is not already shared, call `share_board`.

## Tool Usage

### `create_board`

Use this for the first board creation.

Expected inputs:

```json
{
  "workspace_id": "cmndiuyll0002s601xdikq182",
  "title": "Approval Flow",
  "board_type": "flowchart",
  "source_text": "User submits a request. System validates the payload. If the request is valid, create the board and notify the user. If the request is invalid, return an error and ask for correction.",
  "visibility": "shared"
}
```

### `get_board`

Use this when the user asks to inspect, retrieve, or reason about an existing board.

### `share_board`

Use this when a board should be opened through a tokenized share link.

### `set_board_visibility`

Use this when the user explicitly asks to make a board private, shared, or public.

## Response Pattern

Return the hosted board link first, then one short sentence about what the board contains.

Good pattern:

```text
I created a flowchart for the approval process:
https://boards.pipintama.com/b/<board-id>?t=<share-token>

It includes the intake step, validation step, and yes/no branching for success vs correction.
```

Avoid dumping raw `sceneJson` unless the user explicitly asks for raw data.

## Current Limits

- exports are not implemented yet
- editing existing boards is not implemented yet
- auth is still basic, so shared links are preferred
- generation is structured but still improving by mode
