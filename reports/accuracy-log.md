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
| Forebet | 5 | 10 | 50% | 1 |
| PredixSport | 7 | 10 | 70% | 1 |
| Bueon | -- | -- | -- | 0 |
| Sports Mole | -- | -- | -- | 0 |
| Winning Arena | 1 | 1 | 100% | 1 |
| Before You Bet | 1 | 3 | 33% | 1 |
| Radio Times | 5 | 10 | 50% | 1 |
| Flashscore | -- | -- | -- | 0 |
| BettingPros | -- | -- | -- | 0 |
| Action Network | -- | -- | -- | 0 |
| **Consensus** | 6 | 10 | 60% | 1 |
| **Market (odds favourite)** | -- | -- | -- | 0 |

---

## Confidence Tier Accuracy

Tracks how often predictions at each confidence tier are correct.

| Tier | Correct | Total | Accuracy | Notes |
|------|---------|-------|----------|-------|
| High | 3 | 4 | 75% | Wolves upset was the miss |
| Moderate | 2 | 4 | 50% | |
| Low | 1 | 2 | 50% | |

---

## Market vs. Consensus Comparison

Tracks whether the consensus or the market favourite was more often correct.

| Metric | Value |
|--------|-------|
| Gameweeks tracked | 1 |
| Consensus correct | 6/10 (60%) |
| Market favourite correct | N/A (no odds data for GW28) |
| Both agreed and correct | -- |
| Consensus correct, market wrong | -- |
| Market correct, consensus wrong | -- |

---

## Gameweek Results

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
