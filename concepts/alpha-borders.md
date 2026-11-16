---
type: concept
description: "Draw dividers and card edges as translucent text-color, not fixed grays; control borders still need 3:1"
domain: color
aliases: [translucent borders, rgba borders, hairline, divider color, border opacity]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://www.w3.org/WAI/WCAG22/Understanding/non-text-contrast.html
---
# Alpha borders

**Rule:** Draw decorative borders and dividers as the foreground color at low alpha (e.g. `oklch(L C H / .12)`), not as a fixed gray, so they adapt to any surface, tint and theme. Borders that **identify a control** must still reach 3:1 ([[contrast-ratio]]).

**Why:** A fixed gray border looks heavy on tinted surfaces and disappears on others. An alpha border darkens or lightens whatever is beneath it by the same perceptual amount, so one token works on cards, images and dark mode.

**Values:**
- Decorative opacity: **unverified**, about 8–14% of text color on light surfaces and 10–16% white on dark (common practice; tune by eye on the busiest surface).
- Input or checkbox boundaries with no other indicator: ≥ 3:1 against the adjacent color. *(WCAG 1.4.11)* Alpha borders at 12% will **fail** this, so use a solid, measured color there.
- Two overlapping alpha borders double the darkening (e.g. a table cell edge plus the row edge).

**Failure looks like:** Card edges that vanish on photos. Gray hairlines that look dirty on a blue-tinted surface. Form fields whose only boundary is a 12% line (about 1.3:1). Doubled lines at table intersections.

**Detect in review:** Fixed-gray border tokens (`#E5E5E5`, `gray-200`) reused on tinted or dark surfaces. Inputs whose border is the decorative token. Zoom into intersections for doubled lines.

**Implementation:**
- Web: `--line: oklch(.22 .02 250 / .12)` in light and `oklch(1 0 0 / .1)` in dark. `border-collapse` or single-side borders in tables.
- iOS: `Color.primary.opacity(0.12)` or `.separator`, which is already translucent and adaptive.
- Android: `MaterialTheme.colorScheme.outlineVariant` for decorative lines; `outline` for control boundaries.
- Game UI: `UIStroke` (Roblox) with `Transparency` ≈ 0.85; Unity Image alpha.

**Related:** [[contrast-ratio]] · [[dark-mode-depth]] · [[concentric-radius]]
