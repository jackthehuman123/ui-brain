---
type: component
description: "Counts cap at 99+, tabular, out of layout, full count in name; status pills = icon + text; brief bump"
aliases: [badges, count badge, notification dot, status pill, chip status, tag]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://m3.material.io/components/badges/overview
---
# Badge

**Use when:** a count or "new" marker on a control (inbox, cart), or a short status on an item (Shipped, Failed). **Don't use when:** the information needs action (use [[components/toast]] or inline messaging), or for decoration.

**Anatomy:** count badge (anchored to an icon's corner) · dot badge · status pill (icon + text).

**Required states:** hidden (0) · count · capped (99+) · dot · status variants (neutral, info, success, warning, danger).

**Rules:**
- Counts cap at "99+". The **full** count goes in the parent's accessible name ("Inbox, 120 unread"); the badge itself is `aria-hidden`.
- Positioned absolutely, so badges never change their anchor's layout → [[layout-shift]]. Tabular digits → [[tabular-numbers]].
- A 2px ring in the surface color separates the badge from its icon.
- Status pills = icon + text, never color alone; soft backgrounds with ≥ 4.5:1 text in both themes → [[contrast-ratio]], [[oklch-palettes]].
- A count change can bump the badge briefly (≤ 1.2×, ≤ 250 ms), skipped under reduced motion → [[secondary-action]], [[reduced-motion]].
- Zero hides the badge rather than showing "0".

**Values:** height 20px (count) / 10px (dot), with min-width equal to the height so single digits stay circular. Bump 1.15× over 180 ms (**unverified**).

**Platform variants:**
- iOS: `.badge(_:)` on tab items and list rows.
- Android: M3 `BadgedBox` + `Badge`.
- Game UI: "new item" dots on menu tabs, cleared when viewed; never stack more than one badge per icon.

**Failure looks like:** "1,284" stretching across the icon. A badge that pushes neighboring icons. A red "Failed" pill with no icon. Badges announcing as stray numbers to screen readers. A badge bouncing constantly.

**Review checks:**
- [ ] 99+ cap; full count in the accessible name
- [ ] Out of layout; tabular digits
- [ ] Status pills have an icon + text and pass contrast in both themes

Reference test: `~/Documents/github/ui-test/components/badge`

**Related:** [[components/navigation-bar]] · [[secondary-action]] · [[tabular-numbers]]
