# Principles

> **Purpose:** Distilled wisdom from all ADRs + implementation experience. Read in <2 minutes.
>
> **When to create:** After project onboarding, extract core principles from initial decisions.
>
> **When to update:** After major milestones (v0.5, v1.0) or when pattern emerges across 3+ ADRs.

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

<!-- Example from gym app:
**PP1: Pull Not Push** — Education available when curious, never forced
**PP2: Effort Signals, Not Measurements** — Track direction (heavier/more), not decimals
**PP3: Independence as Goal** — Success = user no longer needs the app
-->

---

## Technical Principles

**TP1: [Principle Name]**
[Brief description of technical approach]

**TP2: [Principle Name]**
[Brief description of technical approach]

**TP3: [Principle Name]**
[Brief description of technical approach]

<!-- Example from gym app:
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

<!-- Example from gym app:
**DP1: Mobile-First** — Design for 375px viewport first
**DP2: CTA Above Fold** — Primary action visible without scrolling
-->

---

## Process Principles

**P1: [Principle Name]**
[Brief description of how team works]

<!-- Example from gym app:
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

## Token Budget Awareness

**Target:**
- **Architect Mode:** ~7,500 tokens (15% of session budget)
  - Loads: PRFAQ, PRINCIPLES, DECISIONS, CONSTRAINTS, TODO, PROGRESS
- **Builder Mode:** ~2,500 tokens (5% of session budget)
  - Loads: PRINCIPLES, CLAUDE, TODO

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
| **CONSTRAINTS.md** | Design system, rejected approaches | Source of Design Principles |
| **DECISIONS.md** | Active ADRs | Source of all principles |
| **CLAUDE.md** | Technical reference | Source of Technical Principles |

---

*This file is extracted from active ADRs after patterns emerge. It replaces the need to read all historical decisions.*

*Template from duo Protocol v1*
