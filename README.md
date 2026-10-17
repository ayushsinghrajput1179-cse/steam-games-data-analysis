# Steam Store Games: Data Analysis & Visualization Using Python

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/ayushsinghrajput1179-cse/steam-games-data-analysis/blob/main/Steam_Games_Data_Analyses.ipynb)

Exploratory Data Analysis (EDA) on the **Steam Store Games** dataset using **Python, Pandas and Matplotlib**. The project cleans the data, analyses game prices, genres, platforms, ratings, playtime and release trends, and presents the findings through **eight visualizations** and a short insights report.

---

## Table of Contents

1. [Project Definition](#1-project-definition)
2. [Dataset and Use Case](#2-dataset-and-use-case)
3. [Data Cleaning](#3-data-cleaning)
4. [Visualizations and Outcomes](#4-visualizations-and-outcomes)
5. [Key Results](#5-key-results)
6. [Python Libraries and Tools](#6-python-libraries-and-tools)
7. [Repository Structure](#7-repository-structure)
8. [How to Run](#8-how-to-run)
9. [Short Insights Report](#9-short-insights-report)
10. [Project Timeline](#10-project-timeline)
11. [Conclusion](#11-conclusion)

---

## 1. Project Definition

This project performs Exploratory Data Analysis (EDA) on the Steam Store Games dataset obtained from Kaggle. It cleans the data, analyses game prices, genres, platforms, ratings, playtime and release trends, and presents the findings through eight Matplotlib visualizations and a short insights report.

The analysis helps to understand which genres dominate the Steam store, how games are priced, which titles are rated highest by players, which platforms are supported, and how the number of releases has changed over the years.

## 2. Dataset and Use Case

**Dataset:** Steam Store Games on Kaggle, with about 27,000 games collected from the Steam store and SteamSpy.
**Dataset link:** <https://www.kaggle.com/datasets/nikdavis/steam-store-games>

The dataset has several CSV files. This project uses the main file, **`steam.csv`** (27,075 rows and 18 columns):

| Column | Meaning |
|---|---|
| `appid` | Unique ID of the game |
| `name` | Name of the game |
| `release_date` | Date the game was released |
| `english` | Whether the game supports English (1 = yes) |
| `developer`, `publisher` | Company that made / published the game |
| `platforms` | Supported platforms (windows, mac, linux) |
| `required_age` | Minimum age needed to play |
| `categories`, `genres`, `steamspy_tags` | Categories, genres and user tags of the game |
| `achievements` | Number of achievements |
| `positive_ratings`, `negative_ratings` | Number of positive / negative reviews |
| `average_playtime`, `median_playtime` | Playtime in minutes |
| `owners` | Estimated number of owners (a range, for example `20000-50000`) |
| `price` | Price of the game |

**Use case:** game developers, publishers and gamers can use the results to understand popular genres, typical price ranges, platform support, highly rated games and release trends. This supports better decisions about game development, pricing and promotion.

## 3. Data Cleaning

| Step | What is done |
|---|---|
| **Missing values** | Missing text values (developer, publisher, genres, etc.) are replaced with `Unknown`. Missing numeric values are filled with the column median. |
| **Duplicates** | Repeated rows and repeated game IDs are found and removed. Repeated game names are only reported, because different games can share a name. |
| **Data types** | Numeric columns are converted, `release_date` becomes a date, and the `owners` range is split into low, high and middle values. Helper columns are added: release year, total ratings, positive-rating percentage and platform flags. |
| **Outliers** | Detected with the IQR rule (values above Q3 + 1.5 x IQR) for price, playtime and positive ratings. Outliers are **flagged, not deleted**, because expensive or long-played games are real games. They stay in the rankings and the scatter plot, and are left out of the histograms and box plot so the main pattern is readable. |

The original `steam.csv` is never changed. Cleaning is done on a copy and saved separately as `steam_cleaned.csv`.

## 4. Visualizations and Outcomes

Eight graphs are made with Matplotlib and saved in the `charts/` folder.

| # | Graph | Plot type | Purpose | Expected outcome |
|---|---|---|---|---|
| 1 | Top 10 Most Common Game Genres | Horizontal bar chart | Count the frequency of individual genres | Identify the genres most represented on Steam |
| 2 | Distribution of Game Prices | Histogram | See how prices are spread | Most games are low-priced, with a long tail of premium titles |
| 3 | Top 10 Games by Positive Ratings | Horizontal bar chart | Compare games by positive ratings | Identify games with the largest base of satisfied players |
| 4 | Platform Support Distribution | Pie chart | Compare Windows only, Windows + Mac, Windows + Linux and all three | Understand platform representation, with Windows expected to dominate |
| 5 | Game Price vs. Positive Ratings | Scatter plot | Explore the link between price and ratings | See whether higher-priced games get more or fewer positive ratings |
| 6 | Number of Games Released per Year | Line chart | See how releases changed over time | Show the growth of the Steam store and the busiest years |
| 7 | Distribution of Average Playtime | Histogram | See how long players typically play | Identify common playtime ranges and long-played titles |
| 8 | Game Prices by Genre | Box plot | Compare prices across the top 5 genres | Compare medians, variability and outliers between genres |

## 5. Key Results

Results from running the notebook on `steam.csv`:

- **Data quality:** 27,075 games, 18 columns. Only 1 developer and 14 publisher values were missing (filled with `Unknown`). No duplicate rows, unreadable dates or negative values were found.
- **Outliers flagged:** 1,455 in price, 726 in playtime and 4,150 in positive ratings.
- **Genres:** *Indie* is the most common genre (19,421 games), followed by *Action* and *Casual*.
- **Prices:** 9.5% of games are free. The median price of paid games is 4.79, and 79.9% of paid games cost 10 or less.
- **Ratings:** *Counter-Strike: Global Offensive* has the most positive ratings (2,644,404).
- **Platforms:** almost every game supports Windows, and only 17.1% support Windows, Mac and Linux together.
- **Release trend:** 2018 had the most releases (8,160 games). The data ends in May 2019, so 2019 is only a partial year.
- **Playtime:** 77.2% of games have no recorded playtime. For the rest, the median average playtime is 3.3 hours.
- **Price vs. ratings:** the Spearman correlation is 0.21, a weak positive relationship.

## 6. Python Libraries and Tools

- **Pandas:** data loading, cleaning, grouping and calculations
- **NumPy:** numerical operations
- **Matplotlib:** bar charts, histograms, pie chart, scatter plot, line chart and box plots
- **Google Colab / Jupyter Notebook:** running the notebook
- **Git and GitHub:** version control, hosting and documentation

## 7. Repository Structure

```text
steam-games-data-analysis/
├── README.md                          # Project documentation (this file)
├── requirements.txt                   # Python libraries needed
├── .gitignore                         # Files Git should ignore
├── Steam_Games_Data_Analyses.ipynb    # Colab notebook with all steps and outputs
├── steam.csv                          # Original dataset (raw, unchanged)
├── steam_cleaned.csv                  # Dataset after cleaning
└── charts/                            # The 8 graphs (PNG)
    ├── graph1_top_genres.png
    ├── graph2_price_distribution.png
    ├── graph3_top_positive_ratings.png
    ├── graph4_platform_support.png
    ├── graph5_price_vs_ratings.png
    ├── graph6_releases_per_year.png
    ├── graph7_playtime_distribution.png
    └── graph8_price_by_genre.png
```

## 8. How to Run

### Option A: Google Colab (easiest)

1. Click the **Open In Colab** badge at the top, or open the `.ipynb` file in [Google Colab](https://colab.research.google.com/).
2. Download `steam.csv` from the [Kaggle dataset](https://www.kaggle.com/datasets/nikdavis/steam-store-games) (or use the copy in this repository).
3. In **Step 2** of the notebook choose how to load the file:
   - `choice = "upload"` to upload `steam.csv` from your computer, or
   - `choice = "drive"` to read it from Google Drive (set `drive_path` to where you saved it).
4. Run all cells (**Runtime > Run all**).
5. The last steps save `steam_cleaned.csv` and `charts.zip`, and download them to your computer.

### Option B: On your own computer

1. Clone the repository and install the libraries:

   ```bash
   git clone https://github.com/ayushsinghrajput1179-cse/steam-games-data-analysis.git
   cd steam-games-data-analysis
   pip install -r requirements.txt
   ```

2. Start Jupyter and open the notebook:

   ```bash
   jupyter notebook Steam_Games_Data_Analyses.ipynb
   ```

3. Step 2 and the last download cell use Google Colab features. On your own computer, replace the Step 2 code with `raw = pd.read_csv("steam.csv")` and skip the last download cell.

## 9. Short Insights Report

**Data quality**
The raw dataset was checked for missing values, duplicate records, incorrect data types and outliers in price, playtime and ratings. Missing developer and publisher values were filled and outliers were flagged.

**Key findings**
Indie and Action games dominate the store, most paid games are low-priced, and the number of releases grew sharply until 2018. Windows is supported by almost every game, while full Windows + Mac + Linux support is much rarer.

**Recommendations**
- Developers in crowded genres such as Indie need a clear point of difference to be noticed.
- Higher prices need strong reviews and clear value, because most paid games cost 10 or less.
- Supporting Mac and Linux in addition to Windows can reach players that fewer games target.
- Launch timing and marketing deserve planning in busy release years.

**Limitations**
- The dataset is a snapshot of the Steam store (collected in 2019), so newer games and current trends are not included.
- Owner counts are ranges, not exact numbers, and there is no sales revenue data.
- Ratings come only from players who chose to leave a review.
- The analysis shows patterns, but it does not prove why players prefer certain games.

## 10. Project Timeline

| Step | Task | Time |
|---|---|---|
| 1 | Explore the dataset and understand the columns | 1 day |
| 2 | Clean the data and perform outlier analysis | 2 days |
| 3 | Create the visualizations and analyse the findings | 2 days |
| 4 | Write the report and README, and upload the project to GitHub | 2 days |

## 11. Conclusion

This project covers the complete data analysis workflow using a real-world Steam games dataset. It delivers a cleaned dataset, eight visualizations, a short insights report and a GitHub repository containing the complete Python analysis project.

---

**GitHub repository:** <https://github.com/ayushsinghrajput1179-cse/steam-games-data-analysis>
**Dataset credit:** Nik Davis, *Steam Store Games*, Kaggle. <https://www.kaggle.com/datasets/nikdavis/steam-store-games>
