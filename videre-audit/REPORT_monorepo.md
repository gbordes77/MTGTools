# monorepo — Technical Findings & Recommendations

Scope: Yarn workspaces for packages and services (`@videre-js`, `@videre-nodejs`, `serverless-*`, `videre-api`, `videre-bot`). Sources: `README.md`, packages/services trees.

Reference: Organization overview — videre-project on GitHub: https://github.com/videre-project

## Verified facts (evidence)
- Shared configs and global runner; extensive unit tests in util packages.
- Services include `videre-api` (Cloudflare Workers) with SQL scripts and validators.

## Strengths
- Strong DX focus: shared configs, test coverage, scripts, validators.
- API service structured with validators and typed queries.

## Risks / issues
- Cross-package version drift risk if release flow isn’t standardized.
- CI complexity across multiple runtimes (Node/Workers/Postgres).

## Recommendations (prioritized)
1) Consistent standards
- Enable strict TS across workspaces; ESLint/Prettier root config.
- Adopt Changesets for versioning and release notes; canary channel for services.

2) CI/CD
- Matrix builds with caching; CodeQL + secret scanning; SBOM (Syft) + Trivy for any containers.
- Contract tests for `videre-api` endpoints; record/replay fixtures.

3) Data/SQL alignment
- Keep `videre-api` SQL scripts aligned with `mtgo-db` migrations; automate drift checks.

## Quick wins (1 week)
- Add root `eslint` + `prettier` and enforce in CI.
- Add Changesets workflow for version bumps and changelogs.

## Suggested PRs
- PR1: "Lint & Strict TS" across workspaces.
- PR2: "Changesets & Releases".
- PR3: "API Contract Tests" for `videre-api`.
