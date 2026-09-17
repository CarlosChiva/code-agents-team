### Context‑Searcher (context-searcher.md)

<div align="center">

![context-searcher](../images/context-searcher/context-searcher.jpeg)

</div>

**Description:** Generic, reusable subagent that receives a task or question in free text and returns a structured context report — relevant code, documentation, skills, MCPs and past lessons learned — without proposing changes or writing anything. It is used by different orchestrators (implementer, qa) and stays generic about why the context is being requested.

**Key responsibilities:**
- Read-only, always — never writes any file, never proposes changes, never invents context.
- Respects an 80k-token budget: locates candidates cheaply with `glob`/`grep` and delegates actual heavy reading to the `explore` builtin subagent.
- Follows a lookup order: documentation (especially `docs/documentation/index.md`) → source code → skills → MCPs → `docs/LESSONS_LEARNED.md`.
- Returns the same structured 5-section context report (Relevant Code Files, Relevant Documentation, Applicable Skills, Applicable MCPs, Relevant Past Lessons) regardless of caller.

### Task Execution Examples

#### First Interaction

```text
I need to refactor the password-reset flow. Find all the relevant code files, documentation,
skills and past lessons that touch authentication or token handling.
```
