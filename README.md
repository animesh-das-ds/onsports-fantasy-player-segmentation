# OnSports — Fantasy Football Player Segmentation

![Course](https://img.shields.io/badge/Course-Unsupervised%20Learning-2ca02c)
![Grade](https://img.shields.io/badge/Grade-A%20(4.0)-success)
![Type](https://img.shields.io/badge/Type-Clustering%20%C2%B7%20K--Means%20%C2%B7%20Hierarchical-blue)
![Tools](https://img.shields.io/badge/Tools-scikit--learn%20%C2%B7%20scipy%20%C2%B7%20Seaborn-orange)

A clustering project that groups English Premier League players by performance so a fantasy sports platform can set **fair, data-driven starting prices** for the new season.

---

## Business Problem

OnSports is a fantasy sports platform. Each player has a price that changes with real-world performance. With a new Premier League season approaching, the company needed to set starting prices that reflect each player's true potential — otherwise the game becomes unbalanced and users lose trust.

## Objective

Perform cluster analysis to identify players of different potential based on last season's performance, using **both K-Means and Hierarchical clustering**, and translate the segments into pricing recommendations.

## Data

| Attribute | Detail |
|---|---|
| Players | **476** |
| Variables | **13** — club, position, goals, assists, total fantasy points, minutes played, goals conceded, creativity, influence, threat, bonus points, clean sheets |
| Coverage | 17 clubs across four positions |

## Approach

1. **EDA** — univariate distributions for all performance metrics, plus club and position distributions; correlation heatmap and bivariate comparisons (points by club, points by position, minutes by position, bonus by club).
2. **Preprocessing** — checked outliers, then **standardised (z-score scaled)** all features so that high-magnitude metrics like minutes and influence would not dominate the clustering.
3. **K-Means clustering** — used the elbow method and silhouette analysis to choose the number of clusters, then built the final model and profiled the clusters.
4. **Hierarchical clustering** — computed cophenetic correlations across distance metrics and linkage methods, compared dendrograms, and selected the best combination.
5. **Comparison** — compared K-Means and Hierarchical results for consistency and business interpretation.

## Key Findings

**Performance is highly skewed** — average goals per player is ~1.9 but the maximum is 23; assists average ~1.75 with a maximum of 14. A small elite dominates.

**Three natural performance dimensions emerged**
1. **Attacking performance** — goals, threat, bonus, assists
2. **Creative influence** — creativity, assists, influence
3. **Defensive solidity** — clean sheets, goals conceded, minutes

**Key correlations:** total points with influence **0.96**, with minutes **0.91**, with clean sheets **0.89**; goals with threat **0.90**; assists with creativity **0.83**.

**Position and club patterns**
- **Midfielders** score the most fantasy points on average, followed by forwards; goalkeepers and defenders score less but more consistently. Midfielders also play the most minutes (~1,400), forwards the fewest (~1,080).
- **Manchester City** players lead on average fantasy points and bonus points, followed by Chelsea, Liverpool and Leicester; Crystal Palace, Burnley and Newcastle trail.

**Optimal cluster count**
- The elbow method suggested k = 3, but the **silhouette score peaked at k = 2 (~0.48)**, so two clusters were chosen.
- Hierarchical clustering with **Euclidean distance and Weighted linkage** achieved the highest cophenetic correlation (**0.862**) and also produced two clusters — matching K-Means.

**The two segments**
- **Cluster 1 — elite, high-impact performers** (e.g. Bruno Fernandes, Harry Kane, Mohamed Salah) with high goals, assists, points, creativity, influence, bonus and minutes.
- **Cluster 0 — supporting/average contributors** with lower output and fewer minutes.

## Recommendations

1. **Tier-based pricing** — price elite players exponentially higher to reflect their outsized impact, and keep supporting players in a budget tier.
2. **Dynamic pricing** — update prices using rolling form metrics (points per 90 minutes, recent 5-match form) rather than static season averages.
3. **Position-aware valuation** — reward attacking output for midfielders and forwards; emphasise defensive reliability for defenders and goalkeepers.
4. **Marketing** — use Cluster 1 players as featured picks and ambassadors.
5. **Predictive scouting** — re-run the clustering each season to spot players moving from Cluster 0 to Cluster 1 ("breakout player" features).
6. **Transparency** — add in-app dashboards showing player tiers, form and value trends.

## Skills Demonstrated

K-Means clustering · elbow method · silhouette analysis · hierarchical/agglomerative clustering · cophenetic correlation · dendrogram interpretation · feature scaling · cluster profiling · comparing two clustering approaches for robustness.

## Repository Structure

```
├── notebooks/
│   └── onsports_clustering.ipynb
├── reports/
│   └── OnSports_Business_Report.pdf
├── screenshots/
│   ├── notebook_chart_01.png … notebook_chart_10.png
│   └── report_page_01.png … report_page_04.png
└── README.md
```

---

*PGP in Data Science & Business Analytics · Great Lakes Executive Learning / The University of Texas at Austin, McCombs School of Business. Content drawn from the project notebook, business report and course transcript.*
