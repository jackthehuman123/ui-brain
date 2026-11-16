# ui-brain

An Obsidian vault of UI design knowledge that Claude Code agents use while designing, refining or reviewing interfaces on web, iOS, Android, desktop, Roblox and Unity. It holds concrete rules, values, failure patterns and review checklists, not tutorials.

**Cheap to load (progressive disclosure):** a small personal skill (`~/.claude/skills/ui-brain/`) puts only its name and description into context. When design work starts, the agent runs `find.sh` to scan every note's one-line `description:`, then opens at most 5 notes.

```
_index.md        search-first entry point (lookup procedure + task table)
project-types/   routing per kind of product        → screens/ → components/ → concepts/
concepts/        atomic notes: Rule · Why · Values · Failure · Detect · Implementation
maps/            one index per domain and per layer
checklists/      yes/no review passes per domain
platforms/       per-platform constants
deploy/          subagent template to copy into projects
CLAUDE.md        maintenance instructions (used only when working *on* the vault)
```

## Install (personal skill)

```bash
git clone https://github.com/<your-user>/ui-brain.git ~/Documents/vaults/ui-brain
```

The skill is two small files in `~/.claude/skills/ui-brain/` that point at the vault in place:
- `SKILL.md`: name, description and the lookup procedure, with absolute paths to the vault folders
- `scripts/find.sh` (executable): `find.sh` lists `path: description` for every note; `find.sh <keywords>` filters by description and aliases. Uses `rg`, falls back to `grep`. Set `UI_BRAIN_VAULT` if the vault lives elsewhere.

They aren't in this repo yet. Copy them from an existing machine, or ask Claude to recreate them from `CLAUDE.md` → *Deployment wiring*.

Let Claude read the vault without prompting. In `~/.claude/settings.json`:

```json
{ "permissions": { "allow": ["Read(~/Documents/vaults/ui-brain/**)", "Bash(~/.claude/skills/ui-brain/scripts/find.sh:*)"] } }
```

Optional design subagent (it preloads the skill):

```bash
mkdir -p ~/.claude/agents && cp ~/Documents/vaults/ui-brain/deploy/ui-designer.md ~/.claude/agents/
```

**Check it:** in a fresh session, run `/context`. Only the skill's name and description should be listed, not its body.

### Things to avoid
- Don't `@`-import vault notes into any `CLAUDE.md`, because that loads them in every session. The skill covers discovery.
- Don't use `--add-dir` on the vault together with `CLAUDE_CODE_ADDITIONAL_DIRECTORIES_CLAUDE_MD=1`. That loads the vault's *maintenance* `CLAUDE.md` into your project.
- Don't symlink the vault itself into a `.claude/skills/` folder. The vault no longer has a `SKILL.md`; the skill is the separate folder above.

## Terms of use (personal subscription)

This vault uses only built-in Claude Code features: skills, subagents, `CLAUDE.md`, and `claude -p` for headless checks. It does **not** use the Claude Agent SDK and contains no code that calls Claude. Running it in your own Claude Code session on your own Pro/Max account is ordinary individual use under the Consumer Terms.

Stay within that:
- Use it yourself, in your own Claude Code sessions.
- Don't wrap it in an app or service that lets **other people** use your claude.ai login. Anthropic doesn't allow third parties to offer claude.ai login or route requests through Free/Pro/Max credentials, and that includes Agent SDK apps.
- Plan limits assume ordinary individual use. Avoid unattended high-volume loops (e.g. scheduled bulk `claude -p` runs).
- If you later build an Agent SDK app around this knowledge, authenticate it with an **API key** from the Claude Console. The Agent SDK falls under the Commercial Terms.

Sources: [Claude Code legal and compliance](https://code.claude.com/docs/en/legal-and-compliance), [Agent SDK overview: authentication note](https://code.claude.com/docs/en/agent-sdk/overview).

## Update

```bash
cd ~/Documents/vaults/ui-brain && git pull
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
