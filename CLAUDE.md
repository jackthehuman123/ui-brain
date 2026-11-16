# ui-brain: maintenance instructions

This is an Obsidian vault of UI design knowledge loaded by design subagents. `_index.md` is the only file that always loads; keep it under one page.

## What belongs here
Content that improves output beyond model defaults: actionable rules, thresholds, concrete values, failure patterns and how to detect them. **Not** definitions, tutorials or copied docs. A note that only explains what something *is* has failed.

## Structure
- `concepts/`: one atomic note per concept, flat, kebab-case filenames, built from `_template.md`.
- `maps/<domain>.md`: one map of content per domain. Every concept appears in exactly one map (its `domain`).
- `checklists/<domain>.md`: yes/no review checks; each item links to its concept note.
- `platforms/<platform>.md`: web, ios, android, desktop, roblox, unity constants. **Constants live only here**; concept notes link to them.
- `inbox/`: candidates (`candidates.md`) and drafts awaiting the owner's review.
- `sources.md`: ranked trusted sources.

Domains (frontmatter `domain:` values = map filenames): `typography`, `color`, `layout-and-spacing`, `motion`, `interaction-and-state`, `components`, `iconography-and-visual-detail`, `platform-and-environment`, `accessibility`.

## Quality rules (every note, every time)
- **Sources:** platform guidelines (Apple HIG, Material 3, Fluent, Roblox Creator Docs) > specs (W3C/CSSWG, WCAG 2.2, MDN) > recognized practitioners. Check every number with web search. List sources in `sources:` frontmatter, and attribute each value inline, e.g. *(M3 tokens)*.
- **Never invent a value.** If unsourced, write `**unverified**, <estimate> (<reasoning>)`.
- **One page maximum** (~45 lines of body). If longer, split or cut.
- **One fact, one place.** Platform constants go in `platforms/`; link, don't repeat.
- **Status:** Claude only writes `status: draft`. Only the owner sets `verified`.
- Use `[[wikilinks]]` and `aliases`. Filenames kebab-case. Links to not-yet-written notes are allowed; they mark future notes.
- **Commit** after each batch; the message lists the notes added or changed.

## Maintenance commands
- **`add <term(s)>`**: Check `aliases` and filenames for an existing note first (`grep -ril "<term>" concepts/`). If one exists, extend it. Otherwise research, write from `_template.md`, link into its map and related notes, and add a checklist item if it adds a reviewable check. Report what changed.
- **`expand <note>`**: Add values, platform implementations or failure examples. Re-verify the sources and bump `last_verified`.
- **`harvest`**: Run at the end of a design session in another repo. Look at what the design subagent struggled with or was corrected on, and propose new concepts or rule changes as files in `inbox/`. **Don't edit concept notes directly.**
- **`gaps <domain>`**: Propose missing concepts for the domain in `inbox/candidates.md` (one line each on why it earns a note). Don't write them.
- **`audit`**: Report broken links, orphan notes, notes missing from a map, missing frontmatter fields, notes over a page, **unverified** values, and `last_verified` older than 6 months. Fix mechanical issues (links, maps) and list the rest for the owner.
- **`promote <inbox item>`**: Turn an approved candidate into a concept note (as `add`), then remove it from `inbox/`.
