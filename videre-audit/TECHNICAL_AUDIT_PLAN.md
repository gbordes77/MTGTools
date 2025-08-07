# Videre Project – Technical Audit Plan (90-day)

Note: This document is written in English as requested. Conversation remains in French.

## Scope
Audit the codebases under the `videre-project` organization to produce an actionable plan for reliability, performance, security, and developer experience.

Reference: organization page — [videre-project on GitHub](https://github.com/videre-project)

## Repositories in scope (cloned locally)
- MTGOSDK (C#/.NET): SDK for inspecting/interacting with MTGO client memory
- Tracker (C# overlay + some JS tooling): real-time in-game/collection tracker
- asi-worker (Python + Wrangler): Archetype Similarity Index computation at the edge
- mtgo-db (TypeScript + Postgres + cloudflared): distributed DB for `api.videreproject.com`
- mlm (Python): ML/embeddings utilities
- MTGOBot (C# + pnpm workspace): MTGO event discovery/reporting bot
- monorepo (TypeScript workspaces): shared packages/services
- videre-bot (JS, archived): Discord bot (legacy)

## Architecture overview (from code discovery)
1) MTGO Client → MTGOSDK (Win32 memory reader) → normalized event stream
2) Event stream feeds:
   - Tracker (overlay UI + telemetry)
   - Ingestion/APIs (edge/Workers) → asi-worker (ASI) → mtgo-db (storage)
3) Public endpoints (metagame, matchups) → visualizations (Observable/website), bots/integrations

## Key audit questions
- Reliability: crash-free rate, memory safety, error handling, backpressure, retries
- Performance: allocations/GC (C#), IPC/stream throughput, network latency, DB contention
- Security: secrets handling, sandboxing, PII policy, code injection, supply chain
- Compliance: MTGO ToS risks of memory reading; distribution guardrails and disclaimers
- Observability: structured logs, metrics, tracing, dashboards, SLOs
- DX: onboarding time, test coverage, CI speed, release automation

## Methodology
1) Static review: solution topology, dependency graphs, CI configs, security policies
2) Build and test locally (Windows for C# components; containers for services)
3) Runtime profiling: perf/allocs for MTGOSDK & Tracker; load tests for APIs/DB
4) Security scans: CodeQL, Trivy, secret scanners; review of cloud access patterns
5) Findings → prioritized backlog with owners, estimates, acceptance criteria

## Preliminary repository findings (quick pass)

### MTGOSDK
- Structure: solution with `MTGOSDK`, `MTGOSDK.Win32`, `MTGOSDK.Tests`; extensive build props/targets.
- Risks: Win32 memory access (P/Invoke), handle safety, privilege elevation, anti-cheat heuristics.
- Actions:
  - Add unit/integration tests for memory readers with mock process snapshots
  - Introduce SafeHandle wrappers and guard-clauses around all Win32 calls
  - Benchmarks: BenchmarkDotNet suite for critical hot paths
  - Structured logging (EventSource/ETW/NLog) with log sampling
  - CodeQL and Dependabot; signed releases and symbol publishing

### Tracker
- Structure: C# app + `ARCHITECTURE.md`; includes `package.json` (possibly for UI assets).
- Risks: overlay injection, window hooks, update delivery, multi-monitor handling
- Actions:
  - Crash reporting (Sentry/Rollbar or custom) + anonymized telemetry opt-in
  - UI thread responsiveness watchdog; frame-time metrics
  - Installer/signing pipeline; auto-update channel with rollback
  - E2E smoke tests on Windows runners (GH Actions + Win VM)

### asi-worker
- Structure: Python with `wrangler.toml`, `uv.lock`, `pyproject.toml`.
- Risks: runtime compatibility (Python on Workers or WASM), cold start, numeric performance
- Actions:
  - Confirm Cloudflare Python Workers runtime or compile critical sections to WASM
  - Add property tests for ASI stability; golden datasets with tolerance bounds
  - Vectorization (NumPy) and optional numba/WASM acceleration
  - Observability: request metrics, latency histograms, error rate, budget alerts

### mtgo-db
- Structure: docker-compose, Postgres, cloudflared, scripts; pnpm monorepo style.
- Risks: schema drift, migrations, long-running queries, index health, DDoS on public endpoints
- Actions:
  - Adopt migration tool (Prisma/Drizzle/Flyway) + migration CI gate
  - Query plans review; add missing indexes; partitioning for time-series tables
  - Rate limiting, caching (KV/Redis), and pagination for heavy endpoints
  - Backups, PITR, and anonymization for shared datasets

### mlm
- Structure: Python utilities, embeddings scripts; README is empty.
- Risks: provenance of datasets, licensing, reproducibility
- Actions:
  - Fill README with dataset lineage, training recipes, eval metrics
  - Reproducible env via `uv` lock + model/artifact versioning (DVC/W&B)
  - Unit tests for feature extraction and evaluation harness

### MTGOBot
- Structure: C# solution + pnpm workspace; servers and scripts folders.
- Risks: event scraping robustness, rate limits, scheduling, duplicate detection
- Actions:
  - Idempotent ingestion with dedup keys; retry policies and jitter
  - Circuit breakers for upstream instability; structured logging
  - Containerize with health checks; GH Actions CI for build/test

### monorepo
- Structure: Yarn workspaces with `packages/` and `services/`.
- Risks: cross-package version drift, inconsistent tsconfig/eslint
- Actions:
  - Apply standard TS project references; strict TS; eslint + prettier
  - Single release process (changesets) + automated canary releases

### videre-bot (archived)
- Note: Legacy Discord bot; keep read-only; mine for useful patterns only.

## Cross-cutting recommendations
- CI/CD:
  - GitHub Actions matrices (Windows/Linux) for .NET/Python/Node
  - CodeQL, secret scanning, Dependabot, SBOM (Syft), container scans (Trivy)
  - Release pipelines with signed artifacts; provenance (SLSA level 2+)
- Observability:
  - Centralized logs (OTLP), metrics (Prom/Grafana or Grafana Cloud), tracing (OTel)
  - SLOs: API latency, error budgets; dashboards + alerting (PagerDuty/opsgenie)
- Security & compliance:
  - Memory access policy; legal review; in-app disclaimers and opt-in
  - Secrets via GitHub OIDC → cloud provider; no static long-lived tokens
- Data governance:
  - PII policy and data minimization; retention schedules; reproducible exports

## 30/60/90-day execution
- 30d: CI hardening, secret scanning, minimal test suites, error/crash reporting, schema migrations
- 60d: perf profiling (SDK/Tracker), ASI stability tests, API rate limits/caching, canary deploys
- 90d: SLOs and dashboards live, signed releases, backup/restore drills, contributor DX polish

## Deliverables
- Detailed findings per repo with annotated PRs
- Risk register and mitigation plan
- Benchmark results and perf budgets
- Roadmap with estimates, owners, and acceptance criteria


