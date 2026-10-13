# PR review pass

Playbook for `pr-review-checklist`. Extend this file when the pattern changes.

## Inputs

- The pull request description and the full diff
- Required CI status checks
- Any extra gates listed in the TODOs below

## Steps

1. Read the description and the full diff. Note the behavior the author intends to change.
2. Correctness: the code does what the description says, and edge cases introduced by the change are handled.
3. Tests: new behavior has a test, or the author explained why it cannot. Existing tests still match the new behavior.
4. Structure: public API, module boundaries, and Gradle wiring match the rest of the repo. Drive-by refactors are separate from the change.
5. Safety: no secrets, tokens, or machine-local paths. No new broad permissions, exported components, or logging of private data unless that is the point of the change and it is justified.
6. CI: required workflows passed, or the missing run is called out.
7. Write the review in this order: blocking issues, questions, optional nits. Cite the file and the behavior. If nothing is blocking, say so.

## Anti-patterns

- Reviewing only the files that look familiar and skipping the rest of the diff
- Asking for a refactor that the change does not require
- Approving while a required check is missing and unmentioned
- Pasting the whole diff back into the review

## TODO

- [ ] Extra gates for this repo (design note, API review, screenshots)
- [ ] Owners who must be included
- [ ] Ticket or label convention the project expects on the pull request

## Done

The review covers the intended behavior, cites files for anything blocking, and states whether CI is green.

## Report

Blocking count, questions, nits, and checks that did not run. Link the review; do not paste the diff.
