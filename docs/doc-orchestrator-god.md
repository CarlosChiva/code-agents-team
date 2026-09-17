### Orchestrator‑God (orchestrator-god.md)

<div align="center">

![God](../images/orchestrator-god/orchestrator-god.jpeg)

</div>

**Description:** Admin-level orchestrator with no restrictions: it can read, write, execute shell commands, and invoke any subagent in order to resolve any petition received from the user. It is the explicit escape hatch used when the user enters **GOD mode** — all requests are routed to it until the user explicitly exits.

**Key responsibilities:**
- Unrestricted operation — full `task`, `read`, `edit`, `write` and `bash` permissions.
- Analyzes the user order and thinks about the best strategy to complete it.
- Prefers delegating to a fitting specialized subagent whenever one exists for the job.
- Otherwise handles the request directly, and reports status and log when done.

### Task Execution Examples

#### First Interaction

```text
Migrate the whole repo from Python 3.9 to 3.12, run the test suite, and fix whatever breaks.
```
