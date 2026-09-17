### Orchestrator‑QA (orchestrator-qa.md)

<div align="center">

</div>

**Description:** Read-only orchestrator whose only purpose is answering the user's questions about the existing codebase — architecture, where something lives, how something works. It never modifies any file, anywhere, under any circumstance, and it never answers by looking at code itself.

**Key responsibilities:**
- Read-only by design — delegates all context gathering to `context-searcher` and never reads source code directly.
- Documentation-first: asks `context-searcher` to check `docs/documentation/index.md` before falling back to source files.
- Flags stale documentation (docs that contradict the actual code) in its answer, but never attempts to fix it.
- Says clearly when the question cannot be answered with the available information, instead of guessing.

### Task Execution Examples

#### First Interaction

```text
Which files implement the session-expiration logic, and what happens to a stored session
when it expires?
```
