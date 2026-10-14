# Decision stub

Replace every TODO. The four fields and the label set are fixed; do not add
either. Canonical skill:
https://github.com/mattyiceunc/mattyiceunc/blob/main/skills/jev/SKILL.md

## Decision

Confidence at or above 0.7 keeps the chosen label:

```json
{
  "label": "follow_up",
  "confidence": 0.91,
  "next_action": "Nudge the reviewer; the pull request is waiting on review.",
  "urgency": "today"
}
```

Confidence below 0.7 is `decide` for Matthew, not a task for Hermes:

```json
{
  "label": "decide",
  "confidence": 0.42,
  "next_action": "Ask Matthew whether TODO_ITEM is in scope before anyone schedules it.",
  "urgency": "this_week"
}
```

## AGENTS.md pointer

```markdown
## Jev

Classify, score, and route with the personal skills library skill `jev`:
https://github.com/mattyiceunc/mattyiceunc/blob/main/skills/jev/SKILL.md

Use that label set and decision shape. Do not copy them into this repo.
Confidence below 0.7 is `decide` and goes to Matthew.
```

## .cursor/skills stub

Use this only when the repo loads `.cursor/skills/` and does not symlink the
library skill. Save as `.cursor/skills/jev/SKILL.md`.

```markdown
---
name: jev
description: Use when classifying, scoring, or routing a ticket or incoming item as a Jev decision for Hermes, Cursor, or Matthew.
---

# Jev

Canonical skill:
https://github.com/mattyiceunc/mattyiceunc/blob/main/skills/jev/SKILL.md

Read that file before emitting or consuming a decision. Do not restate its
labels here. Confidence below 0.7 is `decide` and goes to Matthew.
```

## Optional status map

Lives in the consuming repo, not in this library. Map only onto the v1 labels.

| Repo status | Jev label |
| --- | --- |
| TODO_STATUS | `implement` |
| TODO_STATUS | `investigate` |
| TODO_STATUS | `follow_up` |
| TODO_STATUS | `decide` |
| TODO_STATUS | `park` |
| TODO_STATUS | `done` |
