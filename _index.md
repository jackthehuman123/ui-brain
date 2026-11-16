---
type: index
---
# ui-brain: UI design knowledge for design subagents

This vault holds what improves design output beyond model defaults: rules, thresholds, values, failure patterns and how to detect them. It has no definitions or tutorials. It covers web, iOS, Android, desktop and game UI (Roblox, Unity).

## For agents: how to load
1. Find your task type below and load the listed `maps/` and `checklists/` files.
2. From the map, open **only** the concept notes the task touches.
3. For platform constants (safe areas, touch-target minimums, viewport units, GuiInset), open the file in `platforms/`.
4. **Never load the whole vault.** Notes marked `status: draft` are unreviewed; treat any value marked **unverified** as a starting estimate.

| Task | Load |
|---|---|
| Type scale, fonts, text rendering, numbers in tables | [[maps/typography]] |
| Palette, theming, dark mode, gradients, borders | [[maps/color]] |
| Grids, spacing, alignment, radii, layout stability | [[maps/layout-and-spacing]] |
| Transitions, gestures, micro-interactions | [[maps/motion]] |
| Feedback, loading/empty/error states, disclosure | [[maps/interaction-and-state]] |
| Building or reviewing a specific control | [[maps/components]] |
| Icons, edges, blur, shadows, polish pass | [[maps/iconography-and-visual-detail]] |
| Notches, viewports, input methods, Roblox/Unity screen setup | [[maps/platform-and-environment]] + `platforms/<platform>.md` |
| Accessibility review | [[maps/accessibility]] |
| Full design review | Each relevant domain's checklist, one pass at a time |

## Layout
- `maps/`: one map of content per domain
- `concepts/`: atomic notes, flat folder, kebab-case
- `checklists/`: yes/no review passes, one per domain
- `platforms/`: per-platform constants (web, ios, android, desktop, roblox, unity)
- `inbox/`: candidates and drafts awaiting review (agents: ignore)
- [[sources]]: trusted sources, ranked
