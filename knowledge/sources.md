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

### 3. Bueon

- **URL**: https://www.bueon.com/en/ai-predictions/competition/england-premier-league
- **What it provides**: AI-generated normalized probability predictions (Home/Draw/Away percentages summing to 100%) for every Premier League fixture. Also highlights the strongest favourite, most balanced match, highest draw probability, and top away favourite across the matchweek.
- **How to fetch**: Use `WebFetch` on the URL above. The page lists all upcoming fixtures with probability breakdowns. If the page does not load, use `WebSearch` with query: `site:bueon.com england premier league ai predictions`.
- **Data to extract per fixture**:
  - Home/Draw/Away probability percentages
  - Stance label (e.g., "home favourite", "away favourite")
- **Timing**: Predictions updated continuously; available well in advance of each matchweek.
- **Limitations**: No predicted scores, over/under, or BTTS data. Probabilities only. No qualitative reasoning provided.
- **Accuracy tracking**: New source added GW29. Track reliability over coming weeks.

### 4. Sports Mole

- **URL**: https://www.sportsmole.co.uk/football/premier-league-predictions/
- **What it provides**: Expert-written predictions and previews for every Premier League fixture, with predicted scores and qualitative reasoning. Coverage is split across separate Saturday and Sunday articles each matchweek.
- **How to fetch**: Use `WebFetch` on the URL above to find links to the current matchweek's prediction articles (typically titled "Saturday's Premier League predictions..." and "Sunday's Premier League predictions..."). Then `WebFetch` each article. If the index page is insufficient, use `WebSearch` with query: `site:sportsmole.co.uk premier league predictions [day] [month] [year]`.
- **Data to extract per fixture**:
  - Predicted score (e.g., "We say: Liverpool 2-1 West Ham")
  - Qualitative reasoning: form, H2H, defensive/attacking stats, key factors
- **Timing**: Prediction articles published the day before or day of matches.
- **Limitations**: No probability percentages. Data is split across multiple articles (Saturday and Sunday), so both must be fetched for full matchweek coverage.
- **Accuracy tracking**: New source added GW29. Track reliability over coming weeks.

---

## P2 Sources

### 5. Winning Arena

- **URL**: https://winningarena.com/
- **What it provides**: AI-powered predictions with expert analysis. Covers 1X2, Over/Under goals, Both Teams to Score, and accumulators.
- **How to fetch**: Use `WebSearch` with query: `site:winningarena.com premier league predictions this week` to find the relevant page, then `WebFetch` on the result URL.
- **Data to extract per fixture**:
  - Predicted outcome
  - Over/under and BTTS predictions
  - Any expert analysis or reasoning text
- **Timing**: Predictions are posted throughout the week.
- **Limitations**: Site includes community predictions alongside AI predictions; focus on the AI/expert predictions only. May not cover every fixture -- often features selected "tip of the day" matches.

### 6. Before You Bet

- **URL**: https://www.beforeyoubet.com.au/sports-betting/epl-tips
- **What it provides**: Expert-written matchday previews with detailed qualitative analysis. Covers team form, head-to-head records, tactical matchups, key player absences, and specific betting recommendations (including handicaps and over/under).
- **How to fetch**: Use `WebSearch` with query: `site:beforeyoubet.com.au EPL matchday [number] preview betting tips` to find the current matchweek preview, then `WebFetch` on the result URL. The URL pattern is typically `beforeyoubet.com.au/epl-2025-26-matchday-[number]-preview-betting-tips`.
- **Data to extract per fixture**:
  - Predicted outcome and specific betting tip (e.g., "Team X -1 handicap")
  - Qualitative reasoning: form analysis, injuries, tactical factors
  - Any head-to-head or statistical context mentioned
- **Timing**: Previews usually published 1-2 days before the matchweek.
- **Limitations**: Australian site; may not cover all 10 fixtures (typically picks 3-5 selected matches). Provides qualitative analysis rather than probability percentages.

### 7. Flashscore

- **URL**: https://www.flashscore.co.uk/news/premier-league/dYlOSQODCdnS0XT8/
- **What it provides**: Data-led prediction articles covering approximately 6 selected Premier League fixtures per matchweek. Includes betting tips (moneyline, over/under, BTTS), qualitative analysis with form data, H2H stats, and defensive/attacking metrics.
- **How to fetch**: Use `WebSearch` with query: `site:flashscore.co.uk premier league gameweek [number] predictions` to find the current matchweek article, then `WebFetch` on the result URL.
- **Data to extract per fixture**:
  - Predicted outcome or specific betting tip (e.g., "Under 3.5 goals", "BTTS")
  - Qualitative reasoning: form runs, H2H records, defensive stats
  - Odds quoted (for context, not for reproduction)
- **Timing**: Articles published 1-2 days before the matchweek.
- **Limitations**: Does not cover all 10 fixtures (typically ~6 selected matches). Includes affiliate betting links; focus on the analysis content only.
- **Accuracy tracking**: New source added GW29. Track reliability over coming weeks.

### 8. BettingPros

- **URL**: https://www.bettingpros.com/articles/
- **What it provides**: Expert picks and odds analysis for selected Premier League matches. Covers moneyline, over/under, and specific betting angles with detailed statistical reasoning. Uses American odds format.
- **How to fetch**: Use `WebSearch` with query: `site:bettingpros.com premier league matchday [number] predictions [year]` to find the current matchweek article, then `WebFetch` on the result URL. The URL pattern is typically `bettingpros.com/articles/premier-league-matchday-[number]-odds-picks-predictions-[year]/`.
- **Data to extract per fixture**:
  - Predicted outcome or specific betting angle
  - Qualitative reasoning: team stats, defensive/offensive metrics, form analysis
  - Over/under or BTTS angle if provided
- **Timing**: Articles published 1-2 days before the matchweek.
- **Limitations**: Covers only 3-4 selected matches per matchweek (best bets). US-centric with American odds format. Does not provide probability percentages.
- **Accuracy tracking**: New source added GW29. Track reliability over coming weeks.

### 9. Action Network

- **URL**: https://www.actionnetwork.com/soccer/
- **What it provides**: Expert picks for Premier League matches with probability percentages, betting angles (moneyline, BTTS, over/under), and detailed statistical analysis. Often includes win probability percentages derived from their models.
- **How to fetch**: Use `WebSearch` with query: `site:actionnetwork.com premier league best bets predictions picks [month] [year]` to find the current matchweek article. Direct `WebFetch` may fail (JavaScript-heavy site); rely on search result summaries if needed.
- **Data to extract per fixture**:
  - Predicted outcome with win probability percentage (when available)
  - Specific betting pick (e.g., "Liverpool To Win and BTTS")
  - Qualitative reasoning: expected goals, form, scheduling advantages
- **Timing**: Articles published on or shortly before match days.
- **Limitations**: WebFetch frequently fails due to JavaScript rendering. May need to rely on search result summaries. Covers 3-5 selected matches per matchweek. US-centric with American odds.
- **Accuracy tracking**: New source added GW29. Track reliability over coming weeks.

---

## Odds Sources

These sources are used by **Agent 1** to fetch bookmaker odds for each fixture. Odds are converted to implied probabilities and included in the data file for Agent 2 to compare against prediction source consensus.

### Forebet (Odds Column)

- **URL**: https://www.forebet.com/en/football-tips-and-predictions-for-england/premier-league
- **What it provides**: Alongside predictions, Forebet displays average bookmaker odds for each fixture (Home/Draw/Away decimal odds).
- **How to fetch**: When Agent 1 fetches the Forebet page for predictions context, extract the odds column. Look for decimal odds (e.g., 1.85 / 3.50 / 4.20).
- **Limitations**: Odds may reflect an average across bookmakers rather than a single book. Still useful as a market benchmark.

### OddsPortal

- **URL**: https://www.oddsportal.com/football/england/premier-league/
- **What it provides**: Comprehensive odds comparison from multiple bookmakers for each fixture. Shows opening and closing odds.
- **How to fetch**: Use `WebFetch` on the URL above. If the page is JavaScript-heavy and returns incomplete data, use `WebSearch` with query: `site:oddsportal.com premier league odds [date]`.
- **Limitations**: JavaScript-heavy site; WebFetch may fail. Fall back to search.

### WebSearch Fallback

- **Query**: `Premier League gameweek [number] betting odds [date]`
- **What it provides**: Search results often include odds snippets from comparison sites, bookmaker pages, and news articles.
- **When to use**: If both Forebet odds and OddsPortal fail to provide complete data.

### Converting Odds to Implied Probabilities

1. **Raw implied probability**: `1 / decimal_odds` (e.g., odds of 2.50 → 40%)
2. **Calculate overround**: Sum all three implied probabilities. The amount over 100% is the bookmaker's margin (overround). Typical EPL overround is 3-8%.
3. **Fair (normalized) probability**: `raw_implied / sum_of_all_implied`. This removes the overround and gives probabilities summing to 100%.
4. Record both raw and fair probabilities in the data file. Use fair probabilities for comparison with source consensus.

---

## xG Data Sources

These sources are used by **Agent 1** to fetch expected goals (xG) data for each team in the matchweek. xG data provides an independent statistical signal that Agent 2 uses to identify regression risks and validate or challenge the prediction consensus.

### What xG Metrics Mean

- **xG (Expected Goals)**: The cumulative quality of scoring chances a team has created, measured in "expected goals." A team with 35.0 xG from 27 games has averaged ~1.30 xG per game.
- **xGA (Expected Goals Against)**: The cumulative quality of chances a team has conceded.
- **xGD (xG Difference)**: `xG - xGA`. Positive = creating better chances than conceding. The best proxy for underlying team quality.
- **Overperformance (Goals - xG)**: When a team scores significantly more than their xG, they are likely benefiting from finishing luck and may regress. When they score less, they may be due for improvement.
- A divergence of **3+ goals** between actual and expected over a season is notable. A divergence of **5+** is a strong regression signal.

### FBref (Primary)

- **URL**: `https://fbref.com/en/comps/9/Premier-League-Stats`
- **What it provides**: Comprehensive squad-level xG, xGA, and xGD for the current Premier League season. Also provides per-90-minute rates and non-penalty xG (npxG).
- **How to fetch**: `WebFetch` on the URL above will likely time out (JavaScript-heavy). Fall back to `WebSearch` with query: `site:fbref.com premier league 2025-2026 expected goals stats`. Search results often include squad-level xG summaries.
- **Data to extract per team**:
  - Season xG (total expected goals)
  - Season xGA (total expected goals against)
  - xGD (xG difference)
- **Limitations**: Direct page fetch almost always fails. Rely on `WebSearch` to surface xG data from FBref pages or summaries.

### Understat (Secondary)

- **URL**: `https://understat.com/league/EPL`
- **What it provides**: xG table for the current EPL season with xG, xGA, xGD, npxG, npxGA, and expected points (xPTS) per team. Also provides per-match xG data.
- **How to fetch**: `WebFetch` on the URL above will likely return minimal data (JavaScript-rendered). Fall back to `WebSearch` with query: `site:understat.com EPL xG table 2025-2026`.
- **Data to extract per team**:
  - Season xG and xGA
  - xGD
  - npxGD (non-penalty xG difference, if available)
- **Limitations**: Almost entirely JavaScript-rendered. `WebFetch` returns only page scaffolding. `WebSearch` is the reliable method.

### WebSearch Fallback

If both FBref and Understat fail via direct fetch and site-specific search:

- **Query**: `Premier League xG table 2025-2026 season team stats`
- **Alternative query**: `Premier League expected goals standings [month] [year]`
- **Per-team query**: `[team name] xG 2025-2026 season expected goals` (use if league-wide data is incomplete)
- **What to look for**: Any result showing team-level xG, xGA, and xGD for the current season. Sites like xgstat.com, infogol.net, and football analytics blogs often publish xG tables.

### Calculating Overperformance

After fetching xG data, calculate the following for each team in the matchweek:

1. **Attacking overperformance**: `Actual Goals Scored - xG`. Positive = scoring above expected (luck/hot finishing). Negative = underperforming chances.
2. **Defensive overperformance**: `xGA - Actual Goals Conceded`. Positive = conceding fewer than expected (strong defending or keeper form). Negative = conceding more than expected.
3. Flag any team with an attacking or defensive overperformance magnitude of **3+ goals** as a regression candidate.

---

## Retired Sources

### Transfermarkt

- **URL**: https://www.transfermarkt.com/betting/premier-league/
- **Status**: Retired as of GW28 (2026-02-28).
- **Reason**: The betting tips page did not yield matchweek-specific prediction data in a format the agent could extract. Transfermarkt's primary value is squad/transfer data, not match predictions.

### FootyStats

- **URL**: https://footystats.org/england/premier-league/predictions
- **Status**: Retired as of GW28 (2026-02-28).
- **Reason**: Free tier returned community user picks rather than algorithmic predictions. Structured probability data appeared to require a premium account.

### Bluecrossbar

- **URL**: https://bluecrossbar.com/
- **Status**: Retired as of GW28 (2026-02-28).
- **Reason**: JavaScript-rendered site consistently failed WebFetch. Never returned usable prediction data across multiple report attempts.

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
site:bueon.com england premier league ai predictions
site:sportsmole.co.uk premier league predictions [day] [month] [year]
site:winningarena.com premier league predictions [date]
site:beforeyoubet.com.au EPL matchday [number] preview
site:flashscore.co.uk premier league gameweek [number] predictions
site:bettingpros.com premier league matchday [number] predictions [year]
site:actionnetwork.com premier league best bets predictions picks [month] [year]
premier league predictions gameweek [number] [year]
premier league match predictions [home team] vs [away team]
site:fbref.com premier league 2025-2026 expected goals stats
site:understat.com EPL xG table 2025-2026
Premier League xG table 2025-2026 season team stats
[team name] xG 2025-2026 season expected goals
```

## Handling Source Issues

- If a source has not posted predictions yet, note it in the report and exclude it from the consensus count.
- If a source returns errors or is unreachable, skip it and note the issue in the Sources section of the report.
- **Fallback source discovery**: If fewer than 3 P1 sources return usable prediction data, the agent MUST search for alternative prediction sites before writing the report. Use the query `premier league predictions gameweek [number] [year]` and evaluate the top results for structured prediction data. Record any newly discovered source for potential addition to this file.
- If fewer than 3 total sources (P1 + P2) have predictions available after fallback attempts, note this prominently in the report and recommend re-running the agent closer to match day.
- Never fabricate a prediction to fill a gap. An honest "3/4 sources consulted" is better than a made-up "5/5".

## Source Accuracy

After each matchweek's results are in, source accuracy should be tracked in `reports/accuracy-log.md`. Over time, this data informs which sources to trust most in split decisions and whether sources should be promoted, demoted, or retired.
