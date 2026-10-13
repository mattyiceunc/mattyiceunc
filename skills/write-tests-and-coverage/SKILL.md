---
name: write-tests-and-coverage
description: Use when adding tests for a change and producing a coverage report with the repo's existing runner.
---

# Write tests and coverage

## Purpose

Add tests for the behavior that just changed, then report coverage with the
tool the project already uses. Do not lower an existing coverage gate to make
a run pass.

## Steps

1. Find the test stack already in the repo (JUnit, kotlin.test, Kotest,
   Turbine, Robolectric, instrumented tests) and any coverage plugin (Kover,
   JaCoCo, or an Android report task).
2. List the behaviors the change must keep. Write tests at the seam the
   project already uses, such as a pure function, a view model, or a
   repository. Prefer unit tests unless the behavior needs a device.
3. Cover the success path, one meaningful failure or edge path, and any
   branch the change added.
4. Run the narrowest test task that includes the new tests. If coverage is
   already wired, run it for that same scope.
5. If coverage is not wired, add the project's preferred plugin on the module
   that owns the code and point it at unit-test results. Do not invent a
   numeric threshold.
6. Report the commands, pass or fail, and coverage for the touched code.

## TODO

- [ ] Test framework and assertion style
- [ ] Coverage plugin and Gradle task names
- [ ] Coverage threshold, if this project wants one
- [ ] Packages or build variants to exclude
