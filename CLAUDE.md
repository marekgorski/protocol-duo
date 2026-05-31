# CLAUDE.md

## Hard Rules — Override Everything, No Exceptions

> **All Hard Rules below are protocol-level** (apply across every flavour in the kaygee family — uno, duo, tre). Flavour-level rules specific to duo (Construct) live in the *"Flavour-Specific Rules"* section below. See the kaygee protocol family overview at [kayg.ee/protocol](https://kayg.ee/protocol) for the brewery-and-recipe stratification (v1.3, 2026-05-18).

1. **Files are memory.** Everything in .md files committed to git. No tool-specific persistence (agent memories, session resume). If it's not in a file, it doesn't exist.
2. **Never fabricate.** Accuracy over impressiveness. Don't invent URLs, API endpoints, facts, or capabilities. Say "I'm not sure" instead.
3. **RECORD after every substantive interaction.** Update files and commit when work produces changes worth capturing. Quick read-only checks and context loads do not require RECORD entries. Don't batch substantive work at session end. This is the compound effect.
4. **Pre-scan before changes, post-scan after.** Check all references before modifying. Verify 0 stale references after.
5. **Scope the correction.** When the user gives feedback, change ONLY what was asked. Don't expand scope. State what should NOT change if unclear.
6. **Case-study gate at rule-creation (v1.3).** Every new rule, Hard Rule clause, anti-pattern row, or extension block must cite both a **case study** (a date-stamped incident, a numbered principle reference, or a named worked example) AND a **level designation** (protocol-level or flavour-level). Rules without both are deletion candidates at the next audit. Applies to new rules from 2026-05-18 forward; existing rules are not retroactively gated.

---

## Flavour-Specific Rules

Hard Rules below this line apply because you chose the **duo (Construct)** flavour — they're the recipe, not the brewery.

### D1. Docs travel with code (v1.3 — flavour-level Hard Rule for duo only)

After any code change, commit the matching documentation update in the same push. If the code change is small enough that no doc update is needed, the commit message MUST state so explicitly (e.g., "no doc impact").

**Why this is flavour-level:** duo is the Construct flavour — building bounded things with code. The temporal coupling between code change and doc change is specific to construction work. uno (Operate) is doc-only substrate; tre (Automate) is multi-party orchestration where code↔doc coupling doesn't carry the same load.

**What "matching documentation" means in duo:**
- New feature → PRFAQ.md or DECISIONS.md entry + relevant ROLE_PROTOCOL.md update if commands change
- Bug fix → TODO.md entry marked done + PROGRESS.md note if user-facing
- Refactor → DECISIONS.md if architecture-affecting; otherwise commit-message-only is acceptable
- Dependency bump → CHANGELOG.md or equivalent

**Case study:** Convergent invention May 2026 — two production deployments independently codified the verbatim wording *"After a code change, commit the matching doc update in the same push."* Two-repo convergence with identical phrasing meets the case-study gate (Hard Rule #6) at the flavour level.

---

Technical reference for Claude Code when working on this project.

**Workflow commands:** When user types any `..command`, read and follow [ROLE_PROTOCOL.md](./ROLE_PROTOCOL.md).

### Boot Sequence (runs every session start)

**On ANY first interaction** — whether "hello", "let's start", or a paragraph of instructions — execute this boot sequence before responding:

1. **Read ALL `.md` files** in the project root (including ESSENCE.md)
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

**Step 3: Voice Identity**

After confirming understanding, discover the project's voice influences. These seed the ESSENCE.md file — the three-influence model that shapes how AI-generated content sounds.

Ask these one at a time, conversationally:

1. **Structure Influence**
   > "Who writes and structures information in a way you admire? Someone whose writing makes complex things feel organized."

2. **Clarity Influence**
   > "Who writes in a way that creates clarity from information — makes obvious things obvious, reframes what everyone already knows?"

3. **Voice Influence**
   > "Who speaks in a way you admire their speaking? Someone whose tone or delivery you'd want this project to echo."

After answers, populate ESSENCE.md with the three influences and initial craft rules derived from them. Mark as `Phase: Configured`.

**Step 4: Voice Calibration**

Now calibrate the specifics. This refines how the voice influences apply to all content the AI produces — documentation, UI copy, user-facing text, commit messages, PR descriptions.

Ask these as choices:

1. **Documentation Tone**
   > "How should docs and README files sound?
   > - A: Technical and precise (assume expertise)
   > - B: Conversational but thorough (explain context)
   > - C: Minimal (just enough to get started)
   > - Or describe the tone you want."

2. **UI Copy Style**
   > "For user-facing text (error messages, labels, empty states):
   > - A: Friendly and helpful ('Oops! No items yet. Add one to get started.')
   > - B: Clean and neutral ('No items found.')
   > - C: Technical and direct ('Empty collection. Use POST /items to add.')"

3. **Commit/PR Voice**
   > "For commit messages and PR descriptions:
   > - A: Descriptive ('Add user authentication with JWT tokens and refresh flow')
   > - B: Conventional commits ('feat(auth): add JWT authentication')
   > - C: Minimal ('add auth')"

Store results in this file under `## Project Voice` (below the Project Overview section). Mark as `Phase: Configured`. After ~30 days of corrections, regenerate from accumulated evidence.

**Step 5: Populate Docs**

Once user confirms, update these files with real content:
- `PRFAQ.md` — Write press release and FAQs
- `DECISIONS.md` — Document initial architecture choices
- `TODO.md` — Create prioritized task list
- `ESSENCE.md` — Populate with voice influences from Step 3
   - `CLAUDE.md` — Replace this section with project-specific technical reference
- `README.md` — Replace template README with project-specific description
- `PROGRESS.md` — Fill in the initialization session entry with actual details

Remove all `[PLACEHOLDER]` markers when done.

**Step 6: Confirm Ready**

```
"Project initialized! Here's what I've set up:
- ESSENCE.md: [voice identity seeded]
- PRFAQ.md: [brief summary]
- DECISIONS.md: [key decisions]
- TODO.md: [top priorities]
- CLAUDE.md: [project overview]
- README.md: [project description]
- PROGRESS.md: [initialization session logged]

Use `..gm` for a status briefing. Full context loaded automatically by hook.
Use `..cs` to close a session. Context fossilised before ending.
Use `..wrap` for a periodic deep close after a substantial session.

What would you like to tackle first?"
```

**Step 7: Commit & Push**

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

**Fossilisation is automatic.** The RECORD step commits decisions and context after every substantive interaction. No ceremony required at session end.

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

### Operational Commands

| Command | Purpose |
|---------|---------|
| `..gm` | **Status briefing** — Priorities, blockers, task status (on demand) |
| `..cs` | **Close session** — Fossilize context: update TODO.md, PROGRESS.md, DECISIONS.md, commit |
| `..wrap` | **Deep close** — Periodic deep close: compound learnings, fence failures, reconcile tasks, verify. Ends with `..cs`. |
| `..make` | Design a feature, write specs |
| `..hygiene` | Archive old content, prune files |
| `..recover` | Emergency recovery from crashes |

Boot sequence runs automatically via SessionStart hook — no manual start command needed. `..gm` is on-demand ("brief me"). See `ROLE_PROTOCOL.md` for full command specifications.

### Quick Rules

1. **Every interaction is atomic** — LOAD → CLARIFY → EXECUTE → RECORD → REFLECT
2. **RECORD commits immediately** — Don't let decisions pile up uncommitted
3. **Docs are source of truth** — Update TODO, PROGRESS, DECISIONS as part of RECORD
4. **Default scope is full** — All .md files + 20 git commits loaded every session
5. **Context files stay lean** — Run `..hygiene` when files grow large
6. **Accuracy over impressiveness** — Say "I don't know" rather than guess. Clarify rather than assume.

### v1.2 Principles

| Principle | Rule |
|-----------|------|
| **Generated beats maintained** | If a file can be rebuilt from source, rebuild it. Don't patch stale context — regenerate. See [PATTERNS.md upgrade path](https://kayg.ee/protocol). |
| **Files are memory** | .md files in git are the only persistence layer. No agent memories, no session resume. (Also Hard Rule #1.) |
| **Fewer, louder rules** | Hard Rules at top override everything. The rest is guidance. |
| **Track execution, not intent** | Done = loop closed. Not "drafted." Not "I'll do it later." |
| **Name the blocker, not the person** | TASKS/ files named by what's blocked. Test: "Can I resolve this independently?" |
| **Know your command types** | Rituals (extractable as skills), Cycles (protocol-only), Generators (never extractable), Modes (behavioral switches). |
| **Scope the correction** | When giving feedback, state what should NOT change. (Also Hard Rule #5.) |
| **Seed the voice, grow the style** | Initialize voice at first boot via calibration questions. Refine from corrections. Regenerate from evidence at ~30 days. The seed accelerates — it doesn't replace 90 days of learning. |
| **Structure is the owner** | If you have to ask who owns it, the structure is wrong. Structure encodes three things: who acts (file location), when it's done (acceptance criteria at planning time), and who verifies (criteria exist before work starts). |
| **Build the fence, not the net** | Prevent at the input what you'd otherwise catch at the output. Fences (Hard Rules, CONSTRAINTS.md, hooks) prevent bad output. Nets (review checklists) catch it after. Design fences first. |

### Harness (Claude Code)

This repo ships hookless by default (v1.3, 2026-05-18). `.claude/settings.json` carries `{ "hooks": {} }` — the playbook (these .md files) does the protocol work; the harness stays out of the way.

**Why hookless:** v1.2 shipped 3 hooks (SessionStart, PreToolUse, Stop) to all canonical repos. Two independent reports found per-interaction policing harmful (overhead > value). v1.2.2 simplified to a Stop-on-uncommitted-changes coach. v1.3 retires hooks as canonical default — a production deployment ran hookless cleanly through April–May 2026, proving the protocol works without them. The case-study gate (Hard Rule #6) now prevents future "celebrate the primitive by binding every lifecycle moment" failure modes.

**Opt-in: simplified Stop hook.** If you want a commit nudge on session end, see the kaygee protocol family at [kayg.ee/protocol](https://kayg.ee/protocol) for the opt-in pattern documentation. The minimal binding: a Stop hook that blocks on uncommitted changes only. Don't bind SessionStart or PreToolUse unless you can name a specific protocol gap they fill.

### Anti-Patterns

> **Case Study column** added v1.3 (2026-05-18) per Hard Rule #6 case-study gate. New rows from 2026-05-18 forward require a date-stamped case study at row-creation moment.

| Anti-Pattern | Consequence | Prevention | Case Study |
|--------------|-------------|------------|------------|
| Hooks as taskmasters | Per-interaction policing creates overhead exceeding value. Punishment causes resistance. | Hooks coach (remind, catch drift). They don't punish. v1.3 retired hooks as canonical default — see Harness section. | 2026-04 two independent deployment reports → V1.2.2 simplified (2026-05-10) → v1.3 hookless (2026-05-18) |
| Concurrent sessions without isolation | One session's writes block another session's Stop hook. | Designate one session read-only, or use `isolation: "worktree"` for write-capable subagents. | 2026-04-25 worktree boundary matrix codification |
| **Celebrating a primitive by over-implementing it** (v1.3) | A new harness primitive ships → reflex is to bind every available lifecycle moment. Half the bindings stop getting used; the other half police every interaction. | Apply the case-study gate (Hard Rule #6) before binding any new harness primitive: name the protocol gap the binding fills. If you can't name the gap, don't bind it. | 2026-03 v1.2 hook deployment to all 10 repos (3 hooks bound; 6 lifecycle slots eventually used). Two independent reports found hooks-as-taskmasters failure mode. v1.2.2 simplified the surface (2026-05-10); v1.3 retired hooks as canonical default (2026-05-18). ~10 weeks celebration → correction. |

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

**Claude's responsibilities each session:**
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
├── ESSENCE.md          # Voice identity (three influences, traits, anti-patterns)
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
