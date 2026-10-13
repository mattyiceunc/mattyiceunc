---
name: secrets-and-env-setup
description: Use when declaring required environment variables and secrets so a new checkout can build without committing secret values.
---

# Secrets and env setup

## Purpose

Document every variable a build or CI job needs, and keep the values out of
git. Example files list names only.

## Steps

1. Search for environment reads, Gradle properties, and CI secret references.
   List each name, where it is read, and whether local build, local run, or
   CI needs it.
2. Confirm tracked files and sample configs do not contain secret values. If
   a value is committed, stop and report the path. Do not copy that value
   into another file.
3. Add or update an example file, such as `.env.example` or
   `local.properties.example`, with names and short comments only. Point at
   it from the existing setup doc, or add a short section if the repo has
   none.
4. Ignore real env files, keystores, API-key files, and `local.properties`.
5. For CI, document the secret names the workflow expects. Store values in
   the forge secret store, not in workflow YAML.
6. From a clean shell, confirm the project reports missing names and that the
   example file has no live credentials.

## TODO

- [ ] Required variable names and which command needs each one
- [ ] Example-file path this project prefers
- [ ] Local keystore or signing-config convention
- [ ] CI secret store (repository secrets, an environment, or another store)
- [ ] Who may rotate values
