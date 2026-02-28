# Future Improvements

Improvements to implement after the Priority 1 foundation (accuracy tracking, odds integration, weighted consensus) is established and has accumulated data over several gameweeks.

---

## Priority 2: High Impact, Moderate Effort

### ~~Raw Statistical Data (xG) as an Independent Signal~~ -- IMPLEMENTED

Implemented. Agent 1 now fetches xG data (xG, xGA, xGD) from FBref/Understat via WebSearch and calculates overperformance vs. actual goals. Agent 2 uses this as an independent signal to flag regression risks and cross-check the consensus. See `tasks/fetch-matchweek-data.md` Phase 2.5 and `tasks/matchweek-predictions.md` Phase 3 xG analysis.

### Value Betting Analysis (Edge Calculation)

The current "Value Picks" section highlights high-confidence predictions, not good-value bets. True value = your estimated probability exceeds the implied probability from odds.

- After odds integration (P1) is working, add a calculation: `Edge = Consensus Probability - Implied Probability from Odds`.
- Positive edge means the consensus thinks the outcome is more likely than the market does -- this is where betting value exists.
- Replace or supplement the "Value Picks" section with a "Value Bets" section ranking fixtures by edge.
- Add expected value (EV) to accumulator ideas: `EV = (Consensus Probability x Potential Payout) - Stake`.

### Systematic Injury and Team News Collection

The current system picks up injuries mentioned by prediction sources, but doesn't proactively fetch team news. Late-breaking injuries can significantly shift probabilities.

- Add a dedicated team news step in Agent 1 using sources like BBC Sport team pages, premierleague.com news, or Transfermarkt injury lists.
- For each fixture, record: confirmed absences, doubtful players, and returning players.
- When a key player absence is not yet reflected in prediction sources (published days before), note it as a potential consensus-adjustment factor.
- Add a team news section to Agent 1's data file template.

---

## Priority 3: Structural / Longer-term

### Source Disagreement Pattern Analysis

When sources disagree, the report flags it as a "Split Decision." But some disagreement patterns may be informative.

- After accumulating accuracy data, analyze: when a specific source disagrees with the consensus, is it right more often or less often? (Some sources may be good contrarian indicators.)
- Track: when the consensus is split 3-2, how often does the majority win vs. the minority? By confidence tier?
- Add this meta-analysis to `reports/accuracy-log.md` as a "Patterns" section.

### Elo / Power Ratings as an Independent Model

Prediction sites tend to over-index on recent form and under-index on underlying team quality. An Elo-style rating system provides a stable baseline that smooths out noise.

- Maintain a simple Elo rating for each team in `knowledge/elo-ratings.md`, updated after each gameweek.
- Use the Elo difference between teams as an independent prediction signal (Elo difference maps to expected win probability via a standard formula).
- Compare Elo-based probability to source consensus -- divergences are analytically interesting.

### Context-Conditioned Analysis

Not all matches are created equal. Prediction accuracy varies by context: derbies, relegation six-pointers, dead rubbers, and midweek European congestion all create systematic biases.

- Tag each fixture with context labels: "derby," "relegation battle," "top-6 clash," "European congestion," "nothing to play for."
- Over time, track accuracy by context label.
- Add context-specific adjustments to reasoning: e.g., "Draw probability increases ~8% in top-6 derbies historically."

### Two-Pass Timing Strategy

Predictions fetched on Tuesday differ in accuracy from those fetched on Saturday morning. Late team news substantially shifts probabilities.

- Formalize the existing two-agent split into a timing strategy:
  - **Early pass** (Wednesday/Thursday): Agent 1 fetches fixtures, league table, odds, and algorithmic predictions (Forebet, PredixSport, Bueon).
  - **Late pass** (Friday evening/Saturday morning): Agent 2 fetches editorial predictions (Sports Mole, Before You Bet) and updates with late team news.
- The final report merges both passes, noting which data is early vs. late.
