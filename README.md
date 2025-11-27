## Steam Games: Analyzing Success Factors by Game Type

This project performs an Exploratory Data Analysis (EDA) on a dataset of Steam games (March 2025) to understand the factors driving success. Specifically, the analysis focuses on comparing **Singleplayer**, **Multiplayer**, and **Hybrid** (games containing both elements) categories.

The core goal is to determine if specific game types perform statistically better than others in terms of player ownership and user review positivity.

### Data Source:
- **Dataset:** [Steam Games Dataset on Kaggle](https://www.kaggle.com/datasets/artermiloff/steam-games-dataset)


## Key Metrics & Methodology

### 1. Game Categorization

Games were categorized based on specific keywords found in their `categories` and `tags` columns:

* **Singleplayer:** 'single-player' tag present.
* **Multiplayer:** 'multiplayer', 'co-op', 'online', 'pvp', 'mmo'.
* **Hybrid:** Contains flags for *both* Singleplayer and Multiplayer.

### 2. The "Success Index"

To evaluate games holistically, a custom **Success Index** was engineered. This metric balances **Quality** (Review Positivity) with **Reach** (Player Base).

$$
\text{Success Index} = \text{Review Score} \times \log(1 + \text{Estimated Owners})
$$

* **Review Score:** Fraction of positive reviews (0.0 to 1.0).
* **Log Owners:** Logarithmic transformation of estimated owners (multiplier: 30x reviews) to handle extreme data skew.

## Technologies Used

* **Python 3.14**
* **Pandas & NumPy:** Data manipulation and cleaning.
* **Matplotlib & Seaborn:** Visualization (Boxplots, Bar charts, Heatmaps).
* **SciPy:** Statistical testing (Kruskal-Wallis, ANOVA).

## Project Structure

* `EDA.ipynb`: The main Jupyter Notebook containing data cleaning, feature engineering, and statistical analysis.
* `games_march2025_cleaned.csv`: The source dataset.

## Key Findings

### 1. Hybrid Games Dominate

According to the analysis, **Hybrid games** consistently outperform pure Singleplayer or Multiplayer titles.

* **Mean Success Index:** Hybrid (6.79) > Multiplayer (6.20) > Singleplayer (6.08).
* **Interpretation:** Games that offer both solo and social experiences tend to capture broader audiences and maintain higher engagement.

### 2. Statistical Significance

We performed rigorous statistical testing to validate these observations:

* **Kruskal-Wallis Test:** Confirmed significant differences in review distributions across groups.
* **One-Way ANOVA:** Yielded a high F-statistic (**394.67**), providing strong evidence that the difference in Success Index between game types is statistically significant and not due to random chance.

### 3. Statistical Hypothesis Testing

To scientifically validate differences between game types, we established a formal hypothesis framework using One-Way ANOVA:

* **Null Hypothesis ($H_0$):** The mean Success Index is identical across all game types (Singleplayer, Multiplayer, Hybrid).
  

* **Alternative Hypothesis ($H_1$):** At least one game type has a significantly different mean Success Index compared to the others.



## Visualizations

The notebook generates several key insights:

* **Boxplots:** Comparing Review Positivity across categories.
* **Bar Charts:** Comparing Average Log Owners vs. Raw Owners.
* **Correlation Heatmap:** Analyzing the relationship between Metacritic scores, User Scores, and Estimated Owners.
