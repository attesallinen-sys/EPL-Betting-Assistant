# EPL Betting Assistant

## Overview

This project runs a two-agent workflow for EPL matchweek reporting:

1. Agent 1 collects objective matchweek data.
2. Agent 2 gathers source predictions and writes the report.
3. Accuracy review updates weights after results are final.

`AGENTS.md` is the orchestration entrypoint. Detailed execution lives in task files and source/rule docs listed below.

---

## Run Prompts

### Agent 1: Data Collection

Prompt:

> Fetch data for Gameweek XX (YYYY-MM-DD)

Output: `data/GWxx-matchweek-data.md`

Checklist: `tasks/fetch-matchweek-data.md`

### Agent 2: Predictions and Report

Prompt:

> Generate predictions for Gameweek XX (YYYY-MM-DD)

Prerequisite: Agent 1 output exists.

Output: `reports/GWxx-YYYY-MM-DD-predictions.md`

Checklist: `tasks/matchweek-predictions.md`

### Accuracy Review

Prompt:

> Update accuracy for Gameweek XX

Primary outputs:
- `reports/accuracy-log.md`
- `reports/index.md` (accuracy column update)

Checklist: Phase 6 in `tasks/matchweek-predictions.md`

---

## Typical Weekly Workflow

1. Thursday/Friday: Run Agent 1.
2. Friday/Saturday: Run Agent 2.
3. Monday/Tuesday: Run Accuracy Review.

---

## Canonical Ownership Map

| Artifact | Canonical purpose | Updated by |
|----------|-------------------|------------|
| `AGENTS.md` | Workflow orchestration and prompts | Maintainer |
| `README.md` | Quick start and repo orientation | Maintainer |
| `tasks/fetch-matchweek-data.md` | Agent 1 execution checklist | Agent 1 process |
| `tasks/matchweek-predictions.md` | Agent 2 + accuracy execution checklist | Agent 2/Accuracy process |
| `knowledge/sources.md` | Source URLs, fetch order, fallback queries, reliability policy | Source maintenance |
| `.cursor/rules/research-workflow.mdc` | High-level workflow guardrails that point to tasks/sources | Rule maintenance |
| `.cursor/rules/report-writing.mdc` | Report writing quality standards | Rule maintenance |
| `templates/matchweek-data-template.md` | Agent 1 output schema | Agent 1 template |
| `templates/matchweek-report-template.md` | Agent 2 output schema | Agent 2 template |
| `reports/index.md` | Published report archive + accuracy column | Agent 2/Accuracy |
| `reports/accuracy-log.md` | Source/tier/consensus accuracy history and weights | Accuracy review |
| `feedback-log.md` | Append-only run observations | Agent 1/2/Accuracy |

---

## Key Rule

Never fabricate predictions, probabilities, or reasoning. If data is missing, state the gap explicitly and proceed with available evidence.
