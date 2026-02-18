# Constraints

> What we DON'T do — learned from decisions and failures.
> Loaded during `..architect` scope. Checked during `..make` sessions.

---

## Core Principles

[Extract from project discovery — 2-4 guiding constraints]

<!-- Examples from real projects:
- "Pull Not Push" — Education available when curious, never forced
- "Effort Signals, Not Measurements" — Track direction, not decimals
- "Independence as the Goal" — Success = user no longer needs the app
-->

---

## Explicitly Rejected

| Approach | Why Rejected | Date |
|----------|-------------|------|

---

## Design System

Remove this section for non-UI projects.

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
- Navigation to home: **"[Your canonical text]"**
- Save action: **"[Your canonical text]"**
- Cancel action: **"[Your canonical text]"**

---

*Template from duo Protocol*
