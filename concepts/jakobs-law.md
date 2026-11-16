---
type: concept
description: "Follow conventions users know (logo→home, cart top-right, swipe-back); innovate in content, not controls"
domain: interaction-and-state
aliases: [Jakob's law, conventions, familiarity, mental model, platform conventions, design patterns]
platforms: [all]
status: draft
last_verified: 2026-11-16
sources:
  - https://www.nngroup.com/videos/jakobs-law-internet-ux/
  - https://lawsofux.com/jakobs-law/
---
# Jakob's law

**Rule:** Users spend most of their time on *other* products, so they expect yours to work the same way. Keep established conventions for navigation, controls and placement (per platform), and spend novelty on content and brand, not on how basic controls behave.

**Why:** Convention is free usability: users transfer what they already know. Breaking it adds learning cost to every visit and causes errors.

**Values:**
- Web: logo links to home; cart and account top-right; search near the top; underlined links; footer holds legal and contact. *(NN/g conventions)*
- iOS: back at top-left plus the edge-swipe gesture; a tab bar at the bottom for top-level sections. Android: system back gesture; a navigation bar or rail.
- Games: Escape/Start opens the pause menu; the same confirm and cancel buttons across all menus (platform-specific face-button conventions).
- Change conventions only with evidence (testing). Migrate users gradually, never all at once *(NN/g)*.

**Failure looks like:** A custom scroll-jacking homepage. Hamburger menus on desktop with plenty of room. A logo that doesn't go home. iOS apps with an Android-style back button only. A game where B confirms in one menu and cancels in another.

**Detect in review:** List every navigation and control pattern and compare it with the platform's guidelines ([[platforms/ios]], [[platforms/android]]) and the top 3 competitors. Flag deviations without a tested reason.

**Implementation:** Use system components first (they encode conventions). On the web, follow the standard header, footer and form patterns. For cross-platform apps, adapt navigation per platform instead of shipping one platform's patterns everywhere.

**Related:** [[affordance]] · [[postels-law]] · [[hicks-law]]
