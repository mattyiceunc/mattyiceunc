---
name: kmp-module-scaffold
description: Use when adding a new Kotlin Multiplatform module, its source sets, and its Gradle wiring to an existing project.
---

# KMP module scaffold

Add one Kotlin Multiplatform module that matches the project's Gradle layout.
Ground truth: [Module layout](references/module-layout.md). Do not invent a
second playbook — extend that doc when the pattern changes.

## Checklist

1. Match sibling modules (plugins, source-set names, package root) before creating files.
2. Pick one module kind, and add only the source sets that kind needs.
3. Register it in settings. Depend on it only with the notation the repo already uses.
4. Compile the new module and run its common test. Fix only breakages it caused.
5. If package, targets, or plugin aliases are undecided, stop and fill the TODOs in the reference.

## Read next

| Doc | When |
| --- | --- |
| [Module layout](references/module-layout.md) | Steps, source sets, Gradle wiring, TODOs |
| [Feature module stub](examples/feature-module.md) | A skeleton to adapt |
