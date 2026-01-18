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

## 🟡 Ready to Build

- [ ] **Review feedback_from_spellme.md and decide template integrations**
  - AC: Review PRINCIPLES.md learnings section
  - AC: Decide: Add "Operational Patterns" section to PRINCIPLES.md template?
  - AC: Review TODO.md evolution section
  - AC: Decide: Add "In Progress", "Known Issues", "Technical Debt" sections to TODO.md template?
  - AC: Decide: Add "Strategic Context" as optional section?
  - AC: Document decisions in DECISIONS.md
  - AC: Archive feedback_from_spellme.md after processing
  - Context: SpellMe alignment pass (Jan 17, 2026) identified patterns worth considering

- [ ] **Continue SpellMe downstream sync**
  - AC: After processing feedback, sync protocol improvements back to SpellMe
  - AC: Update SpellMe's ROLE_PROTOCOL.md with any missing v1 features
  - AC: Update SpellMe's WORKFLOW.md with token budget management section
  - AC: Verify SpellMe has enhanced `..hygiene` command
  - Blocks: feedback_from_spellme.md review must complete first

- [ ] **Align remaining repos to v1**
  - AC: Identify all repos using protocol-duo
  - AC: Run alignment pass on each (gym already done, spellme in progress)
  - AC: Capture innovations from each in feedback files
  - AC: All repos on v1 before public launch

## 🔵 Backlog

## Open Questions

> Items needing decisions before becoming tasks. Once decided, move to DECISIONS.md and create a task here.

---

*See ROLE_PROTOCOL.md for full task ownership and handoff protocol*
