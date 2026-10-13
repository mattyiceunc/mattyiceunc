---
name: pr-review-checklist
description: Use when reviewing a pull request and writing findings in a fixed order.
---

# PR review checklist

## Purpose

Review the change the pull request actually makes, then report blocking
issues before questions and nits.

## Steps

1. Read the description and the full diff. Note the behavior the author
   intends to change.
2. Check correctness: the code does what the description says, and edge cases
   introduced by the change are handled.
3. Check tests: new behavior has a test, or the author explained why it
   cannot. Existing tests still match the new behavior.
4. Check structure: public API, module boundaries, and Gradle wiring match
   the rest of the repo. Drive-by refactors are separate from the change.
5. Check safety: no secrets, tokens, or machine-local paths. No new broad
   permissions, exported components, or logging of private data unless that
   is the point of the change and it is justified.
6. Check CI: required workflows passed, or the missing run is called out.
7. Write the review in this order: blocking issues, questions, optional nits.
   Cite the file and the behavior. If nothing is blocking, say so.

## TODO

- [ ] Extra gates for this repo (design note, API review, screenshots)
- [ ] Owners who must be included
- [ ] Ticket or label convention the project expects on the pull request
