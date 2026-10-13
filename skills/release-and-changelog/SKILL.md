---
name: release-and-changelog
description: Use when cutting a versioned release and recording user-visible changes in the changelog.
---

# Release and changelog

Bump the version the project already uses, record user-visible changes, and
tag that commit. Ground truth: [Release steps](references/release-steps.md).
Do not invent a second playbook — extend that doc when the pattern changes.

## Checklist

1. Read the current version source and the existing changelog format before editing.
2. Group user-visible changes since the last release. Leave internal chores out unless this changelog includes them.
3. Bump the version in one place. Add a dated section. Do not rewrite older sections.
4. Tag and push without force. Stop if the version scheme or tag pattern is unknown.

## Read next

| Doc | When |
| --- | --- |
| [Release steps](references/release-steps.md) | Version, tag, publish, and TODOs |
| [Changelog entry](examples/changelog-entry.md) | A section to adapt |
