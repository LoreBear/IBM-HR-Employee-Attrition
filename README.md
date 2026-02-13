# IBM HR Analytics | Employee Attrition Analysis
### Project by Lorenzo Di Salvatore  
Work and Organizational Psychology | HR Data Analytics

![Focus](https://img.shields.io/badge/Focus-People%20Analytics-blue)
![Tools](https://img.shields.io/badge/Tools-Python%20%7C%20Power%20BI-green)
![Status](https://img.shields.io/badge/Status-Completed-success)


---

## About This Project
This project analyzes the IBM HR Employee Attrition dataset (1,470 records) to identify the drivers behind employee turnover. By combining Python for statistical analysis and Power BI for interactive reporting, raw HR data was transformed into actionable retention strategies.

---

## Executive Summary
**Overall Attrition Rate:** 16% (Industry Benchmark: ~12–15%)  
**Highest Risk Segment:** Sales Representatives (39.8% Attrition)  
**Primary Flight Risk Factors:** Overtime + Low Monthly Income (<$3,000)  
**Retention Anchor:** Stock Option Level 1+ (Reduces risk by ~60%)

---

## Key Findings

**Overtime Multiplier**  
- Attrition jumps from ~10% to 30.5% for employees working overtime.  
- Roles like Sales Representatives are most affected.  
![Overtime Impact](chart_overtime_impact.png)

**The $3,000 Danger Zone**  
- Median income for employees leaving is ~$3,000, vs ~$5,000 for those staying.  
- Below $3,000, employees feel under-rewarded, increasing turnover risk.  
![Income vs Attrition](chart_income_impact.png)

**Role-Specific Fragility**  
- Sales Representatives & Lab Technicians show highest exit rates.  
- Combination of high pressure and low job level leads to stagnation and glass ceiling effect.  
![Job Satisfaction Impact](chart_satisfaction_impact.png)

---

## Department-Level Insights
- R&D: Highest number of exits overall  
- Sales: Highest attrition percentage relative to size  
- Sales Representatives: ~40% attrition  
- Lab Technicians: high turnover  
- HR: above company average attrition  

---

## Visual Analysis: Human-Centric Insights

### 1. Attrition by Department (`sns.countplot`)
- **What it shows:** The volume of "Yes" vs "No" attrition responses across Sales, R&D, and HR.  
- **Insight:** While R&D has the most exits in absolute numbers, Sales shows a much higher proportion of exits relative to its size. This reflects workload pressure and psychological strain in Sales roles.  
- **Technical Note:** Using `hue='Attrition'` allows a side-by-side comparison of retention vs turnover per department.  
![Attrition by Department](chart_attrition_by_dept.png)

### 2. The Hygiene Factor Paradox (`sns.boxplot`)
- **What it shows:** Distribution (median, quartiles, outliers) of monthly income for employees who stayed vs left.  
- **Insight:** Median income for leavers sits around $3,000, significantly lower than the $5,000 median of stayers. Income acts as a retention anchor: above $5,000, the probability of exit drops sharply.  
![Income vs Attrition](chart_income_impact.png)

### 3. Overtime Impact (`sns.barplot`)
- **What it shows:** Probability of attrition (0–1) based on whether an employee works overtime.  
- **Insight:** Extra workload acts as a stress multiplier. Employees working overtime have ~31% chance of leaving, compared to ~10% for non-overtime employees.  
![Overtime Impact](chart_overtime_impact.png)

### 4. Job Satisfaction Stacked Bar (`pd.crosstab`)
- **What it shows:** Percentage of employees leaving at each satisfaction level (1 = Low, 4 = High).  
- **Insight:** By normalizing the bars to 100%, the "red" exit portion shrinks as satisfaction increases. Low satisfaction makes attrition nearly certain for a large segment, while high satisfaction reduces—but does not eliminate—risk.  
![Job Satisfaction Impact](chart_satisfaction_impact.png)

### 5. Correlation Heatmap (`sns.heatmap`)
- **What it shows:** Grid of correlation coefficients (-1 to +1) between numeric HR metrics.  
- **Insight:** Confirms the Manager Tenure Effect: high correlation between `YearsWithCurrManager` and `YearsAtCompany` suggests strong manager-employee bonds are a key retention factor.  
![Correlation Heatmap](chart_correlation_heatmap.png)

---

## Deep Dive Conclusions: Hidden Workforce Dynamics

**Commute Fatigue**  
- Attrition ~14% for ≤10km; rises to 22% beyond 20km.  
- Strategy: Flexible policies for employees with long commutes.

**Stock Options**  
- Zero stock options → 24.4% attrition; Level 1+ → <10%.  
- Strategy: Offer stock options to mid-level talent.

**Manager Compatibility Gap**  
- Highest turnover in first year with a new manager (~32%).  
- Strategy: Check-ins at 3 and 6 months for new manager relationships.

**Total Satisfaction Composite Score**  
- Combining Environment, Job, Relationship, Work-Life Balance (4–16) predicts attrition.  
- Strategy: Use retention heatmaps to target at-risk teams.

---

## Strategic HR Framework: E.R.A. Roadmap

**Equity (Salary)**  
- Fix the $3,000 Danger Zone for high-risk roles.

**Reward (Stock Options)**  
- Offer modest stock options to mid-level talent; cheaper than replacing employees.

**Autonomy (Overtime & Travel)**  
- Monitor workloads and commutes; implement flexible arrangements to reduce burnout.

**Implementation:** Present as a roadmap linking each element to metrics and retention levers.

---

## Business Takeaways

1. Salary Adjustment: Raise low-income, high-risk roles above $3,000.  
2. Overtime Monitoring: Red Flag system for teams exceeding 15% overtime.  
3. Career Pathing: 18-month promotion roadmaps for Job Level 2 stagnation.  
4. Manager Training: Check-ins at 3 and 6 months to reduce early turnover.  
5. Retention Heatmaps: Identify at-risk teams via composite satisfaction scores.

---

## How I Built the Analysis

### Tools
- Python (Pandas, NumPy, Seaborn, Matplotlib)  
- Power BI (DAX, Power Query)

### Python Code Example

```python
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt

df = pd.read_csv("WA_Fn-UseC_-HR-Employee-Attrition.csv")

# Attrition by Department
plt.figure(figsize=(10,6))
sns.countplot(x='Department', hue='Attrition', data=df)
plt.savefig('chart_attrition_by_dept.png')

# Salary vs Attrition
plt.figure(figsize=(10,6))
sns.boxplot(x='Attrition', y='MonthlyIncome', data=df)
plt.savefig('chart_income_impact.png')

# Overtime vs Attrition
plt.figure(figsize=(8,5))
sns.barplot(x='OverTime', y=df['Attrition'].map({'Yes':1,'No':0}), data=df)
plt.savefig('chart_overtime_impact.png')

# Job Satisfaction vs Attrition
ct = pd.crosstab(df['JobSatisfaction'], df['Attrition'], normalize='index')
ct.plot(kind='bar', stacked=True, figsize=(10,6))
plt.savefig('chart_satisfaction_impact.png')

# Correlation Heatmap
plt.figure(figsize=(12,10))
numeric_df = df.select_dtypes(include=[np.number])
sns.heatmap(numeric_df.corr(), annot=True, fmt=".2f", cmap='coolwarm')
plt.savefig('chart_correlation_heatmap.png')
```


## Author

Lorenzo Di Salvatore  
HR Analytics | Organizational Psychology | People Data Strategy
* LinkedIn: [Lorenzo Di Salvatore](https://www.linkedin.com/in/lorenzo-di-salvatore-psico)
* Portfolio: [GitHub Repositories](https://github.com/LoreBear)

