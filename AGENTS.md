# EPL Betting Assistant

## Overview

This project uses a two-agent pipeline to produce matchweek prediction reports for the English Premier League. Agent 1 collects objective data (fixtures, league table, xG metrics, bookmaker odds). Agent 2 gathers predictions from multiple sources, analyzes them against the data (including xG as an independent signal), and writes the report.

---

## Agent 1: Data Collection

**Purpose**: Gather objective matchweek data that prediction analysis depends on.

**Prompt**:

> Fetch data for Gameweek XX (YYYY-MM-DD)

Replace `XX` with the gameweek number and `YYYY-MM-DD` with the primary match date.

**Task checklist**: `tasks/fetch-matchweek-data.md`

**What it does**:
1. Fetches the fixture list (teams, dates, kickoff times)
2. Fetches the current league table and form data
3. Fetches xG and advanced metrics (xG, xGA, xGD per team) and calculates overperformance vs. actual goals
4. Fetches bookmaker odds and converts to implied probabilities

**Output**: `data/GWxx-matchweek-data.md` -- a structured data file consumed by Agent 2.

**When to run**: Any time after fixtures are confirmed (typically by midweek). Odds are more stable closer to match day (Friday/Saturday), so running Thursday-Saturday is ideal.

---

## Agent 2: Predictions & Report

**Purpose**: Gather predictions from multiple sources, analyze them against the data, and produce the matchweek report.

**Prompt**:

> Generate predictions for Gameweek XX (YYYY-MM-DD)

**Prerequisite**: Agent 1 must have produced `data/GWxx-matchweek-data.md` first.

**Task checklist**: `tasks/matchweek-predictions.md`

**What it does**:
1. Reads the data file from Agent 1 (including xG data)
2. Fetches predictions from P1 and P2 sources (see `knowledge/sources.md`)
3. Aggregates predictions using weighted consensus (source weights from accuracy tracking)
4. Compares consensus probabilities against bookmaker odds to identify value
5. Uses xG data as an independent analytical signal to flag regression risks and validate the consensus
6. Writes the full matchweek report

**Output**: `reports/GWxx-YYYY-MM-DD-predictions.md`

**When to run**: After Agent 1, ideally Friday evening or Saturday morning to capture the latest editorial predictions and team news.

---

## Accuracy Review

**Purpose**: Track prediction accuracy to improve future reports through source weighting.

**Prompt**:

> Update accuracy for Gameweek XX

**When to run**: After all matchweek results are in (typically Monday/Tuesday).

**What it does**: Follows Phase 6 of `tasks/matchweek-predictions.md`:
1. Fetches actual results
2. Scores each source's predictions and the consensus
3. Updates `reports/accuracy-log.md` with per-source, per-tier accuracy
4. Recalculates source weights (after 5+ gameweeks of data)
5. Updates `reports/index.md` with the gameweek's accuracy percentage

---

## Typical Weekly Workflow

1. **Thursday/Friday**: Run Agent 1 to collect fixtures, league table, xG data, and odds.
2. **Friday/Saturday**: Run Agent 2 to gather predictions and produce the report.
3. **Monday/Tuesday**: Run Accuracy Review after results are in.

---

## Resources

| Resource | Location | Purpose |
|----------|----------|---------|
| Prediction sources | `knowledge/sources.md` | Curated list of prediction sites, xG data sources, odds sources, with URLs and extraction guidance |
| EPL context | `knowledge/epl-context.md` | Background on the Premier League: teams, format, key terms |
| Agent 1 task checklist | `tasks/fetch-matchweek-data.md` | Step-by-step for data collection |
| Agent 2 task checklist | `tasks/matchweek-predictions.md` | Step-by-step for prediction gathering and report writing |
| Data template | `templates/matchweek-data-template.md` | Template for Agent 1's output data file |
| Report template | `templates/matchweek-report-template.md` | Template for Agent 2's matchweek report |
| Report archive | `reports/index.md` | Index of all published prediction reports with accuracy tracking |
| Accuracy log | `reports/accuracy-log.md` | Per-source and cumulative accuracy tracking with source weights |
| Future improvements | `improvements.md` | Planned enhancements (xG data, value betting analysis, Elo ratings, etc.) |

## Quality Standards

- **Accuracy**: Only include predictions that are actually published by the sources. Never fabricate predictions or probabilities.
- **Attribution**: Clearly attribute each prediction to its source.
- **Consensus clarity**: State the predicted outcome and how many sources back it. When source weights are active, note the weighted consensus.
- **Market context**: Every fixture should show how the consensus compares to bookmaker odds.
- **Reasoning depth**: 2-3 sentences per fixture synthesizing *why* sources lean a certain way, with at least one concrete stat. Include xG context when it provides a meaningful signal (regression risk, xG-consensus contradiction).
- **Completeness**: Cover every fixture. If a source lacks a prediction, note it rather than guessing.
- **Tone**: Professional, analytical, balanced. Never guarantee outcomes.

## Rules

- Always follow `.cursor/rules/` for research and report-writing standards.
- Never fabricate predictions, probabilities, or reasoning.
- Always attribute information to its source.
- If a prediction source has not yet published predictions, note this and suggest running the agent closer to match day.
- Include a disclaimer that predictions are for informational purposes only.
