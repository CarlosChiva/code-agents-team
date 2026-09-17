### Coder‑Proposal (coder-proposal.md)

<div align="center">

![Coder proposal](../images/coder-proposal/coder-proposal.png)

</div>

**Description:** Specialized agent that receives a code modification task and generates a **detailed technical proposal** before any line is written. Its value lies in precise prior analysis and clear reporting. It does not execute changes: it proposes, explains, and locates.

**Key responsibilities:**
- Receive the task along with the pre-resolved context report produced by `context-searcher`, and analyze the relevant documentation and source files it points to.
- Search available skills for applicable patterns, conventions, and best practices.
- Produce a structured proposal report with: task summary, analyzed context, applied skills/patterns, proposed changes per file (with exact location), implementation order, and risks/considerations.
- Never execute changes — only propose and document what should be done.
