# GenAI Workflow Log — General Exploration

**Purpose**: Track how I work with Claude across projects — decision stages, inputs, agency, and outcomes — for documentation and meta-analysis of human–AI collaboration.
**Collaborator**: Claude (claude-sonnet-4-6)
**Scope**: Cross-project exploration; not tied to any single project.

## Log Format

Each entry covers one meaningful decision stage (not every conversation turn). Fields are rendered as bullet points.

| Field | Description |
|---|---|
| **Stage ID** | Sequential ID: S01, S02, … |
| **Stage name** | Short descriptive label |
| **Date** | YYYY-MM-DD |
| **Phase** | Planning / Implementation / Debugging / Review / Other |
| **Initiator** | User / Assistant / Joint |
| **User Engagement** | High / Medium / Low |
| **User Action Type** | Problem framing / Constraint setting / Scope rejection / Target definition / Evaluation criteria / Planning & sequencing / Structuring / Approval only / Meta-analysis |
| **Input Modality** | File attachment / URL / Named reference / Search instruction / In-conversation text / In-conversation artifact |
| **Prompt summary** | 1–2 sentences describing what was asked or decided |
| **AI output summary** | What Claude produced or suggested |
| **Decision Dependency** | User-critical / User-influenced / Assistant-driven |
| **Reason for deviation** | *(if User-influenced or User-critical)* Disagreement / Missing context / Ambiguity / Quality / Other |
| **Outcome** | What was actually used and whether it worked |
| **Notes** | Optional retrospective observations |

## Rules

- **Append-only**: no edits to existing entries; add new entries only
- **No speculation about intent**: describe what happened, not why you think it happened
- **Agency must be explicitly classified**: Decision Dependency cannot be left blank

---

## Entries

### S01 — Workflow Logging System Design — 2026-03-08

- **Phase**: Planning
- **Initiator**: User
- **User Engagement**: High
- **User Action Type**: Problem framing, Constraint setting
- **Input Modality**: File attachment, In-conversation text
- **Prompt summary**: User wanted a system to track human–AI interactions across decision stages for documentation and future meta-analysis of collaboration patterns. Shared an Excel-based example from a prior AI exploration for reference.
- **AI output summary**: Proposed a Markdown-based log format with structured fields. Recommended a user-level CLAUDE.md rule + `/log` skill for immediate reusability, with an MCP plugin as the long-term path for team sharing.
- **Decision Dependency**: User-critical
- **Reason for deviation**: N/A
- **Outcome**: Format adopted. `WORKFLOW_LOG.md` created in `genai-workflow-meta/` folder under Colab Notebooks. User-level `CLAUDE.md` rule and PostToolUse hook created. Tracked on GitHub as a private repo (`genai-workflow-meta`).
- **Notes**: Format is provisional — may evolve as we gain experience. Plan to revisit and stabilize before packaging as a plugin. Log is cross-project; project-specific logs may be added later if needed.

### S02 — Log Format Refinement — 2026-03-08

- **Phase**: Review
- **Initiator**: Joint
- **User Engagement**: High
- **User Action Type**: Evaluation criteria, Meta-analysis
- **Input Modality**: File attachment
- **Prompt summary**: User shared a prior Excel-based log schema for comparison. Claude identified gaps in the original format (missing Initiator, User Action Type, Decision Dependency, User Engagement fields; no append-only rule). User approved incorporating improvements.
- **AI output summary**: Updated WORKFLOW_LOG.md format and S01 entry to include new fields; updated CLAUDE.md rule to reference new field taxonomy.
- **Decision Dependency**: User-influenced
- **Reason for deviation**: Quality — prior format lacked the analytical precision needed for attribution analysis.
- **Outcome**: Format updated to v2. All dependencies (WORKFLOW_LOG.md, CLAUDE.md) updated consistently.
- **Notes**: The User Action Type and Decision Dependency fields are the most analytically valuable additions for future meta-analysis.

### S03 — Add Input Modality Field — 2026-03-08

- **Phase**: Review
- **Initiator**: User
- **User Engagement**: High
- **User Action Type**: Evaluation criteria, Structuring
- **Input Modality**: In-conversation text
- **Prompt summary**: User noted that the existing fields don't distinguish how inputs are delivered (e.g., file attachment vs. URL vs. delegated search instruction). Requested a dedicated field to capture this dimension.
- **AI output summary**: Proposed a new Input Modality field with six controlled values: File attachment / URL / Named reference / Search instruction / In-conversation text / In-conversation artifact. Added to format table and CLAUDE.md taxonomy.
- **Decision Dependency**: User-critical
- **Reason for deviation**: N/A
- **Outcome**: Input Modality field added to log format (v3) and CLAUDE.md. All prior entries backfilled where modality was clear.
- **Notes**: This field is orthogonal to User Action Type — together they capture both the purpose and the channel of each input. Enables future analysis of whether input form affects output quality or iteration count.

### S04 — PostToolUse Hook Setup & Validation — 2026-03-08

- **Phase**: Implementation
- **Initiator**: Joint
- **User Engagement**: High
- **User Action Type**: Planning & sequencing
- **Input Modality**: In-conversation text
- **Prompt summary**: User agreed to set up the PostToolUse hook for automated tool call logging. Claude built the hook script and registered it in settings.json; Python turned out not to be installed, requiring user to install it and restart Claude Code.
- **AI output summary**: Created `tool_audit.py` and registered it in `settings.json`. After Python install and restart, hook confirmed working — logging timestamp, session ID, tool name, and input summary to `tool_audit.log`.
- **Decision Dependency**: User-influenced
- **Reason for deviation**: Missing context — Python wasn't installed; required user action before hook could activate.
- **Outcome**: Hook active and confirmed working. `tool_audit.log` generating entries in `genai-workflow-meta/` (gitignored locally).
- **Notes**: Hook captures all tool calls silently from this point forward. No further setup needed.

### S05 — /log UX Design & Project Organisation — 2026-03-08

- **Phase**: Planning
- **Initiator**: User
- **User Engagement**: High
- **User Action Type**: Problem framing, Constraint setting
- **Input Modality**: In-conversation text
- **Prompt summary**: User asked how the /log skill UX would work and how to handle multi-project context, context control, and access control. Clarified preference for sub-folder approach over working from root.
- **AI output summary**: Designed log routing rules (project sub-folder with log → project log; root → global; ambiguous → ask). Recommended separate Claude Code window per project. Proposed `/log new-phase` for explicit phase breaks.
- **Decision Dependency**: User-critical
- **Reason for deviation**: N/A
- **Outcome**: Sub-folder approach adopted. Routing rules defined and later encoded into the /log skill.
- **Notes**: Cross-project or root-level sessions default to global log. Access control handled naturally by per-repo GitHub permissions.

### S06 — /log Skill Implementation — 2026-03-08

- **Phase**: Implementation
- **Initiator**: User
- **User Engagement**: Medium
- **User Action Type**: Approval only
- **Input Modality**: In-conversation text
- **Prompt summary**: User confirmed /log should be a global skill and approved rewriting the existing outdated `log.md` with updated field taxonomy, routing logic, and append-only behaviour.
- **AI output summary**: Rewrote `~/.claude/commands/log.md` with full field taxonomy (including Input Modality), routing logic, confirmation-before-write step, and append-only rule.
- **Decision Dependency**: User-influenced
- **Reason for deviation**: Quality — existing `log.md` referenced old field names and had no routing logic.
- **Outcome**: /log skill updated globally. Confirmed active and tested in this session.
- **Notes**: Skill is global (user-level). Project-level override remains possible if a specific project needs different logging behaviour.

### S07 — Switch Entry Format to Bullet Points — 2026-03-08

- **Phase**: Review
- **Initiator**: User
- **User Engagement**: Medium
- **User Action Type**: Structuring
- **Input Modality**: In-conversation text
- **Prompt summary**: User observed that entries rendered poorly on GitHub (fields running together). Proposed switching from bare bold fields to bullet point format for each field.
- **AI output summary**: Agreed with the approach. Reformatted all existing entries (S01–S06) to bullet point style, updated the format legend, and updated the /log skill to generate bullet point entries going forward.
- **Decision Dependency**: User-critical
- **Reason for deviation**: N/A
- **Outcome**: All entries reformatted. Format and skill updated consistently.
- **Notes**: Bullet points render reliably on GitHub and improve source readability. No functional change to field taxonomy.

### S08 — /log Skill Efficiency & Archive Config — 2026-03-08

- **Phase**: Implementation
- **Initiator**: User
- **User Engagement**: High
- **User Action Type**: Problem framing, Constraint setting
- **Input Modality**: In-conversation text
- **Prompt summary**: User raised concern about performance as the log grows to hundreds/thousands of entries, and asked about trade-offs of reading more vs fewer tail entries. Also specified monthly archive cadence and requested it be configurable.
- **AI output summary**: Explained N=1 (Stage ID only) vs N=3 (context, recommended) vs full-file (wasteful) trade-offs. Proposed a CONFIG block at the top of the skill for `archive_cadence` and `tail_lines`. Implemented tail-read (first 35 lines + last 120 lines) and monthly archive workflow.
- **Decision Dependency**: User-critical
- **Reason for deviation**: N/A
- **Outcome**: /log skill updated with CONFIG block, efficient read logic, and archive trigger. Settings changeable with a one-line edit.
- **Notes**: Sweet spot of 120 tail lines covers ~3 recent entries. Archive creates `WORKFLOW_LOG_YYYY_MM.md` and keeps active file lean.

### S09 — Artifacts Folder & GitHub Tracking — 2026-03-08

- **Phase**: Implementation
- **Initiator**: User
- **User Engagement**: Medium
- **User Action Type**: Structuring
- **Input Modality**: In-conversation text
- **Prompt summary**: User requested an `artifacts/` folder to preserve copies of all system files built today and asked for it tracked on GitHub privately.
- **AI output summary**: Created `artifacts/` under Colab Notebooks with CLAUDE.md, log_skill.md, tool_audit.py, and settings.json. Initialised git repo and pushed to new private GitHub repo.
- **Decision Dependency**: User-critical
- **Reason for deviation**: N/A
- **Outcome**: `artifacts/` folder created with all four system files, tracked at `github.com/shelley-y-he/artifacts` (private).
- **Notes**: Claude flagged that `settings.json` and `tool_audit.py` were also essential to include beyond the .md files the user initially requested.

### S10 — Repo Cleanup & Housekeeping — 2026-03-10

- **Phase**: Implementation
- **Initiator**: User
- **User Engagement**: Medium
- **User Action Type**: Structuring
- **Input Modality**: In-conversation text
- **Prompt summary**: User made three minor housekeeping decisions: changed both repos from private to public for easier sharing; reorganised `artifacts/` into per-project subfolders; added READMEs to both repos.
- **AI output summary**: Changed repo visibility via `gh repo edit` (flagged path disclosure in settings.json first); moved files into `artifacts/genai-workflow-meta/` using `git mv`; wrote and committed READMEs for both repos.
- **Decision Dependency**: User-critical
- **Reason for deviation**: N/A
- **Outcome**: Both repos public, artifacts structure scalable for future projects, READMEs in place.
- **Notes**: `artifacts` README doubles as a setup guide for replicating the workflow logging system on a new machine.
