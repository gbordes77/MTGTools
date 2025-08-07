# MTGOBot — Technical Findings & Recommendations

Scope: C# bot for MTGO event data + Node server for serving/processing; pnpm workspaces. Sources: `README.md`, `server/src`, C# `src`.

Reference: Organization overview — videre-project on GitHub: https://github.com/videre-project

## Verified facts (evidence)
- Bot uses MTGOSDK; server scrapes (mtggoldfish, mtgo decklists) via puppeteer helpers.
- Env: `.env-example` requires MTGO and Postgres creds; pnpm workspace.

## Strengths
- Clear split between ingestion (C#) and serving (Node/Express).
- Types for SQL and jobs; helpers for puppeteer stealth.

## Risks / issues
- Scraping brittleness (selectors, anti-bot, site changes). Rate limits & bans.
- Deduplication/idempotency for events; scheduling and backoff not detailed.
- Secrets handling: ensure no plaintext defaults; use `.env` only locally.

## Recommendations (prioritized)
1) Robust ingestion
- Add idempotent keys on events; retries with jitter; circuit breakers; exponential backoff.
- Queue-based ingestion to isolate scraping from DB writes.

2) Observability
- Structured logs with correlation IDs; metrics for scrape success rate, time, and errors.
- Health checks and admin endpoints; dashboard.

3) Security & ops
- Headless browser hardening; proxy pool if needed; respect robots and site policies.
- Containerize and add health/readiness probes; CI on Windows/Linux.

## Quick wins (1 week)
- Add dedup on (eventId, source) at DB level.
- Implement retry/backoff wrappers around network ops.
- Add a small ops README for running the bot safely.

## Suggested PRs
- PR1: "Dedup & Retries".
- PR2: "Metrics & Health".
- PR3: "Container & CI".
