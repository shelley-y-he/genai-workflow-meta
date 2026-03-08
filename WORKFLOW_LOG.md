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
| **Input type** | User requirement / Artifact provided / Search request / Question / Feedback |
| **Prompt summary** | 1–2 sentences describing what was asked |
| **AI output summary** | What Claude produced or suggested |
| **Agency** | Accepted / Lightly edited / Substantially revised / Rejected / Iterated (N rounds) |
| **Reason for deviation** | *(if not Accepted)* Disagreement / Missing context / Ambiguity / Quality / Other |
| **Outcome** | What was actually used and whether it worked |
| **Notes** | Optional retrospective observations |

---

## Entries

### S01 — Workflow Logging System Design — 2026-03-08

**Phase**: Planning
**Input type**: User requirement
**Prompt summary**: User wanted a system to track human–AI interactions across decision stages for documentation and future meta-analysis of collaboration patterns. Shared an Excel-based example from a prior AI exploration for reference.
**AI output summary**: Proposed a Markdown-based log format with structured fields (stage, input type, prompt summary, AI output, agency, deviation reason, outcome, notes). Recommended a user-level CLAUDE.md rule + `/log` skill for immediate reusability, with an MCP plugin as the long-term path for team sharing.
**Agency**: Accepted
**Reason for deviation**: N/A
**Outcome**: Format adopted. `WORKFLOW_LOG.md` created in `genai-workflow-meta/` folder under Colab Notebooks. User-level `CLAUDE.md` rule and `/log` skill created. To be tracked on GitHub as a private repo (`genai-workflow-meta`).
**Notes**: Format is provisional — may evolve as we gain experience. Plan to revisit and stabilize before packaging as a plugin. Log is cross-project; project-specific logs may be added later if needed.
