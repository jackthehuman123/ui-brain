---
type: concept
description: "Popovers, menus and sheets grow from their trigger or attached edge and return there on close; never from center"
domain: motion
aliases: [transform-origin, anchored animation, scale from trigger, spatial continuity, popover origin]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://www.radix-ui.com/primitives/docs/components/popover
  - https://github.com/emilkowalski/skills
---
# Origin-aware animation

**Rule:** Overlays animate from where they come from. Menus and popovers scale from the side nearest their trigger (and follow collision flips), sheets slide from the edge they attach to, and toasts enter from their stack's edge. Closing reverses to the same origin.

**Why:** The origin tells the user cause and location ("this came from that button"). Center-origin scaling makes every overlay look detached from its trigger.

**Values:**
- Initial scale: **unverified**, ~0.9–0.97 with opacity 0→1. Scaling from 0 (as in Radix's docs example) looks like a pop-in.
- Radix computes the origin from side, align, offsets and collisions and exposes it as `--radix-<component>-content-transform-origin`. *(Radix docs)*
- Duration and easing: [[animation-duration]] (enter ~200 ms, exit shorter), [[easing]] (decelerate on enter).

**Failure looks like:** A dropdown under a top-right button that expands from its own center. A menu flipped above its trigger (collision) that still grows downward. Bottom sheets that fade in place. Modals that zoom from the screen center after a tap in the corner.

**Detect in review:** Record each overlay opening and check which point stays fixed during the scale; it should touch the trigger. In code: `transform-origin` missing (defaults to center) or hardcoded to `top` when placement can flip.

**Implementation:**
- Web: `.menu{transform-origin:var(--radix-dropdown-menu-content-transform-origin)}`, or compute it from the anchor rect. With CSS anchor positioning, set the origin per `position-try` fallback.
- iOS: `.popover` and `.sheet` handle origin; for custom overlays use `.scaleEffect(anchor: .topTrailing)`.
- Android: M3 `DropdownMenu` animates from its anchor. Custom: `TransformOrigin` in `graphicsLayer`.
- Game UI: set the panel's pivot/AnchorPoint to the trigger corner before tweening Size.

**Related:** [[shared-element-transition]] · [[interruptible-animation]] · [[staging]]
