# Do Summer Tournaments Break the Premier League?

**Testing whether Premier League injury rates spike — and whether English clubs get worse in Europe — after major summer football tournaments (Euros, World Cup, Club World Cup).**

A self-contained data analytics portfolio project built entirely on free, publicly available sources.

---

## TL;DR

Tested against public data, with summer tournaments split by **scope** — how much of the league they touch: `league_wide` (Euro/World Cup), `regional` (Copa América only), `club_narrow` (Club World Cup), `none` (clean control):

| Claim | Verdict | Evidence |
|---|---|---|
| Summer tournaments cause a **league-wide injury spike** | ❌ Not at league level; ✅ real at player/club level | PL injury counts *fell* even after the 2024 *double* summer (Euro + Copa) and after the 2025 Club World Cup, but Chelsea (CWC winners) saw +44% and Man City the most post-tournament injuries of any European club |
| PL clubs **perform worse in Europe** after tournament summers | ❌ Rejected — no decline (though only a modest rise) | vs *genuinely clean* controls, England's UEFA coefficient averages **22.01** after league-wide tournaments vs **20.60** (a modest **+1.4**, not the +3.1 you get if you leave Copa seasons in the control group); the record coefficient (29.46) came after the Euro + Copa double summer of 2024 |
| A **narrow** tournament (Club World Cup) can degrade an individual club | ✅ Supported (club-level, domestic) | Chelsea fell from **4th + Champions League** (2024/25) to **8th + no Europe** (2025/26) after winning the CWC with no pre-season; Man City (shallower run) strained but did not collapse |

**Why scope matters — two ways:** (1) The Club World Cup touched only Chelsea and Man City, so pooling it into a league-level comparison is a category error (Arsenal and Aston Villa drove England's 2025/26 coefficient and weren't even in it) — analysed alone, it shows genuine club-level degradation. (2) Copa América ran in summer 2015 and 2019, so two seasons that looked like clean "controls" were actually mildly treated; removing them shrinks the apparent league-wide performance advantage from +3.1 to +1.4. Getting scope right strengthens one finding and honestly weakens another.

**The mechanism:** tournament fatigue is a *dose-dependent, player/club-level* risk. Spread across a league-wide tournament it is absorbed by squad depth; concentrated on one or two clubs by a narrow tournament, it becomes visible.

The only clean *league-wide* injury shock came from the **2022 *winter* World Cup**, which interrupted the season mid-campaign — a different mechanism that doesn't generalise to summer tournaments.

---

## Repository structure

| File | Description |
|---|---|
| `README.md` | This file — project overview & findings |
| `analysis.md` | Full write-up (exec summary → limitations) |
| `analysis.py` | Reproducible pandas analysis script |
| `pl_tournament_dataset.csv` | Season-level dataset, 2015/16–2025/26 |
| `data-schema.md` | Column dictionary & recommended schema |
| `linkedin-post.md` | Project summary written for a general audience |
| `requirements.txt` | Python dependencies (pandas) |
| `LICENSE` | MIT |

---

## Method in one paragraph

Seasons 2015/16–2025/26 are labelled by the *scope* of the summer tournament that preceded them — `league_wide` (Euro/World Cup), `regional_copa` (Copa América only), `club_narrow` (Club World Cup), `winter_control` (the 2022 World Cup), or `none`. European performance is measured with England's UEFA season coefficient (points across UCL/UEL/UECL per club) and English UCL/UEL finalist counts, sourced from kassiesa.net and football-coefficient.eu. Injury signals come from the Howden Men's European Football Injury Index and peer-reviewed UEFA Elite Club Injury Study work. The winter 2022 World Cup and the club-narrow Club World Cup are held out from the league-level comparison as separate cases. Because physical tracking data (GPS/optical load) is proprietary, workload is proxied by tournament-participation dose, recovery-window length, and fixture congestion — with the limitation stated explicitly.

## Reproduce

```bash
pip install -r requirements.txt
python analysis.py
```

Prints the scope-by-scope comparison and regenerates `pl_tournament_dataset.csv`.

---

## Key limitations (read before citing)

- No public exposure-adjusted (per-1,000-hour) PL injury rate exists; injury counts are sensitive to roster size and reporting completeness.
- No public physical-load tracking data — workload is proxied, not measured.
- Small n (11 seasons): findings are descriptive and directional, not significance-tested. Strength comes from consistency across the full window *and* a firm-source-only subset.
- Pre-2020/21 coefficient values are secondary-sourced and flagged approximate; conclusions hold without them.
- Club
