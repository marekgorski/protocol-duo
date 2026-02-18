# duo AI Workflow Protocol (v1.0)

## Atomic Interaction Contract

Every interaction follows this cycle automatically:

| Step | What Happens |
|------|--------------|
| **LOAD** | Read context files (scope-dependent), check git status |
| **CLARIFY** | Confirm understanding before acting |
| **EXECUTE** | Do the work |
| **RECORD** | Update .md files, commit immediately |
| **REFLECT** | Surface improvements, flag drift |

**Default scope:** Lean (CLAUDE.md + TODO.md + TASKS/)

Scope modifiers expand or constrain what gets loaded:

| Modifier | Scope | When to Use |
|----------|-------|-------------|
| `..architect` | Full | Planning, architecture decisions, validating "what good looks like" |
| `..builder` | Lean | Implementation, execution, trusting the instruction |

**Fossilization is automatic.** The RECORD step commits after every interaction. No `..end` or `..exit` ceremony required.

---

## Protocol Evolution Philosophy

This instance may **intentionally drift** from the master template based on project-specific needs. This drift is a feature, not a bug.

**The Reintegration Cycle:**
1. **Clone** — Start from protocol-duo template
2. **Initialize** — Customize for project needs
3. **Drift** — Evolve based on real-world usage
4. **Reintegrate** — Contribute learnings back to master protocol
5. **Redistribute** — Improved protocol benefits all future clones

Each repo's learnings strengthen the collective. See [KayGee Protocol Family](https://kayg.ee/protocol) for upstream process.

---

## Lean Mode

**Check CLAUDE.md for `lean_mode` setting before enforcing scope permissions.**

| Mode | Behavior |
|------|----------|
| `lean_mode: on` | **Strict scope enforcement.** Must explicitly run `..architect` or `..builder` before using scope-specific commands. Loads essentials only by default. |
| `lean_mode: off` | **Free flow.** Commands work without explicit scope switching. Claude loads context as needed. |

**How it works:**
- When `lean_mode: on` — Scope checks in `..start`, `..make` are **enforced**. Claude stops and asks user to set scope.
- When `lean_mode: off` — Scope checks are **advisory**. Claude notes the intended scope but proceeds with the command.

**Default:** `off` (set in CLAUDE.md). Change to `on` for large projects where faster boot matters.

---

## Workflow Summary

| Workflow | Sequence |
|----------|----------|
| **Design** | `..architect` → `..start` → `..make` → (atomic RECORD commits) |
| **Build** | `..builder` → (atomic cycle runs) |
| **Maintenance** | `..architect` → `..hygiene` → (atomic RECORD commits) |
| **Recovery** | `..recover` (Any scope) |

---

## Task Ownership

Location encodes ownership — no markers needed:

| Location | Owner | Purpose |
|----------|-------|---------|
| **TODO.md** | Claude | AI tasks — work Claude does |
| **TASKS/** | Human | Tasks only a human can do |

**Handoff pattern:** When Claude prepares something a human must execute (e.g., a draft to review and send), Claude creates the deliverable and adds a task file in `TASKS/PRIORITY/` pointing to it. When a human makes a decision that unblocks AI work, they add the outcome to the task file in `TASKS/DONE/` and Claude picks up dependent work on next `..start`.

### TODO.md Format

```markdown
## 🔴 High Priority

- [ ] Implement user authentication
  - AC: Login returns JWT token
  - AC: Logout invalidates session

- [ ] Build pricing page
  - AC: Tier structure matches decision in TASKS/DONE/decide-pricing.md
  - AC: Responsive on mobile
```

**Human tasks go in TASKS/, not TODO.md:**
```
TASKS/PRIORITY/record-demo-video.md    ← Human records and uploads
TASKS/TODO/decide-pricing.md           ← Human decides, Claude implements after
```

---

## TASKS/ Folder

Human-only tasks live in TASKS/, organized by folder:

```
TASKS/
├── README.md     # Self-documenting guide
├── TODO/         # Not started
├── PRIORITY/     # Do these next
├── BLOCKED/      # Waiting on something external
└── DONE/         # Completed (consolidated monthly)
```

Each file is a **brief from Claude to the user** — a specific action, decision, or message.

**Task file format:**
```markdown
# [Action Title]

[Context and recommendation from Claude]

---

## The Ask

[Specific action for the user to take]

---

## What Happens Next

[What Claude will do once this is complete]
```

See `TASKS_README_TEMPLATE.md` for detailed format and examples.

---

## Handoff Protocol

### Claude creating human task

1. Create task file in `TASKS/TODO/` or `TASKS/PRIORITY/`
2. Include: context, recommendation, "The Ask", "What Happens Next"
3. Note in PROGRESS.md: "Created task for human: [filename]"

**Example:**
```
Created human task: TASKS/PRIORITY/record-demo-video.md

Contains: Script outline, recording tips, upload instructions
Blocks: VideoWalkthrough.tsx implementation
```

### Claude reprioritizing tasks (each ..start)

1. Review all TASKS/ files against current context
2. Move between folders as situation changes:
   - Urgent now? → Move to `PRIORITY/`
   - Blocked by external? → Move to `BLOCKED/`
   - No longer relevant? → Move to `DONE/` with note
3. Report status in briefing

### Human completing task

1. Add outcome to task file (decision, URL, confirmation number)
2. Move to `TASKS/DONE/` or tell Claude in next session
3. Claude checks TASKS/ on next `..start` or `..builder`
4. Claude unblocks dependent work and logs in PROGRESS.md

**Example outcome added to task file:**
```markdown
---

## Outcome

- **Decision:** €299 early bird, €399 regular
- **Completed:** Dec 28, 2025
- **Notes:** Competitive with similar workshops
```

---

## Scope Definitions

### ..architect

**Scope Expansion:**
1. **Purpose:** System design, strategy, planning, validating "what good looks like"
2. **Context Scope:** FULL (PRFAQ, CONSTRAINTS, DECISIONS, CLAUDE, TODO, PROGRESS, TASKS/)
3. **Allowed Commands:** `..start`, `..make`, `..hygiene`
4. **Behavior:** Challenge drift, validate architecture, ask clarifying questions
5. **Acknowledge:** "🏗️ ARCHITECT SCOPE. Full context loaded. (~15% token budget)"

### ..builder

**Scope Confirmation:**
1. **Purpose:** Implementation & execution, trust the instruction
2. **Context Scope:** LEAN (CLAUDE, TODO, TASKS/ only). Skip PRFAQ, CONSTRAINTS, PROGRESS.
3. **Safety Check:** Run `git status`. If dirty: STOP. "⚠️ Uncommitted changes detected. Commit or stash first."
4. **Allowed Commands:** `..recover`
5. **Behavior:** Execute efficiently, don't re-plan, micro-commit after each unit
6. **Acknowledge:** "🔨 BUILDER SCOPE. Lean context loaded. (~5% token budget)"

---

## Operational Commands

### ..start

**Session Bootloader (Full Scope)**

**Step 1: Scope Verification**
- Check `lean_mode` in CLAUDE.md
- IF `lean_mode: on` AND Scope != FULL: **Stop.** Reply: "⛔ **Builder Optimization:** Builders should skip `..start` — the atomic cycle runs automatically in lean scope."
- IF `lean_mode: off`: Proceed (note: this loads full Architect context)

**Step 2: Context Loading (LOAD step of atomic cycle)**
- Read: PRFAQ, CONSTRAINTS, DECISIONS, CLAUDE, TODO, PROGRESS, TASKS/.

**Step 3: Status Report**
- Report top priority task from TODO.md (including acceptance criteria).
- Note any completed tasks in TASKS/DONE/ that unblock work.
- Flag stale human tasks in TASKS/ (>7 days no progress).
- Wait for `..make` or `..hygiene`.

**Step 4: Task Analysis**
- Identify human tasks in TASKS/ where Claude could prepare something (draft, research, spec)
- Suggest task splits if a human task has Claude-doable subcomponents

---

### ..make

**Design Protocol (Full Scope)**

**Step 1: Scope Check**
- Check `lean_mode` in CLAUDE.md
- IF `lean_mode: on` AND Scope != FULL: **Stop.** Reply: "⛔ Permission Denied. Run `..architect` first."
- IF `lean_mode: off`: Proceed (implicitly loads full context for this command)

**Step 2: Intent Confirmation**
- User provides 1-2 sentence feature goal.
- Confirm understanding before proceeding.

**Step 3: Design Phase (MANDATORY VISUAL)**
- **CRITICAL:** Present a **Design Proposal** (ASCII mockup or detailed description) and ask for user confirmation BEFORE writing to DECISIONS.md or TODO.md.
- Review CONSTRAINTS.md for rejected approaches.
- Review DECISIONS.md for existing patterns.
- Design: data changes, UI flows, integrations.

**Why Design Proposal First:**
- Prevents "blindly building the wrong thing"
- Catches misalignment early (cheaper to fix)
- Visual mockups clarify layout faster than words
- User can redirect before any code is written

**Design Proposal Format:**
```
📐 DESIGN PROPOSAL: [Feature Name]

[ASCII mockup or detailed description]

Questions:
1. [Layout question]
2. [Behavior question]

Approve this design before I write to DECISIONS.md?
```

**Step 4: Task Routing**
- For each task, determine location:
  - Claude can complete entirely? → **TODO.md**
  - Requires human action? → **TASKS/** (create task file)
  - Claude prepares, human executes? → Claude does the work in TODO.md, then creates task file in TASKS/PRIORITY/ with deliverable
  - Human decides, Claude implements? → Create decision task in TASKS/PRIORITY/, add dependent TODO.md item

**Step 5: Output Protocol (MANDATORY)**
- **Write directly to files:**
  - DECISIONS.md: Add/update ADR
  - TODO.md: Add AI tasks with AC
  - TASKS/: Create human task files
- **TODO format required:**
  ```
  - [ ] Task description
    - AC: Specific testable condition
  ```
- **Final Reply:**
  > "✅ Spec written.
  > 📄 `DECISIONS.md`: ADR-XXX added
  > 📋 `TODO.md`: [X] AI tasks added
  > 👤 `TASKS/`: [Y] human tasks created
  >
  > Builder can start implementing."

---

### Builder Execution (Atomic Cycle)

When `..builder` is active, the atomic cycle handles implementation automatically:

**LOAD Phase:**
- Check `TASKS/DONE/` for completed human tasks that unblock work
- Run `git status` and `git pull` — if dirty or changes found, STOP and re-run `..builder`
- Read TODO.md — all items are AI work by definition
- Select top priority task

**CLARIFY Phase:**
- Display task and acceptance criteria
- Confirm: "🎯 Building: [task name]"

**EXECUTE Phase:**
- Write code following CLAUDE.md standards
- **Micro-commits** after each logical unit

**RECORD Phase (automatic — no ceremony):**
- Verify acceptance criteria explicitly
- If AC met: mark `[x]` in TODO.md
- Update PROGRESS.md
- Commit docs immediately after code — docs travel with code, not after it
- For handoff tasks: verify deliverable exists, create task file in `TASKS/PRIORITY/`

**REFLECT Phase:**
- Surface improvements, flag drift
- Suggest next priority

**If Blocked on Human:**
> "🚧 **Blocked on Human:**
> **Task:** [task]
> **Needs:** [what human must provide]
> **Added to:** TASKS/PRIORITY/
>
> Moving to next TODO.md task."

---

### Atomic RECORD Step

**The RECORD step runs automatically after every EXECUTE.** This is not a command — it's built into the atomic interaction cycle.

**Step 1: Verification**
- **For each task worked on:**
  - Check each acceptance criterion explicitly
  - If AC not met: Note what's missing, do NOT mark `[x]`
  - If AC met: Mark `[x]` in TODO.md

**Step 2: Handoff to Human**
- For tasks where Claude prepared something a human must execute:
  - Verify deliverable exists in `/drafts/` or specified location
  - Create task file in TASKS/PRIORITY/ with deliverable
  - Mark complete in TODO.md

**Step 3: Documentation Update**
- Update PROGRESS.md with what was done
- Update TODO.md with task status
- Update TASKS/ if human tasks were created or completed

**Step 4: Commit Immediately**
- `git add` relevant files
- `git commit -m "type: description"`
- `git push`

**Step 5: Output Summary**
- What was done
- What changed in docs
- What's next

**This happens after EVERY interaction, not just at "session end."** Fossilization is continuous, not batched.

---

### ..hygiene

**Context Garbage Collection (Full Scope)**

**Step 1: Token Budget Check**
Run word count to assess documentation load:
```bash
wc -w *.md
```

Evaluate health:
- ✅ **Good:** Total <10,000 words, no single file >3,000 words
- ⚠️ **Warning:** Total 10,000-15,000 words, or any file >3,000 words
- 🚨 **Critical:** Total >15,000 words, or any file >5,000 words

**Target token loads per scope:**
- Architect: ~7,500 tokens (~15% budget) — PRFAQ, CONSTRAINTS, DECISIONS, CLAUDE, TODO, PROGRESS, TASKS/
- Builder: ~2,500 tokens (~5% budget) — CLAUDE, TODO, TASKS/

**Flag if:** PRINCIPLES.md missing after project has >5 ADRs

**Step 2: Scan File Sizes**
Flag files exceeding thresholds:
- `DECISIONS.md`: > 50KB or > 10 ADRs
- `PROGRESS.md`: > 30KB or > 10 sessions
- `TODO.md`: > 100 items
- `TASKS/DONE/`: > 50 files (run consolidation)
- Any `.md` file: > 3,000 words

**Step 3: Apply "Next Session Test"**
For each flagged file, review sections:
- **Keep:** Would Claude need this next session?
  - Active decisions, current architecture, technical reference
- **Archive:** Historical narrative, debugging stories, "how we learned X"

**Step 4: Archive**
- PROGRESS.md entries > 30 days → `_archive/PROGRESS_[YYYY-MM].md`
- Completed TODO items → `_archive/TODO_DONE_[YYYY-MM].md`
- TASKS/DONE/ files → `_archive/TASKS_DONE_[YYYY-MM].md` + `_archive/tasks/[YYYY-MM]/`
- Superseded ADRs → `_archive/DECISIONS_ARCHIVE.md`
- Historical content from CLAUDE.md → `_archive/DEBUGGING_NOTES.md` or similar

**Step 5: Extract Principles (if applicable)**
If DECISIONS.md has >5 implemented ADRs and no PRINCIPLES.md exists:
- Create PRINCIPLES.md from recurring patterns
- Extract mission from PRFAQ.md
- Distill product, technical, and design principles
- Move stable ADRs to archive (keep 2-3 active)

**Step 6: Report**
```
"🗑️ Hygiene Complete

Token Budget:
- Architect: [X] words (~Y% of budget) [✅/⚠️/🚨]
- Builder: [X] words (~Y% of budget) [✅/⚠️/🚨]

Actions:
- Archived [X] sessions to _archive/PROGRESS_[YYYY-MM].md
- Moved [X] ADRs to _archive/DECISIONS_ARCHIVE.md
- [Created/Updated] PRINCIPLES.md

Health: [Good/Warning/Critical]"
```

**Health Levels (scope-specific):**
- ✅ Good: <15% Architect, <5% Builder
- ⚠️ Warning: 15-20% Architect, 5-10% Builder
- 🚨 Critical: >20% Architect, >10% Builder

**Threshold Configuration:** Adjust thresholds to match your project's needs. Smaller projects may want tighter limits. Larger projects may need more headroom. The goal is keeping context loadable in a single AI session.

**When to Run:**
- **Proactive:** Monthly check (first Monday)
- **Reactive:** After v0.5, v1.0, v2.0 milestones
- **Emergency:** When Architect feels sluggish loading context
- **Critical:** When token budget check shows 🚨 Critical

---

### ..recover

**Emergency Recovery Protocol (Any Scope)**

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

### Atomic REFLECT Step

**The REFLECT step runs automatically as part of every atomic cycle.** This is not a command — it's built into the atomic interaction.

**Step 1: Verify Work**
- Check TODO.md: Are completed items actually working?
- Check PROGRESS.md: Does it match current implementation?

**Step 2: TASKS/ Review**
- Flag stale human tasks in TASKS/ (>7 days)
- Suggest splits where Claude could prepare something for a blocked task
- Note any completed human tasks not yet processed

**Step 3: Surface Improvements**
- What patterns emerged that should be documented?
- What constraints were discovered?
- What drift from protocol should be flagged?

**Step 4: Output**
- What was done
- What's next (top TODO.md priority)
- Any blockers or human tasks needed

**This happens after EVERY interaction.** Context is continuously fossilized, not batched at session end.

---

## PR Protocol (MANDATORY)

**With the atomic model, context is fossilized continuously.** Every interaction runs RECORD and REFLECT steps automatically.

**Why this matters for PRs:** Claude Code via web UI creates branches and loses context after merge. With atomic fossilization, context is preserved after every interaction — not just at session end.

**The sequence:**
```
[work] → (atomic RECORD commits) → (atomic REFLECT updates docs) → push → create PR → merge
              ↑                            ↑
         Context preserved HERE      And HERE (every interaction)
```

**Before creating a PR, verify:**
1. TODO.md reflects current state
2. PROGRESS.md has recent entries
3. TASKS/ files are up to date
4. All changes are committed and pushed

**Anti-pattern:**
```
❌ [work] → create PR → merge → (realize docs not updated)
✅ [work] → (atomic cycle commits docs) → create PR → merge → (context preserved)
```

---

## Branch Completion Protocol (MANDATORY)

**With the atomic model, docs are updated continuously.** The RECORD step updates docs and commits after every interaction.

**Before pushing ANY branch, verify:**

```
[work] → (atomic RECORD verifies AC, updates docs, commits) → push
                        ↑
            Happens automatically every interaction
```

**The sequence:**
1. Atomic RECORD step (verifies AC, updates TODO/PROGRESS/TASKS, commits)
2. Push to remote

**Why:** Memory preservation. Next session (human or AI) won't know what shipped if docs aren't updated. The atomic model prevents this by committing docs after every interaction.

**Anti-pattern:**
```
❌ git push  # Pushed code without updating docs
✅ (atomic RECORD) → git push  # Docs already updated, then push
```

---

## The "Save Game" Rule

**CRITICAL:** When implementing a feature, commit and push in incremental steps. Do not wait for perfection.

**Why:** Claude Code has token limits. If a large implementation hits the limit mid-session:
- Uncommitted work exists only in the filesystem
- Context is lost
- Recovery requires manual intervention (Lazarus Protocol)

**The Rule:**
```
After each logical unit of work:
1. git add [files]
2. git commit -m "feat: [specific change]"
3. git push
```

**What counts as a "logical unit":**
- Migration file created → commit
- Types updated → commit
- Component created → commit
- Styles added → commit

**Example (implementing a Tracker page):**
```bash
# Unit 1: Database
git commit -m "feat(db): add tracker table migration" && git push

# Unit 2: Types
git commit -m "feat(types): add TrackerEntry interface" && git push

# Unit 3: UI
git commit -m "feat(ui): add Tracker component shell" && git push

# Unit 4: Styles
git commit -m "feat(styles): tracker page css" && git push
```

### The Lazarus Protocol (Emergency Recovery)

If Claude Code crashes mid-implementation and there's uncommitted work:

1. **Check filesystem**: `git status` — see what exists
2. **Assess damage**: Review uncommitted files
3. **Test locally**: Does the app compile? Does it run?
4. **Recover**: If it compiles, commit with message: `feat: recover [feature] from crashed session`
5. **Document**: Add recovery note to PROGRESS.md

This is a last resort. The Save Game Rule prevents needing it.

---

## Context Loading Reference

| Scope | Files Loaded | Approx Size | Token Budget |
|-------|--------------|-------------|--------------|
| Full (`..architect`) | PRFAQ, CONSTRAINTS, DECISIONS, CLAUDE, TODO, PROGRESS, TASKS/ | ~30KB | ~15% |
| Lean (`..builder`) | CLAUDE, TODO, TASKS/ | ~12KB | ~5% |
| Default (no modifier) | CLAUDE, TODO, TASKS/ | ~12KB | ~5% |

---

## Documentation Requirements

### Acceptance Criteria (in TODO.md)
Every task needs testable conditions:
```
BAD:  - [ ] Fix width bug
GOOD: - [ ] Fix width bug
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
| Skipping RECORD step | Docs out of sync | Atomic cycle makes RECORD automatic |
| AI work in TASKS/ or human work in TODO.md | Wrong owner, task stuck or wasted effort | TODO.md = AI work, TASKS/ = human work |
| Human task without blocker note | Unclear what's waiting | Always note "Blocks: X" in task file |
| Stale human tasks | Work stuck indefinitely | `..start` flags >7 day tasks |
| Ignoring context drift | Stale code conflicts | LOAD phase checks git pull |
| **Push before docs updated** | **Memory lost, context drift** | **Atomic RECORD commits docs every interaction** |
| **Big-bang commits** | **Token crash loses all work** | **Atomic cycle: commit after every interaction** |
| **Design without mockup** | **Build wrong thing** | **`..make` requires design proposal** |
| **PR before fossilization** | **Context lost after merge** | **Atomic model fossilizes continuously** |
| Rationalizing instead of executing | User's goal not achieved | Execute first, then offer opinions if asked |
| Ambiguous instruction → assume | Wrong implementation, rework | Clarify BEFORE implementing (CLARIFY step) |
| Creating but not committing | Work exists only in external tool | If you create it, commit it (RECORD step) |
| Drifting feature branches | Orphaned work, context lost | Delete stale branches, salvage ideas into TODO.md or a parking file |
| Over-scoped features | Builds unvalidated complexity | Simplify → ship → validate → expand |
| Premature optimization | Wasted effort on wrong things | Park features as PRDs until user testing validates need |
| Batching commits at session end | PROGRESS not updated, TODO not cleaned, context lost | Atomic RECORD commits after every interaction — no batching |
| Deferring docs to session end | Stale docs if session ends early or deploy happens | Atomic RECORD commits docs every interaction |
| Summarize-and-commit without RECORD | PROGRESS not updated, TODO not cleaned, no AC verification | Atomic cycle runs automatically — fossilization is continuous |

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
> - Feature design needs rewriting (blocked on stakeholder decision)
> - Database migration is ready to execute
> - Client feedback is still pending
>
> Options:
> 1. Execute the migration now (unblocks clean schema for next feature)
> 2. Draft the API spec (ready when stakeholder confirms requirements)
> 3. Park both and wait for client feedback
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
├── TASKS/PRIORITY/ → Decision: X
├── TODO.md → Execute: Y
└── TASKS/PRIORITY/ → Send: Z

WEEK -1 (After blocker resolves)
├── TODO.md → Build: A
└── TASKS/TODO/ → Review: B
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

- **TASKS/** — Human-only tasks
- **[CONSTRAINTS.md](./CONSTRAINTS.md)** — Principles, rejected approaches, design system
- **[DECISIONS.md](./DECISIONS.md)** — Active ADRs
- **[CLAUDE.md](./CLAUDE.md)** — Technical reference

---

*duo Protocol v1*
