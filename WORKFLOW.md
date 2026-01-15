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

## Token Budget Management

### Why It Matters

AI forgets everything between conversations, so files are its memory. But if those files grow too large, you burn token budget before any work starts.

**The v1.0 Wall:**
After shipping 14+ features, documentation can balloon from 5,000 words to 15,000+ words. Without maintenance, Architect mode burns 25%+ of session budget just loading context.

**Target Budget:**
- **Architect Mode:** ~15% token budget (7,500 tokens, ~10,000 words)
- **Builder Mode:** ~5% token budget (2,500 tokens, ~3,500 words)

### Monitoring

**Check monthly** or after major milestones (v0.5, v1.0):

```bash
wc -w *.md
```

**Health Levels:**
- ✅ **Good:** Total <10,000 words, no single file >3,000 words
- ⚠️ **Warning:** Total 10,000-15,000 words, or any file >3,000 words
- 🚨 **Critical:** Total >15,000 words, or any file >5,000 words

### The "Next Session Test"

For every section in a context file, ask:
> "Would Claude need this to start fresh next session?"

**Keep (Active Reference):**
- Current architecture and tech stack
- Active decisions (last 2-3 ADRs)
- Technical patterns Claude will use
- Design system rules
- Next 5-10 tasks

**Archive (Historical Narrative):**
- "How we discovered X" stories
- Debugging session notes from 2+ weeks ago
- Superseded ADRs (decisions that are now stable)
- Completed tasks from >30 days ago
- Evolution explanations ("variant cycling went through 3 iterations...")

### When Cleanup Becomes Mandatory

**Immediate Blockers** (run `..hygiene` NOW):
1. Token budget shows 🚨 Critical (>15,000 words)
2. Any single .md file exceeds 5,000 words
3. Claude asks "which version?" about a decision (context confusion)
4. Architect spends >2 messages "catching up" on project state

**Warning Signs** (plan cleanup soon):
1. More than 10 implemented ADRs in DECISIONS.md
2. More than 10 sessions in PROGRESS.md
3. Same concept explained in 3+ files
4. CLAUDE.md reads like a story, not reference

**Healthy Maintenance** (proactive, not reactive):
- Monthly hygiene check (first Monday)
- After v0.5, v1.0, v2.0 milestones
- When extracting PRINCIPLES.md from patterns

### Post-v1.0 Hygiene Checklist

Run after major milestones (v0.5, v1.0, v2.0) or when hitting ⚠️ Warning level:

- [ ] Run token budget check: `wc -w *.md`
- [ ] Create/update PRINCIPLES.md from ADR patterns
- [ ] Archive stable ADRs (keep 2-3 active in DECISIONS.md)
- [ ] Archive PROGRESS sessions >30 days to `_archive/PROGRESS_[YYYY-MM].md`
- [ ] Slim CLAUDE.md (remove history, keep reference)
- [ ] Apply "Next Session Test" to all flagged files
- [ ] Update cross-references (link to archives)
- [ ] Commit and push: `git add -A && git commit -m "docs: v[X] hygiene pass" && git push`

**Frequency:**
- After v1.0 shipping (always)
- Monthly if actively developing
- When token budget exceeds 20%

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
├── PRINCIPLES.md       # Distilled wisdom from ADRs (<2 min read)
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
