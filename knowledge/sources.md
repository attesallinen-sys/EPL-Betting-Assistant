# Prediction Sources

This file lists the curated free prediction sources the agent should consult for each matchweek. Sources are ordered by priority. The agent should always attempt P1 sources first, then P2 sources.

## Priority Levels

- **P1 (Primary)**: Reliable, structured prediction data with probabilities. Always consult these.
- **P2 (Secondary)**: Useful supplementary predictions. Consult after P1 sources are covered.

---

## P1 Sources

### 1. Forebet

- **URL**: https://www.forebet.com/en/football-tips-and-predictions-for-england/premier-league
- **What it provides**: Mathematical predictions based on statistical algorithms. For each match: 1X2 probabilities (percentage for Home/Draw/Away), predicted correct score, over/under 2.5 goals prediction, average goals prediction, and BTTS (both teams to score).
- **How to fetch**: Use `WebFetch` on the URL above. The page lists all upcoming Premier League fixtures with predictions. If the page does not load well, use `WebSearch` with query: `site:forebet.com premier league predictions`.
- **Data to extract per fixture**:
  - Predicted outcome (1/X/2) and the associated probability percentages
  - Predicted correct score
  - Over/under 2.5 goals prediction
  - Any stated reasoning or key factors
- **Timing**: Predictions are typically available 2-3 days before matches.
- **Limitations**: Page may be JavaScript-heavy. If WebFetch returns incomplete data, fall back to WebSearch for individual match predictions.

### 2. PredixSport

- **URL**: https://www.predixsport.com/premier_league_predictions
- **What it provides**: AI-powered predictions with result probabilities (percentage for Home Win, Draw, Away Win), over/under 2.5 goals probabilities, and goal/no goal forecasts.
- **How to fetch**: Use `WebFetch` on the URL above. If that fails, use `WebSearch` with query: `site:predixsport.com premier league predictions`.
- **Data to extract per fixture**:
  - Win/Draw/Loss probability percentages
  - Over/under 2.5 goals probability
  - Any match analysis text provided
- **Timing**: Predictions usually available by Friday before the matchweek.
- **Limitations**: Newer site; prediction history is shorter.

### 3. Bluecrossbar

- **URL**: https://bluecrossbar.com/
- **What it provides**: Algorithm-based predictions covering the Premier League. Claims 88%+ accuracy based on 56,000+ historical matches. Provides 1X2 predictions.
- **How to fetch**: Use `WebFetch` on the main URL or navigate to the Premier League section. Use `WebSearch` with query: `site:bluecrossbar.com premier league predictions` if the page structure is unclear.
- **Data to extract per fixture**:
  - Predicted outcome (Home/Draw/Away)
  - Any confidence metric or probability provided
  - Predicted score if available
- **Timing**: Predictions typically posted before the weekend fixtures.
- **Limitations**: Smaller site; may not always have predictions for rescheduled midweek fixtures.

---

## P2 Sources

### 4. Winning Arena

- **URL**: https://winningarena.com/
- **What it provides**: AI-powered predictions with expert analysis. Covers 1X2, Over/Under goals, Both Teams to Score, and accumulators.
- **How to fetch**: Use `WebSearch` with query: `site:winningarena.com premier league predictions this week` to find the relevant page, then `WebFetch` on the result URL.
- **Data to extract per fixture**:
  - Predicted outcome
  - Over/under and BTTS predictions
  - Any expert analysis or reasoning text
- **Timing**: Predictions are posted throughout the week.
- **Limitations**: Site includes community predictions alongside AI predictions; focus on the AI/expert predictions only.

### 5. Transfermarkt

- **URL**: https://www.transfermarkt.com/betting/premier-league/
- **What it provides**: Expert betting tips and predictions based on statistical analysis. Provides match outcome predictions with brief analysis.
- **How to fetch**: Use `WebSearch` with query: `site:transfermarkt.com premier league betting tips predictions` to find current matchweek predictions, then `WebFetch` on the result.
- **Data to extract per fixture**:
  - Predicted outcome
  - Any odds or probability information
  - Expert analysis text or reasoning
- **Timing**: Updated after each matchweek for the next round of fixtures.
- **Limitations**: Predictions may be less structured than algorithm-based sites. Transfermarkt's primary value is its deep statistical context.

---

## Fixture Data Source

To get the upcoming matchweek fixture list, use one of these approaches (in order of preference):

1. **BBC Sport**: `WebFetch` on `https://www.bbc.co.uk/sport/football/premier-league/scores-fixtures` -- provides a clean list of upcoming fixtures with dates and times.
2. **WebSearch**: Search for `Premier League fixtures this weekend [date]` to find the fixture list.
3. **premierleague.com**: `WebFetch` on `https://www.premierleague.com/fixtures` -- official source but may be JavaScript-heavy.

---

## Search Query Templates

When a source's direct URL does not work or returns incomplete data, use these search queries:

```
site:forebet.com premier league predictions [date]
site:predixsport.com premier league predictions
site:bluecrossbar.com premier league predictions
site:winningarena.com premier league predictions [date]
site:transfermarkt.com premier league betting tips
premier league predictions gameweek [number] [year]
premier league match predictions [home team] vs [away team]
```

## Handling Source Issues

- If a source has not posted predictions yet, note it in the report and exclude it from the consensus count.
- If a source returns errors or is unreachable, skip it and note the issue in the Sources section of the report.
- If fewer than 3 sources have predictions available, suggest re-running the agent closer to match day.
- Never fabricate a prediction to fill a gap. An honest "3/4 sources consulted" is better than a made-up "5/5".
