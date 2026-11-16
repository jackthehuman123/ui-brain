# ui-brain: maintenance instructions

This is an Obsidian vault of UI design knowledge loaded by design subagents. `_index.md` is the only file that always loads; keep it under one page.

## What belongs here
Content that improves output beyond model defaults: actionable rules, thresholds, concrete values, failure patterns and how to detect them. **Not** definitions, tutorials or copied docs. A note that only explains what something *is* has failed.

## Structure
- **Three layers, narrow → specific:**
  - `project-types/`: routing per kind of product (`_template-project-type.md`)
  - `screens/`: one note per screen type (`_template-screen.md`)
  - `components/`: one note per component (`_template-component.md`)
  - `concepts/`: one atomic note per concept, flat, kebab-case (`_template.md`). This is the layer the other three link down into.
- **Layering rule:** a screen or component note states each rule in one line and links to the concept that holds the reasoning and general values. Values specific to the component or screen (e.g. checkout field count) live in that note. Never copy a concept's Values block upward.
- Indexes: `maps/project-types.md`, `maps/screens.md`, `maps/components.md`, plus one map per concept domain.
- `maps/<domain>.md`: one map of content per domain. Every concept appears in its home map (its `domain`) and may also be listed in other maps where it applies (e.g. `touch-target` in accessibility too).
- `checklists/<domain>.md`: yes/no review checks; each item links to its concept note.
- `platforms/<platform>.md`: web, ios, android, desktop, roblox, unity constants. **Constants live only here**; concept notes link to them.
- `inbox/`: candidates (`candidates.md`) and drafts awaiting the owner's review.
- `sources.md`: ranked trusted sources.

Concept domains (frontmatter `domain:` values = map filenames): `typography`, `color`, `layout-and-spacing`, `motion`, `interaction-and-state`, `iconography-and-visual-detail`, `platform-and-environment`, `accessibility`. Component-level concepts (e.g. `combobox`) become `components/` notes. `maps/components.md` indexes that folder.

## Deployment wiring (don't break)
- The vault root is a Claude Code skill. `SKILL.md` is a symlink to `_index.md`, so `_index.md`'s frontmatter `name` and `description` are the skill's trigger. Keep the description in the third person and under 1,024 characters, and say *what* the skill covers and *when* to use it.
- `deploy/ui-designer.md` is the subagent template other projects copy. Update it if the loading rules in `_index.md` change.
- Agents resolve `[[name]]` to `concepts/name.md`. Keep `concepts/` flat and filenames unique.
- See `README.md` for install paths.

## Writing rules (from Anthropic's skill-authoring guidance)
- Assume the reader is already a strong model: no definitions or background it already knows. Every line has to earn its tokens.
- Keep each note under ~100 lines; agents may preview long files partially.
- Use one term per concept across the whole vault (match the note filename and aliases).
- No time-relative phrasing ("currently", "recently", "new in"). Use dates and `last_verified`.
- Give one default, not a menu: "use X; for case Y use Z".

## Quality rules (every note, every time)
- **Sources:** platform guidelines (Apple HIG, Material 3, Fluent, Roblox Creator Docs) > specs (W3C/CSSWG, WCAG 2.2, MDN) > recognized practitioners. Check every number with web search. List sources in `sources:` frontmatter, and attribute each value inline, e.g. *(M3 tokens)*.
- **Never invent a value.** If unsourced, write `**unverified**, <estimate> (<reasoning>)`.
- **One page maximum** (~45 lines of body). If longer, split or cut.
- **One fact, one place.** Platform constants go in `platforms/`; link, don't repeat.
- **Status:** Claude only writes `status: draft`. Only the owner sets `verified`.
- Use `[[wikilinks]]` and `aliases`. Filenames kebab-case. Links to not-yet-written notes are allowed; they mark future notes.
- **Commit** after each batch; the message lists the notes added or changed.

## Maintenance commands
- **`add <term(s)>`**: First decide the layer: project type, screen, component or concept. Check `aliases` and filenames for an existing note (`grep -ril "<term>" concepts components screens project-types`). If one exists, extend it. Otherwise research, write from that layer's template, link into its map and related notes, and add a checklist item if it adds a reviewable check. Report what changed.
- **`expand <note>`**: Add values, platform implementations or failure examples. Re-verify the sources and bump `last_verified`.
- **`harvest`**: Run at the end of a design session in another repo. Look at what the design subagent struggled with or was corrected on, and propose new concepts or rule changes as files in `inbox/`. **Don't edit concept notes directly.**
- **`gaps <domain>`**: Propose missing concepts for the domain in `inbox/candidates.md` (one line each on why it earns a note). Don't write them.
- **`audit`**: Report broken links, orphan notes, notes missing from a map, missing frontmatter fields, notes over a page, **unverified** values, and `last_verified` older than 6 months. Fix mechanical issues (links, maps) and list the rest for the owner.
- **`promote <inbox item>`**: Turn an approved candidate into a concept note (as `add`), then remove it from `inbox/`.
