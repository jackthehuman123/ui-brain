---
type: concept
description: "Web fonts must not shift layout: preload 1–2 critical files, metric-matched fallback (size-adjust), font-display set"
domain: typography
aliases: [web fonts, FOUT, FOIT, font-display, size-adjust, fallback font, font swap]
platforms: [web]
status: draft
last_verified: 2026-11-16
sources:
  - https://web.dev/articles/css-size-adjust
  - https://developer.chrome.com/blog/framework-tools-font-fallback
  - https://web.dev/articles/defining-core-web-vitals-thresholds
---
# Font loading

**Rule:** A web font swap must not move layout. Give the fallback the web font's metrics (`size-adjust`, `ascent-override`, `descent-override`), preload only the 1–2 files used above the fold, and choose `font-display` deliberately.

**Why:** `font-display: swap` paints the fallback first. If its metrics differ, every line reflows when the web font arrives, which counts toward CLS (good is ≤ 0.1).

**Values:**
- Metric overrides: Chromium 87+, Firefox 89+; Safari support lagged. *(web.dev)* Values are per font pair, so measure them or use a generator (Next.js/Nuxt font tools, Capsize).
- `swap`: text shows immediately but can shift. `optional`: no shift, but the web font may not show on the first visit. Use `optional` for body text when CLS matters more than brand type, and `swap` + metric overrides for display text.
- CLS budget: ≤ 0.1 at p75. *(web.dev)* See [[layout-shift]].

**Failure looks like:** Headlines that re-wrap a moment after load. Buttons that change width. Hero CTAs that jump down a line.

**Detect in review:** Throttle to Slow 4G with the cache disabled and record the load; watch the hero text. In code: Google Fonts `display=swap` with no fallback `@font-face` overrides, five or more font files preloaded, or a font loaded but unused above the fold.

**Implementation:**
```css
@font-face { font-family: "Brand Fallback"; src: local("Arial");
  size-adjust: 104%; ascent-override: 92%; descent-override: 24%; }  /* measured per pair */
body { font-family: "Brand", "Brand Fallback", sans-serif; }
```
Native and game UI bundle their fonts, so this applies to the web only.

**Related:** [[x-height]] · [[layout-shift]]
