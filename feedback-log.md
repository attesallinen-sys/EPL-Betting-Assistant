# Agent Feedback Log

Items are appended by agents at the end of each run. Review periodically and either implement changes or move to the Archive section.

## Open

<!-- Agents append here. Format: -->
<!-- **[DATE] [AGENT] GW[XX]** [TAG] observation text. Suggested action (if any). -->

**[2026-03-03] Agent 2 GW29** [SOURCE] PredixSport only published 4/10 fixture predictions (Mar 3 matches only) at time of fetch. Consider fetching in two passes or running closer to kickoff.
**[2026-03-03] Agent 2 GW29** [SOURCE] Forebet timed out on 2 individual fixture pages (BHA-ARS, NEW-MUN). Main page loaded but individual pages unreliable.
**[2026-03-03] Agent 2 GW29** [SOURCE] Winning Arena returned no GW29 content. Site shows generic daily tips without gameweek structure. Consider retiring as P2 source.
**[2026-03-03] Agent 2 GW29** [SOURCE] Flashscore article for "Matchweek 29" was from a different season. Site does not tag articles by season. Consider retiring or improving search strategy.
**[2026-03-03] Agent 2 GW29** [SOURCE] BettingPros had not published Matchday 29 predictions as of morning of matchday. Publishes late.
**[2026-03-03] Agent 2 GW29** [DATA] Fulham vs West Ham had only 2 source predictions (below 3-source minimum). Limited source coverage for mid-table fixtures.
**[2026-03-10] Accuracy GW29** [ACCURACY] Consensus hit 2/10 (20%) -- worst recorded week. 6/10 fixtures produced upsets or unexpected draws. Unanimous picks (Wolves-Liverpool 5/5, Man City-Forest 3/3) both missed.
**[2026-03-10] Accuracy GW29** [ACCURACY] Forebet dropped to 33% cumulative (6/18) after a 1/8 week. Approaching the 40% review threshold after only 2 gameweeks.
**[2026-03-10] Accuracy GW29** [ACCURACY] Before You Bet at 20% cumulative (1/5). Small sample but trending poorly. Monitor over next 3 gameweeks.
**[2026-03-10] Accuracy GW29** [ACCURACY] xG contradiction flagged in the report for Tottenham vs Crystal Palace proved prescient -- Palace won 1-3. xG signals may deserve more weight in split/borderline picks.
**[2026-03-10] Accuracy GW29** [ACCURACY] Market outperformed consensus 4/10 vs 2/10. First gameweek with market data -- too early for conclusions but worth tracking.
**[2026-03-14] Agent 1 GW30** [DATA] xG source returned full season totals for all teams but no reliable last-5 xG trend split in fetchable output. Suggested action: add a secondary trend-specific xG source in `knowledge/sources.md`.
**[2026-03-14] Agent 2 GW30** [SOURCE] Sports Mole provided only Saturday fixture previews (5/10) in reliably fetchable form; Sunday/Monday previews were not consistently indexable at run time.
**[2026-03-14] Agent 2 GW30** [SOURCE] Before You Bet, Winning Arena, and BettingPros had no clearly usable GW30 pages available during this run.
**[2026-03-14] Agent 2 GW30** [SOURCE] Flashscore returned a "GW30" article tied to a mismatched fixture slate/season context; excluded from consensus to avoid data contamination.
**[2026-03-20] Accuracy GW30** [ACCURACY] Consensus 2/10 (20%) again; six draws and Chelsea 0-1 Newcastle (unanimous home wrong) dominated misses. Market 3/10; Forebet best source at 4/10.
**[2026-03-20] Accuracy GW30** [PROCESS] Split consensus (SUN-BHA) scored incorrect for headline accuracy; market Away favourite was right. Document if policy should credit directional lean.
**[2026-03-20] Agent 1 GW31** [DATA] Blank gameweek: 8 fixtures only; Arsenal, Man City, Crystal Palace, Wolves idle (EFL Cup final). Template/report flows should not assume 10 matches for GW31.
**[2026-03-20] Agent 1 GW31** [SOURCE] xgstat.com `WebFetch` timed out; xG table taken from search snippets with **P_xg=30 assumed** for normalization. Suggested action: re-fetch xG from FBref/Understat/StatMuse when extractable or add a resilient xG JSON endpoint to `knowledge/sources.md`.
**[2026-03-20] Agent 1 GW31** [SOURCE] Gambletron2000 fixture pages returned home/away win % only in fetch output; draw fair % imputed as remainder. Suggested action: confirm whether deeper page sections list explicit draw %.
**[2026-03-20] Agent 1 GW31** [SOURCE] StatMuse xG table URL did not yield a clean numeric table in automated fetch (navigation-heavy HTML).
**[2026-03-20] Agent 2 GW31** [SOURCE] Forebet Premier League page timed out; consensus used PredixSport + Bueon + Sports Mole (+ Goal.com once for Villa–West Ham).
**[2026-03-20] Agent 2 GW31** [DATA] PredixSport listed Man City–Crystal Palace (not on GW31 slate per Agent 1); that block excluded from extraction.
**[2026-03-20] Agent 2 GW31** [SOURCE] Sports Mole had no fetchable GW31 Villa–West Ham preview; Goal.com used as one-off fallback — consider adding to `knowledge/sources.md` if repeated.
**[2026-03-20] Agent 2 GW31** [DATA] Bueon returned 36%/28%/36% Home/Draw/Away for Tottenham–Forest (no 1X2 stance); recorded as “--” in Prediction Summary.

## Archive

<!-- Move resolved/dismissed items here with a short resolution note. -->
