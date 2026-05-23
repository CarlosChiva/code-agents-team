### Child‑Documenter (child-documenter.md)

<div align="center">

</div>

**Description:** Specialized agent that reads source code and generates hierarchical technical documentation. Operates in three modes directed by the Documenter (main orchestrator): document-folder, index-module, and close-index.

**Key responsibilities:**
- **Mode 1 — document-folder:** Read files in a given folder (leaf or composite) and generate `.md` documentation in `docs/documentation/` replicating the repository structure. Extracts imports, classes, functions, and descriptions.
- **Mode 2 — index-module:** Add generated module documentation to `docs/documentation/index.md` with module map, available classes, and available functions.
- **Mode 3 — close-index:** Read the complete index and generate a quick-reference guide for LLM agents to navigate the codebase without reading full documentation.
