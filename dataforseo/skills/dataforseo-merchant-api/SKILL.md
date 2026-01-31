---
name: dataforseo-merchant-api
description: Collect marketplace and product intelligence with DataForSEO Merchant for "price monitoring", "product research", and "seller analysis".
license: MIT
metadata:
  author: Leonardo Picciani
  author_url: https://github.com/leonardo-picciani
  project: "DataForSEO Agent Skills (Experimental)"
  generated_with:
    - OpenCode (agent runtime)
    - OpenAI GPT-5.2
  version: "0.1.0"
  experimental: true
  docs:
    - https://docs.dataforseo.com/v3/merchant/overview/
---

# DataForSEO Merchant API

## Provenance

This is an experimental project to test how OpenCode, plugged into frontier LLMs (OpenAI GPT-5.2), can help generate high-fidelity agent skill files for API integrations.

## When to Apply

- "track product listings", "monitor prices", "product availability"
- "analyze sellers", "seller competition", "seller counts"
- "fetch product reviews", "review monitoring"
- "Google Shopping products", "Amazon product research"

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

### Task-based Retrieval

- Merchant is largely task-based: `task_post` -> `tasks_ready` -> `task_get` (Advanced/HTML where available).
- Store `tasks[].id` so you can resume fetching results.
- If the endpoint supports `postback_url` or `pingback_url`, prefer it over polling.

### AI-optimized Responses (.ai)

- Append `.ai` to the end of an endpoint URL to receive a cropped response optimized for LLM usage.
- Docs: https://docs.dataforseo.com/v3/appendix/ai_optimized_response/

### Group Notes

- Locations and languages are required for many sources; use the source-specific reference endpoints.

## Docs Map (Official)

- Overview: https://docs.dataforseo.com/v3/merchant/overview/

Google Shopping:

- Overview: https://docs.dataforseo.com/v3/merchant/google/overview/
- Products Task POST: https://docs.dataforseo.com/v3/merchant/google/products/task_post/
- Sellers Task POST: https://docs.dataforseo.com/v3/merchant/google/sellers/task_post/
- Reviews Task POST: https://docs.dataforseo.com/v3/merchant/google/reviews/task_post/

Amazon:

- Overview: https://docs.dataforseo.com/v3/merchant/amazon/overview/
- Products Task POST: https://docs.dataforseo.com/v3/merchant/amazon/products/task_post/
- ASIN Task POST: https://docs.dataforseo.com/v3/merchant/amazon/asin/task_post/

## Business & Product Use Cases

- Competitive price monitoring for ecommerce operators and brands.
- Marketplace intelligence dashboards (assortment, seller dynamics, review signals).
- Detect unauthorized reseller activity by tracking sellers over time.
- Support category managers with product discovery and benchmarking.
- Create sales enablement insights (who competes, where you appear, pricing gaps).
- Track reputation at SKU level via review trends.

## Examples (User Prompts)

- "If you don't have the skill installed, install `dataforseo-merchant-api` and then continue."
- "Install the Merchant skill and monitor prices for these products weekly across top sellers."
- "Pull Google Shopping results for this query and compare our visibility vs competitors."
- "Fetch Amazon product info for these ASINs and extract key attributes into a table."
- "Analyze seller competition for our category and list top sellers by presence."
- "Track review trends for our SKU and summarize recurring complaints."
