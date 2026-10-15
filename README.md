# Google Play Store Apps: EDA and Data Cleaning

An end-to-end data cleaning and exploratory data analysis (EDA) project on **10,800+ Google Play Store apps**: turning raw, messy text columns into analysis-ready numeric features, handling missing values and duplicates, and answering business questions about the Android app market.

📓 **Kaggle notebook:** [Google Play Store EDA](https://www.kaggle.com/code/muneeb2808/googleplaystore-eda)

---

## Problem

App developers need to know where the opportunity is before building a product. This project explores the Play Store to answer:

- Which categories have the most apps?
- Which categories drive the most installs?
- Which categories earn the highest user ratings?

## Dataset

- **Source:** [Google Play Store Apps](https://www.kaggle.com/datasets/lava18/google-play-store-apps) on Kaggle (by lava18)
- **Size:** 10,841 rows × 13 columns (raw) → 10,346 rows × 14 columns (after cleaning and feature engineering)
- **Columns:** `App`, `Category`, `Rating`, `Reviews`, `Size`, `Installs`, `Type`, `Price`, `Content Rating`, `Genres`, `Last Updated`, `Current Ver`, `Android Ver`

> The CSV (`googleplaystore.csv`) is not included in this repository. Download it from the Kaggle link above and place it in the project folder.

## Approach

1. **Data inspection:** shape, data types, descriptive statistics, and a malformed row (values shifted by one column) that was removed during null handling
2. **Fixing text columns that should be numeric**
   - `Size`: converted K and M units to MB (8,830 values in M, 316 in K); 1,695 "Varies with device" values filled with the category median
   - `Installs`: removed `+` and `,` and converted to integers
   - `Price`: removed the `$` sign and converted to float
3. **Missing values**
   - Dropped 12 rows with nulls in `Current Ver`, `Android Ver`, `Category`, `Type`, or `Genres`
   - `Rating` (13.6% missing) imputed with the mean rating of each install segment
4. **Duplicates:** removed 483 exact duplicate rows
5. **Feature engineering:** `Installs_category`, which groups apps into 8 segments from `no` installs to `Top Notch`
6. **Business questions:** answered with pandas `groupby` aggregations

## Key Findings

- **Most apps:** FAMILY (1,939), GAME (1,121), TOOLS (841), BUSINESS (427), MEDICAL (408)
- **Most installs (cumulative):** GAME (~31.5B), COMMUNICATION (~24.2B), SOCIAL (~12.5B), PRODUCTIVITY (~12.5B), TOOLS (~11.5B)
- **Highest average rating:** EVENTS (4.39), EDUCATION (4.37), ART_AND_DESIGN (4.36), BOOKS_AND_REFERENCE (4.36), PERSONALIZATION (4.33)
- **The market is mostly free:** in the raw data, 10,041 of 10,841 records (about 93%) have a price of $0, and the most expensive app costs $400
- **A typical app is small and modestly popular:** median size is about 12 MB and median installs are 100,000 (raw records)

## Tech Stack

Python · pandas · NumPy · Matplotlib · Seaborn · Jupyter

## How to Run

```bash
# 1. Clone the repository
git clone https://github.com/muneebaligit/Google-Playstore-Dataset-EDA.git
cd Google-Playstore-Dataset-EDA

# 2. Install dependencies
pip install -r requirements.txt

# 3. Download googleplaystore.csv from Kaggle and place it in this folder

# 4. Launch the notebook
jupyter notebook googleplaystore-eda.ipynb
```

Make sure the `pd.read_csv()` call in the notebook points to your local copy, for example `pd.read_csv('googleplaystore.csv')`.

## Project Structure

```
├── googleplaystore-eda.ipynb   # Full cleaning and EDA notebook
├── requirements.txt            # Python dependencies
└── README.md
```

## Limitations

- The data is a snapshot from 2018 (the most common `Last Updated` date is August 3, 2018), so current trends may differ.
- `Installs` is published as ranges (for example, "1,000,000+"), so summed installs are approximate lower bounds.
- Missing ratings were filled with install-segment means, which smooths the category rating averages slightly.
- 483 exact duplicate rows were removed; apps that share a name but differ in other fields were kept.

## Author

**Muneeb Ali**: aspiring Data Scientist and AI Engineer

[GitHub](https://github.com/muneebaligit) · [Kaggle](https://www.kaggle.com/muneeb2808) · [LinkedIn](https://www.linkedin.com/in/muneeblink/) · [X / Twitter](https://x.com/muneebalix)

If you found this useful, a ⭐ on the repo is appreciated.
