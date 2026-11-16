---
type: inbox
source: ~/Documents/github/ui-test/REVIEW.md
---
# Harvest: ui-test plan-picker card (2026-11-16)

Proposals only. Concept notes are unchanged until the owner approves.

## Rule changes
- **oklch** → Values or Rule: after any relative-color state shift (`calc(l ± 0.1) c h`), re-check gamut and clamp C, e.g. `min(c, <max C at new L>)`. Evidence: dark accent at L 0.70 / C 0.14 + 0.1 L went out of sRGB (max C at L 0.80 ≈ 0.10, computed with the Oklab matrices).
- **tracking** → Rule: all-caps tracking applies to letter strings, not numerals or symbols ("−17%" at +0.08em read as separate characters).
- **interruptible-animation** → Detect: every property that changes with the state class must be transitioned too; an instant `padding` change caused a 3.5px jump on interrupt. Add the test method: pause the CSS transition via `getAnimations()` + `currentTime`, trigger the opposite state, and compare values.

## New candidates
- `reduced-motion`: the `prefers-reduced-motion` policy (what to keep, what to drop).
- `review-tooling`: headless Chrome's minimum window is ~500px (use an iframe for narrow viewports). Force the color scheme with a stylesheet edit, since `--force-dark-mode` didn't apply in headless. Contrast and gamut script; interrupt-test harness.
- Already on the seed list and needed in this test: `dark-mode-depth` (the selected thumb looked sunken in dark mode), `touch-target`, `tabular-numbers`, `concentric-radius`, `alpha-borders`, `matched-icon-weight`, plus `easing`/`animation-duration` from the animation-principles additions.
