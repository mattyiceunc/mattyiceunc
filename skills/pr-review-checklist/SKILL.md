---
name: pr-review-checklist
description: Use when reviewing a pull request and writing findings in a fixed order.
---

# PR review checklist

Review the change the pull request actually makes, then report blocking
issues before questions and nits. Ground truth:
[Review pass](references/review-pass.md). Do not invent a second playbook —
extend that doc when the pattern changes.

## Checklist

1. Read the description and the full diff. Note the behavior the author intends to change.
2. Check correctness, tests, structure, safety, and CI, in that order.
3. Write blocking issues, then questions, then nits. Cite the file and the behavior.
4. If nothing is blocking, say so.

## Read next

| Doc | When |
| --- | --- |
| [Review pass](references/review-pass.md) | What each check covers, and TODOs |
| [Review notes](examples/review-notes.md) | A writeup to adapt |
