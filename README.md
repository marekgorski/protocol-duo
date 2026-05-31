# duo — Construct Protocol

**Version 1.3** — Construction site for building bounded things.

**Stop explaining your project every session.** duo gives Claude persistent memory through structured documentation.

> **v1.3 — Structural Discipline (2026-05-18):** The locus of discipline moves from rules+hook-enforcement to structure that makes failure modes hard to occur. Five layers move together: rule creation (case-study gate) · schema (front-matter `type/updated/summary`) · harness (hookless default) · falsification (watch public commitments) · release-candidate path. Plus protocol-vs-flavour stratification (the brewery and the recipe). New flavour-level Hard Rule for duo: *Docs travel with code* (convergent invention in 2 production repos). See [kayg.ee/learn/structural-discipline](https://kayg.ee/learn/structural-discipline) for the full articulation.

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

For doc-heavy projects without complex architecture (knowledge bases, guides, process docs), use [protocol-uno](https://github.com/marekgorski/protocol-uno) instead. It's the **uno** (Operate) protocol — an OS for managing X (ongoing substrate, not a bounded build).

> **Protocol Family:** This template is part of the [KayGee Protocol Family](https://kayg.ee/protocol). **uno** = Operate (an ale — top-fermented, monolithic, OS-spec shape), **duo** = Construct (a lager — bottom-fermented, split docs, ADR-shaped — this template), **tre** = Automate (planned). Same brewery; different recipes.

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

### Recommended: `..wrap`

Use `..wrap` as a periodic deep close — after a session that did substantial work, introduced decisions, or corrected earlier claims. It compounds learnings into permanent homes, fences failures, reconciles tasks, and ends with `..cs`.

See [ROLE_PROTOCOL.md](ROLE_PROTOCOL.md) for the full `..wrap` prompt text. For a keyboard-expander paste, see the prompts below.

**Full version** (for Espanso / Raycast / TextExpander, or paste at session end):

```
You are the steward of this repo's memory, closing out a session that did real work. The repo already holds most of what matters — principles, constraints, decisions, tasks — and your job is to make this session's work compound into it, not pile up beside it. So your habit is to read before you write: before you add anything, you open the file it belongs in and check what's already there. The thing you are fighting is the near-duplicate — a fresh entry that says almost what an existing one already says. When you find the entry that covers the ground, you sharpen it instead of adding a rival. Everything you record lives in a repo file the next session will load — never in tool or agent memory, which doesn't travel in git. And you don't trust a claim until the file shows it: the files are the memory; if a change isn't in them, it didn't happen. Any pass below can come up empty — say so plainly and move on; never manufacture an entry to fill a section.

Work through the session in this order.

Start with what you learned. Take each learning and go find where it already lives — the principles home (PRINCIPLES.md, or the Principles section of CLAUDE.md), the constraints home (CONSTRAINTS.md, or the Constraints section of CLAUDE.md), the decisions log (DECISIONS.md, if this repo keeps one), or wherever this repo keeps such notes (e.g. a LEARNINGS file). Read what is already there before you touch it. If an entry covers the ground, merge your learning in and leave it sharper. Write a new entry only once you've looked and nothing fits. While you're in each home, check whether a decision this session made has left an earlier claim now false — if so, correct that claim in every current-state place it appears (leave append-only logs alone). Note where each change went.

Next, account for what went wrong. List what the session got wrong, redid, or corrected. For each, check whether an existing rule or constraint already speaks to it — if so, tighten that one; if not, write the fence that stops it recurring, into a repo file. Prevent at the input what you'd otherwise keep catching at the output. A failure you can't fence is the most important thing to surface.

Next, reconcile the work. Check each task you closed against its full acceptance criteria; if anything shipped short, capture the remainder as a narrower task before removing the original. Write down any open item that won't resurface on its own next session. File handoffs where the right party will find them — work a human must action in TASKS/, finished human work in TASKS/DONE/.

Next, look at the shape of the repo. Scan the git log (ignore routine auto-save commits) for a theme worked hard across recent sessions worth promoting to a permanent home, or a file untouched for many sessions worth retiring. Name one, or say plainly there's nothing this time.

Then close and prove it landed — this is the last step, in this order. Run ..cs to fossilise and commit. THEN open the committed files and confirm every change from every pass above — including the close's own commit — is actually present, and git status is clean; fix and re-commit anything that didn't land. If the commit can't complete in this environment, say so plainly and name exactly what's left uncommitted. If this repo runs a generated STATE.md or a capped TASKS/PRIORITY/, check they're within limits and drain any overflow. A claim is not done until the file shows it. State the safe-to-close verdict, verified by command not memory — working tree clean, no stashes, and whether local main is ahead of origin. Separate committed-and-pushed from committed-local-only (kept on a normal close; lost only if this machine is wiped before a push) from anything uncommitted. Do not push if this repo gates pushes or deploys behind a human — report the unpushed state and let the human decide (offer a non-deploying backup branch if useful). Then name anything that lived only in this conversation and was deliberately not written to a file; offer to persist it in one line or let the human release it — what isn't in a file won't survive the close.
```

**Short version** (native Text Replacement — keeps the spine, trades away durability nuances):

```
you're the steward of this repo's memory, closing a session that did real work, so make it compound into the files, not pile up beside them. read before you write: open the file a thing belongs in, and when an entry already covers the ground, sharpen it instead of adding a near-duplicate. everything lives in a repo file the next session loads, never in tool or agent memory. a claim isn't true until the file shows it. any pass can come up empty, so say so plainly, and never manufacture an entry to fill a section. work in order. first, take each learning and find where it already lives (principles, constraints, decisions, or a learnings file), read what's there, merge it in, then correct any earlier claim this session made false, leaving append-only logs alone. next, list what the session got wrong or redid, and for each either tighten an existing rule or write the fence that stops it recurring, preventing at the input what you'd keep catching at the output. next, check each closed task against its full acceptance criteria, capturing any shortfall as a narrower task before removing the original, and file handoffs where the right party finds them: work a human must action in the TASKS folder, finished work in its DONE subfolder. next, scan the git log (ignoring auto-save commits) for a theme worth promoting or a file worth retiring. name one or say there's nothing. finally, run ..cs to commit, reopen the committed files to confirm every change landed and re-commit anything that didn't, and drain any overflow if a generated STATE.md or capped PRIORITY folder runs over. then state the safe-to-close verdict by command not memory: working tree clean, no stashes, and committed-and-pushed vs committed-but-local-only vs uncommitted.
```

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

These files cost tokens. Without them, you spend 30%+ re-explaining what you already know. You're trading a small, controllable slice of context for a reliable memory. After two or three sessions, you're way ahead.

### The Architect and Builder metaphor

**Architect** designs the thing, gets sign-off, and records the decisions. **Builder** executes. Claude Code's native plan mode handles the architect role: design, present a plan, get approval, then build. The protocol's job is to ensure the approved plan persists — acceptance criteria to `TODO.md`, architectural decisions to `DECISIONS.md` — so the builder phase has a real contract to work from.

### Why so many markdown files?

- Small, focused files cost fewer tokens than one giant file
- Version-controlled — roll back bad decisions like you would code
- Each file answers a specific question; together they give AI persistent memory of your project

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

**Something went wrong and I want to undo**
- Find your last good commit: `git log --oneline`
- Reset to it: `git reset --hard <commit-hash>`
- The "Save Game Rule" — commit before risky changes

**Still stuck?**
- Open an issue on this repo
- Check if your question is answered in ROLE_PROTOCOL.md

---

## Graduation: From Jet Ski to Direct Intent

Most people start by building "jet skis" — exploring what AI can do, shipping side projects, learning where the compound effect kicks in. That's what this template is for. The files (TODO.md, DECISIONS.md, TASKS/) handle the day-to-day.

At some point, you'll stop asking "what can I build?" and start asking "what should I build and why?" That's the graduation signal.

When you're ready, add `INITIATIVES.md` to your project root — a strategic layer that sits above the existing files:

| Level | What | Files | When |
|-------|------|-------|------|
| **1. Initiative Tracker** | Why, what, who, when | INITIATIVES.md | After you've shipped something real |
| 2. Phase Tracker | Progress, priorities | TODO.md + TASKS/ | Day 1 |
| 3. Architecture | Decisions, constraints | DECISIONS.md + CLAUDE.md | Day 1 |
| 4. Daily Work | Tasks, commits | TASKS/ + git | Day 1 |

The Level 1 template asks 6 questions per initiative: **Why**, **Which Models**, **What Revenue**, **How to Measure**, **Who's Building**, **When** (milestones + biggest risk).

Don't add it on day one — it's a roof, not a foundation. Build first, direct later.

**Learn more:** [The 4 Levels](https://kayg.ee/learn/levels) — full guide with working example.

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

## Changelog

- **v1.3.1** (May 31, 2026): Plan Persistence + Deep Close
  - Architect/Builder scope commands retired — Claude Code's native plan mode handles the plan→build handoff natively. The protocol's job is now to persist the approved plan: acceptance criteria → `TODO.md`, architectural decisions → `DECISIONS.md`.
  - New command: `..wrap` — periodic deep close that compounds learnings, fences failures, reconciles tasks, and verifies the repo before ending with `..cs`
  - `..wrap` ships as two artifacts: full v2.1 (for keyboard expanders or paste-at-session-end) and a short ASCII spine variant (for native Text Replacement)
  - Removed `lean_mode` setting and scope machinery (replaced by the tier-based context loading model)

- **v1.3** (May 18, 2026): Structural Discipline
  - Theme: locus of discipline moves from rules+hook-enforcement → structure that makes failure modes hard to occur
  - New Hard Rule #6: Case-study gate at rule-creation (every new rule cites a case study AND a level designation)
  - New Flavour-Specific Rules section with first entry: *D1. Docs travel with code* (after a code change, commit the matching doc update in the same push) — convergent invention in 2 production repos (two production deployments verbatim)
  - Front-matter schema migrated to `type/updated/summary` with 60-day compat shim (2026-05-18 → 2026-07-17)
  - Hookless `{ "hooks": {} }` becomes canonical default; simplified Stop hook is opt-in
  - Anti-pattern table format adds Case Study column (Hard Rule #6 enforcement)
  - New anti-pattern: "Celebrating a primitive by over-implementing it" (case study: v1.2 hook deployment → v1.3 hookless retirement, ~10 weeks)
  - Protocol-vs-flavour stratification codified (the brewery and the recipe — duo is the lager; uno is the ale)
  - Public articulation: kayg.ee/learn/structural-discipline (live 2026-05-17 ahead of canonical)
  - Deferred for v1.3.1+: convergence/accretion ratio (Item 6, baseline 2026-06-30), mandatory front-matter (Item 9, paired with schema), /goal as Hard Rule (Item 10, testing window through 2026-06-15), PROGRESS rolling cadence (Item 11), anti-pattern table consolidation (Item 12)

- **v1.2.2** (May 10, 2026): Coaching Philosophy
  - Stop hook simplified — catches uncommitted changes only; PROGRESS/TODO/DECISIONS diff policing removed
  - Coaching framing: hooks coach the playbook (remind, catch drift); they don't enforce or punish
  - Hard Rule #3 scoped to substantive interactions — quick read-only checks don't require RECORD entries
  - Two new anti-patterns: hooks as taskmasters; concurrent sessions without isolation
  - Production evidence: 29 days clean on a simplified hook in one production deployment; another ran hookless cleanly

- **v1.2.1** (Apr 6, 2026): Hook Architecture Fix
  - SessionStart hook: records session HEAD, enforces boot sequence via `additionalContext`
  - PreToolUse widened: blocks all `~/.claude/` writes, not just two subdirectories
  - Stop hook redesigned: read-only sessions pass silently, checks committed + pending + staged changes
  - Command simplification: `..ss`/`..start` removed (hook does boot), `..gm` promoted to universal status briefing

- **v1.2** (Apr 5, 2026): Structure That Earns Trust
  - Two new principles: #9 (Structure Is the Owner), #10 (Build the Fence, Not the Net)
  - ESSENCE.md: per-repo voice identity file with four minimum sections
  - Harness layer: `.claude/settings.json` ships in canonical with PreToolUse + Stop hooks
  - Protocol/harness split: .md files = protocol (portable), .claude/ = harness (CC enforcement)

- **v1.1** (Mar 26, 2026): Eight Principles From 90 Days
  - Eight principles extracted from 90 days of production use — each earned by evidence
  - Hard Rules hierarchy: inviolable rules at top of CLAUDE.md
  - Voice initialization: first-boot calibration for documentation tone, UI copy, commit style
  - Command type classification: Rituals, Cycles, Generators, Modes
  - Backwards compatible with v1.0
  - Downstream versioning convention: v{canonical}{letter} (e.g., v1.1a)

- **v1.0** (Jan 25, 2026): Official release of protocol-duo
  - Architect/Builder conceptual model for plan→build workflow
  - Commands: `..start`, `..make`, `..hygiene`, `..recover`
  - File patterns: PRFAQ.md, DECISIONS.md, TODO.md, PROGRESS.md, CONSTRAINTS.md
  - Task ownership: TODO.md (AI work), TASKS/ folder (human work)
  - Trust & Integrity principles

---

*duo Protocol v1.3.1 — May 31, 2026*
