# Fetch Matchweek Data -- Task Checklist

This is the task checklist for **Agent 1 (Data Collection)**. Follow it step by step. The output is a structured data file that Agent 2 (Predictions & Report) will consume.

> **Parallelism**: Phases 1, 2, 2.5, and 3 are independent data fetches. Run them in parallel where possible to reduce total fetch time. Phase 4 (compile) depends on all prior phases completing.

---

## Phase 0: Setup

- [ ] Determine the **gameweek number** and **match dates** from the user's prompt.
- [ ] Read `knowledge/sources.md` to review fixture data sources, league table sources, odds sources, and xG sources.
- [ ] Read `knowledge/epl-context.md` for team names and key context.
- [ ] Read `templates/matchweek-data-template.md` for the output format.

---

## Phase 1: Fetch Fixtures

- [ ] Fetch the fixture list using the sources in `knowledge/sources.md`:
  1. Use `WebSearch` for "Premier League fixtures gameweek [number] [date]". This is the most reliable method.
  2. If search results are insufficient, try `WebFetch` on BBC Sport (`https://www.bbc.co.uk/sport/football/premier-league/scores-fixtures`). Note: BBC often returns date headers but no team names due to JavaScript rendering.
  3. As a last resort, try premierleague.com fixtures page.
- [ ] Record all fixtures:
  - Home team
  - Away team
  - Date
  - Kickoff time (UK time)
- [ ] Confirm fixture count (typically 10 per gameweek; note any postponements).

---

## Phase 2: Fetch League Table and Form Data

- [ ] Fetch the current league table and home/away splits:
  1. Try `WebFetch` on SoccerStats.com (`https://www.soccerstats.com/homeaway.asp?league=england`). This single page provides the full table, home/away W-D-L, and form data.
  2. If SoccerStats fails, use `WebSearch` for "Premier League table standings [date]".
  3. As a fallback, try BBC Sport (`https://www.bbc.co.uk/sport/football/premier-league/table`). Note: BBC returns stats but team names are often missing due to JavaScript.
- [ ] Record for each team (at minimum):
  - League position
  - Games played (P)
  - Points
  - W-D-L overall
  - Home W-D-L
  - Away W-D-L
  - Goals scored and conceded
- [ ] Record recent form (last 5-8 results) if available from the source. Note the period covered (e.g., "last 8").

---

## Phase 2.5: Fetch xG Data

- [ ] Fetch expected goals (xG) data using the xG sources in `knowledge/sources.md`:
  1. Use `WebSearch` with query: `Premier League 2025-2026 xG xGA all teams season stats table expected goals against`. StatMuse results typically appear with per-team data.
  2. If incomplete, try `WebSearch` with query: `site:fbref.com premier league 2025-2026 expected goals stats`.
  3. If still incomplete, try: `Premier League xG table 2025-2026 season team stats`.
  4. For any missing teams, try per-team search: `[team name] xG 2025-2026 season expected goals`.
- [ ] For each team, record:
  - Season xG (total expected goals created)
  - Season xGA (total expected goals against)
  - xGD (xG difference: xG - xGA)
  - **Number of matches covered by the xG data** (critical for normalization)
- [ ] **Normalize xG before comparing to actual goals**:
  - Record the xG match count (P_xg) and the league table match count (P_table) for each team.
  - If they differ, scale xG up: `adjusted_xG = xG * (P_table / P_xg)`. Same for xGA.
  - Use adjusted values for all overperformance calculations.
- [ ] **Calculate overperformance**:
  - Attacking overperformance: `GF - adjusted_xG` (positive = scoring above expected)
  - Defensive overperformance: `adjusted_xGA - GA` (positive = conceding fewer than expected)
- [ ] **Flag regression candidates**: any team with attacking or defensive overperformance magnitude of **5+ goals**.
- [ ] Attempt to find last-5-match xG trends per team. If unavailable, note it and proceed with season-level data only.
- [ ] If xG data cannot be fetched, note the gap in the "xG Notes" and "Data Quality Notes" sections. This does not block the rest of the data file.

---

## Phase 3: Fetch Bookmaker Odds

- [ ] Fetch odds/probabilities for each fixture using the odds sources in `knowledge/sources.md`:
  1. Try `WebFetch` on Gambletron2000.com fixture pages for fair (vig-removed) probabilities. This is the most reliable source.
  2. If Gambletron is incomplete, try Dimers.com or RotoWire for additional fixtures.
  3. As a fallback, try Forebet, OddsPortal, or `WebSearch` for "Premier League gameweek [number] odds".
- [ ] For each fixture, record:
  - Home/Draw/Away **fair probabilities** (summing to ~100%)
  - Decimal odds (derived from fair probabilities with ~5% overround if the source provides probabilities only, or directly from the source if decimal odds are provided)
- [ ] If the source provides decimal odds instead of fair probabilities, convert using the formula in `knowledge/sources.md` (under "Converting Odds to Fair Probabilities").
- [ ] Note the odds source, overround percentage, and any notable market signals (heavy favourites, very tight odds, etc.) in the Odds Notes section.

---

## Phase 4: Compile Data File

- [ ] Copy the structure from `templates/matchweek-data-template.md`.
- [ ] Fill in all sections: Fixtures, League Table, Recent Form, Expected Goals (xG) Data, Bookmaker Odds.
- [ ] Save the file as `data/GWxx-matchweek-data.md` (where `xx` is the zero-padded gameweek number).
- [ ] Verify the file is complete: all fixtures listed, league table populated, odds for all fixtures.

### Data quality checks

- [ ] All fixtures have kickoff times.
- [ ] League table data covers at least the teams playing this matchweek, with games played (P) recorded.
- [ ] Odds/probabilities are available for at least 8/10 fixtures (note any missing).
- [ ] Fair probabilities sum to approximately 100% per fixture.
- [ ] xG data is available for at least the majority of teams, with match counts recorded and normalization applied.
- [ ] Note any data gaps in the "Data Quality Notes" section.

---

## Output

The completed file at `data/GWxx-matchweek-data.md` is the handoff artifact. Agent 2 (Predictions & Report) will read this file as its starting point.
