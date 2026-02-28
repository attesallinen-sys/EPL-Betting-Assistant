# Fetch Matchweek Data -- Task Checklist

This is the task checklist for **Agent 1 (Data Collection)**. Follow it step by step. The output is a structured data file that Agent 2 (Predictions & Report) will consume.

---

## Phase 0: Setup

- [ ] Determine the **gameweek number** and **match dates** from the user's prompt.
- [ ] Read `knowledge/sources.md` to review fixture data sources, league table sources, and odds sources.
- [ ] Read `knowledge/epl-context.md` for team names and key context.
- [ ] Read `templates/matchweek-data-template.md` for the output format.

---

## Phase 1: Fetch Fixtures

- [ ] Fetch the fixture list using the sources in `knowledge/sources.md`:
  1. Try `WebFetch` on BBC Sport Premier League fixtures page.
  2. If that fails, use `WebSearch` for "Premier League fixtures gameweek [number] [date]".
  3. As a last resort, try the official premierleague.com fixtures page.
- [ ] Record all fixtures:
  - Home team
  - Away team
  - Date
  - Kickoff time (UK time)
- [ ] Confirm fixture count (typically 10 per gameweek; note any postponements).

---

## Phase 2: Fetch League Table and Form Data

- [ ] Fetch the current league table:
  1. Try `WebFetch` on BBC Sport Premier League table page (`https://www.bbc.co.uk/sport/football/premier-league/table`).
  2. If that fails, use `WebSearch` for "Premier League table standings [date]".
  3. As a last resort, try premierleague.com tables.
- [ ] Record for each team in the matchweek (at minimum):
  - League position
  - Points
  - W-D-L overall
  - Home W-D-L
  - Away W-D-L
  - Goals scored and conceded
- [ ] Note any relevant recent form (last 5 results) if available from the table source.

---

## Phase 2.5: Fetch xG Data

- [ ] Fetch expected goals (xG) data for the teams playing this matchweek using the xG sources in `knowledge/sources.md`:
  1. Try `WebFetch` on FBref (`https://fbref.com/en/comps/9/Premier-League-Stats`). Expect this to fail (JavaScript-heavy).
  2. Try `WebFetch` on Understat (`https://understat.com/league/EPL`). Expect this to fail (JavaScript-heavy).
  3. Fall back to `WebSearch` with query: `site:fbref.com premier league 2025-2026 expected goals stats`.
  4. If still incomplete, try: `Premier League xG table 2025-2026 season team stats`.
  5. For any missing teams, try per-team search: `[team name] xG 2025-2026 season expected goals`.
- [ ] For each team in the matchweek, record:
  - Season xG (total expected goals created)
  - Season xGA (total expected goals against)
  - xGD (xG difference: xG - xGA)
- [ ] **Calculate overperformance** using actual goals from the league table (Phase 2):
  - Attacking overperformance: `GF - xG` (positive = scoring above expected)
  - Defensive overperformance: `xGA - GA` (positive = conceding fewer than expected)
- [ ] **Flag regression candidates**: any team with attacking or defensive overperformance magnitude of 3+ goals.
- [ ] Attempt to find last-5-match xG trends per team. If unavailable from search results, note it and proceed with season-level data only.
- [ ] If xG data cannot be fetched for any source, note the gap in the "xG Notes" and "Data Quality Notes" sections. This does not block the rest of the data file.

---

## Phase 3: Fetch Bookmaker Odds

- [ ] Fetch odds for each fixture using the odds sources in `knowledge/sources.md`:
  1. Try `WebFetch` on Forebet's Premier League page (odds are displayed alongside predictions -- extract only the odds, not the predictions).
  2. If Forebet odds are incomplete, try `WebSearch` for "Premier League gameweek [number] odds" or use OddsPortal.
  3. As a fallback, try Google search results which often show odds snippets.
- [ ] For each fixture, record:
  - Home win decimal odds
  - Draw decimal odds
  - Away win decimal odds
- [ ] **Convert odds to implied probabilities** using this formula:
  - `Implied probability = 1 / decimal_odds`
  - Calculate the overround: `Overround = (sum of all implied probabilities) - 1`
  - Normalize to fair probabilities: `Fair probability = implied_probability / (1 + overround)`
  - Record both raw implied probabilities and fair (normalized) probabilities in the data file.
- [ ] Note the odds source and any notable market signals (heavy favourites, very tight odds, etc.).

---

## Phase 4: Compile Data File

- [ ] Copy the structure from `templates/matchweek-data-template.md`.
- [ ] Fill in all sections: Fixtures, League Table, Recent Form, Expected Goals (xG) Data, Bookmaker Odds.
- [ ] Save the file as `data/GWxx-matchweek-data.md` (where `xx` is the zero-padded gameweek number).
- [ ] Verify the file is complete: all fixtures listed, league table populated, odds for all fixtures.

### Data quality checks

- [ ] All fixtures have kickoff times.
- [ ] League table data covers at least the teams playing this matchweek.
- [ ] Odds are available for at least 8/10 fixtures (note any missing).
- [ ] Implied probabilities sum to approximately 100% per fixture (after normalization).
- [ ] xG data is available for at least the majority of teams in the matchweek (note any missing).
- [ ] Note any data gaps in the "Data Quality Notes" section.

---

## Output

The completed file at `data/GWxx-matchweek-data.md` is the handoff artifact. Agent 2 (Predictions & Report) will read this file as its starting point.
