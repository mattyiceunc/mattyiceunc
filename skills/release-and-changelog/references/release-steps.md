# Release steps

Playbook for `release-and-changelog`. Extend this file when the pattern changes.

## Inputs

- How this repo versions artifacts: Git tag, Gradle version, Android `versionName` / `versionCode`, or another file
- The changelog path and heading style, if one exists
- The tag pattern and the forge used to publish notes

## Steps

1. Find the version source of truth and read the existing changelog format before adding a section.
2. Collect user-visible changes since the last release from merged pull requests or commits. Group them as added, changed, fixed, and removed. Leave internal chores out unless this project's changelog includes them.
3. Bump the version in the single source of truth. If the project has both a version name and an Android `versionCode`, bump both using the project's rule.
4. Add a dated section for the new version. Do not rewrite older sections.
5. Commit the version bump and changelog together. Create an annotated tag that matches the project's tag pattern. Push the commit and the tag without force.
6. Publish release notes from that changelog section on the forge the project already uses. Stop before publishing if the version scheme or tag pattern is unknown.

## Anti-patterns

- Force-pushing the release commit or moving an existing tag
- Editing a previously released changelog section
- Bumping `versionName` and leaving `versionCode` unchanged when the project ships both
- Publishing when the tag pattern TODO is still open

## TODO

- [ ] Version file and scheme (SemVer, date, or `versionCode` rule)
- [ ] Tag pattern
- [ ] Changelog path and heading style
- [ ] Publication step (tag only, GitHub release, or another channel)
- [ ] Artifact build command, if a release must upload binaries

## Done

The version file and changelog section match, the annotated tag points at that commit, and the push was a fast-forward.

## Report

Version, tag, changelog path, publish link or "not published", blocker, and what was skipped.
