# Matchweek Predictions -- Task Checklist

Follow this checklist step by step every time you generate a matchweek prediction report. Do not skip phases. Check off each item as you complete it.

---

## Phase 0: Setup

- [ ] Determine the **gameweek number** and **match dates** from the user's prompt (e.g., Gameweek 28, Saturday 2026-03-07).
- [ ] Read `knowledge/sources.md` to review the prediction sources and how to fetch from each.
- [ ] Read `knowledge/epl-context.md` for team context and key terms.
- [ ] Skim the most recent report in `reports/` (if one exists) for continuity.

---

## Phase 1: Fetch Fixtures and Context

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
- [ ] **Fetch league table and form data** for use in reasoning:
  1. Try `WebFetch` on BBC Sport Premier League table page.
  2. If that fails, use `WebSearch` for "Premier League table standings [date]".
  3. Record for each team in the matchweek: league position, points, home W-D-L, away W-D-L, goals scored, goals conceded.
  4. Note any relevant recent form (last 5 results) or injury/suspension news found during research.

---

## Phase 2: Gather Predictions

Work through sources in priority order. For each source, attempt to retrieve predictions for **all** fixtures in the matchweek.

### P1 Sources (always consult)

- [ ] **Forebet**: Fetch predictions from `forebet.com/en/football-tips-and-predictions-for-england/premier-league`.
  - For each fixture, record: predicted outcome (1/X/2), probability percentages, predicted score, over/under 2.5 prediction, BTTS prediction.
  - If the main page doesn't load, search: `site:forebet.com premier league predictions`.

- [ ] **PredixSport**: Fetch predictions from `predixsport.com/premier_league_predictions`.
  - For each fixture, record: win/draw/loss probabilities, over/under 2.5 probability, BTTS probability, any analysis text.
  - If the page doesn't load, search: `site:predixsport.com premier league predictions`.

- [ ] **FootyStats**: Fetch predictions from `footystats.org/england/premier-league/predictions`.
  - For each fixture, record: win/draw/loss probabilities, over/under 2.5 probability, BTTS probability, team form context.
  - If the page doesn't load, search: `site:footystats.org premier league predictions`.

### P2 Sources (consult after P1)

- [ ] **Winning Arena**: Search `site:winningarena.com premier league predictions this week` and fetch the results.
  - For each fixture, record: predicted outcome, over/under, BTTS, any expert reasoning.

- [ ] **Before You Bet**: Search `site:beforeyoubet.com.au EPL matchday [number] preview betting tips` and fetch the results.
  - For each fixture covered, record: predicted outcome, specific betting tip, qualitative reasoning, any stats or form analysis mentioned.

- [ ] **Bluecrossbar**: Fetch predictions from `bluecrossbar.com`.
  - For each fixture, record: predicted outcome, any confidence metric, predicted score.
  - If the page doesn't load (common -- JavaScript-rendered), search: `site:bluecrossbar.com premier league predictions`. Do not spend excessive time on this source.

### Fallback source discovery

- [ ] **Count usable P1 sources**. If fewer than 3 P1 sources returned prediction data:
  1. Search `premier league predictions gameweek [number] [year]` and evaluate the top results.
  2. Look for sites with structured predictions (probabilities, predicted outcomes) rather than opinion-only articles.
  3. Record predictions from the best alternative source found.
  4. Note the discovered source in the report's Sources section for potential future inclusion.

### Data quality check

- [ ] Verify you have predictions from at least 3 sources total. If fewer than 3, note this prominently in the report and recommend re-running closer to match day.
- [ ] If any source was unavailable or had not yet posted predictions, note which ones and why.

---

## Phase 3: Analyze and Aggregate

For each fixture in the matchweek:

- [ ] **Tally predictions**: Count how many sources predict Home Win, Draw, and Away Win.
- [ ] **Determine consensus**: The outcome with the most sources backing it is the consensus prediction. Record the confidence as "X out of Y sources agree" (where Y = number of sources that had predictions for that fixture).
- [ ] **Assign confidence tier** based on these definitions:
  - **High**: 4+ sources agree, OR 3/3 agree with average probability > 65%
  - **Moderate**: 3 sources agree (not meeting High criteria), OR 2/2 agree with average probability > 70%
  - **Low**: 2 sources agree with average probability <= 70%, or any split decision
- [ ] **Aggregate probabilities**: If multiple sources provide probability percentages, note the range (e.g., "Home win probability: 55-72% across sources").
- [ ] **Aggregate goals markets**: For each fixture, tally Over/Under 2.5 and BTTS predictions across sources that provide them.
- [ ] **Synthesize reasoning**: Combine the key factors mentioned across sources into 2-3 sentences explaining why the consensus leans this way. **Every fixture's reasoning must include at least one specific stat** (e.g., league position, W-D-L record, goals scored/conceded, recent form run). Use the table/form data gathered in Phase 1.
- [ ] **Flag split decisions**: If sources are evenly split (e.g., 2 Home, 2 Away, 1 Draw), flag this fixture as a "Split Decision" for the dedicated section.
- [ ] **Identify value picks**: Fixtures that qualify for the Value Picks section must meet **both** criteria: (a) at least 3 sources provided a prediction for the fixture, and (b) the confidence tier is High or Moderate. If no fixtures meet these criteria, state this explicitly in the Value Picks section.

---

## Phase 4: Write Report

- [ ] Copy the structure from `templates/matchweek-report-template.md`.
- [ ] Fill in the **Header** with gameweek number, dates, and report generation date.
- [ ] Write the **Matchweek Overview** (2-3 sentences on key storylines: title race, relegation battles, derbies, standout fixtures).
- [ ] Fill in the **Predictions Table** with all fixtures, their consensus, confidence tier, and X/Y fraction.
- [ ] Write the **Detailed Match Predictions** for every fixture:
  - Consensus prediction, confidence tier, and X/Y fraction
  - Source breakdown table (only include sources that had predictions -- no placeholder rows for missing sources)
  - Over/Under 2.5 and BTTS consensus
  - Key reasoning with specific stats (2-3 sentences)
- [ ] Write the **Value Picks** section (1-3 highest-confidence predictions with brief explanation). Minimum 3 sources must have covered the fixture to qualify.
- [ ] Write the **Split Decisions** section (fixtures where sources disagree, with analysis of why).
- [ ] Write the **Accumulator Ideas** section (2-3 suggested accumulators from highest-confidence picks, with a clear disclaimer).
- [ ] List all **Sources** consulted with links.
- [ ] Include the **Disclaimer** at the bottom.

### Quality checks

- [ ] Every fixture in the matchweek is covered.
- [ ] Every prediction is attributed to a named source.
- [ ] No predictions are fabricated.
- [ ] Reasoning is specific: every fixture includes at least one concrete stat (position, W-D-L, goals, form run).
- [ ] Confidence tiers (High / Moderate / Low) are assigned correctly per the definitions.
- [ ] Over/Under 2.5 and BTTS data is included where sources provide it.
- [ ] Source breakdown tables only list sources that had predictions (no empty placeholder rows).
- [ ] The report reads well in English, with professional tone.

---

## Phase 5: Publish

- [ ] Save the report as `reports/GWxx-YYYY-MM-DD-predictions.md` where `xx` is the zero-padded gameweek number and `YYYY-MM-DD` is the primary match date.
- [ ] Update `reports/index.md` with a new row for this report (date, gameweek, link, key themes).
- [ ] Confirm the report file was saved successfully.

---

## Phase 6: Post-Matchweek Accuracy Review

Run this phase **after the matchweek results are in** (typically Monday/Tuesday after the weekend fixtures). The user should prompt: "Update accuracy for Gameweek XX."

- [ ] Fetch actual results for all fixtures in the matchweek from BBC Sport or WebSearch.
- [ ] For each fixture, compare:
  - Consensus prediction vs. actual result (Correct / Incorrect)
  - Each individual source's prediction vs. actual result
- [ ] Update `reports/accuracy-log.md` with the results for this gameweek.
- [ ] Calculate and record:
  - Consensus accuracy for the gameweek (e.g., "7/10 correct")
  - Per-source accuracy for the gameweek
  - Running cumulative accuracy for each source across all tracked gameweeks
- [ ] Update `reports/index.md` to add accuracy % for the gameweek report.
- [ ] If a source's cumulative accuracy falls below 40% over 5+ gameweeks, flag it for review in `knowledge/sources.md`.
