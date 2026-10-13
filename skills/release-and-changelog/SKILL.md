---
name: release-and-changelog
description: Use when cutting a versioned release and recording user-visible changes in the changelog.
---

# Release and changelog

## Purpose

Bump the version the project already uses, record user-visible changes, and
tag that commit. Stop before publishing if the version scheme or tag pattern
is unknown.

## Steps

1. Find how this repo versions artifacts: Git tag, Gradle version, Android
   `versionName` / `versionCode`, or another file. Read the existing changelog
   format before adding a section.
2. Collect user-visible changes since the last release from merged pull
   requests or commits. Group them as added, changed, fixed, and removed.
   Leave internal chores out unless this project's changelog includes them.
3. Bump the version in the single source of truth. If the project has both a
   version name and an Android `versionCode`, bump both using the project's
   rule.
4. Add a dated section for the new version. Do not rewrite older sections.
5. Commit the version bump and changelog together. Create an annotated tag
   that matches the project's tag pattern. Push the commit and the tag
   without force.
6. Publish release notes from that changelog section on the forge the project
   already uses.

## TODO

- [ ] Version file and scheme (SemVer, date, or `versionCode` rule)
- [ ] Tag pattern
- [ ] Changelog path and heading style
- [ ] Publication step (tag only, GitHub release, or another channel)
- [ ] Artifact build command, if a release must upload binaries
