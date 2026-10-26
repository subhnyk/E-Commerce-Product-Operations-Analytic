# E-Commerce / Supply Chain Analytics

End-to-end analytics on **180,519 orders** and **469,977 website sessions** from the DataCo supply-chain dataset - covering data cleaning, KPI analysis, hypothesis testing, machine-learning modelling, and an executive PowerPoint deck.

![Status](https://img.shields.io/badge/status-complete-brightgreen)
![Python](https://img.shields.io/badge/python-3.11%20%7C%203.13-blue)
![License](https://img.shields.io/badge/license-MIT-lightgrey)

---

## Project Overview

| | |
|---|---|
| **Domain** | E-commerce / Supply Chain Operations |
| **Datasets** | DataCoSupplyChainDataset.csv (180,519 orders), tokenized_access_logs.csv (469,977 page views) |
| **Period** | 2015-01 to 2018-01 |
| **Tools** | Python, Jupyter, scikit-learn, Power BI |
| **Deliverables** | Analysis notebook, Power BI dashboard, 28-slide presentation deck |

---

## Repository Structure

```
Supply_Chain_Analytics/
  Analysis.ipynb                           # 153-cell end-to-end analysis (8 phases)
  SupplyChainAnalytics.pbix                # Power BI dashboard
  Supply_Chain_Analytics_Presentation.pptx # 28-slide executive deck
  README.md                                # this file
  requirements.txt                         # pinned Python dependencies
  .gitignore                               # ignores venv, build artifacts, caches
  .venv/                                   # (local) project virtual environment
  charts/                                  # (local) PNG charts used in the deck
  data/
    raw/
      DataCoSupplyChainDataset.csv
      DescriptionDataCoSupplyChain.csv
      tokenized_access_logs.csv
```

---

## Environment Setup

Create an isolated environment so packages do not clash with system Python.

### Option A - plain venv (recommended)

```bash
cd "C:\Users\sajal dhuriya\OneDrive\Desktop\Supply_Chain_Analytics"
python -m venv .venv
.venv\Scripts\activate
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### Option B - Conda

```bash
conda create -n supply-chain python=3.11 -y
conda activate supply-chain
pip install -r requirements.txt
```

### Register the env as a Jupyter kernel (optional)

```bash
pip install ipykernel
python -m ipykernel install --user --name=supply-chain --display-name "Python (supply-chain)"
jupyter notebook Analysis.ipynb
```

Then in the browser pick **Kernel -> Python (supply-chain) -> Restart & Run All**.

---

## Notebook Phases (Analysis.ipynb)

| # | Phase | Highlights |
|---|---|---|
| 1 | Data Understanding and Preprocessing | 180,519 x 53 features; dropped 2 high-null columns; 0 duplicates |
| 2 | Univariate (KPI) Analysis | Total Sales $36.78M, Late rate 54.83%, 2.13 items/order |
| 3 | Bivariate Analysis | 12 relationship pairs - profit drivers, logistics dependencies |
| 4 | Multivariate Analysis | Region x Mode x Late Risk, Discount x Category x Profit |
| 5 | Distributions and CLT | Log-normal sales, Bernoulli late risk, CLT verified |
| 6 | Hypothesis Testing | t-test, Chi-square, ANOVA - with effect sizes |
| 7 | Feature Engineering | 10 ML features, 80/20 stratified split, 62 encoded columns |
| 8 | Machine Learning | Tuned Random Forest classifier (Recall 0.55), Regression (R-squared 0.015) |

---

## Dashboard (SupplyChainAnalytics.pbix)

Five pages:
1. **Overview** - KPI tiles (Sales, Profit, Orders, Late %)
2. **Profitability** - Sales vs Profit by Category, Discount impact
3. **Logistics** - Late Delivery heatmap (Region x Shipping Mode)
4. **Customers** - Segment contribution, top regions
5. **ML Output** - Confusion matrix, classification report, feature importance

---

## Headline Findings

- **$36.78M** total sales across 180,519 orders, average $203.77/order
- **54.83%** of orders flagged late - a coin flip per order
- **First Class** is the worst shipping mode for lateness (**95.32%** late)
- **Standard Class** is the most reliable (**38.07%** late) - counterintuitive but explained by order type
- **Europe + LATAM** = **57.80%** of total profit
- **Discounts are a double-edged sword**: lift Electronics/Cardio margin, destroy Apparel/Footwear margin
- Top late-delivery regions (Canada, Caribbean, Central Asia, East Africa, East of USA) all exceed **90%** late rate for First Class

---

## Recommendations

1. **Cap discount at the 75th-percentile ($29.99)** - protects margin in apparel/footwear
2. **Re-route First/Second Class orders** in regions with >90% late rate
3. **Deploy the tuned Random Forest late-delivery classifier** into order-routing
4. **Focus growth investment** on Europe + LATAM and Fishing/Cleats/Camping categories
5. **Re-train models quarterly** with carrier + inventory data

---

## Tech Stack

pandas, numpy, matplotlib, seaborn, plotly, scikit-learn, scipy, jupyter, nbformat, python-pptx, Pillow

---

## Reproduce the PPT deck (optional)

```bash
python _build_charts.py     # regenerates charts/*.png
python _build_pptx.py       # rebuilds Supply_Chain_Analytics_Presentation.pptx
```

Both scripts are kept locally and ignored by .gitignore.

---

## License

MIT - feel free to reuse with attribution.

---

## Author

Generated as a portfolio analytics project, 2026.
