# EPL Betting Assistant

A Cursor AI agent pipeline that aggregates English Premier League match predictions from multiple free sources and produces matchweek prediction reports with consensus analysis, confidence levels, market odds comparison, and reasoning.

## How It Works

The workflow runs in sequence each week:

1. **Agent 1 (Data Collection)**: Produces the matchweek data file.
2. **Agent 2 (Predictions & Report)**: Produces the matchweek prediction report.
3. **Accuracy Review** (after results): Updates source accuracy and weights.

Use `AGENTS.md` for orchestration, `tasks/` for execution checklists, `knowledge/sources.md` for source policy, and `.cursor/rules/` for guardrails.

## Quick Start

### Step 1: Collect data

```
Fetch data for Gameweek XX (YYYY-MM-DD)
```

### Step 2: Generate report

```
Generate predictions for Gameweek XX (YYYY-MM-DD)
```

### Step 3: Track accuracy (after results)

```
Update accuracy for Gameweek XX
```

See `AGENTS.md` for full workflow ownership and run order.

## Project Structure

```
├── AGENTS.md                           # Two-agent workflow and configuration
├── improvements.md                     # Planned future enhancements
├── knowledge/
│   ├── sources.md                      # Canonical source URLs, fetch order, fallbacks
│   └── epl-context.md                  # EPL background, teams, format
├── tasks/
│   ├── fetch-matchweek-data.md         # Agent 1 task checklist
│   └── matchweek-predictions.md        # Agent 2 + accuracy checklist
├── templates/
│   ├── matchweek-data-template.md      # Agent 1 output template
│   └── matchweek-report-template.md    # Agent 2 report template
├── data/                               # Agent 1 output (gitignored)
├── reports/
│   ├── index.md                        # Report archive + accuracy entry
│   ├── accuracy-log.md                 # Source/tier/market accuracy + weights
│   └── GWxx-YYYY-MM-DD-predictions.md  # Generated reports
└── .cursor/rules/
    ├── research-workflow.mdc           # Workflow guardrails
    └── report-writing.mdc              # Report quality + formatting standards
```

## Disclaimer

This tool aggregates publicly available predictions for informational purposes only. It does not guarantee outcomes. Always gamble responsibly.
