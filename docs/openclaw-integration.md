# OpenClaw Integration Notes

## Goal

OpenClaw should use Pipintama Boards through the hosted MCP endpoint, not through hardcoded Telegram-only logic.

## Recommended setup

Give OpenClaw:

1. MCP access to `https://api.pipintama.com/mcp`
2. the Pipintama Boards skill from `skills/pipintama-boards/SKILL.md`

The public docs can be used as reference, but the skill should drive behavior.

## Expected behavior

When a user asks for a visual structure, OpenClaw should:

1. decide whether a board is useful
2. choose the correct mode
3. call `create_board`
4. return the hosted viewer URL
5. add one short explanation

## Recommended defaults

- default visibility: `shared`
- default workspace: `cmndiuyll0002s601xdikq182`
- prefer concise titles
- preserve the user's language in `source_text`

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

## What not to do

- do not ask the user to browse the repo
- do not depend on private VPS details
- do not return raw board JSON first when a hosted link is more useful
- do not make boards public unless the user explicitly asks for that
