# NBA 2024-2025: Slumps & Recoveries

---

## **Introduction**

This study analyzes **game-to-game shooting slumps** of NBA players during the 2024-2025 regular season. It identifies when players fall into shooting slumps, how long they stay in these slumps, and how quickly they recover. Instead of utilizing traditional metrics such as Field Goal Percentage (FG%), this analysis measures shooting slumps using True Shooting Percentage.

**True Shooting Percentage (TS%)** shows how efficiently a player **turns their shooting opportunities into points**, integrating two-point attempts, three-point attempts, and free throw attempts.

```math
TS\% = \frac{PTS}{2 \times (FGA + 0.44 \times FTA)}
```

> **Game Example:** Cade Cunningham scores 25 points on 15 field goals attempted (FGA) and 6 free throws attempted (FTA).
>
> ```math
> TS\% = \frac{PTS}{2 \times (FGA + 0.44 \times FTA)}
> ```
>
> ```math
> TS\% = \frac{25}{2 \times (15 + 0.44 \times 6)}
> ```
>
> ```math
> TS\% = \frac{25}{2 \times (15 + 2.64)}
> ```
>
> ```math
> TS\% = \frac{25}{2 \times 17.64}
> ```
>
> ```math
> TS\% = \frac{25}{35.28} = 0.709
> ```
> 
> TS% = 70.9%, which is a highly efficient scoring performance. The NBA average for the 2024-2025 regular season was 58.3%.

---

## **About the Dataset**

To keep this study statistically stable, **117 players** were included. These players met the Basketball-Reference qualification standard for Field Goal Percentage (FG%):
- **Made at least 300 field goals (shots)** across the entire regular season

This filter ensures each player had a large enough shooting sample for their TS% and slump/recovery patterns to be meaningful.

All game log data was sourced directly from [**Basketball-Reference**](https://www.basketball-reference.com/). Automated data scraping methods proved unsuccessful, so each qualified player's game logs were manually copied and pasted (one by one) into a `.txt` file.

> For example, here is [Nikola Jokić's 2024-2025 game log](https://www.basketball-reference.com/players/j/jokicni01/gamelog/2025) as a reference for how the raw data structure appears.

---

## **Project Goals**

1. Define what a slump is.
> How exactly does a player "trigger" a slump?
2. Define what a recovery is.
> How exactly does a player "trigger" a recovery?
3. Find out how long it takes players to recover from slumps.
> Who recovered fastest from slumps?
4. Compare shot volume during slumps vs recoveries.
> Were there any shot volume adjustments from slump → recovery?

---

## **Table of Contents**

1. [Introduction](#introduction)  
2. [About the Dataset](#about-the-dataset)  
3. [Project Goals](#project-goals)  
4. [Tools Used](#tools-used)  
5. [Project Files](#project-files)  
6. [Data Preparation & Cleaning, Part 1 (Notebook 01)](#data-preparation--cleaning-part-1-notebook-01)  
7. [Data Preparation & Cleaning, Part 2 (Notebook 02)](#data-preparation--cleaning-part-2-notebook-02)  
8. [Data Merging (Notebook 03)](#data-merging-notebook-03)  
9. [Exploratory Analysis (Notebook 04 + Dashboard)](#exploratory-analysis-notebook-04--dashboard)  
10. [Tableau Dashboard](#tableau-dashboard)  
11. [Conclusion](#conclusion)  
12. [Tableau Dashboard Link](#tableau-dashboard-link)

---

## **Tools Used**

- **Python** (via **Jupyter Notebook):** Data loading, cleaning, merging, and analysis
- **Tableau:** Dashboard design and final visualizations

---

## **Project Files**

### **Jupyter Notebooks**
- [`01_NBA_2024_25_cleaning_1.ipynb`](https://github.com/dylanbarrett-analytics/nba-2024-2025-slumps-and-recoveries/blob/main/notebooks/01_NBA_2024_25_cleaning_1.ipynb)
Data import, consolidation of all player game logs, and cleaning
- [`02_NBA_2024_25_cleaning_2.ipynb`](https://github.com/dylanbarrett-analytics/nba-2024-2025-slumps-and-recoveries/blob/main/notebooks/02_NBA_2024_25_cleaning_2.ipynb)
Data import, consolidation of all player game logs, and cleaning (with corrections made to the raw `.txt` file)
- [`03_NBA_2024_25_merge.ipynb`](https://github.com/dylanbarrett-analytics/nba-2024-2025-slumps-and-recoveries/blob/main/notebooks/03_NBA_2024_25_merge.ipynb)
Merge with two additional `.txt` files
- [`04_NBA_2024_25_analysis.ipynb`](https://github.com/dylanbarrett-analytics/nba-2024-2025-slumps-and-recoveries/blob/main/notebooks/04_NBA_2024_25_analysis.ipynb)
Analysis of slumps and recoveries

### **CSV Exports - Cleaning**
- [`NBA_2024_25_game_logs_final.csv`](https://github.com/dylanbarrett-analytics/nba-2024-2025-slumps-and-recoveries/blob/main/cleaning_csv/NBA_2024_25_game_logs_final.csv)
Cleaned player game logs (prepped for analysis)

### **CSV Exports - Analysis**
- [`player_slump_vs_recovery_ts.csv`](https://github.com/dylanbarrett-analytics/nba-2024-2025-slumps-and-recoveries/blob/main/analysis_csv/player_slump_vs_recovery_ts.csv)
TS% in slumps vs TS% in recoveries (player-level)
- [`all_slumps.csv`](https://github.com/dylanbarrett-analytics/nba-2024-2025-slumps-and-recoveries/blob/main/analysis_csv/all_slumps.csv)
Summary table of all slumps
- [`recovered_slumps.csv`](https://github.com/dylanbarrett-analytics/nba-2024-2025-slumps-and-recoveries/blob/main/analysis_csv/recovered_slumps.csv)
Summary table of "recovered slumps"
- [`player_slump_summary.csv`](https://github.com/dylanbarrett-analytics/nba-2024-2025-slumps-and-recoveries/blob/main/analysis_csv/player_slump_summary.csv)
Player-level summary of slumps
- [`league_slump_summary.csv`](https://github.com/dylanbarrett-analytics/nba-2024-2025-slumps-and-recoveries/blob/main/analysis_csv/league_slump_summary.csv)
1 row league-level summary of slumps
- [`player_next_game_recovery.csv`](https://github.com/dylanbarrett-analytics/nba-2024-2025-slumps-and-recoveries/blob/main/analysis_csv/player_next_game_recovery.csv)
Player-level summary of next-game recoveries
- [`league_next_game_recovery.csv`](https://github.com/dylanbarrett-analytics/nba-2024-2025-slumps-and-recoveries/blob/main/analysis_csv/league_next_game_recovery.csv)
1 row league-level summary of next-game recoveries
- [`shot_volume_adjustment.csv`](https://github.com/dylanbarrett-analytics/nba-2024-2025-slumps-and-recoveries/blob/main/analysis_csv/shot_volume_adjustment.csv)
FGA in slumps vs FGA in recoveries (slump-level)
- [`player_shot_profile.csv`](https://github.com/dylanbarrett-analytics/nba-2024-2025-slumps-and-recoveries/blob/main/analysis_csv/player_shot_profile.csv)
FGA in slumps vs FGA in recoveries (player-level)
- [`league_shot_profile.csv`](https://github.com/dylanbarrett-analytics/nba-2024-2025-slumps-and-recoveries/blob/main/analysis_csv/league_shot_profile.csv)
FGA in slumps vs FGA in recoveries (1 row league-level summary)

### **Documentation**
- `README.md`: Project documentation

---

## **Data Preparation & Cleaning, Part 1 (Notebook 01)**

The cleaning process consisted of these primary actions:

- Imported raw `.txt` file containing all qualified players' game logs (**9,720 rows**).
- Dropped full-season summary rows and internal player-header rows.
- Dropped nonessential columns (e.g., "GameScore").
- Encoded home/away status for every game.
- Created boolean column to flag whether or not a player started a game.
- Extracted win/loss result from every game.
- Extracted `team_points`, `opponent_points`, and `point_diff` (`team_points` - `opponent_points`) from every game's score.
- Created a `shoots` column (right-handed or left-handed).
- Applied data type conversions so that all columns have correct data types.
- Verified date range of **October 22, 2024 - April 13, 2025** across the entire regular season.

During the final sanity checks, it was discovered that two percentage columns had integer values greater than 1.0 (`three_point_pct` and `free_throw_pct`). Traditional shooting percentages must only have values between 0 and 1, and since there were several large integers such as 4, 11, and 15, this had to be addressed.

> `effective_fg_pct` also had some values greater than 1.0, but since these values were only *slightly* above 1.0, such as 1.143 and 1.250, these values were acceptable. Effective field goal percentage (eFG%) will have a few values like this because the formula provides extra weight for 3-point makes.

After a query for all `three_point_pct` values greater than 1.0, it was determined that all of these unexpected values came from rows where the player recorded zero 3-point makes and zero 3-point attempts (0 for 0). Division by zero should return a null value (e.g., `NaN` → Not a Number). 

> For example, for Jalen Duren on 10/23/2024, 0 `three_pointers_made` out of 0 `three_pointers_attempted` obviously does not equal a `three_point_pct` of 4.0 (400%).

A similar query for all `free_throw_pct` values greater than 1.0 showed that these unexpected values came from rows where, in a lot of cases, the player had more `free_throws_made` than `free_throws_attempted`. These results are clearly off, as well.

> For example, for Jalen Duren on 10/23/2024, 6 `free_throws_made` out of 1 `free_throws_attempted` for a `free_throw_pct` of 4.0 (400%) is way off.

Next, a search for all players without a single 3-point attempt for the entire regular season was made. Three players were found: Ivica Zubac, Jalen Duren, and Rudy Gobert. Their basketball-reference game logs were investigated further:

- [Ivica Zubac's 2024-2025 game logs](https://www.basketball-reference.com/players/z/zubaciv01/gamelog/2025#header)
- [Jalen Duren's 2024-2025 game logs](https://www.basketball-reference.com/players/d/durenja01/gamelog/2025)
- [Rudy Gobert's 2024-2025 game logs](https://www.basketball-reference.com/players/g/goberru01/gamelog/2025#header)

It was confirmed that there was no `three_point_pct` column for any of these players. Therefore, during the import process, all columns to the right of `three_point_pct` were shifted one column to the left.

> For example, for Ivica Zubac on 4/5/2025, he has 0 `three_pointers_made` out of 0 `three_pointers_attempted` for an incorrect `three_point_pct` of 4.0.
> It turns out, this 4.0 value is actually from the very next column to the right (`two_pointers_made`).
> With the `three_point_pct` column missing (in the original data), this `two_pointers_made` value of 4.0 was shifted leftward into the `three_point_pct` column (in the Python DataFrame).

<sub> After several unsuccessful attempts at addressing this shift issue in Python, I decided to go back to the raw `.txt` file. For these three players without any 3-point attempts, the `three_point_pct` column was manually added with its corresponding `NaN` values. Now the original data is properly aligned and organized.

---

## **Data Preparation & Cleaning, Part 2 (Notebook 02)**

With the shift issue fixed, this notebook involves the same exact cleaning process as Notebook 01. At the end, it was confirmed that there were no `three_point_pct` or `free_throw_pct` values greater than 1.0 this time.

---

## **Data Merging (Notebook 03)**

For additional context, I wanted to add three additional columns to the cleaned game logs data (from Notebook 02):
- the player's primary position
- the player's age
- the player's average shot distance (over the course of the entire regular season)

To do that, these two Basketball-Reference data sources were saved as `.txt` files and loaded into Python:

- [NBA 2024-2025 Per Game Stats](https://www.basketball-reference.com/leagues/NBA_2025_per_game.html)
- [NBA 2024-2025 Shooting Stats](https://www.basketball-reference.com/leagues/NBA_2025_shooting.html)

During the two merges, only the three columns (mentioned above) were kept. With these additions, the data was now complete and ready for analysis.

---

## **Exploratory Analysis (Notebook 04 + Dashboard)**

### Defining the Slump Threshold

To trigger a slump, a player must have a game where his TS% is **below the slump threshold**:

```math
\text{Slump Threshold} = \text{Season TS\%} - k \times \sigma_{\text{TS\%}}
```

- Season TS% = the player's TS% across all regular season games
- σ₍TS%₎ = the standard deviation of the player's game-to-game TS% across all regular season games
- k = a chosen multiplier that controls how strict the slump definition is (k = 0.5 in this study)

> **Example:**
>
> Player A has:
> - Season TS% = 58.0%
> - $\sigma_{\text{TS%}}$ = 0.15
> - k = 0.5
>
> ```math
> \text{Slump Threshold} = 0.58 \;-\; 0.5 \times 0.15 = 0.505
> ```
>
> If Player A has a game where his TS% is below 50.5%, then a slump has officially begun.

### Defining the Recovery Threshold

In the midst of a slump, to trigger a recovery, a player must have a game where his TS% is **at least the recovery threshold**:

```math
\text{Recovery Threshold} = \text{League Average TS\%}
```

The league-wide average TS% is 58.3%.

> For example, if Player A is in a slump, and has a game where his TS% is at least 58.3%, then a recovery has occurred (and the slump is over).

### Why These Particular Thresholds?

Slumps are measured **relative to the player** because scoring efficiency varies widely across the league. A fixed league-level threshold (e.g., TS% < 45%) would not trigger enough slumps for top-tier scorers, and it would trigger too many slumps for lower-tier scorers.

Recoveries are measured **relative to the league average** so that all players are judged by the **same standard of scoring efficiency**. If recoveries were individualized player-level thresholds, then lower-tier scorers would easily "recover" to much lower TS% peaks while top-tier scorers would struggle to "recover" to much higher peaks. Using the league average ensures a fair, comparable benchmark for all players.

This hybrid approach ensures that **slumps are individualized** and **recoveries are comparable**.

### 2nd Game Recovery Rate (a.k.a. Next-Game Recovery Rate)

This metric measures how often players **recover immediately** after entering a slump.

Once a slump begins (the **1st game below the slump threshold**), the very next game (the **2nd game**) becomes the player's **first opportunity to recover**.

So out of all slumps that start, how many players recover in the very next game? The league-wide "2nd Game Recovery Rate" was 48.5%, meaning **almost half of all slumps ended the very next game**.

### Average Games to Recover

Once a slump begins, not every player bounces back right away. To capture how long it takes for a player to recover, every slump was tracked from its 1st game until the "recovery game".

> **Note:** Out of 1,567 total slumps (across all qualified players), 1,502 had recoveries. These are referred to as "recovered slumps". As for the other 65 slumps without recoveries, these are referred to as "unrecovered slumps". "Unrecovered slumps" occur due to:
> - an inactive gap where the player does not play in a game for **at least 14 calendar days** (this ends the slump without a recovery occurring)
> - the end of the season (this ends the slump without a recovery occurring)
>
> The final dashboard accounts for **recovered slumps only**.

The league-wide average was **2.02 games to recover**, meaning that on average, it takes roughly 2 games for a player to successfully exit a slump.

Nikola Jokić led the NBA, only needing 1.05 games to recover. In fact, out of his 21 total slumps across the season, only 1 slump lasted more than 1 game, which is simply amazing.

### Shot Volume Adjustment (Slumps → Recoveries)

To see whether players changed their shooting approach in order to exit a slump, each player's **average field goal attempts (FGA) during slump games** was compared to their **average FGA during recovery games**.

Across all qualified players:
- **50.6%** took **more shots** when they recovered
- **43.5%** took **less shots** when they recovered
- **5.9%** had **no change** when they recovered

The evidence isn't overwhelming, but a slight edge goes to players who increased their shot volume, which encourages the mindset, "The most important shot is the next shot."

---

### **Tableau Dashboard**

![Dashboard Screenshot](nba_slumps_recoveries_dashboard.png)

---

## **Conclusion**

Perhaps one of the most interesting findings of this study was **the performance of centers**, as opposed to any other position.

They posted the **highest 2nd game recovery rate (54.2%)** and also recorded the **lowest average games to recover (1.79 games)**.

This makes sense considering that **TS% naturally favors centers**. They take a larger share of their shots right at the rim, where efficiency is highest, and they draw shooting fouls at high rates due to their physicality and interior presence.

What's even more interesting is how this plays out in the modern NBA, where seemingly everyone is running to the perimeter to shoot as many 3-pointers as possible. So much talk over the last 10 years or so has been that the "traditional big man" is becoming obsolete. However, TS% and this analysis show that centers are still so valuable in today's game.

As metrics like this continue to become more mainstream, it's easy to imagine agents of centers increasingly leaning on TS% during contract negotiations.

---

## **Tableau Dashboard Link**

🔗 [View the Dashboard on Tableau Public](https://public.tableau.com/app/profile/dylan.barrett1539/viz/NBASlumpRecoveriesinprogress/Dashboard)
