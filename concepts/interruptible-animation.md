---
type: concept
domain: motion
aliases: [retargeting, interruptible transitions, redirectable animation, animation interruption]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://drafts.csswg.org/css-transitions-2/
  - https://developer.apple.com/videos/play/wwdc2023/10158/
  - https://developer.apple.com/videos/play/wwdc2018/803/
  - https://developer.android.com/develop/ui/compose/animation/advanced
  - https://create.roblox.com/docs/reference/engine/classes/TweenService
  - https://docs.unity3d.com/ScriptReference/Mathf.SmoothDamp.html
---
# Interruptible animation

**Rule:** If the user can trigger an animation again before it finishes (toggle, drawer, sheet, hover, drag release), it must retarget from its **current on-screen value**, and keep its velocity where the platform allows. It must never restart from the beginning, queue behind the running animation, or ignore input while it plays.

**Why:** Users act faster than animations finish. A snap back to the start, an ignored tap, or a queue of animations that keeps playing after the user stopped all read as lag or a bug. Retargeting keeps the UI under the user's direct control. *(WWDC18 "Designing Fluid Interfaces")*

**Values:**
- Input lockout during an animation: **0 ms**. Handlers never early-return on `isAnimating`.
- CSS transitions retarget by default. Reversing a partly finished transition shortens the reverse duration in proportion to progress (the "reversing shortening factor"). *(CSS Transitions L2 §3.1)* `@keyframes` animations do **not** retarget; they restart.
- SwiftUI: an interrupted spring merges, keeping its current velocity as it heads to the new target. Timing-curve animations combine additively instead. *(WWDC23 10158)*
- Compose: a new `Animatable.animateTo` cancels the running one and keeps its velocity. Velocity stays continuous only with `spring` specs. *(Android docs)*
- Roblox: a new tween on the same property cancels the old one. *(TweenService docs)* It starts from the current value, but tweens take no starting velocity, so each retarget restarts the easing curve from rest. That's inferred from the API, not stated in the docs.

**Failure looks like:** A quickly re-clicked toggle jumps back to its start position and replays. Taps on a menu are ignored while it opens. Hovering on and off several times leaves a queue of fades that keeps playing. A sheet released mid-drag jumps to a fixed position before animating.

**Detect in review:**
- Code: open/close state driven by `@keyframes` instead of `transition`. Restart tricks (removing a class, forcing a reflow, re-adding it). `if (isAnimating) return`. `pointer-events: none` during a transition. Roblox code that resets `.Position = startPos` before `:Play()`. Easing curves (not springs) on gesture release.
- Manual: spam the trigger 5× quickly. Reverse direction halfway through a drag. Release a drag mid-fling. Each should move continuously, with no jumps.

**Implementation:**
- Web: use `transition` for state changes. For JS, use the Web Animations API: read the current value via `getComputedStyle` (or `commitStyles()`), then animate from there. Springs: Motion/Framer `animate()` keeps velocity.
- iOS: SwiftUI `withAnimation(.spring)` (springs are the default and merge). UIKit: `UIViewPropertyAnimator` (`isReversed`, `continueAnimation(withTimingParameters:durationFactor:)`).
- Android: `Animatable` + `spring()`, or `animate*AsState`. Pass the fling velocity into `animateTo(initialVelocity = …)` only right after a gesture.
- Roblox: keep one tween per property, create a new `TweenInfo` from the current value, and prefer `Quad`/`Out` easing so a restart from rest isn't jarring. For drag release, drive a spring in `RenderStepped`.
- Unity: `Mathf.SmoothDamp` / `Vector3.SmoothDamp` carry `ref currentVelocity` across retargets.

**Related:** [[origin-aware-animation]] · [[shared-element-transition]] · [[stagger]] · [[optimistic-update]]
