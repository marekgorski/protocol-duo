# DECISIONS.md - Architecture Decision Records

This file tracks architectural decisions for duo Protocol.

---

## Compressed ADRs

When `..hygiene` runs, stable ADRs are compressed to a table format with full text archived:

| ADR | Title | Status | Summary |
|-----|-------|--------|---------|
| ADR-001 | [Title] | Accepted | [1-line summary]. See `_archive/ADR_FULL/ADR-001.md` |

**Benefits:**
- Reduces token budget (full text only loaded when needed)
- Table provides at-a-glance status
- Archive preserves full rationale for reference

**When to compress:** After ADR is stable (implemented, no recent changes, >30 days old)

---

## Active Decisions

### ADR-001: Verification Steps Required in Protocol

**Status:** Accepted
**Date:** 2025-12-28

**Context:**
In early protocol testing, Builder marked TODO items as complete without verifying they actually worked. Claimed fixes didn't actually fix bugs. TODO showed items complete that weren't actually done. Design systems (button colors, text conventions) weren't documented, causing Builder to improvise inconsistently across implementations.

**Decision:**  
Protocol v1.1 adds mandatory verification:
1. `..make` must write TODO items with acceptance criteria (AC format)
2. `..end` must verify implementation meets AC before marking complete
3. `..exit` must verify recent Builder work actually works
4. CONSTRAINTS.md is now required for design system rules

**Alternatives Considered:**
- Trust Builder's "done" claim — Failed in practice; bugs shipped
- Architect reviews every PR — Too slow; bottleneck
- Automated tests only — Doesn't catch UI/UX issues

**Consequences:**
- ✅ "Done" becomes verifiable, not assumed
- ✅ Design system documented before implementation prevents inconsistency
- ✅ Architect catches discrepancies at `..exit`
- ⚠️ Slightly more overhead for Builder (must test before marking done)
- ⚠️ Architect must actually run `..exit` verification

---

### ADR-002: CONSTRAINTS.md as Required File

**Status:** Accepted
**Date:** 2025-12-28

**Context:**
Builder improvised button colors and text because no design system was documented. This led to inconsistent UI with multiple variations of the same action (synonyms for navigation, varying button styles). Fixing these inconsistencies required rework.

**Decision:**  
Add CONSTRAINTS.md as a required protocol file containing:
- Core principles
- Design system (colors, text conventions, visual hierarchy)
- Explicitly rejected approaches
- Open questions

Architect's context scope now includes CONSTRAINTS.md.

**Consequences:**
- ✅ Design decisions documented before implementation
- ✅ Builder has clear reference for UI conventions
- ✅ Rejected approaches prevent re-litigating past decisions
- ⚠️ More upfront documentation work for Architect

---

### ADR-003: Token Budget Management and Post-v1.0 Hygiene

**Status:** Accepted
**Date:** 2026-01-15

**Context:**
Gym app team (Nov 2025 - Jan 2026) successfully shipped v1.0 using duo protocol but hit a "token ceiling" where context files ballooned from 5,000 words to 13,500 words (27% of session budget). Documentation became a burden instead of a tool. The protocol template lacked guidance on:
- When to archive content
- How to monitor token budget
- What to do after shipping v1.0

**The Problem:**
After shipping 14+ features:
- CLAUDE.md included historical narrative ("how we discovered X")
- DECISIONS.md had 14 ADRs (12 stable, 2 active)
- PROGRESS.md had 17 sessions with full narrative
- Architect spent >2 messages "catching up" before work started
- Files told stories instead of serving as reference

**The Insight:**
KayGee's principle "files ARE the AI's memory" needs a corollary:
> **"Memories should be indexed, not narrated."**

**Decision:**
Add post-v1.0 maintenance to protocol template:

1. **New file: PRINCIPLES.md**
   - Distilled wisdom from all ADRs (<2 min read)
   - Replaces need to read all historical decisions
   - Created after patterns emerge (>5 ADRs)

2. **Enhanced `..hygiene` command**
   - Token budget check (word count monitoring)
   - "Next Session Test" application
   - Principles extraction when >5 ADRs
   - Health levels: Good/Warning/Critical

3. **Token Budget Management (WORKFLOW.md)**
   - Target budgets: 15% Architect, 5% Builder
   - Monthly monitoring guidance
   - "Next Session Test" litmus test
   - Post-v1.0 hygiene checklist

4. **Updated onboarding flow (CLAUDE.md)**
   - PRINCIPLES.md creation during initialization
   - Reference in project structure

**Metrics from Gym App:**
- Before cleanup: 13,500 tokens (27% budget)
- After cleanup: 7,500 tokens (15% Architect), 2,500 tokens (5% Builder)
- Reduction: 40% in CLAUDE.md, 67% in DECISIONS.md, 80% in PROGRESS.md

**Alternatives Considered:**
- Trust teams to figure it out — Failed; gym app hit wall before realizing
- Archive only when critical — Too late; friction already present
- No PRINCIPLES.md file — Forces reading all ADRs every session

**Consequences:**
- ✅ Teams can sustain protocol beyond v1.0
- ✅ Token budget stays healthy (15%/5% targets)
- ✅ "Next Session Test" provides clear litmus test
- ✅ PRINCIPLES.md speeds up context loading
- ✅ Matches "files ARE memory" philosophy
- ⚠️ One more file to maintain (PRINCIPLES.md)
- ⚠️ Requires discipline to run monthly hygiene

**Key Learnings:**
1. **The "Next Session Test":** "Would Claude need this next session?" — Keep active reference, archive historical narrative
2. **The v1.0 Wall:** After 14+ features, documentation needs consolidation
3. **When cleanup is mandatory:** Token budget >20%, any file >3000 words, Architect sluggish
4. **Practice what we preach:** We adopted gym app's improvements immediately

---

## Template: New ADR

Copy this when adding decisions:

```markdown
### ADR-XXX: [DECISION_TITLE]

**Status:** Proposed | Accepted | Deprecated | Superseded
**Date:** [DATE]

**Context:**
[What situation prompted this decision?]

**Decision:**
[What did we decide?]

**Alternatives Considered:**
- [Option] — [why not chosen]

**Consequences:**
- ✅ [Positive]
- ⚠️ [Tradeoff]
```

### Compressing an ADR

When an ADR is stable (>30 days, implemented, no changes):

1. Copy full ADR to `_archive/ADR_FULL/ADR-XXX.md`
2. Replace full text with table row:
   ```markdown
   | ADR-XXX | [Title] | Accepted | [1-line]. See `_archive/ADR_FULL/ADR-XXX.md` |
   ```
3. Move row to "Compressed ADRs" table above

---

## Superseded Decisions

(Decisions that have been replaced go here with a link to the new ADR)

---

*Last updated: 2025-12-28*
