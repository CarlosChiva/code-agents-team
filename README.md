# 📝 code-agents-team - Agent Configuration

This repository contains the full configuration of a team of specialized agents for the automated management of software‑development projects.

## What is this project?

`code-agents-team` is a collaborative system of autonomous agents designed to manage development projects following a structured workflow within the OpenCode and claude code  tool. Each agent has a specific role and responsibility, working in sequence to transform user requirements into functional code while maintaining high standards of quality and security.

The team lives in `agents/opencode-agents/` for Opencode utilization and is mirrored in `agents/claude-agents/` for Claude Code use.

## 🏢 Agent Team

This system consists of 14 specialized agents — 1 in the router, 5 orchestrators and 8 subagents.

<div align="center">

![Team Agent Configuration](images/team-image.png)

</div>

### Router

### 1. 🧑‍💼 Project-Leader — User-System Router
Pure-messenger router and the only point of contact with the user. It makes no technical decisions, never reads or writes code, and only identifies the user's intent to delegate to the corresponding orchestrator.

[Full Documentation](docs/doc-project-leader.md)

### Orchestrators

### 2. 📐 Orchestrator-Planner — Planning Orchestrator
Turns user requirements into a written, atomic implementation plan. It determines NEW PLAN vs UPDATE PLAN mode, delegates to `project-structure` then `task-planner` (strict order), and never writes code — its only writable file is `docs/REQUIREMENTS.md`.

[Full Documentation](docs/doc-orchestrator-planner.md)

### 3. ⚙️ Orchestrator-Implementer — Implementation Orchestrator
Coordinates the complete pipeline to actually implement a task: `context-searcher` → `coder-proposal` → `coder` ⇄ `coder-reviewer` (loop until APPROVED) → `documenter`. It manages task status in `docs/index-tasks.md`, `docs/LOGS.md` and `docs/LESSONS_LEARNED.md` without ever touching source code. Also it can to implement a little implementation ad-hoc if user ask for him following the all him subagents pipeline.

[Full Documentation](docs/doc-orchestrator-implementer.md)

### 4. 🔍 Orchestrator-QA — Read-Only Q&A Orchestrator
Answers the user's questions about the existing codebase (architecture, "where does X live?", "how does Y work?") in a strictly read-only capacity. All context gathering is delegated to `context-searcher`; nothing is ever modified.

[Full Documentation](docs/doc-orchestrator-qa.md)

### 5. 🌐 Orchestrator-Web-Search — Internet Search Orchestrator
Resolves information requests that require searching the internet. Requires the user to name the tool to use (or it stops and asks), delegates at most 4 atomic searches to `web-searcher`, and consolidates the findings into a final cited report.

[Full Documentation](docs/doc-orchestrator-web-search.md)

### 6. 👑 Orchestrator-God — Unrestricted Orchestrator
Explicit escape hatch with no restrictions (full read/write/bash/task permissions). Prefers delegating to a fitting specialized subagent when one exists, otherwise handles the request directly. Invoked exclusively when the user enters GOD mode.

[Full Documentation](docs/doc-orchestrator-god.md)

### Subagents

### 7. 📚 Context-Searcher — Context Gathering Subagent
Generic, reusable read-only subagent that receives a task or question and returns a structured 5-section context report (relevant code, documentation, skills, MCPs, past lessons). Stays within an 80k-token budget by delegating heavy reading to the `explore` subagent builtin. It never writes anything.

[Full Documentation](docs/doc-context-searcher.md)

### 8. 📋 Coder-Proposal — Technical Proposal Generator
Analyzes a code modification task and generates a detailed technical proposal before any line is written — proposed changes per file, implementation order, and risks. Never executes changes, only proposes.

[Full Documentation](docs/doc-coder-proposal.md)

### 9. ⚡ Coder — Technical Executor
The execution arm that implements the assigned task by writing or editing code files while adhering to the existing coding style. Prioritizes corrections from the Coder-Reviewer when provided, and reports the changes made upon completion.

[Full Documentation](docs/doc-coder.md)

### 10. 🛡️ Coder-Reviewer — Code Quality Guardian
The quality gate that reviews every implementation and returns **APPROVED** or **REJECTED** with specific, technical feedback. Verifies adherence to requirements, code quality, security risks and robustness.

[Full Documentation](docs/doc-coder-reviewer.md)

### 11. 📝 Documenter — Technical Documentation Generator
Invoked by `orchestrator-implementer` after each approved task. Writes ONLY inside `docs/documentation/`, maintaining a hierarchical, indexed documentation tree that mirrors the repository structure. Operates in 4 modes: `document-folder`, `index-module`, `close-index` and `update-by-changes`. Never deletes existing docs.

[Full Documentation](docs/doc-documenter.md)

### 12. 🏗️ Project-Structure — Architecture Researcher
Determines the target repo structure and technology stack from `docs/REQUIREMENTS.md`, mapping the current structure if code exists or recommending one if not. Writes only `docs/PROJECT_STRUCTURE.md` and `docs/FRAMEWORKS.md`; never plans tasks.

[Full Documentation](docs/doc-project-structure.md)

### 13. 🧩 Task-Planner — Task Architect
Breaks the requirements into an ordered, atomic, dependency-aware task list, materialized as one file per task in `docs/tasks/NNN-slug.md` (YAML frontmatter + description + acceptance criteria) plus an aggregating index in `docs/index-tasks.md`. Every new task starts as `PENDING`.

[Full Documentation](docs/doc-task-planner.md)

### 14. 🌐 Web-Searcher — Atomic Web Search Subagent
Minimal, single-purpose subagent: exactly one search per call, using ONLY the tool named in its input (explicit anti-fallback), and returning only the 3 most relevant results with brief paraphrased summaries. If the named tool is unavailable it stops and reports — it never substitutes another.

[Full Documentation](docs/doc-web-searcher.md)

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

5. **If agents are going installed into pi:**
   ```bash
   cp -r agents/pi-agents/*.md .pi/agents/
   ```
   Project-level install shown; for a global install use `cp -r agents/pi-agents/*.md ~/.pi/agent/agents/`.

> Requires the delegation plugin for inter-agent delegation: `pi install npm:@tintinweb/pi-subagents`

> Remember set the model and provider from agents.md before to launch opencode.

### Destination Paths

| Operating System | Destination Path | Type of code cli |
|------------------|-------------------|-------------------|
| Linux/macOS      | `~/.config/opencode/agents/` | Opencode |
| Linux/macOS      | `~/.claude/agents/` | Claude code |
| Linux/macOS      | `.pi/agents/` (project) or `~/.pi/agent/agents/` (global) | Pi |

⚠️ **Important:** Don’t forget to edit each file to correctly configure the `provider` and `model` values before using the agents.

---

## 📂 Repository Structure

```
code-agents-team/
├── agents/
│   ├── opencode-agents/                  # 14 agents — canonical (opencode)
│   │   ├── project-leader.md
│   │   ├── orchestrator-planner.md
│   │   ├── orchestrator-implementer.md
│   │   ├── orchestrator-qa.md
│   │   ├── orchestrator-web-search.md
│   │   ├── orchestrator-god.md
│   │   ├── context-searcher.md
│   │   ├── project-structure.md
│   │   ├── task-planner.md
│   │   ├── web-searcher.md
│   │   ├── coder.md
│   │   ├── coder-proposal.md
│   │   ├── coder-reviewer.md
│   │   └── documenter.md
│   ├── claude-agents/                    
│       ├── project-leader.md             
│       ├── orchestrator-planner.md       
│       ├── orchestrator-implementer.md   
│       ├── orchestrator-qa.md            
│       ├── orchestrator-web-search.md    
│       ├── orchestrator-god.md           
│       ├── context-searcher.md           
│       ├── project-structure.md          
│       ├── task-planner.md               
│       ├── web-searcher.md               
│       ├── coder.md                      
│       ├── coder-proposal.md             
│       ├── coder-reviewer.md                 
│       └── documenter.md                  
│   └── pi-agents/                        # mirror for pi coding agent
│       ├── project-leader.md
│       ├── orchestrator-planner.md
│       ├── orchestrator-implementer.md
│       ├── orchestrator-qa.md
│       ├── orchestrator-web-search.md
│       ├── orchestrator-god.md
│       ├── context-searcher.md
│       ├── project-structure.md
│       ├── task-planner.md
│       ├── web-searcher.md
│       ├── coder.md
│       ├── coder-proposal.md
│       ├── coder-reviewer.md
│       └── documenter.md
├── docs/
│   └── doc-*.md                          # one doc-*.md per agent (14 files)
├── images/                               # screenshots folder
└── README.md
```

## 🔗 Main Workflow using Project-Leader

The user only ever talks to **Project-Leader** (the router), which delegates to the single orchestrator that fits the request:

```
                              USER
                               ↓
                  PROJECT-LEADER (pure router)
    ┌───────────┬──────────────┼──────────────┬─────────────┐
    ↓           ↓              ↓              ↓             ↓
PLANNER     IMPLEMENTER          QA      WEB-SEARCH          GOD
    ↓             ↓              ↓           ↓               ↓
PROJECT-     CONTEXT-SEARCHER            WEB-SEARCHER    (delegates to a fitting
STRUCTURE         ↓                          (max 4        subagent when one
    ↓         CODER-PROPOSAL               atomic          exists, otherwise
TASK-PLANNER        ↓                      calls)          handles the order
    ↓             CODER                    ↓               directly, with full
    ↓         ┌──→ CODER-REVIEWER         REPORT            read/write/bash/task)
(docs)        │  (REJECTED → CODER        ↑
 ↓            │   again with feedback)      ↑
 ↓            └──→ DOCUMENTER               ↑
 ↓                 (update-by-changes)      │
 ↓                      ↑                   │
 ↓                     CODER                │
 ↓                  (approved work)         │
 ↓                                          │
    └──── LOGS.md + LESSONS_LEARNED.md (when ≥1 REJECTED)
```

- **PLANNER** branch writes: `docs/REQUIREMENTS.md` (`orchestrator-planner`), `docs/PROJECT_STRUCTURE.md` + `docs/FRAMEWORKS.md` (`project-structure`), `docs/tasks/NNN-*.md` + `docs/index-tasks.md` (`task-planner`).
- **IMPLEMENTER** branch runs: `context-searcher` → `coder-proposal` → `coder` ⇄ `coder-reviewer` (REJECTED → loop back to `coder`) → on **APPROVED** → `documenter` (`update-by-changes`), plus `docs/LOGS.md` (always) and `docs/LESSONS_LEARNED.md` (only if ≥ 1 REJECTED occurred).
- **QA** branch delegates to `context-searcher` only — read-only, nothing is written.
- **WEB-SEARCH** branch delegates to `web-searcher` up to 4 times, then consolidates a report.
- **GOD** branch has full permissions and uses any subagent or handles the request directly.
