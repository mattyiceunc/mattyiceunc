---
name: jev
description: Use when classifying, scoring, or routing a ticket or incoming item as a Jev decision for Hermes, Cursor, or Matthew.
---

# Jev

Jev is the classification, scoring, and routing layer in the stack
Jev → Hermes → Cursor, with Herdr panes for local agent and CLI sessions.
Jev emits a typed decision. It does not schedule, change code, or lay out
panes. Ground truth: [Jev decisions](references/jev-decisions.md). Do not
invent a second playbook — extend that doc when the pattern changes. Do not
invent labels.

## When to emit or consume

Emit a decision when labeling a ticket, issue, or other incoming item, or
when choosing the next owner before work starts. Consume a decision when
acting on an item that already has one: follow its label. Classify again
only when the item itself changed.

## Decision

Four fields only. `label` is one of `implement`, `investigate`, `follow_up`,
`decide`, `park`, `done`. `confidence` is a number from 0 to 1. Below 0.7,
set `label` to `decide` and send it to Matthew, not to Hermes. `next_action`
is one sentence. `urgency` is `today`, `this_week`, or `whenever`.

```json
{
  "label": "implement",
  "confidence": 0.86,
  "next_action": "Add the missing null check and a unit test on the branch.",
  "urgency": "today"
}
```

A score below 0.7 is a human decision even when the first guess was another
label. Consumers apply the same rule if `label` was left unchanged:

```json
{
  "label": "decide",
  "confidence": 0.42,
  "next_action": "Ask Matthew whether this ticket is in scope before anyone schedules it.",
  "urgency": "this_week"
}
```

## Checklist

1. Read the item. Pick one v1 label from the reference. Do not add a label.
2. Score confidence from 0 to 1. Below 0.7, emit `decide` for Matthew.
3. Write `next_action` in one sentence and set `urgency`.
4. Route by that label's owner. Do not open Cursor from classification. For now a human gates every Cursor spawn.

## Making a repo Jev-ready

Point the repo at this skill. Do not copy the label set into the repo.

1. In the repo `AGENTS.md`, link this file and state that decisions use its shape: `skills/jev/SKILL.md` in the personal skills library, https://github.com/mattyiceunc/mattyiceunc/blob/main/skills/jev/SKILL.md.
2. If the repo loads `.cursor/skills/`, add a `jev` stub that links here, or symlink this skill directory. Do not restate labels in the stub.
3. Optionally, in that repo only, map its ticket statuses onto these labels.

Pointer text to adapt: [Decision](examples/decision.md).

## Read next

| Doc | When |
| --- | --- |
| [Jev decisions](references/jev-decisions.md) | Labels, owners, low confidence, and anti-patterns |
| [Decision](examples/decision.md) | A decision and the repo pointer to adapt |
