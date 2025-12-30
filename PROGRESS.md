# PROGRESS

> Session-by-session development log. Newest entries at top.

---

## 2025-12-28 — Protocol Maintenance Admin Folder

**Context**: Need to fossilize the audit/sync workflow discovered during v1.2 rollout across repos.

**Added `/admin` folder with:**
- `INSTRUCTIONS.md` — Full audit, version bump, and sync workflow
- `VERSION-USAGE.md` — Tracker of repos using the protocol with sync status
- `DRIFT-LOG.md` — Log innovations discovered in downstream repos
- `SYNC-CHECKLIST.md` — Quick checklist for performing a sync
- `PATTERNS.md` — Optional patterns not in core protocol (SECURITY.md, CONTEXT_PROMPT.md, etc.)

**Updated:**
- `README.md` — Added admin folder documentation, updated Quick Start to remove admin on clone

**Key decisions:**
- Admin folder is for protocol maintainers only, not project users
- Clone instructions now include `rm -rf admin/`
- Version tracking includes "Last Checked" dates
- Drift log uses `[UPSTREAM]` and `[DONE]` tags

---

## 2025-12-28 — Human/AI Task Handoff System

**Context**: Tasks requiring human action were blocking progress without clear ownership.

Added:
- Task ownership markers: `[C]`, `[M]`, `[C→M]`, `[M→C]`
- MAREK.md restructured with status sections (Blocked, Ready for Marek, Waiting on Decision, Completed)
- Handoff protocol for each marker type
- `..builder` now checks MAREK.md for completed human tasks
- `..architect` now identifies stale `[M]` tasks (>7 days) and suggests task splits
- `..make` assigns ownership markers to each task

Workflow:
1. `..make` assigns markers and routes tasks to TODO.md or MAREK.md
2. Claude completes `[C]` tasks normally
3. For `[C→M]`: Claude creates deliverable → moves to MAREK.md
4. Marek completes `[M]` tasks → adds output
5. `..go` picks up completed human tasks and unblocks dependent work

**Stretch Goals (Future)**:
- SECURITY.md template for security-sensitive projects (learned from pattern-auth)
  - Threat model analysis
  - What it protects vs. doesn't protect
  - Required hardening for production
  - Responsible disclosure process

---

## 2025-12-28 — Protocol v1.2 Final (MAREK.md + Environment Notes)

**Context**: Syncing all repos to v1.2 with final features from KayGee.

Done:
- Added MAREK.md template for human-only tasks
- Added Environment Notes section to CLAUDE.md (tool quirks + workarounds)
- Updated README to include MAREK.md in file structure
- Updated ROLE_PROTOCOL.md Related Documentation section
- Documented `..hygiene` threshold customization tip

Learned from KayGee:
- MAREK.md prevents AI from spinning on tasks it can't complete
- Environment Notes documents tool-specific quirks (e.g., Figma Make behavior)
- "Tom in MySpace" metaphor makes the human tasks file memorable

All repos now at v1.2:
- Layer3 Protocol ✔️
- Gym ✔️
- SpellMe (v3.2) ✔️
- Light Protocol ✔️
- KayGee ✔️

---

## 2025-12-28 — MAREK.md Template Added

**Context**: KayGee had MAREK.md for human-only tasks. Backporting to all repos.

Done:
- Added MAREK.md template (human-only tasks file)
- Updated CLAUDE.md to reference MAREK.md and CONSTRAINTS.md in file structure
- Updated Related Documentation table

The MAREK.md pattern:
- Separates tasks AI can't do (recording, photos, external decisions)
- Prevents AI from spinning on blocked tasks
- Makes handoff explicit ("human does X, then Builder can do Y")
- Fun touch: rename to your own name (like adding Tom on MySpace)

---

## 2025-12-28 — Protocol v1.2 Update (SpellMe Backport)

**Context**: SpellMe v3.1 had features that improve the protocol experience.

Done:
- Backported token budget awareness ("~15% token budget loaded")
- Added Context Drift Check to `..go` (checks git pull)
- Added estimated time to `..go` mission brief
- Improved blocked format with "Tried/Need" structure
- Added Recovery Levels (Level 1: Git, Level 2: Database, Level 3: Full Reset)
- Added permission check error formats
- Added file size thresholds to `..hygiene`
- Added "Context Drift" to anti-patterns table
- Updated README to v1.2

Decided:
- Token budget awareness helps users understand context cost
- Context drift check prevents stale code conflicts
- Recovery levels provide graduated response to problems

Next:
- Consider adding CONTEXT_PROMPT.md template for quick context loading

---

## 2025-12-28 — Protocol v1.1 Update

**Context**: Learnings from gym project revealed gaps in v1.0 protocol.

Done:
- Updated ROLE_PROTOCOL.md to v1.1
  - Added `..recover` command for emergency recovery
  - Added acceptance criteria requirement to `..make`
  - Added verification steps to `..end` (test before marking done)
  - Added verification to `..exit` (check Builder work actually works)
  - Added "Documentation Requirements" section
  - Added "Anti-Patterns Learned" section
- Created CONSTRAINTS.md template
  - Design system rules (button colors, text conventions)
  - Visual hierarchy guidelines
  - Mobile viewport targets
- Updated README.md
  - Added CONSTRAINTS.md to file structure
  - Added `..recover` to commands reference
  - Updated command descriptions
  - Bumped version to v1.1

Decided:
- CONSTRAINTS.md is now a required file (holds design system)
- Every TODO item must have acceptance criteria (AC format)
- Builder must verify implementation before marking complete
- Architect must verify Builder work on `..exit`

Next:
- Consider adding onboarding question for design system preferences
- Document common AC patterns as examples

---

## Session Template

YYYY-MM-DD — [Session Focus]

Done:
- Item completed

Decided:
- Decision made (also add to DECISIONS.md if significant)

Next:
- What's queued for next session
