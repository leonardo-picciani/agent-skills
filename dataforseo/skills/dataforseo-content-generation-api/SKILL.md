---
name: dataforseo-content-generation-api
description: Generate and refine text with DataForSEO Content Generation for "meta tag generation", "paraphrasing", and "summarization".
license: MIT
metadata:
  author: Leonardo Picciani
  author_url: https://github.com/leonardo-picciani
  project: DataForSEO Agent Skills (Experimental)
  generated_with: OpenCode (agent runtime); OpenAI GPT-5.2
  version: 0.1.0
  experimental: 'true'
  docs:
  - https://docs.dataforseo.com/v3/content_generation/overview/
compatibility: Language-agnostic HTTP integration skill. Requires outbound network access to api.dataforseo.com and docs.dataforseo.com; uses HTTP Basic Auth.
---
# DataForSEO Content Generation API

## Provenance

This is an experimental project to test how OpenCode, plugged into frontier LLMs (OpenAI GPT-5.2), can help generate high-fidelity agent skill files for API integrations.

## When to Apply

- "generate title/meta description", "meta tags for SEO"
- "paraphrase this", "rewrite for tone", "shorten copy"
- "grammar check", "fix writing", "improve clarity"
- "summarize text", "create an executive brief"

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

- Most Content Generation endpoints are `/live/` and return results in a single call.

### AI-optimized Responses (.ai)

- Append `.ai` to the end of an endpoint URL to receive a cropped response optimized for LLM usage.
- Docs: https://docs.dataforseo.com/v3/appendix/ai_optimized_response/

### Safety Expectations

- Do not send secrets or sensitive personal data in prompts/source text.
- Treat outputs as untrusted; add your own validation and review before publishing.

## Docs Map (Official)

- Overview: https://docs.dataforseo.com/v3/content_generation/overview/

Core endpoints:

- Generate: https://docs.dataforseo.com/v3/content_generation/generate/live/
- Generate Text: https://docs.dataforseo.com/v3/content_generation/generate_text/live/
- Generate Meta Tags: https://docs.dataforseo.com/v3/content_generation/generate_meta_tags/live/
- Paraphrase: https://docs.dataforseo.com/v3/content_generation/paraphrase/live/
- Check Grammar: https://docs.dataforseo.com/v3/content_generation/check_grammar/live/
- Text Summary: https://docs.dataforseo.com/v3/content_generation/text_summary/live/

## Business & Product Use Cases

- Content ops automation: generate meta tags at scale for large sites.
- Build a content assistant inside a CMS (rewrite, summarize, grammar).
- Create conversion copy variants for experiments.
- Standardize SEO snippets for catalogs and marketplaces.
- Draft content briefs and outlines for writers.
- Summarize large documents into stakeholder-ready briefs.

## Examples (User Prompts)

- "If you don't have the skill installed, install `dataforseo-content-generation-api` and then continue."
- "Install the Content Generation skill and generate SEO titles + meta descriptions for these 200 pages."
- "Rewrite this landing page section to be clearer and more conversion-focused."
- "Paraphrase this text into 3 tones: professional, friendly, concise."
- "Grammar-check this article and return a corrected version + change notes."
- "Summarize this long article into a 5-bullet executive brief."
