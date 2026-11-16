---
type: concept
description: "Retarget animations from the current value and velocity; never restart, queue or lock input; springs for gestures"
domain: motion
aliases: [retargeting, interruptible transitions, redirectable animation, animation interruption]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://developer.apple.com/videos/play/wwdc2018/803/
  - https://developer.apple.com/videos/play/wwdc2023/10158/
  - https://drafts.csswg.org/css-transitions-2/
  - https://developer.android.com/develop/ui/compose/animation/advanced
  - https://create.roblox.com/docs/reference/engine/classes/TweenService
---
# Interruptible animation

**Rule:** New input retargets a running animation from its **current on-screen value**, keeping velocity where possible. Never restart, queue, or ignore input while it plays. Every property that changes with the state must animate, or the interruption jumps.

**Why:** "Thought and gesture happen in parallel." Lockouts and replays read as lag. *(WWDC18)*

**Values:**
- Input lockout: **0 ms**. *(WWDC18)*
- CSS `transition` retargets, and reversals shorten in proportion to progress *(CSS Transitions L2)*. `@keyframes` restart, so use them only for loops.
- SwiftUI springs merge and keep velocity *(WWDC23)*. A new Compose `animateTo` keeps velocity, which stays continuous with `spring` *(Android docs)*.
- Roblox: a new tween cancels the old one, and tweens have no velocity input *(TweenService docs)*. Use `Out` easing.
- Gesture springs: see [[follow-through]] for damping.

**Failure looks like:** A re-clicked toggle snaps back and replays. Ignored taps while a menu opens. Hover fades queue up. A panel jumps 3–4px on reversal because padding toggled instantly (ayxc test).

**Detect in review:** `@keyframes` driving open/close; `if (isAnimating) return`; `pointer-events:none` during transitions; any property that changes with the state class but isn't in `transition`.
- Test: pause the transition via `el.getAnimations()` → `currentTime = 120`, trigger the opposite state, then assert the start value equals the paused value and the duration is shorter (`ui-test/tools/interrupt-test.html`). Headless virtual time never advances transitions, so call `finish()` before asserting end states.

**Implementation:**
- Web: `transition` for two-state UI; the Web Animations API or a spring library for gestures.
- iOS: `withAnimation(.spring)`; `UIViewPropertyAnimator`.
- Android: `Animatable` + `spring()`.
- Unity: `SmoothDamp` with `ref velocity`.

**Related:** [[easing]] · [[animation-duration]] · [[follow-through]] · [[origin-aware-animation]]
