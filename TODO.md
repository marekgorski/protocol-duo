# TODO

> Prioritized task list. Top item = next action.  
> Use ownership markers: `[C]` Claude, `[M]` Marek, `[C→M]` Claude→Marek, `[M→C]` Marek→Claude  
> No marker = `[C]` (Claude can complete)

## 🔴 Blocking

>>> [PLACEHOLDER: Add your first blocking task after onboarding] <<<

Example format:
```
- [ ] [C] Task description
  - AC: Acceptance criterion 1
  - AC: Acceptance criterion 2

- [ ] [M] Human-only task
  - AC: What success looks like
  - Blocks: [component waiting on this]

- [ ] [C→M] Claude prepares, human executes
  - AC: Deliverable created in /drafts/
  - AC: Human reviews and executes

- [ ] [M→C] Human decides, Claude implements
  - AC: Decision documented
  - Unblocks: [what Claude will do after]
```

## 🟠 In Progress

> Active work. Limit to 1-2 items. Complete before starting new work.

(Currently empty)

## 🟡 Ready to Build

- [ ] **Sync SpellMe to protocol v1**
  - AC: Fix PRINCIPLES.md usage (move operational patterns to PATTERNS.md or CLAUDE.md)
  - AC: Move strategic context from TODO.md to PRFAQ.md
  - AC: Remove phase-based organization from TODO.md
  - AC: Add In Progress, Known Issues, Technical Debt sections
  - AC: Verify Open Questions section in place (not "Decisions Pending ADR")
  - AC: Archive `feedback_from_spellme.md` after sync complete
  - Context: Detailed instructions in `feedback_from_spellme.md` "SpellMe Downstream Sync Instructions"

- [ ] **Align remaining repos to v1**
  - AC: Identify all repos using protocol-duo
  - AC: Run alignment pass on each (gym already done, spellme in progress)
  - AC: Capture innovations from each in feedback files
  - AC: All repos on v1 before public launch

## 🔵 Backlog

## ⚠️ Known Issues

> Documented fragility. Bugs and regressions tracked separately from features.

Example format:
```
- [ ] **Issue description**
  - AC: What "fixed" looks like
  - Context: How it manifests, any workarounds
```

## 🔧 Technical Debt

> Code quality improvements. Important but not urgent.

Example format:
```
- [ ] **Debt item**
  - AC: Specific improvement criteria
  - Impact: What this enables or prevents
```

## Open Questions

> Items needing decisions before becoming tasks. Once decided, move to DECISIONS.md and create a task here.

---

*See ROLE_PROTOCOL.md for full task ownership and handoff protocol*
