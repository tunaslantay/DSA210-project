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
* **Pandas & NumPy:** Data manipulation and feature engineering.
* **Scikit-Learn:** Decision Trees, Regressors, and Feature Importance analysis.
* **Matplotlib & Seaborn:** Statistical visualization and correlation plotting.
* **SciPy:** Statistical hypothesis testing (ANOVA, Kruskal-Wallis).

## Project Structure

* **`EDA.ipynb`** (Exploratory Data Analysis)
  * Handles data loading, cleaning, and the categorization of games into Singleplayer, Multiplayer, and Hybrid.
  * Engineers the custom `Success Index` metric.
  * Performs statistical testing (ANOVA) to identify significant performance differences between game categories.
* **`ML.ipynb`** (Machine Learning Analysis)
  * Loads the processed dataset and performs feature selection to remove target leakage.
  * Implements predictive modeling pipelines to isolate causal factors.
  * Analyzes feature importance to determine which variables actually drive the Success Index.
* **`data/`**
  * Contains the source CSV files and the processed datasets generated during the analysis.

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


### 4. Machine Learning Analysis
To isolate the causal factors of success, a ML model was trained to predict the Success Index using features such as Game Type, Price, DLC Count, and Metacritic Score.

**Crucial Observation:**
Contrary to the trends observed in the EDA, the predictive model assigned a feature importance of nearly **0.0** to `game_type`. This indicates that the game category itself (Singleplayer vs. Hybrid) has negligible predictive power when other variables are controlled.



## Conclusion

While Hybrid games statistically trend higher in the Success Index, the Machine Learning analysis reveals that **Game Type is not a primary driver of success.**

The observed success of Hybrid games is likely a result of confounding variables; Hybrid games in this dataset tend to have higher **Metacritic Scores** and more robust post-launch support (**DLC**). Therefore, development resources should be prioritized towards execution quality and content support rather than game mode inclusion. A high-quality Singleplayer game is predicted to be just as successful as a high-quality Hybrid title.

## AI Disclosure
AI tools were used to generate some of the comments and trivial code snippets. All core analysis and conclusions are my own work.
