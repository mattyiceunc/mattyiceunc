# Android Gradle upgrade order

Playbook for `android-gradle-upgrade`. Extend this file when the pattern changes.

## Inputs

- Current Gradle wrapper, Android Gradle Plugin, Kotlin, compileSdk, targetSdk, minSdk, and JDK toolchain
- The file that owns each value (wrapper properties, version catalog, or convention plugin)
- The Android Gradle Plugin and Gradle compatibility table for the target AGP

## Order

Upgrade one axis per change. When the compatibility table requires a predecessor, use this order:

1. JDK toolchain, if the new Android Gradle Plugin requires it
2. Gradle wrapper
3. Android Gradle Plugin
4. Kotlin
5. compileSdk, then targetSdk, then minSdk only if the project intends that bump

Edit the single source of truth, not every module.

## Steps

1. Record the current versions and their owning files before editing.
2. Apply one bump from the order above.
3. Refresh dependencies. Compile a representative Android target and run its unit tests.
4. Read the first real error before changing another version.
5. Fix deprecations that fail the build. Leave formatting and unrelated refactors for a separate change.
6. Run the same compile and test commands again. Report the old version, the new version, and anything still blocked.

## Anti-patterns

- Bumping Gradle, Android Gradle Plugin, Kotlin, and SDK levels in one change
- Copying a version into every module when a catalog or convention plugin already owns it
- Working around a failed upgrade by lowering a lint or test task so the build goes green

## TODO

- [ ] Target Gradle, Android Gradle Plugin, Kotlin, and SDK versions
- [ ] JDK version required by that combination
- [ ] Commands this project uses to compile and test
- [ ] Whether a version catalog or `buildSrc` owns the versions

## Done

One axis is bumped, the recorded compile and unit-test commands pass, and no other version moved.

## Report

Old version, new version, commands run, blocker, and axes left for a later change.
