# 📱 Google Play Store — App Insights Analytics

> **10,841 apps | 34 categories | End-to-End Data Analysis**

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue?logo=python&logoColor=white)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter&logoColor=white)](https://jupyter.org/)
[![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-yellow?logo=powerbi&logoColor=white)](https://powerbi.microsoft.com/)
[![pandas](https://img.shields.io/badge/pandas-Data%20Analysis-green?logo=pandas&logoColor=white)](https://pandas.pydata.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-lightgrey)](LICENSE)

---

## 🌟 Situation

The Google Play Store hosts millions of apps across dozens of categories, yet most developers and product teams lack a clear, data-backed understanding of **what actually drives app success** — whether that's ratings, install volume, pricing, or audience targeting.

With over 10,000 apps in the dataset spanning 34 categories, the raw data held enormous potential but was riddled with quality issues: duplicate entries, malformed numeric fields (installs with `+` and `,` characters, sizes mixing `M` and `k` units), an erroneous 19.0 rating, and missing values across key columns. Without proper cleaning and structured analysis, any insight drawn from this data would be unreliable.

The need was clear: build a **rigorous, end-to-end analytics pipeline** that transforms messy raw data into trustworthy, decision-ready insights for app developers, product managers, and business strategists.

---

## 🎯 Task

The project aimed to answer eight core business questions:

1. Which **categories** dominate the Play Store by volume and install reach?
2. What **rating thresholds** meaningfully impact download numbers?
3. How does **Free vs. Paid** pricing affect installs, reviews, and ratings?
4. What is the relationship between **review volume and installs**?
5. How does **app size** influence user satisfaction and adoption?
6. Does **update recency** correlate with better ratings and installs?
7. Which **content ratings** (audience segments) are over- or under-served?
8. What combination of features are the **strongest predictors** of app success?

The deliverables were a cleaned dataset, a full exploratory analysis notebook with 18 publication-quality charts, and an interactive Power BI executive dashboard.

---

## ⚙️ Action

### 1. Data Cleaning Pipeline

A multi-step cleaning pipeline was built to transform the raw dataset into a reliable analytical foundation:

- **Deduplication** — Removed exact duplicate rows; for apps appearing multiple times, kept the record with the highest review count (most representative snapshot).
- **Rating sanitisation** — Capped ratings to the valid 1–5 range, removing a stray `19.0` data entry error.
- **Type filtering** — Removed a malformed `'0'` value in the `Type` column, retaining only `Free` and `Paid`.
- **Numeric parsing** — Stripped `,` and `+` from Installs; stripped `$` from Price; converted both to float.
- **Size normalisation** — Converted `M` (megabytes) and `k` (kilobytes) size strings to a unified numeric `SizeMB` column; tagged `'Varies with device'` as `NaN`.
- **Date parsing** — Converted `Last Updated` to `datetime`; extracted `YearUpdated` and `MonthUpdated` features.
- **Log transforms** — Applied `log1p` to Installs and Reviews to handle extreme right skew in distribution plots and correlations.

**Result:** 10,359 clean records from 10,841 raw rows — 482 rows removed.

### 2. Exploratory Data Analysis (11 Sections)

| Section | Key Technique |
|---|---|
| Dataset KPI Overview | Colour-coded KPI card layout |
| Distribution Analysis | Histograms with log-scale for skewed metrics |
| Category Performance | Bar charts + bubble chart (rating × installs × app count) |
| Rating Analysis | Band segmentation, avg installs by band |
| Install & Popularity | Tier distribution, top-20 apps, reviews–installs scatter |
| Pricing Strategy | Free vs Paid boxplots, paid price bands and ratings |
| Size Impact | Size band vs rating and installs |
| Update Frequency | Year-over-year rating and install trends |
| Audience Analysis | Content rating breakdown (count, rating, installs) |
| Correlation Analysis | Heatmap + pairplot coloured by app type |
| Executive Dashboard | 18-chart composite figure with KPI header row |

### 3. Power BI Dashboard (`App_Insights_-_Copy.pbix`)

An interactive executive dashboard was built in Power BI to complement the notebook, enabling non-technical stakeholders to explore the same findings through slicers, drill-downs, and dynamic visuals — including category filters, rating band selectors, and Free/Paid toggles.

### 4. Tools & Libraries

```
Python 3.8+    pandas · numpy · matplotlib · seaborn
Power BI       Interactive executive dashboard (.pbix)
Jupyter        Notebook-based reproducible analysis
```

---

## 📊 Result

### Key Findings

| # | Finding | Business Impact |
|---|---|---|
| 1 | **FAMILY & GAME** are the top 2 categories by app count and install volume | Prioritise these categories for new app investment |
| 2 | Apps rated **4.5+** receive significantly more installs than lower-rated peers | A 0.5-point rating improvement is not cosmetic — it's a growth lever |
| 3 | **Free apps get ~8× more installs** than paid apps on average | Default to free + in-app purchase monetisation |
| 4 | **Reviews and Installs** are strongly correlated (Pearson r ≈ 0.64) | In-app review prompts directly drive install momentum |
| 5 | Apps **updated in 2018** outperform stale, un-updated apps on both metrics | Quarterly releases maintain algorithmic and user trust |
| 6 | **10–50 MB apps** show the best balance of rating and install volume | Avoid bloated builds; optimise for mid-range device storage |
| 7 | 80%+ of apps target the "Everyone" audience — **Teen/Mature is underserved** | Adjacent audience segments represent a lower-competition opportunity |
| 8 | **Paid apps priced $4.99–$9.99** earn higher average ratings than cheaper paid tiers | Mid-range pricing signals quality and attracts more committed users |

### Predictive Insight

The strongest predictors of app install volume, in order:

```
1. Review count   2. Rating score   3. Category   4. Free / Paid status
```

### Visualisations Produced

18 figures covering KPI cards, distribution histograms, bubble charts, boxplots, heatmaps, pairplots, donut charts, and a composite executive dashboard — all saved as high-resolution PNG exports.

---

## 📁 Repository Structure

```
├── App_insight_Analysis.ipynb   # Full analysis notebook (11 sections, 18 charts)
├── App_Insights.pbix            # Power BI executive dashboard
├── README.md                    # This file
└── figures/                     # Exported chart PNGs (fig_01 – fig_18)
    ├── fig_01_kpi_overview.png
    ├── fig_02_distributions.png
    ├── ...
    └── fig_18_executive_dashboard.png
```

---

## 🚀 Getting Started

### Prerequisites

```bash
pip install pandas numpy matplotlib seaborn jupyter
```

### Run the Notebook

```bash
git clone https://github.com/your-username/app-insights-analytics.git
cd app-insights-analytics
jupyter notebook App_insight_Analysis.ipynb
```

> **Note:** Update the data path in Section 1 to point to your local copy of `googleplaystore.csv`. The dataset is available on [Kaggle](https://www.kaggle.com/datasets/lava18/google-play-store-apps).

### Open the Power BI Dashboard

Open `App_Insights.pbix` in [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free download). Refresh the data source connection if prompted.

---

## 🤝 Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you'd like to change.

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).
