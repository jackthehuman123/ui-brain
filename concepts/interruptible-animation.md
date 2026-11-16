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
  - https://docs.unity3d.com/ScriptReference/Mathf.SmoothDamp.html
  - https://emilkowal.ski/ui/great-animations
---
# Interruptible animation

**Rule:** Every state animation must be redirectable: a new input retargets it from its **current on-screen value**, keeping velocity where the platform allows. It must never restart from the beginning, queue up, or lock out input. Use springs for anything a gesture hands off to.

**Why:** "Thought and gesture happen in parallel." A redirectable UI lets users layer inputs at the speed of thought, and any timer or lockout feels like lag. *(WWDC18 Designing Fluid Interfaces)*

**Values:**
- Input lockout during an animation: **0 ms**. "Everything needs to respond instantly." *(WWDC18)*
- Spring tuning: start at **100% damping** (no overshoot). Use about **80%** only when the motion carries the momentum of a gesture (Apple Music: tap-to-open 100%, swipe-dismiss 80%). Tune damping and response, not duration. *(WWDC18)*
- Gesture release: hand the gesture's velocity to the spring, and project the end point from velocity × deceleration rate (reuse `UIScrollView.DecelerationRate`) instead of snapping to the nearest position. *(WWDC18)*
- CSS: `transition` retargets, and a reversal is shortened in proportion to progress *(CSS Transitions L2 "reversing shortening factor")*. `@keyframes` runs to completion and restarts when re-triggered, so keep it for loops and multi-step motion only.
- SwiftUI: an interrupted spring merges, keeping its current velocity. Timing curves combine additively. *(WWDC23 10158)*
- Compose: a new `animateTo` cancels the running animation and keeps its velocity, with continuous velocity guaranteed only for `spring`. *(Android docs)*
- Roblox: a new tween on the same property cancels the old one. *(TweenService docs)* Tweens can't take a starting velocity, so each retarget starts the easing from rest (inferred from the API).

**Failure looks like:** A quickly re-clicked toggle snaps to its start and replays. Taps ignored while a menu opens. A queue of hover fades that keeps playing after the pointer leaves. A sheet released mid-flick jumps to a fixed position, or bounces after a plain tap.

**Detect in review:**
- Code: open/close driven by `@keyframes`. Restart tricks (remove class, force reflow, re-add). `if (isAnimating) return`. `pointer-events:none` during a transition. Easing curves (not springs) on drag release. Roblox code that resets `.Position` before `:Play()`. Bouncy springs on non-gesture taps.
- Manual: trigger it 5× quickly. Reverse a drag halfway. Flick, then grab again mid-flight. Motion must stay continuous with no jumps.

**Implementation:**
- Web: `transition` for two-state UI. For programmatic motion, the Web Animations API (read the current value, then animate from it). For velocity-preserving gestures, a spring library (Motion `animate()`).
- iOS: SwiftUI `withAnimation(.spring)` (the default, and springs merge). UIKit `UIViewPropertyAnimator` (`isReversed`, `continueAnimation`).
- Android: `Animatable` + `spring()`. Pass `initialVelocity` only right after a fling.
- Roblox: one tween per property, built from the current value. Use `Out` easing so a restart from rest isn't jarring. For drag release, step a spring in `RenderStepped`.
- Unity: `Mathf/Vector3.SmoothDamp` carries `ref currentVelocity` across retargets.

**Related:** [[origin-aware-animation]] · [[shared-element-transition]] · [[stagger]] · [[optimistic-update]]
