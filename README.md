# skills

A personal collection of agent skills — curated copies of upstream skills plus self-developed ones — for extending coding agents (OpenCode, Claude Code, Codex, Cursor, and [30+ others](https://github.com/antfu/skills-cli#supported-agents)).

Skills are reusable instruction packs: each one is a directory with a `SKILL.md` (YAML frontmatter + Markdown body) and optional supporting files.

## Install

From any project, install with the [`npx skills`](https://github.com/antfu/skills-cli) CLI (GitHub is the registry):

```bash
# install all skills from this repo
npx skills add makmu/skills

# install one skill by name (quote multi-word names)
npx skills add makmu/skills --skill my-skill

# see what's available without installing
npx skills add makmu/skills --list

# install globally instead of per-project
npx skills add makmu/skills -g

# target a specific agent (default: auto-detected)
npx skills add makmu/skills -a opencode
```

Full repo URLs, git URLs, and local paths (`npx skills add ./skills`) also work as sources.

Other commands: `npx skills list` (installed skills), `npx skills find <query>` (search the ecosystem), `npx skills check` / `npx skills update`.

## Layout

```
skills/
  my-skill/
    SKILL.md        # required: name + description frontmatter, then instructions
    scripts/        # optional supporting files
```

A minimal `SKILL.md`:

```markdown
---
name: my-skill
description: What this skill does and when to use it
---

# My Skill

Instructions the agent follows when the skill is activated.
```

The `description` drives discovery — write it as "what it does and when to use it".

## Adding a skill

- **Self-developed:** scaffold with `npx skills init my-skill` inside `skills/`, then fill in the body.
- **Curated copies:** keep the upstream author, license, and source URL in the `SKILL.md`; don't rebrand.
- Mark work-in-progress skills as internal so they stay hidden from discovery:

  ```yaml
  ---
  name: my-skill
  description: ...
  metadata:
    internal: true
  ---
  ```

  (visible only when `INSTALL_INTERNAL_SKILLS=1` is set)

Agent-facing conventions and verification steps live in [AGENTS.md](./AGENTS.md).
