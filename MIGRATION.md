# Migration from leonardo-picciani/agent-skills

This repository used to host multiple skill bundles under a single repo.
Skills are now split into dedicated repositories by domain.

## New canonical repositories

- DataForSEO: `leonardo-picciani/dataforseo-agent-skills`
- Senior ERP: `leonardo-picciani/senior-erp-agent-skills`

## Install mapping

### DataForSEO

```bash
# Old
npx skills add leonardo-picciani/agent-skills --skill dataforseo-serp-api

# New
npx skills add leonardo-picciani/dataforseo-agent-skills --skill dataforseo-serp-api
```

All DataForSEO skills now live in `leonardo-picciani/dataforseo-agent-skills`:

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

### Senior ERP

```bash
# Old
npx skills add leonardo-picciani/agent-skills --skill senior-erp-cliente-upsert

# New
npx skills add leonardo-picciani/senior-erp-agent-skills --skill senior-erp-cliente-upsert
```

All Senior ERP skills now live in `leonardo-picciani/senior-erp-agent-skills`:

- `senior-erp-cliente-upsert`
- `senior-erp-pedido-venda-criar`
- `senior-erp-pedido-venda-consultar-status`
- `senior-erp-estoque-consultar-disponibilidade`
- `senior-erp-titulos-consultar`

## Notes

- Skill names remain the same.
- Old `skills.sh/leonardo-picciani/agent-skills/<skill>` pages may remain indexed for some time.
