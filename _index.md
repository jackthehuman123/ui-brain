---
type: index
description: "Entry point: search-first lookup procedure for the ui-brain vault"
---
# ui-brain

Rules, values, failure patterns and review checks that improve UI output beyond model defaults, for web, iOS, Android, desktop and Roblox/Unity game UI.

## Lookup procedure (agents must follow)
1. **Scan summaries, not files:** `~/.claude/skills/ui-brain/scripts/find.sh [keyword…]` prints `path: description` for each note. Without the skill: `rg "^description:" ~/Documents/vaults/ui-brain/{concepts,components,screens,project-types}`
2. **Whole-domain review:** open `maps/<domain>.md` + `checklists/<domain>.md` instead (see table).
3. **Open at most 5 notes.** Use offset/limit when you only need one section (**Values:**, **Detect in review:**).
4. **Never** read the whole vault or glob-read a folder.

Folders: `project-types/` (routing per product) → `screens/` → `components/` → `concepts/` (atomic rules + values). Constants live in `platforms/`. `[[name]]` = `concepts/name.md`; `[[components/form]]` = that path + `.md`.

## Task → map + checklist
| Task | Load |
|---|---|
| Type scale, fonts, numerals, text rendering | `maps/typography.md` + `checklists/typography.md` |
| Palette, theming, dark mode, gradients, borders | `maps/color.md` + `checklists/color.md` |
| Grid, spacing, alignment, radii, layout stability | `maps/layout-and-spacing.md` + `checklists/layout-and-spacing.md` |
| Transitions, gestures, micro-interactions | `maps/motion.md` + `checklists/motion.md` |
| Feedback, loading/empty/error states, disclosure | `maps/interaction-and-state.md` + `checklists/interaction-and-state.md` |
| Icons, edges, blur, shadows, polish | `maps/iconography-and-visual-detail.md` + `checklists/iconography-and-visual-detail.md` |
| Notches, viewports, input, Roblox/Unity screens | `maps/platform-and-environment.md` + `checklists/platform-and-environment.md` + `platforms/` |
| Accessibility audit | `maps/accessibility.md` + `checklists/accessibility.md` |
| Build a screen or product | `maps/project-types.md` → `maps/screens.md` → `maps/components.md` |

Notes are `status: draft`; treat **unverified** values as estimates. End with **Vault gaps** for `harvest`. Maintenance: `CLAUDE.md`. Sources: `sources.md`. Agents ignore `inbox/`.
