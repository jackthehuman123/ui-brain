---
type: concept
description: "Reserve space for anything that loads late; animate with transform; CLS ≤ 0.1 at p75"
domain: layout-and-spacing
aliases: [CLS, cumulative layout shift, content jump, jank, reserved space, aspect-ratio]
platforms: [web, all]
status: draft
last_verified: 2026-11-16
sources:
  - https://web.dev/articles/cls
  - https://web.dev/articles/defining-core-web-vitals-thresholds
---
# Layout shift

**Rule:** Nothing visible may move unless the user just caused it. Reserve space for images, ads, embeds, fonts and async content before they load, and animate position and size with `transform`, never with layout properties.

**Why:** Content that jumps makes users mis-tap and lose their place, and CLS is a ranking signal on the web.

**Values:** *(web.dev)*
- Good CLS: **≤ 0.1** at the 75th percentile, mobile and desktop measured separately.
- Shifts within **500 ms** of a tap, click or keypress are excluded; scroll and drag are not "input".
- Session windows: shifts < 1 s apart, window ≤ 5 s; the worst window counts.
- `transform` animations never count as layout shifts.

**Failure looks like:** A cookie banner pushing the hero down. Product grids reflowing as images arrive. A "Load more" that inserts above the viewport. Prices or counters changing width ([[tabular-numbers]]). Text re-wrapping when the web font arrives ([[font-loading]]).

**Detect in review:** In code: `<img>` without `width`/`height` or `aspect-ratio`; animations on `top`, `height` or `margin`; late-injected banners above content; skeletons whose size differs from the final content. Measure: Lighthouse / PerformanceObserver `layout-shift` entries on a throttled load.

**Implementation:**
- Web: `img{aspect-ratio:4/5;width:100%;height:auto}`. Make skeletons the final size. Use `transform` for motion. Put banners in reserved slots or overlay them.
- Native: fix image frames before load (`.aspectRatio`, `Modifier.aspectRatio`). Keep list row heights stable while async data arrives.
- Game UI: reserve the HUD slots for elements that appear later (quest tracker, currency) instead of re-laying out the HUD.

**Related:** [[tabular-numbers]] · [[font-loading]] · [[optimistic-update]] · [[interruptible-animation]]
