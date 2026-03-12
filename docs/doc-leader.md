### Leader (leader.md)

<div align="center">

![Team Agent Leader](../images/leader/leader.png)

</div>

**Description:** Front‑end interface agent that acts as a bridge between the user and the technical team. It manages the task‑by‑task confirmation loop.

**Main responsibilities:**
- Gather user requirements  
- Act as an intermediary—no technical decision making  
- Handle task‑by‑task confirmations  
- Connect with the Manager agent  
- Forward completed task reports  
- Await user confirmation before proceeding to the next task  
- Maintain a clear communication protocol  
- Does not implement code

### Interaction Examples with the User

<div align="center">

![Interaction with Agent Leader](../images/leader/requirements-leader.png)
*After extracting the requirements to implement, it returns a summary of the requirements confirmed with the user for modification or approval.*

</div>

<div align="center">

![Interaction Agent Leader to Manager](../images/leader/leader-calling-to-manager.png)
*Once the requirements are approved, it calls the Manager to start the work.*

</div>

<div align="center">

![Interaction Agent Leader to Manager](../images/leader/report-planing-step-finished.png)
*When the Manager reports the completed task, the Leader presents it to the user and requests confirmation.*

</div>