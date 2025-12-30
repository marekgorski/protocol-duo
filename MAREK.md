# MAREK.md - Human Tasks

**Purpose:** Tasks only humans can do (recording, content creation, external decisions)  
**Last Updated:** [DATE]

---

## Why This File Exists

Some tasks can't be done by AI assistants:
- Recording videos or audio
- Taking photos or screenshots
- Making decisions that require external input
- Creating content that needs human creativity or voice
- Tasks requiring accounts/access AI doesn't have

This file tracks those tasks with clear ownership markers:
- `[M]` — Marek must complete entirely
- `[C→M]` — Claude prepared, Marek executes
- `[M→C]` — Marek decides, Claude implements

---

## ⏸️ Blocked (needs Marek action)

Tasks that only Marek can complete. Note what they block.

```
- [ ] [M] Task description
  - AC: Acceptance criteria
  - Blocks: [component/feature waiting on this]
```

<!-- Example:
- [ ] [M] Record 2-min product demo
  - AC: Video uploaded to YouTube
  - AC: URL provided below
  - Blocks: VideoWalkthrough.tsx
-->

---

## ✅ Ready for Marek (Claude prepared)

Claude completed the prep work. Marek reviews and executes.

```
- [ ] [C→M] Task description
  - Deliverable: /drafts/filename.md
  - Action needed: [what Marek does with it]
```

<!-- Example:
- [ ] [C→M] Investor outreach email
  - Deliverable: /drafts/investor-email.md
  - Action needed: Review, personalize, send
-->

---

## ❓ Waiting on Marek Decision

Claude needs a decision before implementing.

```
- [ ] [M→C] Decision question?
  - Options: A, B, C
  - Context: [why this matters]
  - Unblocks: [what Claude will do after]
```

<!-- Example:
- [ ] [M→C] Which repo to link for protocol template?
  - Options: layer3-protocol, layer3-light, new public repo
  - Context: ForEngineers CTA needs a destination
  - Unblocks: Claude adds link to ForEngineers.tsx
-->

---

## ✅ Completed

Mark tasks complete with output and date.

```
- [x] [M] Task — Date
  - Output: [URL, decision, file path]
  - Unblocks: [what's now ready for Claude]
```

<!-- Example:
- [x] [M] Record demo video — Dec 28, 2025
  - Output: https://youtube.com/watch?v=abc123
  - Unblocks: VideoWalkthrough.tsx

- [x] [M→C] Workshop pricing — Dec 28, 2025
  - Decision: €299 early bird, €399 regular
  - Rationale: Competitive with similar workshops
  - Unblocks: Claude implements pricing page
-->

---

## Quick Reference

| Task | Type | Blocks | Priority |
|------|------|--------|----------|
| [Task name] | [M]/[C→M]/[M→C] | [Component] | HIGH/MED/LOW |

---

## Not In This File

These stay in TODO.md (Claude can do them):
- `[C]` tasks — Code, docs, implementation
- Anything that doesn't require human action

---

**Workflow:**
1. Claude adds `[M]` tasks here during `..make`
2. Claude moves `[C→M]` tasks here after completing prep work
3. Marek completes tasks and adds output
4. Claude picks up completed tasks on next `..go`

---

*Rename this file to match your name (e.g., SARAH.md, TEAM.md)*
