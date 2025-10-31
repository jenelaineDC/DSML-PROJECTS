### PROJECT BACKGROUND
In today’s data-driven economy, small and mid-sized online retailers often face challenges leveraging customer and transaction data to make informed marketing and operational decisions. Understanding customer value, purchasing behavior, and product affinities is crucial for improving retention, driving growth, and optimizing marketing spend.

### PROJECT GOAL
The main goals of this project are to:
1. **Estimate Customer Lifetime Value (CLV)**
Model future customer monetary contribution using probabilistic and machine-learning approaches.
2. **Model Customer Activity / Survival
Estimate** the probability that a customer is still “alive” (active) using BG/NBD so we can distinguish dormant from active customers.
3. **Segment Customers Based on Behavioral Patterns**
Use clustering to identify actionable customer groups for targeted marketing and retention.
4. **Build a Product Recommendation System**
Develop a hybrid recommender (association mining + content similarity) to support cross-sell and personalization.
5. **Produce Actionable Business Insights**
Translate model outputs into marketing, CRM, and merchandising recommendations.

### SCOPE AND LIMITATION
**The project will:**
- Use the Online Retail II dataset (2009–2011), focusing only on the variables provided.
- Analytical methods include: BG/NBD (frequency + probability-alive), Gamma-Gamma (monetary modeling), XGBoost (hybrid CLV), K-Means + PCA (segmentation & visualization), and FP-Growth + TF-IDF (hybrid recommendations).


**The project will not:**
- Incorporate external data sources such as competitor activity or macroeconomic conditions.
- Generalize findings beyond this specific retailer, as results are limited to a single dataset.
- Deploy models into production; instead, it will focus on generating insights and analytical frameworks for potential business use.
- Capture all product categories or customer behaviors, since the dataset is time-bound and may not fully represent long-term patterns.

---
### DATASET STRUCTURE AND ENTITY RELATIONSHIP OVERVOEW 

This project is based on the **UCI Online Retail dataset**, which contains transactional data from a UK-based e-commerce retailer.  
The goal was to transform this raw dataset into a structured analytical pipeline to perform **Customer Lifetime Value (CLV) modeling**, **Customer Segmentation**, and **Product Recommendation**.

**Data Tables and Relationships:**

| **Dataset**                             | **Derived From**                       | **Description**                                                  |
| --------------------------------------- | -------------------------------------- | ---------------------------------------------------------------- |
| **Transactions**                        | Original UCI dataset                   | Core transactional data per customer and product                 |
| **RFM Summary (Calibration & Holdout)** | `calibration_and_holdout_data()`       | Used for BG/NBD and Gamma-Gamma customer lifetime modeling       |
| **Hybrid Model Features**               | RFM Summary + BG/NBD outputs + XGBoost | Predictive CLV and behavioral metrics                            |
| **Customer Segments**                   | Combination of RFM + Hybrid Model      | Groups customers based on behavioral and predictive features     |
| **Product Recommendation**              | FP-Growth + TF-IDF cosine similarity   | Provides association-based and content-based product suggestions |

**Entity Relationship Diagram:**
![erd_light](https://github.com/jenelaineDC/DSML-PROJECTS/blob/main/Online%20Retail/files/erd_light.png)

---
### EXPLORATORY DATA ANALYSIS
![kpi_fig](https://github.com/jenelaineDC/DSML-PROJECTS/blob/main/Online%20Retail/files/kpi_fig.png)
![sales_trend](https://github.com/jenelaineDC/DSML-PROJECTS/blob/main/Online%20Retail/files/sales_trend.png)
![top10_combined](https://github.com/jenelaineDC/DSML-PROJECTS/blob/main/Online%20Retail/files/top10_combined.png)
![top10_monthly](https://github.com/jenelaineDC/DSML-PROJECTS/blob/main/Online%20Retail/files/top10_monthly.png)
![top10_tree](https://github.com/jenelaineDC/DSML-PROJECTS/blob/main/Online%20Retail/files/top10_tree.png)
![cancelled_combined](https://github.com/jenelaineDC/DSML-PROJECTS/blob/main/Online%20Retail/files/cancelled_combined.png)
![cancelled_trend](https://github.com/jenelaineDC/DSML-PROJECTS/blob/main/Online%20Retail/files/cancelled_trend.png)
![cancelled_tree](https://github.com/jenelaineDC/DSML-PROJECTS/blob/main/Online%20Retail/files/cancelled_tree.png)
---
### CUSTOMER SEGMENTATION
![segm_table](https://github.com/jenelaineDC/DSML-PROJECTS/blob/main/Online%20Retail/files/segm_table.png)
![segm_radar](https://github.com/jenelaineDC/DSML-PROJECTS/blob/main/Online%20Retail/files/segm_radar.png)
![segm_pca](https://github.com/jenelaineDC/DSML-PROJECTS/blob/main/Online%20Retail/files/segm_pca.png)
![](https://github.com/jenelaineDC/DSML-PROJECTS/blob/main/Online%20Retail/files/.png)
