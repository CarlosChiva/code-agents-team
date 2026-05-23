# 📝 code-agents-team - Agent Configuration

This repository contains the full configuration of a team of specialized agents for the automated management of software‑development projects.

## What is this project?

`code-agents-team` is a collaborative system of autonomous agents designed to manage development projects following a structured workflow within the OpenCode tool. Each agent has a specific role and responsibility, working in sequence to transform user requirements into functional code while maintaining high standards of quality and security.

## 🏢 Agent Team

This system consists of 9 specialized agents:

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

### 7. 🔧 Coder‑fixer
Specific orchestrator agent that receives coding tasks from the user and coordinates their execution using sub-agents: `coder-proposal`, `coder`, `coder-reviewer` and `child-documenter`. It never writes code directly, only delegates and reports.

[Coder-fixer Documentation](docs/doc-coder-fixer.md)

### 8. 📋 Coder‑Proposal – Technical Proposal Generator
Analyzes code modification tasks and generates a detailed technical proposal before any line is written. It searches documentation, reads source files, finds relevant skills, and produces a structured proposal report with proposed changes, implementation order, and risks. Never executes changes, only proposes.

[Coder-Proposal Documentation](docs/doc-coder-proposal.md)

### 9. 📝 Child‑Documenter – Technical Documentation Generator
Specialized agent that reads source code and generates hierarchical technical documentation. Operates in three modes: document-folder (generates `.md` docs replicating repository structure), index-module (adds documentation to index), and close-index (generates quick-reference guide).

[Child-Documenter Documentation](docs/doc-child-documenter.md)

---

## 🚀 Installation

This project provides a ready‑to‑use configuration for the agents. Simply copy the files to the appropriate configuration directory.

### Agents Installation Steps

1. **Copy configuration files:**
   ```bash
   git clone https://github.com/CarlosChiva/code-agents-team.git
   cd code-agents-team/
   ```
2. Ask about which code cli are going to be installed agents, claude code or opencode.
Depends on the code cli where agents are going to be installed, follow the step to install agents in the code cli that user want to install them.

3. **If agents are going installed into claude code:**
   ```bash
   cp -r agents/claude-agents/* ~/.claude/agents/
   ```

4. **If agents are going installed into claude code:**
   ```bash
   cp -r agents/opencode-agents/* ~/.config/opencode/agents/
   ```

> Remember set the model and provider from agents.md before to launch opencode.

### Destination Paths

| Operating System | Destination Path | Type of code cli |
|------------------|-------------------|-------------------|
| Linux/macOS      | `~/.config/opencode/agents/` | Opencode |
| Linux/macOS      | `~/.claude/agents/` | Claude code |

⚠️ **Important:** Don’t forget to edit each file to correctly configure the `provider` and `model` values before using the agents.

---

## 📂 Repository Structure

```
code-agents-team/
├── agents/
│   ├── claude-agents/
│   │   ├── manager.md
│   │   ├── coder.md
│   │   ├── coder-reviewer.md
│   │   ├── coder-proposal.md
│   │   ├── coder-fixer.md
│   │   ├── planner.md
│   │   ├── project-analizer.md
│   │   ├── project-leader.md
│   │   ├── child-documenter.md
│   │   └── documenter.md
│   └── opencode-agents/
│       ├── manager.md
│       ├── coder.md
│       ├── coder-reviewer.md
│       ├── coder-proposal.md
│       ├── coder-fixer.md
│       ├── planner.md
│       ├── project-analizer.md
│       ├── project-leader.md
│       ├── child-documenter.md
│       └── documenter.md
├── images/                    
│   └── ...
├── docs/        
│   └── ...
└── README.md                   
```

## 🔗 Main Workflow using Project-Leader

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
Coder-proposal → Recive task , read all dependecies and files to know about context to make the task and return a proposal report to implement task.
        ↓
Manager → Recive proposal report and send it to coder.
        ↓
Coder (Implementation)
        ↓
Manager →  Send the report and task to coder-reviewer
        ↓
Coder-Reviewer (Verify task completed sucessfully)
        ↓
Manager →  Chose depends on the output of coder-reviewer if task is completed o return the report from coder-reviewer to coder.
        ↓
Manager →  Once coder-reviewer approved task, send report to child-documenter to update documentation file affected by chances made in task implementation.
        ↓
Child-documenter →  Recives report about changes made in code and update or create the documentation into /docs/documentation folder.
        ↓
Manager →  Once documentation is updated, send report to Project leader
        ↓
Project-leader → Show the report of task to user and ask if continue with next task.

```

## 🔗 Workflow using Coder-fixer

```

User ask about changes about code or ask about project 
        ↓
Coder-fixer ← Recives the specifications from user to make a task and send it to coder-proposal
        ↓
Coder-proposal ← Search into repository (or he can to use mcp to search enough context to user task)
        ↓
Coder-fixer ← Recives the report from coder proposal and show it to user to make validate for user. Once is validated by user, the report is sent to coder.
        ↓
coder →  Recive the task from coder-fixer and make the task
        ↓
Coder-fixer →  Chose depends on the output of coder-reviewer if task is completed o return the report from coder-reviewer to coder.
        ↓
Manager →  Once coder-reviewer approved task, send the changes report to child-documenter.
        ↓
child-documenter →  Use the changes report to update current documentation.
        ↓
Manager →  Once coder-reviewer approved task and documentation is updated, return a report to user

```
