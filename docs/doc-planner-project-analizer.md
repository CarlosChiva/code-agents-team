## Planner (planner.md) and Project‑Analyzer (project‑analyzer.md)
<div align="center">

![Team Agent Planner](../images/planner_and_project-analizer/planner-project-analizer.png)

</div>

### Project‑Analyzer (project‑analyzer.md)
**Description:** Technical analysis agent that performs a comprehensive evaluation of existing code and the surrounding environment.  

**Main responsibilities:**
- Technical x‑ray of the environment  
- Project structure mapping  
- Detection of technologies and configurations  
- Reads key files to understand data flow  
- Returns findings in a specific schema: Detected Technologies, Architecture, Critical Context, Risks  
- Provides architecture and risk reports  
- Operates in read‑only mode  

#### Agent execution  

##### Repository state analysis  

<div align="center">

![Initial prompt from Manager to Agent](../images/planner_and_project-analizer/initial_prompt.png)
*Using the first prompt received, the agent will search the current repository for its structure; if no code exists, it will create a blueprint of how the repo should be to accommodate all required functionalities.*

</div>

##### Final analysis report  

<div align="center">

![Risk and distribution detected](../images/planner_and_project-analizer/risk_and_distribution_detected.png)
*Risk report identified during feature development*

</div>

<div align="center">

![Critical context](../images/planner_and_project-analizer/critic_context.png)
*Critical context to consider when creating the feature*

</div>

<div align="center">

![Proposed architecture](../images/planner_and_project-analizer/arquitectura-propuesta.png)
*Proposed architecture for the feature*

</div>

<div align="center">

![Technical recommendations](../images/planner_and_project-analizer/tecnic-recomendations-project-analizer.png)
*Technical recommendations for developing the feature*

</div>

---

### Planner (planner.md)
**Description:** Software architect that transforms requirements and analysis into an executable roadmap.  

**Main responsibilities:**
- Break down requirements into atomic tasks  
- Create logically ordered lists  
- Adhere to mandatory table formats  

**Key responsibilities:**
- Decompose requirements into small atomic tasks  
- Generate logically ordered task lists (Setup → Logic → Interface → Testing → Documentation)  
- Assign tasks to appropriate agents  
- Output tasks in a mandatory table format with specific columns  

#### Agent execution  

##### Analysis of the specification fed with data from the Project‑Analyzer  

<div align="center">

![First prompt from Manager](../images/planner_and_project-analizer/first-prompt.png)
*Receives the instruction to generate a plan of atomic tasks based on the requirements and the Project‑Analyzer report*

</div>

<div align="center">

![Table result](../images/planner_and_project-analizer/table_result.png)
*Once verified that the task guidelines are met, it generates a report with the result [Approved / Denied]*

</div>