# Videre Project — Quick Wins by Repository

Note: Document in English (requested). Use this as a single actionable checklist to drive the first PRs per repo.

## MTGOSDK
- Interop hardening: ensure `SetLastError`, `CharSet`, `CallingConvention` on all DllImports; central `Win32Error` helper.
- Safe handle adoption for process/thread/snapshot/toolhelp (wrap all raw `IntPtr`).
- Structured logging at interop boundaries (EventSource/NLog) with correlation IDs.
- BenchmarkDotNet micro-benchmarks for memory scan, pointer walking, object projection.

## Tracker
- Global exception handler + ProblemDetails; map SDK errors to user-safe messages.
- Async job queue for heavy operations; confirm WebView2 calls marshalled to UI thread.
- EF Core migrations baseline + CI gate; optional Postgres provider for large datasets.
- Crash reporting (opt-in) + minimal healthcheck endpoint.

## asi-worker
- Strict JSON schema validation (size limits, formats, dedupe) with 413 handling.
- Cache API + ETag support; precompute/cold cache for common formats.
- Request metrics (p50/p95, error rate), structured logs, health endpoint.
- Rate limiting (token/IP) via DO/KV; confirm Python runtime or move hotspots to WASM.

## mtgo-db
- Adopt migrations (Drizzle/Prisma/Flyway) + CI migration check.
- Add backup/restore scripts (daily `pg_dump`, retention) and runbook.
- Index review and alignment with API queries; partition large time-series tables if needed.

## mlm
- Fill README (purpose, datasets, licensing, examples).
- Add pytest baseline (BM25, tokenization, tagger fixtures).
- Reproducibility: seeds, artifact versioning (DVC/W&B) and basic eval script.

## MTGOBot
- Idempotency: dedup keys (eventId, source); retry with jitter; circuit breakers.
- Observability: structured logs + scrape metrics; health/readiness endpoints.
- Containerize; CI build/test on Windows/Linux; minimal ops README.

## monorepo
- Root ESLint/Prettier + strict TS across workspaces.
- Changesets for versioning and release notes; canary channel for services.
- API contract tests (record/replay) for `videre-api` endpoints.

## Suggested PR Order (first 2 weeks)
1) MTGOSDK: Interop hardening + SafeHandle (PR1), Diagnostics (PR2)
2) Tracker: Exception handler + migrations baseline (PR1)
3) asi-worker: Validation + 413, Metrics + Cache API (PR1/PR2)
4) mtgo-db: Migrations + backups (PR1)
5) MTGOBot: Dedup + retries (PR1)
6) monorepo: Lint + Changesets (PR1)

## Definition of Done (per quick win)
- Tests updated/added; CI green on relevant runners
- No secrets in code; docs updated (README/CHANGELOG)
- Rollback path documented when applicable
