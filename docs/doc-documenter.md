### Documenter (documenter.md)

<div align="center">

![Documenter](../images/documenter/documenter.png)

</div>

**Description:** Subagent specialized in reading source code and generating hierarchical technical documentation under `docs/documentation/`, replicating the repository's folder structure so an AI agent can find what it needs by reading the minimum necessary documentation. It is invoked by `orchestrator-implementer` after each approved task and writes ONLY inside `docs/documentation/`.

**Key responsibilities:**
- **Mode 1 — `document-folder`:** document a leaf or composite folder into its equivalent `.md` path inside `docs/documentation/` (imports, classes, methods, functions, dependencies).
- **Mode 2 — `index-module`:** add exactly one row to the "🗺️ Module Map" section of `docs/documentation/index.md` — only first-level folders touch `index.md`; anything deeper is skipped.
- **Mode 3 — `close-index`:** read the complete index and generate the "📋 Quick usage guide for agents" section so LLM agents can navigate without reading full docs.
- **Mode 4 — `update-by-changes`:** receive the coder's list of modified files, update or create the affected `.md` files, and re-index only the first-level folders actually touched.

**Rules:**
- Never delete existing documentation — if the `.md` already existed, append a `## 🔄 Changes in this update` section at the end instead.
- Never invent functionality — when a function or file purpose is unclear, use the placeholder `*Purpose undetermined — requires manual review.*`.

### Task Execution Examples

#### First Interaction

```text
mode: update-by-changes
modified_files:
  - src/auth/session.py
  - src/auth/password.py
```
