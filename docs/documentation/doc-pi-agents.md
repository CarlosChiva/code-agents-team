### Pi‑Agents (agents/pi-agents/)

<div align="center">

</div>

**Description:** Mirror of [`agents/opencode-agents/`](../../agents/opencode-agents/) converted to the **[pi coding agent](https://github.com/badlogic/pi-mono) format**: markdown files with a YAML frontmatter reduced to just `name` (kebab-case), `description` (one sentence), `tools` as a **CSV string** of pi builtin tools (`read`, `write`, `edit`, `bash`, `grep`, `find`, `ls`; special values `*` / `all` = every builtin, `none` = no tools; extension-provided tools selectable via `ext:<extension>/<tool>`), plus `allowed_subagents` — the delegation allowlist in [pi-subagents](https://github.com/tintinweb/pi-subagents) syntax (equivalent of opencode's `permission.task`) — and `color` (quoted hex string, kept verbatim from opencode). The 14 markdown bodies (the system prompts) are **byte-for-byte identical** to the opencode originals — verified 14/14 — only the frontmatter changes.

**Key responsibilities:**
- Provide the same 14-agent team (1 router, 5 orchestrators, 8 subagents) for users of the pi coding agent.
- Preserve every opencode restriction that pi cannot express as **YAML comments** (`# pi:`) inside each frontmatter — path-pattern permissions, bash command filters and `webfetch` notes travel inside the file itself, since files are copied individually on install.
- Discard what has no pi equivalent: `mode` and `model`.

### Target format (opencode → pi mapping)

| Concept in opencode | Equivalent in pi |
|---|---|
| `name`, `description` | Kept literally, unchanged |
| `permission.read/grep/bash/write/edit` | `read` / `grep` / `bash` / `write` / `edit` in the `tools` CSV (1:1, only if they were allowed) |
| `permission.glob` | Renamed to `find` |
| `mode`, `model` | Discarded — no equivalent |
| `color: "#hex"` | `color` kept verbatim (quoted hex supported) |
| `permission.skill` | No portable field — skills are inherited by default in pi (`skills: true`) |
| `permission.task` | `allowed_subagents`: omitted = denied by default-off; `all` = any enabled agent; comma-separated list = only those types. Runtime-enforced, unknown types rejected. Requires the pi-subagents plugin |
| `webfetch` | Not builtin in pi — grant an extension-provided fetch/search tool via the `ext:<extension>/<tool>` selector |
| Path-pattern permissions & bash filters | NOT expressible in pi — recorded as `# pi:` comments |

### Tools assigned per agent

| Agent | `tools` | `allowed_subagents` | Original restriction lost |
|---|---|---|---|
| `project-leader` | `none` | `orchestrator-planner,orchestrator-implementer,orchestrator-qa,orchestrator-god,orchestrator-web-search` | Delegation via `task` to the orchestrators (now via `allowed_subagents`; requires the pi-subagents plugin); loses `mode: primary` |
| `orchestrator-planner` | `read,write,edit,bash` ¹ | `project-structure,task-planner` | Only read `docs/REQUIREMENTS.md`, `docs/PROJECT_STRUCTURE.md`, `docs/FRAMEWORKS.md`, `docs/index-tasks.md` and only wrote `docs/REQUIREMENTS.md`; delegated via `task` to project-structure/task-planner (now via `allowed_subagents`; requires the pi-subagents plugin) |
| `orchestrator-implementer` | `read,write,edit,bash` | `context-searcher,coder-proposal,coder,coder-reviewer,documenter` | Only read `docs/*`, `docs/tasks/*`, `docs/index-tasks.md` and only wrote `docs/index-tasks.md`, `docs/LOGS.md`, `docs/LESSONS_LEARNED.md`; delegated via `task` to the full pipeline (now via `allowed_subagents`; requires the pi-subagents plugin) |
| `orchestrator-qa` | `read` | `context-searcher` | Context gathering was delegated via `task` to context-searcher (now via `allowed_subagents`; requires the pi-subagents plugin) |
| `orchestrator-web-search` | `none` | `web-searcher` | Delegated via `task` to web-searcher (now via `allowed_subagents`; requires the pi-subagents plugin); searches relied on `webfetch` (external extension) |
| `orchestrator-god` | `read,write,edit,bash` ¹ | `all` | Delegating to any subagent (now via `allowed_subagents: all`; requires the pi-subagents plugin); see note ¹ about the reverted `grep/find/ls` |
| `context-searcher` | `read,find,grep,bash` | `explore` | Delegation via `task` to the builtin `explore` subagent (80k-token budget) — now via `allowed_subagents: explore`; skills inherited by default |
| `coder-proposal` | `read,bash` | — ² | No edit/write by design; skills inherited by default |
| `coder` | `read,write,edit,bash,grep,find` | — ² | Denied write/edit on `docs/*` and `docs/tasks/*`; denied `cat *` and `git *` in bash |
| `coder-reviewer` | `read,bash` | — ² | Denied `cat *`, `git commit *` and `git push *` in bash; skills inherited by default |
| `documenter` | `read,write,edit,bash,grep,find` | — ² | Could only write/edit inside `docs/documentation/**` AND `docs/documentation/*` |
| `project-structure` | `read,write,edit,bash` | — ² | Only wrote `docs/PROJECT_STRUCTURE.md` and `docs/FRAMEWORKS.md`; `webfetch` not builtin |
| `task-planner` | `read,write,edit,bash` | — ² | Only wrote `docs/index-tasks.md` and `docs/tasks/**`; skills inherited by default |
| `web-searcher` | `none` | — ² | `webfetch` not builtin — inert until an extension-provided fetch/search tool is granted via the `ext:<extension>/<tool>` selector |

> ¹ For `orchestrator-planner` and `orchestrator-god`, `grep/find/ls` were **reverted**: those tools were never granted in the original opencode agents. `bash` covers search/listing via shell; `tools: *` would instead grant **all** builtins.
>
> ² Field omitted in the frontmatter → denied by default-off (no delegation permitted).

### What was lost in the conversion

The conversion is **lossy** by design: pi supports neither path-pattern permissions nor bash command filters, so all those original restrictions are gone at tool level. Each one is still recorded as a `# pi:` comment in the corresponding frontmatter, but containing the agent becomes the job of its system prompt:

- Path-pattern permissions (e.g. `"docs/*": deny`) and bash filters (`"cat *": deny`, `"git *": deny`, `"git commit *": deny`, `"git push *": deny`) — these remain the **only real losses at tool level**.
- The `task` tool: **no longer lost** — delegation is expressable now via the [pi-subagents](https://github.com/tintinweb/pi-subagents) plugin. Install with `pi install npm:@tintinweb/pi-subagents`; its `Agent` tool replaces opencode's `task`; the per-agent allowlist is declared with `allowed_subagents` (default-off: omitted = denied); nested delegation depth is capped by `maxSubagentDepth` in `subagents.json` (default 2). The prompts already order agents to delegate among themselves, so they work unchanged once the plugin is installed.
- `webfetch`: searches require granting an extension-provided fetch/search tool through the `ext:<extension>/<tool>` selector in the `tools` CSV. Fully affected: `web-searcher` (inert until installed). Partially affected: `orchestrator-web-search` and `project-structure`.
- `mode`, `model`: discarded without replacement.

⚠️ Verified against the official pi-subagents README (**v0.18.x**, requires pi >= 0.84.0): the special `tools` values `none` and `*` / `all`, and the `ext:` selectors are supported, and typos trigger a `tools-error:` warning at load time. For deep chains such as project-leader → orchestrator → subagent, raise `maxSubagentDepth` to >= 3 in `subagents.json` (default 2). No `teams.yaml` is included because pi's teams schema is not confirmed by reliable sources (an orientative commented example lives in the [internal guide](../../agents/pi-agents/README.md)).

### Installation Examples

#### Step 0 — pi-subagents plugin (required for inter-agent delegation)

```bash
pi install npm:@tintinweb/pi-subagents
```

Without this plugin the agents run but cannot delegate: it provides the `Agent` tool (replacement of opencode's `task`) that honors each agent's `allowed_subagents`.

#### Project-level install (recommended)

```bash
cp -r agents/pi-agents/*.md .pi/agents/
```

#### Global install

```bash
cp -r agents/pi-agents/*.md ~/.pi/agent/agents/
```

> Agent discovery order: `.pi/agents/` > `.agents/agents/` > `~/.pi/agent/agents/`.

> Detailed internal guide (mapping, limitations, assumptions): [`agents/pi-agents/README.md`](../../agents/pi-agents/README.md)

## 🔄 Changes in this update

- Description now documents the new frontmatter fields `allowed_subagents` (pi-subagents delegation allowlist) and `color`, plus the special `tools` values `*`/`all`, `none` and the `ext:<extension>/<tool>` selectors; links the [pi-subagents](https://github.com/tintinweb/pi-subagents) plugin.
- Removed `task` delegation from the list of restrictions traveling as `# pi:` comments (delegation is expressible now).
- Discarded fields reduced to `mode` and `model` only (`color` is now preserved).
- Mapping table: split `color` into its own row (kept verbatim), replaced the `permission.task` row with the full `allowed_subagents` semantics (default-off, `all`, CSV, runtime-enforced), rewrote the `webfetch` row around the `ext:` selector, and annotated the skill row with `skills: true`.
- Tools table: added the `allowed_subagents` column for all 14 agents; corrected `orchestrator-god` and `orchestrator-planner` tool reverts (footnote ¹); documented the omission semantics (footnote ²); cited both `docs/documentation/**` AND `docs/documentation/*` for `documenter`; listed the read scope of `orchestrator-implementer`.
- "What was lost": `task` bullet rewritten — delegation IS expressable now via pi-subagents (plugin install command, `Agent` tool, `allowed_subagents` default-off, `maxSubagentDepth` cap); webfetch bullet now mentions the `ext:` selector mechanism.
- ⚠️ paragraph replaced: verification against the official pi-subagents README (v0.18.x, pi >= 0.84.0) covering `none`, `*`/`all`, `ext:` selectors and `tools-error:` warnings; recommendation to raise `maxSubagentDepth` >= 3 for deep chains; teams.yaml note kept.
- Installation Examples: added Step 0 (`pi install npm:@tintinweb/pi-subagents`) required for delegation, and documented the discovery order `.pi/agents/` > `.agents/agents/` > `~/.pi/agent/agents/`.
