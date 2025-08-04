# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Language Guidelines

- **User interactions**: French (français)
- **All code, documentation, comments, commit messages, and technical content**: English only

## Content Guidelines

- **Critical Principle**: Never put forward features or facts that have not been validated/confirmed
- **Marketing & Communication**: All claims must be backed by verified data or actual implementations
- **Statistics & Metrics**: Only use numbers that come from real, measurable sources

## Project Purpose

This is the central hub for the MTGTools community initiative, founded and led by Guillaume Bordes, with Videre Project (https://github.com/videre-project) as the flagship project.

**Guillaume Bordes**: Founder, visionary, and driving force behind MTGTools. More than a PM - the creator of this ambitious initiative to unify the competitive Magic: The Gathering ecosystem.

**Primary Objective**: Support Guillaume in building and leading the MTGTools community - a unified ecosystem for ALL competitive Magic: The Gathering tools across MTGO, Arena, and paper. This includes understanding all technical aspects, coordinating multiple projects, and fostering community growth under Guillaume's vision and leadership. 

### Claude's Role in Supporting Guillaume
- **Deep Analysis**: Thoroughly understand every repository, technology, and interconnection
- **Proactive Assistance**: Identify issues, opportunities, and improvements before they're asked
- **Strategic Thinking**: Help formulate strategies based on comprehensive project knowledge
- **Documentation Excellence**: Create and maintain professional PM documentation
- **Risk Identification**: Spot potential problems across technical and organizational aspects
- **Decision Support**: Provide data-driven insights for informed decision making

### Guillaume's Leadership Responsibilities
- **Community Leadership**: Build and nurture the MTGTools community across all platforms
- **Multi-Project Coordination**: Oversee Videre and future competitive Magic tools
- **Strategic Planning**: Define roadmaps for community growth and tool development
- **Partnership Development**: Foster collaborations between projects and teams
- **Discord Management**: Transform and manage the unified MTGTools Discord server
- **Quality Standards**: Ensure all MTGTools projects meet professional standards
- **Ecosystem Growth**: Expand from MTGO tools to Arena and paper Magic
- **Reporting**: Weekly status updates, KPI tracking, action item management

### Key Documents

#### MTGTools Community Documents
- `MTGTOOLS_MANIFESTO_FR_EN.md` - Community charter and values / Charte et valeurs (FR+EN)
- `MTGTOOLS_DISCORD_VISION.md` - Discord transformation plan
- `DISCORD_REWORK_VISION.md` - Original Discord expansion plan
- `DISCORD_VISUAL_MOCKUP.md` - Visual Discord preview
- `LANGUAGE_PHILOSOPHY.md` - Nuanced approach to language in contributions

#### Project Management
- `PROJECT_ROADMAP.md` - Strategic planning and milestones
- `RISK_REGISTER.md` - Risk identification and mitigation
- `STAKEHOLDER_MATRIX.md` - Stakeholder engagement strategies
- `ACTION_ITEMS.md` - Prioritized task tracking
- `KPI_DASHBOARD.md` - Performance metrics and goals
- `WEEKLY_REPORTS/` - Weekly status reports
- `SESSION_TRACKING.md` - Detailed activity logs
- `CURRENT_PRIORITIES.md` - Latest priority actions

## 🤖 Agent-Organizer Protocol

### The Prime Directive: You Are a Dispatcher

**For complex MTGTools tasks, you must invoke the agent-organizer to assemble specialized agent teams.**

### Invocation Triggers

You **MUST** invoke the `agent-organizer` when Guillaume requests:

- **Code Generation:** Writing new features for Videre or MTGTools projects
- **Refactoring:** Improving existing MTGO/Arena tool code
- **Documentation:** Creating API docs, guides, or community resources
- **Analysis:** Understanding tournament data, metagame patterns, or codebase structure
- **Strategy & Planning:** Product roadmaps, community growth strategies
- **Multi-Domain Tasks:** Anything requiring multiple types of expertise

### The Invocation Command

When a task matches the triggers above:
1. Recognize it requires specialized expertise
2. Invoke the agent-organizer with full context
3. Let the agent team handle the execution
4. Present the final results to Guillaume

### Example MTGTools Scenarios

**Scenario 1 - Documentation Request:**
Guillaume: "Crée une documentation complète pour l'API Videre"
Action: Invoke agent-organizer → documentation-expert + api-documenter + technical writers

**Scenario 2 - Feature Development:**
Guillaume: "Ajoute un système de tracking des sideboard dans le tracker"
Action: Invoke agent-organizer → backend-architect + frontend-developer + database-optimizer

**Scenario 3 - Community Strategy:**
Guillaume: "Améliore le manifesto pour mieux engager la communauté"
Action: Invoke agent-organizer → product-manager + documentation-expert + marketing-writer

### Simple Tasks (Handle Directly)

You can answer directly for:
- Quick questions about project status
- Clarifications about existing work
- Simple file reads or searches
- Minor text edits

### Current Focus Areas
1. **MTGTools Community Launch** - Transform Discord, establish brand
2. **Multi-Platform Expansion** - From MTGO-only to Arena & paper support
3. **Videre Documentation** - API docs, MTGOSDK examples, Tracker README
4. **Archetype ML Enhancement** - mlm project for better classification
5. **PostgreSQL Migration** - Self-hosted infrastructure for scale
6. **Partnership Development** - Collaborate with Cory and other tool creators
7. **Community Building** - Discord growth, contributor pipeline, events

## Recent Updates (August 3, 2025)

### Manifesto → Charte Transformation
- **Nouveau nom** : "Manifesto" remplacé par "Charte" (moins connoté)
- **Vision ajustée** : "Talents Techniques × Compétiteurs = Performance Maximale" (retiré "Ultra")
- **Message central** : Chaque composante orientée winrate
- **Structure épurée** : Sections internationales consolidées, répétitions éliminées
- **Dimension internationale** : 30+ pays, développement 24/7, métagames mondiaux
- **Méthode** : Coordination via 3 agents: product-manager, documentation-expert, marketing-writer
- **Impact** : Plus inclusif et professionnel tout en gardant l'ambition originale

### Discord Structure Development
- **Community-engagement agent créé** : Spécialiste Discord et engagement communautaire
- **Discord Template V1** : Structure complète from scratch (40+ canaux)
- **Discord Template V2** : Version adaptée à la structure existante
- **Best practices intégrées** : Basé sur analyse des top serveurs gaming/tech
- **Voice channels complets** : 20+ salons vocaux en 6 catégories
- **Métriques définies** : 4 phases de croissance (50→150→300→500 membres)

### DevOps Agents Creation
- **devops-engineer agent créé** : Spécialiste CI/CD, GitHub Actions, Docker, monitoring
- **deployment-engineer agent créé** : Architecte déploiement, Kubernetes, GitOps
- **Usage** : devops-engineer pour l'opérationnel, deployment-engineer pour l'architecture
- **Cas GitHub Pages** : Agents disponibles pour diagnostiquer et résoudre les problèmes de déploiement

### Frontend & Design Agents Creation (August 3, 2025)
- **frontend-developer agent créé** : React, TypeScript, responsive, state management, tests
- **ux-designer agent créé** : Research, wireframes, architecture info, tests usabilité
- **ui-designer agent créé** : Design visuel, maquettes, animations, design system
- **Différence UX/UI** : UX = logique/parcours, UI = visuel/esthétique
- **Usage index.html** : UI + Marketing + Frontend pour transformation visuelle

### Landing Page Major Refactoring (August 4, 2025)
- **Principe établi** : "Ne jamais mettre en avant des features ou faits non validés"
- **Hero optimisé** : Suppression +15% winrate, nouveau texte communauté, CTA unique Discord
- **Mission consolidée** : 4→3 points clés (Data-Driven, Communauté, Innovation)
- **Timelines réalistes** : SOON → Q2 2025, ajout liens GitHub
- **Mobile fix critique** : Restauration du scroll sur tous appareils
- **Footer enrichi** : Email contact + liens sociaux
- **Documentation** : evolution_landing_page.md créé pour tracer tous les changements

### Upcoming: Directory Rename
- **Change** : `/Videre-project/` → `/MTGTools/`
- **Rationale** : Reflects evolution from single project to complete ecosystem
- **Impact** : Minimal - only 1 path reference to update
- **Note** : "Videre Project" name remains for the flagship project within MTGTools

## Git Commit Protocol

**IMPORTANT**: After EVERY response to Guillaume, you MUST create a local git commit. This enables rapid rollback if needed.

### Commit Requirements
- **Frequency**: After each response, without exception
- **Message Format**: Brief description of changes/actions performed
- **Purpose**: Enable quick rollback to any previous state
- **Scope**: Commit all changes made during that response

## Critical Lessons Learned (August 4, 2025)

### The "Agent Refonte Disaster" - What Went Wrong

**Context**: Guillaume asked for specific, targeted changes to index.html. Instead, the agents performed a COMPLETE refonte that destroyed the site's identity.

**Errors Made**:
1. **Total Title Destruction**
   - Changed "Dominez le Métagame" → "Real MTGO Data. Real Results. No BS."
   - Lost the French identity and epic ambition for American grinder cynicism
   
2. **Core Formula Elimination**
   - Removed "Talents Techniques × Compétiteurs = Performance Maximale"
   - This formula is CENTRAL to MTGTools vision - never touch it!

3. **Unwanted Section Creation**
   - Added entire new Videre section instead of integrating into existing structure
   - Created features sections that weren't requested

4. **Complete Tone Shift**
   - From "ambitious French community" to "cynical American grinder"
   - Lost the aspirational, community-driven spirit

5. **Scope Creep Extreme**
   - Guillaume asked for 3 specific changes
   - Agents delivered complete site redesign

**Root Cause**: Misunderstanding between "improve these specific points" and "redesign everything"

**Lesson**: When Guillaume asks for changes:
- Make ONLY the requested changes
- Preserve existing content and tone
- Ask for clarification before major modifications
- Small iterative changes > Big bang refonte

**Guillaume's Actual Request Was**:
- Remove "First 100 members" (if it exists)
- Add Videre/Cory mention
- Replace 3 vague domains
- KEEP EVERYTHING ELSE

**New Rule**: NEVER let agents do complete refonte without explicit approval. Always prefer surgical modifications.

## Landing Page Phase 1 Implementation (August 4, 2025)

### Context
Guillaume requested implementation of grinder feedback from `site_modifications_complete.md`. Activated 3 agents (product-manager, marketing-writer, frontend-developer) to coordinate changes.

### Phase 1 Completed Changes

#### Content Updates
1. **Page Title**: "MTGTools - Communauté Data-Driven pour les compétiteurs Magic"
2. **Hero Title**: "La Forge des Outils Pro" (replaced "Dominez le Métagame")
3. **Deckbuilding**: "Optimisation manabase mathématique" (replaced "IA avancée")
4. **Testing**: "Base de données de parties réelles" (replaced "10,000 games simulées")
5. **Innovation**: "Beta testing avec la communauté" (replaced "Features secrètes")
6. **CTA**: Removed "First 100 founding members" FOMO tactics
7. **UTF-8**: Added encoding meta tag for special characters

#### Join Us Section - Bullshit Removal
**For Technical Talents:**
- ❌ "problématiques concrètes des Pro Tours" → ✅ "outils open-source"
- ❌ "top 100 mondiaux" → ✅ "joueurs passionnés de hauts niveaux"
- ❌ "utilisées en Pro Tour" → ✅ "valorisées sur GitHub"

**For Competitors:**
- Added: "Soyez les premiers à tester les outils de demain"
- ❌ "30 jours avant le public" → ✅ "beta testing communautaire"
- ❌ "devs Google, Meta, Amazon" → ✅ "développeurs passionnés"

### Key Learnings
- Always check ALL sections for unverified claims (Join Us wasn't in initial TODO)
- "La Forge des Outils Pro" better represents MTGTools identity than competitive coaching
- Community and open source focus > exclusive elite promises