# DECISIONS.md - Architecture Decision Records

This file tracks architectural decisions for duo Protocol.

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

---

## Superseded Decisions

(Decisions that have been replaced go here with a link to the new ADR)

---

*Last updated: 2025-12-28*
