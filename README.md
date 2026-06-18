# HR Employee Attrition Analysis
End-to-end people analytics project identifying why employees leave, who is at risk, and what it's costing the business-using SQL, Python (statistics + machine learning), and Power BI.

## Problem Statement
A mid-size company is experiencing employee attrition at a rate higher than industry benchmarks. Leadership needs to understand which factors are driving employees to leave, identify which employee segments are highest risk, and quantify the financial impact — so HR can prioritize retention actions with the highest ROI.

This project analyzes 1,470 employee records across 35 attributes (IBM HR Analytics dataset) to answer exactly that.

## Tools Used
'Excel' 'MySQL' 'Python (Pandas, Seaborn, Matplotlib, SciPy, Scikit-learn)''`Power BI'

## Project Workflow

Excel (Initial Check) → MySQL (Business Queries) 
→ Python (EDA + Statistical Testing + ML Model) → Power BI (Dashboard)

### 1. Data Cleaning
- Verified 1,470 rows × 35 columns, zero missing values, zero duplicates
- Dropped 3 constant-value columns (`EmployeeCount`, `StandardHours`, `Over18`) that carried no analytical signal
- Encoded `Attrition` and `OverTime` to numeric for correlation and modeling

### 2. SQL Analysis (MySQL)
Wrote 10 business-question queries covering department-wise attrition, overtime impact, salary bands, tenure bands, age groups, job roles, business travel, and high-risk employee profiling.

### 3. Python — Exploratory Analysis & Statistical Testing
- Built 8 visualizations covering attrition distribution, department/job-role/age/salary/tenure breakdowns, and a full correlation heatmap
- Ran a **Chi-Square test of independence** to statistically validate the overtime–attrition relationship rather than relying on visual pattern alone

### 4. Python — Predictive Modeling
- Built a **Logistic Regression model** to predict attrition risk per employee
- Addressed class imbalance (83.9% stayed vs 16.1% left) using `class_weight='balanced'`
- Evaluated using precision, recall, and F1-score — not just raw accuracy, since catching at-risk employees matters more than overall accuracy in this context

### 5. Power BI Dashboard
4-page interactive dashboard: Executive Summary, Risk Analysis, Demographics, and Insights & Recommendations — with department, attrition, and overtime slicers.

## Key Findings
**Overall attrition rate: 16.1%** - above the typical 10–15% industry benchmark.
| Finding | Detail |
| Overtime is the strongest single driver | Employees working overtime leave at **30.5%** vs **10.4%** for those who don't- a 3x difference |
| Statistically confirmed, not coincidental | Chi-square test: χ² = 87.56, **p < 0.001**-the overtime–attrition link is statistically significant |
| Compensation drives retention | Employees earning below ₹3K/month leave at **28.6%** vs **8.9%** for those earning above ₹10K |
| First year is the danger zone | **34.9%** of employees who leave do so within their first year at the company |
| Highest-risk role | Sales Representatives-**39.8%** attrition, the highest of any job role |
| Frequent travel triples risk | Frequent business travelers churn at **24.9%** vs **8.0%** for non-travelers |
| Model confirms SQL findings | Logistic Regression's strongest positive predictor of attrition was `OverTime`; strongest negative predictor (i.e., retention factor) was `YearsAtCompany` |

### Predictive Model Performance
After balancing for class imbalance, the model achieved **70.8% accuracy** with **77% recall** on the "Left" class-meaning it correctly flags roughly 3 out of 4 employees who are actually at risk of leaving. Recall was prioritized over raw accuracy, since missing an at-risk employee is more costly to the business than a false alarm.

## Estimated Financial Impact
Using a standard HR benchmark of 50% of annual salary as replacement cost per departing employee:

237 employees left × ₹78,000 avg annual salary × 50% replacement cost
= ₹92.4 Lakhs in estimated annual attrition cost
If targeted interventions (overtime caps, first-year onboarding, salary correction) reduce attrition by even 30%, the estimated annual savings is **₹27.7 Lakhs**.

## Business Recommendations
1. **Cap overtime hours**, particularly in Sales and R&D where overtime is most concentrated-introduce compensatory time-off or overtime pay to offset burnout-driven exits.
2. **Review compensation for the Below-₹3K salary band**-this group shows the highest pay-linked attrition; even a moderate increase could meaningfully reduce turnover here.
3. **Build a structured 90-day onboarding program** with assigned mentors -since over a third of all attrition happens in year one, this is the highest-leverage intervention available.
4. **Introduce a travel rotation policy** so no employee is on frequent travel assignments for more than 6 consecutive months.

## Dashboard Preview
### Executive Summary
dashboard_page1_executive.png

### Risk Analysis
![Risk Analysis](charts/dashboard_page2_risk.png)

### Employee Demographics
![Demographics](charts/dashboard_page3_demographics.png)

### Insights & Recommendations
![Insights](charts/dashboard_page4_insights.png)

## Repository Structure
├── HR_Attrition_Cleaned.csv          # Cleaned dataset
├── HR_Attrition_Analysis.ipynb       # Python EDA, statistical test, ML model
├── sql_queries.sql                   # All 10 business-question queries
├── HR_Attrition_Dashboard.pbix        # Power BI dashboard file
├── charts/                           # All 10 exported chart images
└── README.md
