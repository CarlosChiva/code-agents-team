### Task‑Planner (task-planner.md)

<div align="center">

</div>

**Description:** Software architect that breaks requirements into an ordered, atomic, dependency-aware task list, materialized as files: one markdown file per atomic task plus an aggregating index. It never writes code — it only produces task files.

**Key responsibilities:**
- Reads `docs/REQUIREMENTS.md`, `docs/PROJECT_STRUCTURE.md` and `docs/FRAMEWORKS.md` before planning.
- Creates one file per atomic task in `docs/tasks/NNN-slug.md` with YAML frontmatter (`id`, `title`, `status` — always starting as `PENDING`, `depends_on`, `involved_files`) plus **Description** and **Acceptance Criteria**.
- Creates/updates `docs/index-tasks.md` as the aggregating index (ID, Title, Status, Depends on, Link).
- On an UPDATE plan, never touches tasks already `DONE` or `IN_PROGRESS` — only adds, modifies or removes `PENDING` tasks while keeping `depends_on` consistent.

### Task Execution Examples

#### First Interaction

```text
Based on docs/REQUIREMENTS.md, docs/PROJECT_STRUCTURE.md and docs/FRAMEWORKS.md,
generate the complete list of atomic tasks for this project.
```
