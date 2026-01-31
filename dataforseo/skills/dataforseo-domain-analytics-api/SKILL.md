---
name: dataforseo-domain-analytics-api
description: Enrich and analyze domains with DataForSEO Domain Analytics for "tech stack detection", "domain research", and "lead enrichment".
license: MIT
metadata:
  author: Leonardo Picciani
  author_url: https://github.com/leonardo-picciani
  project: DataForSEO Agent Skills (Experimental)
  generated_with: OpenCode (agent runtime); OpenAI GPT-5.2
  version: 0.1.0
  experimental: 'true'
  docs: https://docs.dataforseo.com/v3/domain_analytics/overview/
compatibility: Language-agnostic HTTP integration skill. Requires outbound network access to api.dataforseo.com and docs.dataforseo.com; uses HTTP Basic Auth.
---
# DataForSEO Domain Analytics API

## Provenance

This is an experimental project to test how OpenCode, plugged into frontier LLMs (OpenAI GPT-5.2), can help generate high-fidelity agent skill files for API integrations.

## When to Apply

- "what tech does this site use", "detect CMS/frameworks", "technology footprint"
- "find domains by technology", "build a tech-based prospect list"
- "WHOIS lookup", "domain ownership signals", "registrar data"
- "enrich leads with web tech", "segment accounts by stack"

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

### Live-first Usage

- Domain Analytics is commonly Live-first (no crawl tasks); filters/locations/languages are key.

### AI-optimized Responses (.ai)

- Append `.ai` to the end of an endpoint URL to receive a cropped response optimized for LLM usage.
- Docs: https://docs.dataforseo.com/v3/appendix/ai_optimized_response/

## Docs Map (Official)

- Overview: https://docs.dataforseo.com/v3/domain_analytics/overview/

Technologies:

- Technologies Overview: https://docs.dataforseo.com/v3/domain_analytics/technologies/overview/
- Technologies Filters: https://docs.dataforseo.com/v3/domain_analytics/technologies/filters/
- Technologies Locations: https://docs.dataforseo.com/v3/domain_analytics/technologies/locations/
- Technologies Languages: https://docs.dataforseo.com/v3/domain_analytics/technologies/languages/

Whois:

- Whois Overview: https://docs.dataforseo.com/v3/domain_analytics/whois/overview/
- Whois Filters: https://docs.dataforseo.com/v3/domain_analytics/whois/filters/
- Whois Overview (Live endpoint doc): https://docs.dataforseo.com/v3/domain_analytics/whois/overview/live/

## Business & Product Use Cases

- Sales/BD enrichment: tag prospects by CMS/ecommerce platform/analytics tools.
- Build a "BuiltWith-style" product experience using DataForSEO datasets.
- Identify integration opportunities (target sites using a specific platform).
- Monitor competitor stack changes (replatforming, analytics migrations).
- Add WHOIS/tech signals to risk scoring and fraud detection.
- Segment partner programs by stack compatibility.

## Examples (User Prompts)

- "If you don't have the skill installed, install `dataforseo-domain-analytics-api` and then continue."
- "Install the Domain Analytics skill and detect the tech stack for these 500 domains."
- "Find prospects using Shopify in the US and return a ranked list of domains."
- "Enrich this lead list with CMS, analytics tools, and hosting signals."
- "Run a WHOIS overview for these domains and highlight risky registration patterns."
- "Compare our tech stack vs competitor stacks and summarize differences."
