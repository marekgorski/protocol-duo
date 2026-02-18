# duo — Collaborate Protocol

**Version 1.0** — AI works WITH you.

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

> **Protocol Family:** This template is part of the [KayGee Protocol Family](https://kayg.ee/protocol). **uno** = Delegate, **duo** = Collaborate (this template), **tre** = Automate.

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

Start building. Claude handles context automatically.

Optional scope overrides:
- `..architect` — Expands context (loads PRFAQ, DECISIONS, CONSTRAINTS — the full picture)
- `..builder` — Keeps context lean (CLAUDE.md + TODO.md only — focused execution)

These are optional. The protocol works without them.

## File Structure

```
my-project/
├── CLAUDE.md           # Technical reference + onboarding flow
├── PRFAQ.md            # Product vision (Press Release + FAQ)
├── PRINCIPLES.md       # Distilled wisdom from ADRs (<2 min read)
├── CONSTRAINTS.md      # Principles, design system, rejected approaches
├── TODO.md             # Prioritized task list
├── PROGRESS.md         # Session-by-session development log
├── DECISIONS.md        # Architecture Decision Records
├── ROLE_PROTOCOL.md    # AI workflow commands
├── TASKS/              # Human-only tasks (folder-based)
└── README.md           # This file (replace with your own)
```

**TASKS/ folder:**
- Tasks only humans can do (recording videos, strategic decisions, external coordination)
- See [TASKS_README_TEMPLATE.md](TASKS_README_TEMPLATE.md) for the full TASKS/ vs TODO.md explanation

## Task Ownership

Location encodes ownership — no markers needed:

| Location | Owner | Purpose |
|----------|-------|---------|
| **TODO.md** | Claude | AI tasks — work Claude does |
| **TASKS/** | Human | Tasks only a human can do |

Handoffs flow naturally: Claude creates deliverables and adds task files in `TASKS/` for human execution. Humans add outcomes to task files in `TASKS/DONE/` and Claude picks up dependent work.

See `ROLE_PROTOCOL.md` for the full handoff protocol.

## Commands

See [ROLE_PROTOCOL.md](ROLE_PROTOCOL.md) for the full command reference.

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

### The Token Trade

These files cost tokens. How much depends on your scope — `..architect` loads everything, `..builder` loads lean. But without them, you spend 30%+ re-explaining what you already know. You're trading a small, controllable slice of context for a reliable memory. After two or three sessions, you're way ahead. The lever: more context = more accurate but higher cost. Scope modifiers let you control this tradeoff.

### Why separate Architect and Builder?

Architect and Builder are **scopes** that control how much context loads:

- **Architect** loads everything (PRFAQ, DECISIONS, CONSTRAINTS, etc.) for when you need the big picture
- **Builder** loads lean (CLAUDE.md + TODO.md) for focused execution

Architect can do everything Builder does — Builder is just cheaper and faster. You control the tradeoff between context cost and focus.

### Why so many markdown files?

- Small, focused files cost fewer tokens than one giant file
- Different scopes load different files — Builder skips PRFAQ, Architect skips implementation detail
- Version-controlled — roll back bad decisions like you would code
- The token trade stays efficient because you only load what you need

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

**Not sure which scope?**
- Start with `..architect` for planning — it loads the full picture
- Use `..builder` when you're heads-down on a specific task and don't need the big picture

**Something went wrong and I want to undo**
- Find your last good commit: `git log --oneline`
- Reset to it: `git reset --hard <commit-hash>`
- The "Save Game Rule" — commit before risky changes

**Still stuck?**
- Open an issue on this repo
- Check if your question is answered in ROLE_PROTOCOL.md

---

## Contributing

Evolved the protocol? We'd love to hear about it. See [CONTRIBUTING.md](CONTRIBUTING.md) or submit to [kayg.ee/protocol/upstream](https://kayg.ee/protocol/upstream).

---

## License

MIT — Use freely, modify as needed.

---

## Maintenance

Protocol maintenance documentation (audits, version bumps, syncing downstream repos) lives in a separate repository.

---

*duo Protocol v1*
