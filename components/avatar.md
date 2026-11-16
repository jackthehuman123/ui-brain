---
type: component
description: "Image with initials fallback, hue from name at fixed L/C (every hue passes), status by shape + text, groups cap with +N"
aliases: [avatars, profile picture, user image, initials, avatar group, facepile]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html
---
# Avatar

**Use when:** identifying a person or entity next to their content. **Don't use when:** decorating content that isn't about a person; use an icon.

**Anatomy:** circle → image **or** initials → optional status indicator → group: overlapping avatars + "+N" overflow.

**Required states:** image · fallback (initials) · loading · with status (online/away/busy) · in a group.

**Rules:**
- A broken or missing image falls back to 1–2 initials. Never show a broken-image icon.
- Color: hue derived deterministically from the name, with **fixed L and C** per theme, so every hue passes 4.5:1 for the initials → [[oklch-palettes]], [[contrast-ratio]].
- Status differs by shape (filled / hollow / bar) plus text for screen readers, not color alone → [[affordance]].
- Groups show at most ~4 plus a "+N" count (tabular), with the total in the group's accessible name. The overlap is ≤ 25% of the width so initials stay readable → [[tabular-numbers]].
- The overlap ring uses the page color (a cut-out). The status ring sits on the avatar's edge.

**Values:** sizes 24/32/40/56; initials at 40% of the diameter. Light: bg `oklch(.86 .07 h)` / text `oklch(.30 .08 h)`. Dark: bg `oklch(.40 .07 h)` / text `oklch(.94 .03 h)` (every 5° of hue measured ≥ 4.5:1 in component test #3).

**Platform variants:**
- iOS/Android: an async image with a placeholder of the same size; no layout shift on load ([[layout-shift]]).
- Game UI: player avatars carry rank or frame borders. Keep names visible, since avatars alone don't identify people in fast play.

**Failure looks like:** Random colors per render. Yellow avatars with white initials (≈ 1.5:1). Green and red status dots only. Group avatars overlapping 50% so initials are cut. A broken-image glyph.

**Review checks:**
- [ ] Fallback initials on image error
- [ ] All hues pass contrast in both themes
- [ ] Status not color-only; group overflow count and total name

Reference test: `~/Documents/github/ui-test/components/avatar`

**Related:** [[components/list]] · [[components/badge]] · [[oklch-palettes]]
