import pandas as pd
from pathlib import Path

# Resolve data path relative to this script so it works from any working dir
DATA_PATH = Path(__file__).resolve().parent.parent / "data" / "pl_tournament_dataset.csv"

# Season-level dataset. eng_season_coeff = England UEFA season country coefficient
# (sum of English clubs' UCL+UEL+UECL points / number of English clubs).
# Firm-sourced (kassiesa.net / football-coefficient.eu): 2020/21-2025/26. Pre-2020/21 = approx.
#
# tournament_scope  = the primary summer-tournament treatment type for that season:
#   league_wide    -> Euro / World Cup (nearly every PL club sends players)
#   regional_copa  -> Copa America ONLY (no Euro/WC that summer): intermediate scope, ~25-35 PL players
#   club_narrow    -> FIFA Club World Cup 2025 (only 2 PL clubs)
#   winter_control -> 2022 World Cup, mid-season interruption (different mechanism)
#   none           -> no major summer tournament
# copa_america_flag = 1 if a Copa America edition occurred that summer (independent layer)

finals = {"2015/16":0,"2016/17":0,"2017/18":1,"2018/19":4,"2019/20":0,
          "2020/21":2,"2021/22":1,"2022/23":1,"2023/24":0,"2024/25":2,"2025/26":2}

rows = [
    # season, preceding_tournament, scope, copa_flag, coeff, source
    ("2015/16","Copa America 2015","regional_copa",1,14.250,"approx"),
    ("2016/17","Euro 2016 + Copa Centenario","league_wide",1,14.928,"approx"),
    ("2017/18","None","none",0,20.071,"approx"),
    ("2018/19","World Cup 2018","league_wide",0,22.642,"approx"),
    ("2019/20","Copa America 2019","regional_copa",1,18.571,"approx"),
    ("2020/21","None (Euro & Copa postponed)","none",0,24.357,"firm"),
    ("2021/22","Euro 2020(21) + Copa 2021","league_wide",1,21.000,"firm"),
    ("2022/23","Winter WC 2022","winter_control",0,23.000,"firm"),
    ("2023/24","None","none",0,17.375,"firm"),
    ("2024/25","Euro 2024 + Copa 2024","league_wide",1,29.464,"firm"),
    ("2025/26","Club World Cup 2025","club_narrow",0,28.681,"firm"),
]
df = pd.DataFrame(rows, columns=["season","preceding_tournament","tournament_scope","copa_america_flag","eng_season_coeff","coeff_source"])
df["eng_ucl_uel_finalists"] = df["season"].map(finals)
df["league_treatment_flag"] = (df["tournament_scope"]=="league_wide").astype(int)

print("=== SEASON-LEVEL DATASET ===")
print(df[["season","tournament_scope","copa_america_flag","eng_season_coeff","eng_ucl_uel_finalists","coeff_source"]].to_string(index=False))

def m(scope): 
    s=df[df.tournament_scope==scope]; return s.eng_season_coeff.mean(), len(s), list(s.season)

print("\n=== EUROPEAN PERFORMANCE by scope ===")
for sc in ["league_wide","regional_copa","none","club_narrow","winter_control"]:
    mean,k,seas=m(sc); print(f"{sc:14s} n={k}  mean coeff={mean:6.3f}  {seas}")

lw = df[df.tournament_scope=="league_wide"].eng_season_coeff.mean()
clean = df[df.tournament_scope=="none"].eng_season_coeff.mean()
copa = df[df.tournament_scope=="regional_copa"].eng_season_coeff.mean()
allnorm = df[df.tournament_scope.isin(["none","regional_copa"])].eng_season_coeff.mean()

print("\n=== KEY CONTRASTS ===")
print(f"League-wide ({lw:.3f}) vs ALL non-tournament incl. Copa ({allnorm:.3f}): {lw-allnorm:+.3f}  [original framing]")
print(f"League-wide ({lw:.3f}) vs CLEAN controls only ({clean:.3f}): {lw-clean:+.3f}  [Copa removed from controls]")
print(f"Regional-Copa-only ({copa:.3f}) vs clean controls ({clean:.3f}): {copa-clean:+.3f}")

print("\nNote: 2024/25 (England's record 29.464) was a DOUBLE tournament summer (Euro + Copa),")
print("yet posted the best coefficient on record -> counter to a fatigue-decline hypothesis.")

DATA_PATH.parent.mkdir(parents=True, exist_ok=True)
df.to_csv(DATA_PATH, index=False)
print(f"\nSaved {DATA_PATH}")
