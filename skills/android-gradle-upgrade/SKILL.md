---
name: android-gradle-upgrade
description: Use when bumping Gradle, the Android Gradle Plugin, Kotlin, or compile and target SDK levels.
---

# Android Gradle upgrade

Bump the Android and Kotlin build toolchain one axis at a time.
Ground truth: [Upgrade order](references/upgrade-order.md). Do not invent a
second playbook — extend that doc when the pattern changes.

## Checklist

1. Record the current wrapper, Android Gradle Plugin, Kotlin, SDK levels, and JDK toolchain, and the file that owns each one.
2. Change one axis in the single source of truth. Check the compatibility table before editing.
3. Compile one Android target and run its unit tests. Read the first real error before bumping anything else.
4. Leave unrelated cleanups out of the upgrade change.

## Read next

| Doc | When |
| --- | --- |
| [Upgrade order](references/upgrade-order.md) | Order, verification, and TODOs |
| [Version catalog stub](examples/version-catalog.md) | A one-axis bump to adapt |
