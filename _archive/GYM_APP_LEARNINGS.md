# Gym App Protocol Learnings

**Project:** Gym Workout Tracker (gym-chi-flame.vercel.app)
**Timeline:** November 2025 - January 2026
**Protocol Version:** duo/ab v1.2
**Team:** Marek + Claude
**Outcome:** Successfully shipped v1.0 in 2 months with 14 ADRs, 20+ sessions, zero tech debt

---

## Executive Summary

The duo/ab protocol worked exceptionally well for shipping fast. But we hit a **token ceiling at v1.0** that the protocol documentation didn't prepare us for.

**The Problem:**
After shipping 14 features, context files ballooned to **13,500 tokens (~27% of session budget)** before any work started. We were burning Builder budget on historical narrative Claude didn't need.

**The Solution:**
We completed "v1.0 Documentation Consolidation" — a systematic cleanup that:
- Extracted principles from 14 ADRs into PRINCIPLES.md (~500 words)
- Archived historical decisions (kept 2 active, moved 12 to archive)
- Slimmed CLAUDE.md by 40% (614→446 lines)
- Archived progress sessions (kept last 3, moved rest to archive)

**Result:**
Token load dropped from 27% → **15% (Architect) and 5% (Builder)**, matching kayg.ee's stated targets.

---

## What Worked Brilliantly ⭐⭐⭐⭐⭐

### 1. PRFAQ.md as North Star

**Impact:** Every feature decision traced back to mission: "Turn confused beginners into people who know exactly what they're doing."

**Example:** When considering "Coach Dashboard" feature, PRFAQ revealed it violated "Glass Box" philosophy (all roles see same data). Rejected before writing code.

**Lesson:** PRFAQ isn't a one-time doc. It's the tiebreaker for every "should we build this?" question.

### 2. DECISIONS.md as Living Memory

**Impact:** ADRs prevented context loss across 20+ sessions. Each decision documented "why" not just "what."

**Example:** ADR-006 (Weight Adjustment Tracking) went through 2 iterations. When ADR-008 (Session Management) was added, we read ADR-006 and knew to integrate them. No re-explanation needed.

**Lesson:** ADRs ARE the AI's memory between sessions. Without them, you re-explain architecture every conversation.

### 3. TODO.md with Acceptance Criteria

**Impact:** "Done" was verifiable, not ambiguous. Builder marked tasks complete only when AC passed.

**Example:**
```
Task: Implement promotion modal
- AC: 4 consecutive 'over' triggers modal
- AC: Accept writes to exercise_promotions
- AC: Defer dismisses for session
```

Builder verified all 3 before marking done.

**Lesson:** AC prevents "90% done" syndrome where last 10% takes another session.

### 4. CONSTRAINTS.md for Rejected Approaches

**Impact:** Prevented re-proposing dead-end ideas. Captured "why we don't do X" as clearly as "why we do Y."

**Example:** Rejected "Date-based weight tracking" (Dec 10) because same-day sessions would overwrite. When similar pattern came up later, CONSTRAINTS.md blocked it instantly.

**Lesson:** Negative decisions are as valuable as positive ones. Document both.

---

## Where Protocol Hit Limits 🚨

### 1. No Guidance on "v1.0 Cleanup"

**The Problem:**
After shipping 14 features, context files became historical narratives instead of reference docs. CLAUDE.md included:
- "How variant cycling evolved" (history, not reference)
- "Dec 9 debugging session" (archive material)
- "Future direction notes" (belongs in TODO.md)

**The Kayg.ee Insight We Missed:**
> "AI forgets everything between conversations. But files don't forget. Your markdown files ARE the AI's memory."

**What This Actually Means:**
Files should contain **what AI needs for NEXT session**, not **how we learned it**.

**Missing From Protocol:**
When to archive, what to archive, how to extract principles from historical ADRs.

### 2. Token Budget Blind Spot

**The Problem:**
We didn't measure token load until we hit friction. Kayg.ee documentation says "Architect loads ~15%, Builder loads ~5%" but doesn't explain HOW to measure or maintain this.

**What Would Have Helped:**
- Simple token counter in protocol (`wc -w *.md` as proxy)
- Threshold warnings ("CLAUDE.md >2500 words? Time to slim.")
- Example of "before/after" cleanup

### 3. PROGRESS.md as Append-Only Log

**The Problem:**
PROGRESS.md grew to 1,445 words across 17 sessions. Every session added narrative. Nothing ever got removed.

**The Pattern We Discovered:**
- Keep "Current State" (what's working NOW)
- Keep "Last 3 Sessions" (recent context)
- Archive everything else (full details available but not loaded)

---

## The "Next Session Test" 🧪

We developed this heuristic during cleanup:

**For every section in a context file, ask:**
> "Would Claude need this to start fresh next session?"

Examples:
- ✅ Tech stack → Yes (setup decisions)
- ✅ Auth system → Yes (complex, frequently touched)
- ✅ Active ADRs → Yes (inform new decisions)
- ❌ "How we discovered ADR-006" → No (archive)
- ❌ "Dec 9 debugging session" → No (archive)
- ❌ "Evolution of variant cycling" → No (archive)

---

## When Cleanup Becomes Mandatory ⚠️

### Immediate Blockers (do cleanup NOW):
1. Token budget >20% of session budget before work starts
2. Any .md file >3000 words (except PRFAQ)
3. Claude asks "which version?" about a decision
4. Architect spends >2 messages "catching up"

### Warning Signs (plan cleanup soon):
1. More than 10 implemented ADRs in DECISIONS.md
2. More than 10 sessions in PROGRESS.md
3. Same concept explained in 3+ files
4. CLAUDE.md reads like a story, not reference

### Healthy Maintenance (proactive):
1. Monthly hygiene check (first Monday)
2. After major milestones (v0.5, v1.0)
3. When >5 ADRs have same pattern (extract to PRINCIPLES.md)

---

## Implemented Solutions 🛠️

### 1. New File: PRINCIPLES.md

**Purpose:** Distilled wisdom from all ADRs + implementation experience. Read in <2 minutes.

**Contents:**
- Mission (from PRFAQ)
- 4-5 Product Principles
- 5-6 Technical Principles
- 3-4 Design Principles

**When to Update:** After major milestones or when pattern emerges across 3+ ADRs.

**Token Impact:** ~500 words. Replaces need to read all historical ADRs.

### 2. Enhanced `..hygiene` Command

Added to ROLE_PROTOCOL.md:

**Step 1: Token Budget Check**
```bash
wc -w *.md
```

Health levels:
- ✅ Good: Total <10,000 words, no file >3,000 words
- ⚠️ Warning: Total 10,000-15,000 words
- 🚨 Critical: Total >15,000 words

**Step 3: Apply "Next Session Test"**
Review each section: "Would Claude need this next session?"

**Step 5: Extract Principles**
If >5 ADRs and no PRINCIPLES.md, create it from patterns.

### 3. Token Budget Management (WORKFLOW.md)

New section documenting:
- Why it matters (the v1.0 wall)
- Target budgets (15% Architect, 5% Builder)
- Monthly monitoring (`wc -w *.md`)
- "Next Session Test" explanation
- When cleanup becomes mandatory
- Post-v1.0 hygiene checklist

### 4. Updated Onboarding Flow (CLAUDE.md)

Added PRINCIPLES.md to Step 3 (Populate Docs):
> "Extract initial principles from discovery answers (mission, 2-3 product principles)"

---

## Success Metrics 📊

### Before Cleanup (Jan 15, 2026)
- Total context: ~13,500 tokens (27% session budget)
- CLAUDE.md: 614 lines, 2,966 words
- DECISIONS.md: 14 ADRs (all active)
- PROGRESS.md: 17 sessions, 1,445 words
- Builder loaded same context as Architect

### After Cleanup (Jan 15, 2026)
- Total context: ~7,500 tokens (15% session budget, Architect)
- CLAUDE.md: 446 lines, ~1,800 words (40% reduction)
- DECISIONS.md: 2 active ADRs (12 archived)
- PRINCIPLES.md: NEW, ~500 words
- PROGRESS.md: 66 lines, ~300 words (80% reduction)
- Builder context: ~2,500 tokens (5% budget)

**Outcome:** Matched kayg.ee targets exactly.

---

## What We'd Tell Our Past Selves 💡

### Week 1: "PRFAQ first. Everything else flows from mission."
You'll be tempted to jump to code. Don't. Spend Day 1 on PRFAQ. Every future decision gets easier.

### Week 4: "ADRs are your best investment."
It feels like overhead. It's not. When you return to a decision 2 weeks later, you'll thank yourself.

### Week 8: "Run token budget check before every session."
Don't wait for slowdown. Measure: `wc -w *.md`. If total >10,000 words, hygiene time.

### v1.0: "Cleanup is part of shipping."
v1.0 isn't just features working. It's documentation consolidated. Budget 1 session for hygiene.

### Always: "Apply 'Next Session Test' ruthlessly."
Before committing any doc update: "Would Claude need this next session?" If no → archive.

---

## The Core Insight 💎

The duo/ab protocol is **production-grade for shipping v1.0**. We went from idea to deployed app in 2 months with zero technical debt.

But there's a hidden "v1.0 wall" where documentation becomes burden instead of tool. The kayg.ee insight — "files ARE the AI's memory" — needs a corollary:

**"Memories should be indexed, not narrated."**

Add post-v1.0 hygiene to the protocol, and teams won't hit this wall. They'll graduate smoothly from rapid prototyping to sustainable iteration.

---

## Key Learnings Applied to Protocol Template

1. ✅ Created PRINCIPLES.md template
2. ✅ Enhanced `..hygiene` command with token budget monitoring
3. ✅ Added Token Budget Management section to WORKFLOW.md
4. ✅ Updated CLAUDE.md onboarding to include PRINCIPLES.md
5. ✅ Documented ADR-003 in DECISIONS.md
6. ✅ All changes committed to protocol-duo template

---

**Date:** January 15, 2026
**Protocol Version Enhanced:** duo v1.4
**Status:** Implemented in protocol-duo template
**Contact:** Marek (via protocol-duo repository)
