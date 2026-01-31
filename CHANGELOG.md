# Changelog

All notable changes to this repository will be documented in this file.

The format is based on Keep a Changelog (https://keepachangelog.com/en/1.1.0/) and this project adheres to Semantic Versioning (https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- Added a standard `Steps`, `Inputs Checklist`, and language-agnostic `Example (cURL)` section to all DataForSEO skills.

### Fixed

- Ensured all DataForSEO skill `metadata` values are strings (including `metadata.docs`) for strict Agent Skills spec compatibility.

## [0.1.1] - 2026-01-31

### Added

- Added `compatibility` frontmatter to the DataForSEO skills bundle to clarify environment requirements (network access + HTTP Basic Auth).

### Changed

- Normalized DataForSEO skills `metadata` values to strings for stricter Agent Skills spec compatibility.

## [0.1.0] - 2026-01-31

### Added

- Initial DataForSEO bundle with 12 agent skills (SERP, AI Optimization, Keywords Data, Domain Analytics, Labs, Backlinks, OnPage, Content Analysis, Content Generation, Merchant, App Data, Business Data).
