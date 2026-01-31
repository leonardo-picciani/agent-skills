# DataForSEO Agent Skills (Experimental)

This folder is a DataForSEO bundle inside the central `agent-skills` repository.

Repo: https://github.com/leonardo-picciani/agent-skills/tree/main/dataforseo

It contains 12 separate, installable skill files for building language-agnostic integrations with the DataForSEO API v3.

Author: Leonardo Picciani (https://github.com/leonardo-picciani)

Tooling (experimental): OpenCode + OpenAI GPT-5.2

## Install only what you need

This is a multi-skill bundle: users should install only the skill(s) they need.

Option A (recommended, install by skill name):

```bash
npx skills add https://github.com/leonardo-picciani/agent-skills/tree/main/dataforseo --skill dataforseo-serp-api
```

Example:

```bash
npx skills add https://github.com/leonardo-picciani/agent-skills/tree/main/dataforseo --list
npx skills add https://github.com/leonardo-picciani/agent-skills/tree/main/dataforseo --skill dataforseo-serp-api
```

Option B (install by direct path):

```bash
npx skills add https://github.com/leonardo-picciani/agent-skills/tree/main/dataforseo/skills/dataforseo-serp-api
```

Tip: you can list available skills without installing:

```bash
npx skills add https://github.com/leonardo-picciani/agent-skills/tree/main/dataforseo --list
```

## Skills

Replace `dataforseo-serp-api` with one of:

- `dataforseo-serp-api`
- `dataforseo-ai-optimization-api`
- `dataforseo-keywords-data-api`
- `dataforseo-domain-analytics-api`
- `dataforseo-labs-api`
- `dataforseo-backlinks-api`
- `dataforseo-onpage-api`
- `dataforseo-content-analysis-api`
- `dataforseo-content-generation-api`
- `dataforseo-merchant-api`
- `dataforseo-app-data-api`
- `dataforseo-business-data-api`

## Docs

Official docs: https://docs.dataforseo.com/v3/

## License

MIT (see `../LICENSE`).
