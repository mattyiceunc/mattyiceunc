# Jev decisions

Playbook for `jev`. Extend this file when the pattern changes. The v1 labels
and the decision shape below are fixed. Do not add a label.

## What Jev owns

Jev classifies, scores, and routes. It returns a typed decision. It does not
schedule, change code, or own panes.

| Layer | Owns | Does not own |
| --- | --- | --- |
| Jev | Classify / score / route (typed decisions) | Scheduling, code changes, panes |
| Hermes | Follow-up, cron, nudges, escalation | Implementing code, mux UI |
| Cursor | Dev work: branches, PRs, tests, env | Inbox triage, calendars, pane layout |
| Herdr | Terminal multiplexer — agent/CLI panes, sessions, local runtime surface | Classification, cron policy, writing product code |

Herdr is where interactive terminal work lives: Hermes CLI, shell, and other
agent sessions side by side. Cursor stays the IDE and cloud coding surface.
Hermes and agent CLI sessions prefer Herdr panes so progress stays visible.

## Labels (v1)

Use these labels only. Low confidence goes to a human, not to Hermes.

| Label | Meaning | Next owner |
| --- | --- | --- |
| `implement` | Code/docs change needed | Cursor |
| `investigate` | Needs dig, then likely Cursor | Cursor (brief first) |
| `follow_up` | Waiting on human/review/CI | Hermes |
| `decide` | Needs Matthew's judgment | Human |
| `park` | Not active; no chase | None |
| `done` | Closed | None |

## Decision shape

| Field | Value |
| --- | --- |
| `label` | One of the six labels above |
| `confidence` | Number from 0 to 1. Below 0.7, treat as `decide` |
| `next_action` | One sentence |
| `urgency` | `today`, `this_week`, or `whenever` |

No other fields. The next owner comes from the label table, not from a fifth
field.

Emitters write `decide` when confidence is below 0.7, whatever the first
guess was. Consumers do the same: confidence below 0.7 is `decide` even when
`label` says otherwise. The next owner is Matthew. Do not hand that item to
Hermes to chase or to Cursor to build.

`park` and `done` have no next owner. Do not chase a parked item. Do not
reopen a done item by relabeling it in place.

## When to emit

Emit one decision when:

- labeling a ticket, issue, or other incoming item
- choosing a next owner before work starts
- the item changed enough that the previous label is stale

Classification does not start the work. Do not schedule, edit code, or lay
out panes while emitting a decision.

## When to consume

Read the decision, then act only as the layer that owns that label.

- `implement` or `investigate`: Cursor's work. `investigate` gets a brief before implementation. For now a human gates every Cursor spawn. Hermes may draft the brief and nudge Matthew. It does not open Cursor.
- `follow_up`: Hermes owns the nudge while the item waits on a human, review, or CI.
- `decide`, or any confidence below 0.7: stop and ask Matthew.
- `park` or `done`: stop.

A Cursor brief, when one is drafted, names the thread, the desired outcome,
the next action, the constraints, and the links. Unattended Cursor opens are
out of scope for v1. Later, an unattended open is allowed only for
`implement` or `investigate` with confidence of at least 0.7 and a crisp brief.

## Making a repo Jev-ready

The canonical skill stays in this library. A repo points at it.

1. Add a short link in that repo's `AGENTS.md` to `skills/jev/SKILL.md` in this library and say that decisions use this shape.
2. If that repo loads `.cursor/skills/`, add `.cursor/skills/jev/SKILL.md` as a stub that links here, or symlink this skill directory. The stub does not restate the label set.
3. Optionally, in that repo, map its ticket statuses onto these six labels. Keep the map in the repo. Do not add repo statuses to this library.

## Anti-patterns

- Inventing a label (`bug`, `blocked`, `urgent`, `needs-review`, or similar)
- Routing confidence below 0.7 to Hermes or Cursor
- Opening Cursor, scheduling follow-up, or editing product code as part of classification
- Copying this label set into a repo so it can drift
- Adding fields, secrets, hostnames, or machine-local paths to a decision

## TODO

- [ ] Where the consuming repo records a decision (ticket comment, issue body, or a field)
- [ ] That repo's status-to-label map, if it wants one

## Done

The decision has the four fields, a v1 label, and an owner from the table.
Confidence below 0.7 is `decide` for Matthew.

## Report

Label, confidence, next owner, and where the decision was written. Do not
paste secrets or local paths.
