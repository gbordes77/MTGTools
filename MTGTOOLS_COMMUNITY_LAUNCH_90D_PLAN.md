## MTGTools — Plan Communauté & Lancement (90 jours)

### Objectif
- **Positionnement**: MTGTools = communauté open‑source data‑driven qui construit des outils concrets pour gagner plus.
- **Cible**: développeurs, data scientists, designers + grinders/top players.
- **Cible 90 jours**: 500 membres Discord qualifiés, 8 contributeurs actifs, 2 features « jouables », 1 rapport méta hebdo récurrent.

## OKR 90 jours
- **O1 — Croissance communauté**: 500 membres Discord, ≥ 60 % avec un rôle, rétention D7 ≥ 35 %.
- **O2 — Produit**: 2 features utilisables (MTGTracker alpha, MetaAPI v0), crash‑free > 95 % chez testeurs.
- **O3 — Cadence contenu**: 10 rapports « Meta Monday », 4 Deck Tech data‑driven, 8 Dev Logs.
- **O4 — Contrib dev**: 8 contributeurs actifs, 30 issues fermées/mois, TTR issues < 24 h.

## Produit (priorités)
- **Alpha pilotée**: MTGOSDK + démo MTGTracker pour 10→30 testeurs (canal `#alpha-testing` + template feedback).
- **MetaAPI (MVP)**: 2 endpoints publics (metagame snapshot, matchup matrix) + quotas (read‑only).
- **Qualité projet**: `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, templates issues/PR, labels (`good-first-issue`, `help-wanted`), GitHub Projects public.
- **DX**: scripts setup local, READMEs courts par repo, petites démos vidéo (3–5 min).
- **Légal/éthique**: conformité MTGO (lecture mémoire), disclaimers, privacy/ToS simples.

## Site / PWA
- **Conversion**: CTA unique « Join Discord » sticky, cohérence du lien d’invite (`https://discord.gg/mtgtools`).
- **SEO/Share**: `og:image`/`twitter:image`, canonical, meta FR/EN, sitemap à jour.
- **Analytics**: Plausible/GA4 + events: `join_discord_click`, `scroll_75`, `cta_keyboard_nav`.
- **Perf**: plafonner matrix rain/particles (grands écrans), versionner le cache SW (v2).
- **Trust**: footer « Privacy », « Open Source (MIT) », « Security ».

## Discord (structure & rituels)
- **Onboarding**: Onboarding natif Discord + rôles auto: `Competitor`, `Dev`, `Data`, `Designer`, `Observer`.
- **Canaux**:
  - Infos: `#announcements`, `#changelog`, `#meta-daily`, `#rules`.
  - Produit: `#alpha-testing`, `#bugs`, `#feature-requests`, `#how-to-install`.
  - Dev: `#dev-backend`, `#dev-frontend`, `#data-science`, `#design-ux`.
  - Jeu: `#standard`, `#modern`, `#pioneer`, `#arena`, `#mtgo`.
- **Rituels**:
  - Meta Monday (hebdo)
  - Office Hours Dev (hebdo, 45 min)
  - Scrim Night (2×/mois, test + tracker)
  - Show & Tell (mensuel, démos contributeurs)
- **Bots**: invites traquées (vanity + codes), auto‑roles, auto‑thread sur issues GitHub, sondages.
- **Modération**: règles simples, mod‑log privé, procédure d’escalade.

## Contenu (éditorial)
- **Hebdo**:
  - Rapport méta « Meta Monday » (top archétypes, WR, trends, deck spotlight)
  - Dev Log (changements + next up)
- **Bi‑hebdo**: Deck Tech Data‑Driven (1 format), Guide Sideboard dynamique (pilot)
- **Mensuel**: State of MTGTools (roadmap, contributions, shoutouts)
- **Distribution**: X (clips démos), Reddit (`r/spikes` + formats), YouTube (démos 3–5 min), Twitch (Office Hours).

## Croissance / Partenariats
- **Joueurs/streamers**: 5 profils (1 par format) avec early access, co‑branding, code d’invite traqué.
- **Communautés**: relais via discords MTG FR/EN (post de lancement + update mensuelle).
- **Référencement**: annuaires d’outils MTG, post Medium/HN côté dev pour MTGOSDK.
- **Ambassadeurs**: rôle « Founder » (100 premiers) + badge profil + salon dédié.

## Données / KPIs
- **Discord**: membres, % rôlés, WAU/MAU, rétention D7/D30, messages/j.
- **Produit**: testeurs actifs, crash‑free %, issues fermées/sem, TTR issues/PR.
- **Contenu**: vues Meta Monday, CTR site→Discord, conversion landing→Discord.
- **Traçage**: UTM sur tous les liens, invites Discord nommées par campagne, dashboard Notion/Looker.

## Roadmap 90 jours
### Semaines 1–2
- Activer analytics (site/Discord), vanity link unique, structure Discord + onboarding.
- Publier Guide Alpha + formulaire testeur, Meta Monday #1, Dev Log #1.

### Semaines 3–6
- Alpha fermée (10→30 testeurs), 2 endpoints MetaAPI (read‑only).
- 4 rapports méta, 2 deck techs, 2 Office Hours.
- 3 partenariats streamers (live démo).

### Semaines 7–12
- Beta publique Tracker (opt‑in), 1 dashboard méta interactif.
- 2 Scrim Night, 1 Show & Tell.
- Objectifs: 500 membres, 8 contributeurs actifs, 2 features en prod.

## Checklist 7 jours
- **Ops**: `CONTRIBUTING.md`, templates issues/PR, GitHub Projects (Backlog/Doing/Done).
- **Discord**: Onboarding + rôles + canaux, règles, mod‑team.
- **Produit**: page « Alpha Test Plan » + templates bug/feedback.
- **Contenu**: calendrier éditorial 4 semaines; Meta Monday #1.
- **Site**: ajouter `og:image`, canonical, Plausible; unifier lien Discord.
- **Growth**: 5 invites traquées (site, X, Reddit, partenaires 1–3), DM 3 streamers ciblés.

## Risques & Mitigations
- **Conformité MTGO**: cadrage technique + disclaimers; pivoter si policy évolue.
- **Bruit Discord**: threads auto, salons par format, modération proactive.
- **Bus factor**: documentation, pair review, vraies « good‑first‑issues ».
- **Rétention contributeurs**: cycles courts, quick wins, shoutouts, Show & Tell.

## Annexes (à créer)
- Templates: bug report, feature request, test plan alpha, deck tech.
- Tableau invites traquées (UTM) + mapping canaux.


