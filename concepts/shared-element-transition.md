---
type: concept
description: "Morph the one element that persists between views (thumbnail→detail); interruptible, ≤ ~400 ms, reduced-motion fallback"
domain: motion
aliases: [hero transition, view transitions, matchedGeometryEffect, container transform, morph transition]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://web.dev/blog/same-document-view-transitions-are-now-baseline-newly-available
  - https://developer.chrome.com/docs/web-platform/view-transitions
  - https://developer.android.com/develop/ui/compose/animation/shared-elements
---
# Shared element transition

**Rule:** When one element exists in both views (product thumbnail → product hero, avatar → profile), morph that element between its two positions instead of cross-fading whole screens. Use one shared element per transition, keep it interruptible (back gesture mid-flight), and give it a cross-fade fallback for reduced motion.

**Why:** It preserves object constancy: the user sees *what* they tapped become the new screen, so no reorientation is needed.

**Values:**
- Web: same-document View Transitions are Baseline since Oct 2025 (Chrome 111, Safari 18, Firefox 144). Cross-document (`@view-transition`) works in Chrome 126+ and Safari, but not Firefox. *(web.dev, Chrome docs)*
- Duration: **unverified**, ~300–400 ms. It's a large spatial move, at the top of the [[animation-duration]] range.

**Failure looks like:** Several elements morphing at once into a chaotic swirl. The aspect ratio squashing mid-morph (image not cropped consistently). The back gesture freezing until the morph finishes. A morph between elements that aren't the same object.

**Detect in review:** Check that exactly one `view-transition-name` (or matched ID) is shared per navigation, and that it's unique on the page. Swipe back mid-transition. Test with reduced motion on.

**Implementation:**
- Web: `img{view-transition-name: product-42}` then `document.startViewTransition(update)`; `object-fit: cover` on both sides.
- iOS: `.matchedGeometryEffect(id:in:)` within a view; `.navigationTransition(.zoom(sourceID:in:))` for push (iOS 18).
- Android: `SharedTransitionLayout` + `Modifier.sharedElement(...)` (Compose 1.7+).
- Game UI: tween a temporary clone from the source rect to the target rect, then swap in the real element.

**Related:** [[origin-aware-animation]] · [[interruptible-animation]] · [[arcs]] · [[reduced-motion]]
