# ⚽ Premier League Football Analysis Dashboard | Power BI

> An interactive **Power BI dashboard** analyzing **10 seasons of English Premier League data (2009–2019)** — covering team performance, goal trends, home/away strength, disciplinary records, and referee behavior. Built using **Power Query**, **advanced DAX**, and a **star-schema data model** to transform 3,630 matches into actionable football insights.

---

<p align="center">
  <img src="Images/Premier%20League%20Banner.png" alt="Premier League Football Analysis Banner" width="100%">
</p>

---

# 📌 Project Overview

Football generates enormous volumes of match-level data every season — goals, shots, fouls, cards, corners, and refereeing decisions. Turning this raw data into insight is what separates clubs that win from those that merely compete.

This project presents an **interactive 3-page Power BI dashboard** built on **10 English Premier League seasons (2009–2019)**. It provides a comprehensive view of team performance, goal-scoring patterns, home vs away strength, aggression and discipline metrics, and referee influence — all explorable through dynamic slicers and DAX-driven calculations.

---

# 🎯 Project Objectives

- Analyze overall team performance across 10 EPL seasons
- Identify the strongest home teams and strongest away teams
- Compare total goals, average goals per match, and season-wise scoring trends
- Evaluate discipline metrics — yellow cards, red cards, and fouls
- Analyze the "Aggression Index" of clubs and referees
- Detect matches where half-time results were overturned at full-time
- Enable season-level and team-level dynamic filtering
- Build an interactive dashboard using advanced DAX and star-schema modeling

---

# 📊 Dashboard Preview

<p align="center">
  <img src="Images/Team%20Performance%20Dashboard.png" alt="Team Performance Overview" width="100%">
</p>

<p align="center">
  <img src="Images/Goal%20Analysis%20Dashboard.png" alt="Goal Analysis Dashboard" width="100%">
</p>

<p align="center">
  <img src="Images/Discipline%20and%20Referee%20Dashboard.png" alt="Discipline & Referee Analysis Dashboard" width="100%">
</p>

---

# 📁 Dataset Information

The dataset contains **match-level records from 10 English Premier League seasons (2009–2019)**, sourced from [football-data.co.uk](http://www.football-data.co.uk/) under the **ODC-PDDL** license.

Each seasonal CSV includes:

- Match Date
- Home Team & Away Team
- Full-Time Home/Away Goals & Result
- Half-Time Home/Away Goals & Result
- Referee
- Home/Away Shots & Shots on Target
- Home/Away Fouls Committed
- Home/Away Corners
- Home/Away Yellow Cards
- Home/Away Red Cards

**Total Matches Analyzed:** 3,630
**Total Goals Analyzed:** 9,979

---

# 🛠️ Tools & Technologies

- Microsoft Power BI Desktop
- Power Query (Data Cleaning & Transformation)
- DAX (Advanced Measures)
- Star-Schema Data Modeling
- Custom Date Table
- Interactive Slicers & Cross-Filtering Visuals

---

# 📐 Data Modeling

The project follows a **star-schema style data model** where a consolidated match-level fact table is connected with supporting dimension tables.

Main tables include:

- **All Data** (Fact table — combined 10 seasons)
- **All Teams** (Dimension)
- **All Measures** (Measure table for organized DAX)
- **Date Table** (Custom calendar for time intelligence)

A **role-playing dimension** approach was used for `All Teams` — connected twice to the fact table (Home Team and Away Team) using `USERELATIONSHIP()` in DAX to correctly attribute home vs away statistics per team.

---

# ⚙️ DAX Measures

Several custom DAX measures were created to handle both **home and away contexts** dynamically.

### Core Match Measures

- Total Matches
- Total Goals
- Average Goals Per Match
- Total Win (Home + Away)

### Team Strength Measures

- Home Strong Team
- Away Strong Team
- Highest Goal Scoring Team

### Discipline Measures

- Total Yellow Cards
- Total Red Cards
- Total Fouls
- Total Shots
- Total Shots on Target
- Total Corners

### Example DAX Pattern (Role-Playing Dimension)

```dax
M TotalGoal =
VAR TotalHomeGoal =
    CALCULATE(
        SUM('All Data'[Full Time Home Goal]),
        USERELATIONSHIP('All Data'[HomeTeam], 'All Teams'[Teams])
    )
RETURN
IF(
    ISFILTERED('All Teams'[Teams]),
    TotalHomeGoal + SUM('All Data'[Full Time Away Goal]),
    TotalHomeGoal + SUM('All Data'[Full Time Away Goal])
)
```

Key functions used:

- `CALCULATE()`
- `USERELATIONSHIP()`
- `DIVIDE()`
- `SELECTEDVALUE()`
- `TOPN()`
- `ISFILTERED()`
- `COUNTA()`
- `SUM()`
- `VAR / RETURN`

---

# 📈 Dashboard Features

### Executive KPI Cards

- Total Matches — **3,630**
- Total Goals — **9,979**
- Total Red Cards — **530**
- Total Yellow Cards — **12K**
- Most Experienced Referee — **A. Madley**

---

### Interactive Visualizations

- Top 10 Home Strong Teams
- Top 10 Away Strong Teams
- Strongest Teams by Matches Won
- Most Red Cards by Team
- Most Yellow Cards by Team
- Total Goals per Season
- Average Goals per Season
- Avg Goals Scored by Team
- Win by Highest Goal Difference
- Games Changed: HT Leading Team vs FT Winning Team
- Most Aggressive Team (Shots, Shots on Target & Goals)
- Fouls Committed by Teams
- Referee Performance Cards

---

# 💡 Key Business Insights

### 🏆 Team Performance

- **Man City** ranks #1 in total wins overall (231 wins).
- **Chelsea**, **Man United**, and **Tottenham** dominate the top-4 win statistics.
- **Best Home Teams:** Man City, Chelsea, Arsenal.
- **Best Away Teams:** Man City, Chelsea, Man United.

---

### 🥅 Goal Analysis

- **Average Goals per Match:** ~2.75
- **Max Goals in a Single Match:** 10
- **Top Goal-Scoring Team:** Tottenham
- **High-Scoring Seasons:** 2016–17 & 2017–18 (both exceeded 2,000 goals)
- **Top Average Goal Scorers:**
  - Man City — 2.21 goals/match
  - Chelsea — 1.96
  - Arsenal — 1.95
  - Liverpool — 1.85
  - Tottenham — 1.82

---

### 🟨 Aggression & Discipline

- **Total Red Cards:** 530 — led by Sunderland, Arsenal, West Ham
- **Total Yellow Cards:** Over 12,000 — led by Man City, Man United, Stoke
- **Foul Leaders:** Man United, Everton, Stoke, Tottenham, Man City
- **Top Referees by Match Count:** M. Dean, M. Atkinson, A. Marriner

---

### 🔄 Match Swing Patterns

- Multiple matches where **half-time leads were overturned at full-time**
- Frequent **4–5 goal wins**, especially by Arsenal, Man United, Tottenham

---

# 🎯 Strategic Insights

- **Man City** consistently ranks top across **wins, goals, and aggression** — reflecting a high-risk, high-reward playing style.
- Teams like **Sunderland** and **West Ham** show high aggression with **low performance payoff** — indicating possible tactical inefficiencies.
- **Referee behavior** visibly influences match dynamics — a strong candidate for deeper predictive modeling.

---

# 🎨 Dashboard Highlights

- Football-themed Dark Green UI
- Custom Premier League Banner
- Interactive Season & Team Slicers
- Dynamic KPI Cards
- Cross-Filtering Visuals
- Role-Playing Dimension Handling
- Clean Executive Dashboard Design

---

# 🚀 Skills Demonstrated

- Data Cleaning & Transformation
- Star-Schema Data Modeling
- Role-Playing Dimensions
- Advanced DAX Programming
- KPI Development
- Sports Analytics
- Referee & Discipline Analytics
- Dashboard Design
- Interactive Reporting
- Business Intelligence

---

# 📂 Repository Structure

```
Premier-League-Analysis-PowerBI/
│
├── Dashboard/
│   └── Premier League Football Analysis.pbix
│
├── Dataset/
│   ├── season-0910.csv
│   ├── season-1011.csv
│   ├── season-1112.csv
│   ├── season-1213.csv
│   ├── season-1314.csv
│   ├── season-1415.csv
│   ├── season-1516.csv
│   ├── season-1617.csv
│   ├── season-1718.csv
│   └── season-1819.csv
│
├── Images/
│   ├── Premier League Banner.png
│   ├── Team Performance Dashboard.png
│   ├── Goal Analysis Dashboard.png
│   └── Discipline & Referee Dashboard.png
│
├── Documents/
│   ├── Summary Report.pdf
│   ├── DAX & Measures.pdf
│   └── Premier League Analysis Dashboard.pdf
│
├── schema.json
├── datapackage.json
└── README.md
```

---

# 🌟 Project Highlights

✔ Interactive 3-Page Football Dashboard
✔ Advanced DAX with Role-Playing Dimensions
✔ Dynamic KPI Cards
✔ Season-Wise Goal Trend Analysis
✔ Home vs Away Team Strength Analysis
✔ Discipline & Referee Analytics
✔ Match Swing (HT vs FT) Detection
✔ Football-Themed Responsive Dashboard

---

# 📚 Key Learnings

Throughout this project, I strengthened my skills in:

- Handling **role-playing dimensions** with `USERELATIONSHIP()`
- Writing reusable DAX for **home/away context switching**
- Building efficient **season-level data models** across multiple CSV files
- Designing **interactive football dashboards**
- Developing sports-specific KPIs
- Applying **business intelligence** to sports performance data
- Detecting **match outcome swings** using HT vs FT comparison logic

---

# ✅ Conclusion

This project demonstrates how **Power BI** can transform 10 seasons of raw football data into meaningful strategic insights through interactive dashboards and advanced DAX. By combining team performance KPIs, goal-trend analytics, discipline metrics, and referee analysis, the dashboard provides a **centralized analytical view of Premier League football**, supporting tactical decision-making for analysts, fantasy managers, and sports bettors alike.

---

## 👨‍💻 Author

**Sabbir Uddin Akash**

- 💼 Aspiring Data Analyst
- 📊 Power BI | SQL | Excel | Python
- 🌐 Portfolio: [Sabbir Uddin Akash](https://sabbirakash.github.io)
- 💻 GitHub: [sabbirakash](https://github.com/sabbirakash)
- 🔗 LinkedIn: [Sabbir Uddin Akash](https://www.linkedin.com/in/sabbirakash)

If you found this project useful, consider giving it a ⭐.
