---
type: concept
description: "Design and code animation as transitions between named states (key poses); generate the in-betweens, never hand-sequence"
domain: motion
aliases: [pose to pose, key poses, keyframes, state-driven animation, straight ahead, declarative animation]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://developer.android.com/develop/ui/compose/animation/value-based
  - https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_transitions/Using_CSS_transitions
---
# Pose to pose

**Rule:** Define every UI animation as a transition between **named states** (closed/open, idle/pressed/loading/done), each fully specified as a "key pose". The engine generates the in-betweens. Use frame-by-frame or procedural ("straight-ahead") motion only for particles, physics and ambient effects.

**Why:** State-driven animation can be interrupted, reversed and tested, because there's always a defined pose to retarget to. Imperative chains ("move 20px, then wait, then fade") break when input arrives mid-sequence and drift out of sync with real state.

**Values:**
- Each animated component documents its states with their property values (position, scale, opacity, color) plus the transition spec between pairs (duration, easing). See [[animation-duration]] and [[easing]].
- A design handoff with 2 states (start/end) is enough for most UI; add an intermediate pose only for overshoot or multi-step reveals.

**Failure looks like:** Chained `setTimeout` animation sequences that leave half-finished states when the user acts. Motion specs delivered as a video with no state values. Animations whose end state differs from the component's static design.

**Detect in review:** For each animation, can you name its start and end states, and do those match a static design frame? In code: imperative sequences (`setTimeout` chains, nested `.then()` tweens, Roblox `Tween.Completed:Wait()` chains for UI state) instead of animating to a state.

**Implementation:**
- Web: toggle classes or data attributes (`[data-state=open]`) with CSS transitions; Motion `variants`.
- iOS: SwiftUI animates state changes (`withAnimation { isOpen.toggle() }`); `PhaseAnimator` for multi-pose sequences.
- Android: `updateTransition(targetState)` with `animateFloat` per property.
- Roblox: one tween per property to the state's target values; cancel and retarget on state change.
- Unity: Animator states plus transitions.

**Related:** [[interruptible-animation]] · [[easing]] · [[anticipation]]
