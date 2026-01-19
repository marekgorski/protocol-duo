# CLAUDE.md

## 🚀 First-Time Setup

**Claude:** If you see `[PLACEHOLDER]` markers in these files, this project hasn't been initialized yet. Run the onboarding flow below.

---

### Onboarding Flow

When a user first opens this project, guide them through discovery before doing anything else.

**Step 1: Discovery Questions**

Ask these one at a time, conversationally. Don't dump all questions at once.

1. "What are we building? Give me the one-liner."
2. "Who is it for? Who's the primary user?"
3. "What problem does it solve? What's broken or painful today?"
4. "What does MVP success look like? How will we know it's working?"
5. "Any constraints I should know? (tech preferences, timeline, budget, etc.)"

**Step 2: Reflect Understanding**

After gathering answers, reflect back before proceeding:

```
"Let me make sure I understand:

**Project:** [What we're building]
**Users:** [Who it's for]
**Problem:** [What's broken today]
**MVP Success:** [How we'll know it works]
**Constraints:** [Tech/time/budget limits]

Does this capture it? Anything I'm missing or got wrong?"
```

**Step 3: Populate Docs**

Once user confirms, update these files with real content:
- `PRFAQ.md` — Write press release and FAQs
- `PRINCIPLES.md` — Extract initial principles from discovery answers (mission, 2-3 product principles)
- `DECISIONS.md` — Document initial architecture choices
- `TODO.md` — Create prioritized task list
- `CLAUDE.md` — Replace this section with project-specific technical reference
- `README.md` — Replace template README with project-specific description
- `PROGRESS.md` — Fill in the initialization session entry with actual details

Remove all `[PLACEHOLDER]` markers when done.

**Step 4: Confirm Ready**

```
"Project initialized! Here's what I've set up:
- PRFAQ.md: [brief summary]
- DECISIONS.md: [key decisions]
- TODO.md: [top priorities]
- CLAUDE.md: [project overview]
- README.md: [project description]
- PROGRESS.md: [initialization session logged]

Ready to start building. You can use:
- `..architect` — Enter planning mode
- `..builder` — Enter implementation mode

What would you like to tackle first?"
```

**Step 5: Commit & Push**

After user confirms, commit and push all changes:

```bash
git add -A && git commit -m "Initialize project: [PROJECT_NAME]" && git push
```

Always commit and push after completing a unit of work. Don't let changes pile up locally.

---

## System Protocol

This project uses the **duo workflow protocol** for AI-assisted development.

### Protocol Evolution Philosophy

This instance of protocol-duo may **intentionally drift** from the master template based on project-specific needs. This drift is a feature, not a bug.

**The Reintegration Cycle:**
1. **Clone** — Start from protocol-duo template
2. **Initialize** — Customize for project needs (one-way door)
3. **Drift** — Evolve based on real-world usage
4. **Reintegrate** — Contribute learnings back to master protocol
5. **Redistribute** — Improved protocol benefits all future clones

Each repo's learnings strengthen the collective. When you discover patterns that work well, document them and consider contributing back to `protocol-duo`.

### Commands

| Command | Mode | Purpose |
|---------|------|---------|
| `..architect` | Planning | Design, strategy, architecture |
| `..builder` | Implementation | Write code, execute tasks |
| `..start` | Architect | Load context, show priorities |
| `..make` | Architect | Design a feature, write specs |
| `..go` | Builder | Execute top task from TODO |
| `..end` | Builder | Close session, update docs |
| `..hygiene` | Architect | Archive old content, prune files |
| `..exit` | Architect | Fossilize context for handoff |

See `ROLE_PROTOCOL.md` for full command specifications.

### Quick Rules

1. **Architect designs, Builder implements** — Don't mix roles
2. **Docs are source of truth** — Update TODO, PROGRESS, DECISIONS after changes
3. **Commit & push after each task** — Don't let work pile up locally
4. **Context files stay lean** — Run `..hygiene` when files grow large

---

## Environment Notes

Document tool-specific quirks and workarounds here. This helps future contributors (human or AI) avoid known pitfalls.

**Example format:**

| Tool/Integration | Known Behavior | Workaround |
|------------------|----------------|------------|
| Figma Make | Sometimes claims fixes without making them | Always verify code changes actually happened |
| Figma Make | Leaves orphan files when refactoring | Use explicit delete prompts |
| [Your Tool] | [Behavior] | [Workaround] |

**Tip:** Add entries as you discover issues. This section is project-specific — remove the examples above once you have real entries.

---

## Project Overview

> ⚠️ **Not yet initialized.** Run onboarding flow above.

**Project:** [PROJECT_NAME]

**One-liner:** [BRIEF_DESCRIPTION]

**Status:** Not started

---

## Tech Stack

| Layer | Choice | Rationale |
|-------|--------|-----------|
| [LAYER] | [CHOICE] | [WHY] |

---

## Project Structure

```
[PROJECT_NAME]/
├── CLAUDE.md           # Technical reference (this file)
├── PRFAQ.md            # Product vision (Press Release + FAQ)
├── PRINCIPLES.md       # Distilled wisdom from ADRs (<2 min read)
├── TODO.md             # Prioritized task list
├── PROGRESS.md         # Session-by-session log
├── DECISIONS.md        # Architecture Decision Records
├── CONSTRAINTS.md      # Principles, rejected approaches
├── WORKFLOW.md         # Development process
├── ROLE_PROTOCOL.md    # AI workflow commands
├── MAREK.md            # Human-only tasks (optional - rename to your name)
└── README.md           # User-facing documentation
```

---

## Data Model

[DESCRIBE_DATA_STRUCTURES]

---

## Key Flows

[DESCRIBE_USER_FLOWS]

---

## Implementation Notes

[TECHNICAL_DETAILS]

---

## Related Documentation

| File | Purpose |
|------|---------|
| `PRFAQ.md` | Product vision (Press Release + FAQ) |
| `PRINCIPLES.md` | Distilled wisdom from ADRs (<2 min read) |
| `DECISIONS.md` | Architecture Decision Records |
| `CONSTRAINTS.md` | Principles, rejected approaches, design system |
| `TODO.md` | Prioritized task list |
| `PROGRESS.md` | Session-by-session development log |
| `WORKFLOW.md` | Development process and commit strategy |
| `ROLE_PROTOCOL.md` | AI workflow commands |
| `MAREK.md` | Human-only tasks (optional - rename to your name) |
| `README.md` | User/setup documentation |

---

*Last updated: [DATE]*
*Status: [STATUS]*
