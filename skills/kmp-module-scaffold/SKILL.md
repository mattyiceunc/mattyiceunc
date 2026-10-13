---
name: kmp-module-scaffold
description: Use when adding a new Kotlin Multiplatform module, its source sets, and its Gradle wiring to an existing project.
---

# KMP module scaffold

## Purpose

Add one Kotlin Multiplatform module that matches the project's current Gradle
layout. Keep the new module small enough to compile and test before filling
in real features.

## Steps

1. Read the existing module layout and version catalog before creating files.
   Match the style already in the repo: convention plugins or per-module build
   files, source-set names, and the package root.
2. Choose the module kind and write it down: shared logic, a single platform,
   or a feature with more than one target.
3. Create the module directory and a `build.gradle.kts` that applies the same
   Kotlin Multiplatform plugin (and the Android plugin only if a sibling
   module does).
4. Add the source sets the project already uses. Start with `commonMain` and
   `commonTest`. Add platform sets such as `androidMain` or `iosMain` only
   when a chosen target needs them. Put one public type and one unit test in
   `commonTest`.
5. Register the module in the root settings file. If another module should
   depend on it, add that dependency with the notation the repo already uses.
6. Sync, compile the new module, and run its common tests. Fix only breakages
   caused by the new module.
7. If the project does not already decide the package, targets, or plugin
   aliases, stop and resolve the TODOs before writing more code.

## TODO

- [ ] Module name and Gradle path
- [ ] Package prefix
- [ ] Targets (Android, iOS, JVM, JS, Wasm, native)
- [ ] Whether an Android namespace or manifest is required
- [ ] Version-catalog aliases for the Kotlin and Android plugins
