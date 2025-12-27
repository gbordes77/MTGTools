# MTGTools - Plan de Nettoyage du Projet

**Date d'analyse**: 27 Decembre 2025  
**Analyste**: Claude (Project Planner)  
**Statut**: EN ATTENTE DE VALIDATION

---

## RESUME EXECUTIF

| Metrique | Valeur |
|----------|--------|
| **Taille totale actuelle** | 272 MB |
| **Taille estimee apres nettoyage** | ~35 MB |
| **Espace recuperable** | ~237 MB (87%) |
| **Fichiers a supprimer** | ~400+ fichiers |
| **Fichiers a archiver** | ~25 fichiers |
| **Fichiers a deplacer** | ~15 fichiers |

---

## PHASE 1: INVENTAIRE COMPLET

### Repartition de l'espace disque

```
272 MB  TOTAL
├── 130 MB  videre-audit/        (48%) - Projet SEPARE
├──  66 MB  icons/               (24%) - Pages web sauvegardees INUTILES
├──  31 MB  .git/                (11%) - Normal
├──  25 MB  subagent-resources.zip (9%) - Archive HORS-SUJET
├──  17 MB  subagent-resources/   (6%) - Dossier HORS-SUJET
└──   3 MB  Reste du projet       (2%) - UTILE
```

### Structure actuelle des dossiers

```
MTGTools/
├── .claude/                    # Images de chat Claude (a nettoyer)
├── .github/                    # CI/CD (ESSENTIEL)
├── .vscode/                    # Config editeur (ESSENTIEL)
├── design/                     # Design system (ESSENTIEL)
│   ├── components/
│   └── tokens/
├── discord/                    # Ressources Discord (ESSENTIEL)
├── docs/                       # Documentation (ESSENTIEL)
│   └── design/
├── icons/                      # OBSOLETE - Pages web sauvegardees
├── marketing/                  # Contenu marketing (ESSENTIEL)
├── subagent-resources/         # HORS-SUJET - Agents Claude
├── videre-audit/               # HORS-SUJET - Projet separe
└── [52 fichiers .md racine]    # A trier
```

---

## PHASE 2: CLASSIFICATION DES FICHIERS

### Legende

| Statut | Description |
|--------|-------------|
| ESSENTIEL | Fichier actif et necessaire au projet |
| ARCHIVE | Ancien mais a conserver pour historique |
| OBSOLETE | A supprimer (redondant, remplace, inutile) |
| MAL PLACE | A deplacer dans un autre dossier |
| HORS-SUJET | N'appartient pas a ce projet |

---

### FICHIERS HTML

| Fichier | Taille | Derniere modif | Classification | Justification |
|---------|--------|----------------|----------------|---------------|
| `index.html` | 39 KB | 2025-12-27 | ESSENTIEL | Site principal actif |
| `index_old.html` | 115 KB | 2025-08-08 | ARCHIVE | Backup avant refonte |
| `index copie.html` | 115 KB | 2025-08-08 | OBSOLETE | Doublon exact de index_old.html |
| `index_mono.html` | 23 KB | 2025-08-31 | OBSOLETE | Version intermediaire depassee |
| `test.html` | 244 B | 2025-08-03 | OBSOLETE | Fichier de test temporaire |
| `reset_preferences.html` | 473 B | 2025-08-31 | MAL PLACE | Utilitaire -> tools/ |

---

### FICHIERS MARKDOWN RACINE

#### ESSENTIELS (a conserver a la racine)

| Fichier | Classification | Justification |
|---------|----------------|---------------|
| `README.md` | ESSENTIEL | Documentation principale |
| `CLAUDE.md` | ESSENTIEL | Instructions Claude Code |
| `HANDOFF.md` | ESSENTIEL | Suivi de session |
| `SESSION_NOTES.md` | ESSENTIEL | Notes de travail |
| `LICENSE` | ESSENTIEL | Licence du projet |

#### A ARCHIVER (planning/strategie obsolete)

| Fichier | Classification | Justification |
|---------|----------------|---------------|
| `30_60_90_DAY_IMPLEMENTATION_ROADMAP.md` | ARCHIVE | Roadmap aout 2025, depasse |
| `MTGTOOLS_COMMUNITY_LAUNCH_90D_PLAN.md` | ARCHIVE | Plan de lancement depasse |
| `LANDING_PAGE_TODO.md` | ARCHIVE | ToDo termine |
| `LANDING_PAGE_IMPLEMENTATION_PLAN.md` | ARCHIVE | Plan termine |
| `PLAN_B_SUMMARY.md` | ARCHIVE | Historique decision |
| `evolution_landing_page.md` | ARCHIVE | Historique |
| `site_modifications_complete.md` | ARCHIVE | Historique |
| `SESSION_TRACKING.md` | ARCHIVE | 45KB de logs, archiver |
| `AGENT_COORDINATION_GUIDE.md` | ARCHIVE | Guide agents non utilise |
| `agent_organizer_request.md` | ARCHIVE | Requete ponctuelle |

#### MAL PLACES (a deplacer)

| Fichier | Destination | Justification |
|---------|-------------|---------------|
| `DISCORD_BOT_SETUP.md` | `discord/` | Documentation Discord |
| `DISCORD_ENGAGEMENT_COMPLETE.md` | `discord/` | Documentation Discord |
| `DISCORD_ENHANCEMENT_PLAN.md` | `discord/` | Documentation Discord |
| `DISCORD_FINAL_STRUCTURE.md` | `discord/` | Documentation Discord |
| `DISCORD_ICON_SPECIFICATION.md` | `docs/design/` | Doublon, existe deja |
| `DISCORD_LAUNCH_STRATEGY.md` | `discord/` | Documentation Discord |
| `DISCORD_PRESEED_CONTENT.md` | `discord/` | Documentation Discord |
| `DISCORD_SEED_CONTENT_ENGLISH.md` | `discord/` | Documentation Discord |
| `DISCORD_TEMPLATE_V2.md` | `discord/` | Documentation Discord |
| `MTGTOOLS_DISCORD_VISION.md` | `discord/` | Documentation Discord |
| `discord-icon-final.svg` | `docs/design/` | Asset design |
| `INFRASTRUCTURE_AUDIT_REPORT.md` | `docs/` | Documentation technique |
| `CICD_PIPELINE_BLUEPRINT.md` | `docs/` | Documentation technique |
| `MONITORING_STRATEGY.md` | `docs/` | Documentation technique |
| `COST_OPTIMIZATION_PLAN.md` | `docs/` | Documentation technique |
| `GITHUB_PAGES_SETUP.md` | `docs/` | Documentation technique |
| `meta_descriptions.md` | `marketing/` | Contenu marketing |
| `guillaume_intro_english.md` | `marketing/` | Contenu marketing |
| `MTGTOOLS_MANIFESTO_EN.md` | `marketing/` | Contenu marketing |
| `MTGTOOLS_MANIFESTO_FR.md` | `marketing/` | Contenu marketing |
| `INTERNATIONAL_DIMENSION_TEXT.md` | `marketing/` | Contenu marketing |
| `requested_features.md` | `docs/` | Documentation produit |

#### POTENTIELLEMENT OBSOLETES (a revoir)

| Fichier | Classification | Justification |
|---------|----------------|---------------|
| `MTGTOOLS_STRATEGIC_ANALYSIS.md` | ARCHIVE? | Analyse strategique initiale |
| `MTGTOOLS_ANALYSE_STRATEGIQUE_COMPLETE.md` | ARCHIVE? | Doublon en francais? |
| `LANGUAGE_PHILOSOPHY.md` | ARCHIVE? | Philosophie etablie |
| `ANALYSIS_SITE_DISCORD_ALIGNMENT.md` | ESSENTIEL? | Recent (dec 2025) |
| `RELAUNCH_PLAN.md` | ESSENTIEL? | Recent (dec 2025) |

---

### DOSSIERS PROBLEMATIQUES

#### 1. `icons/` - 66 MB - OBSOLETE

**Contenu**: Pages web sauvegardees depuis un navigateur (probablement Figma ou autre outil)
- 3 fichiers HTML de 800KB+ chacun
- 3 dossiers `*_files/` avec CSS/JS (14MB chacun!)
- 2 fichiers PNG utiles: `discord server icon.png`, `telechargement.png`

**Diagnostic**: Ce sont des pages web completes sauvegardees, pas des icones.  
**Action**: Extraire les PNG utiles, supprimer le reste.

#### 2. `subagent-resources/` - 17 MB - HORS-SUJET

**Contenu**: Templates d'agents Claude Code de differents repos GitHub
- `temp-wshobson/` - Agents de wshobson
- `temp-lst97/` - Agents de lst97 avec images
- `subagent-resources/` - Sous-dossier imbrique

**Diagnostic**: Aucun rapport avec MTGTools. Probablement telecharge pour reference.  
**Action**: Deplacer vers `~/Documents/` ou supprimer.

#### 3. `subagent-resources.zip` - 25 MB - HORS-SUJET

**Contenu**: Archive du dossier subagent-resources  
**Diagnostic**: Doublon du dossier + metadata macOS  
**Action**: Supprimer (redondant).

#### 4. `videre-audit/` - 130 MB - HORS-SUJET

**Contenu**: Audit technique complet d'un ecosysteme MTGO
- `MTGOSDK/` - SDK .NET pour MTGO
- `MTGOBot/` - Bot Discord
- `Tracker/` - Application de tracking
- `monorepo/` - Monorepo JS avec Chromium (51MB!)
- `videre-bot/` - Autre bot
- `mlm/` - Machine learning
- `asi-worker/` - Worker ASI
- `mtgo-db/` - Database scripts

**Diagnostic**: Projet d'audit technique separe. Contient son propre `.git`.  
**Action**: Deplacer vers un repo/dossier separe.

#### 5. `.claude/claude-code-chat-images/` - ~1 MB

**Contenu**: Images de conversations Claude Code  
**Action**: Nettoyer periodiquement (peut etre supprime).

---

## PHASE 3: STRUCTURE PROPOSEE

```
MTGTools/
├── index.html                  # Site principal
├── manifest.json               # PWA config
├── sw.js                       # Service Worker
├── robots.txt                  # SEO
├── sitemap.xml                 # SEO
├── _config.yml                 # GitHub Pages
│
├── README.md                   # Documentation principale
├── CLAUDE.md                   # Instructions Claude
├── HANDOFF.md                  # Suivi session
├── SESSION_NOTES.md            # Notes de travail
├── LICENSE                     # Licence
│
├── .github/                    # CI/CD GitHub
│   ├── dependabot.yml
│   └── workflows/
│
├── .vscode/                    # Config editeur
│
├── assets/                     # NOUVEAU - Assets web
│   └── icons/
│       ├── discord-server-icon.png
│       └── discord-icon-final.svg
│
├── design/                     # Design system
│   ├── components/
│   │   └── button-variants.css
│   └── tokens/
│       └── design-tokens.json
│
├── discord/                    # Ressources Discord (consolide)
│   ├── COMMUNITY_RULES.md
│   ├── FAQ.md
│   ├── ONBOARDING_GUIDE.md
│   ├── BOT_SETUP.md
│   ├── LAUNCH_STRATEGY.md
│   ├── STRUCTURE.md
│   ├── VISION.md
│   ├── content/
│   │   ├── seed-content-en.md
│   │   ├── preseed-content.md
│   │   └── channel-descriptions.md
│   └── templates/
│       └── template-v2.md
│
├── docs/                       # Documentation technique
│   ├── API.md
│   ├── INFRASTRUCTURE.md
│   ├── CICD_PIPELINE.md
│   ├── MONITORING.md
│   ├── COST_OPTIMIZATION.md
│   ├── GITHUB_PAGES.md
│   └── design/
│       ├── discord-icon-specification.md
│       ├── discord-icon-visual-guide.md
│       └── discord-icon-example.svg
│
├── marketing/                  # Contenu marketing
│   ├── discord_landing_page.html
│   ├── discord_launch_content.md
│   ├── discord_launch_reddit_posts.md
│   ├── email_templates.md
│   ├── partner_streamer_kit.md
│   ├── homepage_taglines.md
│   ├── meta_descriptions.md
│   ├── manifesto-en.md
│   ├── manifesto-fr.md
│   └── international-dimension.md
│
├── tools/                      # NOUVEAU - Utilitaires
│   └── reset_preferences.html
│
└── archive/                    # NOUVEAU - Historique
    ├── 2025-08/
    │   ├── index_old.html
    │   ├── 30_60_90_roadmap.md
    │   ├── landing_page_todo.md
    │   ├── landing_page_plan.md
    │   ├── session_tracking.md
    │   └── ...
    └── strategy/
        ├── strategic_analysis_en.md
        ├── strategic_analysis_fr.md
        └── plan_b_summary.md
```

---

## PHASE 4: PLAN D'ACTION

### ETAPE 1: Sauvegarde (OBLIGATOIRE)

```bash
# Creer une sauvegarde complete avant toute modification
cd /Volumes/DataDisk/_Projects
tar -czvf MTGTools_backup_$(date +%Y%m%d).tar.gz MTGTools/
```

### ETAPE 2: Suppression des fichiers HORS-SUJET (237 MB)

```bash
cd /Volumes/DataDisk/_Projects/MTGTools

# Supprimer l'archive zip redondante (25 MB)
rm subagent-resources.zip

# Deplacer subagent-resources hors du projet (17 MB)
# Option A: Supprimer si non necessaire
rm -rf subagent-resources/

# Option B: Deplacer vers Documents
# mv subagent-resources ~/Documents/claude-agent-templates/

# Deplacer videre-audit vers un repo separe (130 MB)
mv videre-audit /Volumes/DataDisk/_Projects/videre-audit-standalone/
# OU supprimer si plus necessaire:
# rm -rf videre-audit/
```

### ETAPE 3: Nettoyage du dossier icons/ (66 MB)

```bash
cd /Volumes/DataDisk/_Projects/MTGTools

# Creer le dossier assets
mkdir -p assets/icons

# Sauvegarder les fichiers utiles
cp "icons/discord server icon.png" assets/icons/discord-server-icon.png
mv discord-icon-final.svg assets/icons/

# Supprimer le dossier icons problematique
rm -rf icons/
```

### ETAPE 4: Suppression des fichiers obsoletes

```bash
cd /Volumes/DataDisk/_Projects/MTGTools

# Supprimer les doublons HTML
rm "index copie.html"
rm index_mono.html
rm test.html
```

### ETAPE 5: Creation de la structure archive/

```bash
cd /Volumes/DataDisk/_Projects/MTGTools

# Creer les dossiers
mkdir -p archive/2025-08
mkdir -p archive/strategy
mkdir -p tools

# Deplacer les fichiers a archiver
mv index_old.html archive/2025-08/
mv 30_60_90_DAY_IMPLEMENTATION_ROADMAP.md archive/2025-08/30_60_90_roadmap.md
mv MTGTOOLS_COMMUNITY_LAUNCH_90D_PLAN.md archive/2025-08/
mv LANDING_PAGE_TODO.md archive/2025-08/
mv LANDING_PAGE_IMPLEMENTATION_PLAN.md archive/2025-08/
mv evolution_landing_page.md archive/2025-08/
mv site_modifications_complete.md archive/2025-08/
mv SESSION_TRACKING.md archive/2025-08/
mv AGENT_COORDINATION_GUIDE.md archive/2025-08/
mv agent_organizer_request.md archive/2025-08/

# Archiver les analyses strategiques
mv MTGTOOLS_STRATEGIC_ANALYSIS.md archive/strategy/
mv MTGTOOLS_ANALYSE_STRATEGIQUE_COMPLETE.md archive/strategy/
mv PLAN_B_SUMMARY.md archive/strategy/
mv LANGUAGE_PHILOSOPHY.md archive/strategy/

# Deplacer l'utilitaire
mv reset_preferences.html tools/
```

### ETAPE 6: Reorganisation Discord

```bash
cd /Volumes/DataDisk/_Projects/MTGTools

# Consolider la documentation Discord
mv DISCORD_BOT_SETUP.md discord/BOT_SETUP.md
mv DISCORD_FINAL_STRUCTURE.md discord/STRUCTURE.md
mv DISCORD_LAUNCH_STRATEGY.md discord/LAUNCH_STRATEGY.md
mv MTGTOOLS_DISCORD_VISION.md discord/VISION.md

# Creer sous-dossiers
mkdir -p discord/content
mkdir -p discord/templates

mv DISCORD_SEED_CONTENT_ENGLISH.md discord/content/seed-content-en.md
mv DISCORD_PRESEED_CONTENT.md discord/content/preseed-content.md
mv DISCORD_TEMPLATE_V2.md discord/templates/template-v2.md

# Supprimer le doublon (existe deja dans docs/design/)
rm DISCORD_ICON_SPECIFICATION.md

# Archiver les plans d'engagement (historique)
mv DISCORD_ENGAGEMENT_COMPLETE.md archive/2025-08/
mv DISCORD_ENHANCEMENT_PLAN.md archive/2025-08/
```

### ETAPE 7: Reorganisation docs/

```bash
cd /Volumes/DataDisk/_Projects/MTGTools

# Deplacer la documentation technique
mv INFRASTRUCTURE_AUDIT_REPORT.md docs/INFRASTRUCTURE.md
mv CICD_PIPELINE_BLUEPRINT.md docs/CICD_PIPELINE.md
mv MONITORING_STRATEGY.md docs/MONITORING.md
mv COST_OPTIMIZATION_PLAN.md docs/COST_OPTIMIZATION.md
mv GITHUB_PAGES_SETUP.md docs/GITHUB_PAGES.md
mv requested_features.md docs/REQUESTED_FEATURES.md
```

### ETAPE 8: Reorganisation marketing/

```bash
cd /Volumes/DataDisk/_Projects/MTGTools

# Deplacer le contenu marketing
mv meta_descriptions.md marketing/
mv guillaume_intro_english.md marketing/
mv MTGTOOLS_MANIFESTO_EN.md marketing/manifesto-en.md
mv MTGTOOLS_MANIFESTO_FR.md marketing/manifesto-fr.md
mv INTERNATIONAL_DIMENSION_TEXT.md marketing/international-dimension.md

# Deplacer les descriptions de channels
mv marketing/discord_channel_descriptions.md discord/content/channel-descriptions.md
```

### ETAPE 9: Nettoyage Claude cache

```bash
cd /Volumes/DataDisk/_Projects/MTGTools

# Supprimer le cache d'images Claude (optionnel)
rm -rf .claude/claude-code-chat-images/
```

### ETAPE 10: Commit final

```bash
cd /Volumes/DataDisk/_Projects/MTGTools

git add -A
git commit -m "chore: major project cleanup - reorganized structure, removed 237MB of unrelated files"
git push
```

---

## ESTIMATION DE L'ESPACE RECUPERE

| Action | Espace libere |
|--------|---------------|
| Supprimer `subagent-resources.zip` | 25 MB |
| Supprimer/deplacer `subagent-resources/` | 17 MB |
| Deplacer `videre-audit/` | 130 MB |
| Supprimer `icons/` (garder 2 PNG) | 65 MB |
| Supprimer doublons HTML | 250 KB |
| **TOTAL** | **~237 MB** |

**Taille finale estimee**: ~35 MB (dont 31 MB de .git)

---

## CHECKLIST DE VALIDATION

Avant d'executer ce plan, Guillaume doit confirmer:

- [ ] **subagent-resources/**: Supprimer ou deplacer vers `~/Documents/`?
- [ ] **videre-audit/**: Deplacer vers repo separe ou supprimer?
- [ ] **icons/**: Confirmer que seuls les 2 PNG sont utiles
- [ ] **Fichiers "ESSENTIEL?"**: Confirmer le statut de ANALYSIS_SITE_DISCORD_ALIGNMENT.md et RELAUNCH_PLAN.md
- [ ] **Archive**: Le dossier archive/ convient-il ou preferer supprimer?

---

## NOTES IMPORTANTES

1. **Ne rien supprimer sans backup** - La premiere commande cree une archive complete
2. **videre-audit contient des repos git** - Si deplace, les historiques git sont preserves
3. **Fichiers recents** - ANALYSIS_SITE_DISCORD_ALIGNMENT.md et RELAUNCH_PLAN.md sont de decembre 2025, donc probablement actifs
4. **PWA files** - `manifest.json` et `sw.js` doivent rester a la racine

---

*Document genere le 27 decembre 2025 par Claude Project Planner*
*En attente de validation avant execution*
