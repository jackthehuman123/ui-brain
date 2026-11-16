---
type: component
description: "One primary per view, verb labels, ≥44px, press feedback on press, loading keeps width, explained disabling"
aliases: [buttons, CTA, call to action, icon button, primary button, ghost button]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://www.w3.org/WAI/ARIA/apg/patterns/button/
  - https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html
---
# Button

**Use when:** triggering an action (submit, save, open). **Don't use when:** navigating to a page (use a link styled as needed), or toggling a setting that applies immediately (use [[components/switch]]).

**Anatomy:** container → optional leading icon → label (verb + object) → optional trailing icon. Variants: primary · secondary (outlined) · tonal · ghost · destructive · icon-only.

**Required states:** default · hover · focus-visible · pressed · loading · disabled (`disabled` or `aria-disabled`).

**Rules:**
- One primary button per view or group → [[hicks-law]], [[staging]].
- Height ≥ 44px; icon-only buttons are 44×44 with an `aria-label` → [[touch-target]].
- Press feedback starts on press (scale ~0.97), not on release → [[squash-and-stretch]].
- Loading: keep the label in layout (invisible), overlay a spinner, set `aria-busy` and ignore repeat clicks → [[layout-shift]], [[doherty-threshold]].
- If the reason for disabling is useful, use `aria-disabled="true"` (still focusable) and explain on activation. Use `disabled` only when no explanation is needed.
- Icon stroke matches the label weight → [[matched-icon-weight]]. Labels never wrap.

**Values:** heights 44 (default) and 52 (large). Press scale 0.97 (**unverified**, see [[squash-and-stretch]]). Disabled opacity ~0.45 (exempt from contrast; **unverified** value).

**Platform variants:**
- iOS: `.buttonStyle(.borderedProminent)` for primary; system styles handle press highlight.
- Android: M3 `Button` / `FilledTonalButton` / `OutlinedButton` / `TextButton`.
- Game UI: bevel or shadow + press state ([[affordance]]). Controller focus ring visible at 10-foot distance.

**Failure looks like:** Three equal primaries. A spinner that shrinks the button. Double submissions. A disabled button with no reason given. "Click here" labels.

**Review checks:**
- [ ] Exactly one primary per group
- [ ] Every button ≥ 44px; icon-only ones have names
- [ ] Loading keeps width and blocks repeat clicks
- [ ] Disabled buttons that need a reason use `aria-disabled` + explanation

Reference test: `~/Documents/github/ui-test/components/button`

**Related:** [[affordance]] · [[components/form]] · [[components/modal]]
