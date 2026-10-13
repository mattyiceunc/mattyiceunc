# Changelog entry stub

Match the heading style already in the project's changelog. If the project
has no changelog, start one with the sections below and record that choice.
Replace every TODO. Drop empty groups rather than leaving them as TODOs in
the published notes.

```markdown
## TODO_VERSION — TODO_DATE

### Added

- TODO_USER_VISIBLE_ADDITION

### Changed

- TODO_USER_VISIBLE_CHANGE

### Fixed

- TODO_USER_VISIBLE_FIX

### Removed

- TODO_USER_VISIBLE_REMOVAL
```

Annotated tag, only after the version scheme TODO is filled:

```text
git tag -a TODO_TAG -m "TODO_VERSION"
git push TODO_REMOTE TODO_TAG
```

Do not pass `--force`.
