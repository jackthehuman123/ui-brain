---
type: concept
description: "Swap icons in place (copy→check, play→pause) with a short blur+scale+opacity crossfade, not a hard cut or slide"
domain: iconography-and-visual-detail
aliases: [icon swap, icon morph, content transition, symbol replace, copy to check, state icon change]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://developer.apple.com/documentation/symbols/replacesymboleffect
---
# Blurred icon swaps

**Rule:** When an icon changes state in place (copy → check, play → pause, menu → close, bookmark → bookmarked), crossfade the two with a brief blur and slight scale, so it reads as one object changing rather than two objects trading places.

**Why:** A hard cut is easy to miss, so the user doesn't notice the confirmation. Sliding or rotating swaps imply movement that didn't happen. Blur masks the shape difference during the overlap.

**Values:**
- Duration: ~**100–200 ms** (feedback range; see [[animation-duration]]).
- Blur: **unverified**, 2–4px at the midpoint. Scale: **unverified**, 0.8–0.9 → 1 for the incoming icon.
- Confirmation states (check after copy) revert after **unverified** ~1.5–2 s; never revert while the pointer is still on it.
- Apple ships this as a system effect: `.contentTransition(.symbolEffect(.replace))`. *(Apple docs)*

**Failure looks like:** A copy button whose check appears so abruptly users click again. Two icons visibly overlapping as sharp shapes mid-transition. Icons that slide sideways for a state change. A swap that shifts layout because the icons differ in width.

**Detect in review:** Step through the swap frame by frame: at the midpoint both shapes should be soft, not two crisp silhouettes. Check that the container size stays fixed during the swap.

**Implementation:**
- Web: stack both icons in one grid cell (`display:grid;> *{grid-area:1/1}`) and transition `opacity, filter: blur(), scale` on state. Set a fixed container size.
- iOS: `Image(systemName: copied ? "checkmark" : "doc.on.doc").contentTransition(.symbolEffect(.replace))`.
- Android: `AnimatedContent(targetState){…}` with `fadeIn + scaleIn togetherWith fadeOut + scaleOut`; on API 31+ `Modifier.blur`.
- Game UI: crossfade two ImageLabels with a scale tween; skip the blur on low-end devices.

**Related:** [[matched-icon-weight]] · [[secondary-action]] · [[interruptible-animation]]
