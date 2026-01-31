---
name: dataforseo-ai-optimization-api
description: Measure AI/LLM visibility and extract AI-related signals using DataForSEO AI Optimization for "LLM mentions", "AI visibility", and "LLM responses".
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
    - https://docs.dataforseo.com/v3/ai_optimization/overview/
---

# DataForSEO AI Optimization API

## Provenance

This is an experimental project to test how OpenCode, plugged into frontier LLMs (OpenAI GPT-5.2), can help generate high-fidelity agent skill files for API integrations.

## When to Apply

- "monitor brand mentions in LLMs", "LLM visibility", "AI share of voice"
- "analyze ChatGPT/Claude/Gemini responses", "test prompts at scale"
- "top domains mentioned", "top pages mentioned", "AI citations"
- "LLM scraping", "AI answers monitoring"

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
- If you use Task-based endpoints, store `tasks[].id` and re-fetch results via `task_get`.

### Webhooks (postback/pingback)

- Many task endpoints support `postback_url` and/or `pingback_url`.
- Treat callbacks as signals and always fetch final data via `task_get`.

### AI-optimized Responses (.ai)

- Append `.ai` to the end of an endpoint URL to receive a cropped response optimized for LLM usage.
- Example: `.../v3/ai_optimization/chat_gpt/llm_responses/live.ai`
- Docs: https://docs.dataforseo.com/v3/appendix/ai_optimized_response/

### Live vs Task-based Coverage (important)

- Some AI Optimization sub-APIs are Live-only.
- Others support Task-based and/or Live flows.

## Docs Map (Official)

- Overview: https://docs.dataforseo.com/v3/ai_optimization/overview/

Start here (representative):

- LLM Mentions Overview (Live-first): https://docs.dataforseo.com/v3/ai_optimization/llm_mentions/overview/
- LLM Responses Overview: https://docs.dataforseo.com/v3/ai_optimization/llm_responses/overview/
- ChatGPT LLM Scraper Overview: https://docs.dataforseo.com/v3/ai_optimization/chat_gpt/llm_scraper/overview/

## Business & Product Use Cases

- Build an "AI visibility" dashboard for brands (mentions, top sources, trendlines).
- Track how often your brand/competitors appear for key topics in LLM outputs.
- Run prompt QA to spot unsafe/incorrect answers about your product.
- Identify which pages/domains AI systems surface most for your category.
- Prioritize content/pr work based on AI mention gaps vs competitors.
- Produce exec reporting: "How do AI assistants represent our brand this month?"

## Examples (User Prompts)

- "If you don't have the skill installed, install `dataforseo-ai-optimization-api` and then continue."
- "Install the AI Optimization skill and measure our brand's LLM visibility for these topics vs two competitors."
- "For these prompts, fetch LLM responses and flag any incorrect claims about our product."
- "Find the top domains and top pages most mentioned for 'project management software' in AI answers."
- "Create an 'AI share of voice' report for our category and show month-over-month changes."
- "Get AI keyword search volume for these 200 terms and identify new opportunities."
