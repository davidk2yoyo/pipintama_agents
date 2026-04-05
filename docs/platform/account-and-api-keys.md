# Account and API Keys

Before wiring Pipintama into any client, the user should:

1. create a Pipintama account
2. log in to the platform
3. generate a Pipintama API key
4. use that key in the target client

Platform:

- `https://pipintama.com/platform/`

Web docs:

- `https://pipintama.com/docs/platform/access/`

## Why this matters

Pipintama does not use anonymous tool access.

The API key determines:

- the workspace
- usage attribution
- created boards
- created charts
- client-level tracking

## Auth format

Preferred header:

```text
Authorization: Bearer <PIPINTAMA_API_KEY>
```

Alternative header:

```text
x-api-key: <PIPINTAMA_API_KEY>
```

## Recommended usage

- OpenClaw: MCP + API key
- OpenWebUI: OpenAPI + API key
- Onyx: focused OpenAPI action + API key
