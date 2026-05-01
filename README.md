# 📊 Retail Business Analytics Pipeline

> **A real-world data analytics engagement** conducted for a live food & beverage business — covering data infrastructure design, 87 days of operational data collection, SKU-level profitability analysis, and actionable recommendations that directly improved the owner's pricing and expansion decisions.

[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat&logo=python&logoColor=white)](https://python.org)
[![pandas](https://img.shields.io/badge/pandas-Data_Analysis-150458?style=flat&logo=pandas&logoColor=white)](https://pandas.pydata.org)
[![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualisation-11557C?style=flat)](https://matplotlib.org)
[![Jupyter](https://img.shields.io/badge/Notebook-Jupyter-F37626?style=flat&logo=jupyter&logoColor=white)](https://jupyter.org)
[![IIT Madras](https://img.shields.io/badge/IIT_Madras-BDM_Capstone-003580?style=flat)](https://study.iitm.ac.in)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat)](LICENSE)

---

## 📌 Overview

This is not a practice dataset project. This was a **real consulting engagement** with a functioning small business — *Shubham Sweet Corner*, a food & beverage shop in Saharsa, Bihar — conducted as the **Business Data Management (BDM) Capstone** for the IIT Madras BS in Data Science programme.

The business had no digital records, no pricing strategy grounded in margin data, and no visibility into which products were actually driving profitability. The owner was making daily decisions — pricing, staffing, what to stock — entirely on intuition and memory.

This project built the entire data infrastructure from scratch: designed the tracking system, collected 87 days of operational records across sales, expenses, employee costs, and pricing, then ran a full analytical pipeline to surface insights that the owner could act on immediately.

**The data is not included in this repository** to protect the confidentiality of the business and its owner. The full analysis methodology, findings, and recommendations are documented here and in the attached project reports.

---

## 🏪 Business Context

| Detail | Value |
|--------|-------|
| Business Name | Shubham Sweet Corner |
| Type | Small B2C Food & Beverage Shop |
| Location | Saharsa, Bihar, India |
| Operating Hours | 7 AM – 9 PM, 7 days/week |
| Employees | 3 |
| Data Collection Period | 87 operational days |
| Products | Snacks, Sweets, Dairy, Beverages |

**Product categories tracked:**

- **Snacks:** Samosa, Litti
- **Sweets:** Rasgulla, Laddoo, Gulab Jamun
- **Dairy:** Milk, Paneer, Dahi
- **Beverages:** Seasonal drinks

---

## 🎯 Business Problem

Small offline businesses in India's Tier-2 and Tier-3 cities commonly operate without any digital data infrastructure. The consequences are concrete and recurring:

**The owner couldn't answer basic questions like:**
- Which products are actually profitable, not just high-volume?
- Is the business growing, stable, or quietly declining month-over-month?
- Are labour and variable costs eating into margins during slow periods?
- What would happen to profit if a high-selling product's price changed by ₹2?

Without records, these questions have no answers. The business was running blind — not because the owner lacked intelligence, but because no one had ever built the system to capture and surface this information.

This project built that system.

---

## 🗂️ Data Infrastructure Design

Before any analysis, the data collection framework itself had to be designed. There was no existing system to pull from — every sheet was created from scratch based on what questions the business needed to answer.

### Data schema

**Sheet 1 — Product Pricing Master**

Captured cost price, selling price, and unit profit margin for every SKU. This became the foundation for all profitability analysis downstream.

| Column | Description |
|--------|-------------|
| `product_name` | SKU identifier |
| `cost_price` | Raw material + preparation cost per unit (₹) |
| `selling_price` | Price charged to customer (₹) |
| `unit_profit` | Selling price minus cost price (₹) |
| `margin_pct` | Unit profit as % of selling price |

**Sheet 2 — Daily Sales Log**

Recorded quantity sold and revenue for every product, every day, for 87 consecutive operating days. This is the core dataset for all time-series and correlation analysis.

| Column | Description |
|--------|-------------|
| `date` | Operating day |
| `product_name` | SKU sold |
| `quantity_sold` | Units sold that day |
| `daily_revenue` | Revenue from that SKU (₹) |

**Sheet 3 — Employee Cost Tracking**

Daily labour cost by employee, enabling accurate profit calculation rather than rough estimates.

**Sheet 4 — Variable Expenses Log**

Daily gas, electricity, and miscellaneous costs — tracked separately to understand how fixed vs variable cost behaviour affects margins across high and low revenue days.

---

## 🔍 Analysis Pipeline

### Phase 1 — Data Cleaning & Preprocessing

Raw Excel sheets contained the messy reality of manual daily entry: missing values on shop closure days, mixed date formats, string-encoded numeric fields, and occasional duplicate rows.

The cleaning pipeline handled:
- Closed-day NaN imputation (revenue = 0, not missing)
- `datetime` parsing and standardisation across inconsistent date formats
- Type coercion for all numeric fields (quantity, revenue, cost)
- Removal of metadata rows accidentally included in data ranges
- Column name normalisation for programmatic access

All cleaning was done programmatically in pandas — no manual Excel edits — so the pipeline is fully reproducible.

### Phase 2 — Descriptive Statistics

Computed summary statistics across the full 87-day window to establish the business baseline:

| Metric | Value |
|--------|-------|
| Average Daily Revenue | ₹10,333 |
| Average Daily Profit | ₹2,024 |
| Average Profit Margin | 19.6% |
| Revenue Stability | ±5% day-to-day variation |
| Total Days Analysed | 87 operational days |

The ±5% revenue stability finding was significant — it indicated that demand was predictable and consistent, which meant pricing changes (rather than volume growth) were the most reliable lever for improving profitability.

### Phase 3 — SKU-Level Profitability Analysis

This phase answered the question the owner could not previously answer: *which products are actually worth selling?*

Every SKU was analysed across three dimensions — volume contribution, revenue contribution, and margin contribution — because a high-selling product can be a profit drag if its margin is poor.

**Key finding: Samosa is a volume trap.**

Samosa was the highest-selling product by units. But at ₹10/unit with a 6% margin, it contributed disproportionately to cost and labour while delivering minimal profit per unit. It was driving footfall, not profit.

**Paneer and sweets were the real profit drivers.**

| Product | Margin | Revenue Correlation | Role |
|---------|--------|-------------------|------|
| Samosa | 6% | Weak / negative | Footfall driver |
| Paneer | High | 0.62 | Primary profit driver |
| Gulab Jamun | High | 0.54 | High-margin upsell |
| Rasgulla | High | 0.53 | Consistent margin contributor |
| Laddoo | Medium | 0.48 | Steady volume + margin |

### Phase 4 — Revenue Correlation Analysis

Correlation analysis was run between individual SKU daily sales and total daily revenue to identify which products, when they sell well, actually lift the whole business — versus products that sell consistently but don't move the revenue needle.

```
Revenue correlation by product (Pearson r):

Paneer        ████████████████████  0.62  ← Strongest revenue driver
Gulab Jamun   ████████████████      0.54
Rasgulla      ███████████████       0.53
Laddoo        ████████████          0.48
Milk          ███████████           0.43
Samosa        ██                    0.11  ← Volume ≠ revenue impact
```

This finding directly shaped the recommendations: push the high-correlation products, don't over-invest in high-volume / low-margin items.

### Phase 5 — Visualisations

All analysis was accompanied by visualisations built in matplotlib and seaborn:

- **Daily revenue time series** — 87-day trend with 7-day rolling average to smooth noise
- **Product profitability bar chart** — unit margin (%) ranked by SKU
- **Revenue contribution breakdown** — stacked bar showing which products drive total revenue
- **Correlation heatmap** — product-to-revenue and product-to-product relationships
- **Monthly trend analysis** — revenue by calendar month to surface seasonal patterns
- **Cost structure breakdown** — variable vs fixed costs as % of revenue by week

---

## 💡 Recommendations & Business Impact

All recommendations were presented to the business owner and evaluated for feasibility given the shop's operational constraints (3 staff, limited working capital, no e-commerce presence).

### Recommendation 1 — Samosa price increase: ₹10 → ₹12

**Rationale:** Samosa's 6% margin means each unit sold barely covers its cost. A ₹2 price increase (20%) on the highest-volume item would increase daily profit by an estimated ₹300–400 without significantly affecting demand (demand for ₹10–12 snacks is typically inelastic at this price point).

**Projected impact:** +₹9,000–12,000 monthly profit increase.

### Recommendation 2 — College pushcart expansion

**Rationale:** A nearby college represented an untapped high-footfall customer segment with peak demand at breakfast and lunch times — exactly when the main shop is typically slow. A low-capital pushcart deployment (₹15,000–20,000 initial investment) could add a second revenue stream without cannibalising main shop operations.

**Projected impact:** ₹3,000–5,000 additional daily revenue at marginal incremental cost.

### Recommendation 3 — SKU promotional focus on high-margin items

**Rationale:** The correlation analysis showed that Paneer (0.62) and sweets (0.53–0.54) are the strongest revenue multipliers. Verbal recommendations to customers, positioning of these products near the counter, and bundling with popular items could shift the product mix toward higher-margin SKUs.

### Recommendation 4 — Structured daily record keeping system

**Rationale:** The business had no mechanism to track whether performance was improving or declining over time. A simple daily log — 5 minutes of entry per day — was designed and handed over to the owner to maintain independently. This alone transforms the owner's ability to make informed decisions going forward.

### Recommendation 5 — Employee retention via security deposit system

**Rationale:** High employee turnover was identified as a hidden cost driver — training time, inconsistent service, and temporary understaffing all reduce throughput. A refundable security deposit policy (common in similar F&B setups) was recommended to improve retention without increasing base salary costs.

---

## 📁 Repository Structure

```
Data-Processing-and-Analytics-Pipeline-for-Retail-Business/
├── Proposal.pdf              # Initial project scope and methodology proposal
├── Mid-Term_Report.pdf       # Progress report: data collection + preliminary EDA
├── Final-Term-Report.pdf     # Complete analysis, findings, and recommendations
└── README.md
```

> **Note on data:** The operational dataset is not included in this repository to protect the confidentiality of the business owner and their commercial data. The full analysis methodology, all quantitative findings, and the complete recommendation set are documented in the PDF reports above and in this README.

---

## 🛠️ Tech Stack

| Tool | Usage |
|------|-------|
| Python 3.10+ | Core analysis language |
| pandas | Data cleaning, transformation, aggregation, correlation |
| NumPy | Numerical operations and statistical summaries |
| Matplotlib | Time-series charts, bar charts, trend visualisations |
| Seaborn | Correlation heatmaps, distribution plots |
| Excel | Manual daily data entry (collection only — all analysis in Python) |
| Jupyter Notebook | End-to-end analysis environment |

---

## 🚀 Skills Demonstrated

This project is distinct from academic or competition-based ML work because it involved the full consulting lifecycle — not just the technical analysis.

**Data engineering:** Designed a data collection schema from scratch for a business with zero existing records. Defined what to collect, how to structure it, and built the cleaning pipeline to handle real-world data entry inconsistencies.

**Business analytics:** Translated raw operational numbers into insights the owner could understand and act on — margin analysis, correlation-to-revenue, cost structure decomposition.

**Stakeholder communication:** Presented findings and recommendations to a non-technical business owner. Recommendations had to be practical, low-cost, and immediately implementable — not theoretical.

**Real-world EDA:** Dealt with genuinely messy data — closed days, entry errors, missing records — rather than a pre-cleaned dataset. The cleaning decisions (e.g. how to handle closure-day nulls) had real implications for downstream analysis.

**Profitability modelling:** Built a unit economics framework (cost price → selling price → margin → revenue contribution) that the business can continue using independently.

---

## 🔮 Potential Extensions

- [ ] Demand forecasting model using the 87-day time series (ARIMA / XGBoost)
- [ ] Break-even analysis for the pushcart expansion recommendation
- [ ] Price elasticity modelling for the Samosa price increase
- [ ] Automated daily reporting dashboard (Streamlit) for the owner

---

## 👨‍💻 Author

**Piyush Jha** — ML Engineer & Data Analyst  
[GitHub](https://github.com/jhapiyush44) · [LinkedIn](https://www.linkedin.com/in/piyush-jha-3904a81a6/) · jhapiyush44@gmail.com

---

*Found this useful? Consider leaving a ⭐ — it helps others discover the work!*
