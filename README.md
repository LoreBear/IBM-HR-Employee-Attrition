# 📊 IBM HR Analytics: Employee Attrition Deep Dive

## 🎯 Project Overview
This project addresses a critical HR challenge: **Employee Turnover**. Using a dataset of 1,470 employees, I combined **Python** for data exploration and **Power BI** for executive-level storytelling. The goal is to move from reactive "exit interviews" to proactive, data-driven retention strategies.

---

## 🔍 Key Analytical Findings

Through data modeling, I identified three major drivers of attrition:

* **The "Pay Gap" Effect:** Employees with lower monthly income show a significantly higher probability of leaving. Salary is a primary retention lever.
* **Departmental Risk:** The **Sales Department** experiences the highest turnover frequency compared to R&D and HR.
* **The Overtime Trap:** A strong correlation exists between frequent overtime and the decision to leave the company.
* **Benchmark:** The current attrition rate is **16.1%**, which serves as our baseline for future retention KPIs.

---

## 📈 Python Data Exploration
Using Python, I analyzed the raw data to find correlations and trends.

### 1. Income vs. Retention
*Visualizing the financial threshold where attrition risk increases.*
![Income Analysis](chart_income_impact.png)

### 2. Attrition by Department
*Identifying high-risk areas within the organization.*
![Dept Analysis](chart_attrition_by_dept.png)

---

## 🖥️ Power BI Executive Dashboard
I developed an interactive dashboard to allow stakeholders to drill down into the data.

![Power BI Dashboard](dashboard_final.png)

### Business Insights & Recommendations:
* **Targeted Retention:** Retention plans should be prioritized for **Sales Representatives** and **Lab Technicians**, where the attrition rate is highest.
* **Managerial Intervention:** Further analysis is needed on "Years with Current Manager" to identify potential leadership training needs.
* **Data Governance:** Used **Power Query** for data transformation and created custom **DAX measures** for real-time KPI tracking.

---

## 🛠 Tech Stack
* **Python:** Pandas, Seaborn, Matplotlib.
* **Power BI:** DAX, Power Query.
* **Data Sourcing:** Kaggle API / IBM HR Dataset.

---

## 👤 Contact & Links
* **LinkedIn:** [Lorenzo Di Salvatore](www.linkedin.com/in/lorenzo-di-salvatore-psico)
* **Portfolio:** [GitHub Repositories](https://github.com/LoreBear)
