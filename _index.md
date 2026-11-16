---
name: ui-brain
description: UI design rules, concrete values, failure patterns and review checklists for web, iOS, Android, desktop and game UI (Roblox, Unity), organized by project type, screen, component and design concept. Use when designing, refining or reviewing any user interface or UI code, such as homepages, forms, cards, menus, dashboards, game HUDs, typography, color, spacing, motion, accessibility, safe areas and touch targets.
type: index
---
# ui-brain: UI design knowledge for design subagents

These notes record rules, thresholds, values and failure patterns that improve on model defaults; nothing here is a definition or tutorial.

## For agents: how to load (narrow → specific, stop when you have enough)
1. **Project type** → `project-types/<type>.md`: platforms, typical screens, core components, priority concepts, quality bars.
2. **Screen** you're building → `screens/<screen>.md`: job, section order, rules, review checks.
3. **Components** on it → `components/<component>.md`: anatomy, states, rules, review checks.
4. **Concepts**: open only the `[[links]]` you need for reasoning or values. For a pure style pass (e.g. "fix the typography"), go straight to `maps/<domain>.md` + `checklists/<domain>.md`.
5. **Platform constants** → `platforms/<platform>.md`.
6. **Never load the whole vault.** Notes are `status: draft`. Treat **unverified** values as estimates and say so.
7. Link resolution: paths are relative to this file's directory (`${CLAUDE_SKILL_DIR}` as a skill). `[[name]]` = `concepts/name.md`. A prefixed link (`[[components/form]]`, `[[maps/color]]`) = that path + `.md`.
8. Finish by listing missing or wrong knowledge under **Vault gaps** (for `harvest`).

## Where things are
| Layer | Index | Use it for |
|---|---|---|
| Project types | [[maps/project-types]] | "I'm building a storefront / SaaS app / iOS app / Roblox game" |
| Screens | [[maps/screens]] | homepage, checkout, settings, HUD… |
| Components | [[maps/components]] | form, card, menu, combobox… |
| Concepts by domain | [[maps/typography]] · [[maps/color]] · [[maps/layout-and-spacing]] · [[maps/motion]] · [[maps/interaction-and-state]] · [[maps/iconography-and-visual-detail]] · [[maps/platform-and-environment]] · [[maps/accessibility]] | the reasoning and values behind rules |
| Review passes | `checklists/<domain>.md` | yes/no audits |

Humans: maintenance rules are in `CLAUDE.md`; sources are ranked in [[sources]]; `inbox/` holds candidates (agents ignore it).
