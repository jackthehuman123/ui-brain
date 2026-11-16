---
type: component
description: "Independent choices; label row is the target, mixed state for parents, 3:1 box, glyph not just fill"
aliases: [checkboxes, check box, tick box, indeterminate, select all]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://www.w3.org/WAI/ARIA/apg/patterns/checkbox/
  - https://www.w3.org/WAI/WCAG22/Understanding/non-text-contrast.html
---
# Checkbox

**Use when:** zero or more independent choices, or a single opt-in that's submitted with a form. **Don't use when:** the setting takes effect immediately (use [[components/switch]]) or only one choice is allowed (use [[components/radio]]).

**Anatomy:** box (20px) → label → optional description · group: fieldset + legend · parent "select all" with children.

**Required states:** unchecked · checked · indeterminate (mixed) · focus-visible · disabled · error.

**Rules:**
- The whole label row is the hit area, ≥ 44px tall → [[touch-target]], [[fitts-law]].
- The unchecked box boundary is ≥ 3:1 against its background → [[contrast-ratio]].
- Checked shows a glyph (check, or a dash for mixed), not only a fill color.
- A parent shows mixed when its children differ; toggling the parent sets all children.
- Groups use `fieldset` + `legend`. Errors sit under the group, linked by `aria-describedby`.
- `[hidden]` messages must stay hidden. Author `display` rules override the attribute (component test #3), so add a global `[hidden]{display:none!important}`.

**Values:** box 20px, radius 5px, stroke 1.5px (**unverified**, common practice). The check glyph animates in ≤ 100–200 ms.

**Platform variants:**
- Web: native `<input type=checkbox>` with `appearance:none` for styling keeps keyboard and form behavior for free.
- iOS: no native checkbox. Use a `Toggle` (immediate) or a checkmark list row.
- Android: M3 `Checkbox` / `TriStateCheckbox` with `Modifier.toggleable` on the row.
- Game UI: a checkmark sprite plus a label row as the hit target.

**Failure looks like:** Only the 20px box is clickable. A parent that shows unchecked while some children are on. Light-gray boxes at 1.5:1. Error text visible before any interaction.

**Review checks:**
- [ ] Label row toggles; ≥ 44px tall
- [ ] Mixed state on parents
- [ ] Box ≥ 3:1; checked state shows a glyph

Reference test: `~/Documents/github/ui-test/components/checkbox`

**Related:** [[components/switch]] · [[components/radio]] · [[components/form]]
