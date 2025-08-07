# Videre Tracker — Technical Findings & Recommendations

Scope: C#/.NET app with ASP.NET Core backend and React UI (WebView2). Sources: `ARCHITECTURE.md`, `README.md`, server source layout.

Reference: Organization overview — videre-project on GitHub: https://github.com/videre-project

## Verified facts (evidence)
- Backend: ASP.NET Core Web API launched in background thread; EF Core for persistence; SQLite connection builder in `DatabaseService.cs`.
- Frontend: React in WebView2 hosted by Windows Forms HostForm with JS↔C# interop and console log bridging.
- MTGOSDK integration via `ClientAPIService` singleton provider and recovery middleware.

## Strengths
- Clear layered architecture, robust reconnect/retry design for MTGO client.
- Good separation between UI host, API, and SDK connection management.
- Extensibility model documented (plugins via DI and interfaces).

## Risks / issues
- UI thread responsiveness: potential blocking on heavy operations if interop is synchronous.
- Error handling coverage: recovery middleware exists, but no evidence of global exception handling with user-safe prompts.
- Storage: SQLite default (good for dev) may hinder concurrency or large datasets; migration strategy not detailed.
- Packaging: installer/signing/auto-update flow not specified.

## Recommendations (prioritized)
1) Reliability & UX safety
- Global exception handler with graceful UI prompts and safe shutdown/restart.
- Background queue for heavy operations; ensure WebView2 interop calls are marshalled to the correct thread.

2) Data & migrations
- Add EF Core migrations and migration gating in CI; document schema versioning.
- Consider Postgres option for larger datasets; abstract via provider.

3) Telemetry & diagnostics
- Crash reporting (Sentry/Rollbar or custom with minidumps). Opt‑in telemetry with anonymized IDs.
- Structured logs with correlation IDs across SDK↔Tracker↔API.

4) Packaging & updates
- Signed installer; auto-update with delta patches and rollback (Squirrel/GH Releases/MSIX). Canary channel.

## Quick wins (1 week)
- Add `UseExceptionHandler` and `ProblemDetails` middleware; map common SDK exceptions.
- Introduce an async job queue + health endpoints.
- Add minimal crash reporter and log upload (opt‑in).

## Suggested PRs
- PR1: "Resilience": exception handler + problem details + healthchecks.
- PR2: "Telemetry": crash reporting + structured logs.
- PR3: "Data": EF migrations baseline + CI gate.
