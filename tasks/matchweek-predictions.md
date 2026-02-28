# Matchweek Predictions -- Task Checklist

Follow this checklist step by step every time you generate a matchweek prediction report. Do not skip phases. Check off each item as you complete it.

---

## Phase 0: Setup

- [ ] Determine the **gameweek number** and **match dates** from the user's prompt (e.g., Gameweek 28, Saturday 2026-03-07).
- [ ] Read `knowledge/sources.md` to review the prediction sources and how to fetch from each.
- [ ] Read `knowledge/epl-context.md` for team context and key terms.
- [ ] Skim the most recent report in `reports/` (if one exists) for continuity.

---

## Phase 1: Fetch Fixtures

- [ ] Fetch the upcoming fixture list using the fixture data sources described in `knowledge/sources.md`:
  1. Try `WebFetch` on BBC Sport Premier League fixtures page.
  2. If that fails, use `WebSearch` for "Premier League fixtures gameweek [number]".
  3. As a last resort, try the official premierleague.com fixtures page.
- [ ] Record all fixtures for the matchweek in a working list:
  - Home team
  - Away team
  - Date
  - Kickoff time (UK time)
- [ ] Confirm the fixture count matches expectations (typically 10 matches per gameweek, but can vary due to postponements or rescheduling).

---

## Phase 2: Gather Predictions

Work through sources in priority order. For each source, attempt to retrieve predictions for **all** fixtures in the matchweek.

### P1 Sources (always consult)

- [ ] **Forebet**: Fetch predictions from `forebet.com/en/football-tips-and-predictions-for-england/premier-league`.
  - For each fixture, record: predicted outcome (1/X/2), probability percentages, predicted score, over/under prediction.
  - If the main page doesn't load, search: `site:forebet.com premier league predictions`.

- [ ] **PredixSport**: Fetch predictions from `predixsport.com/premier_league_predictions`.
  - For each fixture, record: win/draw/loss probabilities, over/under probability, any analysis text.
  - If the page doesn't load, search: `site:predixsport.com premier league predictions`.

- [ ] **Bluecrossbar**: Fetch predictions from `bluecrossbar.com`.
  - For each fixture, record: predicted outcome, any confidence metric, predicted score.
  - If the page doesn't load, search: `site:bluecrossbar.com premier league predictions`.

### P2 Sources (consult after P1)

- [ ] **Winning Arena**: Search `site:winningarena.com premier league predictions this week` and fetch the results.
  - For each fixture, record: predicted outcome, over/under, BTTS, any expert reasoning.

- [ ] **Transfermarkt**: Search `site:transfermarkt.com premier league betting tips` and fetch the results.
  - For each fixture, record: predicted outcome, any odds info, expert analysis text.

### Data quality check

- [ ] Verify you have predictions from at least 3 sources. If fewer than 3, note this prominently in the report and recommend re-running closer to match day.
- [ ] If any source was unavailable or had not yet posted predictions, note which ones and why.

---

## Phase 3: Analyze and Aggregate

For each fixture in the matchweek:

- [ ] **Tally predictions**: Count how many sources predict Home Win, Draw, and Away Win.
- [ ] **Determine consensus**: The outcome with the most sources backing it is the consensus prediction. Record the confidence as "X out of Y sources agree" (where Y = number of sources that had predictions for that fixture).
- [ ] **Aggregate probabilities**: If multiple sources provide probability percentages, note the range (e.g., "Home win probability: 55-72% across sources").
- [ ] **Synthesize reasoning**: Combine the key factors mentioned across sources into 2-3 sentences explaining why the consensus leans this way. Consider: form, injuries, home advantage, head-to-head, tactical matchups, league position.
- [ ] **Flag split decisions**: If sources are evenly split (e.g., 2 Home, 2 Away, 1 Draw), flag this fixture as a "Split Decision" for the dedicated section.
- [ ] **Identify value picks**: Fixtures where 4+ out of 5 sources agree are "High Confidence" picks. Note these for the Value Picks section.

---

## Phase 4: Write Report

- [ ] Copy the structure from `templates/matchweek-report-template.md`.
- [ ] Fill in the **Header** with gameweek number, dates, and report generation date.
- [ ] Write the **Matchweek Overview** (2-3 sentences on key storylines: title race, relegation battles, derbies, standout fixtures).
- [ ] Fill in the **Predictions Table** with all fixtures and their consensus + confidence.
- [ ] Write the **Detailed Match Predictions** for every fixture:
  - Consensus prediction and confidence
  - Source breakdown (which source predicted what)
  - Key reasoning (2-3 sentences)
- [ ] Write the **Value Picks** section (1-3 highest-confidence predictions with brief explanation).
- [ ] Write the **Split Decisions** section (fixtures where sources disagree, with analysis of why).
- [ ] List all **Sources** consulted with links.
- [ ] Include the **Disclaimer** at the bottom.

### Quality checks

- [ ] Every fixture in the matchweek is covered.
- [ ] Every prediction is attributed to a named source.
- [ ] No predictions are fabricated.
- [ ] Reasoning is specific (mentions actual factors like form, injuries) not generic.
- [ ] The report reads well in English, with professional tone.

---

## Phase 5: Publish

- [ ] Save the report as `reports/GWxx-YYYY-MM-DD-predictions.md` where `xx` is the zero-padded gameweek number and `YYYY-MM-DD` is the primary match date.
- [ ] Update `reports/index.md` with a new row for this report (date, gameweek, link, key themes).
- [ ] Confirm the report file was saved successfully.
