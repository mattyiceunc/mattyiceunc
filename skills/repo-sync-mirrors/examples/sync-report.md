# Sync report stub

Use one of these three reports. Replace every TODO. Do not include remote URLs when they contain credentials.

## Already in sync

```text
Outcome: already in sync
Remotes: TODO_GITHUB_REMOTE, TODO_ORIGIN_REMOTE
Branch: TODO_BRANCH
SHA: TODO_SHA
Push: no
```

## Fast-forwarded

```text
Outcome: fast-forwarded TODO_BEHIND_REMOTE
Remotes: TODO_GITHUB_REMOTE, TODO_ORIGIN_REMOTE
Branch: TODO_BRANCH
Before: TODO_BEHIND_SHA -> TODO_AHEAD_SHA
After: TODO_AHEAD_SHA on both
Push: yes, no --force
```

## Diverged

```text
Outcome: stopped, histories diverged
Remotes: TODO_GITHUB_REMOTE TODO_SHA_A
         TODO_ORIGIN_REMOTE TODO_SHA_B
Merge-base: TODO_MERGE_BASE
Push: no
Blocker: a person must choose how to reconcile
```
