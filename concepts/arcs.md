---
type: concept
description: "Long moves (item to cart, FAB to sheet) travel on a curved path; short UI shifts stay straight"
domain: motion
aliases: [moving in arcs, arc motion, curved motion path, fly-to-cart, offset-path]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://developer.mozilla.org/en-US/docs/Web/CSS/offset-path
  - https://m2.material.io/design/motion/customization.html
---
# Arcs

**Rule:** When an element travels a long diagonal distance across the screen (an item flying to the cart, a FAB expanding into a sheet, a collectible flying to the HUD counter), move it along a curved path. Keep short, axis-aligned shifts (lists, tabs, drawers) straight.

**Why:** Natural motion follows arcs; straight diagonal lines look robotic. A curve also makes the destination easier to track.

**Values:**
- Simplest arc: animate x and y with **different easings** (e.g. x ease-out, y ease-in), so the path bends without any path math.
- Material 2 documented "arc motion" for container transforms and FAB moves. *(M2 motion customization)*
- Arc height: **unverified**, ~10–25% of the travel distance. Higher looks like a throw, lower like a slide.
- Duration follows the distance; see [[animation-duration]].

**Failure looks like:** A product thumbnail sliding in a straight diagonal line to the cart icon. Collectibles teleporting to the counter. Arcs on small UI shifts, which look floaty.

**Detect in review:** Identify every motion longer than about a third of the viewport diagonal. Check whether it uses a single easing on a `translate` (straight line) or split axes or a path (arc).

**Implementation:**
- Web: split axes with nested elements (outer `translateX` ease-out, inner `translateY` ease-in), or `offset-path: path('M0,0 Q120,-80 240,0')` with `offset-distance` animated.
- iOS: `.keyframeAnimator` with separate X and Y tracks; `CAKeyframeAnimation` with a path.
- Android: `ArcMode` in keyframes (Compose 1.7+), or animate X and Y with different easings.
- Roblox: tween position along a quadratic Bezier stepped in `RenderStepped`. Unity: DOTween `DOPath` with `PathType.CatmullRom`.

**Related:** [[shared-element-transition]] · [[easing]] · [[secondary-action]]
