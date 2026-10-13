# Agent & Subagent Workflow Architecture

Practical patterns for this Project (Skill/agent optimizations). Stub — grow sections as we learn what actually works.

## Single agent vs coordinator + workers

**Prefer a single agent when:**
- One clear deliverable, one checkout, one sequential chain of edits
- Scope fits in one context window without heavy fan-out
- Latency of coordination would exceed the work itself

**Prefer coordinator + workers when:**
- Independent workstreams can run in parallel (explore vs draft vs verify)
- Different tools/environments are needed (cloud agent, computer-use, local checkout)
- The root must stay responsive while long work runs elsewhere

**Rule of thumb:** If the next step depends on the previous step’s *content*, stay sequential (often single agent). If it depends only on a *path or acceptance criteria*, fan out.

## Parallel vs sequential workstreams

| Pattern | Use when | Risk |
| --- | --- | --- |
| Sequential | Shared files, cumulative edits, “fix then document” | Slow; root blocked if done inline |
| Parallel | Disjoint paths, read-only research + write elsewhere | Merge conflicts; duplicated effort |
| Staged parallel | Explore in parallel → one writer integrates | Coordinator must reconcile |

**Anti-patterns**
- Parallel writers on the same file without ownership
- Parallel “research” that each inlines a novel into chat
- Fan-out without a named owner for merge/completion

## Handoff: paths & artifacts vs inlining

**Hand off paths** for anything longer than a short verdict: docs, reports, diffs, screenshots, media.
**Inline** only: decision, blocker, 2–3 sentence summary, and links/paths.

**Patterns**
- Worker writes to an assigned path → coordinator cites that path, does not paste the body
- Shared store (`docs/`, `internal/`, `media/`) is the contract; chat is the pointer
- Assigned path wins over improvising a new location

**Anti-patterns**
- Pasting full reports into coordinator/root chat
- “Here’s the content…” when a file already exists
- Renaming or relocating deliverables without updating the assignment

## Cloud vs local / shared checkout

| Mode | Good for | Watch for |
| --- | --- | --- |
| Local / shared checkout | Edits in an existing repo the root already owns | Contended branches; accidental scope creep |
| Cloud / isolated agent | Long jobs, separate env, no need for root’s working tree | No repo access unless launched with it; push/PR only if authorized |
| Shared Project store | Cross-agent docs, notes, media, status | Treat as coordination surface, not a git substitute |

**Stub to grow:** when this Project should force “no checkout” workers vs “same worktree” workers.

## Chat vs notes vs docs / context

| Surface | Belongs here |
| --- | --- |
| Chat | Asks, decisions, blockers, short status, links |
| `notes.md` | Coordinator-owned checklist / live status (workers: don’t edit unless assigned) |
| `docs/` | User-facing guidance and deliverables |
| `internal/` | Evidence, audits, working notes, cross-agent context |
| Preferences / memory | Reusable guidance — only when explicitly allowed |

**Anti-pattern:** dumping architecture into chat; dumping ephemeral status into `docs/`.

## Using Context (Project store)

Context = this Project’s shared agent store (e.g. `/cursor/stores/self/` → Project store). Coordinator and workers share it; the user sees `docs/`, `plans/`, `media/` — not private scratch.

**What’s shared**
- Paths under the Project store are the coordination contract across agents
- Chat carries pointers and decisions; durable work lands in store files
- Workers do **not** inherit the store by osmosis — assignments must pass the store root and exact target paths

**Where to write**
- `docs/` — user-facing deliverables and guidance (assigned path wins)
- `internal/` — evidence, audits, working notes (default when no user-facing path is assigned)
- `notes.md` — coordinator status only; workers leave it alone unless explicitly assigned
- `media/` — screenshots, recordings, other binaries cited from docs/chat

**Path handoffs**
- Prefer “wrote `/cursor/stores/self/docs/…`” over pasting the body
- Read assigned paths before asking for content that already lives there
- Don’t invent sibling locations on retry; reuse the same assigned paths

**Anti-patterns**
- Assuming a worker can see Context without an explicit store/path in the assignment
- Writing user-facing material under `internal/`, or dumping ephemeral status into `docs/`
- Editing `notes.md` or preferences/memory without ownership

## Subagents: short-lived tools vs persistent workers

**Short-lived (tool-like)**
- One question, one search, one verify pass
- Return a compact result; no ongoing ownership
- Prefer for explore, lint, “does this path exist?”

**Persistent workers**
- Own a workstream across multiple turns
- Hold checkout or browser state; report milestones + final path
- Need clear completion criteria and a single merge owner (usually coordinator)

**Anti-patterns**
- Spawning persistent workers for a one-shot lookup
- Treating short-lived agents as if they retain memory next turn
- Nested coordinators without a reason

## Failure, retry, and completion reporting

**Minimum completion report:** outcome · path(s) written · blocker (if any) · what was *not* done
**Retries:** same assignment, same paths; don’t invent sibling docs on retry
**Failures:** one short reason + whether retry is safe; no partial “helpful” rewrites of unowned files

**Stub to grow:** standard retry budget and when to escalate to the user vs re-fan-out.

## Keeping the root responsive

- Root/coordinator orchestrates; workers do long I/O and deep edits
- Prefer path handoffs over waiting on large inlined blobs
- Defer slow verify while follow-ups are queued; verify the cumulative result when idle
- Don’t block the root on research that a worker can own

**Anti-pattern:** root does all the work “to save a hop,” then can’t answer the user.

## Quick decision checklist

1. One deliverable, shared files? → single agent or strict sequential ownership
2. Independent paths or envs? → coordinator + parallel workers
3. Result longer than a blurb? → write a file, hand back the path
4. User-facing? → `docs/` (or assigned path). Working evidence? → `internal/`
5. Done? → short report to coordinator; no essay in chat

## Open questions (fill later)

- Default fan-out width for this Project
- When computer-use / video review is worth the hop
- Naming conventions for worker reports under `internal/`
- How aggressively to hill-climb skills vs document patterns here
