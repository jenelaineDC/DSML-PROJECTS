---
### PROJECT BACKGROUND
In today’s competitive e‑commerce landscape, small and mid‑sized online retailers are under constant pressure to retain customers, increase revenue, and allocate marketing budgets efficiently. While these businesses generate large volumes of transactional data, they often lack the analytical frameworks to translate raw data into strategic insights.

### PROJECT GOAL
This project addresses that gap by showing how customer analytics and predictive modeling can be leveraged to:
1. **Estimate Customer Lifetime Value (CLV)**
Model future customer monetary contribution using probabilistic and machine-learning approaches.
2. **Model Customer Activity / Survival
Estimate** the probability that a customer is still “alive” (active) using BG/NBD so we can distinguish dormant from active customers.
3. **Segment Customers Based on Behavioral Patterns**
Use clustering to identify actionable customer groups for targeted marketing and retention.
4. **Build a Product Recommendation System**
Develop a hybrid recommender (association mining + content similarity) to support cross-sell and personalization.

By combining probabilistic models (BG/NBD, Gamma‑Gamma) with machine learning (XGBoost) and hybrid recommendation systems (FP‑Growth + TF‑IDF), the project demonstrates how data science can directly support business growth, customer loyalty, and marketing ROI.

### SCOPE AND LIMITATION
**The project will:**
- Use the Online Retail II dataset (2009–2011), focusing only on the variables provided.
- Methods include: BG/NBD (frequency + probability-alive), Gamma-Gamma (monetary modeling), XGBoost (hybrid CLV), K-Means + PCA (segmentation & visualization), and FP-Growth + TF-IDF (hybrid recommendations).

**The project will not:**
- Incorporate external data sources such as competitor activity or macroeconomic conditions.
- Generalize findings beyond this specific retailer, as results are limited to a single dataset.
- Deploy models into production; instead, it will focus on generating insights and analytical frameworks for potential business use.
- Capture all product categories or customer behaviors, since the dataset is time-bound and may not fully represent long-term patterns.
---
### PROJECT SUMMARY

![segm_overview](https://github.com/jenelaineDC/DSML-PROJECTS/blob/main/Online%20Retail/files/segm_overview.png)
| Cluster | Segment Name | Recency (weeks) | Frequency | Predicted Purchases | Value per Purchase (£) | Behavioral & Strategic Insights |
|---------|--------------|-----------------|-----------|---------------------|------------------------|--------------------------------|
| **0**   | **Mid-Value Customers** | 30.4 | 5.11 | 1.64 | 4.77 | Consistent buyers with stable engagement and moderate order values. **Prob. Alive ≈ 0.98**, **Predicted CLV ≈ £22.8**. High retention likelihood; best suited for **upselling and cross-selling** to increase wallet share. |
| **1**   | **Occasional Buyers** | 12.1 | 1.37 | 0.88 | 5.80 | Lower engagement and shorter tenure. **Prob. Alive ≈ 0.78**, **Predicted CLV ≈ £13.2**. Smaller revenue contribution, with recency ratio ≈ 0.51 indicating declining activity. Target with **reactivation campaigns and win-back offers**. |
| **2**   | **VIP High-Value Customers** | 33.3 | 9.43 | 2.40 | 38.14 | Elite segment with very high CLV (**≈ £219**) and large order sizes. **Prob. Alive ≈ 0.97**. Loyal and profitable, requiring **retention focus, exclusivity programs, and advocacy initiatives**. |

**Survival Analysis**

---
### DATASET STRUCTURE AND ENTITY RELATIONSHIP OVERVIEW 

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
![segm_monthly](https://github.com/jenelaineDC/DSML-PROJECTS/blob/main/Online%20Retail/files/segm_monthly.png)
