# Do Summer Tournaments Break the Premier League? Injuries and European Performance After Major Summer Football Tournaments

**A data-driven portfolio analysis of injury load and European competitiveness in English clubs following the Euros, World Cup, and Club World Cup.**

*Author: Jordan Florence · Last updated: July 2026*

---

## Executive Summary

Every summer that ends in a major international tournament, the same worry circulates through Premier League fanbases and press rooms: the players are coming back exhausted, the injuries will pile up, and English clubs will pay for it in Europe. This project tests that intuition against publicly available evidence.

The finding is more nuanced than the folklore. **The claim that summer tournaments trigger a league-wide injury spike is not well supported at the aggregate level, and the claim that Premier League clubs underperform in Europe afterwards is contradicted outright by the data.** Two effects that are real and well-documented get conflated with two effects that are not.

A critical distinction runs through the whole analysis: **not all summer tournaments are the same kind of treatment, and they differ in *scope* — how much of the Premier League they actually touch.** The Euros and World Cup are effectively *league-wide* shocks (nearly every club sends players). Copa América is an *intermediate, regional* shock (~25–35 PL players, mostly at a dozen clubs). The FIFA Club World Cup is a *narrow, club-level* shock (in 2025, just Chelsea and Manchester City). These must be analysed as different experiments, and doing so is what makes the results coherent. Copa also matters as a *confounder of the control group*: it ran in summer 2015 and 2019, so two seasons that look like clean "no-tournament" baselines were not.

What the evidence actually shows:

- **Injury risk after summer tournaments is a dose-response effect concentrated in the most-exposed players and clubs, not a uniform league-wide surge.** Chelsea, who played deepest into the 2025 Club World Cup, saw a 44% rise in injuries in the following months; Manchester City, also involved, recorded the most post-tournament injuries of any participating European club. Yet across Europe's top five leagues, the aggregate injury count in the months following that tournament actually *fell* versus the prior year, and Premier League injury counts have declined for four consecutive seasons.
- **The Club World Cup is the cleanest evidence that a summer tournament *can* degrade a club — precisely because it is isolated to a few clubs.** Chelsea, the winners, went from 4th (69 points, Champions League qualification) in 2024/25 to **8th and out of Europe entirely** in 2025/26, a decline widely attributed to injuries and Club World Cup fatigue after a near-zero pre-season. This is a genuine, measurable *club-level, domestic* effect — and it is a dose-response signal (Chelsea ran deepest and fell hardest; Manchester City, eliminated in the round of 16, showed injury strain but no comparable collapse), not a league-wide law.
- **The one unambiguous league-wide injury spike came from the 2022 *winter* World Cup — a fundamentally different mechanism.** Because it interrupted the domestic season rather than preceding it, players returned mid-campaign with no reconditioning window, and severity (days lost per injury) rose sharply. This is strong evidence *against* generalising to summer tournaments, not for it.
- **English clubs do not get worse in *European* competition after tournament summers.** Restricting the treatment to genuinely league-wide tournaments (Euros/World Cup), England's UEFA season coefficient averaged **22.01** versus **20.60 in truly clean control summers** — a positive but modest **+1.4** gap once Copa América is stripped out of the control group (the naïve gap of +3.1 was inflated by two Copa-affected "controls"). The decline hypothesis is firmly rejected; the strong "they get *much* better" version is not supported. The clinching data point: **2024/25 was a *double* tournament summer — Euro 2024 *and* Copa América 2024 — and still produced England's best coefficient on record (29.46).**

The through-line is that **Premier League squad depth and financial resources appear to absorb tournament fatigue faster than a fatigue-driven decline can set in — except where a single club's involvement is deep and its recovery window near-zero.** The clubs with the most players at league-wide tournaments are also the clubs with the deepest squads, so league-wide effects wash out. But the Club World Cup concentrates the entire dose on one or two clubs, and there the damage becomes visible (Chelsea). The portfolio-level takeaway for anyone modelling this: treat "summer tournament" as a *player-level and club-level* workload variable with a dose-response gradient and a *scope* dimension (how much of the league it touches), not a *league-level* switch that flips performance downward.

*Note on scope: physical tracking metrics (GPS distance, high-speed running, accelerations) are proprietary and not publicly available. This analysis uses defensible public proxies — documented injury counts and costs, fixture-congestion research, and UEFA coefficients — and flags every limitation explicitly.*

---

## 1. Research Question and Hypotheses

### Primary research questions

1. **Injury question:** Do Premier League injury rates spike in the season *following* a major summer tournament (European Championship, FIFA World Cup, FIFA Club World Cup), relative to seasons following a normal summer?
2. **Performance question:** Do Premier League clubs perform *worse* in UEFA European competitions in the season following a major summer tournament?

### Hypotheses

- **H1 (injury spike):** Summer-tournament seasons show elevated Premier League injury incidence and/or severity versus non-tournament seasons.
- **H2 (European decline):** English clubs' UEFA performance (season coefficient and finalist count) is lower in tournament-following seasons.
- **H0 (null / competing explanation):** Any observed effects are driven by fixture congestion and individual player workload generally — not by summer tournaments specifically — and are absorbed at club level by squad depth.

### Why the framing matters

The popular version of this argument treats "the tournament" as the cause and "the league" as the unit of effect. The sports-medicine literature treats *accumulated match exposure and inadequate recovery windows* as the cause, and the *individual player* as the unit of effect. These are not the same claim, and separating them is the analytical core of this project.

---

## 2. Data Sources

All sources used are free or publicly accessible. No paywalled or proprietary tracking data was used.

### Source-by-source assessment

**Howden Men's European Football Injury Index (2021/22–2024/25 editions)**
- *Contributes:* Season-level injury counts and salary-cost estimates for the Premier League and Europe's top five leagues; a dedicated 2025 chapter on the Club World Cup's injury impact; club-level breakdowns.
- *Pros:* The most comprehensive public, longitudinal, cross-league injury dataset available for free; consistent methodology year to year; explicitly analyses tournament effects.
- *Cons:* "Injury" is operationalised partly through *cost* (salary paid while injured), which is confounded by wage inflation and squad value; produced by an insurance broker, so framed around financial risk; underlying player-level data is not released.

**UEFA Elite Club Injury Study (ECIS) subanalysis of the 2022/23 World Cup season (Ekstrand et al., *BJSM*, 2025)**
- *Contributes:* A peer-reviewed, methodologically rigorous read on whether the winter World Cup season changed injury incidence in elite European clubs.
- *Pros:* Gold-standard prospective injury surveillance (medical-staff recorded, exposure-adjusted per 1,000 hours); directly on-topic.
- *Cons:* Covers the *winter* 2022 World Cup, not a summer tournament; sample is elite clubs, not all Premier League clubs.

**Ekstrand, Waldén & Hägglund, "A congested football calendar and the wellbeing of players" (*BJSM*, 2004)**
- *Contributes:* The foundational quantitative link between pre-tournament match exposure and injury/underperformance *during* the World Cup 2002.
- *Pros:* Peer-reviewed; establishes the dose-response logic this whole question rests on.
- *Cons:* Measures effects *during* the tournament, not in the following club season; dated squad-management context.

**Independent peer-reviewed study on the 2022 winter World Cup and first-division injury rates (2024–25)**
- *Contributes:* External corroboration that the winter World Cup increased injury rates/severity in top European leagues, with the Premier League most affected (23.6% of players at the tournament).
- *Pros:* Independent replication of the ECIS-adjacent finding; league-specific detail.
- *Cons:* Again winter-specific; media-reported effect sizes require care.

**kassiesa.net UEFA coefficient database & football-coefficient.eu**
- *Contributes:* Season-by-season UEFA country (association) coefficients for England, 2020/21–2025/26, with firm sourcing.
- *Pros:* Transparent, reproducible calculation matching UEFA's official method (points per club across UCL/UEL/UECL); free and complete.
- *Cons:* A season coefficient is a *team-strength-in-Europe* proxy, not a fatigue measure; earlier seasons (pre-2020/21) rely on widely published secondary values and are flagged as approximate here.

**Premier Injuries / PhysioRoom / club injury tables (contextual)**
- *Contributes:* Real-time and historical club injury lists for qualitative cross-checks.
- *Cons:* Crowd/press-sourced, inconsistent injury definitions, not suitable as a primary quantitative spine — used only for context.

### What no free source provides

There is **no public, season-level, exposure-adjusted (per-1,000-hour) Premier League injury rate series** and **no public physical-load tracking data** (GPS/optical distance, sprint counts, accelerations). This is the central data limitation of the project and is addressed with proxies in Section 4.

---

## 3. Tournament Timeline and Study Windows

### Summer tournaments in scope (2015–2025)

The single most important design choice in this project is classifying tournaments by **scope** — how much of the Premier League they actually treat — not just by whether they happened.

| Summer | Tournament(s) | Scope | Season it precedes | Mechanism |
|---|---|---|---|---|
| 2015 | Copa América 2015 | **Regional** (~South-American PL players only) | 2015/16 | Shortened pre-season for involved players |
| 2016 | UEFA Euro 2016 **+ Copa América Centenario** | **League-wide** (double: European + S-American) | 2016/17 | Shortened pre-season for involved players |
| 2018 | FIFA World Cup 2018 | **League-wide** | 2018/19 | Shortened pre-season for involved players |
| 2019 | Copa América 2019 | **Regional** | 2019/20 | Shortened pre-season for involved players |
| 2021 | UEFA Euro 2020 (played 2021) **+ Copa América 2021** | **League-wide** (double) | 2021/22 | Shortened pre-season for involved players |
| 2022 | FIFA World Cup 2022 | League-wide but **winter** | 2022/23 (mid-season) | **Mid-season interruption — different mechanism** |
| 2024 | UEFA Euro 2024 **+ Copa América 2024** | **League-wide** (double; both finals 14 Jul) | 2024/25 | Shortened pre-season for involved players |
| 2025 | FIFA Club World Cup 2025 | **Club-narrow** (only Chelsea & Man City) | 2025/26 | Near-zero recovery for finalists (final 13 Jul) |

**Truly clean (no-tournament) summers**, used as the control group: 2017/18, 2020/21 (both Euro and Copa were postponed out of summer 2020 by COVID), and 2023/24. The summers of 2015 and 2019 are *not* clean — they held a standalone Copa América — so they form a separate **regional** category rather than sitting in the control group.

### Where Copa América fits

Copa América runs in June–July, exactly overlapping the European window. It is included as a distinct scope tier because its Premier League footprint is real but smaller than the Euros': the 2024 edition drew roughly 25–35 PL players (Argentina alone sent eight — Martínez, Enzo Fernández, Mac Allister, Álvarez, Garnacho, L. Martínez, Lo Celso, Romero), spread across a dozen-odd clubs. Two consequences follow. First, the Euro summers of 2016, 2021 and 2024 were actually *double* tournament summers, raising — not lowering — their treatment intensity. Second, and more importantly for rigor, Copa 2015 and 2019 mean two apparent "control" seasons were mildly treated, so they are separated out to keep the control group genuinely clean.

### Why the Club World Cup is *not* pooled into the league-level comparison

The Euros and World Cup pull players from across the league — roughly a quarter of Premier League players were at the 2022 World Cup, spread over most clubs. A league-level metric like the England UEFA coefficient is therefore a *fair* outcome to test them against: the treatment touches the whole population the metric measures.

The 2025 Club World Cup did not. Only **two** English clubs took part, and neither Arsenal (2025/26 Champions League finalists) nor Aston Villa (2025/26 Europa League winners) — the clubs that actually drove England's strong 2025/26 coefficient — was among them. Counting 2025/26 as a "tournament-recovery season" and crediting its high coefficient to tournament resilience would be a category error: **the clubs that lifted the coefficient were never exposed to the treatment.** The Club World Cup is therefore removed from the league-level performance comparison and analysed as a **club-level natural experiment** (Section 5.3), which is where its effect genuinely lives — and where it turns out to be real.

### Why the 2022 World Cup is also analysed separately

The 2022 tournament sat *inside* the 2022/23 domestic season (November–December). Its documented injury effect operates through a mid-season interruption and abrupt return, not through a compressed pre-season. Pooling it with summer tournaments would contaminate the comparison, so it is treated as a **mechanistic control case** rather than a member of the "summer tournament" group.

---

## 4. Methodology

### 4.1 Pre/post comparison design

The design is a **season-level natural experiment**: each season is labelled by the *scope* of the summer tournament that preceded it — `league_wide` (Euro/World Cup), `regional` (Copa América only), `club_narrow` (Club World Cup), `winter_control` (the 2022 World Cup), or `none` (clean control) — and outcome means are compared across these tiers rather than through a single tournament-vs-not binary. Because tournaments recur on a fixed international calendar, the assignment is exogenous to any single club's decisions, which strengthens causal interpretation relative to a within-club comparison. Using graded scope instead of a binary is what surfaces the two effects a binary hides: the Club World Cup's club-level damage, and Copa América's contamination of the control group.

Two robustness moves are built in:
1. **Full-window analysis** (2015/16–2025/26, 11 seasons) for historical comparability.
2. **Firm-source sensitivity analysis** (2020/21–2025/26) using only coefficient values with primary sourcing.

### 4.2 Injury definition

Because no free exposure-adjusted rate exists, injury is operationalised on three complementary public measures, each flagged for its confound:

- **Injury count** — number of recorded injury incidents per season (Howden). *Confound: roster size, reporting completeness.*
- **Injury severity** — average days lost per injury (ECIS / winter-WC studies). *The cleanest available severity proxy.*
- **Injury cost** — salary paid to injured players (Howden). *Confound: wage inflation, squad value; used directionally only.*

The **preferred internal metric is severity (days lost)**, because it is least sensitive to roster size and reporting drift.

### 4.3 Performance definition

Two public, historically comparable measures:

- **England UEFA season coefficient** — total UCL + UEL + UECL points earned by all English clubs that season, divided by the number of English entrants. This is the standard, method-consistent measure of how English clubs performed in Europe in a given season.
- **English UCL/UEL finalist count** — number of English clubs reaching a Champions League or Europa League final that season. A blunt but unambiguous "deep run" indicator.

### 4.4 Workload and physical-proxy variables

Direct physical tracking is unavailable, so workload is proxied by:

- **Tournament participation dose** — share of a club's/league's players active at the summer tournament (Howden reports ~23.6% of PL players at World Cup 2022 as a benchmark).
- **Recovery-window length** — days between a player's final tournament match and the start of pre-season/competitive football (near-zero for 2025 Club World Cup finalists; ~3–4 weeks for typical Euro/WC involvement).
- **Fixture congestion** — matches per week in the run-up, drawing on the Bengtsson/Ekstrand congestion literature (muscle-injury rates rise measurably when recovery between matches drops below ~4–6 days).

These proxies are explicitly *indirect*. The limitation is stated plainly: **we are inferring physical load from schedule structure and outcomes, not measuring it.**

---

## 5. Analysis

### 5.1 Injuries: a concentrated dose-response effect, not a league-wide spike

The strongest, cleanest injury signal in the public record comes from the **2022 winter World Cup**, which is the wrong tournament type for the summer hypothesis. Peer-reviewed and independent analyses agree it raised injury severity across the top five leagues, with the Premier League most exposed; one widely reported figure shows average days-lost per injury roughly **doubling** from the pre-tournament to the post-tournament phase of that season, adding an estimated ~8 days to the average absence in the second half. The mechanism — abrupt mid-season return with no reconditioning — does not transfer to summer tournaments.

Notably, the **UEFA Elite Club Injury Study subanalysis found *no* major change in overall injury incidence in elite European club football across the 2022/23 World Cup season** when measured on an exposure-adjusted basis. Even for the mid-season disruption, the effect showed up in *severity and specific injury types*, not a blanket rise in incidence.

For **summer** tournaments, the aggregate picture is muted:

- After **Euro 2024 *and* Copa América 2024** — a double summer tournament stacking European and South-American load onto the league — Premier League injury *counts still fell*, to 958 in 2024/25 from 986 in 2023/24, the fourth consecutive annual decline. Across the top five leagues the count rose only marginally (+27). A genuine league-wide fatigue shock should have been most visible in exactly this double-tournament summer; it was not.
- After the **2025 Club World Cup**, the nine participating top-five-league clubs recorded **25 injuries during June–July 2025 — identical to the same window a year earlier** — and combined injuries in the three months after were *lower* than the prior year for that period.

But the *club-level* signal is real and follows a dose gradient:

- **Chelsea**, Club World Cup winners with essentially no pre-season, saw a **+44% rise in injuries** in the following months and a visibly depleted defensive unit by mid-season.
- **Manchester City**, also involved, recorded **22 injuries** in August–October 2025, the most of any participating European club.

This is the pattern the 2004 Ekstrand study predicts: **the players and clubs with the highest accumulated exposure and the shortest recovery carry the risk.** In 2002, players who had played more than one match per week in the ten weeks before the World Cup were far more likely to be injured or to underperform. The effect is dose-dependent and individual — which is exactly why it does not show up cleanly when averaged across an entire league of 20 clubs, most of whom send few or no players deep into a tournament.

### 5.2 European performance: no decline after tournament summers — but the "improvement" is modest once Copa is controlled

Breaking the seasons out by scope (excluding the club-narrow Club World Cup and the winter-WC control, both handled separately):

| Scope group | n | Seasons | Mean England season coefficient |
|---|---|---|---|
| **League-wide** (Euro/WC, incl. double Euro+Copa summers) | 4 | 2016/17, 2018/19, 2021/22, 2024/25 | **22.01** |
| **Clean control** (no summer tournament at all) | 3 | 2017/18, 2020/21, 2023/24 | **20.60** |
| **Regional (Copa América only)** | 2 | 2015/16, 2019/20 | **16.41** |

The reclassification matters, and it cuts against the strong version of my earlier claim. When Copa América is left inside the control group (as it implicitly was before), the control mean is dragged down to 18.93 and the league-wide advantage looks like a decisive **+3.08**. But two of those "controls" (2015/16, 2019/20) actually had a Copa and were weak English-in-Europe seasons. **Against genuinely clean controls, the league-wide advantage is only +1.41** — positive, but modest and small-n.

So the honest reading of the European-performance question is:

- **The decline hypothesis (H2) is firmly rejected.** In no tournament category do English clubs underperform clean controls; the league-wide group is *higher*, not lower.
- **The stronger claim that they clearly *improve* is not well supported.** A +1.4 coefficient gap across 4 vs 3 seasons is directionally consistent but not decisive.
- **The most robust single fact points the same way:** 2024/25 was a *double* tournament summer (Euro 2024 + Copa América 2024) and still delivered **England's best coefficient on record (29.46)** — Tottenham winning the Europa League, Chelsea the Conference League, Arsenal to the Champions League semi-finals. If double-tournament fatigue degraded English clubs, this is the season it should have shown; instead it was the peak.

*(One caveat in the other direction: the regional-Copa seasons are the lowest of any group at 16.41. This is almost certainly not a Copa effect — n=2, and 2015/16 and 2019/20 were simply lean years for English clubs in Europe with no finalists — but it is flagged rather than spun, because with this little data a low number should not be over-read either way.)*

Sensitivity check on firm-sourced seasons only (2020/21–2025/26): league-wide summers (2021/22, 2024/25) average **25.23** versus the clean control 2020/21 (24.36) and 2023/24 (17.38) — direction unchanged, still no decline.

### 5.3 The Club World Cup: a club-level natural experiment where the effect *is* real

The Club World Cup is the exception that proves the rule — and the reason the reclassification matters. Because it concentrated an entire summer's tournament load onto just two English clubs, it functions as an unusually clean club-level natural experiment, free of the league-wide averaging that masks fatigue effects elsewhere. And here the fatigue narrative holds.

**Chelsea (winners — the maximum dose).** Chelsea played to the final on 13 July 2025, returning with essentially no pre-season. The consequences were visible across the campaign:

| Chelsea | 2024/25 (pre-CWC) | 2025/26 (post-CWC) |
|---|---|---|
| Premier League finish | **4th** | **8th** |
| Points | 69 | Faded from title contention (2 pts from final 3 games) |
| European qualification | Champions League | **None** |
| Injuries (months after summer) | baseline | **+44%** |
| Matches played | — | 38+ (among the most of any club) |

Chelsea were installed as shortened title contenders (backed from 16-1 to 8-1) after winning the trophy, then slid to 8th and out of Europe entirely — a decline consistently attributed by analysts to the combination of injuries, fixture load, and the absent pre-season that the Club World Cup imposed.

**Manchester City (round of 16 — a smaller dose).** City exited earlier and returned sooner. They still showed injury strain — 22 injuries in August–October 2025, the most of any participating European club — but suffered no comparable domestic collapse. Less tournament exposure, less damage: the dose-response gradient in miniature, within a single tournament, across two clubs.

This is the strongest single piece of evidence in the project *for* a tournament effect. It is also, crucially, **a club-level and domestic effect, not a league-level or European one** — exactly the scope at which the mechanism should operate.

### 5.4 Reconciling the findings

The resolution is straightforward once two things are fixed: the **unit of analysis** and the **scope of the treatment.**

Tournament fatigue is a **player-level and club-level risk that concentrates in heavily-used squads with short recovery windows.** For *league-wide* tournaments, that dose is spread thinly across most of the league, and it lands hardest on exactly the elite clubs with the **deepest squads and largest budgets** — the clubs best equipped to rotate, reinforce, and manage load, and the clubs that carry English performance in Europe. So the effect washes out of any league-level metric.

The *Club World Cup* breaks that averaging. It dumps the entire dose on one or two clubs, and for the club that ran deepest with no recovery (Chelsea), the damage surfaces clearly — in the domestic table, not the European coefficient. That is why **H1 (injury risk) holds at the player/club level, H2 (European decline) fails at the league level, and the one clean club-level case of degradation shows up in domestic rather than European performance.** All three are consistent once scope and unit are respected.

---

## 6. Results and Conclusions

1. **No league-wide summer-tournament injury spike is evident in public data.** Premier League injury counts declined after both Euro 2024 and the 2025 Club World Cup. (H1 rejected at league level.)
2. **A real, dose-dependent injury effect exists at the individual/club level** for the most-exposed players and deepest-running clubs (Chelsea +44%, Manchester City's post-CWC total). (H1 supported at player/club level.)
3. **The Club World Cup produced the clearest single case of tournament-driven degradation — at club level, in domestic performance.** Chelsea, the winners, fell from 4th and Champions League qualification to 8th and no European football, with Manchester City (a shallower run) showing strain but no collapse. Because the tournament was isolated to two clubs, this is the cleanest available club-level natural experiment, and it supports the fatigue mechanism where scope predicts it should.
4. **The only clear league-wide injury shock came from the 2022 *winter* World Cup**, via a distinct mid-season-interruption mechanism that does not generalise to summer tournaments — and even then it manifested as increased *severity*, not incidence.
5. **English clubs do not underperform in *Europe* after tournament summers.** Against genuinely clean controls (Copa América seasons removed), league-wide tournament summers average **+1.4** coefficient points — no decline, though the improvement is modest, not the +3.1 that appears when Copa-affected seasons are wrongly counted as controls. The decline hypothesis is rejected; England's record coefficient (2024/25) came after a *double* Euro-plus-Copa summer. (H2 rejected.)
6. **Squad depth and treatment scope are the moderators.** The competing explanation (H0) — that risk is about individual/club workload and is absorbed at club level by resources for league-wide tournaments, but concentrates and becomes visible when a tournament touches only a few clubs — fits the full evidence best.

**Bottom line:** the "summer tournaments break the Premier League" narrative is half-true in a way that matters, and the half that is true depends on *scope*. Squad-wide tournaments (Euros, World Cup) stress individual players but do not measurably weaken the league's injury profile in aggregate or blunt English clubs' European competitiveness — if anything, the seasons after big summers have been English football's best in Europe. A *narrow* tournament like the Club World Cup, which dumps the entire load on one or two clubs, genuinely can degrade them — as Chelsea's fall from 4th to 8th and out of Europe demonstrates. The lesson for analysts and clubs alike is to stop asking whether "tournaments" hurt the league and start asking *which clubs, how deep, and how much recovery.*

---

## 7. Limitations and Caveats

- **No physical tracking data.** GPS/optical load metrics are proprietary. All workload claims rest on schedule-structure proxies and outcome data. This is the single largest limitation.
- **No public exposure-adjusted PL injury rate.** Injury counts are not normalised per 1,000 player-hours, so they are sensitive to roster size and reporting completeness. Severity (days lost) is the cleaner metric and is used where available.
- **Cost as an injury proxy is confounded** by wage inflation and squad value; it is used only directionally.
- **Small season-level n.** Eleven seasons, five per group, means the coefficient comparison is descriptive, not inferentially powerful — no significance test is claimed. The finding's strength comes from *direction and consistency* (including a same-direction firm-source subset), not statistical power.
- **Coefficient is a performance proxy, not a fatigue measure,** and it is dominated by a few elite clubs; it says little about mid-table clubs.
- **Pre-2020/21 coefficient values are secondary-sourced** and flagged as approximate; the core conclusion holds even when they are dropped.
- **Selection/correlation confound:** clubs sending the most players to tournaments are also the strongest clubs, which both creates the injury risk and supplies the resources that mask it. This is discussed as a feature of the finding, not controlled away.
- **Survivorship in the injury literature:** players who stay fit under high load may be inherently more resilient, biasing "no effect" findings.
- **Scope tiers rest on small samples.** With only 3 clean-control and 2 regional-Copa seasons, the coefficient contrasts are illustrative, not inferential — the +1.4 league-wide advantage and the low regional-Copa mean could both shift materially with one more season. The robust claims are the *directional* ones (no decline) and the individual-season facts (record coefficient after a double-tournament summer), not the precise gaps.
- **Copa América exposure is approximated, not measured per club.** PL participation counts are from squad lists; the tournament is treated as a single regional-scope layer rather than modelled club-by-club, which a fuller build should do.
- **The Club World Cup case is n=2 clubs, one tournament.** Chelsea's domestic decline is a compelling, well-attributed signal, but it is a single instance and is confounded by non-fatigue factors (a young squad in transition, disciplinary issues, a managerial change). It should be read as a strong illustrative natural experiment, not a proven general law — the club-level effect will only be confirmable once several editions of the expanded Club World Cup have been played.

---

## 8. Reproducibility

The season-level dataset (`pl_tournament_dataset.csv`) and analysis script (`analysis.py`) are included. The analysis is fully reproducible with Python and pandas; every coefficient value is traceable to kassiesa.net or football-coefficient.eu, and every injury figure to the Howden Index or a cited peer-reviewed study.

---

## Sources

- [Howden — Men's European Football Injury Index 2024/25](https://www.howdengroup.com/au-en/reports/mens-european-football-injury-index-202425)
- [Chelsea injuries up 44% after Club World Cup — Washington Times](https://www.washingtontimes.com/news/2025/dec/16/chelsea-injuries-44-club-world-cup/)
- [How injuries, ill discipline and Club World Cup fatigue derailed Chelsea's title hopes — Racing Post](https://www.racingpost.com/sport/opinion/how-injuries-ill-discipline-and-club-world-cup-fatigue-have-derailed-chelseas-title-hopes-aJK2Z2W3CBNQ/)
- [2024–25 Chelsea F.C. season (finished 4th, CL qualification) — Wikipedia](https://en.wikipedia.org/wiki/2024%E2%80%9325_Chelsea_F.C._season)
- [2025–26 Premier League final table — Wikipedia](https://en.wikipedia.org/wiki/2025%E2%80%9326_Premier_League)
- [No major changes in injury incidence during the 2022/23 World Cup season — UEFA Elite Club Injury Study subanalysis (PMC)](https://pmc.ncbi.nlm.nih.gov/articles/PMC12406901/)
- [A Winter World Cup Interrupted Season Increased Injury Rates in First Division European Soccer Leagues (AOAO)](https://aoao.org/2025/07/31/a-winter-world-cup-interrupted-season-increased-injury-rates-in-first-division-european-soccer-leagues/)
- [2022 winter World Cup increased severity of injuries — study (ESPN)](https://www.espn.com/soccer/story/_/id/38939319/2022-winter-world-cup-increased-severity-injuries-study)
- [Ekstrand, Waldén & Hägglund (2004): A congested football calendar and the wellbeing of players (PubMed)](https://pubmed.ncbi.nlm.nih.gov/15273193/)
- [Bengtsson/Ekstrand: Muscle injury rates increase with fixture congestion (UEFA Champions League injury study)](https://www.researchgate.net/publication/249319881_Muscle_injury_rates_in_professional_football_increase_with_fixture_congestion_An_11-year_follow-up_of_the_UEFA_Champions_League_injury_study)
- [UEFA Country Ranking 2025 — kassiesa.net](https://kassiesa.net/uefa/data/method5/crank2025.html)
- [England country coefficient by season — football-coefficient.eu](https://www.football-coefficient.eu/country/3-england/)
- [English football clubs in international competitions — Wikipedia](https://en.wikipedia.org/wiki/English_football_clubs_in_international_competitions)
- [2024 Copa América (dates, USA, 20 Jun–14 Jul) — Wikipedia](https://en.wikipedia.org/wiki/2024_Copa_Am%C3%A9rica)
- [Premier League players appearing at Copa América 2024 by club — PremierLeague.com](https://www.premierleague.com/en/news/4036668)
- [Copa América editions and history — Wikipedia](https://en.wikipedia.org/wiki/Copa_Am%C3%A9rica)

---

*This is an independent analytical portfolio project. It uses only free/public data and clearly flags every proxy and limitation. It is not affiliated with the Premier League, UEFA, FIFA, Howden, or any club.*
