# duo AI Workflow Protocol (v1.3)

## Changelog
- **v1.3** (Dec 29, 2025): Added multi-tool handoffs, conversational guidance, GitHub Template setup
- **v1.2** (Dec 28, 2025): Added task ownership markers, human/AI handoff system, token budget awareness, context drift check, recovery levels
- **v1.1** (Dec 28, 2025): Added verification steps, acceptance criteria requirements, `..recover` command
- **v1.0** (Dec 2024): Initial protocol

## Workflow Summary

| Workflow | Commands |
|----------|----------|
| **Design** | `..architect` → `..start` → `..make` → `..exit` |
| **Build** | `..builder` → `..go` → `..end` |
| **Maintenance** | `..architect` → `..hygiene` → `..exit` |
| **Recovery** | `..recover` (Any role) |

---

## Task Ownership Markers

Tasks in TODO.md use markers to indicate who can complete them:

| Marker | Meaning | Example |
|--------|---------|---------|
| `[C]` | Claude can complete | `[C] Write landing page spec` |
| `[M]` | Marek must complete | `[M] Record 2-min video` |
| `[C→M]` | Claude prepares, Marek executes | `[C→M] Draft outreach email` |
| `[M→C]` | Marek decides, Claude implements | `[M→C] Choose workshop city` |

**No marker = `[C]`** — Tasks without markers are assumed Claude-completable.

### TODO.md Format with Markers

```markdown
## 🔴 High Priority

- [ ] [C] Implement user authentication
  - AC: Login returns JWT token
  - AC: Logout invalidates session

- [ ] [M] Record product demo video
  - AC: 2-min walkthrough uploaded to YouTube
  - AC: URL provided in MAREK.md
  - Blocks: VideoWalkthrough.tsx

- [ ] [C→M] Draft investor outreach email
  - AC: Draft in /drafts/investor-email.md
  - AC: Marek reviews and sends

- [ ] [M→C] Decide on pricing tier structure
  - AC: Decision documented in MAREK.md
  - AC: Claude implements pricing page after decision
```

---

## MAREK.md Structure

Human-only tasks live in MAREK.md, organized by status:

```markdown
# MAREK.md - Human Tasks

## ⏸️ Blocked (needs Marek action)
- [ ] [M] Record video → blocks VideoWalkthrough.tsx
- [ ] [M] Approve outreach email → blocks sending

## ✅ Ready for Marek (Claude prepared)
- [ ] [C→M] Outreach email drafted → /drafts/anthropic-outreach.md
- [ ] [C→M] Webinar script written → /drafts/webinar-script.md

## ❓ Waiting on Marek Decision
- [ ] [M→C] Which repo to link for protocol template?
- [ ] [M→C] Final workshop pricing?

## ✅ Completed
- [x] [M] Initial repo setup — Dec 15, 2024
```

---

## Handoff Protocol

### Claude completing [C→M] task

1. Create deliverable in `/drafts/` folder (or appropriate location)
2. Move task from TODO.md to MAREK.md "Ready for Marek" section
3. Note in PROGRESS.md: "Drafted X, awaiting Marek review"
4. Update TODO.md: Remove task, add note about where draft lives

**Example:**
```
Completed [C→M] task: Draft investor email

- Created: /drafts/investor-email.md
- Moved to: MAREK.md "Ready for Marek"
- Logged in: PROGRESS.md

Marek: Review draft and send when ready.
```

### Marek completing [M] task

1. Mark complete in MAREK.md with output (URL, decision, file path)
2. Claude checks MAREK.md on next `..builder` or `..go`
3. Claude unblocks dependent `[C]` tasks and moves to "Ready"
4. Claude logs in PROGRESS.md

**Example in MAREK.md:**
```markdown
## ✅ Completed
- [x] [M] Record demo video — Dec 28, 2025
  - Output: https://youtube.com/watch?v=abc123
  - Unblocks: VideoWalkthrough.tsx
```

### Marek making [M→C] decision

1. Add decision to MAREK.md "Completed" section
2. Claude picks up on next session
3. Claude implements and moves to TODO.md "Done"
4. Claude logs decision rationale in DECISIONS.md if significant

**Example:**
```markdown
## ✅ Completed
- [x] [M→C] Workshop pricing — Dec 28, 2025
  - Decision: €299 early bird, €399 regular
  - Rationale: Competitive with similar workshops
```

---

## Role Definitions

### ..architect

**System Initialization:**
1. **Identity:** You are the ARCHITECT. Goal: System Design, Strategy, Planning.
2. **Context Scope:** FULL (PRFAQ, CONSTRAINTS, DECISIONS, CLAUDE, TODO, PROGRESS, MAREK).
3. **Allowed Commands:** `..start`, `..make`, `..hygiene`, `..exit`
4. **Forbidden:** Do NOT write implementation code. Do NOT run build commands.
5. **Acknowledge:** "🏗️ ARCHITECT MODE ACTIVE. Ready to plan. (~15% token budget loaded)"

### ..builder

**System Initialization:**
1. **Identity:** You are the BUILDER. Goal: Implementation & Execution.
2. **Context Scope:** LEAN (CLAUDE, TODO, MAREK only). Skip PRFAQ, CONSTRAINTS, PROGRESS.
3. **Safety Check:** Run `git status`. If dirty: STOP. "⚠️ Uncommitted changes detected. Commit or stash first."
4. **Allowed Commands:** `..go`, `..end`, `..recover`
5. **Forbidden:** Do NOT question architecture. Do NOT re-plan features.
6. **Acknowledge:** "🔨 BUILDER MODE ACTIVE. Ready to build. (~5% token budget loaded)"

---

## Operational Commands

### ..start

**Session Bootloader (Architect Only)**

**Step 1: Role Verification**
- IF Role != ARCHITECT: Reply: "⛔ **Builder Optimization:** Builders should skip `..start` and run `..go` directly to save tokens."

**Step 2: Context Loading**
- Read: PRFAQ, CONSTRAINTS, DECISIONS, CLAUDE, TODO, PROGRESS, MAREK.

**Step 3: Status Report**
- Report top `[C]` task from TODO.md (including acceptance criteria).
- Note any `[M]` tasks completed in MAREK.md that unblock work.
- Flag stale `[M]` tasks (>7 days no progress).
- Wait for `..make` or `..hygiene`.

**Step 4: Task Analysis**
- Identify `[M]` tasks that could become `[C→M]` (Claude can prepare something)
- Suggest task splits if `[M]` task has Claude-doable subcomponents

---

### ..make

**Design Protocol (Architect Only)**

**Step 1: Permission Check**
- IF Role != ARCHITECT: Stop. Reply: "⛔ Permission Denied. Run `..architect` first."

**Step 2: Intent Confirmation**
- User provides 1-2 sentence feature goal.
- Confirm understanding before proceeding.

**Step 3: Design Phase**
- Review CONSTRAINTS.md for rejected approaches.
- Review DECISIONS.md for existing patterns.
- Design: data changes, UI flows, integrations.

**Step 4: Task Ownership Assignment**
- For each task, determine marker:
  - Can Claude complete entirely? → `[C]`
  - Requires human action? → `[M]`
  - Claude can prepare, human executes? → `[C→M]`
  - Human decides, Claude implements? → `[M→C]`

**Step 5: Output Protocol (MANDATORY)**
- **Write directly to files:**
  - DECISIONS.md: Add/update ADR
  - TODO.md: Add `[C]` and `[M→C]` tasks with AC
  - MAREK.md: Add `[M]` and `[C→M]` tasks
- **TODO format required:**
  ```
  - [ ] [C] Task description
    - AC: Specific testable condition
  ```
- **Final Reply:**
  > "✅ Spec written.
  > 📄 `DECISIONS.md`: ADR-XXX added
  > 📋 `TODO.md`: [X] Claude tasks added
  > 👤 `MAREK.md`: [Y] human tasks added
  >
  > Builder can run `..go` for Claude tasks."

---

### ..go

**Implementation Protocol (Builder Only)**

**Step 1: Permission Check**
- IF Role != BUILDER: Stop. Reply: "⛔ Permission Denied. Run `..builder` first."

**Step 2: MAREK.md Check**
- Read MAREK.md "Completed" section
- If completed `[M]` tasks have outputs that unblock `[C]` tasks:
  - Note unblocked tasks
  - Move dependent tasks to "Ready" in TODO.md

**Step 3: Context Drift Check**
- Run `git status`
- Run `git pull`
- If dirty OR pull finds changes:
  - **STOP.** Reply: "⚠️ **Context Drift:** File system changed. Run `..builder` again to refresh context."

**Step 4: Task Selection**
- Read TODO.md, filter to `[C]` tasks only
- Skip `[M]`, `[C→M]` (can't complete), `[M→C]` (waiting on decision)
- Select top priority `[C]` task

**Step 5: Mission Brief**
- Display task and acceptance criteria.
- Confirm: "🎯 Building: [task name]. Estimated: [X] minutes."

**Step 6: Implementation**
- Write code following CLAUDE.md standards.
- **Micro-commits** after each logical unit.

**Step 7: Completion Signal**
- When task is done, reply:
  > "✅ Task complete.
  > 📦 [X] commits made.
  > Run `..end` to verify and update documentation."

**Step 8: If Blocked on Human**
- If task requires human input not yet provided:
  > "🚧 **Blocked on Human:**
  > **Task:** [task]
  > **Needs:** [what Marek must provide]
  > **Added to:** MAREK.md
  >
  > Moving to next `[C]` task."

---

### ..end

**Session Cleanup (Builder Only)**

**Step 1: Verification (CRITICAL)**
- **For each task worked on:**
  - Check each acceptance criterion explicitly
  - If AC not met: Note what's missing, do NOT mark `[x]`
  - If AC met: Mark `[x]` in TODO.md

**Step 2: [C→M] Handoff**
- For any `[C→M]` tasks completed:
  - Verify deliverable exists in `/drafts/` or specified location
  - Move task to MAREK.md "Ready for Marek" section
  - Remove from TODO.md

**Step 3: Documentation Update**
- Add session entry to PROGRESS.md:
  - **Session:** [Date] — [Feature Name]
  - **Completed:** [Tasks with AC verified]
  - **Handed off:** [C→M tasks moved to MAREK.md]
  - **Commits:** [List or count]
  - **Next:** [What's queued]

**Step 4: Final Verification**
- Is `git status` clean?
- Is TODO.md accurate?
- Is MAREK.md updated?
- Is PROGRESS.md updated?

**Step 5: Final Output**
- `git push`
- Session summary.
- Suggested next `[C]` priority.
- "✅ Session closed."

---

### ..hygiene

**Context Garbage Collection (Architect Only)**

**Step 1: Scan File Sizes**
Flag files exceeding thresholds:
- `DECISIONS.md`: > 50KB
- `PROGRESS.md`: > 30KB
- `TODO.md`: > 100 items
- `MAREK.md`: > 50 items

**Step 2: Archive**
- PROGRESS.md entries > 30 days → `_archive/PROGRESS_[YYYY-MM].md`
- Completed TODO items → `_archive/TODO_DONE_[YYYY-MM].md`
- Completed MAREK.md items → `_archive/MAREK_DONE_[YYYY-MM].md`
- Superseded ADRs → `_archive/DECISIONS_ARCHIVE.md`

**Step 3: Report**
```
"🗑️ Archived [X] KB. Active context now [Y] KB.

Health: [Good/Warning/Critical]"
```

---

### ..recover

**Emergency Recovery Protocol (Any Role)**

**Level 1: Git Reset**
```bash
git status
git log --oneline -10
git reset --hard [last-good-commit]
```

**Level 2: Database Reset** (if applicable)
```sql
DROP SCHEMA public CASCADE;
CREATE SCHEMA public;
```
Then re-run init migration.

**Level 3: Full Environment Reset**
1. Delete `node_modules`
2. `npm install`
3. Reset database (Level 2)
4. `npm run dev`

**After Recovery:**
- Update PROGRESS.md with recovery note.
- Reply: "🔧 Recovery complete. Run `..builder` to resume."

---

### ..exit

**Context Fossilization (Architect Only)**

**Step 1: Verify Recent Builder Work**
- Check TODO.md: Are completed items actually working?
- Check PROGRESS.md: Does it match current implementation?

**Step 2: MAREK.md Review**
- Flag stale `[M]` tasks (>7 days)
- Suggest `[C→M]` splits for blocked work
- Note any completed `[M]` tasks not yet processed

**Step 3: Audit Documentation**
- PRFAQ current?
- CONSTRAINTS.md updated?
- CLAUDE.md has new patterns?
- DECISIONS.md complete?

**Step 4: Reprioritize**
- TODO.md: Re-sort by priority
- MAREK.md: Highlight urgent human tasks

**Step 5: Output**
- Checklist of updated files.
- Top `[C]` priority for next session.
- Top `[M]` priority for Marek.
- "✅ Context fossilized. Ready for new session."

---

## Context Loading Reference

| Role | Files Loaded | Approx Size | Token Budget |
|------|--------------|-------------|--------------|
| Architect | PRFAQ, CONSTRAINTS, DECISIONS, CLAUDE, TODO, PROGRESS, MAREK | ~30KB | ~15% |
| Builder | CLAUDE, TODO, MAREK | ~12KB | ~5% |

---

## Documentation Requirements

### Acceptance Criteria (in TODO.md)
Every task needs testable conditions:
```
BAD:  - [ ] [C] Fix width bug
GOOD: - [ ] [C] Fix width bug
        - AC: Container fills 100% width when panel collapsed
        - AC: Test passes on 375px viewport
```

### Design System (in CONSTRAINTS.md)
Before Builder implements UI, document:
- Button colors and meanings
- Canonical button text (no synonyms)
- Spacing rules and target viewports

---

## Anti-Patterns Learned

| Anti-Pattern | Consequence | Prevention |
|--------------|-------------|------------|
| TODO without AC | "Done" but broken | `..make` requires AC format |
| Skipping `..end` | Docs out of sync | Builder must run `..end` |
| No task markers | Claude attempts `[M]` tasks | Use ownership markers |
| `[M]` task without blocker note | Unclear what's waiting | Always note "Blocks: X" |
| Stale `[M]` tasks | Work stuck indefinitely | `..start` flags >7 day tasks |
| Ignoring context drift | Stale code conflicts | `..go` checks git pull |

---

## Multi-Tool Handoffs

When working across multiple AI tools (Claude Code, Figma Make, Lovable, Cursor), context doesn't sync automatically. Each tool has its own copy of files.

### The Problem

```
Claude Code                    Figma Make
     │                              │
     ▼                              ▼
[Updates DECISIONS.md]    [Still has old DECISIONS.md]
[Updates TODO.md]         [Still has old TODO.md]
     │                              │
     ▼                              ▼
 Context: Fresh              Context: Stale
```

Git tracks the source of truth, but tools like Figma Make don't auto-pull from Git.

### When Handing Off to Another Tool

**Claude's responsibility:**

1. **Identify what changed** — List files modified this session
2. **Prepare copy-paste content** — Output the changed sections, not just file names
3. **Provide the sync prompt** — Give the human the exact prompt for the other tool

**Example handoff output:**

```
---
Files Changed This Session

| File | What Changed |
|------|--------------|
| DECISIONS.md | Added DEC-023 (lines 120-145) |
| TODO.md | Added 3 tasks to Ready section |
| PROGRESS.md | Added session entry |

---
For Figma Make (or other tool)

1. Open each file in the tool's code view
2. Paste the updated content (below)
3. Prompt the tool:

   "Read DECISIONS.md, TODO.md, and PROGRESS.md to gain 
   the new context. Ask me anything if unclear."

---
Content to Paste

[DECISIONS.md changes]
...

[TODO.md changes]
...
```

### Human's Responsibility

1. **Paste updated content** into the other tool's code view (it autosaves)
2. **Prompt the tool** to read the updated files
3. **Verify** the tool understood the new context before continuing

### When to Trigger This

Claude should prepare a multi-tool handoff when:

- Human mentions switching to another tool ("I'm going to Figma Make now")
- Session involved significant protocol file changes
- `..end` is run and human has mentioned using other AI tools in this project

### Anti-Pattern

| Anti-Pattern | Consequence | Prevention |
|--------------|-------------|------------|
| Assuming tools sync via Git | Other tool has stale context, makes wrong decisions | Always prepare copy-paste handoff |
| Listing files without content | Human has to manually extract changes | Output the actual changed content |
| No sync prompt provided | Human forgets to prompt other tool | Always include the prompt to use |

---

## Conversational Guidance

Beyond the `..` commands, Claude can help through Socratic dialogue. When stuck or uncertain, these patterns help realign.

### "Help me, what do we do next?"

Claude should:
1. Summarize current state (what's done, what's blocked)
2. Identify the decision or action needed
3. Suggest 2-3 concrete next steps
4. Ask which direction resonates

**Example response:**
> "Based on where we are:
> - Session files need rewriting (blocked on curriculum decision)
> - Admin folder migration is ready to execute
> - Helen's response is still pending
>
> Options:
> 1. Execute the migration now (unblocks clean repo for workshop)
> 2. Draft the gym starter spec (ready when Helen confirms)
> 3. Park both and wait for Helen
>
> Which feels right?"

### "What are your recommendations?"

Claude should:
1. Use existing decision frameworks (from DECISIONS.md, project principles)
2. Map options against those frameworks
3. State a clear recommendation with reasoning
4. Acknowledge trade-offs

**Example pattern:**
> "Using the pedagogical principles from Decision 8:
> 
> | Option | Pain/Relief | Progressive | Rails |
> |--------|-------------|-------------|-------|
> | A | ✅ | ❌ | ✅ |
> | B | ❌ | ✅ | ✅ |
> 
> **Recommendation:** Option B because [reasoning].
> **Trade-off:** [what you give up]"

### "Is there a roadmap?"

Claude should:
1. Identify blocking dependencies
2. Sequence work logically
3. Mark what's waiting on human vs. Claude
4. Present as timeline or ordered list

**Example format:**
```
WEEK -2 (Now)
├── [M] Decision: X
├── [C] Execute: Y
└── [M] Send: Z

WEEK -1 (After blocker resolves)
├── [C] Build: A
└── [M] Review: B
```

### Clarifying Before Acting

When a request is ambiguous, Claude should:
1. State what it understood
2. Identify the ambiguity
3. Offer interpretations
4. Ask which to proceed with

**Anti-pattern:** Guessing and building the wrong thing.
**Good pattern:** "I could interpret this as X or Y. Which did you mean?"

### Pushing Back Constructively

When Claude sees a potential issue, it should:
1. Acknowledge the direction
2. Name the concern specifically
3. Offer an alternative
4. Let human decide

**Example:**
> "I like where this is going. One thing to consider: [concern].
> 
> Alternative: [different approach].
> 
> Your call — want to proceed as planned or adjust?"

---

## Related Documentation

- **[MAREK.md](./MAREK.md)** — Human-only tasks
- **[WORKFLOW.md](./WORKFLOW.md)** — Commit strategy, session handoff
- **[CONSTRAINTS.md](./CONSTRAINTS.md)** — Principles, rejected approaches, design system
- **[DECISIONS.md](./DECISIONS.md)** — Active ADRs
- **[CLAUDE.md](./CLAUDE.md)** — Technical reference

---

*v1.3 — December 29, 2025*
