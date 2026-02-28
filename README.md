# EPL Betting Assistant

A Cursor AI agent that aggregates English Premier League match predictions from multiple free sources and produces matchweek prediction reports with consensus analysis, confidence levels, and reasoning.

## How It Works

Before each Premier League matchweek, the agent:

1. **Fetches fixtures** for the upcoming gameweek
2. **Crawls 5 prediction sources** (Forebet, PredixSport, Bluecrossbar, Winning Arena, Transfermarkt)
3. **Aggregates predictions** into a consensus view per fixture
4. **Produces a report** with confidence levels (e.g., "4/5 sources agree") and synthesized reasoning

## Quick Start

Open a new Cursor agent conversation in this project and paste:

```
Generate predictions for Gameweek XX (YYYY-MM-DD)
```

Replace `XX` with the gameweek number and `YYYY-MM-DD` with the Saturday date. The agent follows the task checklist in `tasks/matchweek-predictions.md` automatically.

## Project Structure

```
├── AGENTS.md                  # Agent configuration and instructions
├── knowledge/
│   ├── sources.md             # Prediction sources with URLs and priorities
│   └── epl-context.md         # EPL background, teams, format
├── tasks/
│   └── matchweek-predictions.md   # Step-by-step agent checklist
├── templates/
│   └── matchweek-report-template.md   # Report structure template
├── reports/
│   ├── index.md               # Report archive
│   └── GWxx-YYYY-MM-DD-predictions.md  # Generated reports
└── .cursor/rules/
    ├── research-workflow.mdc  # How to crawl and fetch predictions
    └── report-writing.mdc     # Report formatting standards
```

## Disclaimer

This tool aggregates publicly available predictions for informational purposes only. It does not guarantee outcomes. Always gamble responsibly.
