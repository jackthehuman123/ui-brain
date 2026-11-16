---
type: component
description: "Uniform rows: whole row one target ≥56px, one-line truncation with full text kept, inset alpha dividers"
aliases: [list view, rows, inbox list, table rows, list item]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://m3.material.io/components/lists/overview
---
# List

**Use when:** many items of the same shape that users scan and compare (messages, files, settings). **Don't use when:** items are visual and browsed (use [[components/card]]), or need column comparison (use a table).

**Anatomy:** list → optional sticky section headers → rows (leading avatar/icon · title · supporting line · trailing meta or action) → inset dividers.

**Required states:** default · hover · pressed · focus-visible · selected/current · unread · loading · empty.

**Rules:**
- The whole row is one target (one link or button); nested actions only as a separate trailing control → [[touch-target]], [[fitts-law]].
- Titles and supporting lines truncate to one line with an ellipsis, and the full text stays available (title, accessible name or detail view). Long names must not push meta off the row.
- Meta (times, sizes, counts) right-aligned with tabular digits → [[tabular-numbers]].
- Dividers are translucent and inset past the leading element → [[alpha-borders]].
- Unread or new = weight + dot + screen-reader text, not color alone → [[affordance]].
- Semantic `ul`/`li` (or a `role=list`). Section headers can be sticky.

**Values:** row ≥ 56px (64px with two lines). Divider inset = leading element width + gap.

**Platform variants:**
- iOS: `List` with `.swipeActions` for frequent row operations ([[frequency-of-use]]).
- Android: M3 `ListItem`; swipe-to-dismiss with an undo snackbar ([[components/toast]]).
- Game UI: virtualized scroll lists; focus wraps or stops predictably; selected row has a frame.

**Failure looks like:** Rows where only the title text is clickable. Previews wrapping to 3 lines and breaking rhythm. Time stamps jittering in width. Full-width dark dividers. Unread shown by a faint blue tint only.

**Review checks:**
- [ ] Row is one target ≥ 56px
- [ ] Truncation with ellipsis; full text recoverable
- [ ] Tabular right-aligned meta; inset translucent dividers

Reference test: `~/Documents/github/ui-test/components/list`

**Related:** [[components/card]] · [[components/avatar]] · [[components/badge]]
