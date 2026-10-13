# Using this skills library

This folder is a personal library of repo-agnostic Cursor agent skills. The
profile `README.md` is only a title and a link here. Do not add repository
names, packages, or secrets to the library.

## Discovery

Cursor does not load these skills from the profile repo. A project loads a
skill only after that skill directory is copied or symlinked to
`.cursor/skills/<skill-name>/SKILL.md`.

Start at [README.md](README.md). Match the task to a skill's frontmatter
`description`, then read that `SKILL.md`. Do not load `_templates/` as a
skill.

## Read order

1. `SKILL.md` — when to use the skill, the short checklist, and links.
2. `references/` — the playbook. Extend that doc when the pattern changes.
   Do not invent a second procedure in chat or in another file.
3. `examples/` — a stub to adapt. It is not a finished project file. Replace
   every TODO before using it.

If the next step needs the previous step's content, stay sequential. If it
needs only a path or acceptance criteria, fan out. Orchestration rules live
in [agent-workflow](agent-workflow/SKILL.md).

## Install into a project

```bash
mkdir -p .cursor/skills
cp -R /path/to/mattyiceunc/skills/<skill-name> /path/to/project/.cursor/skills/
```

Copy the whole skill directory so `references/` and `examples/` stay next to
`SKILL.md`. Re-copy after this library changes. Symlink the directory instead
when one checkout should be the source of truth.

For a new project, copy [_templates/AGENTS.md](_templates/AGENTS.md) to the
project root and fill its TODOs. Author a new skill from
[_templates/SKILL.md](_templates/SKILL.md) plus the template `references/`
and `examples/` folders.

## Editing this library

- Keep each `SKILL.md` short. Put steps, anti-patterns, and TODOs in
  `references/`. Put one concrete stub in `examples/`.
- `name` matches the directory. `description` says when to use the skill.
  Live skills other than `agent-workflow` keep that to one line starting
  with "Use when".
- Hand off paths, not file bodies.
- When finished, report outcome, path(s) written, blocker, and what was
  skipped.
- Leave the profile `README.md` unchanged except for its existing link to
  `skills/`.

## What not to do

- Do not install `_templates` into `.cursor/skills/`.
- Do not commit secret values, keystores, or machine-local paths.
- Do not parallel-write the same `SKILL.md` without a named owner.
- Do not fork a skill's reference into a second playbook.
