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

- [ ] Fetch fixtures using the Fixture Data Source section in `knowledge/sources.md` (follow its source order and fallback strategy).
- [ ] Record all fixtures:
  - Home team
  - Away team
  - Date
  - Kickoff time (UK time)
- [ ] Confirm fixture count (typically 10 per gameweek; note any postponements).

---

## Phase 2: Fetch League Table and Form Data

- [ ] Fetch league table and form data using the League Table and Form Data section in `knowledge/sources.md`.
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

- [ ] Fetch expected goals (xG) data using the xG Data Sources section in `knowledge/sources.md`.
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

- [ ] Fetch odds/probabilities using the Odds Sources section in `knowledge/sources.md` (primary, secondary, then fallback sources).
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

---

## Finalize Feedback Loop

- [ ] Fill `## Agent Observations` in the data file (`None` if no issues).
- [ ] Append concise observations to `feedback-log.md` `## Open` using the required format from `.cursor/rules/research-workflow.mdc`.
