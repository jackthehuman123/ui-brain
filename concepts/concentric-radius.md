---
type: concept
description: "Nested corners share a center: inner radius = outer radius − gap; go square when the result is ≤ 0"
domain: layout-and-spacing
aliases: [nested radius, inner radius, concentric corners, ConcentricRectangle, border radius nesting]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://developer.apple.com/documentation/swiftui/concentricrectangle
---
# Concentric radius

**Rule:** When a rounded shape sits inside another, make the corners concentric: `inner = outer − gap`, where gap is the padding between their edges. If that's ≤ 0, use a square (or a 1–2px) corner.

**Why:** The same radius inside and out makes the gap thicker at the corners than along the edges, so the inner shape looks pinched and misplaced.

**Values:**
- `inner = max(outer − padding, 0)`. Example: a card with radius 20 and padding 8 gets an inner image radius of 12 *(geometry)*.
- Apple ships this as a primitive: `ConcentricRectangle` derives each corner from the container shape (iOS 26+). *(Apple docs)*
- Corners on the screen edge: match the device's display corner, not your outer radius (use the platform API).

**Failure looks like:** A segmented-control thumb with the same radius as its track, which looks bulged at the corners. Image cards with 16px corners inside 16px cards with 8px padding. Buttons in a sheet whose corners fight the sheet's.

**Detect in review:** Zoom into nested corners and check that the gap stays constant around the curve. In code: one `--radius` token applied at every nesting level; padding changed without updating the inner radius.

**Implementation:**
- Web: `.card{--r:20px;--p:8px;border-radius:var(--r);padding:var(--p)} .card>img{border-radius:max(calc(var(--r) - var(--p)),0px)}`
- iOS: `.containerShape(.rect(cornerRadius: 24))` on the parent and `ConcentricRectangle()` children (iOS 26+). Earlier, compute manually.
- Android: derive from shape tokens, e.g. `RoundedCornerShape(outer - padding)`.
- Roblox: `UICorner.CornerRadius` (UDim); compute it from the parent's corner minus `UIPadding`. Unity: 9-slice sprites per nesting level.

**Related:** [[optical-center]] · [[alpha-borders]]
