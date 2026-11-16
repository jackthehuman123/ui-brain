---
type: project-type
description: "Storefront routing: homepage, listing, product, cart, checkout; priorities CLS, tabular prices, touch targets, ~8 fields"
aliases: [online store, storefront, shop, DTC brand site, e-commerce]
status: draft
last_verified: 2026-11-16
sources:
  - https://baymard.com/blog/checkout-flow-average-form-fields
  - https://web.dev/articles/defining-core-web-vitals-thresholds
---
# E-commerce site

**Covers:** brand and retail storefronts on the web (DTC brands, catalogs, single-product shops). For native shopping apps, also load the iOS/Android platform files.

**Platforms:** [[platforms/web]]

**Typical screens:** [[screens/homepage]] · category listing · product detail · cart · checkout · account / order status · search results (screens other than homepage are not yet written)

**Core components:** [[components/form]] · product card · navigation bar / mega-menu · filter and sort · image gallery · size selector · button · toast. Written: [[components/form]], [[components/combobox]] (search)

**Priority concepts:**
- [[layout-shift]]: images and prices loading late are the main source of CLS on product grids
- [[tabular-numbers]]: prices and specs in columns must align
- [[touch-target]]: size and color selectors are often too small on mobile
- [[optimistic-update]]: add-to-cart should respond instantly
- [[oklch]]: brand palette plus accessible sale/error/success colors
- [[tracking]]: brand display type and all-caps nav labels
- [[interruptible-animation]]: drawers (cart, filters) must reverse cleanly on a second tap
- [[progressive-disclosure]]: specs, size guides and shipping details

**Quality bars:** Core Web Vitals good at p75 (LCP ≤ 2.5 s, INP ≤ 200 ms, CLS ≤ 0.1) *(web.dev)*. Checkout needs about 8 fields; the average is 11.3 *(Baymard 2024)*. WCAG 2.2 AA.

**Gotchas:**
- Aesthetic brand sites hide what's for sale behind mood imagery; the homepage must still pass the 5-second test.
- Product photos on varied backgrounds break grid rhythm. Normalize the backgrounds or crop to a fixed aspect ratio.
- Sale and error reds collide; keep them as separate tokens.
- Don't put spec claims in images; keep them as text so they're searchable, translatable and accessible.
