# agent-skills

Experimental agent skills for coding agents.

Author: Leonardo Picciani (https://github.com/leonardo-picciani)

Tooling (experimental): OpenCode + OpenAI GPT-5.2

This repository is structured to work well with the Skills CLI (`npx skills`) and to be renderable/listable on https://skills.sh/.

---

## English

### What is this?

This repo is a multi-skill bundle. Each installable skill lives at `skills/<skill-name>/SKILL.md`.

### Install

List all available skills in this repo:

```bash
npx skills add leonardo-picciani/agent-skills --list
```

Install a specific skill by name:

```bash
npx skills add leonardo-picciani/agent-skills --skill dataforseo-serp-api
```

Tip: you can also list skills from your local clone:

```bash
npx skills add . --list
```

### Bundles

- `skills/` - installable skills (each `skills/<name>/SKILL.md`)
- `dataforseo/` - DataForSEO bundle notes/docs
- `senior/` - Senior (Brazilian ERP) bundle notes/docs

### Available Skills (high level)

DataForSEO (EN): 12 API integration skills (SERP, Backlinks, OnPage, etc.). See `dataforseo/README.md`.

Senior (pt-BR): ERP integration starter set (v0.1). See `senior/README.md`.

### Conventions

- Agent Skills format: each skill is a folder that contains at least `SKILL.md`.
- `SKILL.md` uses YAML frontmatter (`name`, `description`) + Markdown body.
- Skills should follow progressive disclosure: keep `SKILL.md` lean and move details into `references/`.

---

## Portugues (Brasil)

### O que e isto?

Este repositorio e um bundle com varias skills. Cada skill instalavel fica em `skills/<nome-da-skill>/SKILL.md`.

### Instalar

Listar todas as skills disponiveis neste repo:

```bash
npx skills add leonardo-picciani/agent-skills --list
```

Instalar uma skill especifica pelo nome:

```bash
npx skills add leonardo-picciani/agent-skills --skill senior-erp-cliente-upsert
```

Dica: voce tambem pode listar as skills a partir de um clone local:

```bash
npx skills add . --list
```

### Bundles

- `skills/` - skills instalaveis (cada `skills/<name>/SKILL.md`)
- `dataforseo/` - notas/documentacao do bundle DataForSEO
- `senior/` - notas/documentacao do bundle Senior (ERP brasileiro)

### Skills disponiveis (visao geral)

- DataForSEO (EN): 12 skills de integracao de API (SERP, Backlinks, OnPage, etc.). Veja `dataforseo/README.md`.
- Senior (pt-BR): conjunto inicial (v0.1) de integracao com ERP Senior. Veja `senior/README.md`.

## License

MIT (see `LICENSE`).
