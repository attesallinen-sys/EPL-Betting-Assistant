# Prediction Accuracy Log

This file tracks prediction accuracy across gameweeks, per source, per confidence tier, and for the overall consensus. It also maintains source weights used for weighted consensus in future reports.

---

## Source Weights

Weights are used by Agent 2 to compute weighted consensus predictions. Default weight is 1.0 for all sources until at least 5 gameweeks of accuracy data have been collected.

**Status**: Not yet calculated (fewer than 5 gameweeks tracked).

### Current Weights

| Source | Weight | Based On | Last Updated |
|--------|--------|----------|-------------|
| Forebet | 1.0 | Default | -- |
| PredixSport | 1.0 | Default | -- |
| Bueon | 1.0 | Default | -- |
| Sports Mole | 1.0 | Default | -- |
| Winning Arena | 1.0 | Default | -- |
| Before You Bet | 1.0 | Default | -- |
| Radio Times | 1.0 | Default | -- |
| Flashscore | 1.0 | Default | -- |
| BettingPros | 1.0 | Default | -- |
| Action Network | 1.0 | Default | -- |

### Weight Calculation Formula

After 5+ gameweeks of data, recalculate weights using:

1. Compute each source's cumulative accuracy rate (correct predictions / total predictions).
2. Compute the average accuracy across all sources.
3. Weight = source accuracy / average accuracy. This normalizes around 1.0.
   - A source with 60% accuracy when the average is 50% gets weight 1.2.
   - A source with 40% accuracy when the average is 50% gets weight 0.8.
4. Cap weights between 0.5 and 2.0 to prevent any single source from dominating.
5. Sources with fewer than 20 total predictions keep the default weight of 1.0 until they accumulate enough data.

---

## Cumulative Source Accuracy

| Source | Correct | Total | Accuracy | Gameweeks Tracked |
|--------|---------|-------|----------|-------------------|
| Forebet | 10 | 28 | 36% | 3 |
| PredixSport | 12 | 24 | 50% | 3 |
| Bueon | 7 | 20 | 35% | 2 |
| Sports Mole | 4 | 13 | 31% | 2 |
| Winning Arena | 1 | 1 | 100% | 1 |
| Before You Bet | 1 | 5 | 20% | 2 |
| Radio Times | 5 | 10 | 50% | 1 |
| Flashscore | -- | -- | -- | 0 |
| BettingPros | -- | -- | -- | 0 |
| Action Network | 1 | 5 | 20% | 2 |
| **Consensus** | 10 | 30 | 33% | 3 |
| **Market (odds favourite)** | 7 | 20 | 35% | 3 |

---

## Confidence Tier Accuracy

Tracks how often predictions at each confidence tier are correct.

| Tier | Correct | Total | Accuracy | Notes |
|------|---------|-------|----------|-------|
| High | 6 | 13 | 46% | GW30: only Arsenal correct among five High picks; Liverpool/Brentford draws and Chelsea home loss |
| Moderate | 3 | 8 | 38% | GW30: Man Utd correct; Burnley-Bournemouth draw wrong vs Bournemouth lean |
| Low | 1 | 9 | 11% | GW30: 0/3 Low correct (split, Palace, Forest) |

---

## Market vs. Consensus Comparison

Tracks whether the consensus or the market favourite was more often correct.

| Metric | Value |
|--------|-------|
| Gameweeks tracked | 3 |
| Consensus correct | 10/30 (33%) |
| Market favourite correct | 7/20 (35%) (GW28: N/A; GW29--30 with odds) |
| Both agreed and correct | 4 (GW29: Everton, Arsenal; GW30: Arsenal vs Everton, Man Utd vs Aston Villa) |
| Consensus correct, market wrong | 0 |
| Market correct, consensus wrong | 3 (GW29: Aston Villa vs Chelsea, Newcastle vs Man United; GW30: Sunderland vs Brighton -- market Away fav, split consensus) |

---

## Gameweek Results

### Gameweek 30 (2026-03-14)

Scores cross-checked: Guardian / BBC Sport / ESPN match reports (March 14--16, 2026).

| # | Home | Away | Actual Result | Consensus | Correct? | Market Fav | Market Correct? |
|---|------|------|--------------|-----------|----------|-----------|----------------|
| 1 | Burnley | Bournemouth | 0-0 (Draw) | Away Win | No | Away (53%) | No |
| 2 | Sunderland | Brighton | 0-1 (Away Win) | Split (Away lean) | No | Away (45%) | Yes |
| 3 | Chelsea | Newcastle | 0-1 (Away Win) | Home Win | No | Home (52%) | No |
| 4 | Arsenal | Everton | 2-0 (Home Win) | Home Win | Yes | Home (70%) | Yes |
| 5 | West Ham | Man City | 1-1 (Draw) | Away Win | No | Away (58%) | No |
| 6 | Crystal Palace | Leeds | 0-0 (Draw) | Home Win | No | Home (39%) | No |
| 7 | Man Utd | Aston Villa | 3-1 (Home Win) | Home Win | Yes | Home (57%) | Yes |
| 8 | Nottm Forest | Fulham | 0-0 (Draw) | Home Win | No | Home (42%) | No |
| 9 | Liverpool | Tottenham | 1-1 (Draw) | Home Win | No | Home (76%) | No |
| 10 | Brentford | Wolves | 2-2 (Draw) | Home Win | No | Home (62%) | No |

**Per-source accuracy this gameweek**:

| Source | Predictions Made | Correct | Accuracy |
|--------|-----------------|---------|----------|
| Forebet | 10 | 4 | 40% |
| PredixSport | 10 | 3 | 30% |
| Bueon | 10 | 3 | 30% |
| Sports Mole | 5 | 1 | 20% |
| Action Network | 4 | 1 | 25% |

**Per-source detail**:

| # | Fixture | Actual | Forebet | PredixSport | Bueon | Sports Mole | Action Network |
|---|---------|--------|---------|-------------|-------|-------------|----------------|
| 1 | BUR-BOU | Draw | Draw (/) | Away Win (X) | Away Win (X) | Away Win (X) | -- |
| 2 | SUN-BHA | Away Win | Home Win (X) | Away Win (/) | Away Win (/) | Home Win (X) | Draw (X) |
| 3 | CHE-NEW | Away Win | Home Win (X) | Home Win (X) | Home Win (X) | Home Win (X) | Home Win (X) |
| 4 | ARS-EVE | Home Win | Home Win (/) | Home Win (/) | Home Win (/) | Home Win (/) | Home Win (/) |
| 5 | WHU-MCI | Draw | Away Win (X) | Away Win (X) | Away Win (X) | Away Win (X) | Away Win (X) |
| 6 | CRY-LEE | Draw | Draw (/) | Home Win (X) | Home Win (X) | -- | -- |
| 7 | MUN-AVL | Home Win | Home Win (/) | Home Win (/) | Home Win (/) | -- | -- |
| 8 | NFO-FUL | Draw | Away Win (X) | Home Win (X) | Home Win (X) | -- | -- |
| 9 | LIV-TOT | Draw | Home Win (X) | Home Win (X) | Home Win (X) | -- | -- |
| 10 | BRE-WOL | Draw | Home Win (X) | Home Win (X) | Home Win (X) | -- | -- |

**Confidence tier accuracy this gameweek**:

| Tier | Correct | Total | Accuracy |
|------|---------|-------|----------|
| High | 1 | 5 | 20% |
| Moderate | 1 | 2 | 50% |
| Low | 0 | 3 | 0% |

**Consensus accuracy**: 2/10 (20%)
**Market favourite accuracy**: 3/10 (30%)

**Notable observations**:
- Draw-heavy week: six draws (half the slate), including Liverpool 1-1 Tottenham and Brentford 2-2 Wolves, sank most home/away consensus calls.
- Chelsea 0-1 Newcastle was a clean sweep miss -- all five sources backed Chelsea at Stamford Bridge.
- West Ham 1-1 Man City denied the unanimous High-confidence Away pick (and the largest consensus edge vs. odds).
- Forebet led the panel at 4/10, benefiting from correct Draw calls on Burnley-Bournemouth and Crystal Palace-Leeds.
- Sunderland 0-1 Brighton: market favourite (Brighton) was correct; consensus remained a split (scored incorrect as no single 1X2 outcome).
- **Governance**: No demotion/retirement actions -- minimum evidence window (5 gameweeks or 20+ predictions) not met for panel sources under `knowledge/sources.md`.

---

### Gameweek 29 (2026-03-03)

| # | Home | Away | Actual Result | Consensus | Correct? | Market Fav | Market Correct? |
|---|------|------|--------------|-----------|----------|-----------|----------------|
| 1 | Bournemouth | Brentford | 0-0 (Draw) | Home Win (split) | No | Home (39%) | No |
| 2 | Everton | Burnley | 2-0 (Home Win) | Home Win | Yes | Home (61%) | Yes |
| 3 | Leeds United | Sunderland | 0-1 (Away Win) | Home Win | No | Home (50%) | No |
| 4 | Wolves | Liverpool | 2-1 (Home Win) | Away Win | No | Away (69%) | No |
| 5 | Aston Villa | Chelsea | 1-4 (Away Win) | Draw | No | Away (39%) | Yes |
| 6 | Brighton | Arsenal | 0-1 (Away Win) | Away Win | Yes | Away (59%) | Yes |
| 7 | Fulham | West Ham | 0-1 (Away Win) | Home Win | No | Home (47%) | No |
| 8 | Man City | Nottm Forest | 2-2 (Draw) | Home Win | No | Home (73%) | No |
| 9 | Newcastle | Man United | 2-1 (Home Win) | Away Win | No | Split H/A (37%) | Yes |
| 10 | Tottenham | Crystal Palace | 1-3 (Away Win) | Home Win | No | Home (41%) | No |

**Per-source accuracy this gameweek**:

| Source | Predictions Made | Correct | Accuracy |
|--------|-----------------|---------|----------|
| Forebet | 8 | 1 | 13% |
| PredixSport | 4 | 2 | 50% |
| Bueon | 10 | 4 | 40% |
| Sports Mole | 8 | 3 | 38% |
| Before You Bet | 2 | 0 | 0% |
| Action Network | 1 | 0 | 0% |

**Per-source detail**:

| # | Fixture | Actual | Forebet | PredixSport | Bueon | Sports Mole | Before You Bet | Action Network |
|---|---------|--------|---------|-------------|-------|-------------|----------------|----------------|
| 1 | BOU-BRE | Draw | Away Win (X) | Home Win (X) | Home Win (X) | Draw (/) | -- | -- |
| 2 | EVE-BUR | Home Win | Home Win (/) | Home Win (/) | Home Win (/) | Home Win (/) | -- | -- |
| 3 | LEE-SUN | Away Win | Home Win (X) | -- | Home Win (X) | Home Win (X) | -- | -- |
| 4 | WOL-LIV | Home Win | Away Win (X) | Away Win (X) | Away Win (X) | Away Win (X) | -- | Away Win (X) |
| 5 | AVL-CHE | Away Win | Draw (X) | -- | Away Win (/) | -- | Draw (X) | -- |
| 6 | BHA-ARS | Away Win | -- | Away Win (/) | Away Win (/) | Away Win (/) | -- | -- |
| 7 | FUL-WHU | Away Win | Home Win (X) | -- | Home Win (X) | -- | -- | -- |
| 8 | MCI-NFO | Draw | Home Win (X) | -- | Home Win (X) | Home Win (X) | -- | -- |
| 9 | NEW-MUN | Home Win | -- | -- | Home Win (/) | Away Win (X) | Away Win (X) | -- |
| 10 | TOT-CRY | Away Win | Home Win (X) | -- | Home Win (X) | Home Win (X) | -- | -- |

**Confidence tier accuracy this gameweek**:

| Tier | Correct | Total | Accuracy |
|------|---------|-------|----------|
| High | 2 | 4 | 50% |
| Moderate | 0 | 2 | 0% |
| Low | 0 | 4 | 0% |

**Consensus accuracy**: 2/10 (20%)
**Market favourite accuracy**: 4/10 (40%)

**Notable observations**:
- Worst consensus accuracy on record. Only 2/10 correct, with 6 fixtures producing outright upsets or unexpected results.
- Wolves 2-1 Liverpool was the biggest shock -- a unanimous 5/5 High-confidence Away Win pick undone by a 90+4' winner from bottom-placed Wolves. This mirrors the GW28 Wolves-Villa upset.
- Man City 2-2 Nottm Forest was the second major miss -- a High-confidence Home Win at the Etihad derailed by a late Forest equaliser.
- Tottenham's collapse continued (1-3 to Crystal Palace), defying 3/3 Home Win picks. The xG data in the report had flagged this as a risky pick.
- The market outperformed the consensus this week (4/10 vs 2/10), correctly picking Chelsea at Villa and catching Newcastle vs Man United as a coin-flip.
- Forebet had a historically poor week at 1/8 (13%), dragging its cumulative accuracy to 33%.
- Bueon was the most reliable source at 4/10, correctly backing Chelsea (Away Win) and Newcastle (Home Win) where other sources missed.

---

### Gameweek 28 (2026-02-28)

| # | Home | Away | Actual Result | Consensus | Correct? | Market Fav | Market Correct? |
|---|------|------|--------------|-----------|----------|-----------|----------------|
| 1 | Wolves | Aston Villa | 2-0 (Home Win) | Away Win | No | N/A | N/A |
| 2 | Bournemouth | Sunderland | 1-1 (Draw) | Home Win | No | N/A | N/A |
| 3 | Burnley | Brentford | 3-4 (Away Win) | Away Win | Yes | N/A | N/A |
| 4 | Liverpool | West Ham | 5-2 (Home Win) | Home Win | Yes | N/A | N/A |
| 5 | Newcastle | Everton | 2-3 (Away Win) | Home Win | No | N/A | N/A |
| 6 | Leeds | Man City | 0-1 (Away Win) | Away Win | Yes | N/A | N/A |
| 7 | Brighton | Nottm Forest | 2-1 (Home Win) | Draw | No | N/A | N/A |
| 8 | Fulham | Tottenham | 2-1 (Home Win) | Home Win | Yes | N/A | N/A |
| 9 | Man United | Crystal Palace | 2-1 (Home Win) | Home Win | Yes | N/A | N/A |
| 10 | Arsenal | Chelsea | 2-1 (Home Win) | Home Win | Yes | N/A | N/A |

**Per-source accuracy this gameweek**:

| Source | Predictions Made | Correct | Accuracy |
|--------|-----------------|---------|----------|
| Forebet | 10 | 5 | 50% |
| PredixSport | 10 | 7 | 70% |
| Radio Times | 10 | 5 | 50% |
| Winning Arena | 1 | 1 | 100% |
| Before You Bet | 3 | 1 | 33% |

**Per-source detail**:

| # | Fixture | Actual | Forebet | PredixSport | Radio Times | Winning Arena | Before You Bet |
|---|---------|--------|---------|-------------|-------------|---------------|----------------|
| 1 | WOL-AVL | Home Win | Away Win (X) | Away Win (X) | Away Win (X) | -- | -- |
| 2 | BOU-SUN | Draw | Home Win (X) | Home Win (X) | Home Win (X) | -- | -- |
| 3 | BUR-BRE | Away Win | Away Win (/) | Away Win (/) | Home Win (X) | -- | -- |
| 4 | LIV-WHU | Home Win | Home Win (/) | Home Win (/) | Home Win (/) | -- | -- |
| 5 | NEW-EVE | Away Win | Draw (X) | Home Win (X) | Home Win (X) | -- | Home Win (X) |
| 6 | LEE-MCI | Away Win | Away Win (/) | Away Win (/) | Away Win (/) | -- | -- |
| 7 | BHA-NFO | Home Win | Draw (X) | Home Win (/) | Draw (X) | -- | -- |
| 8 | FUL-TOT | Home Win | Home Win (/) | Home Win (/) | Home Win (/) | -- | -- |
| 9 | MUN-CRY | Home Win | Home Win (/) | Home Win (/) | Home Win (/) | -- | Home Win (/) |
| 10 | ARS-CHE | Home Win | Draw (X) | Home Win (/) | Home Win (/) | Home Win (/) | Draw (X) |

**Confidence tier accuracy this gameweek**:

| Tier | Correct | Total | Accuracy |
|------|---------|-------|----------|
| High | 3 | 4 | 75% |
| Moderate | 2 | 4 | 50% |
| Low | 1 | 2 | 50% |

**Consensus accuracy**: 6/10 (60%)
**Market favourite accuracy**: N/A (no odds data available for GW28)

**Notable observations**:
- Wolves 2-0 Aston Villa was the biggest upset, defying a unanimous High-confidence Away Win prediction. Every source got this wrong.
- PredixSport was the standout performer at 70%, correctly picking Brighton's home win against Forest where others predicted a draw.
- Before You Bet had the worst accuracy (1/3, 33%), missing on both Newcastle and Arsenal fixtures.
- All 3 High-confidence picks that were correct (Liverpool, Leeds-City, Man Utd) were comfortable wins for the favourites.
