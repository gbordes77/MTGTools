# mtgo-db — Technical Findings & Recommendations

Scope: Postgres + pgbouncer + Cloudflared tunnel; scripts and Node tooling. Sources: `docker-compose.yml`, `package.json`, `scripts/`.

Reference: Organization overview — videre-project on GitHub: https://github.com/videre-project

## Verified facts (evidence)
- Postgres exposed locally with tuned env vars; pgbouncer in front; Cloudflared tunnel container.
- Scripted helpers for tunnel setup and table listing in TS.

## Strengths
- Sensible separation (DB, pooler, tunnel) with healthchecks and resource limits.
- Clear local development posture (ports, volumes, init SQL mounts).

## Risks / issues
- Migrations: no explicit tool (Prisma/Drizzle/Flyway) visible; risk of schema drift.
- Backups/retention: not specified; volumes only.
- Security: ensure secrets via env, not hardcoded; tunnel auth management.

## Recommendations (prioritized)
1) Schema management
- Introduce migration tool and gate CI on forward/backward migrations.
- Version and document schema in `scripts/schema.sql`; auto-run migrations.

2) Performance & safety
- Index review and query plans for heavy endpoints; add partial/covering indexes.
- Enable logical backups (pg_dump) and PITR; schedule automated backups.

3) Access & security
- Rotate credentials; use Cloudflared scoped service tokens; restrict ingress/IP allowlists.

## Quick wins (1 week)
- Add `Makefile` with `migrate`, `backup`, `restore` recipes.
- Add `READMEs` for ops runbooks (backup/restore/checks).

## Suggested PRs
- PR1: "Migrations": adopt Drizzle/Prisma + baseline.
- PR2: "Backups": daily pg_dump + retention policy and restore doc.
- PR3: "Indexes": add missing indexes from `services/@videre-api/scripts/indexes.sql` alignment.
