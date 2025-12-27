# MTGTools Discord Bot Configuration Guide

*Detailed setup instructions for all recommended bots*

---

## 🤖 MEE6 Configuration

### Basic Setup
```yaml
# Leveling System
xp_rate:
  message_xp: 15-25 (random)
  cooldown: 60 seconds
  voice_xp: 10/minute
  
level_rewards:
  level_2:
    role: @verified
    message: "🎉 GG {user}! You've reached Level 2 and earned the Verified role!"
  level_5:
    role: @regular
    message: "⚡ {user} is on fire! Level 5 - Regular status unlocked!"
  level_10:
    role: @veteran
    message: "🏆 {user} has become a Veteran! Level 10 achieved!"
  level_20:
    role: @elite
    message: "👑 Bow to {user}! Elite status at Level 20!"

# Auto Moderator
automod:
  spam:
    duplicate_messages: 3
    action: timeout_10min
  caps:
    percentage: 70
    action: delete_and_warn
  mentions:
    max: 5
    action: delete_and_warn
  links:
    require_role: @verified
    whitelist: [github.com, mtgtools.com, youtube.com]
  
# Custom Commands
commands:
  !help: "Check out #faq and #resources for help! Ping @helper if you need assistance."
  !videre: "Videre Project: https://github.com/videre-project | Tracker: (link)"
  !manifesto: "Read our manifesto: #manifesto-manifeste"
  !events: "Check #announcements for upcoming events!"
  !contribute: "Want to contribute? Check #looking-for-contributors"
```

### MEE6 Welcome Message
```
Welcome {user} to MTGTools! 🎉

You're now part of the community where technical talent meets competitive excellence!

Quick Start:
1️⃣ Read our #rules-manifesto
2️⃣ Introduce yourself in #introductions  
3️⃣ Check today's #daily-challenge
4️⃣ Join the conversation in #lounge

Pro tip: Complete your first week for exclusive achievements! 🏆
```

---

## 🎭 Carl-bot Configuration

### Reaction Roles Setup
```yaml
# In #start-here channel
embed:
  title: "🎯 Choose Your Path"
  description: "React to select your roles and customize your experience!"
  color: 0x7289DA
  
reaction_roles:
  # Interests
  🔧: @developer
  🏆: @competitor  
  📊: @data-enthusiast
  🎨: @designer
  📝: @content-creator
  
  # Platforms
  🖥️: @mtgo-player
  ⚔️: @arena-player
  📋: @paper-player
  
  # Languages (Phase 2)
  🇫🇷: @french-speaker
  🇪🇸: @spanish-speaker
  🇯🇵: @japanese-speaker
  
  # Notifications
  📢: @announcement-pings
  🎮: @event-pings
  💻: @dev-updates
```

### Automod Rules
```yaml
automod:
  - trigger: 
      type: spam
      threshold: 5 messages in 5 seconds
    action:
      - delete
      - timeout: 10m
      - log: #mod-log
      
  - trigger:
      type: mass_mention
      threshold: 5
    action:
      - delete  
      - warn
      - log: #mod-log
      
  - trigger:
      type: banned_words
      words: [list_of_inappropriate_terms]
    action:
      - delete
      - warn
      - notify_mods: true
```

### Scheduled Messages
```yaml
scheduled_posts:
  meta_monday:
    channel: #meta-alerts
    time: "09:00 CET"
    day: Monday
    message: |
      🔔 **META MONDAY** 🔔
      
      Weekend tournament results are being analyzed!
      
      Expect full meta breakdown by 10 AM CET.
      Voice discussion tonight at 8 PM CET! 🎙️
      
      What surprised you this weekend? 👇

  daily_challenge:
    channel: #daily-challenge
    time: "10:00 CET"
    repeat: daily
    message: Use command /challenge to generate

  weekly_recap:
    channel: #announcements
    time: "18:00 CET"  
    day: Sunday
    message: Use template from engagement doc
```

---

## 🐙 Discord GitHub Bot

### Repository Connections
```yaml
repositories:
  - repo: videre-project/videre-project
    channels:
      commits: #videre-updates
      issues: #videre-general
      pulls: #videre-testing
      releases: #announcements
      
  - repo: mtgtools/archetype-ml
    channels:
      all: #ml-discussion
      
  - repo: mtgtools/*
    channels:
      releases: #announcements
```

### Webhook Configuration
```json
{
  "commit_format": "🔧 New commit in **{repo}** by {author}:\n`{message}`\n{url}",
  "pr_format": "🔀 PR #{number} in **{repo}**:\n**{title}**\nBy {author} | {status}\n{url}",
  "issue_format": "📋 Issue #{number} in **{repo}**:\n**{title}**\nBy {author}\n{url}",
  "release_format": "🚀 **NEW RELEASE**: {repo} {version}\n{description}\n{url}"
}
```

---

## 📊 Statbot Configuration

### Tracking Settings
```yaml
tracking:
  enabled_metrics:
    - member_count
    - messages_per_day
    - active_users_daily
    - voice_minutes
    - channel_activity
    - role_distribution
    - join_leave_rate
    
  reports:
    daily:
      time: "23:59"
      channel: #team-coordination
      
    weekly:
      day: Sunday
      time: "20:00"
      channel: #announcements
      public: true
      
  dashboards:
    public_url: true
    refresh_rate: 60 # minutes
```

---

## 🏆 Custom MTGTools Bot Features

### Core Functionality
```python
# Pseudo-code for custom bot features

class MTGToolsBot:
    def __init__(self):
        self.commands = {
            'challenge': self.daily_challenge,
            'meta': self.meta_snapshot,
            'winrate': self.winrate_calc,
            'archetype': self.archetype_lookup,
            'tournament': self.tournament_info
        }
    
    async def daily_challenge(self, ctx):
        """Generate daily challenge based on day"""
        challenges = {
            'Monday': self.meta_prediction_challenge,
            'Tuesday': self.tool_usage_challenge,
            'Wednesday': self.workshop_challenge,
            'Thursday': self.theory_challenge,
            'Friday': self.feature_vote_challenge,
            'Saturday': self.data_analysis_challenge,
            'Sunday': self.weekly_recap_challenge
        }
        
    async def meta_snapshot(self, ctx):
        """Fetch and display current meta breakdown"""
        # Integration with MTGO data sources
        # Beautiful embed with percentages
        # Trends and movements
        
    async def achievement_tracker(self, user_id, achievement):
        """Track and award achievements"""
        # Check completion criteria
        # Award XP
        # Announce in #achievements
        # Update user profile
```

### Tournament Integration
```yaml
tournament_feeds:
  sources:
    - mtgo_challenges
    - mtgo_preliminaries  
    - major_events
    
  notifications:
    results:
      channel: #tournament-results
      format: embed
      include_decklists: true
      
    live_updates:
      channel: #tournament-results
      top8_only: false
      
  analysis:
    auto_meta_calc: true
    archetype_detection: true
    performance_tracking: true
```

### Achievement System
```yaml
achievements:
  implementation:
    storage: PostgreSQL
    tracking: Real-time
    notifications: DM + Channel
    
  categories:
    - onboarding
    - engagement
    - competitive
    - development
    - community
    
  xp_values:
    common: 10-50
    uncommon: 50-100
    rare: 100-250
    mythic: 250-500
    legendary: 500-1000
```

---

## 🛠️ Bot Permissions Matrix

```yaml
bot_permissions:
  MEE6:
    - manage_roles
    - manage_messages
    - read_messages
    - send_messages
    - embed_links
    - attach_files
    - add_reactions
    - use_external_emojis
    - manage_webhooks
    
  Carl-bot:
    - administrator # Requires for full functionality
    
  GitHub:
    - read_messages
    - send_messages
    - embed_links
    - manage_webhooks
    
  Statbot:
    - read_messages
    - read_message_history
    - view_audit_log
    
  MTGTools_Bot:
    - manage_roles
    - manage_channels
    - read_messages
    - send_messages
    - embed_links
    - attach_files
    - add_reactions
    - manage_messages
    - mention_everyone # For important announcements only
```

---

## 🚀 Quick Setup Checklist

### Phase 1: Core Bots (Day 1)
- [ ] MEE6: Levels, automod, welcome
- [ ] Carl-bot: Reaction roles, automation
- [ ] Statbot: Analytics tracking

### Phase 2: Integration (Week 1)
- [ ] GitHub bot: Repository connections
- [ ] Custom bot: Basic features
- [ ] Webhook setup: External integrations

### Phase 3: Advanced (Week 2+)
- [ ] Tournament feeds
- [ ] Achievement system
- [ ] Advanced automation
- [ ] Custom commands expansion

---

*This configuration guide ensures all bots work together harmoniously to create an engaging, automated, and scalable Discord experience.*