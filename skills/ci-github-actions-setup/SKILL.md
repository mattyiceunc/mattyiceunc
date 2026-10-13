---
name: ci-github-actions-setup
description: Use when adding or adjusting a GitHub Actions workflow that builds and tests the project.
---

# CI GitHub Actions setup

Make GitHub Actions run the same build and test commands a local check runs.
Ground truth: [Workflow shape](references/workflow-shape.md). Do not invent a
second playbook — extend that doc when the pattern changes.

## Checklist

1. Read current workflows and the local build and test commands before adding a file.
2. Extend the workflow that already runs those commands. Add a new workflow only if none does.
3. Set up the same JDK, cache Gradle the way the repo already does, and keep secret values out of the YAML.
4. Leave the job name equal to the status check branch protection should require.

## Read next

| Doc | When |
| --- | --- |
| [Workflow shape](references/workflow-shape.md) | Triggers, cache, secrets, and TODOs |
| [Workflow stub](examples/ci-workflow.yml) | A workflow to adapt |
