# Videre Public API (MVP)

Status: draft (based on code in `videre-audit/monorepo/services/videre-api/`), no unverified claims.

Base URL
- Production: `https://api.videreproject.com`

Conventions
- Format parameter values are title‑cased: `Standard`, `Modern`, `Pioneer`, `Legacy`, `Vintage`, `Pauper`
- Default window: last 31 days (`min_date`), up to `max_date` (today)
- Default `limit`: 100
- Errors: HTTP 4xx/5xx with JSON body `{ error: string }`

Auth
- Current endpoints documented here are public, no auth required.

Caching & rate limiting
- CDN/browser caching set via Cloudflare (Cache-Control): browser ~1h, CDN ~30min (see `CACHE_POLICY`)
- Pas de quotas explicites dans le code; gérer 429 si le CDN en renvoie

Endpoints

1) GET `/events/:format?`
- Description: list MTGO events, newest first
- Path params:
  - `format` (optional): one of formats above
- Query params (all optional):
  - `event_id` (number)
  - `min_date` (ISO date)
  - `max_date` (ISO date)
  - `limit` (number, default 100)
- Response (excerpt):
```json
[
  {
    "id": 123456,
    "name": "Standard Challenge 64",
    "date": "2025-08-03T17:00:00.000Z",
    "format": "Standard",
    "kind": "Challenge",
    "rounds": 7,
    "players": 64
  }
]
```
- Examples:
```bash
curl "https://api.videreproject.com/events/Standard?limit=10"
```
```ts
const r = await fetch("https://api.videreproject.com/events/Standard?limit=10");
const data = await r.json();
```
Sample response (limit=3):
```json
{"parameters":{"format":"Standard","min_date":"2025-07-08T11:20:45.298Z","max_date":"2025-08-08T11:20:45.298Z","limit":3},"data":[{"id":12807454,"name":"Standard Challenge 32","date":"2025-08-07T00:00:00.000Z","format":"Standard","kind":"Challenge","rounds":9,"players":53},{"id":12807448,"name":"Standard Preliminary","date":"2025-08-07T00:00:00.000Z","format":"Standard","kind":"Preliminary","rounds":4,"players":15},{"id":12807440,"name":"Standard Challenge 32","date":"2025-08-06T00:00:00.000Z","format":"Standard","kind":"Challenge","rounds":9,"players":59}]}
```

2) GET `/metagame/:format?`
- Description: aggregated metagame presence for a format
- Path params:
  - `format` (required by validator, optional in route signature): one of formats above
- Query params (optional): inherit from `events` (date range, limit)
- Response: rows from `getMetagame` (join de `presence` + `winrates`):
  - `archetype`, `count`, `percentage`, `match_count`, `match_winrate`, `match_ci`, `game_count`, `game_winrate`, `game_ci`
- Examples:
```bash
curl "https://api.videreproject.com/metagame/Modern?limit=50"
```
```ts
const r = await fetch("https://api.videreproject.com/metagame/Modern?min_date=2025-07-01");
const data = await r.json();
```
Sample response (limit=5):
```json
{"parameters":{"format":"Modern","min_date":"2025-07-08T11:20:45.291Z","max_date":"2025-08-08T11:20:45.291Z","limit":5},"data":[{"id":25356,"archetype":"Boros Energy","count":188,"percentage":"16.80%","match_count":659,"match_winrate":"50.99%","match_ci":"±3.82%","game_count":1684,"game_winrate":"50.97%","game_ci":"±2.38%"}]}
```

3) GET `/matchups/:format?`
- Description: matchup matrix by archetype for a format
- Path params:
  - `format` (required): format name
- Query params (optional):
  - `archetype` (string) — if provided, returns one row filtered to this archetype
  - Date window and `limit` like above
- Response: `[{ id, archetype, matchups: [{ id, archetype, match_count, match_winrate, match_ci, game_count, game_winrate, game_ci }] }]`
- Examples:
```bash
curl "https://api.videreproject.com/matchups/Pioneer?limit=100"
curl "https://api.videreproject.com/matchups/Standard?archetype=Dimir%20Midrange&limit=1"
```
Sample response (limit=1, excerpt):
```json
{"parameters":{"format":"Standard","min_date":"2025-07-08T11:20:45.307Z","max_date":"2025-08-08T11:20:45.307Z","limit":1},"data":[{"id":25671,"archetype":"Dimir Midrange","matchups":[{"id":27942,"archetype":"Izzet Cauldron","match_count":147,"match_winrate":"48.30%"}]}]}
```

4) GET `/archetypes/:format?`
- Description: deck statistics by archetype (mainboard/sideboard card presence)
- Path params:
  - `format` (required)
- Query params (optional):
  - `archetype` (string) — if provided, returns one row for that archetype
  - Date window and `limit` like above
- Response (excerpt):
```json
[
  {
    "archetype": "Dimir Midrange",
    "mainboard": [
      { "card": "Sheoldred, the Apocalypse", "count": 42, "percentage": "84.00%", "total": 126, "average": 3.00 }
    ],
    "sideboard": [
      { "card": "Duress", "count": 30, "percentage": "60.00%", "total": 45, "average": 1.50 }
    ]
  }
]
```
- Examples:
```bash
curl "https://api.videreproject.com/archetypes/Standard?limit=20"
```
Sample response (limit=1, excerpt):
```json
{"parameters":{"format":"Standard","min_date":"2025-07-08T11:20:45.295Z","max_date":"2025-08-08T11:20:45.295Z","limit":1},"data":[{"id":25671,"archetype":"Dimir Midrange","count":128,"mainboard":[{"card":"Swamp","count":128,"percentage":"100.00%","total":542,"average":4.23}],"sideboard":[{"card":"Duress","count":126,"percentage":"98.44%","total":261,"average":2.07}]}]}
```

5) GET `/mtgo/manifest`
- Description: returns parsed MTGO ClickOnce deployment manifest and application manifest (public Daybreak URLs)
- Response (excerpt):
```json
{
  "version": "3.4.0.0",
  "codebase": "MTGO_20250729_123456",
  "date": "2025-07-29T12:34:56",
  "public_key": "a1b2…",
  "dependencies": [
    { "name": "MTGO.Core", "file": "MTGO.Core.dll", "version": "3.4.0.0", "size": 123456 }
  ]
}
```
- Example:
```bash
curl "https://api.videreproject.com/mtgo/manifest"
```
Sample response (excerpt):
```json
{"version":"3.4.150.4579","codebase":"3.4.150.4579.20250805090037","date":"2025-08-05T09:00:37","public_key":"dbac2845cba5280e","dependencies":[{"name":"AdminScene","file":"AdminScene.dll","version":"3.4.150.4579","size":36864}]}
```

Validation & Defaults
- `format` is validated; invalid values return 400
- Optional params must have defaults (limit=100, min/max date set in backend)

Notes
- This document only lists routes present in the codebase above. If an endpoint is missing here, treat it as internal or not yet public.
- Shapes shown are indicative based on query names; exact fields may differ by DB schema version. Always inspect live JSON.
