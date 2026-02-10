# 📊 Optimizing Small F&B Businesses with Data Analytics

**Business Data Management (BDM) Capstone Project**

Real-world analytics project conducted for a local food & beverage shop to improve profitability, operational stability, and decision-making using structured data collection and analysis.

---

## 🧠 Problem Statement

Many small businesses operate without digital systems, relying on memory and rough estimates for:

- Daily sales
- Expenses
- Profits
- Employee costs
- Customer demand

This leads to:

- ❌ unclear profitability
- ❌ poor pricing decisions
- ❌ employee turnover issues
- ❌ missed growth opportunities

This project demonstrates how simple data analytics + structured record keeping can transform decision-making even without expensive software.

---

## 🏪 Business Context

- **Shop Name:** Shubham Sweet Corner
- **Type:** Small B2C Food & Beverage Shop
- **Location:** Saharsa, Bihar, India
- **Employees:** 3
- **Operations:** 7 days/week, 7 AM – 9 PM

**Products sold:** Snacks (Samosa, Litti), Sweets (Rasgulla, Laddoo, Gulab Jamun), Dairy (Milk, Paneer, Dahi), Beverages

---

## 🎯 Objectives

- Build a manual yet structured data tracking system
- Analyze daily revenue and profitability
- Identify high/low margin products
- Study customer demand patterns
- Improve employee stability
- Recommend low-cost growth strategies

---

## 📦 Dataset Design

Data was manually collected for **87 operational days**.

**Sheets created:**

| Sheet | Purpose |
|---|---|
| Product Pricing | Cost, selling price, profit margin per SKU |
| Daily Sales Log | Daily quantity sold & revenue |
| Employee Details | Salary & labor cost tracking |
| Variable Expenses | Gas, rent, electricity |

---

## 🛠 Tech Stack

- Python
- pandas
- matplotlib
- seaborn
- Excel (data entry only)

All analysis performed programmatically in Python.

---

## 🔍 Analysis Workflow

1. **Data Collection**

	Manual daily logs converted into structured Excel sheets.

2. **Cleaning & Preprocessing**

	- Handled missing values (shop closure days)
	- Converted dates to `datetime`
	- Standardized numeric types
	- Removed redundant columns

3. **Descriptive Statistics**

	- Mean, Median, Std deviation, Min/Max revenue

4. **SKU-Level Analysis**

	- Profit per unit
	- Margin comparison
	- Revenue contribution

5. **Correlation Analysis**

	Identified which products actually drive total revenue.

6. **Visualizations**

	- Time series revenue trends
	- Product profitability charts
	- Correlation heatmaps

---

## 📈 Key Results

**Business Performance**

- Average Daily Revenue: **₹10,333**
- Average Profit Margin: **19.6%**
- Average Daily Profit: **₹2,024**
- Revenue variation: **very stable (±5%)**

**Product Insights**

- Top 5 products contribute **78%+** revenue
- Samosa = highest volume but very low margin (**6%**)
- Paneer & sweets = high margin + high correlation with revenue

**Correlation Findings**

- Products most associated with revenue growth:
  - Paneer (0.62)
  - Gulab Jamun (0.54)
  - Rasgulla (0.53)
- Samosa showed weak negative correlation → drives footfall, not profit.

---

## 💡 Recommendations Implemented

- ✅ **Pricing Optimization** — Increase Samosa price from **₹10 → ₹12** → improves daily profit without hurting demand
- ✅ **College Pushcart Strategy** — Temporary stall near college → low investment, higher reach
- ✅ **SKU-Level Promotion** — Highlight high-margin items (Paneer, sweets)
- ✅ **Structured Record Keeping** — Daily logs for sales, expenses, employee attendance
- ✅ **Employee Retention** — Refundable security deposit policy to reduce turnover

---

## 📊 Business Impact

This project helped:

- ✔ quantify actual profits
- ✔ identify wasteful costs
- ✔ improve pricing strategy
- ✔ stabilize workforce
- ✔ support expansion decisions
- ✔ enable data-driven management

Most importantly: proved that analytics works even for small offline businesses.

---

## 📁 Repository Structure (suggested)

```
data/
  ├── product_pricing.xlsx
  ├── daily_sales_log.xlsx
  ├── expenses.xlsx

notebooks/
  ├── cleaning.ipynb
  ├── analysis.ipynb
  ├── visualization.ipynb

reports/
  ├── proposal.pdf
  ├── midterm_report.pdf
  ├── final_report.pdf

README.md
```

---

## 🚀 Skills Demonstrated

- Data Cleaning & Preprocessing
- Descriptive Statistics
- Exploratory Data Analysis (EDA)
- Business Analytics
- Profitability Analysis
- Correlation Analysis
- Data Visualization
- Real-world stakeholder interaction
- Decision-driven recommendations
