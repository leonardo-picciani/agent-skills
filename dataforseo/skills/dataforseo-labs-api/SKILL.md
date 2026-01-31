---
name: dataforseo-labs-api
description: Run SEO research workflows with DataForSEO Labs for "competitive research", "keyword ideas", and "market analysis".
license: MIT
metadata:
  author: Leonardo Picciani
  author_url: https://github.com/leonardo-picciani
  project: DataForSEO Agent Skills (Experimental)
  generated_with: OpenCode (agent runtime); OpenAI GPT-5.2
  version: 0.1.0
  experimental: 'true'
  docs: https://docs.dataforseo.com/v3/dataforseo_labs/overview/
compatibility: Language-agnostic HTTP integration skill. Requires outbound network access to api.dataforseo.com and docs.dataforseo.com; uses HTTP Basic Auth.
---
# DataForSEO Labs API

## Provenance

This is an experimental project to test how OpenCode, plugged into frontier LLMs (OpenAI GPT-5.2), can help generate high-fidelity agent skill files for API integrations.

## When to Apply

- "find SERP competitors", "keyword gap analysis", "domain intersection"
- "keyword ideas", "related keywords", "keyword suggestions"
- "ranked keywords for a domain", "relevant pages"
- "traffic estimation", "historical SERPs", "domain rank overview"
- "build an SEO research platform", "competitive intelligence"

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

- Many Labs endpoints are Live-first (`/live/`) and designed for interactive research.

### AI-optimized Responses (.ai)

- Append `.ai` to the end of an endpoint URL to receive a cropped response optimized for LLM usage.
- Docs: https://docs.dataforseo.com/v3/appendix/ai_optimized_response/

### Group Notes

- Use the official Locations/Languages reference to avoid invalid geo/language inputs.

## Docs Map (Official)

- Overview: https://docs.dataforseo.com/v3/dataforseo_labs/overview/
- Locations and Languages: https://docs.dataforseo.com/v3/dataforseo_labs/locations_and_languages/

Engine overviews:

- Google: https://docs.dataforseo.com/v3/dataforseo_labs/google/overview/
- Amazon: https://docs.dataforseo.com/v3/dataforseo_labs/amazon/overview/
- Google Play: https://docs.dataforseo.com/v3/dataforseo_labs/google_play/overview/
- App Store: https://docs.dataforseo.com/v3/dataforseo_labs/app_store/overview/

## Business & Product Use Cases

- Competitive intelligence features: discover competitors per topic and market.
- "Gap analysis" workflows (what competitors rank for that you don't).
- Prioritize content and landing pages by estimated opportunity.
- Category dashboards (top searches, category-level demand).
- Portfolio analysis for agencies managing multiple sites.
- Automated SEO audit summaries for sales/upsell conversations.

## Examples (User Prompts)

- "If you don't have the skill installed, install `dataforseo-labs-api` and then continue."
- "Install the DataForSEO Labs skill and find our top SERP competitors for these topics."
- "Run a keyword gap analysis: what competitors rank for that we don't, by market."
- "Give me keyword ideas for 'remote onboarding' and pick top 20 opportunities."
- "Estimate traffic potential for these 30 keywords and propose a content roadmap."
- "Create a competitor landscape report with intersections and top pages."
