### Orchestrator‑Planner (orchestrator-planner.md)

<div align="center">

</div>

**Description:** Orchestrator that turns user requirements into a written, atomic implementation plan. It determines whether the request is a NEW PLAN or an UPDATE PLAN and coordinates the specialized subagents that produce the planning documents. It never writes code and never touches source files — its only writable file is `docs/REQUIREMENTS.md`.

**Key responsibilities:**
- Writes only `docs/REQUIREMENTS.md` (create for a new plan, append/merge for an update — never deletes previous requirements).
- Coordinates `project-structure` first and `task-planner` second — strict order, never reversed; `task-planner` is only called after `project-structure`'s output files exist.
- Determines NEW PLAN vs UPDATE PLAN mode based on the existing state of `docs/`.
- On UPDATE, instructs `task-planner` to preserve tasks already `DONE` or `IN_PROGRESS` and to merge only the `PENDING` ones.

### Task Execution Examples

#### First Interaction

```text
Plan a new feature: add a user login with email + password, persist sessions in a JSON
file, and extend the current plan if it already covers authentication.
```
