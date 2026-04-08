# LobeHub Integration Notes

## Status

Validated.

The successful path in LobeHub was:

1. go to Settings
2. add a custom MCP skill
3. use the hosted Pipintama MCP endpoint
4. authenticate with a Pipintama API key
5. enable the MCP skill inside the chat
6. run the request

## Before LobeHub setup

1. Create a Pipintama account
2. Generate a Pipintama API key
3. Use that key as Bearer auth in the custom MCP skill

## MCP configuration

- MCP type: `Streamable HTTP`
- MCP name: `pipintama`
- Endpoint: `https://api.pipintama.com/mcp`
- Header: `Authorization`
- Value: `Bearer <PIPINTAMA_API_KEY>`

## What worked

- Charts through MCP
- Boards through MCP
- Forms use the same MCP path and return hosted form links
- Maps use the same MCP path and return hosted map and PNG links
- Hosted viewer URLs returned in chat
- PNG URLs returned in chat

## Important behavior

In LobeHub, adding the custom MCP skill is not enough by itself.

The validated path required:

- install the custom MCP skill
- enable that MCP skill in the target chat
- then run the request

## Recommended prompts

Charts:

```text
Create a bar chart from this data:
January: 12
February: 18
March: 15

Return the hosted chart link and PNG URL.
```

Boards:

```text
Create a flowchart for this process:
User submits a request. Team validates the request. If approved, create the board and notify the user. If rejected, ask for corrections.

Return the hosted board link and PNG URL.
```

Forms:

```text
Create a poll called "Next feature vote".

Question:
What should we build next?

Options:
Forms results dashboard
Docs / invoices
Analysis
Tables

Collect optional name, email, and comment.

Return the hosted form link.
```

Maps:

```text
Show the main cities of Colombia on a map: Bogotá, Medellín, Cali, Barranquilla, Cartagena.

Return the hosted map link and PNG URL.
```

## Expected outputs

LobeHub should return:

1. hosted viewer URL
2. PNG URL
3. one short explanation

For Forms, LobeHub should return:

1. hosted form URL
2. one short explanation

For Maps, LobeHub should return:

1. hosted map URL
2. PNG URL
3. one short explanation
