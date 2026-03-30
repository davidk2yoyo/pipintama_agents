---
name: pipintama-boards
description: Create, fetch, share, or change visibility for hosted Pipintama Boards through the MCP server. Use when a user needs a mindmap, flowchart, kanban board, or architecture map, and the right output is a hosted visual board link instead of only prose.
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

## When to use this skill

Use Boards when the user asks for:

- a mind map
- a flowchart
- a task board or kanban
- an architecture map
- a hosted diagram they can open or share
- a structured breakdown for planning, brainstorming, process design, or system design

Do not use Boards when:

- the user only wants prose
- the answer is a short factual reply
- the visual structure would not add value

## Core workflow

1. Understand the user request and decide whether a hosted board is useful.
2. Choose the simplest correct board mode.
3. Build a concise board title.
4. Preserve the user intent in `source_text` instead of rewriting the task into something unrelated.
5. Default visibility to `shared` unless the user explicitly wants `public` or `private`.
6. Call the MCP tool that matches the job.
7. Return the hosted viewer URL first.
8. Add one short sentence explaining what the board contains.

## Mode selection

- `mindmap`: concept exploration, brainstorming, clustering ideas
- `flowchart`: processes, approvals, decisions, yes/no branching
- `kanban`: tasks grouped by stage, backlog/doing/review/done planning
- `architecture`: services, databases, integrations, gateways, system maps

Prefer the simplest correct mode. Do not use `architecture` for a human workflow. Do not use `kanban` for a concept breakdown.

## Mode-specific rules

### `mindmap`

Use when:

- the user is exploring ideas
- the problem needs breakdown into branches
- a concept hierarchy is more useful than a process diagram

Rules:

- keep one clear root concept
- keep node labels short
- avoid long paragraphs inside nodes
- do not flatten everything into a list

### `flowchart`

Use when:

- the user describes a process
- there are step-by-step actions
- there are decisions, approvals, or branches

Rules:

- prefer start, process, decision, and end semantics
- use branching only when a real condition exists
- phrase nodes as actions or events
- avoid turning a concept map into a fake flowchart

### `kanban`

Use when:

- the user has tasks or deliverables
- the work should be organized by stage
- execution and coordination matter more than system structure

Rules:

- lanes should represent workflow stage or status
- cards should be concrete tasks, not vague themes
- avoid using kanban for conceptual exploration

### `architecture`

Use when:

- the user is describing systems
- the task involves services, stores, gateways, or integrations
- component relationships matter more than human workflow

Rules:

- keep component names short
- emphasize dependencies and boundaries
- do not use architecture mode for an approval flow or task board

## Visibility rules

- default to `shared`
- use `public` only when the user explicitly wants an open link
- use `private` only when the user explicitly asks for restricted access

If a board needs to be shareable and is not already shared, call `share_board`.

## Tool usage

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

## Output format

Default output:

1. hosted viewer URL
2. one short explanation sentence

Optional raw output only when explicitly requested:

- board metadata
- `sceneJson`
- visibility or share token details

Good response pattern:

```text
I created a flowchart for the approval process:
https://boards.pipintama.com/b/<board-id>?t=<share-token>

It includes the intake step, validation step, and yes/no branching for success vs correction.
```

## Guardrails

- avoid flat list thinking when the task needs hierarchy
- avoid choosing a board type just because the user used the word “diagram”
- avoid public boards unless the user explicitly asks for an open link
- avoid returning raw JSON first when a hosted viewer URL is more useful
- prioritize clarity over completeness inside node text
- keep titles concise and useful
- do not invent capabilities that do not exist yet

## Current limits

- exports are not implemented yet
- editing existing boards is not implemented yet
- auth is still basic, so shared links are preferred
- generation is structured but still improving by mode
