### Manager (manager.md)

<div align="center">

![Team Agent Manager](../images/manager/manager.png)

</div>

**Description:** Technical leader who manages the project state and delegates tasks.  

**Main responsibilities:**
- Manage `PROJECT_STATE.md` as the single database containing user requirements, project architecture, and tasks required to implement those requirements.  
- Coordinate calls to the various sub‑agents to plan tasks, inspect the project structure, schedule work, and verify completed tasks.  
- Ensure a strict sequential workflow.  
- Maintain task status (PENDING → DONE).  
- Return a report of the completed task to the user.  

### Task Execution Examples  

#### First Interaction  

<div align="center">

![First interaction](../images/manager/first-step-manager.png)
*During the first interaction the manager will always look for the `PROJECT_STATE.md` file and create it if it does not exist.*

</div>

##### Structure of the `PROJECT_STATE.md` file  

<div align="center">

![First interaction](../images/manager/structure-project_status1.png)
*The file begins by describing the user requirements.*

</div>

<div align="center">

![First interaction](../images/manager/structure-project_status2.png)
*It continues with an analysis of the current project—or the one to be created—based on those requirements.*

</div>

<div align="center">

![First interaction](../images/manager/structure-project_status3.png)
*A generic current state is generated, and a to‑do list with atomic tasks is created to fulfill the user requirements.*

</div>

##### Execution Flow  

<div align="center">

![First task](../images/manager/first_step_tasks.png)
*Upon its first execution, once `PROJECT_STATE` is visible to identify the task to start, it requests user confirmation.*

</div>

<div align="center">

![User confirmation](../images/manager/recibing_user_confirmation.png)
*After receiving confirmation, it calls the Coder agent to begin the task.*

</div>

<div align="center">

![User confirmation](../images/manager/pass_result_coder_to_reviewer.png)
*Once the Coder agent completes the task, the result is passed to the Reviewer agent for validation.*

</div>

<div align="center">

![User confirmation](../images/manager/final_report.png)
*After the Reviewer confirms acceptance, the manager returns a final report to the user.*

</div>