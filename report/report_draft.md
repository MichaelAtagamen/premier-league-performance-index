# Premier League Team Performance Composite Index

**Module:** Data Analysis and Visualisation  
**Assessment:** CA1 - Index Generation and Visualisation  
**Student:** Michael Atagamen  
**Project Theme:** Football / Premier League performance analytics  

---

## 1. Introduction and Theoretical Framework

The aim of this project is to develop a **composite indicator** that ranks Premier League teams using a single overall performance score. A composite indicator is useful when the concept being measured is multidimensional and cannot be represented properly by one variable alone.

Football team performance is multidimensional. A team cannot be judged only by points, wins, or goals scored because overall performance is influenced by several connected areas. In this project, team performance is measured using three main dimensions:

- **Attacking performance**
- **Defensive performance**
- **Discipline**

These dimensions are combined into sub-indices and then aggregated into one final **Premier League Team Performance Composite Index**. The unit of analysis is **team-season**, meaning each row represents one Premier League team in one season.

The index is designed to answer the following question:

> Can a composite performance index provide a useful ranking of Premier League teams using attacking, defensive, and discipline-based indicators?

---

## 2. Data Selection

The project uses publicly available Premier League match data from **Football-Data.co.uk**. Five Premier League seasons were used:

- 2020/21
- 2021/22
- 2022/23
- 2023/24
- 2024/25

The raw data was match-level data. Each row represented one match. The project transformed this into a team-season dataset so that teams could be compared consistently.

The selected variables were chosen because they relate directly to football performance:

| Category | Variables Used | Reason |
|---|---|---|
| Results | Points, wins, draws, losses, league rank | Used for comparison with real league outcomes |
| Attack | Goals for, shots for, shots on target for, corners for, shot conversion rate | Measures attacking strength and chance creation |
| Defence | Goals against, shots against, shots on target against, clean sheets | Measures defensive stability |
| Discipline | Fouls, yellow cards, red cards | Measures discipline and negative match behaviour |

The final processed dataset contains **100 team-season rows** and **54 columns**.

---

## 3. Missing Data and Imputation

The selected variables were checked for missing values using `.isnull().sum()` in Python. The key columns used in the index did not contain major missing values after selection and processing.

Because of this, no major imputation was required. This is a strength of the dataset because the composite index is mainly based on observed values rather than estimated ones.

If missing values had been present, median imputation would have been suitable for numerical variables because the median is less sensitive to outliers than the mean.

---

## 4. Data Preparation and Team-Season Aggregation

The raw match-level data was converted into team-season level data. This was necessary because the composite index compares teams across seasons rather than individual matches.

For each team and season, the following totals and rates were calculated:

- Matches played
- Points
- Wins, draws, losses
- Goals for and against
- Shots for and against
- Shots on target for and against
- Corners for and against
- Fouls, yellow cards, red cards
- Clean sheets
- Per-match rates
- Goal difference
- Shot conversion rate
- League rank

This aggregation created a consistent dataset where each row represented one team in one Premier League season.

---

## 5. Multivariate Analysis

Multivariate analysis was used to examine the structure of the dataset and relationships between the variables. A correlation matrix was created to understand how the sub-indices and final composite index relate to real football outcomes such as points and league rank.

The correlation results showed that the final Composite Index had a strong relationship with actual football performance:

| Relationship | Correlation |
|---|---:|
| Composite Index vs Points | 0.919 |
| Composite Index vs League Rank | -0.878 |
| Composite Index vs Attack Index | 0.942 |
| Composite Index vs Defence Index | 0.93 |
| Composite Index vs Discipline Index | 0.546 |

The positive correlation between Composite Index and Points suggests that teams with higher index scores generally earned more points. The negative correlation between Composite Index and League Rank is expected because a lower league rank number means a better table position.

This supports the validity of the index because it broadly aligns with real Premier League outcomes while still including additional performance dimensions.

---

## 6. Normalisation

Normalisation was required because the indicators were measured on different scales. For example, goals per match, shots per match, yellow cards, and red cards cannot be directly combined without scaling.

The project used **Min-Max normalisation**, which scales values between 0 and 1.

For positive indicators, higher values represent better performance. Examples include:

- Goals for per match
- Shots for per match
- Shots on target for per match
- Clean sheets per match
- Shot conversion rate

For negative indicators, the normalised values were inverted so that higher scores always represented better performance. Examples include:

- Goals against per match
- Shots against per match
- Fouls per match
- Yellow cards per match
- Red cards per match

This ensured that all indicators moved in the same direction before aggregation.

---

## 7. Weighting and Aggregation

The final composite index was created using three sub-indices:

- **Attack Index**
- **Defence Index**
- **Discipline Index**

The final weighting structure was:

| Sub-index | Weight |
|---|---:|
| Attack Index | 40% |
| Defence Index | 40% |
| Discipline Index | 20% |

The final formula was:

`Composite Index = (0.4 × Attack Index) + (0.4 × Defence Index) + (0.2 × Discipline Index)`

Attack and defence were given the highest weights because scoring goals and preventing goals are the most direct contributors to football success. Discipline was included with a lower weight because it influences performance but is less direct than attacking and defensive output.

---

## 8. Cluster Analysis

K-means clustering was used to group team-seasons with similar performance profiles. The clustering was based on the three sub-indices:

- Attack Index
- Defence Index
- Discipline Index

The aim was to identify groups of teams with similar performance patterns rather than only ranking them.

Cluster summary:

|   Cluster |   Count |   Avg_Index |   Avg_Points |   Avg_Attack |   Avg_Defence |   Avg_Discipline |   Avg_League_Rank |
|----------:|--------:|------------:|-------------:|-------------:|--------------:|-----------------:|------------------:|
|         0 |      28 |       0.244 |       32.857 |        0.187 |         0.211 |            0.423 |            16.714 |
|         1 |      51 |       0.488 |       53.471 |        0.447 |         0.498 |            0.55  |            10.235 |
|         2 |      21 |       0.789 |       77.143 |        0.809 |         0.819 |            0.69  |             2.857 |

Based on the averages, the clusters can be interpreted as follows:

- **Cluster 2**: Strongest performance group. This cluster has the highest average Composite Index, strongest average attack and defence scores, and the best average league rank.
- **Cluster 1**: Mid-level performance group. These teams are generally around mid-table performance.
- **Cluster 0**: Weakest performance group. This cluster has the lowest average Composite Index and the weakest average league rank.

This clustering adds value because it shows that the index can group teams into meaningful performance profiles.

---

## 9. Link to Other Indices / Real League Table

The project links the Composite Index to a real-world benchmark: the actual Premier League table. The league table is used as a comparison index because it is the official ranking of team performance in each season.

The Composite Index was compared with:

- Points
- League rank
- Team ranking by Composite Index

Top three teams by Composite Index in each season:

|   Season |   Composite_Rank | Team      |   Composite_Index |   League_Rank |   Points |
|---------:|-----------------:|:----------|------------------:|--------------:|---------:|
|  2020_21 |                1 | Man City  |             0.934 |             1 |       86 |
|  2020_21 |                2 | Liverpool |             0.799 |             3 |       69 |
|  2020_21 |                3 | Chelsea   |             0.751 |             4 |       67 |
|  2021_22 |                1 | Man City  |             0.992 |             1 |       93 |
|  2021_22 |                2 | Liverpool |             0.906 |             2 |       92 |
|  2021_22 |                3 | Chelsea   |             0.715 |             3 |       74 |
|  2022_23 |                1 | Man City  |             0.928 |             1 |       89 |
|  2022_23 |                2 | Arsenal   |             0.809 |             2 |       84 |
|  2022_23 |                3 | Newcastle |             0.74  |             4 |       71 |
|  2023_24 |                1 | Man City  |             0.894 |             1 |       91 |
|  2023_24 |                2 | Arsenal   |             0.835 |             2 |       89 |
|  2023_24 |                3 | Liverpool |             0.69  |             3 |       82 |
|  2024_25 |                1 | Man City  |             0.869 |             3 |       71 |
|  2024_25 |                2 | Liverpool |             0.856 |             1 |       84 |
|  2024_25 |                3 | Arsenal   |             0.774 |             2 |       74 |

The results broadly align with real Premier League performance. For example, Manchester City ranked first in the Composite Index in several seasons and also finished near the top of the actual league table. This supports the usefulness of the index.

However, the Composite Index does not simply copy the league table. It can rank teams differently where underlying performance statistics are strong or weak compared with actual points. This is useful because it provides a broader view of performance beyond final league position.

Overall top teams by average Composite Index:

| Team        |   Avg_Composite |   Seasons |   Avg_League_Rank |   Avg_Points |
|:------------|----------------:|----------:|------------------:|-------------:|
| Man City    |           0.923 |         5 |               1.4 |         86   |
| Liverpool   |           0.791 |         5 |               2.8 |         78.8 |
| Arsenal     |           0.716 |         5 |               3.8 |         75.4 |
| Chelsea     |           0.603 |         5 |               5.8 |         63.4 |
| Tottenham   |           0.543 |         5 |               8.2 |         59.4 |
| Brighton    |           0.542 |         5 |              10   |         52.6 |
| Newcastle   |           0.538 |         5 |               7.8 |         58.2 |
| Man United  |           0.531 |         5 |               6.8 |         61.8 |
| Aston Villa |           0.509 |         5 |               8.4 |         59   |
| Brentford   |           0.458 |         4 |              12   |         50   |

---

## 10. Visualisation of Results

The project produced several visualisations to support interpretation of the results:

### Final Index Ranking

This chart ranks teams by their Composite Index score. It makes it easy to identify the highest and lowest performing teams according to the index.

### Attack vs Defence Scatter Plot

This visualisation compares attacking performance against defensive performance. It helps show whether teams are balanced or stronger in one area.

### Team Clusters

The cluster plot shows how team-seasons are grouped based on attack, defence, and discipline. This helps identify elite, mid-level, and weaker performance profiles.

### Correlation Matrix

The correlation matrix shows relationships between indicators. It supports the multivariate analysis section by showing how the final index relates to sub-indices, points, and league rank.
Showing and outlining key correlation values

---

## 11. Version Control

Git and GitHub were used to track development of the project. Version control was used to record progress across the notebook, dataset processing, visualisation generation, and report writing.

Example commit stages include:

- Initialising the project structure
- Adding the notebook and data loading process
- Creating the team-season dataset
- Adding normalisation and sub-index calculations
- Adding clustering analysis and visualisations
- Writing and improving the report

Using Git supports transparency and shows how the project developed over time.

---

## 12. Limitations

This index is useful, but it has limitations.

First, the index is based only on available match statistics. It does not include squad market value, injuries, fixture difficulty, tactical context, player quality, or expected goals.

Second, the weighting system is manually chosen. Although the weights are justified, different weighting choices could lead to different final rankings.

Third, discipline is included as a sub-index, but its influence on performance may vary between teams and seasons.

Finally, the 2024/25 season may depend on the completeness of the available data. If the season data is incomplete, results for that season should be interpreted carefully.

Despite these limitations, the index provides a structured and transparent way to compare Premier League team performance using multiple indicators.

---

## 13. AI Acknowledgement

Generative AI was used to support project planning, code structuring, explanation drafting, debugging, and report organisation. All final outputs were reviewed, edited, and adapted by the student. The student remained responsible for the final interpretation, submission, and academic integrity of the work.

---

## 14. Conclusion

This project developed a Premier League Team Performance Composite Index using five seasons of publicly available football data. The index combined attack, defence, and discipline indicators into a single composite score.

The results show that the Composite Index generally aligns with real Premier League outcomes, especially points and league rank. The use of normalisation, weighting, clustering, and visualisation helped turn raw football statistics into a meaningful analytical model.

Overall, the project demonstrates how a composite indicator can be used to compare football teams in a multidimensional way rather than relying on one statistic alone.
