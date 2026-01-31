---
name: dataforseo-serp-api
description: Fetch localized SERP results from DataForSEO (task or live) for "rank tracking", "get Google SERP", and "SERP monitoring".
license: MIT
metadata:
  author: Leonardo Picciani
  author_url: https://github.com/leonardo-picciani
  project: DataForSEO Agent Skills (Experimental)
  generated_with: OpenCode (agent runtime); OpenAI GPT-5.2
  version: 0.1.0
  experimental: 'true'
  docs:
  - https://docs.dataforseo.com/v3/serp/overview/
compatibility: Language-agnostic HTTP integration skill. Requires outbound network access to api.dataforseo.com and docs.dataforseo.com; uses HTTP Basic Auth.
---
# DataForSEO SERP API

## Provenance

This is an experimental project to test how OpenCode, plugged into frontier LLMs (OpenAI GPT-5.2), can help generate high-fidelity agent skill files for API integrations.

## When to Apply

- "track keyword rankings", "rank tracking", "SERP monitoring"
- "get Google SERP", "Bing SERP", "YouTube SERP", "localized SERP"
- "compare SERP by country/city", "location-based SERP", "language-based SERP"
- "SERP features", "local pack", "news results", "images results"
- "SERP screenshot", "SERP HTML", "SERP snapshot"
- "build an SEO dashboard", "SERP alerts", "SERP volatility"

## Integration Contract (Language-Agnostic)

### Base URLs

- Production: `https://api.dataforseo.com/` (all endpoints are under `/v3/...`)
- Sandbox: `https://sandbox.dataforseo.com/` (test most endpoints for free)
  - Sandbox uses a dynamic path pattern: `POST https://sandbox.dataforseo.com/v3/$path`
  - Docs: https://docs.dataforseo.com/v3/appendix/sandbox/

### Authentication (HTTP Basic)

- Use HTTP Basic Auth with your DataForSEO credentials (API Access): https://app.dataforseo.com/api-access
- Language-agnostic header:
  - `Authorization: Basic base64(login:password)`
- Docs: https://docs.dataforseo.com/v3/auth/

### Request/Response Envelope + Status Handling

- Many endpoints return HTTP `200` even for application-level errors; do not rely on HTTP status alone.
- Always check:
  - top-level `status_code` / `status_message`
  - each object inside `tasks[]` (task-level `status_code` / `status_message`)
- Treat any `status_code != 20000` as a failure and surface a helpful error with:
  - `status_code`, `status_message`, and the relevant `tasks[].id` (if present)
- Docs:
  - Appendix Errors: https://docs.dataforseo.com/v3/appendix/errors/
  - Appendix Status: https://docs.dataforseo.com/v3/appendix/status/

### Live vs Task-based Endpoints

- Live endpoints return results in a single call (synchronous).
- Task-based endpoints follow: `task_post` -> poll `tasks_ready` -> fetch via `task_get`.
- Prefer task-based endpoints for scheduled or high-volume workflows.

### Webhooks (postback/pingback)

- Many task endpoints support `postback_url` and/or `pingback_url` so your system can receive completion callbacks.
- If webhooks are used, implement signature/verification if documented, and always re-fetch results with `task_get`.

### AI-optimized Responses (.ai)

- You can often append `.ai` to the end of an endpoint URL to receive a cropped response optimized for LLM usage.
- Example: `.../v3/serp/google/organic/live/advanced.ai`
- Docs: https://docs.dataforseo.com/v3/appendix/ai_optimized_response/

### Implementation Expectations (for the agent)

1) Choose the exact SERP endpoint family (Google/Bing/YouTube/etc.) and the result format (Regular/Advanced/HTML) from the docs.
2) Collect required inputs:
   - query/keyword
   - location + language (when applicable)
   - device, depth, and any optional SERP modifiers
3) Decide Live vs Task-based flow.
4) Execute HTTP request(s) with Basic Auth.
5) Validate `status_code` and return:
   - a normalized, compact result for the user
   - the raw response payload for debugging

## Docs Map (Official)

- Overview: https://docs.dataforseo.com/v3/serp/overview/
- Endpoints list: https://docs.dataforseo.com/v3/serp/endpoints/
- Example task flow (Google Organic Task POST): https://docs.dataforseo.com/v3/serp/google/organic/task_post/
- Authentication: https://docs.dataforseo.com/v3/auth/
- Sandbox: https://docs.dataforseo.com/v3/appendix/sandbox/
- Errors: https://docs.dataforseo.com/v3/appendix/errors/
- AI-optimized response: https://docs.dataforseo.com/v3/appendix/ai_optimized_response/

## Business & Product Use Cases

- Build a rank tracking product (scheduled keywords, multi-location, historical charts).
- Monitor competitors' search visibility across markets and languages.
- Detect SERP volatility and feature changes and send alerts to stakeholders.
- Validate SEO impact after releases (content updates, internal linking, template changes).
- Power an SEO reporting dashboard for clients (white-label PDFs/CSVs).
- Feed SERP output into a content roadmap (what formats and intent types win).

## Examples (User Prompts)

- "If you don't have the skill installed, install `dataforseo-serp-api` and then continue."
- "Install the DataForSEO SERP skill and track daily rankings for these 50 keywords in New York (EN)."
- "Get the top 10 Google organic results for 'best running shoes' in Brazil (PT) and summarize the intent."
- "Compare SERPs for 'crm software' in US vs UK and highlight different competitors."
- "Pull Google Maps results for 'pizza near me' in Chicago and extract top businesses + ratings."
- "Take a SERP screenshot for 'wireless earbuds' in Germany and save the URL in the report."
