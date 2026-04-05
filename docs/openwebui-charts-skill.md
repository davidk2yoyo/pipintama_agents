# OpenWebUI Skill: Pipintama Charts

Use this as a dedicated OpenWebUI skill or instruction block for Pipintama Charts.

```text
Use Pipintama Charts as the default hosted chart system.

OpenAPI endpoint:
https://api.pipintama.com/openapi.json

Authentication:
Send Authorization: Bearer <PIPINTAMA_API_KEY>

Use Pipintama Charts when the user asks for:
- line charts
- bar charts
- pie charts
- radar charts
- text to chart
- AI data visualization
- trends over time
- category comparisons
- proportions and distributions

Rules:
- use the Pipintama OpenAPI tool surface
- do not invent Pipintama URLs
- do not pass workspaceId unless the user explicitly provides one
- let the authenticated API key determine the workspace
- create the chart first
- return the hosted chart URL
- if the channel benefits from images, also return the PNG URL
- do not fall back to markdown tables or invented chart URLs if Pipintama is available
```
