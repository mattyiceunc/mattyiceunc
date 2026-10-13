# AGENTS.md

Project instructions for agents. Replace every TODO before relying on this
file. Skills from the personal library are installed under `.cursor/skills/`.
Re-copy a skill when the library copy changes.

## Skills

Read `.cursor/skills/<name>/SKILL.md` when its `description` matches the
task. Follow `references/` for the procedure and `examples/` for a stub.
Extend the reference when the pattern changes. Do not invent a second
playbook.

Installed skills (delete rows that are not installed):

- [ ] `agent-workflow` — fan-out, path handoffs, completion reports
- [ ] `kmp-module-scaffold`
- [ ] `android-gradle-upgrade`
- [ ] `write-tests-and-coverage`
- [ ] `ci-github-actions-setup`
- [ ] `pr-review-checklist`
- [ ] `release-and-changelog`
- [ ] `secrets-and-env-setup`
- [ ] `interview-prep-practice`
- [ ] `repo-sync-mirrors`

## Workflow

Follow `agent-workflow` when it is installed.

- One deliverable and shared files: one agent, or strict sequential ownership.
- Independent paths: a coordinator plus workers. Pass the store root and the
  exact target paths in every assignment. Workers do not discover that store
  on their own.
- Anything longer than a short verdict goes in a file. Chat gets the path.
- User-facing material goes in the docs path below. Evidence and working
  notes go in the internal path. Workers do not edit the coordinator status
  file unless that file is assigned to them.
- Done means a short report: outcome, path(s) written, blocker, and what was
  skipped.

## Project facts

- [ ] Docs path: TODO
- [ ] Working-notes path: TODO
- [ ] Coordinator status file: TODO
- [ ] Default branch: TODO
- [ ] Build command: TODO
- [ ] Test command: TODO
- [ ] Version source of truth: TODO
- [ ] GitHub remote name and Cursor Origin remote name, if this repo is mirrored: TODO
- [ ] Env example file path: TODO

## Safety

- Do not commit secrets, keystores, or local machine paths.
- Fast-forward mirrored remotes only. If the histories have diverged, stop.
- Do not force-push.
