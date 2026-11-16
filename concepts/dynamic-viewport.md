---
type: concept
description: "Size full-screen web layouts with svh (stable) or dvh (live), never 100vh on mobile"
domain: platform-and-environment
aliases: [100vh bug, svh, lvh, dvh, viewport units, mobile browser toolbar]
platforms: [web]
status: draft
last_verified: 2026-11-16
sources:
  - https://web.dev/blog/viewport-units
  - https://developer.mozilla.org/en-US/docs/Web/CSS/length
---
# Dynamic viewport

**Rule:** On mobile web, `100vh` is the *large* viewport (toolbars hidden), so it overflows when they're showing. Use `svh` for "fits on first view" sections such as a hero, `dvh` only for app shells that must track toolbar changes, and `lvh` for backgrounds that should never show a gap.

**Why:** Mobile browsers' address and tool bars expand and retract. Content sized to 100vh hides the CTA behind the toolbar on first load, which is exactly the first-screen content the homepage depends on.

**Values:**
- `svh/lvh/dvh` (and the `vw/vi/vb/vmin/vmax` variants) ship in Chrome/Edge 108, Firefox 101 and Safari 15.4. *(web.dev)*
- `dvh` changes **while scrolling**, so a `dvh`-sized element resizes and reflows. Don't use it for content height on long pages or animate to it. *(web.dev, secondary sources)*

**Failure looks like:** A hero whose primary CTA sits just below the visible area on iPhone Safari until the user scrolls. A full-height app shell with a 70px gap or overflow when the toolbar collapses. A page jittering as the toolbar animates (`dvh` on a large section).

**Detect in review:** Load on a real phone (or a device emulator with dynamic toolbars) and compare the first view with the toolbar expanded and collapsed. In code: `height: 100vh` / `min-height: 100vh` on heroes or shells; JS `window.innerHeight` resize hacks.

**Implementation:**
- Hero: `min-height: min(100svh, 900px)` (as in the ayxc test).
- App shell: `height: 100dvh` with internal scroll regions.
- Fallback for very old engines: declare `100vh` first, then the new unit.
- Combine with [[safe-area]] insets for edge-to-edge layouts.

**Related:** [[safe-area]] · [[layout-shift]]
