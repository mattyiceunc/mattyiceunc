# Personal Cursor skills

Repo-agnostic agent skills for day-to-day project work. Each skill is a
directory with one `SKILL.md`. Nothing here names a specific repository,
package, or secret.

Copy a skill into a project so Cursor loads it from that project's
`.cursor/skills/` directory. This folder is the library. The project copy
is what the agent reads.

## Install into a project

From the root of the target project, copy only the skills you want:

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

Do not commit secrets, machine-local paths, or project-specific values back
into this library. Fill those in the project copy, or leave the `TODO`
items for the agent to resolve from that repo.

## Skills

| Skill | Use when |
| --- | --- |
| [kmp-module-scaffold](kmp-module-scaffold/SKILL.md) | Adding a Kotlin Multiplatform module and its Gradle wiring. |
| [android-gradle-upgrade](android-gradle-upgrade/SKILL.md) | Bumping Gradle, Android Gradle Plugin, Kotlin, or SDK levels. |
| [write-tests-and-coverage](write-tests-and-coverage/SKILL.md) | Adding tests and a coverage report for a change. |
| [ci-github-actions-setup](ci-github-actions-setup/SKILL.md) | Adding or adjusting a GitHub Actions build-and-test workflow. |
| [pr-review-checklist](pr-review-checklist/SKILL.md) | Reviewing a pull request with a fixed pass. |
| [release-and-changelog](release-and-changelog/SKILL.md) | Cutting a version and writing the changelog. |
| [secrets-and-env-setup](secrets-and-env-setup/SKILL.md) | Declaring env and secrets so a checkout can build. |
| [interview-prep-practice](interview-prep-practice/SKILL.md) | Running a timed computer-science practice session. |
| [repo-sync-mirrors](repo-sync-mirrors/SKILL.md) | Fast-forwarding GitHub and Cursor Origin copies onto the same commit. |

## Format

`name` matches the directory. `description` is the one-line hint Cursor uses
to decide when to load the skill. The body has a purpose, ordered steps, and
`TODO` markers for anything that must stay project-specific.
