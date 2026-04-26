### Coder‑fixer (coder-reviewer.md)

<div align="center">

</div>

**Description:** Simple orquestator agent to do simple tasks recived by user. He collect all necesary information about the task searching context into repository then he delegate the task to coder and coder-reviewer to check the task is completed sucessfully 

**Key responsibilities:**
- Based on the task recived. He search the context necesary to understand the task and what changes should be done or what functionalities should be implemented.
- Delegate to coder subagent to execute the task with all context necesary.  
- Pass the coder report to coder-reviewer to verify the task is completed.
