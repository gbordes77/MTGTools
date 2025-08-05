# MTGTools Documentation System Architecture

*Version 1.0 - August 2025*
*Making MTGTools the gold standard for open-source documentation*

## 🎯 Documentation Vision

> "Every contributor should go from zero to productive in under 30 minutes, with 90% of their questions answered through self-service documentation."

## 📚 Documentation Hierarchy

```
docs/
├── getting-started/          # 0-to-hero in 30 minutes
│   ├── quickstart.md        # 5-minute first success
│   ├── installation/        # Platform-specific guides
│   ├── first-contribution/  # Your first PR guide
│   └── concepts.md          # Core concepts explained
│
├── user-guides/             # End-user documentation
│   ├── videre/             # Videre tracker guides
│   ├── tools/              # Other MTGTools
│   └── troubleshooting/    # Common issues & solutions
│
├── developer/              # Technical documentation
│   ├── architecture/       # System design & decisions
│   ├── api/               # API reference (auto-generated)
│   ├── sdk/               # MTGOSDK documentation
│   └── tutorials/         # Step-by-step guides
│
├── contributing/          # Contribution guidelines
│   ├── code-style/       # Language-specific standards
│   ├── documentation/    # How to write docs
│   ├── testing/          # Test requirements
│   └── review-process/   # PR workflow
│
├── reference/            # Reference materials
│   ├── glossary/        # MTG & technical terms
│   ├── architecture/    # ADRs & design docs
│   ├── api/            # OpenAPI specs
│   └── schemas/        # Data schemas
│
└── community/          # Community resources
    ├── roadmap/       # Project direction
    ├── events/        # Hackathons & meetups
    └── showcase/      # Built with MTGTools
```

## 🏗️ Documentation Stack

### 1. Documentation Site Generator
**Tool**: Docusaurus 3.0
- **Why**: React-based, great search, i18n support, versioning
- **Features**: 
  - Algolia search integration
  - MDX for interactive docs
  - Built-in API doc support
  - Dark mode (essential for devs)

### 2. API Documentation
**Tool**: OpenAPI 3.1 + Redoc/Swagger UI
- **Why**: Industry standard, interactive, auto-generated
- **Implementation**:
  ```yaml
  openapi: 3.1.0
  info:
    title: MTGTools API
    version: 1.0.0
    description: |
      Unified API for MTG competitive tools
      
      ## Authentication
      All endpoints require API key authentication...
  ```

### 3. Code Documentation
**Standards by Language**:
- **.NET/C#**: XML documentation comments → DocFX
- **TypeScript**: TSDoc → TypeDoc
- **Python**: Sphinx + Google style docstrings
- **SQL**: Inline comments + schema docs

### 4. Interactive Examples
**Tool**: CodeSandbox/StackBlitz embeds
- Live, editable code examples
- Framework-specific templates
- Direct GitHub integration

## 📋 Documentation Standards

### 1. Writing Style Guide

```markdown
# Component Name

## Overview
Brief description in 1-2 sentences.

## Quick Example
```language
// Minimal working example
```

## Installation
```bash
npm install @mtgtools/component
```

## API Reference
Detailed API documentation...

## Examples
### Basic Usage
### Advanced Patterns
### Common Pitfalls

## Related
- [Link to related docs]
```

### 2. Documentation Requirements

Every feature MUST include:
- [ ] User guide (how to use)
- [ ] API reference (what it does)
- [ ] Architecture doc (how it works)
- [ ] Examples (show me the code)
- [ ] Troubleshooting (when it breaks)

### 3. Language Standards

**Primary Language**: English for all technical content
**Translations**: French for user-facing guides
**Code**: English only (comments, variables, docs)

## 🤖 Documentation Automation

### 1. API Documentation Pipeline
```yaml
name: Generate API Docs
on:
  push:
    paths:
      - 'api/**'
      - 'openapi.yaml'

jobs:
  generate-docs:
    steps:
      - uses: actions/checkout@v3
      - name: Validate OpenAPI
        run: npx @apidevtools/swagger-cli validate
      - name: Generate docs
        run: npx @redocly/cli build-docs
      - name: Deploy to docs site
        run: npm run deploy:api-docs
```

### 2. Code Documentation Extraction
```yaml
# .NET Projects
- name: Generate XML docs
  run: dotnet build -p:GenerateDocumentationFile=true

# TypeScript Projects  
- name: Generate TypeDoc
  run: npx typedoc --out docs/api/typescript

# Python Projects
- name: Generate Sphinx docs
  run: sphinx-build -b html docs/source docs/build
```

### 3. Documentation Testing
```yaml
- name: Test documentation
  run: |
    # Check all links
    npm run docs:check-links
    
    # Validate code examples
    npm run docs:test-examples
    
    # Check for missing docs
    npm run docs:coverage
```

## 🎓 Contributor Onboarding Framework

### Phase 1: First 5 Minutes
1. **Landing Page**: Clear value prop + quick wins
2. **Interactive Tour**: Guided walkthrough
3. **Quick Success**: Run your first command

### Phase 2: First 30 Minutes
1. **Choose Your Path**:
   - Frontend Developer → React/TypeScript track
   - Backend Developer → .NET/API track
   - Data Scientist → Python/ML track
   
2. **Hands-on Tutorial**: Build something real
3. **Join Community**: Discord onboarding flow

### Phase 3: First Contribution
1. **Good First Issues**: Curated list with mentors
2. **Pair Programming**: Discord sessions
3. **Recognition**: Contributors hall of fame

## 📊 Documentation Metrics

### Success Metrics
- **Time to First Success**: < 5 minutes
- **Documentation Coverage**: > 90%
- **Search Success Rate**: > 80%
- **Contributor Retention**: > 60% after first PR

### Tracking Implementation
```javascript
// Analytics for documentation
gtag('event', 'doc_page_view', {
  page_path: window.location.pathname,
  time_on_page: timeSpent,
  search_terms: searchQuery,
  helpful_vote: wasHelpful
});
```

## 🌍 Internationalization Strategy

### Approach
1. **Core Docs**: English only (technical accuracy)
2. **User Guides**: French + English
3. **Community Content**: Multilingual encouraged

### Implementation
```jsx
// Docusaurus i18n config
module.exports = {
  i18n: {
    defaultLocale: 'en',
    locales: ['en', 'fr'],
    localeConfigs: {
      en: { label: 'English' },
      fr: { label: 'Français' }
    }
  }
};
```

## 🚀 30-Day Documentation Sprint Plan

### Week 1: Foundation
- [ ] Set up Docusaurus site
- [ ] Create documentation templates
- [ ] Write quickstart guide
- [ ] Document Videre API endpoints

### Week 2: Developer Docs
- [ ] Architecture overview
- [ ] MTGOSDK documentation
- [ ] API reference generation
- [ ] First tutorial series

### Week 3: User Documentation
- [ ] Videre user guide
- [ ] Troubleshooting guides
- [ ] Video tutorials
- [ ] FAQ compilation

### Week 4: Polish & Launch
- [ ] Search implementation
- [ ] Documentation testing
- [ ] Community feedback
- [ ] Official launch

## 📝 Documentation Templates

See `/docs/templates/` for:
- API endpoint template
- Tutorial template
- Architecture Decision Record (ADR)
- Troubleshooting guide template
- Release notes template

## 🤝 Maintenance Strategy

### Documentation Review Cycle
- **Weekly**: New feature docs
- **Monthly**: Accuracy review
- **Quarterly**: Full audit
- **Annually**: Major restructure

### Documentation Champions
- Each major component has a doc champion
- Responsible for accuracy and completeness
- Monthly sync meetings

## 🎯 Next Steps

1. **Immediate** (This Week):
   - Create `/docs` directory structure
   - Set up Docusaurus locally
   - Write first quickstart guide
   
2. **Short-term** (Month 1):
   - Complete API documentation
   - Launch documentation site
   - Create video tutorials
   
3. **Long-term** (Quarter 1):
   - Full test coverage for docs
   - Advanced tutorials series
   - Documentation automation complete

---

*"Great documentation is not written, it's cultivated through continuous improvement and community feedback."*