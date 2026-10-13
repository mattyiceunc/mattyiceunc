# Env inventory

Playbook for `secrets-and-env-setup`. Extend this file when the pattern changes.
Example files list names only. Never write a live token, keystore password, or
API key into the skill, the example, or a commit.

## Inputs

- Environment reads, Gradle properties, and CI secret references in the repo
- The example-file path the project already prefers
- Ignore rules for env files, keystores, and `local.properties`

## Steps

1. Search for environment reads, Gradle properties, and CI secret references. List each name, where it is read, and whether local build, local run, or CI needs it.
2. Confirm tracked files and sample configs do not contain secret values. If a value is committed, stop and report the path. Do not copy that value into another file.
3. Add or update an example file, such as `.env.example` or `local.properties.example`, with names and short comments only. Point at it from the existing setup doc, or add a short section if the repo has none.
4. Ignore real env files, keystores, API-key files, and `local.properties`.
5. For CI, document the secret names the workflow expects. Store values in the forge secret store, not in workflow YAML.
6. From a clean shell, confirm the project reports missing names and that the example file has no live credentials.

## Inventory

Copy this table into the project's setup notes and fill it there. Do not fill values in this library.

| Name | Read from | Needed for | Example file |
| --- | --- | --- | --- |
| TODO_NAME | TODO_FILE | local build, local run, or CI | TODO_EXAMPLE_PATH |

## Anti-patterns

- Committing `.env`, `local.properties`, or a keystore "just for CI"
- Putting a real-looking token in an example to show the shape
- Duplicating secret values into workflow YAML, skill docs, or chat

## TODO

- [ ] Required variable names and which command needs each one
- [ ] Example-file path this project prefers
- [ ] Local keystore or signing-config convention
- [ ] CI secret store (repository secrets, an environment, or another store)
- [ ] Who may rotate values

## Done

A new checkout can see which names are missing, the example file has no live credentials, and CI references names only.

## Report

Example path, names added, any committed secret path found, blocker, and names still unknown.
