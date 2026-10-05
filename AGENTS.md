# AGENTS.md

Personal collection of agent skills — curated copies of upstream skills plus self-developed ones — that get installed into other projects with the `npx skills` CLI. GitHub acts as the registry: consumers run `npx skills add <owner>/skills` from any project (full URLs, git URLs, and local paths also work).

## Structure

- One skill per directory: `skills/<name>/SKILL.md`. This is the CLI's standard discovery location; `npx skills add . --list` shows what it finds in this repo.
- `SKILL.md` = YAML frontmatter + Markdown body. Frontmatter **requires** `name` (lowercase, hyphens allowed) and `description` (what it does and when to use it — this drives discovery).
- Supporting files (scripts, references) live inside the skill directory; the whole directory is the installable unit.
- Work-in-progress skills: add `metadata.internal: true` to hide them from discovery unless `INSTALL_INTERNAL_SKILLS=1`.

## Conventions

- The command is `npx skills add` — there is no `npx skills install` subcommand.
- Curated skills: keep upstream author, license, and source URL in the `SKILL.md`; don't rebrand.
- Scaffold new skills with `npx skills init <name>` inside `skills/`, then fill in the body.
- Smoke-test before pushing: `npx skills add . --list` here, then `npx skills add . -a opencode -y` in a scratch project (OpenCode reads `.opencode/skills/`, or `~/.config/opencode/skills/` with `-g`).
- Other commands: `npx skills list` (installed), `npx skills find <query>` (search registry), `npx skills check` / `update`.
