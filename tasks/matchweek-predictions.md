# Matchweek Predictions -- Task Checklist

This is the task checklist for **Agent 2 (Predictions & Report)**. It assumes Agent 1 has already produced a data file at `data/GWxx-matchweek-data.md` containing fixtures, league table, xG data, and bookmaker odds.

Follow this checklist step by step every time you generate a matchweek prediction report. Do not skip phases.

---

## Phase 0: Setup

- [ ] Determine the **gameweek number** and **match dates** from the user's prompt.
- [ ] Read the data file at `data/GWxx-matchweek-data.md` (produced by Agent 1). If it does not exist, inform the user they need to run Agent 1 first.
- [ ] Read `knowledge/sources.md` to review prediction sources and how to fetch from each.
- [ ] Read `knowledge/epl-context.md` for team context and key terms.
- [ ] Read `reports/accuracy-log.md` for current source weights (default 1.0 if no accuracy data yet).
- [ ] Skim the most recent report in `reports/` (if one exists) for continuity.

---

## Phase 1: Load Matchweek Data

- [ ] From the data file, load:
  - All fixtures (home, away, date, kickoff time)
  - League table positions, points, W-D-L (home and away), goals scored/conceded
  - Expected goals (xG) data: xG, xGA, xGD, overperformance, and regression flags per team
  - Bookmaker odds and implied probabilities for each fixture
- [ ] Verify data completeness: all fixtures present, odds available for most fixtures.
- [ ] Note any data gaps flagged in the data file's "Data Quality Notes" and "xG Notes" sections. If xG data is missing, proceed without it -- it is supplementary.

---

## Phase 2: Gather Predictions

Work through sources in priority order. For each source, attempt to retrieve predictions for **all** fixtures.

### P1 Sources (always consult)

- [ ] **Forebet**: Fetch predictions from `forebet.com/en/football-tips-and-predictions-for-england/premier-league`.
  - For each fixture, record: predicted outcome (1/X/2), probability percentages, predicted score, over/under 2.5 prediction, BTTS prediction.
  - If the main page doesn't load, search: `site:forebet.com premier league predictions`.

- [ ] **PredixSport**: Fetch predictions from `predixsport.com/premier_league_predictions`.
  - For each fixture, record: win/draw/loss probabilities, over/under 2.5 probability, BTTS probability, any analysis text.
  - If the page doesn't load, search: `site:predixsport.com premier league predictions`.

- [ ] **Bueon**: Fetch predictions from `bueon.com/en/ai-predictions/competition/england-premier-league`.
  - For each fixture, record: home/draw/away probability percentages.
  - If the page doesn't load, search: `site:bueon.com england premier league ai predictions`.

- [ ] **Sports Mole**: Fetch from `sportsmole.co.uk/football/premier-league-predictions/`.
  - Find the current matchweek's Saturday and Sunday prediction articles and fetch both.
  - For each fixture, record: predicted score, qualitative reasoning.
  - If the index page doesn't work, search: `site:sportsmole.co.uk premier league predictions [day] [month] [year]`.

### P2 Sources (consult after P1)

- [ ] **Winning Arena**: Search `site:winningarena.com premier league predictions this week` and fetch the results.
  - For each fixture, record: predicted outcome, over/under, BTTS, any expert reasoning.

- [ ] **Before You Bet**: Search `site:beforeyoubet.com.au EPL matchday [number] preview betting tips` and fetch the results.
  - For each fixture covered, record: predicted outcome, specific betting tip, qualitative reasoning.

- [ ] **Flashscore**: Search `site:flashscore.co.uk premier league gameweek [number] predictions` and fetch the results.
  - For each fixture covered, record: predicted outcome/tip, qualitative reasoning, form/H2H stats.

- [ ] **BettingPros**: Search `site:bettingpros.com premier league matchday [number] predictions [year]` and fetch the results.
  - For each fixture covered, record: predicted outcome, qualitative reasoning, stats.

- [ ] **Action Network**: Search `site:actionnetwork.com premier league best bets predictions picks [month] [year]` and fetch the results.
  - For each fixture covered, record: predicted outcome, win probability (if provided), reasoning.

### Fallback source discovery

- [ ] **Count usable P1 sources**. If fewer than 3 P1 sources returned prediction data:
  1. Search `premier league predictions gameweek [number] [year]` and evaluate the top results.
  2. Look for sites with structured predictions (probabilities, predicted outcomes).
  3. Record predictions from the best alternative source found.
  4. Note the discovered source in the report's Sources section.

### Data quality check

- [ ] Verify predictions from at least 3 sources total. If fewer, note this prominently and recommend re-running closer to match day.
- [ ] Note any sources that were unavailable or had not yet posted predictions.

---

## Phase 3: Analyze and Aggregate

For each fixture in the matchweek:

### Consensus and confidence

- [ ] **Tally predictions**: Count sources predicting Home Win, Draw, and Away Win.
- [ ] **Apply source weights**: Read current source weights from `reports/accuracy-log.md` (see Source Weights section). If no weights exist yet, use 1.0 for all sources.
  - For each outcome, compute weighted score: `sum of weights for sources backing that outcome`.
  - The outcome with the highest weighted score is the consensus.
  - Example: if Forebet (weight 1.2) and PredixSport (weight 1.0) say Home, and Bueon (weight 1.0) and Sports Mole (weight 0.9) say Draw, the Home weighted score is 2.2 vs Draw weighted score of 1.9 -- Home wins.
- [ ] **Determine consensus**: Record the weighted consensus outcome and the unweighted source fraction (e.g., "3/5 sources").
- [ ] **Assign confidence tier** based on these definitions:
  - **High**: 4+ sources agree, OR 3/3 agree with average probability > 65%
  - **Moderate**: 3 sources agree (not meeting High criteria), OR 2/2 agree with average probability > 70%
  - **Low**: 2 sources agree with average probability <= 70%, or any split decision

### Probabilities and odds comparison

- [ ] **Aggregate source probabilities**: Note the range across sources (e.g., "Home win: 55-72%").
- [ ] **Compare consensus to market odds**: For each fixture, compare the consensus probability to the implied probability from bookmaker odds (loaded from data file).
  - If consensus probability > implied probability by 5+ percentage points, flag as a **potential value bet** (consensus sees more edge than the market).
  - If consensus probability < implied probability by 5+ percentage points, flag as a **market disagreement** (the market is more confident than sources -- proceed with caution).
  - Record the edge: `Edge = Average consensus probability - Fair implied probability from odds`.

### Goals markets and reasoning

- [ ] **Aggregate goals markets**: Tally Over/Under 2.5 and BTTS predictions across sources.
- [ ] **Synthesize reasoning**: Combine key factors from sources into 2-3 sentences per fixture. **Every fixture must include at least one concrete stat** (league position, W-D-L, goals, form run). Use the league table data from the data file.
- [ ] **Flag split decisions**: If sources are evenly split, flag for the Split Decisions section.
- [ ] **Identify value picks**: Fixtures qualifying for Value Picks must meet **both**: (a) at least 3 sources provided a prediction, and (b) confidence tier is High or Moderate. Additionally, note any fixtures with a positive edge vs. odds (from the comparison above).

### xG analysis (if data available)

Skip this subsection if the data file has no xG data.

- [ ] **Check for regression risks**: For each fixture, review both teams' overperformance flags from the data file.
  - If a team is flagged for **attacking regression** (GF - xG >= 3): their goal output may be unsustainable. Note this if the consensus backs them to win or if Over 2.5 is the goals consensus.
  - If a team is flagged for **defensive regression** (xGA - GA <= -3): they may concede more going forward. Note this if the consensus backs a clean sheet or low-scoring game.
- [ ] **Cross-check xG vs. consensus**: Does the xGD ranking support the predicted outcome? If xG data contradicts the consensus (e.g., consensus says Home Win but the away team has a much stronger xGD), note this as a reason for caution.
- [ ] **Cross-check xG vs. market odds**: If xGD suggests a team is stronger than the market prices them (or weaker), note the divergence. This can reinforce or weaken a value bet flag.
- [ ] **Integrate into reasoning**: Where xG provides a clear signal (supports or contradicts the consensus), weave it into the fixture's key reasoning. Do not force xG commentary onto every fixture -- only include it where the signal is meaningful (overperformance >= 3 goals, or xGD contradicts the consensus).

---

## Phase 4: Write Report

- [ ] Copy the structure from `templates/matchweek-report-template.md`.
- [ ] Fill in the **Header** with gameweek number, dates, report generation date, and sources consulted.
- [ ] Write the **Matchweek Overview** (2-3 sentences on key storylines).
- [ ] Fill in the **Predictions Table** with all fixtures, consensus, confidence tier, source fraction, average probability, and market implied probability.
- [ ] Write the **Detailed Match Predictions** for every fixture:
  - Consensus prediction, confidence tier, and source fraction
  - Source breakdown table (only sources with data; include O/U 2.5 and BTTS columns)
  - Market odds comparison line (consensus probability vs. implied probability, edge)
  - Goals market summary
  - xG context line (optional -- include when xG diverges meaningfully from actual results or contradicts the consensus; omit when xG simply confirms what other data already shows)
  - Key reasoning with specific stats
- [ ] Write the **Value Picks** section (1-3 highest-confidence predictions with strong edge vs. market).
- [ ] Write the **Split Decisions** section (fixtures where sources disagree, with analysis of why).
- [ ] Write the **Accumulator Ideas** section (2-3 suggested accumulators with disclaimer).
- [ ] List all **Sources** consulted with links and coverage notes.
- [ ] Include the **Disclaimer** at the bottom.

### Quality checks

- [ ] Every fixture in the matchweek is covered.
- [ ] Every prediction is attributed to a named source.
- [ ] No predictions are fabricated.
- [ ] Reasoning is specific: every fixture includes at least one concrete stat.
- [ ] Confidence tiers are assigned correctly per definitions.
- [ ] Market odds comparison is included for each fixture.
- [ ] xG context is included for fixtures where regression flags or xG-consensus contradictions exist.
- [ ] Source breakdown tables only list sources with predictions (no empty rows).
- [ ] Professional, analytical tone throughout.

---

## Phase 5: Publish

- [ ] Save the report as `reports/GWxx-YYYY-MM-DD-predictions.md`.
- [ ] Update `reports/index.md` with a new row for this report.
- [ ] Confirm the report file was saved successfully.

---

## Phase 6: Post-Matchweek Accuracy Review

Run this phase **after the matchweek results are in** (typically Monday/Tuesday). The user should prompt: "Update accuracy for Gameweek XX."

### Step 1: Fetch and verify actual results

- [ ] Fetch results for all fixtures from a primary source. Use `WebSearch` targeting an all-in-one results page rather than assembling scores from individual searches. Recommended query: `"Premier League results gameweek [XX] [matchweek date range] scores"`. See the Results Sources section in `knowledge/sources.md` for reliable sources.
- [ ] **Cross-reference every score** against a second source (e.g., if primary was BBC Sport, check ESPN or Sky Sports). This catches search snippet errors.
- [ ] If any score conflicts between sources, fetch a third source to break the tie before proceeding.

### Step 2: Load market data (if available)

- [ ] Check if `data/GWxx-matchweek-data.md` exists.
  - **If yes**: Load bookmaker odds / fair implied probabilities. Determine the market favourite for each fixture (the outcome with the highest implied probability).
  - **If no**: Mark all Market Fav / Market Correct columns as "N/A". Note in observations that market comparison requires Agent 1 to have been run before the matchweek. Optionally attempt to fetch closing odds retroactively via `WebSearch` (e.g., `"Premier League gameweek [XX] closing odds [date]"`) -- but treat retroactive odds as best-effort and label them accordingly.

### Step 3: Reconcile sources

- [ ] Read the Sources section of `reports/GWxx-YYYY-MM-DD-predictions.md` to identify which sources were actually used in the report.
- [ ] Compare that list against the Source Weights and Cumulative Source Accuracy tables in `reports/accuracy-log.md`.
- [ ] If any source in the report is missing from the accuracy log tables, add it to both the Source Weights table (with default weight 1.0) and the Cumulative Source Accuracy table before recording results.
- [ ] Do not remove inactive sources from the tables (they retain historical data). Only record results for sources that were actually consulted.

### Step 4: Compare predictions vs. results

- [ ] Read the Prediction Summary table from the report (if present) to extract each source's prediction per fixture. If no summary table exists, extract predictions from the detailed match prediction sections.
- [ ] For each fixture, compare:
  - Consensus prediction vs. actual result (Correct / Incorrect)
  - Each individual source's prediction vs. actual result
  - Market favourite (from odds) vs. actual result (or N/A if no odds data)

### Step 5: Update accuracy log

- [ ] Update `reports/accuracy-log.md`:
  - Add a new Gameweek Results block with per-fixture, per-source results.
  - Update the Cumulative Source Accuracy table (add this gameweek's correct/total to the running totals).
  - Update the Confidence Tier Accuracy table.
  - Update the Market vs. Consensus Comparison table.
  - **Recalculate source weights** if 5+ gameweeks of data exist (see formula in accuracy-log.md).
- [ ] Update `reports/index.md` to add accuracy % for the gameweek.
- [ ] If a source's cumulative accuracy falls below 40% over 5+ gameweeks, flag it for review in `knowledge/sources.md`.
