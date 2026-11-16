---
type: component
description: "One choice from 2–5 visible options; whole card is the target, recommended option marked, dot + border not color alone"
aliases: [radio button, radio group, option cards, plan picker, single choice]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://www.w3.org/WAI/ARIA/apg/patterns/radio/
---
# Radio

**Use when:** exactly one choice from 2–5 options that benefit from being compared side by side. **Don't use when:** there are more options (use [[components/select]]), or there's a single binary (use [[components/checkbox]] or [[components/switch]]).

**Anatomy:** fieldset + legend → options (circle + label + optional description, price or meta). Card variant: the whole card is the label.

**Required states:** unselected · selected · focus-visible · disabled · error (group level).

**Rules:**
- Same `name` per group, with one option preselected when a sensible default exists → [[hicks-law]] (mark a "Recommended" option).
- Arrow keys move the selection within the group (native radios do this). Tab enters and leaves the group as one stop.
- Selected = inner dot + accent border + tint, not color alone → [[affordance]].
- The whole row or card is the hit area → [[touch-target]]. The circle boundary is ≥ 3:1 → [[contrast-ratio]].
- Prices and numbers right-aligned with tabular digits → [[tabular-numbers]].

**Values:** 2–5 options per group (beyond that, use a select). Circle 20px with a 10px dot.

**Platform variants:**
- Web: native `<input type=radio>` styled with `appearance:none`.
- iOS: no native radio. Use a list with checkmarks, or a segmented `Picker` for 2–4 short options.
- Android: M3 `RadioButton` with `Modifier.selectable(role = Role.RadioButton)` on the row.
- Game UI: option cards with a clear selected frame; controller left/right moves the selection.

**Failure looks like:** No preselection on a choice that has a sensible default. Only the circle clickable on large cards. Selection shown by a faint tint only. 8 radio options in a long list.

**Review checks:**
- [ ] One checked per group; whole card or row selects
- [ ] Selected state has a dot + border, not just color
- [ ] 2–5 options; recommended marked when relevant

Reference test: `~/Documents/github/ui-test/components/radio`

**Related:** [[components/select]] · [[hicks-law]] · [[components/checkbox]]
