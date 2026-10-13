---
name: android-gradle-upgrade
description: Use when bumping Gradle, the Android Gradle Plugin, Kotlin, or compile and target SDK levels.
---

# Android Gradle upgrade

## Purpose

Upgrade the Android and Kotlin build toolchain in small steps, with a compile
and test check after each step. Keep unrelated cleanups out of the upgrade.

## Steps

1. Record the current Gradle wrapper, Android Gradle Plugin, Kotlin,
   compileSdk, targetSdk, minSdk, and JDK toolchain. Note the file that owns
   each value.
2. Upgrade one axis at a time. Prefer this order when a compatibility table
   requires it: JDK toolchain, Gradle wrapper, Android Gradle Plugin, Kotlin,
   then SDK levels. Check the Android Gradle Plugin and Gradle compatibility
   table before editing.
3. Change the version in the single source of truth (version catalog or
   convention plugin), not once per module.
4. Refresh dependencies and compile a representative Android target plus its
   unit tests. Read the first real error before changing another version.
5. Fix deprecations that fail the build. Leave formatting and unrelated
   refactors for a separate change.
6. Run the same compile and test commands again. Report the old version, the
   new version, and anything still blocked.

## TODO

- [ ] Target Gradle, Android Gradle Plugin, Kotlin, and SDK versions
- [ ] JDK version required by that combination
- [ ] Commands this project uses to compile and test
- [ ] Whether a version catalog or `buildSrc` owns the versions
