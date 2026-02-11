# IBM HR Analytics | Employee Attrition Analysis

## About This Project
I analyzed the IBM HR dataset (1,470 employees) to understand why people leave and where companies should focus retention efforts.

The goal was simple:
Find patterns HR teams can act on.  
Turn raw HR data into decisions.

---

## What I Found

### Salary matters more than most factors
Employees who left earn much less on average.

Median monthly income:
- Employees who left → around $3,000  
- Employees who stayed → around $5,000  

Higher salary links with lower exit risk in this dataset.

---

### Some departments lose people faster than others
R&D loses the highest number of employees overall.  
Sales loses the highest percentage compared to its size.

When you go deeper into job roles:
- Sales Representatives show attrition close to 40%
- Laboratory Technicians also show high turnover
- HR roles sit above company average attrition

---

### Overtime is a strong risk signal
Attrition rate difference is large:

- Employees working overtime → above 30%
- Employees without overtime → around 10%

This suggests workload pressure plays a major role in exits.

---

## Visual Analysis

### Attrition by Department
![Attrition by Department](chart_attrition_by_dept.png)

Shows where most exits happen across the company.

---

### Salary vs Attrition
![Income vs Attrition](chart_income_impact.png)

Shows salary distribution difference between employees who leave and stay.

---

### Overtime vs Attrition
![Overtime Impact](chart_overtime_impact.png)

Shows how overtime links with higher exit probability.

---

### Job Satisfaction vs Attrition
![Job Satisfaction Impact](chart_satisfaction_impact.png)

Lower satisfaction scores show higher exit share.

---

### Correlation Heatmap
![Correlation Heatmap](chart_correlation_heatmap.png)

This chart shows how HR metrics relate to each other.

Example:
If two variables show strong correlation, they move together.  
If correlation is near zero, they behave independently.

This helps detect hidden patterns in workforce data.

---

## How I Built The Analysis

### Tools
Python  
Pandas  
NumPy  
Seaborn  
Matplotlib  
Power BI (for dashboard layer)

---

### Python Code Used

```python
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt

df = pd.read_csv("WA_Fn-UseC_-HR-Employee-Attrition.csv")

plt.figure(figsize=(10,6))
sns.countplot(x='Department', hue='Attrition', data=df)
plt.savefig('chart_attrition_by_dept.png')

plt.figure(figsize=(10,6))
sns.boxplot(x='Attrition', y='MonthlyIncome', data=df)
plt.savefig('chart_income_impact.png')

plt.figure(figsize=(8,5))
sns.barplot(
    x='OverTime',
    y='Attrition',
    data=df.replace({'Attrition': {'Yes': 1, 'No': 0}})
)
plt.savefig('chart_overtime_impact.png')

ct = pd.crosstab(df['JobSatisfaction'], df['Attrition'], normalize='index')
ct.plot(kind='bar', stacked=True, figsize=(10,6))
plt.savefig('chart_satisfaction_impact.png')

plt.figure(figsize=(12,10))
numeric_df = df.select_dtypes(include=[np.number])
sns.heatmap(numeric_df.corr())
plt.savefig('chart_correlation_heatmap.png')
```

---

## Business Takeaways

Where I would focus first:

Salary review for low income high risk roles  
Overtime monitoring in high workload teams  
Manager training in low satisfaction teams  

---

## Tech Stack
Python (Pandas, NumPy, Seaborn, Matplotlib)  
Power BI (DAX, Power Query)  
Dataset: IBM HR Kaggle dataset

---

## 👤 Author
**Lorenzo Di Salvatore**
* **LinkedIn:** [Lorenzo Di Salvatore](www.linkedin.com/in/lorenzo-di-salvatore-psico)
* **Portfolio:** [GitHub Repositories](https://github.com/LoreBear)
