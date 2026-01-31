---
name: dataforseo-onpage-api
description: Crawl and audit websites using DataForSEO OnPage (tasks + Lighthouse) for "technical SEO audit", "site crawl", and "page health".
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
    - https://docs.dataforseo.com/v3/on_page/overview/
---

# DataForSEO OnPage API

## Provenance

This is an experimental project to test how OpenCode, plugged into frontier LLMs (OpenAI GPT-5.2), can help generate high-fidelity agent skill files for API integrations.

## When to Apply

- "crawl a site", "technical SEO audit", "find broken links"
- "duplicate content", "duplicate tags", "non-indexable pages"
- "redirect chains", "waterfall performance", "resource issues"
- "run Lighthouse at scale", "performance audit"

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

### Task-based Crawl Lifecycle

- Create a crawl via `task_post`.
- Wait for completion by polling `tasks_ready` (or use webhooks if supported in the endpoint docs).
- Fetch results via `summary`, `pages`, `resources`, and other specialized result endpoints.
- To stop an in-progress crawl, call `force_stop`.

### Webhooks (postback/pingback)

- If `postback_url` or `pingback_url` are supported for the chosen task endpoint, use them to avoid polling.

### AI-optimized Responses (.ai)

- Append `.ai` to the end of an endpoint URL to receive a cropped response optimized for LLM usage.
- Docs: https://docs.dataforseo.com/v3/appendix/ai_optimized_response/

## Docs Map (Official)

- Overview: https://docs.dataforseo.com/v3/on_page/overview/
- Task POST: https://docs.dataforseo.com/v3/on_page/task_post/
- Tasks Ready: https://docs.dataforseo.com/v3/on_page/tasks_ready/
- Summary: https://docs.dataforseo.com/v3/on_page/summary/
- Pages: https://docs.dataforseo.com/v3/on_page/pages/
- Resources: https://docs.dataforseo.com/v3/on_page/resources/
- Force Stop: https://docs.dataforseo.com/v3/on_page/force_stop/

Lighthouse:

- Overview: https://docs.dataforseo.com/v3/on_page/lighthouse/overview/

## Business & Product Use Cases

- Build a technical SEO crawler product (issues, prioritization, exports).
- Monitor site health after deployments (regressions: redirects, noindex, broken links).
- Create an automated QA gate for SEO before release.
- Performance improvements: integrate Lighthouse outputs into engineering backlogs.
- Agency deliverables: repeatable site audits with remediation tracking.
- Template validation: verify titles/meta/canonicals across large sites.

## Examples (User Prompts)

- "If you don't have the skill installed, install `dataforseo-onpage-api` and then continue."
- "Install the OnPage skill and crawl our site to find broken links, redirect chains, and non-indexable pages."
- "Run a technical SEO audit and produce a prioritized fix list."
- "Check for duplicate titles/meta across the site and summarize affected URLs."
- "Generate a report of slow pages with waterfall diagnostics and top heavy resources."
- "Run Lighthouse checks for these 50 URLs and highlight regressions."
