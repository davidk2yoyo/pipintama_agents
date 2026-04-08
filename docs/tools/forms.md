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

## Flow

1. Create the form from MCP or OpenAPI
2. Share the public form URL
3. Collect responses on the hosted form page
4. Review results in the owner-only results page or fetch responses through MCP/OpenAPI

## URLs

- Form URL: `https://pipintama.com/forms/<form-id>?t=<share-token>`
- Results URL: `https://pipintama.com/forms/<form-id>/results/`

## Typical fields

Poll:

- `title`
- `question`
- `options`
- optional `collectName`
- optional `collectEmail`
- optional `collectComment`

Survey:

- `title`
- multiple questions
- ratings
- written feedback

Form:

- `title`
- `name`
- `email`
- `company`
- `project type`
- `budget`
- `timeline`
- `notes`

## Results

- humans can review results in the owner-only results page
- agents can fetch responses through MCP `list_form_responses`
- OpenAPI clients can fetch responses through `GET /openapi/forms/{formId}/responses`

## Notes

- polls can collect optional `name`, `email`, and `comment`
- results are owner-only in the web UI
- agents can fetch responses through MCP or OpenAPI with the correct workspace-scoped API key
