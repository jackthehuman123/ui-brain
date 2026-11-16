---
type: platform
description: "Web constants: target sizes, Core Web Vitals, viewport units, safe-area env(), input zoom threshold"
platforms: [web]
status: draft
last_verified: 2026-11-16
sources:
  - https://www.w3.org/WAI/WCAG22/Understanding/target-size-minimum.html
  - https://web.dev/articles/defining-core-web-vitals-thresholds
  - https://web.dev/blog/viewport-units
---
# Web constants

## Target size
- WCAG 2.2 **2.5.8 (AA): 24×24 CSS px**, or 24px spacing to the nearest target. Inline links are exempt.
- WCAG **2.5.5 (AAA): 44×44 CSS px**.
- Working default for touch-first UIs: 44–48px (matches the iOS and Material minimums).

## Core Web Vitals (good, at p75)
LCP ≤ 2.5 s · INP ≤ 200 ms · CLS ≤ 0.1. Shifts within 500 ms of discrete input are excluded from CLS.

## Viewport and insets
- `svh/lvh/dvh`: Chrome/Edge 108, Firefox 101, Safari 15.4.
- Safe area: `viewport-fit=cover` + `env(safe-area-inset-top|right|bottom|left)`.

## Text inputs
- iOS Safari zooms on focus when an input's rendered font-size is < **16px** (practitioner consensus).

Used by [[touch-target]], [[layout-shift]], [[dynamic-viewport]], [[safe-area]], [[components/form]].
