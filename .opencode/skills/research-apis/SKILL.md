---
name: research-apis
description: Use when the user wants to research a third-party API, learn how to set up a developer account, get API keys, or see example requests. Triggers on requests to explore, integrate, or understand external APIs.
---

# Research APIs

Research third-party APIs and produce a ready-to-use integration guide with working examples.

## Process

If the user does NOT specify which API or service to research, ASK:

> What API or service would you like to research? (e.g., Stripe, AccessTrade, Shopify, Twilio)

Once the API is known, research and produce the output below.

## Output Format

Generate a markdown file saved to `docs/api-research/{api-name}.md` with this structure:

```markdown
# {API Name} — API Research

## 1. Developer Account Setup

| Step | Action |
|------|--------|
| 1 | Go to `{signup-url}` |
| 2 | {Registration steps} |
| 3 | {Verification or approval process} |
| ... | ... |

**Approval time:** {instant / X days / manual review}

## 2. API Key / Authentication

| Item | Detail |
|------|--------|
| **Auth type** | {API key / OAuth2 / Bearer token / etc.} |
| **Where to find** | {Dashboard path to get credentials} |
| **Header format** | `{e.g., Authorization: Bearer <token>}` |
| **Rate limits** | {requests per second/minute if known} |

## 3. API Examples

### {Endpoint name} — {short description}

**curl**

\`\`\`bash
curl -X {METHOD} '{full-url}' \
  -H 'Authorization: Bearer <YOUR_API_KEY>' \
  -H 'Content-Type: application/json' \
  -d '{request-body}'
\`\`\`

**Sample Response**

\`\`\`json
{
  "status": 200,
  "data": { ... }
}
\`\`\`

**{Library name}** ({language})

\`\`\`{language}
{library code example}
\`\`\`

(Repeat for each relevant endpoint)
```

## Rules

- Use **WebSearch** and **WebFetch** to find official API documentation
- Always show **curl first**, then a library example (pick the most popular SDK/library for that API)
- Include **real endpoint URLs** from official docs — do not fabricate URLs
- Include **sample request bodies** and **sample responses** based on official docs
- If the API has a sandbox/test mode, note it in the authentication section
- If official docs are unclear, state what is uncertain rather than guessing
- Group endpoints by the user's use case, not by the full API surface — only cover what the user needs
