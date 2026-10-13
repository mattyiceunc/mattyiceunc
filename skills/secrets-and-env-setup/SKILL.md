---
name: secrets-and-env-setup
description: Use when declaring required environment variables and secrets so a new checkout can build without committing secret values.
---

# Secrets and env setup

Document every variable a build or CI job needs, and keep the values out of
git. Ground truth: [Env inventory](references/env-inventory.md). Do not
invent a second playbook — extend that doc when the pattern changes.

## Checklist

1. List each variable name, where it is read, and whether local build, local run, or CI needs it.
2. If a secret value is already committed, stop and report the path. Do not copy it.
3. Update the example file with names and comments only. Ignore the real env files and keystores.
4. Point CI at secret names in the forge secret store, not at values in the workflow.

## Read next

| Doc | When |
| --- | --- |
| [Env inventory](references/env-inventory.md) | Search, ignore rules, and TODOs |
| [Example env file](examples/env.example) | Names and comments to adapt |
