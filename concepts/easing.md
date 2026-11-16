---
type: concept
description: "Enter ease-out, exit ease-in, on-screen moves ease-in-out; linear only for loops; springs for gestures"
domain: motion
aliases: [slow in and slow out, slow in slow out, timing function, cubic-bezier, ease-out, ease-in, deceleration curve]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://developer.mozilla.org/en-US/docs/Web/CSS/easing-function
  - https://m3.material.io/styles/motion/easing-and-duration/tokens-specs
  - https://github.com/emilkowalski/skills
---
# Easing

**Rule:** Elements **entering** decelerate (ease-out), elements **leaving** accelerate (ease-in), and elements moving within the screen ease in and out. Use linear only for continuous motion (spinners, progress, marquee). Anything released from a gesture uses a spring.

**Why:** Real objects speed up and slow down ("slow in, slow out"). Ease-out puts the motion's speed at the start, so UI feels responsive, and it settles gently where the eye lands.

**Values:**
- Standard (on-screen): `cubic-bezier(0.2, 0, 0, 1)`. Decelerate (enter): `cubic-bezier(0.05, 0.7, 0.1, 1)`. *(Material 3 tokens via secondary sources; official names vary, so check m3.material.io before citing)*
- CSS keywords: `ease` = `cubic-bezier(0.25, 0.1, 0.25, 1)`; `ease-out` = `(0, 0, 0.58, 1)`. *(MDN)* The keywords are mild; custom curves read snappier.
- The classic mistake is `ease-in` on an entering element: it starts slow and feels laggy. *(Emil Kowalski)*

**Failure looks like:** Menus that creep open and then snap. Linear slides that look mechanical. A bouncy spring on a plain tap (bounce belongs to gestures). Exits slower than entrances.

**Detect in review:** Grep for `ease-in` on enter/open states, `linear` outside loaders, and missing timing functions (the default `ease` everywhere). Step through frames: an entering element should cover most of its distance in the first third of the duration.

**Implementation:**
- Web: easing tokens `--ease-out: cubic-bezier(0.05,0.7,0.1,1); --ease-standard: cubic-bezier(0.2,0,0,1)`.
- iOS: SwiftUI defaults to springs; use `.snappy` / `.smooth` presets, or `.spring(duration:bounce: 0)` for taps.
- Android: `FastOutSlowInEasing`, M3 `MotionScheme` tokens.
- Roblox: `Enum.EasingStyle.Quint/Quart` + `EasingDirection.Out` for enter; `In` for exit.
- Unity: AnimationCurve presets, or DOTween `Ease.OutQuint`.

**Related:** [[animation-duration]] · [[interruptible-animation]] · [[follow-through]] · [[arcs]]
