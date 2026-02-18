# Principles

> **Purpose:** Distilled wisdom from all ADRs + implementation experience. Read in <2 minutes.
>
> **When to create:** Emerges after 5+ ADRs — populated by `..hygiene`, not during onboarding.
>
> **When to update:** After major milestones or when pattern emerges across 3+ ADRs.

---

## The Core Trade

The protocol asks you to trade a small percentage of your context window for a reliable memory. Protocol files (~5% of tokens) give AI persistent context across sessions. Without them, you spend 30%+ re-explaining what you already know. The trade is asymmetric — invest a little, compound over time.

---

## Mission

[Extract from PRFAQ.md — What is this project's core purpose?]

---

## Product Principles

**PP1: [Principle Name]**
[Brief description of how this guides product decisions]

**PP2: [Principle Name]**
[Brief description of how this guides product decisions]

**PP3: [Principle Name]**
[Brief description of how this guides product decisions]

<!-- Example from a fitness app:
**PP1: Pull Not Push** — Education available when curious, never forced
**PP2: Effort Signals, Not Measurements** — Track direction (heavier/more), not decimals
**PP3: Independence as Goal** — Success = user no longer needs the app

Example from a SaaS product:
**PP1: Adoption Is the Win State** — Not traffic. People using it.
**PP2: The Compound Effect** — Small investments compound over time.
**PP3: Show, Don't Tell** — Real products prove more than testimonials.
-->

---

## Technical Principles

**TP1: [Principle Name]**
[Brief description of technical approach]

**TP2: [Principle Name]**
[Brief description of technical approach]

**TP3: [Principle Name]**
[Brief description of technical approach]

<!-- Example:
**TP1: Files ARE Memory** — Docs persist, conversations don't
**TP2: Verifiable Done** — AC must be testable, not assumed
**TP3: Micro-commits** — Every logical unit gets its own commit
-->

---

## Design Principles

**DP1: [Principle Name]**
[Brief description of design approach]

**DP2: [Principle Name]**
[Brief description of design approach]

<!-- Example:
**DP1: Mobile-First** — Design for 375px viewport first
**DP2: CTA Above Fold** — Primary action visible without scrolling
-->

---

## Process Principles

**P1: [Principle Name]**
[Brief description of how team works]

<!-- Example:
**P1: Architect Designs, Builder Implements** — Roles stay separate
**P2: Practice What We Preach** — Adopt improvements we recommend
-->

---

## The "Next Session Test"

**For every section in a context file, ask:**
> "Would Claude need this to start fresh next session?"

- ✅ **Keep:** Active decisions, current architecture, technical reference
- ❌ **Archive:** Historical narrative, debugging stories, "how we learned X"

---

## Context Hygiene

Protocol files are the trade — they cost tokens but save more than they cost. Keep them lean so the trade stays in your favor.

**Check monthly:**
```bash
wc -w *.md
```

**Thresholds:**
- ✅ **Good:** Total <10,000 words, no single file >3,000 words
- ⚠️ **Warning:** Total 10,000-15,000 words, or any file >3,000 words
- 🚨 **Critical:** Total >15,000 words, or any file >5,000 words

**When critical:** Run `..hygiene` to archive old content.

---

## Related Files

| File | Purpose | Relationship to PRINCIPLES.md |
|------|---------|------------------------------|
| **PRFAQ.md** | Product vision | Source of Mission statement |
| **DECISIONS.md** | Active ADRs | Source of all principles |
| **CLAUDE.md** | Technical reference | Source of Technical Principles |

---

*This file is extracted from active ADRs after patterns emerge. It replaces the need to read all historical decisions.*

*Template from duo Protocol*
