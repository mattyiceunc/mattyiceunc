---
name: ci-github-actions-setup
description: Use when adding or adjusting a GitHub Actions workflow that builds and tests the project.
---

# CI GitHub Actions setup

## Purpose

Make GitHub Actions run the same build and test commands a local check would
run. Extend an existing workflow when one already does that job.

## Steps

1. Read current workflows, the local build and test commands, and the JDK,
   Android SDK, or Gradle version those commands need.
2. If a workflow already runs those commands, edit that workflow instead of
   adding a second pipeline.
3. Check out the repo, set up the same JDK, and cache Gradle with the cache
   the repo already uses or with Gradle's current recommended cache. Then run
   the project's build and test commands.
4. Trigger on pull requests and on pushes to the default branch, unless the
   repo documents a different trigger. Do not add a path filter that skips
   the workflow when shared build logic changes.
5. Keep secret values out of the workflow file. Reference a repository or
   environment secret by name only when a step cannot run without it.
6. Upload test or coverage artifacts only when the project already produces
   those reports.
7. Check that the YAML parses and that the job name is the status check branch
   protection should require.

## TODO

- [ ] Gradle or other commands CI must run
- [ ] JDK and Android SDK versions
- [ ] Required status-check name
- [ ] Secret names the workflow may read (names only)
- [ ] Whether workflow files must also be mirrored outside GitHub
