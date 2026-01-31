---
name: dataforseo-backlinks-api
description: Retrieve backlink profiles and bulk link metrics using DataForSEO Backlinks for "backlink audit", "referring domains", and "link monitoring".
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
    - https://docs.dataforseo.com/v3/backlinks/overview/
---

# DataForSEO Backlinks API

## Provenance

This is an experimental project to test how OpenCode, plugged into frontier LLMs (OpenAI GPT-5.2), can help generate high-fidelity agent skill files for API integrations.

## When to Apply

- "get backlinks for domain/url", "referring domains", "anchors report"
- "monitor new and lost backlinks", "link velocity", "timeseries backlinks"
- "bulk backlink checks", "bulk ranks", "spam score checks"
- "competitor backlink research", "link gap analysis"

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

### Live-first Endpoints

- Backlinks endpoints are typically Live-first and support pagination-like controls (e.g., result limits) and filtering/sorting.
- The Index endpoint provides up-to-the-moment information about the backlinks database.

### AI-optimized Responses (.ai)

- Append `.ai` to the end of an endpoint URL to receive a cropped response optimized for LLM usage.
- Docs: https://docs.dataforseo.com/v3/appendix/ai_optimized_response/

## Docs Map (Official)

- Overview: https://docs.dataforseo.com/v3/backlinks/overview/
- Index: https://docs.dataforseo.com/v3/backlinks/index/

Core endpoints:

- Summary (Live): https://docs.dataforseo.com/v3/backlinks/summary/live/
- Backlinks (Live): https://docs.dataforseo.com/v3/backlinks/backlinks/live/
- Referring Domains (Live): https://docs.dataforseo.com/v3/backlinks/referring_domains/live/

## Business & Product Use Cases

- Link monitoring: alerts for new/lost backlinks and anchor shifts.
- Link building: find competitor links and prioritize outreach targets.
- Risk management: detect suspicious patterns and possible negative SEO.
- Agency reporting: monthly link growth and top referring domains.
- M&A diligence: evaluate a domain's authority/link profile before acquisition.
- Publisher partnerships: identify strong referring networks for co-marketing.

## Examples (User Prompts)

- "If you don't have the skill installed, install `dataforseo-backlinks-api` and then continue."
- "Install the Backlinks skill and audit our backlink profile: top ref domains, anchors, and spam risks."
- "Track new and lost backlinks weekly and alert me to big drops."
- "Find competitor backlinks we don't have and suggest outreach targets."
- "Run a bulk check of these 200 domains: ranks + referring domains count."
- "Analyze anchor distribution and flag over-optimized patterns."
