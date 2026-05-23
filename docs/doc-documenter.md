### Documenter (documenter.md)

<div align="center">

</div>

**Description:** Orchestrator agent specialized in code documentation. Coordinates complete repository documentation by delegating work to Child-Documenters, following a **bottom-up strategy**: leaf folders first, then ascending level by level.

**Key responsibilities:**
- **Step 1 — Full tree scan:** Scan the complete repository tree, ignoring `node_modules`, `.git`, `__pycache__`, `dist`, `build`, and other hidden directories. Classify folders as leaf or composite and build the processing order (deepest to shallowest).
- **Step 2 — Delegation (bottom-up):** Invoke Child-Documenters sequentially in bottom-up order for each folder, passing folder path, type, and repository root.
- **Step 3 — Index construction:** Initialize `docs/documentation/index.md` and launch Child-Documenters to index each generated `.md` file into the index.
- **Step 4 — Index closure:** Launch final Child-Documenter to generate the quick-reference guide in the index.
- **Step 5 — Final summary:** Display documented folder tree, failed or empty folders, and index generation confirmation.
