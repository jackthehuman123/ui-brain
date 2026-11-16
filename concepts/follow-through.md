---
type: concept
description: "Gesture-driven motion may overshoot and settle (~80% damping); parts settle a beat apart; taps never bounce"
domain: motion
aliases: [follow through, overlapping action, overshoot, settle, spring damping, bounce]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://developer.apple.com/videos/play/wwdc2018/803/
  - https://developer.apple.com/videos/play/wwdc2023/10158/
---
# Follow-through

**Rule:** Motion that carries momentum (a flicked sheet, a thrown card, a reward landing) may overshoot slightly and settle. Parts of a composite element can settle a beat apart (overlapping action). Motion triggered by a tap, with no momentum, lands without overshoot.

**Why:** Overshoot "rewards momentum" and makes objects feel physical. Unearned bounce on taps feels toy-like and slows the UI.

**Values:**
- Start every spring at **100% damping** (no overshoot). Use ~**80%** only when a gesture carries momentum: Apple Music uses 100% for tap-to-open and 80% for swipe-to-dismiss. *(WWDC18)*
- Tune springs by damping and response, not duration *(WWDC18)*. SwiftUI's `bounce: 0` equals critically damped *(WWDC23)*.
- Overlapping parts: **unverified**, 20–40 ms lag for children (handle, content) behind their container.
- Project the gesture's end point from velocity × deceleration rate before springing there *(WWDC18)*.

**Failure looks like:** Every modal bouncing on open. A flicked sheet that stops dead (no momentum transfer). Overshoot so large that content clips. Child elements lagging so far they look detached.

**Detect in review:** Classify each animation's trigger (tap vs gesture). Taps → critically damped; gestures → spring with velocity hand-off. Check that the release velocity reaches the spring (no snap on release).

**Implementation:**
- Web: Motion `animate(el, {x}, {type:"spring", bounce:0.2, velocity})`. CSS `linear()` can approximate a spring curve for non-gesture overshoot.
- iOS: `.spring(duration: 0.4, bounce: 0.15)` for gestures, `bounce: 0` for taps.
- Android: `spring(dampingRatio = 0.8f)` vs `Spring.DampingRatioNoBouncy`.
- Game UI: overshoot-and-settle (`Back` easing in Roblox/DOTween) for rewards only.

**Related:** [[squash-and-stretch]] · [[interruptible-animation]] · [[easing]] · [[secondary-action]]
