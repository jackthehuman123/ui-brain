---
type: screen
description: "First screen says what's sold, to whom, one primary CTA; no carousel; hero not lazy; text passes worst-pixel contrast"
aliases: [home page, landing page, front page, hero]
project_types: [ecommerce-site, marketing-site]
platforms: [web]
status: draft
last_verified: 2026-11-16
sources:
  - https://www.nngroup.com/articles/scrolling-and-attention/
  - https://www.nngroup.com/articles/113-design-guidelines-homepage-usability/
  - https://www.nngroup.com/articles/auto-forwarding/
  - https://web.dev/articles/defining-core-web-vitals-thresholds
  - https://web.dev/articles/optimize-lcp
---
# Homepage

**Job:** within the first screen, a stranger can say **what this is, who it's for and what to do next**. One primary action; everything else routes visitors to the right section.

**Structure (brand or e-commerce):**
1. **First screen (must hold all of this):** logo + primary nav · a one-sentence tagline saying what you do · one primary CTA (+ at most one secondary) · hero imagery that shows the product in use
2. Category or path entry points (by need, not org chart)
3. Featured products or proof (specs, reviews, press, numbers)
4. Brand story / differentiator
5. Secondary conversion (newsletter, store finder)
6. Footer: full nav, support, legal

Order after section 1: **unverified**, common practice. Test it against your analytics.

**Components:** [[components/form]] (newsletter) · card · navigation bar · button (component notes planned; see `maps/components.md`)

**Rules:**
- Spend the best content on the first two screens, because attention falls sharply after the fold. *(NN/g)*
- The tagline names the category and the benefit; brand-mood lines go *under* it, not in its place. *(NN/g homepage guidelines)*
- No auto-advancing hero carousel; users find auto-forwarding annoying and miss slides. *(NN/g)*
- The hero image is the likely LCP element: never lazy-load it, and give it `fetchpriority="high"`. *(web.dev)*
- Text over imagery must pass contrast at the **worst** pixel behind it. Use a scrim/gradient or keep text off the busy area → [[oklch]], [[contrast-ratio]].
- Reserve space for media and fonts so nothing jumps → [[layout-shift]].

**Values:**
- Viewing time: **57%** above the fold, **74%** within the first two screenfuls. *(NN/g eyetracking, 2018)*
- Core Web Vitals "good" at the 75th percentile: **LCP ≤ 2.5 s · INP ≤ 200 ms · CLS ≤ 0.1**. *(web.dev)*

**States:** first visit vs returning (don't hide the value proposition for new visitors) · slow network (hero area holds its size with a fallback color) · no-JS (content and links still work).

**Platform variants:** Mobile: the first screen is ~1/3 of desktop. Keep the tagline and CTA in it, and put hero media *below* the text if both won't fit. App "home" screens are a different screen type: they show the user's own content, not a pitch.

**Failure looks like:** A full-bleed mood photo with a poetic slogan and no product category. Three equal-weight CTAs. A carousel. A CTA below the fold on mobile. White text on a bright part of the photo. The hero popping in late and shifting the layout.

**Review checks:**
- [ ] 5-second test: from the first screen alone, can you say what's sold and to whom?
- [ ] Exactly one primary CTA in the first screen, on desktop and on a 390px-wide viewport
- [ ] No auto-advancing carousel
- [ ] Hero image not lazy-loaded; dimensions or aspect-ratio set
- [ ] Text on imagery ≥ 4.5:1 (≥ 3:1 for large text) at its worst rendered pixel. A token check isn't enough: rasterize the hero art plus scrim and sample under each line box ([[contrast-ratio]])
- [ ] LCP ≤ 2.5 s and CLS ≤ 0.1 in a throttled mobile run

**Related:** [[project-types/ecommerce-site]] · [[layout-shift]] · [[progressive-disclosure]] · [[line-length]]
