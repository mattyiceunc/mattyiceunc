---
name: repo-sync-mirrors
description: Use when a GitHub copy and a Cursor Origin copy of the same repo should match, using fast-forward only.
---

# Repo sync mirrors

## Purpose

Make the GitHub remote and the Cursor Origin remote point at the same commit
on the tracked branch. Update a remote only when the update is a
fast-forward. If the histories have diverged, stop without changing either
remote.

## Steps

1. Confirm which remote is GitHub and which is Cursor Origin. Use the names
   already configured. Do not put credentials in the remote URL you pass on
   the command line.
2. Fetch both remotes and prune deleted remote branches. Record the branch
   name and the tip SHA on each remote.
3. If the two tips are equal, stop. The copies already match.
4. If one tip is a strict ancestor of the other, push the ahead tip to the
   behind remote with a fast-forward-only push. Do not force, rebase, squash,
   or create a merge commit.
5. If neither tip is an ancestor of the other, the branches have diverged.
   Stop. Report both SHAs and the merge base, and leave both remotes
   unchanged until a person chooses how to reconcile them.
6. After a fast-forward push, fetch both remotes again and confirm the tips
   match. Report the remote names, the branch, and the final SHA.

## TODO

- [ ] GitHub remote name
- [ ] Cursor Origin remote name
- [ ] Branch to keep in sync
- [ ] Whether feature branches are mirrored, or only the default branch
