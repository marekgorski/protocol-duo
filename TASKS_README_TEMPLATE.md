# TASKS

Human tasks prepared by Claude for the user.

---

## How This Works

| Component | Purpose |
|-----------|---------|
| **TODO.md** | Claude's work — AI tasks |
| **TASKS/** | Human work — Human tasks (this folder) |

Each `.md` file in this folder is a **brief from Claude to the user** — a specific action, decision, or message that only a human can complete.

---

## Folder Structure

```
TASKS/
├── README.md      ← You are here
├── TODO/          ← Not started
├── PRIORITY/      ← Do these next
├── BLOCKED/       ← Waiting on something external
└── DONE/          ← Completed (consolidated monthly by ..hygiene)
```

---

## Task File Format

Each task file is a self-contained brief:

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

**Examples:**

### Decision Request
```markdown
# Choose Color Scheme

I've researched color options for the dashboard. Here's my recommendation:

**Option A: Blue (#3B82F6)** — Professional, matches existing brand
**Option B: Green (#10B981)** — Fresh, differentiates from competitors

I recommend **Blue** because it maintains brand consistency and tested well in similar apps.

---

## The Ask

Let me know: Blue or Green?

---

## What Happens Next

Once you decide, I'll update the design system and apply across all components.
```

### Send Message
```markdown
# Message for Workshop Organizer

Draft message for Amy about the upcoming workshop:

---

**To:** Amy
**Subject:** Workshop - Mar 10 Confirmation

Hi Amy,

Confirming the workshop for Mar 10 at [venue].
I'll bring printed handouts for 12 participants.

Let me know if you need anything else before then.

Best,
Human

---

## The Ask

Review and send (or edit first).

---

## What Happens Next

Once sent, I'll add to calendar and prepare handout materials.
```

### Purchase/Action
```markdown
# Buy Conference Ticket

Need to purchase early-bird ticket for the developer conference.

**Details:**
- Event: DevConf 2026
- Cost: $199 (early bird, expires Mar 1)
- Deadline: Before Mar 1

**Link:** [DevConf Registration](https://example.com/devconf)

---

## The Ask

Purchase the ticket and paste confirmation number here.

---

## What Happens Next

I'll update BOOKINGS.md with the confirmation and mark this complete.
```

---

## Claude's Responsibilities

Each `..start` session, Claude:

1. **Reviews all TASKS/ files** against current context
2. **Moves files** between folders as situation changes:
   - Urgent now? → Move to `PRIORITY/`
   - Blocked by something? → Move to `BLOCKED/`
   - No longer relevant? → Move to `DONE/` with note
3. **Creates new task files** when human action is needed
4. **Reports status** in briefing:
   ```
   ### Human Tasks
   | Priority | Task | Action Needed |
   |----------|------|---------------|
   | 🔴 | book-conference-hotel.md | Decision: which hotel? |
   | 🟡 | send-workshop-confirmation.md | Review and send |
   ```

---

## Completing Tasks

When the user completes a task:

1. **Add outcome** to the task file (e.g., "Chose Blue", "Sent on Jan 28", "Confirmation: ABC123")
2. **Move to DONE/** or tell Claude in next session
3. Claude will update dependent work and consolidate during `..hygiene`

---

## Monthly Consolidation

During `..hygiene`, Claude:

1. Creates `_archive/TASKS_DONE_[YYYY-MM].md` summary
2. Moves completed task files to `_archive/tasks/[YYYY-MM]/`
3. Keeps DONE/ folder empty for next month

---

*This README lives in TASKS/ for self-reference. Update as the system evolves.*
