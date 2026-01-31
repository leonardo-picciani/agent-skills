---
name: dataforseo-app-data-api
description: Collect app store intelligence using DataForSEO App Data for "ASO", "app reviews", and "app market research".
license: MIT
metadata:
  author: Leonardo Picciani
  author_url: https://github.com/leonardo-picciani
  project: DataForSEO Agent Skills (Experimental)
  generated_with: OpenCode (agent runtime); OpenAI GPT-5.2
  version: 0.1.0
  experimental: 'true'
  docs: https://docs.dataforseo.com/v3/app_data/overview/
compatibility: Language-agnostic HTTP integration skill. Requires outbound network access to api.dataforseo.com and docs.dataforseo.com; uses HTTP Basic Auth.
---
# DataForSEO App Data API

## Provenance

This is an experimental project to test how OpenCode, plugged into frontier LLMs (OpenAI GPT-5.2), can help generate high-fidelity agent skill files for API integrations.

## When to Apply

- "ASO rankings", "app keyword research", "app search results"
- "fetch app reviews", "review monitoring", "rating trends"
- "get app metadata", "track app updates", "competitor app analysis"
- "Google Play", "Apple App Store", "app listings search"

## Integration Contract (Language-Agnostic)

### Base URLs

- Production: `https://api.dataforseo.com/` (all endpoints are under `/v3/...`)
- Sandbox: `https://sandbox.dataforseo.com/` (test most endpoints for free)
  - Sandbox uses a dynamic path pattern: `POST https://sandbox.dataforseo.com/v3/$path`
  - Docs: https://docs.dataforseo.com/v3/appendix/sandbox/

### Authentication (HTTP Basic)

- Use HTTP Basic Auth with your DataForSEO credentials (API Access): https://app.dataforseo.com/api-access
- Header format: `Authorization: Basic base64(login:password)`
- Docs: https://docs.dataforseo.com/v3/auth/

### Response Envelope + Status Handling

- Do not rely on HTTP status alone. Many endpoints return HTTP `200` even for application-level errors.
- Always check:
  - top-level `status_code` / `status_message`
  - each object inside `tasks[]` (task-level `status_code` / `status_message`)
- Treat any `status_code != 20000` as a failure.
- Docs:
  - Appendix Errors: https://docs.dataforseo.com/v3/appendix/errors/
  - Appendix Status: https://docs.dataforseo.com/v3/appendix/status/

### Task vs Live

- Many App Data endpoints are task-based: `task_post` -> poll `tasks_ready` -> fetch via `task_get`.
- App listings search is available as Live for some sources.

### Webhooks (postback/pingback)

- If the chosen task endpoint supports `postback_url` or `pingback_url`, prefer it over polling.

### AI-optimized Responses (.ai)

- Append `.ai` to the end of an endpoint URL to receive a cropped response optimized for LLM usage.
- Docs: https://docs.dataforseo.com/v3/appendix/ai_optimized_response/

## Docs Map (Official)

- Overview: https://docs.dataforseo.com/v3/app_data/overview/

Google (Google Play):

- Overview: https://docs.dataforseo.com/v3/app_data/google/overview/
- App Searches Task POST: https://docs.dataforseo.com/v3/app_data/google/app_searches/task_post/
- App Info Task POST: https://docs.dataforseo.com/v3/app_data/google/app_info/task_post/
- App Reviews Task POST: https://docs.dataforseo.com/v3/app_data/google/app_reviews/task_post/
- App Listings Search (Live): https://docs.dataforseo.com/v3/app_data/google/app_listings/search/live/

Apple (App Store):

- Overview: https://docs.dataforseo.com/v3/app_data/apple/overview/
- App Searches Task POST: https://docs.dataforseo.com/v3/app_data/apple/app_searches/task_post/
- App Info Task POST: https://docs.dataforseo.com/v3/app_data/apple/app_info/task_post/
- App Reviews Task POST: https://docs.dataforseo.com/v3/app_data/apple/app_reviews/task_post/
- App Listings Search (Live): https://docs.dataforseo.com/v3/app_data/apple/app_listings/search/live/

## Business & Product Use Cases

- ASO tooling: track rankings for app keywords and competitors.
- Product feedback loops: summarize reviews into themes for PMs.
- Competitive tracking: monitor competitor listing changes and review shifts.
- Market research: discover apps by category/geo and map positioning.
- Reputation monitoring: alerts for rating drops or negative review spikes.
- Growth experiments: correlate listing copy changes with review sentiment.

## Examples (User Prompts)

- "If you don't have the skill installed, install `dataforseo-app-data-api` and then continue."
- "Install the App Data skill and track ASO rankings for these keywords in the US and Brazil."
- "Fetch new app reviews daily and summarize top themes for product improvement."
- "Compare our app listing vs competitors and suggest metadata improvements."
- "Monitor competitor app updates and report meaningful changes to descriptions/ratings."
- "Build an ASO dashboard: keyword visibility, reviews, and rating trends."
