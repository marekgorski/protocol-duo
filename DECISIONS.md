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
The protocol adds mandatory verification:
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
A team using duo protocol successfully shipped their v1.0 but hit a "token ceiling" where context files ballooned from 5,000 words to 13,500 words (27% of session budget). Documentation became a burden instead of a tool. The protocol template lacked guidance on:
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

3. **Token Budget Management (CLAUDE.md)**
   - Target budgets: 15% Architect, 5% Builder
   - Monthly monitoring guidance
   - "Next Session Test" litmus test
   - Post-v1.0 hygiene checklist

4. **Updated onboarding flow (CLAUDE.md)**
   - PRINCIPLES.md creation during initialization
   - Reference in project structure

**Observed Metrics:**
- Before cleanup: 13,500 tokens (27% budget)
- After cleanup: 7,500 tokens (15% Architect), 2,500 tokens (5% Builder)
- Reduction: 40% in CLAUDE.md, 67% in DECISIONS.md, 80% in PROGRESS.md

**Alternatives Considered:**
- Trust teams to figure it out — Failed; teams hit the wall before realizing
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
4. **Practice what we preach:** Adopt improvements from downstream immediately

---

### ADR-004: TODO.md Template Enhancement — In Progress, Known Issues, Technical Debt

**Status:** Accepted
**Date:** 2026-01-19

**Context:**
A downstream project's alignment pass revealed innovations in TODO.md structure that evolved beyond the template. After assessment, three patterns proved genuinely valuable while others were rejected for duplicating existing mechanisms or adding premature structure.

**Decision:**
Add three new sections to TODO.md template:

1. **🟠 In Progress** — Active work tracking
   - Prevents starting new work while something is half-done
   - Solves "what was I working on?" across sessions
   - Limit to 1-2 items

2. **⚠️ Known Issues** — Documented fragility
   - Separates bugs from features
   - Maintains awareness of known fragility without blocking feature work
   - Includes AC + context format

3. **🔧 Technical Debt** — Code quality improvements
   - Prevents debt from getting lost in feature backlog
   - Keeps it visible without blocking feature prioritization
   - Includes AC + impact format

**Rejected Patterns:**

| Pattern | Why Rejected |
|---------|--------------|
| Operational Patterns in PRINCIPLES.md | PRINCIPLES.md is for ADR distillation, not code standards. Projects needing this can spawn PATTERNS.md |
| Strategic Context in TODO.md | Duplicates PRFAQ.md's purpose |
| Phase-based organization | Time estimates contradict protocol guidance; premature structure |
| Decisions Pending ADR | Already covered by Open Questions in TODO.md and CONSTRAINTS.md |

**Consequences:**
- ✅ TODO.md becomes more complete task management tool
- ✅ Bugs, debt, and features have separate tracking
- ✅ "In Progress" provides session continuity
- ✅ Template stays lean (example format, not mandatory content)
- ⚠️ Slightly more sections to understand
- ⚠️ Downstream projects need alignment to use corrected patterns

---

### ADR-005: v1.3 Structural Discipline — five layers move at once

**Status:** Accepted
**Date:** 2026-05-18

**Context:**
v1.2 shipped the coaching philosophy (hooks remind rather than punish). v1.2.2 simplified the Stop hook after 29 days clean production data on one production deployment. By 2026-05-18 the locus of discipline was still rules+hook-enforcement — declarative anti-patterns caught failures at output, not input.

Multiple mid-2026 signals converged on the same operationalisation of Principle #10: move discipline from declarative anti-patterns to write-time structural gates. Convergent across sources, with date-stamped case studies — meeting the case-study bar that v1.3 also codifies.

**Decision:**
v1.3 moves five layers in a single release because they're load-bearing on each other:

| Layer | Before | After |
|---|---|---|
| Rule creation | Rules added on conviction, trimmed at audit | Hard Rule #6: case-study gate at the moment a rule is written (case study AND level designation) |
| Schema | Pre-deployment 4-type front-matter; status field rotted to 30+ snowflake values at scale | At-scale-proven `type/updated/summary` schema migrates in with 60-day compat shim |
| Harness | Coaching philosophy with simplified hooks still policing every interaction | Hookless `{ "hooks": {} }` becomes canonical default; hooks remain available as opt-in |
| Falsification | Public commitments published; nobody watching them | a dedicated folder watches each commitment with explicit promotion criteria + falsification triggers |
| RC mechanism | Release candidates ad-hoc; V1.2.2 was the worked example without the rule | a release-candidate carve-out with 5 conditions and named promotion triggers |

Plus foundational protocol-vs-flavour stratification: Hard Rules sit at TWO levels (protocol-level = the brewery, constants; flavour-level = the recipe, this canonical template's specific rules). duo gets its first flavour-level Hard Rule in v1.3: *D1. Docs travel with code* — convergent invention in two production deployments verbatim.

Plus new anti-pattern: *"Celebrating a primitive by over-implementing it"* — codifies the v1.2 hook deployment lesson so the next harness primitive doesn't trigger the same over-implementation reflex.

**Alternatives Considered:**
- Stay at v1.2.x and iterate philosophy further — Risk: the locus stays in rules+hooks; the structural-gate insight gets lost
- Ship each layer separately as v1.2.3 / v1.2.4 / v1.2.5 — Risk: the layers are load-bearing on each other (case-study gate without level designation = muddled; schema without compat shim = forced fleet sync timing; hookless without anti-pattern fence = same celebration reflex on next primitive)
- Ship as v2.0 — The shift is a paradigm shift but builds on v1.2.x foundations rather than replacing them; minor bump (v1.3) signals continuity with significance

**Consequences:**
- ✅ Audits become lookups (does the rule cite a case study?) rather than judgment calls
- ✅ Schema reconciliation unblocks fleet `..sync` (duo repos lagging finally migrate)
- ✅ Hookless retires v1.2 over-implementation; harness gets out of the way unless a specific gap is named
- ✅ Public commitments get a structural watching mechanism (incubation folder)
- ✅ Protocol-vs-flavour stratification clears asymmetry-vs-distinction confusion (the DECISIONS.md presence and CLAUDE.md-shape distinctions no longer "drift")
- ⚠️ Migration cost: existing front-matter files need sed migration (compat shim 60 days)
- ⚠️ Repos resistant to hookless migration may stay on simplified hooks indefinitely (opt-in pattern, not enforced)

**Public articulation:** kayg.ee/learn/structural-discipline (live 2026-05-17 ahead of canonical).

**Source-of-truth:** the v1.3 patch brief — 14-item dispositioned brief; 9 PROMOTE applied this release; 5 DEFER documented in changelog with re-evaluation triggers.

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
