---
name: pipintama-forms
description: Create, fetch, share, update, and review hosted Pipintama Forms through the MCP server. Use when a user needs a poll, survey, onboarding form, intake form, lead capture flow, or hosted response collection link instead of only prose.
---

# Pipintama Forms

Use this skill when the user would benefit from a hosted form, poll, or survey instead of only plain text.

Primary MCP endpoint:

- `https://api.pipintama.com/mcp`

Access model:

- this hosted MCP requires a valid Pipintama API key
- clients should provide it through `Authorization: Bearer <key>` or `x-api-key`
- usage is attributed to the authenticated client and workspace

Health check:

- `https://api.pipintama.com/mcp-health`

Primary tools:

- `list_form_modes`
- `create_form`
- `get_form`
- `share_form`
- `set_form_visibility`
- `update_form`
- `list_form_responses`

## When to use this skill

Use Forms when the user asks for:

- a poll
- a survey
- a lead capture form
- a client onboarding form
- an event RSVP form
- an intake or request form
- feedback collection
- a hosted link where other people can answer
- results that the agent can later summarize

Do not use Forms when:

- the user only wants a static document with no response collection
- the answer should be a chart, board, or map instead of a submission flow
- a simple prose answer is enough and there is no benefit to collecting external responses

## Core workflow

1. Understand whether the request needs response collection.
2. Choose the correct mode: `poll`, `survey`, or `form`.
3. Build a concise title.
4. Preserve the user intent in the schema and prompt-derived fields instead of rewriting the request into something unrelated.
5. Default visibility to `shared` unless the user explicitly wants `public` or `private`.
6. Do not pass `workspace_id` unless the user explicitly provides one. Let the authenticated API key determine the workspace.
7. Create the form and return the hosted form URL first.
8. If the user asks for results later, fetch responses from the same workspace with `list_form_responses`.
9. Summarize the results without inventing IDs, URLs, or response counts.

## Mode selection

- `poll`: one-question voting with options
- `survey`: multi-question feedback with ratings, selects, and text answers
- `form`: intake, onboarding, requests, lead capture, and operational data collection

Prefer the simplest correct mode. Do not use `survey` when the user only needs one vote question. Do not use `poll` for a structured intake workflow.

## Mode-specific rules

### `poll`

Use when:

- the user wants one main question
- there are predefined options
- the goal is quick decision making or prioritization

Rules:

- keep one clear vote question
- keep options short and readable
- optionally collect `name`, `email`, and `comment` when the user asks or when lightweight identity/feedback would add value
- mention that repeat votes are currently blocked per browser in the MVP

### `survey`

Use when:

- the user needs multiple questions
- the user wants ratings plus comments
- the goal is product feedback, customer satisfaction, or structured research

Rules:

- keep question wording concise
- use text questions only when they add value
- do not overbuild long questionnaires when 3 to 6 questions would do the job

### `form`

Use when:

- the user needs structured data collection
- the task is onboarding, intake, requests, or lead capture
- responses should be operational and reusable later

Rules:

- keep fields practical and clearly labeled
- prefer standard fields like name, email, company, budget, timeline, and notes when relevant
- avoid unnecessary fields that slow completion

## Visibility rules

- default to `shared`
- use `public` only when the user explicitly wants an open link
- use `private` only when the user explicitly asks for restricted access

If the form should be answerable by others, it needs a shareable form URL.

## Tool usage

### `create_form`

Use this for the first form creation.

Expected inputs:

```json
{
  "title": "Next Feature Vote",
  "form_type": "poll",
  "source_text": "Question: What should we build next? Options: Forms results dashboard, Docs / invoices, Analysis, Tables.",
  "visibility": "shared",
  "collect_name": true,
  "collect_email": true,
  "collect_comment": true
}
```

### `get_form`

Use this when the user asks to inspect or retrieve an existing form.

### `share_form`

Use this when a form should be opened through a tokenized share link.

### `set_form_visibility`

Use this when the user explicitly asks to make a form private, shared, or public.

### `update_form`

Use this when the user wants to refine an existing form instead of creating a new one.

Typical cases:

- rename the form
- change options in a poll
- add or remove questions in a survey
- add optional identity/comment fields
- change visibility

### `list_form_responses`

Use this when the user asks for results, votes, comments, or summary.

Typical cases:

- "show me the poll results"
- "what did people say in the comments?"
- "summarize the feedback"
- "which option is winning?"

## Output format

Default creation output:

1. hosted form URL
2. one short explanation sentence

When the user asks for results:

1. one short summary of the result
2. the results URL when relevant
3. optionally a count or top option, but only if it comes directly from the tool response

Good creation response pattern:

```text
I created the poll:
https://pipintama.com/forms/<form-id>?t=<share-token>

It collects votes and optional name, email, and comment.
```

Good results response pattern:

```text
The leading option is "Forms results dashboard" with the most votes so far.

Results: https://pipintama.com/forms/<form-id>/results/
```

Only use live Pipintama URL patterns.

Valid:

- `https://pipintama.com/forms/<form-id>?t=<share-token>`
- `https://pipintama.com/forms/<form-id>/results/`

Invalid:

- `https://pipintama.com/form/<form-id>`
- `https://api.pipintama.com/forms/<form-id>/results.png`
