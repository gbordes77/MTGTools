# MTGTools Discord Template - Complete Configuration

*Optimized synthesis from 4 specialized agents' recommendations*

---

## 🏗️ Channel Structure

### 📍 WELCOME & INFO
- 📢 **announcements** (read-only)
- 📜 **rules-and-charter** 
- 🚀 **start-here** (interactive onboarding)
- 👋 **introductions**
- 🏆 **success-stories** (community wins)
- ❓ **faq-support**

### 💬 COMMUNITY
- 🌐 **general-chat** (bilingual welcome)
- 🎯 **daily-challenge** 
- 📊 **share-your-stats** 
- 💡 **feature-suggestions** (voting enabled)
- 🎨 **deck-brewing**
- 🎮 **off-topic**

### 🏆 COMPETITIVE INTELLIGENCE
- 📈 **meta-alerts** (automated alerts)
- 🔬 **archetype-lab** 
- 📝 **tournament-prep** 
- 🎯 **sideboard-academy**
- 📊 **data-insights**

### 👨‍💻 DEVELOPMENT
- 💻 **dev-general**
- 🐛 **bug-reports** (with templates)
- 🚀 **feature-requests** (voting)
- 📖 **api-discussion**
- 🤝 **contributors-wanted**
- 📚 **documentation**

### 🛠️ PROJECTS
```
├── VIDERE PROJECT
│   ├── videre-news
│   ├── videre-support
│   └── videre-data
├── ARCHETYPE ML
│   ├── ml-discussion
│   └── training-help
└── FUTURE PROJECTS
    └── project-proposals
```

### 🔊 VOICE CHANNELS
- 🎙️ Community Hangout
- 📞 Dev Office Hours
- 🏆 Tournament Room
- 🎮 Practice Rooms 1-3

---

## 🎭 Role System

### Main Hierarchy
1. **@everyone** - Basic access
2. **@verified** ✅ - After 3 days + intro
3. **@contributor** 🛠️ - 1+ PR merged
4. **@grinder** 🏆 - Active competitive player
5. **@helper** 💡 - Community support
6. **@project-lead** 📂 - Project leader
7. **@moderator** 🛡️ - Moderation
8. **@founder** ⭐ - Early adopters

### Self-Assignable Roles
- **Platform**: 🟦 @mtgo | 🟧 @arena | 📄 @paper
- **Expertise**: 💻 @developer | 📊 @data-scientist | 🎨 @designer
- **Language**: 🇫🇷 @french-speaker | 🇬🇧 @english | 🌍 @polyglot

---

## 🤖 Essential Bots

### 1. **MEE6** - Engagement & Levels
```yaml
config:
  - XP system enabled
  - Level-up announcements in #success-stories
  - Commands: !rank, !leaderboard
  - Auto-moderation for spam/links
```

### 2. **Carl-bot** - Automation
```yaml
config:
  - Reaction roles in #start-here
  - Scheduled messages (daily challenges)
  - Auto-threads for bug reports
  - Moderation logs
```

### 3. **GitHub Bot** - Dev Integration
```yaml
repos:
  - videre-project/MTGOSDK
  - videre-project/Tracker
  - mtgtools/community
channels:
  - commits → #videre-news
  - issues/PR → #dev-general
```

### 4. **Custom MTGTools Bot** (to develop)
```yaml
features:
  - Tracking achievements
  - Meta alerts depuis API
  - Tournois communautaires
  - Stats winrate intégrées
```

---

## 🎮 Gamification System

### Main Achievements
- 🌟 **First Steps** (10 XP) - Complete onboarding
- 💬 **Active Member** (50 XP) - 50 messages
- 🏆 **Tournament Grinder** (100 XP) - Share 5 reports
- 👨‍💻 **Code Contributor** (500 XP) - First PR
- 📊 **Data Wizard** (200 XP) - Share insight
- 🌍 **Ambassador** (300 XP) - Invite 5 members

### Levels & Rewards
```
Level 1-3: Active member → Custom color
Level 4-6: Contributor → Beta access
Level 7-9: Expert → Private channels
Level 10: Elite → Merch + VIP events
```

---

## 📅 Engagement Calendar

### Weekly Schedule
- **Meta Monday** 📊 - Weekly metagame analysis
- **Tool Tuesday** 🛠️ - Feature focus/tutorial
- **Workshop Wednesday** 💻 - Dev/data session
- **Theory Thursday** 🎯 - Competitive strategy
- **Feature Friday** 🚀 - Community vote
- **Stats Saturday** 📈 - Data deep dive
- **Summary Sunday** 🏆 - Recap + celebrations

### Monthly Events
- 🏆 **Community Tournament** (1st Saturday)
- 💻 **Hackathon Weekend** (3rd weekend)
- 🎙️ **AMA with Pro/Dev** (last Thursday)
- 📊 **Data Challenge** (mid-month)

---

## 🚀 Launch Plan

### Phase 0: Pre-launch (D-7)
- [ ] Configure all channels and permissions
- [ ] Install and setup 4 bots
- [ ] Pre-seed 100+ messages in each channel
- [ ] Recruit 10 core team members
- [ ] Prepare first week content

### Phase 1: Soft Launch (D1-D7)
- [ ] Invite 50 targeted early adopters
- [ ] Launch onboarding program
- [ ] First daily challenge
- [ ] Office hours with Guillaume
- [ ] Adjust based on feedback

### Phase 2: Videre Migration (D8-D21)
- [ ] Email to 100+ Videre users
- [ ] @founder role for early joiners
- [ ] Launch weekly events
- [ ] Reach 150 active members
- [ ] First external contribution

### Phase 3: Public Launch (D22-D60)
- [ ] Reddit, Twitter, forums announcements
- [ ] Streamer/creator partnerships
- [ ] 300+ members target
- [ ] 3+ active projects
- [ ] Governance model established

---

## 📊 Success KPIs

### Daily Metrics
- Messages/day: 100+ (D30), 500+ (D90)
- Active members: 30% of total
- Support response time: <2h
- New members: 5+/day (phase 3)

### Key Objectives
- **30 days**: 100 members, 3 contributors
- **90 days**: 300 members, 5 projects
- **180 days**: 500+ members, self-sustaining ecosystem

---

## 💡 Final Recommendations

1. **Start small but active** - Better 50 engaged members than 500 ghosts
2. **Critical pre-seeding** - At least 1000 messages before public opening
3. **Smart bilingual** - One unified channel at start, split if needed
4. **Progressive gamification** - Add features based on growth
5. **Data-driven** - Track everything, adjust weekly

---

*This template synthesizes best practices to transform the MTGTools Discord into THE community reference for competitive Magic tools.*