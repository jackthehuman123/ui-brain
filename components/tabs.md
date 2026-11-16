---
type: component
description: "Switch peer views in place: APG roles, arrows+Home/End with roving tabindex, transform-only indicator that retargets"
aliases: [tab bar top, tablist, segmented tabs, tab panel]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://www.w3.org/WAI/ARIA/apg/patterns/tabs/
---
# Tabs

**Use when:** switching between peer views of the same object (Overview / Issues / Settings) without leaving the page. **Don't use when:** destinations are app sections (use [[components/navigation-bar]]), or steps must happen in order (use a stepper).

**Anatomy:** tablist → tabs (label + optional count) → selection indicator → tabpanels.

**Required states:** selected · unselected · hover · focus-visible · disabled (rare).

**Rules:**
- APG: `role=tablist/tab/tabpanel`, `aria-selected`, `aria-controls`, `aria-labelledby`. ←/→ move with wrap-around, Home and End jump, and Tab leaves the list (roving `tabindex`). Use automatic activation when panels render instantly.
- The indicator moves with `transform` (translate + scaleX), never `left`/`width`, and retargets on rapid switches → [[layout-shift]], [[interruptible-animation]].
- Counts use tabular digits → [[tabular-numbers]]. Tabs are ≥ 44px tall → [[touch-target]].
- 2–5 visible tabs. Beyond that, scroll with [[masked-edges]] or group with [[progressive-disclosure]].

**Values:** indicator 2–3px thick, ~200 ms standard easing ([[easing]]).

**Platform variants:**
- iOS: segmented `Picker` for 2–4 short in-page views. Top tabs aren't an iOS convention ([[jakobs-law]]).
- Android: M3 `PrimaryTabRow` / `SecondaryTabRow`.
- Game UI: shoulder buttons (LB/RB) cycle tabs; show the button glyphs at the ends of the tab row.

**Failure looks like:** Every tab is a Tab stop. An indicator that animates `left`/`width` (layout thrash) or snaps back on a double switch. Tabs used as page navigation. 9 tabs squeezed to fit.

**Review checks:**
- [ ] Arrow/Home/End keys; only the selected tab is tabbable
- [ ] Indicator lands exactly under the tab; transform-only; interruptible
- [ ] Only the selected panel is shown

Reference test: `~/Documents/github/ui-test/components/tabs`

**Related:** [[components/navigation-bar]] · [[interruptible-animation]] · [[jakobs-law]]
