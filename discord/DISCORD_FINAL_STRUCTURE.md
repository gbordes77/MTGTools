# Discord MTGTools - Structure Finale

## Icônes pour les canaux existants

### WELCOME ZONE
- `#welcome` → 🚀 **ICÔNE VALIDÉE** - La fusée = on décolle ensemble
- `#📣-announcements` → 📣 (déjà présent)
- `#🔗-resources` → 🔗 (déjà présent)
- `#❓-faq` → ❓ (déjà présent)
- `#📜-charter` → 📜 (déjà présent)
- `#📖-welcome` → 📖 (déjà présent)

### COMMUNITY
- `#😄-introductions` → 😄 (déjà présent)
- `#💡-features` → 💡 (déjà présent)
- `#🐛-bug-reports` → 🐛 (déjà présent)
- `#💬-general-chat` → 💬 (déjà présent)
- `#🆘-support` → 🆘 (déjà présent)

### VIDERE PROJECT - Structure recommandée

#### Canaux Core (garder existants)
- `#dev-general` → 🔧
- `#ui-ux-design` → 🎨
- `#project-coordination` → 📋
- `#documentation` → 📚

#### Nouveaux canaux par composant GitHub
- `#⚙️-mtgosdk` → Discussion sur le SDK C# (repo principal, 14 stars)
- `#📊-tracker` → Le tracker temps réel MTGO (3 stars)
- `#🌐-api-worker` → API Cloudflare et ASI worker
- `#📈-observable` → Visualisations Observable (@qonfused/mtg-metagame)
- `#🤖-mtgobot` → Bot de recherche d'events
- `#🧠-mlm` → Machine learning pour archetypes

### FUTURE PROJECTS
(Garder vide pour l'instant - sera peuplé selon les besoins)

## Canaux à SUPPRIMER (redondants)
- `dev-general` dans VIDERE PROJECT → Trop générique, utiliser les canaux spécifiques
- Peut-être fusionner `ui-ux-design` et `project-coordination` en un seul `#🎯-project-planning`

## Structure finale VALIDÉE pour VIDERE PROJECT

```
VIDERE PROJECT
├── #⚙️-mtgosdk        (SDK C# + docs intégrées)
├── #📊-tracker         (Tracker app + docs intégrées)
├── #📈-observable      (Data viz metagame + docs intégrées)
├── #🌐-api-endpoints   (API & Workers + docs intégrées)
├── #🤖-bots           (MTGOBot & automation + docs intégrées)
├── #🧠-ml-archetypes  (Machine learning + docs intégrées)
├── #🎨-ui-ux-design   (Design & UX discussions)
└── #📋-project-coordination (Planning & roadmap)
```

## Canaux à MODIFIER MAINTENANT

### À CRÉER (6 nouveaux) :
1. `#⚙️-mtgosdk` - Le cœur du projet, SDK C#
2. `#📊-tracker` - Application principale de tracking
3. `#📈-observable` - Pour @qonfused/mtg-metagame
4. `#🌐-api-endpoints` - Toutes les APIs et workers
5. `#🤖-bots` - Automatisation et bots
6. `#🧠-ml-archetypes` - Machine learning pour classification

### À RENOMMER (2 existants) :
- `ui-ux-design` → `#🎨-ui-ux-design`
- `project-coordination` → `#📋-project-coordination`

### À SUPPRIMER (2 redondants) :
- ❌ `dev-general` (trop vague)
- ❌ `documentation` (intégrée dans chaque canal)

## Principe : Chaque canal = autonome

Chaque canal technique contient :
- Discussion du composant
- Documentation épinglée en haut
- Guides et tutoriels
- Issues et bug reports
- Roadmap spécifique

## Justification des choix

1. **Pas de canal docs global** : Chaque projet gère sa propre doc
2. **Séparation claire** : Un canal = un repo/projet GitHub
3. **Observable dédié** : Projet important avec @qonfused
4. **ML séparé** : Sujet complexe qui mérite son espace

## Prochaines actions

1. Ajouter les icônes manquantes
2. Créer les nouveaux canaux Videre
3. Supprimer/fusionner les canaux redondants
4. Épingler un message dans chaque canal expliquant son usage

## Notes

- Les icônes choisies sont standard Discord (pas d'emojis custom nécessaires)
- Structure modulaire : facile d'ajouter/retirer des canaux
- Focus sur les projets actifs (ceux avec activité GitHub)