# duo — Collaborate Protocol

**Stop explaining your project every session.** duo gives Claude persistent memory through structured documentation.

## The Problem

Claude is powerful but forgetful. Every session starts from zero. You re-explain your project, your decisions, your constraints. duo solves this.

## How It Works

1. **Create a repo from this template**
2. **Answer 5 questions** about what you're building
3. **Claude populates your docs** (PRFAQ, TODO, DECISIONS, etc.)
4. **Start building** — Claude remembers everything across sessions

## 5-Minute Demo

After creating your repo, Claude will ask:

> "What are we building? Give me the one-liner."

You say: "A CLI tool that converts screenshots to code"

Claude asks 4 more questions, then generates:
- **PRFAQ.md** — Press release describing your finished product
- **TODO.md** — Prioritized task list
- **DECISIONS.md** — Architecture choices

Now when you return next week, Claude knows your project.

## Requirements

- **Claude Code** (CLI or VS Code extension) — The onboarding flow triggers automatically when Claude reads CLAUDE.md
- **Git** — For version control of your documentation
- **Any project** — Works for code, writing, research, or planning

> **Note:** The documentation structure works with any AI, but the automatic onboarding flow is optimized for Claude Code.

### Not building code?

For doc-heavy projects without complex architecture (knowledge bases, guides, process docs), use [protocol-uno](https://github.com/marekgorski/protocol-uno) instead. It's the **uno** (Delegate) protocol — simplified for tasks where AI works FOR you without architect/builder role separation.

> **Protocol Family:** This template is part of the [KayGee Protocol Family](https://github.com/marekgorski/admin/tree/main/protocol). **uno** = Delegate, **duo** = Collaborate (this template), **tre** = Automate.

## Compatibility

| Scenario | Notes |
|----------|-------|
| **Other AIs** (GPT, Gemini, Cursor) | Structure works; onboarding flow is Claude-optimized |
| **New to Git?** | You need: `clone`, `add`, `commit`, `push` — that's it |
| **Team projects** | Everyone clones the repo; Git handles merging; PROGRESS.md tracks who did what |

## Quick Start

### 1. Create your repo from template

1. Go to [github.com/marekgorski/protocol-duo](https://github.com/marekgorski/protocol-duo)
2. Click **"Use this template"** → **"Create a new repository"**
3. Name your repo, set visibility, click **"Create repository"**

### 2. Clone and open

```bash
git clone https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git
cd YOUR_REPO_NAME
claude
```

### 3. Answer discovery questions

Claude sees the `[PLACEHOLDER]` markers and asks:
1. What are we building?
2. Who is it for?
3. What problem does it solve?
4. What does MVP success look like?
5. Any constraints?

### 4. Review and confirm

Claude reflects back understanding. Confirm or correct.

### 5. Start building

Use the workflow commands:
- `..architect` — Enter planning mode
- `..builder` — Enter implementation mode
- `..go` — Execute top task
- `..end` — Verify and close session

## File Structure

```
my-project/
├── CLAUDE.md           # Technical reference + onboarding flow
├── PRFAQ.md            # Product vision (Press Release + FAQ)
├── CONSTRAINTS.md      # Principles, design system, rejected approaches
├── TODO.md             # Prioritized task list
├── PROGRESS.md         # Session-by-session development log
├── DECISIONS.md        # Architecture Decision Records
├── WORKFLOW.md         # Development process
├── ROLE_PROTOCOL.md    # AI workflow commands
├── MAREK.md            # Human-only tasks (optional - rename to your name)
└── README.md           # This file (replace with your own)
```

**Optional file:**
- **MAREK.md** — Tasks only humans can do (recording videos, strategic decisions, external coordination). Named like adding "Tom" in MySpace. Prevents AI from spinning on work it can't complete.

## Task Ownership

Tasks in TODO.md use markers to indicate who can complete them:

| Marker | Meaning | Example |
|--------|---------|--------|
| `[C]` | Claude can complete | `[C] Write API endpoint` |
| `[M]` | Human must complete | `[M] Record demo video` |
| `[C→M]` | Claude prepares, human executes | `[C→M] Draft outreach email` |
| `[M→C]` | Human decides, Claude implements | `[M→C] Choose pricing tier` |

**No marker = `[C]`** — Tasks without markers are assumed Claude-completable.

See `ROLE_PROTOCOL.md` for the full handoff protocol.

## Commands Reference

| Command | Mode | Purpose |
|---------|------|---------|
| `..architect` | — | Enter planning mode |
| `..builder` | — | Enter implementation mode |
| `..start` | Architect | Load context, show priorities |
| `..make` | Architect | Design a feature (with acceptance criteria) |
| `..go` | Builder | Execute top task |
| `..end` | Builder | Verify, close session, update docs |
| `..recover` | Any | Emergency recovery from crash |
| `..hygiene` | Architect | Archive old content |
| `..exit` | Architect | Verify work, fossilize context |

## Philosophy

### Why Files Work

AI forgets everything between conversations. Start a new chat, and it's meeting you for the first time.

But files don't forget.

When you write what you learned in a file, AI reads it next session. When you track what's done, AI knows where you left off. When you log what didn't work, AI doesn't suggest it again.

**Your markdown files ARE the AI's memory.** That's the whole trick:

| File | What It Remembers |
|------|-------------------|
| CLAUDE.md | What this project is and how it works |
| DECISIONS.md | Why we chose this approach (so we don't re-debate) |
| TODO.md | What needs doing next |
| PROGRESS.md | What happened (so the next session knows) |

Each file solves a specific forgetting problem. Together, they give AI persistent memory.

### Why separate Architect and Builder?

- **Architect** has full context (PRFAQ, DECISIONS, etc.) for big-picture thinking
- **Builder** has lean context (CLAUDE, TODO only) for focused execution
- Prevents scope creep during implementation
- Mirrors how humans work: plan first, then execute

### Why so many markdown files?

- Claude reads these automatically
- Version-controlled documentation
- Easy to review what changed and when
- Survives across sessions (Claude has no memory otherwise)

### Why the onboarding flow?

- Ensures Claude understands the project before acting
- Prevents "helpful" assumptions that miss the mark
- Creates documentation as a byproduct

## Troubleshooting

**Claude isn't asking onboarding questions**
- Make sure you're using Claude Code (not Claude.ai web)
- Check that CLAUDE.md still has `[PLACEHOLDER]` markers
- Try explicitly saying: "Read CLAUDE.md and run the onboarding flow"

**Claude is ignoring my documentation files**
- Use `..start` command to reload context
- Check file sizes — if over 50KB, run `..hygiene`
- Make sure you're in Architect mode for planning, Builder mode for coding

**I don't know which mode to use**
- Planning, designing, deciding → `..architect`
- Building, coding, fixing → `..builder`
- When in doubt, start with `..architect`

**Something went wrong and I want to undo**
- Find your last good commit: `git log --oneline`
- Reset to it: `git reset --hard <commit-hash>`
- The "Save Game Rule" — commit before risky changes

**Still stuck?**
- Open an issue on this repo
- Check if your question is answered in WORKFLOW.md or ROLE_PROTOCOL.md

---

## License

MIT — Use freely, modify as needed.

---

## Maintenance

Protocol maintenance documentation (audits, version bumps, syncing downstream repos) lives in a separate repository.

---

*duo Protocol v1.3 — December 29, 2025*
