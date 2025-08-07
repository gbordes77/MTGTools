# asi-worker — Technical Findings & Recommendations

Scope: Cloudflare Worker (Python) computing Archetype Similarity Index (ASI). Sources: `README.md`, `SPECIFICATION.md`, `pyproject.toml`, `wrangler.toml`, `build.py`.

Reference: Organization overview — videre-project on GitHub: https://github.com/videre-project

## Verified facts (evidence)
- Endpoint: `POST https://ml.videreproject.com/asi?format=...` expects JSON array of card names; returns meta and data with scores.
- Uses D1 (Cloudflare) for bigrams; `build.py` updates bigrams; `uv` for deps.
- API key handled via env/Secrets (`CLOUDFLARE_API_KEY`).

## Strengths
- Clear spec and request/response contracts with example payloads.
- Good separation of router, worker, ASI library modules.

## Risks / issues
- Python on Workers: confirm runtime support/perf; risk of cold start and numeric performance.
- Input validation: large payloads could cause CPU spikes; need limits and timeouts.
- Observability: no explicit request metrics, rate limits, or caching strategy mentioned.

## Recommendations (prioritized)
1) Runtime & performance
- Validate Python runtime or compile core to WASM (e.g., Pyodide/NumPy-lite) for deterministic perf.
- Precompute/cache frequent formats; enable KV/Cache API with ETag.

2) API robustness
- Strict JSON schema validation (max cards, allowed formats, dedupe) and 413 handling.
- Rate limiting per IP/API token; add server-timeouts and circuit breakers to D1.

3) Observability
- Structured logs with request IDs; metrics: p50/p95 latency, D1 exec time, read_count, error rate.
- Alerting on error budget burn; add health endpoint.

## Quick wins (1 week)
- Add schema validator and payload size limits.
- Add basic caching (Cache API) and `If-None-Match` support.
- Enable Wrangler secrets; remove any plaintext keys from `.env` in CI.

## Suggested PRs
- PR1: "Validation & Limits": strict schema + 413 responses.
- PR2: "Caching & Metrics": Cache API + request metrics and logs.
- PR3: "Rate limiting": rudimentary token/IP limiter (Workers Durable Objects or KV).
