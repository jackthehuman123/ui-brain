---
type: concept
description: "Interactive elements must look interactive (strong signifiers: shape, underline, color, hover); static elements must not"
domain: interaction-and-state
aliases: [signifier, signifiers, clickability, perceived affordance, flat design]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://www.nngroup.com/articles/flat-ui-less-attention-cause-uncertainty/
---
# Affordance

**Rule:** Give every interactive element a strong signifier: a button shape, an underline or link color, a chevron, or a hover/press state. Remove those cues from non-interactive elements. Don't style static text like links or static cards like buttons.

**Why:** Weak signifiers cause "click uncertainty". Users hesitate, scan longer and miss actions. Interactive and static elements that look alike train users to distrust the UI.

**Values:**
- NN/g eyetracking: pages with weak signifiers took **22%** more time looking and **25%** more fixations than the same pages with strong signifiers. *(NN/g study via secondary coverage; it measured gaze, not task success)*
- Links in body text: underline, or color plus another cue (WCAG 1.4.1, don't rely on color alone).
- Pointer devices: hover states confirm interactivity. Touch has no hover, so the resting style alone must signal it.

**Failure looks like:** Ghost buttons indistinguishable from labels. Cards with hover lift that aren't clickable. Clickable cards with no cue. Icon-only actions with no tooltip or label. Game HUD icons that look decorative but are buttons.

**Detect in review:** Take a screenshot with the cursor away and ask what's clickable; compare with the DOM's interactive elements. In code: `cursor:pointer` or hover effects on non-interactive elements; `<div onClick>` without button styling or a role; links without underline or a distinct non-color cue.

**Implementation:**
- Web: real `<button>` and `<a>` elements; a visible `:hover`, `:active` and `:focus-visible` on every one; underlined inline links.
- iOS/Android: use system button styles; custom tappable rows get a chevron or accessory.
- Game UI: buttons get bevel, outline or drop shadow plus a press state ([[squash-and-stretch]]); static icons stay flat.

**Related:** [[touch-target]] · [[jakobs-law]] · [[squash-and-stretch]] · [[fitts-law]]
