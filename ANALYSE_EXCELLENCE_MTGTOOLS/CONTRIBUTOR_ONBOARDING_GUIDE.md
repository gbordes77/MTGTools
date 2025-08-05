# MTGTools Contributor Onboarding Guide

*Welcome to the MTGTools community! 🚀*
*From zero to your first contribution in 30 minutes*

## 🎯 Quick Start (5 minutes)

### 1. Choose Your Path

<div align="center">

| 🎨 **Frontend Dev** | 🔧 **Backend Dev** | 📊 **Data Science** | 📝 **Documentation** |
|:---:|:---:|:---:|:---:|
| React, TypeScript | .NET, APIs | Python, ML | Guides, Tutorials |
| [Jump to Frontend](#frontend-developer-track) | [Jump to Backend](#backend-developer-track) | [Jump to Data](#data-science-track) | [Jump to Docs](#documentation-track) |

</div>

### 2. Your First Success

```bash
# Clone and setup (works on all platforms)
git clone https://github.com/mtgtools/getting-started
cd getting-started
npm install
npm run dev

# 🎉 You're now running MTGTools locally!
# Visit http://localhost:3000 to see it in action
```

### 3. Join the Community

<div align="center">

[![Discord](https://img.shields.io/badge/Discord-MTGTools-7289da?style=for-the-badge&logo=discord)](https://discord.gg/mtgtools)
[![GitHub](https://img.shields.io/badge/GitHub-MTGTools-181717?style=for-the-badge&logo=github)](https://github.com/mtgtools)

</div>

## 🚀 Getting Started Tracks

### Frontend Developer Track

**Your Mission**: Build user interfaces that help players dominate the metagame.

#### Prerequisites
- Node.js 18+ and npm/yarn
- Basic React knowledge
- TypeScript helpful but not required

#### 30-Minute Tutorial
1. **Setup Development Environment**
   ```bash
   git clone https://github.com/mtgtools/videre-ui
   cd videre-ui
   npm install
   npm run dev
   ```

2. **Make Your First Change**
   - Open `src/components/Welcome.tsx`
   - Change the welcome message
   - See it live update!

3. **Understand the Stack**
   - **React 18** - UI framework
   - **TypeScript** - Type safety
   - **Tailwind CSS** - Styling
   - **Vite** - Build tool
   - **React Query** - Data fetching

4. **Your First Contribution**
   ```bash
   # Find a good first issue
   npm run find-issue
   
   # This will show you pre-selected issues perfect for beginners
   ```

#### Learning Resources
- [MTGTools Frontend Architecture](./developer/frontend-architecture.md)
- [Component Style Guide](./contributing/frontend-style-guide.md)
- [Testing React Components](./developer/testing-react.md)

#### Next Steps
- [ ] Complete the [Metagame Visualizer Tutorial](./tutorials/metagame-viz.md)
- [ ] Join #frontend-dev on Discord
- [ ] Pick a ["good first issue"](https://github.com/mtgtools/videre-ui/labels/good%20first%20issue)

---

### Backend Developer Track

**Your Mission**: Build robust APIs that power the competitive Magic ecosystem.

#### Prerequisites
- .NET 8+ SDK
- Basic C# knowledge
- REST API understanding

#### 30-Minute Tutorial
1. **Setup Development Environment**
   ```bash
   git clone https://github.com/mtgtools/mtgtools-api
   cd mtgtools-api
   dotnet restore
   dotnet run --project src/MTGTools.Api
   ```

2. **Explore the API**
   - Visit http://localhost:5000/swagger
   - Try the `/metagame/current` endpoint
   - See real MTG data flowing!

3. **Add Your First Endpoint**
   ```csharp
   // src/Controllers/StatsController.cs
   [HttpGet("winrate/{deckId}")]
   public async Task<IActionResult> GetDeckWinrate(string deckId)
   {
       // You'll implement this!
       return Ok(new { deckId, winrate = 0.521 });
   }
   ```

4. **Run the Tests**
   ```bash
   dotnet test
   # All green? You're ready to contribute!
   ```

#### Learning Resources
- [MTGTools API Architecture](./developer/api-architecture.md)
- [MTGOSDK Documentation](./developer/mtgosdk-guide.md)
- [Database Schema Guide](./developer/database-schema.md)

#### Next Steps
- [ ] Complete the [API Extension Tutorial](./tutorials/extend-api.md)
- [ ] Join #backend-dev on Discord
- [ ] Implement a missing API endpoint

---

### Data Science Track

**Your Mission**: Turn Magic data into competitive insights using ML and analytics.

#### Prerequisites
- Python 3.9+
- Basic pandas/numpy knowledge
- Jupyter notebooks

#### 30-Minute Tutorial
1. **Setup Data Environment**
   ```bash
   git clone https://github.com/mtgtools/data-science
   cd data-science
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   pip install -r requirements.txt
   jupyter lab
   ```

2. **Explore MTG Data**
   - Open `notebooks/01-explore-metagame.ipynb`
   - Run all cells
   - See real tournament data!

3. **Build Your First Model**
   ```python
   # Predict deck archetype from card list
   from mtgtools.ml import ArchetypeClassifier
   
   model = ArchetypeClassifier()
   model.train(training_data)
   
   # 85% accuracy on first try!
   ```

4. **Contribute an Analysis**
   - Pick a hypothesis (e.g., "Aggro beats Control post-board")
   - Write analysis notebook
   - Share insights!

#### Learning Resources
- [MTG Data Schema](./data/mtg-data-schema.md)
- [ML Pipeline Guide](./data/ml-pipeline.md)
- [Statistical Analysis Best Practices](./data/stats-guide.md)

#### Next Steps
- [ ] Complete the [Sideboard Analysis Tutorial](./tutorials/sideboard-ml.md)
- [ ] Join #data-science on Discord
- [ ] Improve archetype classification accuracy

---

### Documentation Track

**Your Mission**: Help others succeed by creating clear, helpful documentation.

#### Prerequisites
- Markdown knowledge
- Clear writing skills
- Empathy for learners

#### 30-Minute Tutorial
1. **Setup Docs Environment**
   ```bash
   git clone https://github.com/mtgtools/documentation
   cd documentation
   npm install
   npm run docs:dev
   ```

2. **Fix Your First Typo**
   - Find any typo in the docs
   - Click "Edit this page"
   - Submit PR directly from GitHub!

3. **Write Your First Guide**
   - Pick something you learned
   - Write a short guide
   - Help the next person!

4. **Add an Example**
   ```markdown
   ## Example: Fetching Metagame Data
   
   Here's how to get current Modern metagame data:
   
   \```javascript
   const response = await fetch('https://api.mtgtools.com/v1/metagame/current?format=modern');
   const data = await response.json();
   console.log(`Top deck: ${data.archetypes[0].name}`);
   \```
   ```

#### Learning Resources
- [Documentation Style Guide](./contributing/docs-style-guide.md)
- [Technical Writing Best Practices](./contributing/technical-writing.md)
- [Screenshot Guidelines](./contributing/screenshots.md)

#### Next Steps
- [ ] Improve any confusing section
- [ ] Add a missing code example
- [ ] Translate a guide to French

## 🎓 Understanding MTGTools

### Architecture Overview

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│                 │     │                 │     │                 │
│  Frontend Apps  │────▶│   API Gateway   │────▶│  Data Services  │
│  (React, TS)    │     │  (Cloudflare)   │     │  (.NET, Python) │
│                 │     │                 │     │                 │
└─────────────────┘     └─────────────────┘     └─────────────────┘
         │                                               │
         │                                               │
         ▼                                               ▼
┌─────────────────┐                           ┌─────────────────┐
│                 │                           │                 │
│   MTG Clients   │                           │   Databases     │
│  (MTGO, Arena)  │                           │  (PostgreSQL)   │
│                 │                           │                 │
└─────────────────┘                           └─────────────────┘
```

### Key Concepts

1. **Archetype Classification**: How we identify deck types
2. **Metagame Analysis**: Understanding format composition
3. **Performance Metrics**: Win rates, conversion rates
4. **Data Pipeline**: Collection → Processing → API → UI

### Technology Choices

| Layer | Technology | Why |
|-------|------------|-----|
| Frontend | React + TypeScript | Type safety, component ecosystem |
| API | .NET 8 + Minimal APIs | Performance, MTGO compatibility |
| Data | Python + PostgreSQL | ML libraries, time-series data |
| Infrastructure | Cloudflare | Edge performance, DDoS protection |

## 🤝 Making Your First Contribution

### 1. Find an Issue

```bash
# Use our issue finder
npm run find-issue

# Or browse manually
# https://github.com/mtgtools/*/labels/good%20first%20issue
```

### 2. Claim It

Comment on the issue:
> I'd like to work on this! This would be my first contribution to MTGTools.

A maintainer will:
- Assign it to you
- Provide guidance
- Pair program if needed

### 3. Development Workflow

```bash
# 1. Fork and clone
git clone https://github.com/YOUR_USERNAME/PROJECT_NAME
cd PROJECT_NAME

# 2. Create feature branch
git checkout -b feature/your-feature-name

# 3. Make changes
# ... code ...

# 4. Test thoroughly
npm test  # or dotnet test, or pytest

# 5. Commit with conventional commits
git commit -m "feat: add deck winrate endpoint"

# 6. Push and create PR
git push origin feature/your-feature-name
```

### 4. Pull Request Template

```markdown
## Description
Brief description of what this PR does

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Documentation update
- [ ] Performance improvement

## Testing
- [ ] Unit tests pass
- [ ] Manual testing completed
- [ ] Documentation updated

## Screenshots (if applicable)
[Add screenshots here]

## Related Issues
Fixes #123
```

## 🌟 Recognition & Growth

### Contributor Levels

1. **🥉 Bronze Contributor** (1-3 PRs)
   - Discord role
   - Mentioned in release notes

2. **🥈 Silver Contributor** (4-10 PRs)
   - Feature in contributor spotlight
   - Early access to new features

3. **🥇 Gold Contributor** (11+ PRs)
   - Core team consideration
   - Conference ticket sponsorship

4. **💎 Core Team**
   - Repository write access
   - Architecture decisions
   - Mentoring others

### Ways to Contribute Beyond Code

- **🐛 Bug Reports**: Detailed reports help us improve
- **💡 Feature Ideas**: Share your vision
- **🌍 Translations**: Help us reach more players
- **📹 Video Tutorials**: Create content
- **👥 Community Support**: Help others in Discord
- **🎨 Design**: UI/UX improvements

## 📚 Resources

### Essential Reading
- [MTGTools Manifesto](../MTGTOOLS_MANIFESTO_EN.md)
- [Code of Conduct](../CODE_OF_CONDUCT.md)
- [Architecture Overview](./developer/architecture.md)

### Quick References
- [API Documentation](https://api.mtgtools.com/docs)
- [Component Storybook](https://storybook.mtgtools.com)
- [Data Schemas](./reference/schemas)

### Getting Help
- **Discord**: #contributor-help (fastest)
- **GitHub Discussions**: For design decisions
- **Email**: contributors@mtgtools.com

## 🎯 What's Next?

You've completed onboarding! Here are your next adventures:

### Week 1 Goals
- [ ] Make your first PR (even a typo fix!)
- [ ] Join Discord and introduce yourself
- [ ] Star the repos you're interested in

### Month 1 Goals
- [ ] Complete one tutorial series
- [ ] Contribute to 2-3 different repositories
- [ ] Help another new contributor

### Month 3 Goals
- [ ] Become a Bronze contributor
- [ ] Lead a small feature
- [ ] Write a blog post about your experience

## 🙏 Welcome to MTGTools!

We're thrilled to have you join our mission to democratize competitive Magic data. Every contribution, no matter how small, makes a difference.

Remember:
- **Ask questions** - We all started somewhere
- **Share ideas** - Your perspective is valuable
- **Have fun** - We're building cool stuff for a game we love

See you in the Discord! 

---

<div align="center">

**Ready to contribute?**

[![Start Contributing](https://img.shields.io/badge/Start%20Contributing-00C851?style=for-the-badge)](https://github.com/mtgtools)

*"From zero to hero in 30 minutes or less!"*

</div>