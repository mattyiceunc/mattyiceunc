---
name: agent-workflow
description: >-
  Architect single-agent vs coordinator+worker flows for this Project:
  parallel vs sequential work, Context/store path handoffs, docs vs
  internal vs notes, completion reporting, keeping the root responsive.
  Use when planning fan-out, assigning workers, or deciding where work
  should live in the Project store.
---

# Agent workflow (Project)

Practical rules for Skill/agent optimizations. Ground truth (longer stub):
[Agent workflow architecture](references/agent-workflow-architecture.md).
Do not invent a second playbook — extend that doc when patterns change.

## Single agent vs coordinator + workers

- **Single agent:** one deliverable, shared files, sequential edits, fan-out cost > work
- **Coordinator + workers:** independent workstreams, different envs/tools, root must stay responsive
- **Thumb rule:** next step needs prior *content* → sequential; needs only *path/criteria* → fan out

## Parallel vs sequential

- Parallel only on disjoint paths or read-only research + one writer later
- Never parallel-write the same file without a named owner
- Staged parallel: explore many → one integrator merges

## Context (Project store)

Context = shared Project store (often `/cursor/stores/self/`). Coordinator and
workers share it; chat is not durable storage.

- Pass the **store root and exact target paths** in every worker assignment — workers do not discover Context by default
- Hand off **paths**, not bodies; inline only decision / blocker / short summary + links
- `docs/` = user-facing; `internal/` = evidence and working notes; `media/` = binaries
- `notes.md` = coordinator status — workers do not edit unless assigned
- Assigned path wins; retries reuse the same paths (no sibling sprawl)

## Chat vs files

| Put here | What |
| --- | --- |
| Chat | Asks, decisions, blockers, short status, path links |
| `docs/` | User-facing deliverables / guidance |
| `internal/` | Audits, evidence, cross-agent working notes |
| `notes.md` | Live checklist (coordinator-owned) |

## Subagents

- **Short-lived:** one lookup/verify; compact return; no ongoing ownership
- **Persistent:** multi-turn workstream; clear done criteria; one merge owner (usually coordinator)
- Don’t nest coordinators without a reason; don’t treat tool-like agents as sticky memory

## Cloud vs local checkout

- Shared checkout: edits in a tree the root already owns — watch branch contention
- Cloud/isolated: long jobs or separate env — no repo unless launched with it; push/PR only if authorized
- Project store coordinates docs/status; it is not a git substitute

## Failure, retry, completion

Minimum report: **outcome · path(s) written · blocker · what was skipped**
- Retry same assignment and paths; don’t rewrite unowned files “helpfully”
- Escalate when retry isn’t safe; otherwise re-fan-out with the same contracts

## Keep the root responsive

- Root orchestrates; workers own long I/O and deep edits
- Path handoffs over large inlined blobs
- Don’t block the root on research a worker can own

## Quick checklist

1. Shared files / one chain? → single agent or strict sequential ownership
2. Independent paths/envs? → coordinator + parallel workers
3. Longer than a blurb? → write a file, return the path
4. User-facing → `docs/`; evidence → `internal/`
5. Done → short report to coordinator; no essay in chat

## Read next

| Doc | When |
| --- | --- |
| [Architecture](references/agent-workflow-architecture.md) | Full patterns, anti-patterns, and open questions |
| [Worker assignment](examples/worker-assignment.md) | A path handoff and a completion report to adapt |
