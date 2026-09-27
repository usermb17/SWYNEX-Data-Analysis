# SWYNEX-Data-Analytics


# Customer Purchase Analysis & Business Insights Dashboard

[![Python 3.8+](https://img.shields.io/badge/Python-3.8%2B-blue.svg)](https://www.python.org/)
[![Pandas](https://img.shields.io/badge/Library-Pandas-orange.svg)](https://pandas.pydata.org/)
[![Power BI](https://img.shields.io/badge/BI-Power%20BI-yellow.svg)](https://powerbi.microsoft.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT)

An end-to-end data analytics and business intelligence project analyzing transactional records, demographic spending drivers, and post-purchase customer satisfaction across South Asian regional markets.

---

## Table of Contents
1. [Project Overview & Problem Statement](#1-project-overview--problem-statement)
2. [Dataset Information & Schema](#2-dataset-information--schema)
3. [Data Cleaning & Preprocessing](#3-data-cleaning--preprocessing)
4. [Exploratory Data Analysis (EDA) & Charts](#4-exploratory-data-analysis-eda--charts)
5. [Dashboard Architecture & Wireframe](#5-dashboard-architecture--wireframe)
6. [Key Business Insights & Actionable Strategies](#6-key-business-insights--actionable-strategies)
7. [Repository Structure & Setup Instructions](#7-repository-structure--setup-instructions)
8. [Submission Details](#8-submission-details)

---

## 1. Project Overview & Problem Statement

### Context
Modern enterprise retail platforms accumulate large quantities of transactional logs. Without structured pipeline validation, exploratory analysis, and executive dashboarding, organizations face blind spots regarding:
- High-volume revenue drivers versus high average-basket-value categories.
- Demographic spending power disparities across customer segments.
- Early warning signs in post-purchase satisfaction that lead to customer churn.

### Objectives
- **Ingest & Validate:** Clean and audit 500 transaction records from `python_practice_dataset.xlsx`.
- **Demographic Segmentation:** Analyze spending dynamics across gender, age groups, and geographical markets.
- **Product Category Evaluation:** Compare Gross Merchandise Value (GMV) against Average Order Value (AOV).
- **Customer Satisfaction Tracking:** Identify customer rating patterns across categories to address operational pain points.
- **BI Visual Delivery:** Build an interactive executive dashboard design in Power BI / Python.

---

## 2. Dataset Information & Schema

The dataset consists of 500 customer transactions with 9 feature columns:

- **Total Records:** 500
- **Total Attributes:** 9
- **Gross Revenue (GMV):** 4,957,478
- **Average Order Value (AOV):** 9,914.96
- **Overall Mean Rating:** 2.98 / 5.00
- **Age Distribution:** 18 – 59 years (Mean: 39.3 years)
- **Covered Markets:** India, Pakistan, Bangladesh, Nepal, Sri Lanka, Afghanistan
- **Product Categories:** Clothing, Furniture, Books, Toys, Electronics, Grocery

### Data Dictionary

| Column Name | Data Type | Null Count | Description |
| :--- | :--- | :--- | :--- |
| `ID` | Integer | 0 | Unique customer transaction identifier |
| `Name` | String | 0 | Full customer profile name |
| `Age` | Integer | 0 | Customer age in years |
| `Gender` | String | 0 | Customer gender (`Female`, `Male`) |
| `Country` | String | 0 | Operating country/market |
| `Join_Date` | Datetime | 0 | Platform registration timestamp |
| `Purchase_Amount` | Numeric | 0 | Monetary transaction value |
| `Product_Category` | String | 0 | Merchandising vertical |
| `Rating` | Numeric | 0 | Post-purchase review score (1.0 to 5.0) |

---

## 3. Data Cleaning & Preprocessing

The dataset was audited and transformed using Python (`pandas`):

```python
import pandas as pd

# Load dataset
df = pd.read_excel('python_practice_dataset.xlsx')

# Data quality audits
null_summary = df.isnull().sum()
duplicate_count = df.duplicated().sum()
unique_id_count = df['ID'].nunique()

# Type casting and normalization
df['Join_Date'] = pd.to_datetime(df['Join_Date'])
df['Purchase_Amount'] = pd.to_numeric(df['Purchase_Amount'])
df['Rating'] = pd.to_numeric(df['Rating'])

print(f"Dataset clean status: {duplicate_count == 0 and null_summary.sum() == 0}")
```

### Preprocessing Audit Summary
| Validation Step | Method | Result | Outcome |
| :--- | :--- | :--- | :--- |
| **Missing Values** | `isnull().sum()` | 0 nulls detected | Complete dataset; no imputation required |
| **Duplicate Rows** | `duplicated().sum()` | 0 duplicates | Entire dataset is unique |
| **Primary Key Audit** | `nunique()` on `ID` | 500 / 500 unique | 100% relational integrity |
| **Data Types** | `dtypes` verification | Validated datetime & float | Stored in standard analytical types |
| **Value Boundaries** | Range check | `Rating`: 1–5, `Age`: 18–59 | Zero out-of-bound anomalies |

---

## 4. Exploratory Data Analysis (EDA) & Charts

### A. Product Category Performance
| Product Category | Order Volume | Gross Revenue | Average Order Value (AOV) | Mean Rating |
| :--- | :--- | :--- | :--- | :--- |
| **Clothing** | 96 | 968,014 | 10,083.48 | 2.91 |
| **Furniture** | 89 | 935,008 | 10,505.71 | 3.20 |
| **Books** | 77 | 851,866 | 11,063.19 | 3.04 |
| **Toys** | 92 | 839,527 | 9,125.29 | 2.90 |
| **Electronics** | 79 | 744,760 | 9,427.34 | 2.87 |
| **Grocery** | 67 | 618,303 | 9,228.40 | 2.93 |

```text
Revenue by Product Category (GMV in Thousands):
Clothing    [████████████████████████████████] 968K (19.5%)
Furniture   [███████████████████████████████ ] 935K (18.9%)
Books       [████████████████████████████    ] 852K (17.2%)
Toys        [██████████████████████████      ] 840K (16.9%)
Electronics [████████████████████████        ] 745K (15.0%)
Grocery     [████████████████████            ] 618K (12.5%)
```

### B. Customer Gender Spending Dynamics
| Gender | Customer Count | Volume Share | Total Spend | Average Spend | Spend Share |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Female** | 252 | 50.4% | 2,632,213 | 10,445.29 | 53.1% |
| **Male** | 248 | 49.6% | 2,325,265 | 9,376.07 | 46.9% |

```text
Gross Revenue Contribution by Gender:
Female (53.1%) [███████████████████████████                    ] 2,632,213
Male   (46.9%) [████████████████████████                       ] 2,325,265
```

### C. Geographic Market Distribution
| Country | Customer Count | Market Share (%) |
| :--- | :--- | :--- |
| **Pakistan** | 92 | 18.4% |
| **Sri Lanka** | 86 | 17.2% |
| **Bangladesh** | 85 | 17.0% |
| **Nepal** | 81 | 16.2% |
| **India** | 78 | 15.6% |
| **Afghanistan** | 78 | 15.6% |

```text
Customer Concentration by Country:
Pakistan    (92) [████████████████████████████████] 18.4%
Sri Lanka   (86) [██████████████████████████████  ] 17.2%
Bangladesh  (85) [█████████████████████████████   ] 17.0%
Nepal       (81) [████████████████████████████    ] 16.2%
India       (78) [███████████████████████████     ] 15.6%
Afghanistan (78) [███████████████████████████     ] 15.6%
```

### D. Customer Satisfaction Ratings (1.0 to 5.0)
```text
Average Rating by Category:
Furniture   [████████████████████████████████] 3.20 (Top Performer)
Books       [██████████████████████████████  ] 3.04
Grocery     [█████████████████████████████   ] 2.93
Clothing    [█████████████████████████████   ] 2.91
Toys        [████████████████████████████    ] 2.90
Electronics [████████████████████████████    ] 2.87 (Bottom Performer)
--------------------------------------------------
Benchmark Average: 2.98 / 5.00
```

---

## 5. Dashboard Architecture & Wireframe

### Multi-Panel Analytics Dashboard
The generated visual analytics suite visualizes category revenue, gender split, country volumes, and customer ratings:

![Dashboard Charts](visuals/dashboard_charts.png)

### Power BI Canvas Wireframe Layout
```
+---------------------------------------------------------------------------------------------------------+
|                                CUSTOMER PURCHASE & BUSINESS INSIGHTS DASHBOARD                          |
+---------------------+---------------------+-----------------------+-------------------------------------+
| TOTAL REVENUE (GMV) | TOTAL TRANSACTIONS  | AVERAGE BASKET VALUE  | CSAT SCORE                          |
| 4.96M               | 500                 | 9,914.96              | 2.98 / 5.00                         |
+---------------------+---------------------+-----------------------+-------------------------------------+
| SLICERS / FILTERS:  [Country: All v]   [Gender: All v]   [Category: All v]   [Join Date: Slider]        |
+-------------------------------------------+-------------------------------------------------------------+
| TOTAL PURCHASE AMOUNT BY CATEGORY         | REVENUE BREAKDOWN BY GENDER                                 |
| (Horizontal Bar Chart)                    | (Donut Chart)                                               |
| - Clothing:    968K                       | - Female: 2.63M (53.1%)                                     |
| - Furniture:   935K                       | - Male:   2.33M (46.9%)                                     |
| - Books:       852K                       +-------------------------------------------------------------+
| - Toys:        840K                       | CUSTOMER COUNT BY COUNTRY                                   |
| - Electronics: 745K                       | (Bar Chart)                                                 |
| - Grocery:     618K                       | Pakistan (92) | Sri Lanka (86) | Bangladesh (85)            |
|                                           | Nepal (81)    | India (78)     | Afghanistan (78)           |
+-------------------------------------------+-------------------------------------------------------------+
| AVERAGE CUSTOMER RATING BY CATEGORY       | REVENUE DRILLDOWN MATRIX                                    |
| (Column Chart: 0.0 - 5.0)                 | (Tabular Matrix with Cross-filtering)                       |
| - Furniture:   3.20                       | Country | Category | Transactions | Total Spend | Rating |
| - Books:       3.04                       | [Allows interactive multi-level dynamic slice and drill]    |
| - Electronics: 2.87 (Critical)            |                                                             |
+-------------------------------------------+-------------------------------------------------------------+
```

---

## 6. Key Business Insights & Actionable Strategies

1. **Capitalize on High-Ticket Categories (Books & Furniture):**
   - **Insight:** While Clothing drives gross sales volume (968K across 96 orders), **Books** achieves the highest individual average order value at 11,063.19, followed closely by **Furniture** at 10,505.71.
   - **Action:** Develop high-margin cross-sell bundles (e.g., educational collections, home office setups) to maximize transaction sizes for premium customers.

2. **Remediate Electronics Satisfaction Deficit:**
   - **Insight:** **Electronics** ranks lowest in customer satisfaction (2.87 / 5.00) and accounts for only 15.0% of total revenue.
   - **Action:** Audit warranty policies, product packaging, and vendor reliability. Implement automated post-delivery check-ins within 48 hours to handle troubleshooting before dissatisfaction occurs.

3. **Tailor Campaigns to High-Spending Female Demographics:**
   - **Insight:** Female customers spend **11.4% more per transaction** than male buyers (10,445.29 vs. 9,376.07) and contribute 53.1% of gross revenue.
   - **Action:** Introduce personalized loyalty tiers, category-specific early-access sales, and tailored email sequences highlighting top-converting categories for female cohorts.

4. **Regional Merchandising & Supply Chain Alignment:**
   - **Insight:** Pakistan represents the largest single user base (92 records, 18.4%), while India and Afghanistan represent 78 records (15.6%) each.
   - **Action:** Optimize localized payment gateways, offer domestic parcel fulfillment in key logistics hubs (Pakistan and Sri Lanka), and target under-penetrated markets with dedicated acquisition campaigns.

---

## 7. Repository Structure & Setup Instructions

```text
customer-purchase-analysis/
├── README.md                          # Comprehensive project documentation
├── requirements.txt                   # Python dependencies
├── data/
│   └── python_practice_dataset.xlsx   # Cleaned source dataset
├── notebooks/
│   └── customer_analysis.ipynb        # Data cleaning, EDA, and statistical routines
├── visuals/
│   └── dashboard_charts.png           # Exported visual dashboard panels
└── dashboard/
    └── customer_insights.pbix         # Power BI interactive report file
```

### Installation & Reproduction

1. **Clone the repository:**
   ```bash
   git clone https://github.com/<your-username>/customer-purchase-analysis.git
   cd customer-purchase-analysis
   ```

2. **Set up a virtual environment:**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows use: venv\Scripts\activate
   ```

3. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Execute the analysis script:**
   ```bash
   jupyter notebook notebooks/customer_analysis.ipynb
   ```

---

## 8. Submission Details

- **Project Repository:** `https://github.com/<your-username>/customer-purchase-analysis`
- **Dashboard File:** Power BI Report located in `/dashboard/customer_insights.pbix`
- **Contact / Author:** Data Analytics Team
