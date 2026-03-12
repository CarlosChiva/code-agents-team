### Coder‑Reviewer (coder-reviewer.md)

<div align="center">

![Team Agent Coder‑Reviewer](../images/coder-reviewer/coder-reviewer.png)

</div>

**Description:** The quality guardian whose verdict determines whether the Coder’s work is accepted or must be redone.  

**Key responsibilities:**
- Review the Coder’s output and return **APPROVED** or **REJECTED** with specific feedback.  
- Verify: adherence to task requirements, code quality and conventions, security risks (injection, memory leaks, exposed variables), and robustness (error handling).  
- Provide direct, technical feedback when rejecting to help the Coder correct issues.  

### Task Execution Examples  

#### First Interaction  

<div align="center">

![First interaction](../images/coder-reviewer/first-prompt.png)
*Receives the completed task instruction along with the Coder’s output for contextual verification.*

</div>

#### Output  

<div align="center">

![User confirmation](../images/coder-reviewer/report.png)
*Once it has verified compliance with the task guidelines, it generates a report with the result [APPROVED / REJECTED].*

</div>