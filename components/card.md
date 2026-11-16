---
type: component
description: "Whole card clickable via one stretched link, secondary action above it, fixed media ratio, concentric corners"
aliases: [cards, product card, content card, tile, article card]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://inclusive-components.design/cards/
---
# Card

**Use when:** a self-contained summary that links to more (product, article, project). **Don't use when:** items are uniform rows that are scanned rather than browsed (use [[components/list]]).

**Anatomy:** container → media (fixed ratio) → eyebrow/meta → title (the link) → supporting text → price/meta → optional secondary action (wishlist, menu).

**Required states:** default · hover (lift) · focus-visible (ring on the card) · pressed · selected (when selectable).

**Rules:**
- One link (the title) stretched over the card with `::after{inset:0}`. Secondary actions sit above it (`z-index`), so there are ≤ 2 tab stops → [[affordance]], [[fitts-law]].
- Media keeps a fixed `aspect-ratio` before load → [[layout-shift]].
- Inner radius = outer − padding → [[concentric-radius]].
- White-background shots go on a light plate with multiply. The plate's lightness decides it, not the theme → [[multiply-blending]].
- Titles balanced and excerpts clamped (3 lines) → [[widow]], [[line-length]]. Prices tabular → [[tabular-numbers]].
- Hover lift with `translate` and a shadow on one light source → [[consistent-light-source]].

**Values:** product media 4:5 or 1:1, consistent within a grid. Card padding 8–20px with matching inner radius. Hover lift 2px (**unverified**).

**Platform variants:**
- iOS/Android: the whole card is one button or `Modifier.clickable`; secondary actions in a context menu or a separate icon button.
- Game UI: card focus scales slightly with a frame highlight; controller A opens and X/Y does the secondary action.

**Failure looks like:** Three separate links per card (image, title, "Read more"). Images that pop in and push text down. Inner corners as round as outer ones. White boxes around product shots. Ragged one-word title lines.

**Review checks:**
- [ ] Card body click opens; ≤ 2 tab stops; ring drawn on the card
- [ ] Aspect-ratio reserved; concentric radius
- [ ] No white boxes on tinted plates, in either theme

Reference test: `~/Documents/github/ui-test/components/card`

**Related:** [[components/list]] · [[concentric-radius]] · [[multiply-blending]]
