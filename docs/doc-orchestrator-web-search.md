### Orchestrator‑Web‑Search (orchestrator-web-search.md)

<div align="center">

</div>

**Description:** Orchestrator that resolves information requests requiring the internet. It never searches by itself — it crafts focused queries, delegates them one at a time to `web-searcher`, judges whether the accumulated evidence is sufficient, and consolidates everything into a final report. It never touches any project file.

**Key responsibilities:**
- **Step 0 — mandatory input check:** verifies the user named a specific tool; otherwise stops and reports **MISSING INPUT** instead of guessing.
- Confirms the named tool is actually one `web-searcher` is allowed to use; otherwise reports **TOOL NOT AVAILABLE** with the real list of permitted tools.
- Delegates at most **4 searches** per request to `web-searcher`, each with exactly one query and the exact confirmed tool.
- Consolidates all gathered results into a single final report, in its own words, citing the source of each claim and flagging remaining gaps.

### Task Execution Examples

#### First Interaction

```text
Find the current best practices for configuring CORS in FastAPI, using the websearch tool.
```
