# Personal Cursor skills

Repo-agnostic agent skills for day-to-day project work. Each skill is a
directory: a short `SKILL.md`, a longer playbook in `references/`, and a stub
in `examples/`. Nothing here names a specific repository, package, or secret.

Agents working in this library should read [AGENTS.md](AGENTS.md) first.
Copy a skill into a project so Cursor loads it from that project's
`.cursor/skills/` directory. This folder is the library. The project copy
is what the agent reads.

## Install into a project

From the root of the target project, copy only the skills you want. Copy the
whole skill directory so the reference and the example stay beside `SKILL.md`:

```bash
mkdir -p .cursor/skills
cp -R /path/to/mattyiceunc/skills/<skill-name> .cursor/skills/
```

Cursor reads `.cursor/skills/<skill-name>/SKILL.md`. Re-copy a skill after
you change it here.

To keep a single source of truth, symlink instead of copying:

```bash
mkdir -p .cursor/skills
ln -s /absolute/path/to/mattyiceunc/skills/<skill-name> .cursor/skills/<skill-name>
```

For a new project, copy [_templates/AGENTS.md](_templates/AGENTS.md) to the
project root and fill its TODOs. Author a new skill from
[_templates/SKILL.md](_templates/SKILL.md). Do not copy `_templates` into
`.cursor/skills/`.

Do not commit secrets, machine-local paths, or project-specific values back
into this library. Fill those in the project copy, or leave the `TODO`
items in the skill's `references/` doc.

## Skills

| Skill | Use when |
| --- | --- |
| [agent-workflow](agent-workflow/SKILL.md) | Choosing single-agent vs coordinator work, path handoffs, and where notes live. |
| [kmp-module-scaffold](kmp-module-scaffold/SKILL.md) | Adding a Kotlin Multiplatform module and its Gradle wiring. |
| [android-gradle-upgrade](android-gradle-upgrade/SKILL.md) | Bumping Gradle, Android Gradle Plugin, Kotlin, or SDK levels. |
| [write-tests-and-coverage](write-tests-and-coverage/SKILL.md) | Adding tests and a coverage report for a change. |
| [ci-github-actions-setup](ci-github-actions-setup/SKILL.md) | Adding or adjusting a GitHub Actions build-and-test workflow. |
| [pr-review-checklist](pr-review-checklist/SKILL.md) | Reviewing a pull request with a fixed pass. |
| [release-and-changelog](release-and-changelog/SKILL.md) | Cutting a version and writing the changelog. |
| [secrets-and-env-setup](secrets-and-env-setup/SKILL.md) | Declaring env and secrets so a checkout can build. |
| [interview-prep-practice](interview-prep-practice/SKILL.md) | Running a timed computer-science practice session. |
| [repo-sync-mirrors](repo-sync-mirrors/SKILL.md) | Fast-forwarding GitHub and Cursor Origin copies onto the same commit. |
| [jev](jev/SKILL.md) | Classifying, scoring, or routing a ticket or incoming item as a Jev decision. |

## Layout

| Path | Role |
| --- | --- |
| `skills/AGENTS.md` | How agents discover and use this library |
| `skills/<name>/SKILL.md` | Short checklist and links. `name` matches the directory |
| `skills/<name>/references/` | Playbook. Extend this instead of starting a second procedure |
| `skills/<name>/examples/` | A stub to adapt. Not a finished project file |
| `skills/_templates/SKILL.md` | Starting point for a new skill |
| `skills/_templates/AGENTS.md` | Starting point for a new project's root `AGENTS.md` |

`description` is the one-line hint Cursor uses to decide when to load the
skill. `agent-workflow` uses a folded description because it names several
triggers; the other skills stay on one line.
