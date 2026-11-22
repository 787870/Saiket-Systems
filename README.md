# Telco Customer Churn Analysis – Power BI Dashboard

An interactive two-page Power BI report built during my **Power BI Internship at Saiket Systems** to analyse telecommunications customer churn, uncover key retention drivers, and quantify monthly revenue at risk.

---

## 📊 Key Metrics Overview

| Metric | Value |
| :--- | :--- |
| **Total Customers** | 7,043 |
| **Churned Customers** | 1,869 |
| **Retained Customers** | 5,174 |
| **Overall Churn Rate** | 26.54% |
| **Monthly Revenue Lost** | $139.13K |

---

## 🛠️ Tools & Skills Used

- **Power BI Desktop** – Interactive dashboard design, cross-filtering, and conditional formatting.
- **Power Query** – Data cleaning, type conversion, null/error handling, and deduplication.
- **DAX (Data Analysis Expressions)** – Custom KPI and revenue impact measures.

---

## 🧹 Data Preparation (Power Query)

- Imported `Telco_Customer_Churn_Dataset (2).csv` (7,043 rows, 21 columns).
- Converted `TotalCharges` to **Decimal Number** and replaced errors/null values with `0`.
- Transformed `SeniorCitizen` from binary (`0`/`1`) to readable text (`No`/`Yes`).
- Removed duplicate records on `customerID` and verified 100% valid data quality (0% errors, 0% empty values) across all columns.
- Created 6-month **Tenure Bins** (`tenure (bins)`) for distribution analysis.

---

## 📐 Core DAX Measures

```dax
Total Customers = COUNTROWS('Telco_Churn')

Churned Customers =
CALCULATE(
    COUNTROWS('Telco_Churn'),
    KEEPFILTERS('Telco_Churn'[Churn] = "Yes")
)

Retained Customers =
CALCULATE(
    COUNTROWS('Telco_Churn'),
    KEEPFILTERS('Telco_Churn'[Churn] = "No")
)

Churn Rate = DIVIDE([Churned Customers], [Total Customers], 0)

Avg Tenure (Months) = AVERAGE('Telco_Churn'[tenure])

Monthly Revenue Lost =
CALCULATE(
    SUM('Telco_Churn'[MonthlyCharges]),
    KEEPFILTERS('Telco_Churn'[Churn] = "Yes")
)
```

---

## 📈 Dashboard Pages

### 1. Overview & Demographics

- **KPI Cards:** Total Customers, Churned Customers, Retained Customers, Churn Rate, and Monthly Revenue Lost.
- **Churn Rate Split:** Donut chart comparing retained vs. churned customers.
- **Customer Demographics:** Gender breakdown of churned customers (Pie chart), plus Partner and Dependents churn comparison (Clustered bar charts).
- **Tenure Distribution:** 6-month binned histogram showing churn concentration across customer tenure.

### 2. Churn Analysis (Key Drivers)

- **Contract Type:** Stacked bar chart comparing churn across Month-to-month, One year, and Two year contracts.
- **Internet Service:** Stacked column chart across Fiber optic, DSL, and No internet service.
- **Payment Method:** Stacked bar chart comparing Electronic check, Mailed check, Bank transfer, and Credit card payments.
- **Churn Rate Heatmap:** Matrix visual with conditional background formatting crossing `Contract` against `InternetService`.

---

## 💡 Key Insights & Recommendations

- **Contract Length Drives Retention:** Month-to-month plans carry a **42.71%** churn rate compared to **11.27%** for one-year and just **2.83%** for two-year contracts.  
  *Action: Offer targeted discounts or loyalty perks to migrate month-to-month users onto annual plans.*

- **Fiber Optic Risk Hotspot:** Fiber optic customers churn at **41.89%** overall—spiking to **54.61%** among month-to-month Fiber optic subscribers.  
  *Action: Audit Fiber optic pricing, service reliability, and onboarding support.*

- **Early-Tenure Drop-Off:** Churn is heavily concentrated in the **0–6 month** tenure window.  
  *Action: Introduce structured 90-day onboarding check-ins for new subscribers.*

- **Payment Method Friction:** Customers paying via **Electronic check** account for the highest churn volume.  
  *Action: Incentivise enrolment in automatic credit card or bank transfer billing.*

- **Demographic Stability:** Churn is nearly even by gender (**50.24%** Female vs. **49.76%** Male), while customers without partners or dependents churn at noticeably higher rates.

---

## 📁 Repository Structure

```text
Saiket-Systems/
│
├── Customer_Churn_Analysis.pbix
├── Customer_Churn_Analysis.pdf
├── Telco_Customer_Churn_Dataset (2).csv
├── overview_demographics.png
├── churn_analysis.png
└── README.md
```

---

## 👨‍💻 Author

**A. Mohammed Aslam**

- **GitHub:** [github.com/787870](https://github.com/787870)
- **LinkedIn:** [linkedin.com/in/mohammed-aslam-a-363568298](https://www.linkedin.com/in/mohammed-aslam-a-363568298)

---

⭐ If you find this project interesting, consider giving the repository a star!
