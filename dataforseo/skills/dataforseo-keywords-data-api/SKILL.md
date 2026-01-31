---
name: dataforseo-keywords-data-api
description: Retrieve keyword metrics and trends using DataForSEO Keywords Data for "keyword research", "search volume", and "ad planning".
license: MIT
metadata:
  author: Leonardo Picciani
  author_url: https://github.com/leonardo-picciani
  project: DataForSEO Agent Skills (Experimental)
  generated_with: OpenCode (agent runtime); OpenAI GPT-5.2
  version: 0.1.0
  experimental: 'true'
  docs: https://docs.dataforseo.com/v3/keywords_data/overview/
compatibility: Language-agnostic HTTP integration skill. Requires outbound network access to api.dataforseo.com and docs.dataforseo.com; uses HTTP Basic Auth.
---
# DataForSEO Keywords Data API

## Provenance

This is an experimental project to test how OpenCode, plugged into frontier LLMs (OpenAI GPT-5.2), can help generate high-fidelity agent skill files for API integrations.

## When to Apply

- "get search volume", "keyword research", "keyword metrics"
- "CPC", "competition", "ad traffic", "paid search planning"
- "Google Trends", "seasonality", "rising queries"
- "clickstream", "market sizing", "global search volume"

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

### Live vs Task-based Endpoints

- Live endpoints return results in a single call (synchronous).
- Task-based endpoints typically follow: `task_post` -> poll `tasks_ready` -> fetch via `task_get`.
- If you use Task-based endpoints:
  - store `tasks[].id`
  - fetch results via `task_get`
  - optionally use `postback_url`/`pingback_url` to avoid polling

### Webhooks (postback/pingback)

- Many task endpoints support `postback_url` and/or `pingback_url`.
- Treat callbacks as signals; fetch final data via `task_get`.

### AI-optimized Responses (.ai)

- Append `.ai` to the end of an endpoint URL to receive a cropped response optimized for LLM usage.
- Example: `.../v3/keywords_data/google_ads/search_volume/live.ai`
- Docs: https://docs.dataforseo.com/v3/appendix/ai_optimized_response/

### Group Notes

- Many keyword endpoints support both Live and Task-based flows; task-based is often used for bulk/scheduled jobs.

## Steps

1) Identify the exact endpoint(s) in the official docs for this use case.
2) Choose execution mode:
   - Live (single request) for interactive queries
   - Task-based (post + poll/webhook) for scheduled or high-volume jobs
3) Build the HTTP request:
   - Base URL: `https://api.dataforseo.com/`
   - Auth: HTTP Basic (`Authorization: Basic base64(login:password)`) from https://docs.dataforseo.com/v3/auth/
   - JSON body exactly as specified in the endpoint docs
4) Execute and validate the response:
   - Check top-level `status_code` and each `tasks[]` item status
   - Treat any `status_code != 20000` as a failure; surface `status_message`
5) For task-based endpoints:
   - Store `tasks[].id`
   - Poll `tasks_ready` then fetch results with `task_get` (or use `postback_url`/`pingback_url` if supported)
6) Return results:
   - Provide a normalized summary for the user
   - Include the raw response payload for debugging

## Inputs Checklist

- Credentials: DataForSEO API login + password (HTTP Basic Auth)
- Target: keyword(s) / domain(s) / URL(s) / query string (depends on endpoint)
- Targeting (if applicable): location + language, device, depth/limit
- Time window (if applicable): date range, trend period, historical flags
- Output preference: regular vs advanced vs html (if the endpoint supports it)

## Example (cURL)

```bash
curl -u "${DATAFORSEO_LOGIN}:${DATAFORSEO_PASSWORD}"   -H "Content-Type: application/json"   -X POST "https://api.dataforseo.com/v3/<group>/<path>/live"   -d '[
    {
      "<param>": "<value>"
    }
  ]'
```

Notes:
- Replace `<group>/<path>` with the exact endpoint path from the official docs.
- For task-based flows, use the corresponding `task_post`, `tasks_ready`, and `task_get` endpoints.


## Docs Map (Official)

- Overview: https://docs.dataforseo.com/v3/keywords_data/overview/

Representative endpoints:

- Google Ads Search Volume (Live): https://docs.dataforseo.com/v3/keywords_data/google_ads/search_volume/live/
- Google Ads Search Volume (Task POST): https://docs.dataforseo.com/v3/keywords_data/google_ads/search_volume/task_post/
- Google Trends Explore (Live): https://docs.dataforseo.com/v3/keywords_data/google_trends/explore/live/
- Clickstream Data Overview: https://docs.dataforseo.com/v3/keywords_data/clickstream_data/overview/

## Business & Product Use Cases

- Power a keyword research product (seed -> expand -> prioritize -> export).
- Support paid search planning (market size, seasonality, geo targeting).
- Build topic clustering for content strategy (group by demand and intent).
- Forecast traffic potential for new pages/features (SEO business cases).
- Identify new markets by comparing geo/language demand patterns.
- Provide client-facing keyword reports for agencies and consultants.

## Examples (User Prompts)

- "If you don't have the skill installed, install `dataforseo-keywords-data-api` and then continue."
- "Install the Keywords Data skill and get search volume for this list of keywords in Canada (EN)."
- "Generate keyword ideas from this seed topic and cluster them with a priority score."
- "Show seasonality for 'tax filing software' and recommend publishing months."
- "Use clickstream data to estimate market size for these topics globally vs the US."
- "Build a simple keyword research workflow: seed -> expand -> filter -> export."
