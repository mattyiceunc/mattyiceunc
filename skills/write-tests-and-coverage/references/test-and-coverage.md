# Tests and coverage

Playbook for `write-tests-and-coverage`. Extend this file when the pattern changes.

## Inputs

- The behavior the change must keep
- The test stack already in the repo (JUnit, kotlin.test, Kotest, Turbine, Robolectric, or instrumented tests)
- The coverage plugin if one exists (Kover, JaCoCo, or an Android report task)

## Steps

1. Find the test stack and any coverage task before adding a dependency.
2. List the behaviors the change must keep. Write tests at the seam the project already uses: a pure function, a view model, or a repository. Prefer a unit test unless the behavior needs a device.
3. Cover the success path, one meaningful failure or edge path, and any branch the change added.
4. Run the narrowest test task that includes the new tests.
5. If coverage is already wired, run it for that same scope. If it is not wired, add the project's preferred plugin on the module that owns the code and point it at unit-test results. Do not invent a numeric threshold.
6. Report the commands, pass or fail, and coverage for the touched code. Do not lower an existing threshold to make a run pass.

## Anti-patterns

- Snapshotting unrelated UI to raise a coverage number
- Adding a second test framework beside the one the module already uses
- Skipping the failure path when the change added an error branch
- Treating an instrumented test as the default when a unit test can reach the seam

## TODO

- [ ] Test framework and assertion style
- [ ] Coverage plugin and Gradle task names
- [ ] Coverage threshold, if this project wants one
- [ ] Packages or build variants to exclude

## Done

New tests fail if the new behavior is removed, the narrow test task passes, and coverage for the touched code is reported or explicitly absent.

## Report

Commands, pass or fail, coverage for the touched code, blocker, and cases not covered.
