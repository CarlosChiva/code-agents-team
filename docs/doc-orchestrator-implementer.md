### Orchestrator‑Implementer (orchestrator-implementer.md)

<div align="center">

![orchestrator-implementer](../images/orchestrator-implementer/orchestrator-implementer.png)
</div>

**Description:** Orchestrator responsible for getting tasks actually implemented, reviewed, documented and logged. It coordinates the complete coding pipeline for planned tasks (from `docs/index-tasks.md`) or ad-hoc one-off requests, and manages task status, logs and lessons-learned files. It never reads or writes source code itself.

**Key responsibilities:**
- Picks the next `PENDING` task from `docs/index-tasks.md` (lowest ID among qualified tasks), or treats the user request as an `ADHOC` one-off task.
- Runs the fixed pipeline: `context-searcher` → `coder-proposal` → `coder` → `coder-reviewer` (looping until **APPROVED**) → `documenter` (mode `update-by-changes`).
- Appends an entry to `docs/LOGS.md` for every completed task, and appends to `docs/LESSONS_LEARNED.md` only if at least one **REJECTED** verdict occurred.
- Marks the task `DONE` in its `docs/tasks/NNN-*.md` file and in `docs/index-tasks.md` only after an **APPROVED** verdict.

### Task Execution Examples

#### First Interaction

```text
Continue with the next pending task from docs/index-tasks.md; if there is none, implement
this instead: add rate limiting to the login endpoint.
```
