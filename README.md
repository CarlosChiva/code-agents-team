# 📝 code-agents-team - Agent Configuration

This repository contains the full configuration of a team of specialized agents for the automated management of software‑development projects.

## What is this project?

`code-agents-team` is a collaborative system of autonomous agents designed to manage development projects following a structured workflow within the OpenCode tool. Each agent has a specific role and responsibility, working in sequence to transform user requirements into functional code while maintaining high standards of quality and security.

## 🏢 Agent Team

This system consists of 6 specialized agents:

<div align="center">

![Team Agent Configuration](images/team-image.png)

</div>

### 1. 🎯 Manager – Technical Project Manager
The technical lead responsible for coordinating all system operations. It manages the project state via `PROJECT_STATE.md`, delegates tasks to the appropriate agents, and ensures the workflow follows the INIT → PLANNING → EXECUTION cycle.

[Manager Documentation](docs/doc-manager.md)

### 2. ⚡ Coder – Technical Executor
The execution arm that implements assigned tasks by writing or editing code files. It strictly follows existing coding styles, prioritizes corrections from the review agent, and reports all changes in detail.

[Coder Documentation](docs/doc-coder.md)

### 3. 🔍 Coder‑Reviewer – Code Quality Guardian
The final quality filter, reviewing each implementation by the Coder agent to determine if it should be accepted or corrected. It provides specific technical feedback when the code does not meet standards of quality, security, robustness, and coding conventions.

[Coder‑Reviewer Documentation](docs/doc-coder-reviewer.md)

### 4. 📋 Planner – Software Architect
Transforms long, complex user requirements into a list of small, atomic, and logically ordered tasks. It uses structured tabular formats to organize execution from configuration to final documentation.

[Planner Documentation](docs/doc-planner-project-analizer.md#planner-plannermd)

### 5. 🔬 Project‑Analyzer – Technical Environment Analyst
Conducts a complete technical “x‑ray” of the existing environment and project structure. It maps files, detects used technologies, identifies architectures, and returns critical findings that serve as a basis for technical decision‑making.

[Project‑Analyzer Documentation](docs/doc-planner-project-analizer.md#project-analyzer-project-analizermd)

### 6. 👤 Project-Leader – User‑System Interface
The human‑technology bridge that gathers user requirements and manages task‑by‑task confirmations. It acts as an intermediary between user needs and technical execution, controlling workflow through clear confirmations.

[Leader Documentation](docs/doc-leader.md)

---

## 🚀 Installation

This project provides a ready‑to‑use configuration for the agents. Simply copy the files to the appropriate configuration directory.

### Installation Steps

1. **Copy configuration files:**
   ```bash
   git clone https://github.com/CarlosChiva/code-agents-team.git
   cd code-agents-team/
   cp -r agents/* ~/.config/opencode/agents/
   ```

2. **Configure providers and models:**
   Each configuration file must be edited to specify the `provider` and `model` that will be used. The format is as follows:
   ```yaml
   # Example agent configuration
   name:  # model name
   description: # model description
   mode: primary/subagent
   # Provider configuration (TO EDIT)
   model: openai/gpt-4  # Change according to your provider
   temperature: 0.1 # adjust to be more strict or creative as needed
   system_prompt: |
     Your role is to manage the project state...
   ```

### Destination Paths

| Operating System | Destination Path |
|------------------|-------------------|
| Linux/macOS      | `~/.config/opencode/agents/` |

⚠️ **Important:** Don’t forget to edit each file to correctly configure the `provider` and `model` values before using the agents.

---

## 📂 Repository Structure
```
```

```
code-agents-team/
├── agents/                    
│   ├── manager.md
│   ├── coder.md
│   ├── coder-reviewer.md
│   ├── planner.md
│   ├── project-analizer.md
│   └── project-leader.md
├── images/                    
│   └── ...
├── docs/        
│   └── ...
└── README.md                   
```

## 🔗 Workflow

This system works based 2 stages:

```
# First interaction with team

User Requirements
        ↓
Project-leader (Interfaz) ← Collect user requirements
        ↓
Manager → Project-analizer (First analisys from repo)
        ↓
Manager → Planner (Planning TODO List) 
        ↓
Project-leader (Interfaz) ← Project_State created. Waiting user confirmation to start.


# Once Project_State is created.

User Confirmation
        ↓
Project-leader (Interfaz) ← ask yo user for continue the tasks.
        ↓
Manager → read project state to send to coder the first pending task.
        ↓
Coder (Implementation)
        ↓
Manager →  Send the report and task to coder-reviewer
        ↓
Coder-Reviewer (Verify task completed sucessfully)
        ↓
Manager →  Chose depends on the output of coder-reviewer if task is completed o return the report from coder-reviewer to coder.
        ↓
Manager →  Once coder-reviewer approved task, send report to Project leader
        ↓
Project-leader → Show the report of task to user and ask if continue with next task.

```

