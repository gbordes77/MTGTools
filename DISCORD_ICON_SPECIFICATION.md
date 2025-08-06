# MTGTools Discord Icon - Spécification Complète

## Vision Globale
Créer une icône Discord qui représente "La Forge des Outils Pro" - l'endroit où les talents techniques et les compétiteurs forgent ensemble des outils data-driven pour Magic: The Gathering.

## Mockup ASCII

```
┌────────────────┐
│                │
│      MTG       │  <- Lettres dorées, bold
│     Tools      │  <- Plus petit, sous MTG
│                │
│    ╔═════╗     │  <- Forge/enclume
│    ╚══╤══╝     │
│   ████████     │  <- Base trapézoïdale
│                │
│   ▐█▌▐██▌▐█▌   │  <- Barres de données
│   ▐█▌▐██▌▐██▌  │     (hauteurs variables)
│                │
└────────────────┘
```

## Structure en 4 Éléments

### 1. TEXTE (Partie Haute)
- **Ligne 1**: "MTG" - Large, bold, centré
- **Ligne 2**: "Tools" - Plus petit (60% de MTG), centré
- **Police**: Sans-serif bold (type Montserrat ou Inter)
- **Position**: Top 25% de l'icône

### 2. FORGE (Partie Centrale)
- **Forme**: Enclume stylisée géométrique
- **Composition**:
  - Rectangle supérieur (plateforme)
  - Trapèze inversé (corps de l'enclume)
  - Base rectangulaire
- **Position**: Centre de l'icône (40-60%)

### 3. DATA BARS (Partie Basse)
- **Nombre**: 4-5 barres verticales
- **Hauteurs**: Variables (60px, 80px, 100px, 90px)
- **Espacement**: Régulier
- **Style**: Coins arrondis (radius: 3px)
- **Dégradé**: Plus clair en haut de chaque barre
- **Position**: Bottom 25% de l'icône

### 4. EFFETS VISUELS
- **Glow**: Lueur dorée autour des éléments
- **Gradient**: Dégradé or (#fbbf24 → #f59e0b)
- **Étincelles**: Optionnel - petits points lumineux

## Palette de Couleurs

```
Primaire:
- Or principal: #fbbf24 (yellow-400)
- Or clair: #fde047 (yellow-300)
- Or foncé: #f59e0b (amber-500)

Secondaire:
- Noir fond: #000000
- Glow: #fbbf24 avec opacity 0.5

Accents:
- Highlights: #fde047
- Shadows: #d97706
```

## Dimensions & Contraintes

### Tailles Requises
- **512x512px**: Version haute résolution
- **128x128px**: Taille standard Discord
- **32x32px**: Miniature (doit rester lisible)

### Zones de Sécurité
- **Margin**: 10% de chaque côté
- **Text spacing**: 20px entre MTG et Tools
- **Element spacing**: 30px entre sections

## Hiérarchie Visuelle

1. **MTG** (plus gros, plus lumineux) - 30% de l'attention
2. **Forge** (forme distinctive) - 30% de l'attention
3. **Data bars** (mouvement/dynamisme) - 25% de l'attention
4. **Tools** (support du message) - 15% de l'attention

## Règles de Lisibilité

### À 512px
- Tous les détails visibles
- Gradients complexes OK
- Effets de glow prononcés

### À 128px
- MTG et forge clairement distincts
- Barres de données visibles individuellement
- "Tools" lisible

### À 32px
- "MTG" reste lisible
- Forme générale reconnaissable
- Couleur dorée distinctive

## Variantes

### Version 1: Statique
- Barres fixes à hauteurs différentes
- Pour Discord et avatars

### Version 2: Animée (optionnel)
- Barres qui pulsent doucement
- Étincelles qui montent
- Pour site web et présentations

## Messages à Transmettre

1. **Professionnalisme**: Design clean et moderne
2. **Data-driven**: Les barres représentent l'analyse
3. **Forge/Création**: On construit ensemble
4. **Gaming**: Lié à Magic sans être générique
5. **Open Source**: Accessible, pas élitiste

## Références Visuelles

- **Style**: Entre GitHub et Discord - tech mais accessible
- **Inspiration Forge**: Minecraft anvil (simplifié)
- **Inspiration Data**: Grafana/DataDog charts
- **Inspiration Text**: Logo Stripe (bold, simple)

## Checklist de Validation

- [ ] "MTG" lisible à 32px
- [ ] Reconnaissable en noir et blanc
- [ ] Distinct des autres serveurs Discord
- [ ] Cohérent avec le site web
- [ ] Exportable en PNG avec transparence
- [ ] Pas de détails perdus en compression
- [ ] Fonctionne sur fond clair ET foncé

## Notes Techniques

- **Format final**: PNG 512x512 avec transparence
- **Fallback**: Version carrée avec fond noir inclus
- **Optimisation**: < 100KB pour Discord
- **Accessibilité**: Contraste minimum 4.5:1