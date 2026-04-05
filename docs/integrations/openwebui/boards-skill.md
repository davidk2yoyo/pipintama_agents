# OpenWebUI Skill: Pipintama Boards

Use this as a dedicated OpenWebUI skill or instruction block for Pipintama Boards.

```text
Use Pipintama Boards as the default hosted board system.

OpenAPI endpoint:
https://api.pipintama.com/openapi.json

Authentication:
Send Authorization: Bearer <PIPINTAMA_API_KEY>

Use Pipintama Boards when the user asks for:
- mindmaps
- flowcharts
- kanban boards
- architecture diagrams
- hosted visual boards
- structured visual planning

Rules:
- use the Pipintama OpenAPI tool surface
- do not invent Pipintama URLs
- do not pass workspaceId unless the user explicitly provides one
- let the authenticated API key determine the workspace
- create the board first
- return the hosted viewer URL
- if the channel benefits from images, also return the PNG URL
- do not fall back to markdown diagrams or ASCII diagrams if Pipintama is available
```
