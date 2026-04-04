# Pipintama Agents

Documentation for humans and agents that want to use Pipintama Boards through the hosted MCP.

Here you can read:

- what the MCP endpoint is
- how authentication works
- how the Pipintama Boards skill works
- how an agent such as OpenClaw should use the tools
- which board modes are supported and when to choose them

## Live endpoints

- MCP: `https://api.pipintama.com/mcp`
- MCP health: `https://api.pipintama.com/mcp-health`
- Viewer: `https://boards.pipintama.com`
- Public docs: `https://pipintama.com/docs/`
- Public skill reference: `https://pipintama.com/docs/pipintama-boards-skill.md`

## Repo structure

- `skills/pipintama-boards/SKILL.md`: reusable skill for agents
- `docs/mcp-overview.md`: MCP tools and behavior contract
- `docs/openclaw-integration.md`: practical integration notes for OpenClaw-like agents

## OpenClaw

If you are wiring OpenClaw, start here:

- `docs/openclaw-integration.md`

That file includes a ready-to-paste instruction block telling OpenClaw to use Pipintama Boards as the default visual-board system instead of searching ClawHub for alternate diagram skills.

## Core idea

Pipintama Boards is meant to be consumed as a hosted capability.

Current access model:

- remote MCP clients authenticate with API keys
- usage is attributed to client id and client name
- tool metadata includes safety annotations
- OAuth is planned for a later user-scoped phase

An agent should:

1. read the skill
2. connect to the hosted MCP endpoint
3. create or fetch boards through MCP tools
4. return hosted viewer links to users

## Support and public docs

- Public docs: `https://pipintama.com/docs/`
- Public skill: `https://pipintama.com/docs/pipintama-boards-skill.md`
- Support entry point: `https://pipintama.com/contact/`
