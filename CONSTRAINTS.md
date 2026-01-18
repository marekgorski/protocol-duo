# Constraints

Philosophical boundaries, design system rules, and explicitly rejected approaches.

---

## Core Principles

> Document your project's core principles here. Examples:
> - "Pull Not Push" — Education available when curious, never forced
> - "Effort Signals, Not Measurements" — Track direction, not decimals
> - "Independence as the Goal" — Success = user no longer needs the app

---

## Design System

### Button Hierarchy

| Color | Use | Examples |
|-------|-----|----------|
| 🟢 Green | Primary positive action | "Save", "Accept", "Continue" |
| 🟠 Orange | Secondary warm action | "Edit", "Return" |
| 🟡 Yellow/Amber | Alternative flow | "Skip", "Switch" |
| 🔵 Blue | Navigation/reset | "Next", "Start Over" |
| ⚪ Gray | Tertiary/cancel | "Cancel", "Defer" |

### Text Conventions

Document canonical text for common actions to prevent synonyms:
- Navigation to home: **"[Your canonical text]"** (never "Go Home", "Back to Start", etc.)
- Save action: **"[Your canonical text]"**
- Cancel action: **"[Your canonical text]"**

### Visual Hierarchy

1. **Primary** — What the user is doing (largest, boldest)
2. **Secondary** — Supporting details (smaller, gray)
3. **Tertiary** — Metadata (smallest, muted)

### Spacing & Viewport

- **Target mobile viewport**: 375×667 (iPhone SE)
- **CTA placement**: Primary action visible without scrolling
- **Touch targets**: Minimum 44×44px

---

## Explicitly Rejected

| Option | Why Rejected | Date |
|--------|--------------|------|
| Example: localStorage only | Too limited for multi-user | YYYY-MM-DD |
| Example: Complex state management | Overkill for current scope | YYYY-MM-DD |

---

## AI Boundaries (Optional)

Define acceptable vs rejected AI use cases to prevent feature creep. Remove this section if not applicable to your project.

### Acceptable AI Use Cases ✅

AI applications that **amplify your core value** without corrupting it:

1. **[Use Case 1]**
   - What: [Description]
   - Why acceptable: [Rationale]

2. **[Use Case 2]**
   - What: [Description]
   - Why acceptable: [Rationale]

<!-- Example from SpellMe:
1. **Error-pattern clustering across learners**
   - What: Identify common confusion patterns
   - Why acceptable: Helps coaches see patterns, doesn't replace judgment
-->

### Explicitly Rejected AI ❌

AI applications that would **corrupt your core value proposition**:

1. **[Rejected Use Case 1]**
   - What: [Description]
   - Why rejected: [How it undermines core value]

2. **[Rejected Use Case 2]**
   - What: [Description]
   - Why rejected: [How it undermines core value]

<!-- Example from SpellMe:
1. **LLM chat tutors**
   - What: Built-in AI tutor for explanations
   - Why rejected: Pedagogically dubious, expensive, optimizes for conversation not mastery
-->

**Principle:** Define the line clearly. If an AI feature optimizes for engagement over your core metric, reject it.

---

## Open Questions

1. Document unresolved design questions here
2. These become inputs for future `..make` sessions

---

*Template from duo Protocol v1*
