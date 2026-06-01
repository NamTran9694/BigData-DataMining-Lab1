# MSCS 634 - Lab 1: Data Visualization, Preprocessing, and Statistical Analysis

## Purpose
The purpose of this lab is to apply core data analytics techniques using Python and Jupyter Notebook
on a real-world retail dataset (Sample Superstore). The lab covers four main areas:
- Loading and exploring a dataset using Pandas
- Creating meaningful visualizations to uncover patterns and trends
- Preprocessing the data by handling missing values, removing outliers, reducing dimensions, and scaling features
- Performing statistical analysis to summarize and understand the data

---

## Dataset
**Source:** Sample Superstore Dataset — [Kaggle](https://www.kaggle.com/datasets/vivek468/superstore-dataset-final)  
**Size:** ~9,994 rows × 21 columns  
**Description:** Retail transaction records from a US superstore covering orders from 2014–2017,
including sales, profit, discount, product category, customer segment, and region.

---

## Key Insights

### Visualizations
| Chart | Insight |
|---|---|
| Scatter Plot (Sales vs Profit) | Higher sales do not always mean higher profit — many transactions fall below zero profit due to heavy discounting |
| Line Plot (Monthly Sales Trend) | Sales show a consistent upward trend year-over-year with Q4 peaks every year, likely driven by holiday shopping |
| Bar Chart (Sales by Region) | The West region leads total sales, followed by East — coastal regions outperform interior ones |
| Histogram (Discount Distribution) | Most transactions have 0–20% discount; very high discounts (>50%) are rare but are the main cause of losses |
| Box Plot (Profit by Category) | Furniture has a median profit near zero with frequent losses; Technology has the highest and most variable profit |
| Pie Chart (Sales by Segment) | Consumer segment accounts for ~50% of total sales, making it the most important customer group |

### Statistical Measures
- The mean Sales value after outlier removal was approximately **$226**, with a standard deviation of **$185**
- Profit ranged from large losses to large gains, confirming high variability in transaction profitability
- **Discount and Profit showed a strong negative correlation** — the most critical finding, meaning the more discount applied, the less profit the store makes
- Sales and Profit had a moderate positive correlation, while Quantity showed very little correlation with either

---

## Preprocessing Decisions

| Step | Decision | Reason |
|---|---|---|
| Missing Values | Filled Postal Code nulls with 0; dropped rows missing Sales/Profit | Postal Code is non-critical; Sales and Profit are essential for analysis |
| Outlier Removal | Used IQR method on the Sales column | IQR is robust to non-normal distributions and removed extreme high-value transactions |
| Data Reduction | Dropped admin columns (Row ID, Customer Name, Product ID, etc.); sampled 70% of rows | These columns add no analytical value; sampling reduces computation while preserving patterns |
| Scaling | Min-Max on Sales and Quantity; Z-score on Profit | Min-Max works well for bounded features; Z-score is better for Profit which has negative values |
| Discretization | Discount grouped into: No Discount, Low, Medium, High | Makes discount impact easier to analyze and visualize categorically |

---

## Challenges Faced

1. **Handling Skewed Discount Data** — The discount column was heavily skewed toward zero,
   with most transactions having little or no discount. This made it necessary to use
   discretization (grouping into categories) rather than using the raw values directly
   for meaningful analysis.

2. **Profit Outliers Across Categories** — The Profit column contained extreme values
   (both large gains and large losses), making visualization difficult. Deciding whether
   to remove or keep these outliers required careful consideration since they represent
   real business events such as bulk discounts and product returns.

3. **Choosing the Right Scaling Method** — Different numeric columns had different
   distributions. Sales and Quantity were strictly positive and bounded, making Min-Max
   scaling appropriate. Profit had negative values and a wider spread, making Z-score
   standardization a better fit.

4. **Imbalanced Category Representation** — The dataset had significantly more
   Office Supplies transactions than Furniture or Technology. This imbalance had to
   be considered when interpreting average statistics, as Office Supplies could
   disproportionately influence overall means and totals.
---

## Repository Structure
```
MSCS_634_Lab_1/
├── Lab1_DataMining_SuperStore.ipynb   # Main Jupyter Notebook
├── Sample - Superstore.csv           # Dataset
├── README.md                         # This file
└── screenshots/
    ├── viz_scatter.png
    ├── viz_line.png
    ├── viz_bar.png
    ├── viz_histogram.png
    ├── viz_boxplot.png
    ├── viz_pie.png
    └── viz_correlation.png
```
