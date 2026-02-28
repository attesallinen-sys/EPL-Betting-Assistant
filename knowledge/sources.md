# Prediction Sources

This file lists the curated free prediction sources the agent should consult for each matchweek. Sources are ordered by priority. The agent should always attempt P1 sources first, then P2 sources.

## Priority Levels

- **P1 (Primary)**: Reliable, structured prediction data with probabilities. Always consult these first.
- **P2 (Secondary)**: Useful supplementary predictions with qualitative analysis. Consult after P1 sources are covered.

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
  - BTTS prediction
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
  - BTTS probability (if available)
  - Any match analysis text provided
- **Timing**: Predictions usually available by Friday before the matchweek.
- **Limitations**: Newer site; prediction history is shorter.

### 3. FootyStats

- **URL**: https://footystats.org/england/premier-league/predictions
- **What it provides**: Data-driven predictions with win/draw/loss probabilities for each fixture. Also provides team stats, form data, over/under probabilities, and BTTS predictions. Integrates betting odds from major bookmakers.
- **How to fetch**: Use `WebFetch` on the URL above. If the page does not load, use `WebSearch` with query: `site:footystats.org premier league predictions`.
- **Data to extract per fixture**:
  - Win/Draw/Loss probability percentages
  - Over/under 2.5 goals probability
  - BTTS probability
  - Team form and stats context
- **Timing**: Predictions updated daily based on current season performance.
- **Limitations**: Some detailed stats may require a premium account; free tier provides core predictions and probabilities.
- **Accuracy tracking**: New source added GW29. Track reliability over coming weeks.
- **GW28 note**: The predictions page returned community user predictions (individual tipster picks) rather than algorithmic forecasts. The structured probability data may require a premium account or a different page URL. Excluded from consensus calculations for GW28.

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
- **Limitations**: Site includes community predictions alongside AI predictions; focus on the AI/expert predictions only. May not cover every fixture -- often features selected "tip of the day" matches.

### 5. Before You Bet

- **URL**: https://www.beforeyoubet.com.au/sports-betting/epl-tips
- **What it provides**: Expert-written matchday previews with detailed qualitative analysis. Covers team form, head-to-head records, tactical matchups, key player absences, and specific betting recommendations (including handicaps and over/under).
- **How to fetch**: Use `WebSearch` with query: `site:beforeyoubet.com.au EPL matchday [number] preview betting tips` to find the current matchweek preview, then `WebFetch` on the result URL. The URL pattern is typically `beforeyoubet.com.au/epl-2025-26-matchday-[number]-preview-betting-tips`.
- **Data to extract per fixture**:
  - Predicted outcome and specific betting tip (e.g., "Team X -1 handicap")
  - Qualitative reasoning: form analysis, injuries, tactical factors
  - Any head-to-head or statistical context mentioned
- **Timing**: Previews usually published 1-2 days before the matchweek.
- **Limitations**: Australian site; may not cover all 10 fixtures (typically picks 3-5 selected matches). Provides qualitative analysis rather than probability percentages.

### 6. Bluecrossbar

- **URL**: https://bluecrossbar.com/
- **What it provides**: Algorithm-based predictions covering the Premier League. Claims 88%+ accuracy based on 56,000+ historical matches. Provides 1X2 predictions.
- **How to fetch**: Use `WebFetch` on the main URL or navigate to the Premier League section. Use `WebSearch` with query: `site:bluecrossbar.com premier league predictions` if the page structure is unclear.
- **Data to extract per fixture**:
  - Predicted outcome (Home/Draw/Away)
  - Any confidence metric or probability provided
  - Predicted score if available
- **Timing**: Predictions typically posted before the weekend fixtures.
- **Limitations**: JavaScript-rendered site that frequently fails WebFetch. Has failed to return data in previous reports. Try it each week, but do not rely on it -- treat any data retrieved as a bonus.

---

## Retired Sources

### Transfermarkt

- **URL**: https://www.transfermarkt.com/betting/premier-league/
- **Status**: Retired as of GW28 (2026-02-28).
- **Reason**: The betting tips page did not yield matchweek-specific prediction data in a format the agent could extract. Transfermarkt's primary value is squad/transfer data, not match predictions.

---

## Fixture Data Source

To get the upcoming matchweek fixture list, use one of these approaches (in order of preference):

1. **BBC Sport**: `WebFetch` on `https://www.bbc.co.uk/sport/football/premier-league/scores-fixtures` -- provides a clean list of upcoming fixtures with dates and times.
2. **WebSearch**: Search for `Premier League fixtures this weekend [date]` to find the fixture list.
3. **premierleague.com**: `WebFetch` on `https://www.premierleague.com/fixtures` -- official source but may be JavaScript-heavy.

## League Table and Form Data

Before writing reasoning for each fixture, fetch current standings and form:

1. **BBC Sport**: `WebFetch` on `https://www.bbc.co.uk/sport/football/premier-league/table` -- current league table with points, W-D-L, GF, GA, GD.
2. **WebSearch**: Search for `Premier League table standings [date]` or `Premier League form guide [date]`.
3. **premierleague.com**: `WebFetch` on `https://www.premierleague.com/tables` for official standings.

Use this data to support reasoning with specific stats (league position, points, home/away W-D-L, goals scored/conceded).

---

## Search Query Templates

When a source's direct URL does not work or returns incomplete data, use these search queries:

```
site:forebet.com premier league predictions [date]
site:predixsport.com premier league predictions
site:footystats.org premier league predictions
site:winningarena.com premier league predictions [date]
site:beforeyoubet.com.au EPL matchday [number] preview
site:bluecrossbar.com premier league predictions
premier league predictions gameweek [number] [year]
premier league match predictions [home team] vs [away team]
```

## Handling Source Issues

- If a source has not posted predictions yet, note it in the report and exclude it from the consensus count.
- If a source returns errors or is unreachable, skip it and note the issue in the Sources section of the report.
- **Fallback source discovery**: If fewer than 3 P1 sources return usable prediction data, the agent MUST search for alternative prediction sites before writing the report. Use the query `premier league predictions gameweek [number] [year]` and evaluate the top results for structured prediction data. Record any newly discovered source for potential addition to this file.
- If fewer than 3 total sources (P1 + P2) have predictions available after fallback attempts, note this prominently in the report and recommend re-running the agent closer to match day.
- Never fabricate a prediction to fill a gap. An honest "3/4 sources consulted" is better than a made-up "5/5".

## Source Accuracy

After each matchweek's results are in, source accuracy should be tracked in `reports/accuracy-log.md`. Over time, this data informs which sources to trust most in split decisions and whether sources should be promoted, demoted, or retired.
