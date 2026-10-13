---
name: repo-sync-mirrors
description: Use when a GitHub copy and a Cursor Origin copy of the same repo should match, using fast-forward only.
---

# Repo sync mirrors

Make the GitHub remote and the Cursor Origin remote point at the same commit
on one branch. Update a remote only when the update is a fast-forward.
Ground truth: [Fast-forward only](references/fast-forward-only.md). Do not
invent a second playbook — extend that doc when the pattern changes.

## Checklist

1. Use the remote names already configured. Do not put credentials in a remote URL.
2. Fetch both. If the tips match, stop.
3. If one tip is a strict ancestor of the other, fast-forward the behind remote. Do not force, rebase, or merge.
4. If the histories have diverged, stop and report both SHAs and the merge base. Leave both remotes unchanged.

## Read next

| Doc | When |
| --- | --- |
| [Fast-forward only](references/fast-forward-only.md) | Fetch, ancestor check, push, and TODOs |
| [Sync report](examples/sync-report.md) | The three outcomes to report |
