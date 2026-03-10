# genai-workflow-meta

A cross-project log tracking human–AI collaboration across decision stages.

## Purpose

Documents meaningful stages of working with Claude — what inputs were provided, who drove each decision, and what the outcomes were. Designed for both project documentation (e.g. sharing with a manager) and future meta-analysis of collaboration patterns.

## Contents

| File | Description |
|---|---|
| `WORKFLOW_LOG.md` | Append-only log of decision stages |
| `tool_audit.log` | Auto-generated log of every Claude tool call (local only, gitignored) |

## How it works

- `/log` — a Claude Code skill that reviews the recent conversation, pre-fills a structured entry, and appends it after user confirmation
- A `PostToolUse` hook silently logs every tool call Claude makes to `tool_audit.log`
- System files (skill, hook, settings) are backed up in the [artifacts](https://github.com/shelley-y-he/artifacts) repo

## Log format

Each entry captures: phase, initiator, user engagement, user action type, input modality, prompt summary, AI output summary, decision dependency, outcome, and notes. See the header of `WORKFLOW_LOG.md` for the full field taxonomy.
