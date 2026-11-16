---
type: concept
description: "Press and impact feedback: brief scale-down on press, volume-preserving squash on impact; amplitude grows with stakes"
domain: motion
aliases: [exaggerated feedback, exaggeration, juice, press scale, bounce feedback, game feel]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://developer.apple.com/videos/play/wwdc2018/803/
---
# Squash and stretch

**Rule:** Make physical feedback proportional to the stakes. Use a subtle scale-down on press in app UI, and exaggerated, volume-preserving squash and stretch for game rewards, hits and collectibles. Never deform text-heavy elements or anything the user is reading.

**Why:** Deformation sells mass and impact: the button "gives" under the finger, and the coin "lands". Exaggeration (another animation principle) is how game UI communicates importance at a glance.

**Values:**
- App press scale: **unverified**, 0.95–0.98, starting on press (no delay), released with a spring.
- Volume preservation: squash X by k and stretch Y by 1/k (e.g. 1.15 × 0.87) *(geometry)*.
- Game reward pop: **unverified**, overshoot to 1.1–1.25 and then settle; see [[follow-through]].
- Feedback starts on the input frame; see [[animation-duration]].

**Failure looks like:** App buttons that wobble like jelly. Scale applied to a whole card, distorting its text. Feedback that starts after a delay (reads as lag). Game rewards with no impact, so a legendary drop looks the same as a common one.

**Detect in review:** Press-and-hold buttons: they should respond on press, not release. Measure the scale amplitude per element type (UI controls small, rewards large). Check that no text block scales non-uniformly.

**Implementation:**
- Web: `.btn:active{scale:.97}` with `transition: scale 100ms`; on release a spring (Motion).
- iOS: `.scaleEffect(isPressed ? 0.97 : 1)` in a `ButtonStyle`; system buttons already highlight.
- Android: `Modifier.graphicsLayer(scaleX, scaleY)` driven by `interactionSource`.
- Roblox: tween `UIScale.Scale` (not Size), so layout and text stay stable.
- Unity: `transform.localScale` via a spring, plus particles and sound for game juice.

**Related:** [[anticipation]] · [[follow-through]] · [[secondary-action]] · [[affordance]]
