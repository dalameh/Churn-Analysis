# Customer Churn & Customer Lifetime Value (CLV) Pipeline

This project delivers an end-to-end statistical modeling and machine learning pipeline for an e-commerce store. By analyzing raw transactional data, it predicts individual customer purchase behavior, calculates the **Probability of Life ($P_{Alive}$)**, and forecasts **Customer Lifetime Value (CLV)**. 

The technical intelligence is translated into a **Holistic 3x3 Strategic Matrix** (Segmenting Statistical Risk vs. Behavioral Urgency) to protect projected revenue and systematically mitigate churn.

---

## 📊 Pipeline Architecture & Project Phases

### Phase I: System Imports & Dependencies
The pipeline utilizes specialized libraries for probabilistic modeling, data processing, and predictive analytics:
* **Probabilistic Modeling:** `lifetimes` (BetaGeoFitter, GammaGammaFitter)
* **Machine Learning & Clustering:** `scikit-learn` (KMeans, RandomForestClassifier, StandardScaler)
* **Data Engine:** `pandas`, `numpy`, `sqlite3`, `openpyxl`
* **Interactive Visualizations:** `plotly`, `matplotlib`, `seaborn`

### Phase II: Data ETL & Comprehensive Cleaning
Processes multi-year transaction data from an Excel database to enforce strict structural integrity:
* **Heterogeneous Merging:** Combines individual sheets into a single core dataframe consisting of `1,067,371` rows across columns: `Invoice`, `StockCode`, `Description`, `Quantity`, `InvoiceDate`, `Price`, `Customer ID`, and `Country`.
* **Data Quality & Integrity Audit:** * **Missing Value Dropping:** Filters out `22.77%` of anonymous rows lacking a `Customer ID` to avoid skewing individual customer models.
* **Revenue Integrity Filtration:** Strips out transactions with $Quantity \le 0$ (returns/cancellations, including invoice prefix 'C') and $Price \le 0$ (errors/free items).

### Phase III: Probabilistic Modeling ($P_{Alive}$ & CLV)
Differentiates between a customer's natural purchase gap and high-risk structural churn using advanced non-contractual statistical models:
* **BG/NBD Model (Beta-Geometric/Negative Binomial Distribution):** Fits customer transaction data using Recency, Frequency ($x$), and Time ($T$) metrics to estimate future transaction rates and calculate the active lifecycle probability ($P_{Alive}$).
* **Gamma-Gamma Model:** Evaluates monetary value distribution. It calculates the expected average profit per transaction based on the assumption that monetary value is independent of transaction frequency.
* **CLV Pipeline Generation:** Merges both models to output a dollar-quantified, multi-month projected financial value for every unique customer id.

### Phase IV: Multi-Dimensional Customer Segmentation
Transforms calculated probabilistic statistics into actionable operational groups:
* **K-Means Clustering:** Standardizes data via `StandardScaler` and clusters customers across statistical, behavioral, and monetary axes.
* **Cluster Profiling:** Explicitly defines granular segments including *VIP / Champions*, *Loyal Legacy Buyers*, *Potentially Loyal/At-Risk*, and *One-Time New/Hibernating Buyers*.

### Phase V: Business Insights & Holistic 3x3 Strategic Matrix
Maps customers into an operationally clear 3x3 decision matrix to drive retention strategies:
* **Y-Axis (Statistical Risk):** $P_{Alive}$ Percentiles generated from the BG/NBD model.
* **X-Axis (Behavioral Urgency):** Days Overdue (time elapsed since the individual expected transaction cycle).
* **Strategic Deliverable:** Quantifies total revenue at risk within each matrix intersection, providing leadership with a precise roadmap to deploy win-back campaigns to high-value cohorts before churn occurs.

---

## 🚀 Quick Start & Installation

1. Clone this repository and ensure your transaction data file (`ecomm_transactions.xlsx` or equivalent) is placed in the project root folder.
2. Install dependencies:
```bash
pip install pandas numpy lifetimes scikit-learn matplotlib seaborn plotly openpyxl
