---
type: inbox
source: ~/Documents/github/ui-test/components/REVIEW.md
---
# Harvest: 16 component tests (2026-11-16)

Proposals only. Notes are unchanged until the owner approves.

## Rule changes
- **multiply-blending** → Rule: the condition is the **immediate surface** the image sits on (a light plate), not the app theme. Evidence: card test, where multiply was turned off for the dark theme while the plate stayed light, which produced white boxes. The test encoded the same misreading and passed.
- **reduced-motion** → Values: list rotation (chevrons, spinners) and scale (progress fills, toggles) as movement. Implementation: a `--dur-move` token for all transform transitions, set to 0 under reduce. Two components broke this by using a general duration token.
- **interruptible-animation** → Detect: note that headless/virtual-time runs need transitions finished manually (`getAnimations().finish()`), or end-state assertions read start values.
- **touch-target** → Detect: measure the *declared* hit area for stretched links and label-wrapped inputs, not the element's own box.

## New component notes (only form and combobox exist)
button · text-field · select · checkbox · radio · switch · tabs · navigation-bar · card · list · modal · toast · tooltip · avatar · badge · progress. Each test page already contains the rules, values and checks to distil (see `ui-test/components/<name>/index.html` → `componentTest`).

## New concept candidates
- `focus-visible` (already a candidate): every component needed a ring, including wrapper-drawn rings for inputs and stretched cards.
- `toast-timing`: queue one at a time; auto-dismiss ~5 s, ~10 s with an action; pause on hover and focus; Undo over confirm.
- `hidden-attribute-pitfall` (or part of `review-tooling`): author `display` rules override `[hidden]`. Add a global `[hidden]{display:none!important}`.
- `review-tooling` (already a candidate): add overlap detection, the contact-sheet visual pass, and virtual-time transitions.
