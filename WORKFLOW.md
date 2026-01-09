# WORKFLOW.md - Development Process

## Session Commands Reference

| Command | Purpose | When to Use |
|---------|---------|-------------|
| `..architect` | Enter planning mode | Design decisions, architecture |
| `..builder` | Enter implementation mode | Writing code, building features |
| `..start` | Load context | Every session start |
| `..make` | Design a feature | Before building |
| `..go` | Execute a task | Ready to implement |
| `..end` | Close session | After completing work |
| `..hygiene` | Prune old context | Files getting large |
| `..exit` | Fossilize context | End of major phase |

---

## Role Definitions

### Architect (Planning Mode)
- Design decisions and architecture
- Product prioritization
- Reviews codebase via filesystem access
- Does NOT write implementation code

### Builder (Implementation Mode)
- Executes code changes
- Follows micro-commit strategy
- Reports back on implementation status
- Does NOT question architecture

---

## Commit Strategy

### Micro-Commits
Every meaningful change gets its own commit:
- Single feature or fix per commit
- Descriptive commit message
- Easy to revert if something breaks

### Commit Message Format
```
[AREA] Brief description

- Detail 1
- Detail 2

Context: Why this change was made
```

### Save Game Rule
Before any major refactor or risky change:
1. Commit current working state
2. Note commit hash in conversation
3. Proceed with changes
4. Can always `git reset --hard [hash]` to recover

---

## Session Handoff Protocol

### Starting a Session
1. Read PROGRESS.md for last session state
2. Read TODO.md for current priorities
3. Review recent commits: `git log --oneline -5`

### Ending a Session
1. Update PROGRESS.md with what was accomplished
2. Update TODO.md — mark complete, add new items
3. Update DECISIONS.md if architectural choices were made
4. Commit all documentation changes
5. Push to remote

---

## File Size Thresholds

Run `..hygiene` when files exceed these sizes:
- `DECISIONS.md` > 50KB
- `PROGRESS.md` > 30KB  
- `TODO.md` > 100 items

### Hygiene Process
1. Archive old PROGRESS entries → `_archive/PROGRESS_[YYYY-MM].md`
2. Archive completed TODOs → `_archive/TODO_DONE_[YYYY-MM].md`
3. Compress superseded ADRs → `_archive/DECISIONS_ARCHIVE.md`

---

## Context Files

```
[PROJECT_NAME]/
├── CLAUDE.md           # Technical reference
├── PRFAQ.md            # Product vision (Press Release + FAQ)
├── CONSTRAINTS.md      # Principles, design system, rejected approaches
├── DECISIONS.md        # Architecture decisions
├── TODO.md             # Task list
├── PROGRESS.md         # Session log
├── WORKFLOW.md         # This file
├── ROLE_PROTOCOL.md    # AI commands
├── MAREK.md            # Human-only tasks (optional)
└── _archive/           # Old content
```

---

*Last updated: [DATE]*
