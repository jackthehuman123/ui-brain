# ui-brain

An Obsidian vault of UI design knowledge that Claude Code agents load while designing, refining or reviewing interfaces on web, iOS, Android, desktop, Roblox and Unity. It holds concrete rules, values, failure patterns and review checklists, not tutorials.

The vault root is also a **Claude Code skill**: `SKILL.md` (a symlink to `_index.md`) gives the skill's name and description. Claude sees only that description until a design task comes up, then reads the index, and from there only the map, checklist and notes the task needs.

```
_index.md / SKILL.md   entry point and loading rules (the only always-relevant file)
maps/                  one map per design domain
concepts/              atomic notes: Rule · Why · Values · Failure · Detect · Implementation
checklists/            yes/no review passes per domain
platforms/             per-platform constants (safe areas, touch targets, GuiInset…)
deploy/ui-designer.md  subagent template to copy into projects
CLAUDE.md              maintenance instructions (used only when working *on* the vault)
```

## Install

### Option A: personal skill (recommended, one install for all projects)

```bash
# 1. Get the vault
git clone https://github.com/<your-user>/ui-brain.git ~/vaults/ui-brain

# 2. Register it as a personal skill (Claude Code follows the symlink)
mkdir -p ~/.claude/skills
ln -s ~/vaults/ui-brain ~/.claude/skills/ui-brain
```

3. Let Claude read the vault without a permission prompt each time. Add this to `~/.claude/settings.json`:

```json
{
  "permissions": {
    "allow": ["Read(~/vaults/ui-brain/**)"]
  }
}
```

4. (Optional) Install the design subagent. It preloads the skill through its `skills:` field:

```bash
mkdir -p ~/.claude/agents
cp ~/vaults/ui-brain/deploy/ui-designer.md ~/.claude/agents/
```

5. (Optional) Make delegation explicit in a project's `CLAUDE.md`:

```markdown
## Design work
For any UI design, refinement or design review, delegate to the `ui-designer` subagent
(or use the `ui-brain` skill directly). Load only the maps and checklists the task needs.
```

**Check it worked:** in any project, type `/ui` and `ui-brain` should appear in the slash menu. Then ask for a small design review and confirm Claude reads `maps/…` and a few `concepts/…` files, not the whole vault.

### Option B: per-project, shared with a team (git submodule)

The vault lives inside the project, so teammates get it on clone and Claude needs no extra read permissions.

```bash
git submodule add https://github.com/<your-user>/ui-brain.git .claude/skills/ui-brain
mkdir -p .claude/agents && cp .claude/skills/ui-brain/deploy/ui-designer.md .claude/agents/
git commit -m "Add ui-brain design knowledge skill"
# Teammates: git clone --recurse-submodules …  (or: git submodule update --init)
```

### Option C: import the index into CLAUDE.md (always loaded)

Add `@~/vaults/ui-brain/_index.md` to a project's `CLAUDE.md` or to `~/.claude/CLAUDE.md`. The one-page index then loads in every session, whether or not the work is design. External imports in a project file trigger a one-time approval dialog. You still need the `Read(...)` allow rule from Option A.

### Things to avoid
- **Don't** use `--add-dir` on the vault together with `CLAUDE_CODE_ADDITIONAL_DIRECTORIES_CLAUDE_MD=1`. That loads the vault's *maintenance* `CLAUDE.md` into your project session.
- **Windows:** git checks symlinks out as plain text unless `core.symlinks` is enabled. If `SKILL.md` breaks, replace it with a copy of `_index.md`.

## Update

```bash
cd ~/vaults/ui-brain && git pull          # Option A
git submodule update --remote .claude/skills/ui-brain   # Option B
```

## Maintain

Open the vault folder in Claude Code (and in Obsidian to browse it). `CLAUDE.md` defines these commands:

| Command | What it does |
|---|---|
| `add <term(s)>` | Research a concept and write a note (or extend an existing one); link it into its map and checklist |
| `expand <note>` | Add values, platform implementations or failure examples, and re-verify sources |
| `harvest` | After a design session elsewhere, turn the agent's "Vault gaps" and corrections into proposals in `inbox/` |
| `gaps <domain>` | Propose missing concepts in `inbox/candidates.md` |
| `audit` | Check links, maps, frontmatter, length, unverified values, and notes verified more than 6 months ago |
| `promote <item>` | Turn an approved inbox candidate into a note |

Claude writes notes with `status: draft`. Only the owner marks them `verified`.
