---
type: concept
description: "Honor reduce-motion: replace movement, zoom and parallax with fades or instant changes; keep feedback, drop decoration"
domain: accessibility
aliases: [prefers-reduced-motion, reduce motion, vestibular, motion sensitivity, ReducedMotionEnabled]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://www.w3.org/WAI/WCAG22/Understanding/animation-from-interactions.html
  - https://www.w3.org/WAI/WCAG22/Understanding/pause-stop-hide.html
  - https://create.roblox.com/docs/production/publishing/accessibility
---
# Reduced motion

**Rule:** When the user asks for reduced motion, **reduce, don't remove**. Replace movement, scaling, parallax and zoom with opacity fades or instant state changes, keep feedback (state changes stay visible), and drop purely decorative motion. Auto-playing motion must be pausable regardless.

**Why:** Large movements, parallax and zooms trigger vestibular symptoms (nausea, dizziness). Removing *all* feedback hurts comprehension, so a fade still says "this changed".

**Values:**
- WCAG 2.3.3 (AAA): motion triggered by interaction can be disabled unless essential. *(W3C)*
- WCAG 2.2.2 (A): auto-moving content lasting **> 5 s** needs pause, stop or hide. *(W3C)*
- Roblox: `GuiService.ReducedMotionEnabled` (client-only, read-only); set the TweenInfo time to 0 or fade instead. *(Roblox docs)*

**Failure looks like:** Parallax heroes and zoom transitions ignoring the setting. A reduced-motion mode that also hides focus and state changes. Shared-element morphs still flying across the screen. Auto-advancing carousels with no pause.

**Detect in review:** Turn on the OS setting (macOS/iOS Reduce Motion, Android Remove animations, Roblox Reduce Motion) and walk the key flows; anything that still translates, zooms or parallaxes is a finding. In code: animations not wrapped by `prefers-reduced-motion` handling.

**Implementation:**
- Web: `@media (prefers-reduced-motion: reduce){ .sheet{transition:opacity 150ms} .parallax{transform:none} }`. Prefer opting *in* to motion under `no-preference`.
- iOS: `@Environment(\.accessibilityReduceMotion)`; swap `.move` for `.opacity` transitions.
- Android: read the animator duration scale (Settings › Remove animations) and provide fade alternatives. Compose behavior varies by API; test with the setting on.
- Unity: expose a Reduce Motion option in settings (there's no OS hook on most platforms).

**Related:** [[stagger]] · [[shared-element-transition]] · [[staging]] · [[animation-duration]]
