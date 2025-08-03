# Revised Priorities After Cory's Input

**Date**: August 1, 2025  
**Updated based on**: Technical insights from Cory

---

## 🎯 NEW TOP PRIORITIES

### 1. ✅ MTGOSDK CI/CD - ALREADY DONE!
Great news - this was our #5 priority but it's already complete!

### 2. API Documentation (NEW HIGH PRIORITY)
- **What**: Create usage docs for the API
- **Why**: API is stable but only has inline docstrings
- **Action**: Add examples, usage guides, endpoint documentation
- **Owner**: Cory/Tech Lead
- **Time**: 4-6 hours

### 3. MTGOSDK Examples Documentation
- **What**: Extract examples from MTGOBot/Tracker
- **Why**: Currently must read complex codebases to understand usage
- **Action**: Create standalone example files
- **Owner**: Tech Lead
- **Time**: 3-4 hours

### 4. PostgreSQL Migration Testing
- **What**: Test self-hosted postgres setup
- **Why**: Needed for Tracker volume + better plugins
- **Status**: Hardware ready, needs testing
- **Owner**: Cory
- **Time**: 1-2 days

---

## 📊 UPDATED PROJECT UNDERSTANDING

### Architecture Flow
```
MTGOBot (data collection) 
    ↓
PostgreSQL on Neon (current)
    ↓
API (Cloudflare Workers)
    ↓
Users/Services
```

### Key Technical Challenge
- **Problem**: MTGGoldfish archetype labels are poor quality
- **Impact**: Affects Tracker and API accuracy
- **Solution**: mlm repository (machine learning approach)

---

## 🔄 ORIGINAL PRIORITIES STILL VALID

1. **Fix website reference** - Still critical
2. **Document Tracker** - Still needed
3. **Security scanning** - Still important
4. **Discord expansion** - Still valuable
5. **Documentation sprint** - Even more important now

---

## 💡 NEW INSIGHTS

### What's Working Well
- MTGOSDK is mature with CI/CD ✅
- API is stable (just needs docs)
- MTGOBot is stable and feeding data

### What Needs Attention
- API usage documentation
- Example code extraction
- Database migration path
- Archetype quality improvement (mlm)

### Infrastructure Note
- Current: Neon (cloud PostgreSQL)
- Future: Self-hosted PostgreSQL
- Reason: Volume + plugins for Tracker

---

## 📋 REVISED ACTION PLAN

### Week 1 (Immediate)
1. Remove website reference ⏱️ 30min
2. Create Tracker README ⏱️ 2-3hr
3. Enable security scanning ⏱️ 1hr
4. **NEW**: API usage docs ⏱️ 4-6hr

### Week 2-3
1. Extract MTGOSDK examples ⏱️ 3-4hr
2. Test postgres migration ⏱️ 1-2 days
3. Discord expansion ⏱️ 4hr
4. Documentation sprint ⏱️ 1 day

### Month 2
1. Complete mlm pipeline documentation
2. Migrate to self-hosted postgres
3. Improve archetype clustering

---

## ❓ Questions for Cory

1. What's the expected volume increase from Tracker?
2. What are the specific MTGGoldfish quality issues?
3. Can we get the GitHub gist link for mlm pipeline?
4. Timeline preference for postgres migration?

---

*This update shows the project is more mature than initially assessed, with different documentation needs than expected.*