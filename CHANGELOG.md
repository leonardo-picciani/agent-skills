# Changelog

All notable changes to this repository will be documented in this file.

The format is based on Keep a Changelog (https://keepachangelog.com/en/1.1.0/) and this project adheres to Semantic Versioning (https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Changed

- Deprecated this monorepo and moved published skills into dedicated repositories:
  - `leonardo-picciani/dataforseo-agent-skills`
  - `leonardo-picciani/senior-erp-agent-skills`

### Added

- Added a standard `Steps`, `Inputs Checklist`, and language-agnostic `Example (cURL)` section to all DataForSEO skills.
- Added the initial Senior (Brazilian ERP) bundle (v0.1) with 5 installable skills:
  - `senior-erp-cliente-upsert`
  - `senior-erp-pedido-venda-criar`
  - `senior-erp-pedido-venda-consultar-status`
  - `senior-erp-estoque-consultar-disponibilidade`
  - `senior-erp-titulos-consultar`
- Added `references/REFERENCE.md` (pt-BR) to each Senior skill with X Platform auth/headers/security/reliability conventions.
- Updated docs to document the Senior v0.1 skills list and install commands.

### Changed

- Previously: restructured repository to use the standard `skills/<skill>/SKILL.md` layout so skills.sh can render owner/repo skill tables.
- Added `references/REFERENCE.md` to each DataForSEO skill and slimmed `SKILL.md` to better follow the progressive disclosure best practice.

### Fixed

- Ensured all DataForSEO skill `metadata` values are strings (including `metadata.docs`) for strict Agent Skills spec compatibility.

### Added

- Added a repository `CHANGELOG.md` (Keep a Changelog format) to track skill evolution.

## [0.1.1] - 2026-01-31

### Added

- Added `compatibility` frontmatter to the DataForSEO skills bundle to clarify environment requirements (network access + HTTP Basic Auth).

### Changed

- Normalized DataForSEO skills `metadata` values to strings for stricter Agent Skills spec compatibility.

## [0.1.0] - 2026-01-31

### Added

- Initial DataForSEO bundle with 12 agent skills (SERP, AI Optimization, Keywords Data, Domain Analytics, Labs, Backlinks, OnPage, Content Analysis, Content Generation, Merchant, App Data, Business Data).
