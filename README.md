# EPL Betting Assistant

A Cursor AI agent pipeline that aggregates English Premier League match predictions from multiple free sources and produces matchweek prediction reports with consensus analysis, confidence levels, market odds comparison, and reasoning.

## How It Works

The pipeline uses two agents run in sequence before each matchweek:

1. **Agent 1 (Data Collection)**: Fetches fixtures, league table, and bookmaker odds. Outputs a structured data file.
2. **Agent 2 (Predictions & Report)**: Crawls prediction sources, aggregates into a weighted consensus, compares against market odds, and produces the report.
3. **Accuracy Review** (after results): Tracks per-source accuracy and updates source weights for future reports.

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

See `AGENTS.md` for the full workflow and resource guide.

## Project Structure

```
├── AGENTS.md                           # Two-agent workflow and configuration
├── improvements.md                     # Planned future enhancements
├── knowledge/
│   ├── sources.md                      # Prediction + odds sources with URLs
│   └── epl-context.md                  # EPL background, teams, format
├── tasks/
│   ├── fetch-matchweek-data.md         # Agent 1 task checklist
│   └── matchweek-predictions.md        # Agent 2 task checklist
├── templates/
│   ├── matchweek-data-template.md      # Agent 1 output template
│   └── matchweek-report-template.md    # Agent 2 report template
├── data/                               # Agent 1 output (gitignored)
├── reports/
│   ├── index.md                        # Report archive
│   ├── accuracy-log.md                 # Source accuracy + weights
│   └── GWxx-YYYY-MM-DD-predictions.md  # Generated reports
└── .cursor/rules/
    ├── research-workflow.mdc           # Research workflow for both agents
    └── report-writing.mdc             # Report formatting standards
```

## Disclaimer

This tool aggregates publicly available predictions for informational purposes only. It does not guarantee outcomes. Always gamble responsibly.
