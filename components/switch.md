---
type: component
description: "Immediate on/off: role=switch, label toggles, icon in thumb, retargets mid-flight, rolls back on failure"
aliases: [toggle, toggle switch, on off switch]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://www.w3.org/WAI/ARIA/apg/patterns/switch/
---
# Switch

**Use when:** a setting takes effect **immediately** (no Save). **Don't use when:** the choice is submitted later with a form (use [[components/checkbox]]).

**Anatomy:** label (+ description) → track → thumb (with on/off icon). The whole row is clickable.

**Required states:** off · on · focus-visible · pressed · disabled (with a reason) · pending/failed.

**Rules:**
- `role="switch"` + `aria-checked` (or a native checkbox with `role=switch`), named by its label. Clicking the label toggles it.
- On and off differ by thumb position **and** an icon or label inside the thumb, not only the track color → [[affordance]].
- The thumb moves with `transform` on the motion token and retargets on rapid toggles → [[interruptible-animation]], [[reduced-motion]].
- Changes save optimistically. On failure, restore the **previous** state (capture it before flipping) and say why → [[optimistic-update]].
- Track boundary ≥ 3:1 in the off state → [[contrast-ratio]].

**Values:** track 52×32 with a 24px thumb, inside a 44px-tall hit area (**unverified** sizes; iOS and M3 differ slightly). Thumb travel ~200 ms ([[animation-duration]]).

**Platform variants:**
- iOS: `Toggle` (the system style is the convention; don't restyle it).
- Android: M3 `Switch` with `thumbContent` showing an icon when checked.
- Game UI: two-state selector (On / Off) for controllers; it's clearer than a small switch at 10 ft.

**Failure looks like:** A switch that needs a Save button. Off and on differing only by gray versus blue. A failed save that silently leaves the switch on (component test #3 rolled back to the *new* value). A thumb that snaps back when tapped twice quickly.

**Review checks:**
- [ ] Immediate effect; failure rolls back to the previous state with a message
- [ ] Non-color on/off cue; label toggles
- [ ] Thumb retargets mid-flight; no movement with reduced motion on

Reference test: `~/Documents/github/ui-test/components/switch`

**Related:** [[components/checkbox]] · [[optimistic-update]] · [[interruptible-animation]]
