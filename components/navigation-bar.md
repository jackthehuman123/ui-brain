---
type: component
description: "App-level destinations: 3–5 icon+label items, active = filled icon + pill + weight, aria-current, safe-area padding"
aliases: [tab bar, bottom navigation, bottom nav, navigation rail, app bar navigation]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://m3.material.io/components/navigation-bar/overview
  - https://developer.apple.com/design/human-interface-guidelines/tab-bars
---
# Navigation bar

**Use when:** switching between an app's top-level destinations on phones (a bottom bar), with a rail or sidebar on larger screens. **Don't use when:** switching views of one object (use [[components/tabs]]), or for actions (use a toolbar or FAB).

**Anatomy:** bar → items (icon + label + optional badge) → active indicator (pill).

**Required states:** active (`aria-current="page"`) · inactive · pressed · focus-visible · with badge.

**Rules:**
- 3–5 destinations, each with a visible label → [[jakobs-law]], [[frequency-of-use]]. **unverified** source count: M3 and Apple both cap the bar at about 5.
- Active = filled icon + pill + heavier label, not color alone → [[affordance]].
- Bottom padding uses `env(safe-area-inset-bottom)` (or the platform inset API) → [[safe-area]].
- Items ≥ 48dp tall → [[touch-target]]. Badges carry an accessible count → [[components/badge]].
- Order by frequency of use. The bar stays put across destinations (no shifting).

**Values:** 3–5 items; icon 24px; label 12px (**unverified** typical sizes).

**Platform variants:**
- iOS: `TabView` (system tab bar; on iPad it adapts to a sidebar).
- Android: M3 `NavigationBar` (compact) → `NavigationRail` (medium) → drawer (expanded).
- Web: bottom bar on mobile only; a top nav or sidebar on desktop.
- Game UI: top tabs with LB/RB cycling in menus. A bottom bar is a mobile pattern.

**Failure looks like:** Icon-only items. Six or more destinations. An active state differing by color only. A bar sitting under the home indicator. A hamburger hiding the 2–3 most-used sections.

**Review checks:**
- [ ] 3–5 labelled items; exactly one `aria-current`
- [ ] Non-color active state
- [ ] Safe-area padding; items ≥ 48dp

Reference test: `~/Documents/github/ui-test/components/navigation-bar`

**Related:** [[components/tabs]] · [[safe-area]] · [[frequency-of-use]]
