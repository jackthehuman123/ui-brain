---
type: inbox
---
# Candidate concepts (not yet written; awaiting approval)

One line each on why it earns a note. `promote <name>` to write one.

## Typography
- **optical-size**: variable `opsz` axes (Inter, SF, Roboto Flex) change stroke contrast and spacing by size; most UIs leave the axis at a default that's wrong for display or caption text.
- **type-scale**: modular ratio + fluid `clamp()` steps with per-step tracking and leading; agents default to ad-hoc sizes.
- **text-truncation**: when to ellipsize vs wrap vs line-clamp, and the full text recovery (tooltip, expand); truncated prices and names are a common silent failure.
- **hyphenation**: `hyphens: auto` with `lang` for narrow columns and German/Dutch strings; prevents rivers and overflow in cards.

## Color
- **state-layers**: M3-style hover, focus and pressed overlays at fixed opacities over any surface; one rule instead of per-component hover colors.
- **semantic-color-tokens**: role-based names (surface, on-surface, danger) over palette names, so themes and dark mode swap cleanly.
- **color-blindness**: never encode state by hue alone; red/green pairs fail for ~8% of men. A checkable rule with simulation tools.

## Layout and spacing
- **spacing-scale**: a 4/8-pt step scale with rules for inner ≤ outer spacing (proximity); agents mix arbitrary px values.
- **container-queries**: components that adapt to their container instead of the viewport; fixes cards that break in sidebars.
- **density**: compact/comfortable modes for data-heavy UIs (tables, dashboards), with minimum row heights tied to touch target.

## Motion
- **scroll-driven-animation**: CSS `animation-timeline: scroll()/view()` performance rules and when scroll-linked motion helps vs nauseates.
- **haptics**: iOS/Android haptic feedback pairing with visual feedback (success, warning, selection); often missing or overused.

## Interaction and state
- **skeleton-screens**: sized like the final content, a shimmer optional, shown only past ~300 ms; prevents layout shift and flash.
- **empty-states**: first-use vs no-results vs cleared, each with a next action; agents leave blank panels.
- **error-messages**: what happened + why + how to fix, placed at the source; ties form, toast and full-page errors together.
- **undo-over-confirm**: prefer undo for reversible destructive actions over "Are you sure?" dialogs that users click through.
- **von-restorff-effect**: the isolation effect; one visually distinct item (recommended plan, primary CTA) is remembered. Pairs with Hick's law.
- **serial-position-effect**: first and last items in lists and navs get the most recall; put key items at the ends.
- **peak-end-rule**: experiences are judged by their peak and their end; invest polish in success states and checkout completion.
- **goal-gradient-effect**: progress indicators that show closeness to completion increase completion (onboarding, checkout, quests).

## Platform and environment
- **input-modality**: `(hover: hover)` / `(pointer: coarse)` media queries and per-modality hit sizes; hover-only affordances break on touch.
- **gamepad-navigation**: focus order, focus visuals and confirm/cancel mapping for console and Roblox 10-foot UI.
- **right-to-left**: mirroring rules (icons that flip vs don't, logical CSS properties) for Arabic and Hebrew.

## Accessibility
- **focus-visible**: focus indicator size and contrast (WCAG 2.4.7, 2.4.11/2.4.13) and never removing outlines without a replacement.
- **text-scaling**: Dynamic Type / Android font scale / 200% browser zoom (WCAG 1.4.4) without clipping or truncating essentials.
