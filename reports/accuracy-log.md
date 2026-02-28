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
| Forebet | -- | -- | -- | 0 |
| PredixSport | -- | -- | -- | 0 |
| Bueon | -- | -- | -- | 0 |
| Sports Mole | -- | -- | -- | 0 |
| Winning Arena | -- | -- | -- | 0 |
| Before You Bet | -- | -- | -- | 0 |
| Flashscore | -- | -- | -- | 0 |
| BettingPros | -- | -- | -- | 0 |
| Action Network | -- | -- | -- | 0 |
| **Consensus** | -- | -- | -- | 0 |
| **Market (odds favourite)** | -- | -- | -- | 0 |

---

## Confidence Tier Accuracy

Tracks how often predictions at each confidence tier are correct.

| Tier | Correct | Total | Accuracy | Notes |
|------|---------|-------|----------|-------|
| High | -- | -- | -- | |
| Moderate | -- | -- | -- | |
| Low | -- | -- | -- | |

---

## Market vs. Consensus Comparison

Tracks whether the consensus or the market favourite was more often correct.

| Metric | Value |
|--------|-------|
| Gameweeks tracked | 0 |
| Consensus correct | -- |
| Market favourite correct | -- |
| Both agreed and correct | -- |
| Consensus correct, market wrong | -- |
| Market correct, consensus wrong | -- |

---

## Gameweek Results

<!-- Add a new block below for each gameweek after results are in. -->
<!-- Template:

### Gameweek XX (YYYY-MM-DD)

| # | Home | Away | Actual Result | Consensus | Correct? | Market Fav | Market Correct? |
|---|------|------|--------------|-----------|----------|-----------|----------------|
| 1 | | | | | | | |

**Per-source accuracy this gameweek**:

| Source | Predictions Made | Correct | Accuracy |
|--------|-----------------|---------|----------|
| Forebet | | | |
| PredixSport | | | |
| ... | | | |

**Confidence tier accuracy this gameweek**:

| Tier | Correct | Total | Accuracy |
|------|---------|-------|----------|
| High | | | |
| Moderate | | | |
| Low | | | |

**Consensus accuracy**: X/10 (XX%)
**Market favourite accuracy**: X/10 (XX%)

-->
