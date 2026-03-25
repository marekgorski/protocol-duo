# CLAUDE.md

## Hard Rules — Override Everything, No Exceptions

1. **Files are memory.** Everything in .md files committed to git. No tool-specific persistence (agent memories, session resume). If it's not in a file, it doesn't exist.
2. **Never fabricate.** Accuracy over impressiveness. Don't invent URLs, API endpoints, facts, or capabilities. Say "I'm not sure" instead.
3. **RECORD after every interaction.** Update files and commit immediately. Don't batch at session end. This is the compound effect.
4. **Pre-scan before changes, post-scan after.** Check all references before modifying. Verify 0 stale references after.
5. **Scope the correction.** When the user gives feedback, change ONLY what was asked. Don't expand scope. State what should NOT change if unclear.

---

Technical reference for Claude Code when working on this project.

**Workflow commands:** When user types `..architect`, `..builder`, or any `..command`, read and follow [ROLE_PROTOCOL.md](./ROLE_PROTOCOL.md).

### Boot Sequence (runs every session start)

**On ANY first interaction** — whether "hello", "let's start", `..architect`, or a paragraph of instructions — execute this boot sequence before responding:

1. **Read ALL `.md` files** in the project root
2. **Scan TASKS/ folder** — read all task files
3. **Read last 20 git commits:** `git log --oneline -20`
4. **Check git status:** `git status`
5. **Then** process the user's input with full context

This is non-negotiable. CLAUDE.md is loaded automatically — this boot sequence IS the startup behavior. Users should never need to ask for context to be loaded.

---

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

By default, I load full project context every session — all your docs, decisions, and history. This gives me the full picture for any kind of work.

When you're deep in implementation and want faster sessions, use `..builder` — I'll load just the essentials and focus on executing.

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

### Atomic Interaction Contract

Every interaction follows this cycle automatically:

| Step | What Happens |
|------|--------------|
| **LOAD** | Read context files, check git status |
| **CLARIFY** | Confirm understanding before acting |
| **EXECUTE** | Do the work |
| **RECORD** | Update .md files, commit immediately |
| **REFLECT** | Surface improvements, flag drift |

**Default scope:** Full (all .md files + recent git history — see Boot Sequence above)

**Scope modifiers:**
- `..architect` — Full context: all docs, decisions, and history loaded
- `..builder` — Lean context: essentials only (CLAUDE.md, TODO.md, TASKS/)

Without a modifier, use default full scope. The atomic cycle runs regardless of scope.

**Fossilization is automatic.** The RECORD step commits decisions and context every interaction. No ceremony required at session end.

### Protocol Settings

Configure protocol behavior per-project:

```
lean_mode: off
```

| Setting | Values | Effect |
|---------|--------|--------|
| `lean_mode` | `on` / `off` | **on:** Load essentials only (CLAUDE.md + TODO.md + TASKS/). Faster boot, less context. Use `..architect` to expand. **off:** Full boot sequence — all .md files + git history loaded every session. |

**Default:** `off` (full context). Set to `on` for large projects where faster boot matters.

**To change:** Edit the `lean_mode` line above. Claude reads this on each session.

### Protocol Evolution Philosophy

This instance of protocol-duo may **intentionally drift** from the master template based on project-specific needs. This drift is a feature, not a bug.

**The Reintegration Cycle:**
1. **Clone** — Start from protocol-duo template
2. **Initialize** — Customize for project needs (one-way door)
3. **Drift** — Evolve based on real-world usage
4. **Reintegrate** — Contribute learnings back to master protocol
5. **Redistribute** — Improved protocol benefits all future clones

Each repo's learnings strengthen the collective. When you discover patterns that work well, contribute them back.

**Upstream innovations:** If this project has evolved the protocol in useful ways (new commands, anti-patterns, workflow improvements), the user can submit an innovation report to [kayg.ee/protocol/upstream](https://kayg.ee/protocol/upstream). See `CONTRIBUTING.md` for details.

**Important:** Always ask the user before preparing or submitting an innovation report. Never auto-report.

### Scope Modifiers

| Modifier | Scope | Purpose |
|----------|-------|---------|
| `..architect` | Full | Load all project docs, decisions, and history |
| `..builder` | Lean | Load essentials only — focus on executing |

### Operational Commands

| Command | Purpose |
|---------|---------|
| `..start` | Load full context, show priorities |
| `..make` | Design a feature, write specs |
| `..hygiene` | Archive old content, prune files |
| `..recover` | Emergency recovery from crashes |

See `ROLE_PROTOCOL.md` for full command specifications.

### Quick Rules

1. **Every interaction is atomic** — LOAD → CLARIFY → EXECUTE → RECORD → REFLECT
2. **RECORD commits immediately** — Don't let decisions pile up uncommitted
3. **Docs are source of truth** — Update TODO, PROGRESS, DECISIONS as part of RECORD
4. **Default scope is full** — All .md files + 20 git commits loaded every session
5. **Context files stay lean** — Run `..hygiene` when files grow large
6. **Accuracy over impressiveness** — Say "I don't know" rather than guess. Clarify rather than assume.

### v1.1 Principles

| Principle | Rule |
|-----------|------|
| **Generated beats maintained** | If a file can be rebuilt from source, rebuild it. Don't patch stale context — regenerate. See [PATTERNS.md upgrade path](https://kayg.ee/protocol). |
| **Files are memory** | .md files in git are the only persistence layer. No agent memories, no session resume. (Also Hard Rule #1.) |
| **Fewer, louder rules** | Hard Rules at top override everything. The rest is guidance. |
| **Track execution, not intent** | Done = loop closed. Not "drafted." Not "I'll do it later." |
| **Name the blocker, not the person** | TASKS/ files named by what's blocked. Test: "Can I resolve this independently?" |
| **Know your command types** | Rituals (extractable as skills), Cycles (protocol-only), Generators (never extractable), Modes (behavioral switches). |
| **Scope the correction** | When giving feedback, state what should NOT change. (Also Hard Rule #5.) |

### Commit Strategy

**Micro-commits** after each logical unit of work. One feature or fix per commit.

**Format:** `[AREA] Brief description` — with optional bullet details and context below.

Customize `[AREA]` tags for your project (e.g., `[core]`, `[ui]`, `[docs]`, `[build]`).

### Trust & Integrity

Collaboration requires trust. These principles protect it:

- **Never fabricate** — Don't invent URLs, API endpoints, facts, or capabilities. Say "I'm not sure" instead.
- **Disagree honestly** — If a design is wrong or a task is unclear, say so during CLARIFY. Don't build something you know is broken.
- **Execute, don't rationalize** — When given a clear instruction, do it. Offer opinions after, not instead.
- **Clarify before assuming** — Ambiguous instruction + assumption = rework. Ask first.

---

## Environment Notes

Document tool-specific quirks and workarounds here as you discover them.

| Tool/Integration | Known Behavior | Workaround |
|------------------|----------------|------------|

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

## Task Management

duo separates AI work from human work:

| Location | Owner | Purpose |
|----------|-------|---------|
| **TODO.md** | Claude | AI tasks — work Claude does |
| **TASKS/** | Human | Tasks only a human can do |

Each file in TASKS/ is a **brief from Claude to the user** — a specific action, decision, or message that only a human can complete.

**TASKS/ Structure:**
```
TASKS/
├── README.md     # Self-documenting guide
├── TODO/         # Not started
├── PRIORITY/     # Do these next
├── BLOCKED/      # Waiting on something external
└── DONE/         # Completed (consolidated monthly)
```

**Claude's responsibilities each `..start`:**
1. Review all TASKS/ files against current context
2. Move between folders as situation changes
3. Create new task files when human action needed
4. Report status in briefing

See `TASKS_README_TEMPLATE.md` for task file format and examples.

---

## Project Structure

```
[PROJECT_NAME]/
├── CLAUDE.md           # Technical reference (this file)
├── PRFAQ.md            # Product vision (Press Release + FAQ)
├── TODO.md             # Claude's tasks (AI work)
├── TASKS/              # Human tasks (only a human can do)
│   ├── README.md       # Self-documenting guide
│   ├── TODO/           # Not started
│   ├── PRIORITY/       # Do these next
│   ├── BLOCKED/        # Waiting on something
│   └── DONE/           # Completed
├── PROGRESS.md         # Session-by-session log
├── DECISIONS.md        # Architecture Decision Records
├── PRINCIPLES.md       # Emerges from ADRs (populated by ..hygiene)
├── CONSTRAINTS.md      # Design system, rejected approaches
├── ROLE_PROTOCOL.md    # AI workflow commands
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
| `DECISIONS.md` | Architecture Decision Records |
| `PRINCIPLES.md` | Distilled from ADRs — populated by `..hygiene` |
| `CONSTRAINTS.md` | Design system, rejected approaches |
| `TODO.md` | Claude's tasks (AI work) |
| `TASKS/` | Human tasks (only a human can do) |
| `PROGRESS.md` | Session-by-session development log |
| `ROLE_PROTOCOL.md` | AI workflow commands |
| `README.md` | User/setup documentation |

---

*Last updated: [DATE]*
*Status: [STATUS]*
