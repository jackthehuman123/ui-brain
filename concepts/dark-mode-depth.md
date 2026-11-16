---
type: concept
description: "In dark mode, raised surfaces are lighter, not darker; shadows barely read, so elevation is shown with lightness"
domain: color
aliases: [dark theme elevation, elevated surface, surface tint, dark mode layering]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://developer.apple.com/design/human-interface-guidelines/dark-mode
  - https://m2.material.io/design/color/dark-theme
  - https://m3.material.io/styles/color/roles
---
# Dark-mode depth

**Rule:** In dark themes, each level of elevation gets a **lighter** surface: page < card < raised control < popover/sheet. Selected or "on top" elements must be lighter than what they sit on. Never invert the light theme's shadows.

**Why:** Shadows are nearly invisible on dark backgrounds, so lightness carries depth. Darker-on-top reads as a hole or a pressed state.

**Values:**
- Apple: two background sets, **base** (dimmer, recedes) and **elevated** (brighter, advances). The system switches to elevated for popovers and sheets automatically. *(Apple HIG)*
- Material 2: a white overlay whose opacity rises with elevation, about 5% at 1dp to 16% at 24dp *(M2 dark theme; Flutter formula `4.5·ln(e+1)+2`%)*. M3 replaces this with tonal roles `surfaceContainerLowest…Highest`. *(M3)*
- OKLCH practice: about +0.04–0.05 L per level (bg .16 → surface .205 → raised .25 in the ayxc test; **unverified** as a general rule).

**Failure looks like:** A segmented-control thumb that's darker than its track, so the selected tab looks sunken (found in test #1). A dark modal identical to the page, held apart only by a shadow. Cards distinguished only by a border.

**Detect in review:** List surface tokens by elevation and confirm L increases monotonically. In screenshots, the selected or "floating" element should be the lighter one. Look for `box-shadow` as the only separation in dark mode.

**Implementation:**
- Web: elevation tokens `--surface-0…3` with rising L; swap them under `prefers-color-scheme: dark`.
- iOS: use semantic colors (`systemBackground`, `secondarySystemBackground`); they resolve to elevated variants automatically.
- Android: M3 `surfaceContainer*` roles.
- Game UI: menus over the 3D world are always "elevated". Use a lighter translucent panel plus a backdrop dim.

**Related:** [[oklch]] · [[alpha-borders]] · [[contrast-ratio]]
