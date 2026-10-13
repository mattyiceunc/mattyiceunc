# Fast-forward only

Playbook for `repo-sync-mirrors`. Extend this file when the pattern changes.
This updates a remote ref only when git accepts a fast-forward. It does not
reconcile diverged history.

## Inputs

- The GitHub remote name and the Cursor Origin remote name already configured
- The branch to keep in sync
- A fetch of both remotes. Do not add a remote whose URL contains a token.

## Steps

1. Confirm which remote is GitHub and which is Cursor Origin. If either TODO below is still unknown, stop.
2. Fetch both remotes and prune deleted remote branches. Record the branch name and the tip SHA on each remote.
3. If the two tips are equal, stop. The copies already match.
4. If one tip is a strict ancestor of the other, push that ahead SHA to the behind remote's branch. A push without `--force` is rejected when it is not a fast-forward. Do not pass `--force` or `--force-with-lease`. Do not rebase, squash, or create a merge commit.
5. If neither tip is an ancestor of the other, stop. Report both SHAs and the merge base. Leave both remotes unchanged until a person chooses how to reconcile them.
6. After a fast-forward push, fetch both remotes again and confirm the tips match. Report the remote names, the branch, and the final SHA.

Use the ahead SHA explicitly so the push does not depend on a dirty local branch:

```bash
git fetch TODO_GITHUB_REMOTE --prune
git fetch TODO_ORIGIN_REMOTE --prune
git rev-parse TODO_GITHUB_REMOTE/TODO_BRANCH
git rev-parse TODO_ORIGIN_REMOTE/TODO_BRANCH
git merge-base --is-ancestor TODO_BEHIND_SHA TODO_AHEAD_SHA
git push TODO_BEHIND_REMOTE TODO_AHEAD_SHA:TODO_BRANCH
```

`git merge-base --is-ancestor` exits 0 when the first SHA is an ancestor of the second. If it fails both ways, the branches have diverged. The merge base for the report is:

```bash
git merge-base TODO_GITHUB_SHA TODO_ORIGIN_SHA
```

## Anti-patterns

- `--force`, `--force-with-lease`, or deleting the diverged branch to "unblock" the sync
- A merge commit or rebase to paper over divergence
- Putting a token or username in the remote URL passed on the command line
- Mirroring every feature branch when the TODO says only the default branch

## TODO

- [ ] GitHub remote name
- [ ] Cursor Origin remote name
- [ ] Branch to keep in sync
- [ ] Whether feature branches are mirrored, or only the default branch

## Done

Both remote tips for the branch are equal, or the sync stopped because the histories diverged and neither remote was updated.

## Report

Remote names, branch, both SHAs before the push, the final SHA or the merge base, and whether a push happened.
