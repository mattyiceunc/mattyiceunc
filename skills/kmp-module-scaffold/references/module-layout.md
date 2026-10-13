# KMP module layout

Playbook for `kmp-module-scaffold`. Extend this file when the pattern changes.

## Inputs

- Existing modules, the version catalog or convention plugins, and the settings file
- One module kind: shared logic, a single platform, or a feature with more than one target

## Steps

1. Read the existing module layout before creating files. Match convention plugins or per-module build files, source-set names, and the package root.
2. Write down the module kind. Do not scaffold a second module in the same change.
3. Create the module directory and a `build.gradle.kts` that applies the same Kotlin Multiplatform plugin the sibling modules use. Apply the Android plugin only when a sibling multiplatform module does.
4. Add the source sets the project already uses. Start with `commonMain` and `commonTest`. Add a platform set such as `androidMain` or `iosMain` only when a chosen target needs it. Put one public type in `commonMain` and one unit test in `commonTest`.
5. Register the module in the root settings file. If another module should depend on it, add that dependency with the notation already in the repo.
6. Sync, compile the new module, and run its common tests. Fix only breakages caused by the new module.
7. If the project does not already decide the package, targets, or plugin aliases, stop. Fill the TODOs below before writing more code.

## Source sets

| Kind | Start with | Add only when a target needs it |
| --- | --- | --- |
| Shared logic | `commonMain`, `commonTest` | Platform sets the siblings already declare |
| Single platform | The source sets of the sibling module on that platform | Sets for platforms this module does not target |
| Multi-target feature | `commonMain`, `commonTest` | One platform set per chosen target |

## Anti-patterns

- Inventing a package, target, or plugin version the repo does not use
- Copying an external sample when a sibling module is the template
- Retuning unrelated modules, catalogs, or wrapper versions in the scaffold change

## TODO

- [ ] Module name and Gradle path
- [ ] Package prefix
- [ ] Targets (Android, iOS, JVM, JS, Wasm, native)
- [ ] Whether an Android namespace or manifest is required
- [ ] Version-catalog aliases for the Kotlin and Android plugins

## Done

The new module is included from settings, its common test task passes, and the diff does not retune unrelated modules.

## Report

Outcome, paths written, blocker, and what was skipped (targets not added, package still TODO).
