# MTGTools - Project Documentation

## Project Overview

**MTGTools** is a community hub for competitive Magic: The Gathering players and IT professionals. The project aims to co-create open-source tools that provide measurable impact on players' winrates.

**Type**: Static website (landing page) + Community resources  
**Stack**: Pure HTML/CSS/JS (no framework)  
**Hosting**: GitHub Pages  
**Live URL**: https://gbordes77.github.io/MTGTools/

## Core Mission

```
Technical Talents × Competitive Players = Maximum Performance
```

MTGTools connects:

- **Grinders**: Competitive players seeking data-driven tools
- **IT Professionals**: Developers who play Magic and want to contribute
- **Open Source Philosophy**: Everything transparent and collaborative

## Project Structure

```
MTGTools/
├── index.html              # Main landing page (bilingual EN/FR)
├── index_old.html          # Backup of previous version
├── index_mono.html         # Intermediate monolingual version
├── manifest.json           # PWA configuration
├── sw.js                   # Service Worker for offline support
├── _config.yml             # GitHub Pages configuration
├── robots.txt              # SEO robots configuration
├── sitemap.xml             # SEO sitemap
│
├── design/                 # Design system
│   ├── components/         # CSS component styles
│   │   └── button-variants.css
│   └── tokens/             # Design tokens
│       └── design-tokens.json
│
├── discord/                # Discord community resources
│   ├── COMMUNITY_RULES.md  # Server rules
│   ├── FAQ.md              # Frequently asked questions
│   └── ONBOARDING_GUIDE.md # New member guide
│
├── marketing/              # Marketing materials
│   ├── discord_channel_descriptions.md
│   ├── discord_launch_content.md
│   ├── discord_launch_reddit_posts.md
│   ├── email_templates.md
│   ├── homepage_taglines.md
│   └── partner_streamer_kit.md
│
├── videre-audit/           # Technical audit of Videre Project
│   ├── ARCHITECTURE.md     # System architecture diagram
│   ├── QUICK_WINS.md       # High-impact fixes checklist
│   ├── TECHNICAL_AUDIT_PLAN.md
│   ├── REPORT_*.md         # Individual repo reports
│   ├── MTGOSDK/            # SDK source code audit
│   ├── Tracker/            # Tracker app audit
│   └── [other repos]/      # Additional Videre repos
│
├── docs/                   # Documentation assets
│   └── design/             # Design documentation
│
├── icons/                  # Icon assets
│
└── [Documentation Files]   # Project documentation (*.md)
```

## Key Files

### Website

| File            | Purpose                                          |
| --------------- | ------------------------------------------------ |
| `index.html`    | Main site - 500 lines, bilingual, dark mode, PWA |
| `manifest.json` | PWA manifest with app metadata                   |
| `sw.js`         | Service Worker v3 for caching                    |
| `_config.yml`   | GitHub Pages Jekyll config                       |

### Documentation (Root)

| File                         | Purpose                      |
| ---------------------------- | ---------------------------- |
| `README.md`                  | Public project documentation |
| `HANDOFF.md`                 | Session handoff notes        |
| `SESSION_NOTES.md`           | Detailed session logs        |
| `MTGTOOLS_MANIFESTO_EN.md`   | English manifesto/charter    |
| `MTGTOOLS_MANIFESTO_FR.md`   | French manifesto/charter     |
| `MTGTOOLS_DISCORD_VISION.md` | Discord server structure     |

## Technology Stack

### Frontend (Static Site)

- **HTML5**: Semantic markup, bilingual with `data-lang` attributes
- **CSS3**: Custom properties (CSS variables), responsive design
- **JavaScript**: Vanilla JS for language toggle, dark mode, PWA
- **Font**: Inter (Google Fonts)
- **Icons**: Inline SVG (Discord, GitHub)

### Features

- **Bilingual**: English default, French toggle (localStorage persistence)
- **Dark Mode**: Toggle with localStorage persistence
- **PWA**: Installable with offline support
- **Responsive**: Mobile-first design with breakpoint at 768px

### Design System

- **Primary Color**: `#3B82F6` (Blue)
- **Theme**: Light default, dark mode available
- **Typography**: Inter font family, weights 400-800
- **Layout**: Max-width 1200px container

## External Integrations

### Videre Project (Flagship)

- **GitHub**: https://github.com/videre-project
- **MTGOSDK**: C# SDK for MTGO data extraction
- **Observable**: https://observablehq.com/@qonfused/mtg-metagame

### Community

- **Discord**: https://discord.gg/nzb6mVctAb
- **GitHub Pages**: https://gbordes77.github.io/MTGTools/

## Development Commands

```bash
# View site locally
open index.html

# Or use Python server for proper MIME types
python -m http.server 8000

# Push to GitHub (auto-deploys to Pages)
git add -A
git commit -m "description"
git push

# Check live site (wait 2-5 min after push)
open https://gbordes77.github.io/MTGTools/
```

## LocalStorage Keys

| Key                       | Values                | Purpose             |
| ------------------------- | --------------------- | ------------------- |
| `language`                | `'en'` \| `'fr'`      | Language preference |
| `theme`                   | `'light'` \| `'dark'` | Theme preference    |
| `mtgtools-v2-initialized` | `'true'`              | First load flag     |

## Content Guidelines

### Language Rules

- **User interactions**: French (français)
- **Code, docs, commits**: English only
- **Website**: Bilingual with English default

### Critical Principles

- **Never claim unverified features or facts**
- **All statistics must be from real, measurable sources**
- **Undersell rather than overpromise**
- **Community focus over marketing hype**

## Current Status (December 2025)

### Completed

- Site redesign (Plan B - August 31, 2025)
- Bilingual support (EN/FR)
- Dark mode implementation
- PWA configuration
- Discord server structure defined
- Videre Project technical audit

### In Progress

- Discord community launch
- API documentation for MTGOSDK
- Contributor onboarding

### Planned

- Real tool development based on community needs
- Partnership development
- Multi-platform expansion (MTGO → Arena → Paper)

## Key Lessons Learned

### From August 2025 Sessions

1. **No Bullshit**: Never inflate metrics or make unverified claims
2. **Surgical Changes**: Make only requested changes, preserve existing content
3. **Verify Before Claiming**: Count and check before stating numbers
4. **Community First**: Focus on co-creation, not marketing promises
5. **Trust Through Transparency**: Admit errors immediately

### Site Evolution

- **Before**: Black/yellow, Matrix animations, 1700 lines, marketing hype
- **After**: White/blue, clean design, 500 lines, co-creation focus

## Quick Reference

### File Editing

```bash
# Main site
vim index.html

# Design tokens
vim design/tokens/design-tokens.json

# Discord content
vim discord/COMMUNITY_RULES.md
```

### Testing PWA

1. Open site in Chrome
2. DevTools → Application → Service Workers
3. Check "Offline" and refresh

### Updating Content

1. Edit `index.html` sections with `data-lang="en"` and `data-lang="fr"`
2. Test both languages locally
3. Commit and push
4. Wait 2-5 minutes for GitHub Pages deployment

## Project Philosophy

> "Every feature aims to bring concrete value to players."

MTGTools is not about:

- Marketing buzzwords
- Fake statistics
- Exclusive elite promises

MTGTools is about:

- Real tools for real players
- Open source collaboration
- Data-driven competitive advantage
- Community-defined priorities

---

_Last updated: December 2025_
