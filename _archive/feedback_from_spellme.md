# Feedback from SpellMe

**Date:** January 17, 2026
**Source:** SpellMe repo alignment pass
**Status:** Pending protocol review

This document captures innovations discovered in the SpellMe repo during the alignment pass. These patterns have been battle-tested in production and may warrant integration into the protocol-duo template.

---

## 1. PRINCIPLES.md Learnings

SpellMe's PRINCIPLES.md evolved beyond the template to include **operational patterns** — specific, actionable rules extracted from repeated decisions.

### What SpellMe Added

**Code Quality Principles:**
- Zero TypeScript Errors in Main Branch
- Test Migrations in Supabase Before Commit
- Explicitly Grant View Permissions

**Database & Schema Principles:**
- Database Schema is Source of Truth
- Migrations Run Before Frontend Deployment

**Access Control Principles:**
- Coach-Specific Features Enforce Role Checks (with code pattern example)

**Task Management Principles:**
- All TODOs Require Testable Acceptance Criteria
- Feature Commits Must Update Documentation

**Commit Strategy Principles:**
- Micro-Commits: One Feature Per Commit

**UI Development Principles:**
- All UI Features Work on 375px Viewport
- CTA Buttons Visible Without Scrolling

**Testing Principles:**
- Regression Tests Required After Deployment

**Architecture Principles:**
- External AI Over Built-In LLM
- Coach Autonomy Over Opaque Recommendations

### Example Pattern Format

```markdown
### Zero TypeScript Errors in Main Branch
> **Pattern:** Fixed TS6133, TS6196, TS2339 errors multiple times (commits 3dde116, b3b439a)

**Principle:** Main branch must have zero TypeScript errors. Fix all errors before merging.

**Rationale:** Unused variables and type errors compound. Catching them early prevents production bugs.
```

### Potential Protocol Integration

**Option A:** Add "Operational Patterns" section to PRINCIPLES.md template with example categories

**Option B:** Create separate PATTERNS.md for project-specific operational rules

**Option C:** Include SpellMe's PRINCIPLES.md as exemplar in `_archive/EXAMPLES/`

---

## 2. TODO.md Evolution

SpellMe's TODO.md evolved beyond simple priority buckets to include strategic context and specialized sections.

### Additions Beyond Template

**1. Strategic Context Section (at top)**
```markdown
## Strategic Context (Jan 17, 2026)

**The Problem:** Schools assign 18 words/week, kids retain ~5. Teacher feedback shows need for:
- 5 words per week (not 18)
- Daily 5-10 min practice routine
...

**Marketing Position:** "Learn Less, Remember More"
```
- Provides "why" for the work below
- Updated periodically, not per-session
- Helps new sessions understand current focus

**2. Phase-Based Organization**
```markdown
### PHASE A: AI Export Trust Layer (2-4 hours)
> **Rationale:** Quick win that differentiates from competitors...

### PHASE B: Guided Daily Practice MVP (4-6 weeks)
> **Rationale:** Core product evolution...
```
- Groups related work into logical phases
- Includes effort estimates per phase
- Rationale explains why this phase matters

**3. "In Progress" Section**
```markdown
## In Progress

(Nothing currently in progress)
```
- Explicit tracking of what's actively being worked
- Prevents starting new work while something is half-done

**4. Known Issues Section**
```markdown
## Known Issues

- [ ] **Space creation fragility**
  - AC: Space creation works on first attempt
  - Context: Has regressed before, workaround in CLAUDE.md troubleshooting
```
- Separates bugs from features
- Maintains awareness of known fragility

**5. Technical Debt Section**
```markdown
## Technical Debt

- [ ] **Add TypeScript strict mode**
  - AC: `strict: true` in tsconfig.json
  - AC: All type errors resolved
```
- Separates debt from features
- Prevents debt from getting lost in backlog

**6. Decisions Pending ADR**
```markdown
## Decisions Pending ADR

- [ ] **ADR-015: Guided Daily Practice Mode**
  - Decision: Replace freeform sessions OR add as parallel mode?
  - Recommendation: Add as parallel mode...
```
- Tracks items needing formal decision
- Prevents analysis paralysis by documenting recommendations

### Potential Protocol Integration

**Option A:** Add all sections to TODO.md template with [PLACEHOLDER] markers

**Option B:** Add as optional sections with HTML comments showing examples

**Option C:** Document in WORKFLOW.md as "TODO.md can grow these sections as project matures"

---

## 3. Summary of Upstream Opportunities

| Innovation | Complexity | Value | Recommendation |
|------------|------------|-------|----------------|
| Operational patterns in PRINCIPLES.md | Medium | High | Add example categories to template |
| Strategic Context in TODO.md | Low | Medium | Add as optional section |
| Phase-based TODO organization | Medium | Medium | Document as pattern, don't enforce |
| In Progress section | Low | High | Add to template |
| Known Issues section | Low | High | Add to template |
| Technical Debt section | Low | High | Add to template |
| Decisions Pending ADR | Low | Medium | Add as optional section |

---

## Protocol Review Complete (2026-01-19)

**Reviewed by:** Architect session
**Decision:** ADR-004 in DECISIONS.md

### Integrated into Template ✅

| Pattern | Location |
|---------|----------|
| In Progress section | TODO.md `## 🟠 In Progress` |
| Known Issues section | TODO.md `## ⚠️ Known Issues` |
| Technical Debt section | TODO.md `## 🔧 Technical Debt` |

### Rejected (with rationale)

| Pattern | Reason |
|---------|--------|
| Operational Patterns in PRINCIPLES.md | PRINCIPLES.md is for ADR distillation, not code standards |
| Strategic Context in TODO.md | Duplicates PRFAQ.md's purpose |
| Phase-based TODO organization | Time estimates contradict protocol; not working well in SpellMe |
| Decisions Pending ADR | Already covered by Open Questions |

---

## SpellMe Downstream Sync Instructions

When syncing SpellMe to protocol v1:

### 1. Fix PRINCIPLES.md Usage
- **Current state:** Contains operational patterns (Zero TS Errors, Test Migrations, etc.)
- **Correct usage:** Distilled wisdom from ADRs only
- **Action:** Move operational patterns to new PATTERNS.md or CLAUDE.md "Code Standards" section

### 2. Move Strategic Context to PRFAQ.md
- **Current state:** Strategic Context section in TODO.md
- **Correct location:** PRFAQ.md "Appendix: The Problem We're Solving"
- **Action:** Move content, update PRFAQ.md, remove from TODO.md

### 3. Remove Phase-Based Organization
- **Current state:** Phase A, Phase B with time estimates
- **Issue:** Not working well, time estimates contradict protocol
- **Action:** Flatten to standard priority sections (Blocking, In Progress, Ready, Backlog)

### 4. Adopt Standard TODO.md Sections
- **Add:** 🟠 In Progress, ⚠️ Known Issues, 🔧 Technical Debt
- **Use:** Open Questions (not "Decisions Pending ADR")

### 5. Align CONSTRAINTS.md
- **Ensure:** Open Questions section present
- **Check:** AI Boundaries section (already present from earlier sync)

---

*This file has been processed. Archive to `_archive/` when SpellMe sync is complete.*
