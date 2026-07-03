# Dataset Schema — `pl_tournament_dataset.csv`

Season-level dataset, one row per Premier League season, 2015/16–2025/26.

## Columns (as shipped)

| Column | Type | Description | Source / notes |
|---|---|---|---|
| `season` | string | Season label, e.g. `2024/25` | — |
| `preceding_tournament` | string | Major tournament in the summer before the season, or `None` | — |
| `tournament_scope` | string | `league_wide` (Euro/WC) / `regional_copa` (Copa América only) / `club_narrow` (Club World Cup) / `winter_control` (WC 2022) / `none` | **The key classification variable** |
| `copa_america_flag` | int (0/1) | 1 if a Copa América edition ran that summer (2015, 2016, 2019, 2021, 2024) | Independent exposure layer; note the overlap with Euro summers |
| `eng_season_coeff` | float | England UEFA season country coefficient (UCL+UEL+UECL points ÷ clubs) | kassiesa.net / football-coefficient.eu; 2020/21–2025/26 firm |
| `coeff_source` | string | `firm` (primary-sourced) or `approx` (secondary) | Pre-2020/21 = approx |
| `eng_ucl_uel_finalists` | int | English clubs reaching a UCL or UEL **final** that season | Wikipedia / UEFA |
| `league_treatment_flag` | int (0/1) | 1 only if a **squad-wide** tournament (Euro/WC) preceded the season; Copa-only, Club World Cup and Winter WC coded 0 and analysed separately | Derived from `tournament_scope` |

**Why `tournament_scope` matters:** only `league_wide` tournaments are pooled into the league-level European-performance comparison. The `regional_copa` seasons (Copa América only) are held separate because Copa touches ~25–35 PL players — enough to disqualify a season as a clean control but not to make it a league-wide treatment. The `club_narrow` Club World Cup is analysed as a club-level natural experiment (it touched only 2 PL clubs), and the `winter_control` 2022 World Cup is held out for its distinct mid-season mechanism. Collapsing these into one binary flag is the modelling error this schema is designed to prevent — it is exactly what would put Copa-affected 2015/16 and 2019/20 into the control group and inflate the measured tournament effect.

## Recommended extended schema (for a fuller build)

If extending this project with more granular data, these columns are recommended:

| Column | Type | Description | Best free proxy if unavailable |
|---|---|---|---|
| `season` | string | Season key | — |
| `tournament_flag` | int | Summer tournament preceded season | — |
| `tournament_scope` | string | league_wide / regional_copa / club_narrow / winter_control / none | — |
| `copa_america_flag` | int | Copa América ran that summer | Wikipedia |
| `tournament_recovery_days` | int | Days from tournament end to season start | Calendar arithmetic (public fixtures) |
| `pl_players_at_tournament` | int | PL players active at the tournament(s) — sum across Euro/WC + Copa | Squad lists (public) |
| `pl_players_at_tournament_pct` | float | Share of PL players involved | Howden benchmark (~23.6% for WC 2022) |
| `pl_injury_count` | int | Recorded PL injuries in season | Howden Injury Index |
| `pl_injury_cost_gbp_m` | float | Salary cost of injuries (£m) | Howden Injury Index (confounded by wages) |
| `pl_avg_days_lost` | float | Mean days lost per injury (severity) | ECIS / press-reported |
| `eng_season_coeff` | float | UEFA season coefficient | kassiesa.net |
| `eng_ucl_uel_finalists` | int | English UCL/UEL finalists | UEFA / Wikipedia |
| `eng_clubs_in_ucl_ko` | int | English clubs reaching UCL knockouts | UEFA |
| `pl_champion_pts` | int | Title-winner points (context) | Premier League |
| `fixture_congestion_index` | float | Matches per available day, congested windows | Derived from public fixtures |
| `coeff_source` | string | firm / approx | Provenance flag |

## Data-quality flags to carry

- `coeff_source` — always distinguish primary vs secondary sourcing.
- Any injury column should carry a `_definition` note (count vs cost vs severity are **not** interchangeable).
- Mark the 2022/23 row explicitly as the winter-WC control so it is never silently pooled with summer tournaments.
