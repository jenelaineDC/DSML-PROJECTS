---
### BACKGROUND

The HR department at Salifort Motors has expressed concern about employee satisfaction and retention. While they have gathered data from their workforce, they lack clarity on how to transform this information into actionable insights. Employee turnover is a costly process involving recruitment, training, and lost productivity. Therefore, understanding the underlying reasons for employee attrition is crucial for supporting long-term organizational success.

### PROJECT GOAL

The primary objective of this project is to analyze employee data to uncover patterns and factors influencing turnover. Specifically, the project aims to:

1. **Predict Employee Attrition:** Build a predictive model that estimates the likelihood of an employee leaving the company.
2. **Identify Key Drivers:** Highlight the most influential factors behind employee attrition using advanced model explainability techniques.
3. **Support HR Decisions:** Provide actionable insights to help HR design interventions that improve employee satisfaction and retention.

### SCOPE AND LIMITATION

**This project will:**

- Utilize the HR dataset provided by Salifort Motors.
- Conduct survival analysis using Kaplan–Meier curves and Cox Proportional Hazards models to understand employee tenure and risk factors over time.
- Apply machine learning techniques, specifically Classification models, to predict employee turnover.
- Apply model explainability methods, including Permutation Feature Importance, Partial Dependence Plots, and SHAP values, to uncover the most influential factors in turnover.
- Provide HR with recommendations based on quantitative evidence to improve employee satisfaction and retention.

**This project will not:**
- Collect additional employee data beyond the dataset provided.
- Address external market or economic factors outside the scope of internal HR policies.

---
### PROJECT SUMMARY

---
### DATASET STRUCTURE AND ENTITY RELATIONSHIP DIAGRAM

---
### EXPLORATORY DATA ANALYSIS
![hr_kpi](https://github.com/jenelaineDC/DSML-PROJECTS/blob/main/HR%20Analytics/files/hr_kpi.png)
![distribution_fig](https://github.com/jenelaineDC/DSML-PROJECTS/blob/main/HR%20Analytics/files/distribution_fig.png)
![boxplot_fig](https://github.com/jenelaineDC/DSML-PROJECTS/blob/main/HR%20Analytics/files/boxplot_fig.png)
![hr_dept_table](https://github.com/jenelaineDC/DSML-PROJECTS/blob/main/HR%20Analytics/files/hr_dept_table.png)
---
### SURVIVAL ANALYSIS

---
#### Kaplan-Meier Survival Curves
![kp_curve](https://github.com/jenelaineDC/DSML-PROJECTS/blob/main/HR%20Analytics/files/kpcurve_small.png)
![kpcurve_attribute](https://github.com/jenelaineDC/DSML-PROJECTS/blob/main/HR%20Analytics/files/kpcurve_attribute.png)
---
#### Cox Proportional Hazard
![coxph](https://github.com/jenelaineDC/DSML-PROJECTS/blob/main/HR%20Analytics/files/coxph_small.png)
---
### EMPLOYEE TURNOVER PREDICTION

---
### MODEL EXPLAINABILITY
