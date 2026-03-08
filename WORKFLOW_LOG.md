# GenAI Workflow Log — General Exploration

**Purpose**: Track how I work with Claude across projects — decision stages, inputs, agency, and outcomes — for documentation and meta-analysis of human–AI collaboration.
**Collaborator**: Claude (claude-sonnet-4-6)
**Scope**: Cross-project exploration; not tied to any single project.

## Log Format

Each entry covers one meaningful decision stage (not every conversation turn).

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

**Phase**: Planning
**Initiator**: User
**User Engagement**: High
**User Action Type**: Problem framing, Constraint setting
**Prompt summary**: User wanted a system to track human–AI interactions across decision stages for documentation and future meta-analysis of collaboration patterns. Shared an Excel-based example from a prior AI exploration for reference.
**AI output summary**: Proposed a Markdown-based log format with structured fields. Recommended a user-level CLAUDE.md rule + `/log` skill for immediate reusability, with an MCP plugin as the long-term path for team sharing.
**Decision Dependency**: User-critical
**Reason for deviation**: N/A
**Outcome**: Format adopted. `WORKFLOW_LOG.md` created in `genai-workflow-meta/` folder under Colab Notebooks. User-level `CLAUDE.md` rule and PostToolUse hook created. Tracked on GitHub as a private repo (`genai-workflow-meta`).
**Notes**: Format is provisional — may evolve as we gain experience. Plan to revisit and stabilize before packaging as a plugin. Log is cross-project; project-specific logs may be added later if needed.

### S02 — Log Format Refinement — 2026-03-08

**Phase**: Review
**Initiator**: Joint
**User Engagement**: High
**User Action Type**: Evaluation criteria, Meta-analysis
**Prompt summary**: User shared a prior Excel-based log schema for comparison. Claude identified gaps in the original format (missing Initiator, User Action Type, Decision Dependency, User Engagement fields; no append-only rule). User approved incorporating improvements.
**AI output summary**: Updated WORKFLOW_LOG.md format and S01 entry to include new fields; updated CLAUDE.md rule to reference new field taxonomy.
**Decision Dependency**: User-influenced
**Reason for deviation**: Quality — prior format lacked the analytical precision needed for attribution analysis.
**Outcome**: Format updated to v2. All dependencies (WORKFLOW_LOG.md, CLAUDE.md) updated consistently.
**Notes**: The User Action Type and Decision Dependency fields are the most analytically valuable additions for future meta-analysis.

### S03 — Add Input Modality Field — 2026-03-08

**Phase**: Review
**Initiator**: User
**User Engagement**: High
**User Action Type**: Evaluation criteria, Structuring
**Input Modality**: In-conversation text
**Prompt summary**: User noted that the existing fields don't distinguish how inputs are delivered (e.g., file attachment vs. URL vs. delegated search instruction). Requested a dedicated field to capture this dimension.
**AI output summary**: Proposed a new Input Modality field with six controlled values: File attachment / URL / Named reference / Search instruction / In-conversation text / In-conversation artifact. Added to format table and CLAUDE.md taxonomy.
**Decision Dependency**: User-critical
**Reason for deviation**: N/A
**Outcome**: Input Modality field added to log format (v3) and CLAUDE.md. All prior entries backfilled where modality was clear.
**Notes**: This field is orthogonal to User Action Type — together they capture both the purpose and the channel of each input. Enables future analysis of whether input form affects output quality or iteration count.
