---
name: ui-brain
description: UI design rules, concrete values, failure patterns and review checklists for web, iOS, Android, desktop and game UI (Roblox, Unity). Use when designing, refining or reviewing any user interface or UI code, including typography, color, spacing, motion, interaction states, components, icons, accessibility, safe areas and touch targets.
type: index
---
# ui-brain: UI design knowledge for design subagents

These notes record rules, thresholds, values and failure patterns that improve on model defaults; nothing here is a definition or tutorial. They cover web, iOS, Android, desktop and game UI (Roblox, Unity).

## For agents: how to load
1. Find your task type below. Read that domain's map and checklist.
2. From the map, open **only** the concept notes the task touches.
3. For platform constants (safe areas, touch-target minimums, viewport units, GuiInset), read `platforms/<platform>.md`.
4. **Never load the whole vault.** Notes are `status: draft` until the owner verifies them. Treat values marked **unverified** as estimates and say so in your output.
5. Link resolution: all paths are relative to this file's directory (`${CLAUDE_SKILL_DIR}` when loaded as a skill). `[[name]]` = `concepts/name.md`. `[[maps/x]]` = `maps/x.md`, and likewise for `checklists/`, `platforms/`.
6. Finish by listing anything the vault was missing or got wrong under **Vault gaps**, so the owner can `harvest` it.

| Task | Map (+ same-named checklist) |
|---|---|
| Type scale, fonts, text rendering, numbers in tables | [[maps/typography]] |
| Palette, theming, dark mode, gradients, borders | [[maps/color]] |
| Grids, spacing, alignment, radii, layout stability | [[maps/layout-and-spacing]] |
| Transitions, gestures, micro-interactions | [[maps/motion]] |
| Feedback, loading/empty/error states, disclosure | [[maps/interaction-and-state]] |
| Building or reviewing a specific control | [[maps/components]] |
| Icons, edges, blur, shadows, polish pass | [[maps/iconography-and-visual-detail]] |
| Notches, viewports, input methods, Roblox/Unity screen setup | [[maps/platform-and-environment]] + `platforms/` |
| Accessibility review | [[maps/accessibility]] |
| Full design review | Each relevant checklist, one domain pass at a time |

Humans: the folders are `maps/`, `concepts/`, `checklists/`, `platforms/`, `inbox/` (agents ignore it), and [[sources]]. Maintenance rules live in `CLAUDE.md`.
