---
name: write-tests-and-coverage
description: Use when adding tests for a change and producing a coverage report with the repo's existing runner.
---

# Write tests and coverage

Add tests for the behavior that just changed, then report coverage with the
tool the project already uses. Ground truth:
[Tests and coverage](references/test-and-coverage.md). Do not invent a
second playbook — extend that doc when the pattern changes.

## Checklist

1. Use the test stack and coverage plugin already in the repo.
2. Cover the success path, one edge or failure path, and any branch the change added.
3. Run the narrowest test task that includes the new tests, then coverage for that same scope if it is already wired.
4. Do not invent a numeric gate, and do not lower an existing one to go green.

## Read next

| Doc | When |
| --- | --- |
| [Tests and coverage](references/test-and-coverage.md) | Seams, commands, and TODOs |
| [Common test stub](examples/common-test.md) | A unit-test skeleton to adapt |
