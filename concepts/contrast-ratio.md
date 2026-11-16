---
type: concept
description: "Text ≥4.5:1 (large ≥3:1), UI boundaries and icons ≥3:1, measured against the worst pixel behind them"
domain: accessibility
aliases: [contrast, WCAG contrast, color contrast, 4.5:1, APCA, non-text contrast]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://www.w3.org/WAI/WCAG22/Understanding/contrast-minimum.html
  - https://www.w3.org/WAI/WCAG22/Understanding/non-text-contrast.html
  - https://www.w3.org/WAI/WCAG22/Understanding/contrast-enhanced.html
---
# Contrast ratio

**Rule:** Text needs ≥ 4.5:1 (≥ 3:1 when large). Control boundaries, focus indicators and meaningful icons need ≥ 3:1 against what's adjacent. Measure text on imagery or gradients at its **worst** pixel, not against a token.

**Why:** Low-vision users, bright sunlight and cheap screens all compress contrast. Ratios are strict thresholds: 4.49 fails.

**Values:** *(WCAG 2.2)*
- 1.4.3 (AA): 4.5:1 for text; 3:1 for large text, meaning ≥ 18pt (24px) or ≥ 14pt bold (≈ 18.66px).
- 1.4.6 (AAA): 7:1 and 4.5:1.
- 1.4.11 (AA): 3:1 for UI component boundaries and states, and for graphics needed to understand content. An input identified only by its border needs a 3:1 border. A borderless input needs 3:1 between its fill and the page.
- Disabled controls and logos are exempt.
- APCA is a WCAG 3 *draft* method. Use it as a second opinion, not for compliance.

**Failure looks like:** Light-gray placeholder-style labels. Input borders at about 1.5:1 (#E5E5E5 on white). Orange text that passes on the page color but fails over the hero sky (4.23:1 measured in the ayxc test). Focus rings invisible on the accent color.

**Detect in review:** Compute ratios for every token pair in light and dark mode. For text on images, render the background and sample the lightest and darkest pixels under each line box. Check hover, focus and disabled states, not only the default.

**Implementation:** Keep a contrast test in CI over the token pairs, plus a per-pixel check for hero text. Native: test with Increase Contrast (iOS) and high-contrast text (Android) enabled.

**Related:** [[oklch]] · [[oklch-palettes]] · [[alpha-borders]] · [[dark-mode-depth]]
