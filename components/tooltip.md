---
type: component
description: "Short hint: focus shows at once, hover after delay, Escape dismisses, hoverable, no controls inside"
aliases: [tooltips, hint, title tooltip, toggletip, hover text]
platforms: [web, desktop]
status: draft
last_verified: 2026-11-16
sources:
  - https://www.w3.org/WAI/ARIA/apg/patterns/tooltip/
  - https://www.w3.org/WAI/WCAG22/Understanding/content-on-hover-or-focus.html
---
# Tooltip

**Use when:** naming icon-only controls or adding a short hint (shortcut, limit) on pointer and keyboard UIs. **Don't use when:** the content is essential or long, contains links or buttons (use a popover or toggletip), or the UI is touch-first (there's no hover; show the label instead).

**Anatomy:** trigger → tooltip (`role="tooltip"`, text + optional shortcut) → arrow.

**Required states:** hidden · showing (delay) · shown · dismissed (Escape).

**Rules:**
- Focus shows it immediately; hover shows it after a short delay; blur and pointer-leave hide it.
- WCAG 1.4.13: **dismissible** (Escape, without moving focus), **hoverable** (the pointer can move onto it), **persistent** (stays until dismissed or no longer relevant).
- Icon-only buttons: the tooltip can be the accessible name (`aria-labelledby`). Otherwise link it with `aria-describedby`.
- It grows from the trigger side → [[origin-aware-animation]]. Fades only under reduced motion → [[reduced-motion]].
- No interactive content inside. Max width ~32ch → [[line-length]].

**Values:** hover delay ~400 ms, hide grace ~120 ms (**unverified**, tuned to avoid flicker). Enter ~150 ms, exit ~100 ms.

**Platform variants:**
- macOS/Windows: the native tooltip (`.help()` in SwiftUI). Fluent and AppKit have their own delays.
- iOS/Android: no hover. Long-press shows a tooltip for icon buttons (M3 `TooltipBox`), but visible labels are better.
- Game UI: hold-to-inspect item tooltips, positioned so they never cover the focused item.

**Failure looks like:** A tooltip that vanishes when the pointer moves onto it. One that appears instantly on every pass, flickering. The only way to learn what an icon does on touch. Links inside a tooltip.

**Review checks:**
- [ ] Focus shows; Escape hides without moving focus
- [ ] Hover delay; hoverable
- [ ] Icon-only triggers named; no interactive content

Reference test: `~/Documents/github/ui-test/components/tooltip`

**Related:** [[components/button]] · [[affordance]] · [[origin-aware-animation]]
