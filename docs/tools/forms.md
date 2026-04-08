# Pipintama Forms

Pipintama Forms turns text into hosted forms, polls, and surveys.

It is the right tool when an agent needs to:

- collect responses from people
- share a hosted form link
- run a quick poll
- gather onboarding or intake information
- read results later and summarize them

## Modes

- `form`: intake forms, lead capture, onboarding, operational requests
- `poll`: one-question voting, option selection, optional name/email/comment capture
- `survey`: multi-question feedback, ratings, and written opinions

## URLs

- Form URL: `https://pipintama.com/forms/<form-id>?t=<share-token>`
- Results URL: `https://pipintama.com/forms/<form-id>/results/`

## Notes

- polls can collect optional `name`, `email`, and `comment`
- results are owner-only in the web UI
- agents can fetch responses through MCP or OpenAPI with the correct workspace-scoped API key
