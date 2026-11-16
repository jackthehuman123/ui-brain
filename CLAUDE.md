# ui-brain: maintenance instructions

This is an Obsidian vault of UI design knowledge. Agents reach it through the personal skill `~/.claude/skills/ui-brain/` (only its name and description load at startup) and look notes up search-first through each note's `description:`. `_index.md` is the in-vault entry point; keep it under ~40 lines.

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
- The skill lives **outside** the vault at `~/.claude/skills/ui-brain/` (`SKILL.md` + `scripts/find.sh`). It references the vault in place; never copy notes into it. The vault is the single source of truth.
- `find.sh` reads the `description:` and `aliases:` lines of every note in `concepts/`, `components/`, `screens/` and `project-types/`, and prints one line per note.
- **Keep `_index.md` and `SKILL.md` in sync.** Both hold the same lookup procedure. **Any new top-level folder** must be added to the lookup procedure and folder list in both files, and to the folder list in `find.sh` if it holds notes.
- `deploy/ui-designer.md` is the subagent template other projects copy. Update it if the lookup procedure changes.
- Agents resolve `[[name]]` to `concepts/name.md`. Keep `concepts/` flat and filenames unique.
- See `README.md` for install paths.

## Description field (every note, map and template)
- `description:` comes right after `type:` in the frontmatter. It's one line, **≤ 120 characters**, and **double-quoted** (descriptions often contain `: `, which breaks unquoted YAML).
- It states the **rule**, written from the note's **Rule:** line (or its Use when / Job / Covers line). Not a definition. Good: `"Loosen tracking on all-caps and small text; tighten on large display text"`. Bad: `"Note about tracking"`.
- Maps describe what the domain covers.

## Size cap
- Concept notes: **≤ 300 words** of body, never past one page. If a note grows past that, cut, split it, or move constants to `platforms/`.

## Writing rules (from Anthropic's skill-authoring guidance)
- Assume the reader is already a strong model: no definitions or background it already knows. Every line has to earn its tokens.
- Keep each note under ~100 lines; agents may preview long files partially.
- Use one term per concept across the whole vault (match the note filename and aliases).
- No time-relative phrasing ("currently", "recently", "new in"). Use dates and `last_verified`.
- Give one default, not a menu: "use X; for case Y use Z".

## Quality rules (every note, every time)
- **Sources:** platform guidelines (Apple HIG, Material 3, Fluent, Roblox Creator Docs) > specs (W3C/CSSWG, WCAG 2.2, MDN) > recognized practitioners. Check every number with web search. List sources in `sources:` frontmatter, and attribute each value inline, e.g. *(M3 tokens)*.
- **Never invent a value.** If unsourced, write `**unverified**, <estimate> (<reasoning>)`.
- **One page maximum**, and ≤ 300 words for concept notes (see Size cap).
- **One fact, one place.** Platform constants go in `platforms/`; link, don't repeat.
- **Status:** Claude only writes `status: draft`. Only the owner sets `verified`.
- Use `[[wikilinks]]` and `aliases`. Filenames kebab-case. Links to not-yet-written notes are allowed; they mark future notes.
- **Commit** after each batch; the message lists the notes added or changed.

## Maintenance commands
- **`add <term(s)>`**: First decide the layer: project type, screen, component or concept. Check `aliases` and filenames for an existing note (`grep -ril "<term>" concepts components screens project-types`). If one exists, extend it. Otherwise research, write from that layer's template, link into its map and related notes, and add a checklist item if it adds a reviewable check. **Always write `description:`**, and keep the note within the size cap. Report what changed.
- **`expand <note>`**: Add values, platform implementations or failure examples. Re-verify the sources and bump `last_verified`. **Update `description:`** if the Rule changed. Stay within the size cap; if you can't, propose a split instead.
- **`harvest`**: Run at the end of a design session in another repo. Look at what the design subagent struggled with or was corrected on, and propose new concepts or rule changes as files in `inbox/`. **Don't edit concept notes directly.**
- **`gaps <domain>`**: Propose missing concepts for the domain in `inbox/candidates.md` (one line each on why it earns a note). Don't write them.
- **`audit`**: Report broken links, orphan notes, notes missing from a map, missing frontmatter fields, notes over a page, **unverified** values, and `last_verified` older than 6 months. Also flag: **missing or overlong (> 120 chars) or unquoted descriptions**, **descriptions that don't match the note's Rule**, and **concept notes over 300 words**. Run `~/.claude/skills/ui-brain/scripts/find.sh` and confirm every note file appears exactly once. Check that `_index.md` and `SKILL.md` list the same folders. Fix mechanical issues (links, maps) and list the rest for the owner.
- **`promote <inbox item>`**: Turn an approved candidate into a concept note (as `add`), then remove it from `inbox/`.
