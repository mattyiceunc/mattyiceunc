# GitHub Actions workflow shape

Playbook for `ci-github-actions-setup`. Extend this file when the pattern changes.

## Inputs

- Existing workflows under `.github/workflows/`
- The local build and test commands
- The JDK, Android SDK, or Gradle version those commands need
- The status-check name branch protection already requires, if any

## Steps

1. Read current workflows and the local commands before editing YAML.
2. If a workflow already runs those commands, edit that workflow. Do not add a second pipeline for the same job.
3. Check out the repo, set up the same JDK, and cache Gradle with the cache the repo already uses or with Gradle's current recommended action. Then run the project's build and test commands.
4. Trigger on pull requests and on pushes to the default branch, unless the repo documents a different trigger. Do not add a path filter that skips the workflow when shared build logic changes.
5. Keep secret values out of the workflow file. Reference a repository or environment secret by name only when a step cannot run without it.
6. Upload test or coverage artifacts only when the project already produces those reports.
7. Check that the YAML parses and that the job name is the status check branch protection should require.

## Anti-patterns

- A second workflow that duplicates an existing build job
- Pinning a path filter that ignores changes to the version catalog or convention plugins
- Putting a token, keystore, or password in the workflow or in this skill
- Running a heavier matrix than the local check until the single-job workflow is green

## TODO

- [ ] Gradle or other commands CI must run
- [ ] JDK and Android SDK versions
- [ ] Required status-check name
- [ ] Secret names the workflow may read (names only)
- [ ] Whether workflow files must also be mirrored outside GitHub

## Done

The workflow runs the project's build and test commands on pull requests and on the default branch, and the job name matches the required check.

## Report

Workflow path, job name, commands, blocker, and secret names referenced (never values).
