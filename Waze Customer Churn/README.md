---
### BACKGROUND

The Waze data team is developing a data analytics project to address the challenge of monthly user churn. For this project, churn is defined as users who either uninstall the app or stop using it entirely. Churn represents a significant barrier to growth, as acquiring new users is more costly than retaining existing ones.

By predicting churn, Waze can take proactive measures to retain users, such as improving in-app experiences, personalizing engagement, and targeting at-risk users with retention campaigns. Reducing churn will not only lower acquisition costs but also strengthen long-term user loyalty, increase app engagement, and support sustainable growth for Waze’s platform.

### PROJECT GOAL

The primary goal of this project is to analyze user data to uncover patterns and factors that influence churn. Specifically, the aim is to:
- Build machine learning models that estimate whether a user is likely to churn.
- Compare the performance of different algorithms (e.g., Random Forest, XGBoost) to identify the most effective approach.
- Provide actionable insights to support product and engagement strategies that improve user retention.

### SCOPE AND LIMITATION

This project will:
- Use the current user dataset collected by Waze.
- Explore the impact of engineered features on model performance.
- Perform SMOTE and stratified sampling to deal with class imbalance.

This project will not:
- Collect new data beyond what is already available at this stage.
- Address external factors such as competitor activity or broader market trends.
- Deploy the models into production but will instead inform future iterations of the project.
---
### PROJECT SUMMARY

---

### DATA STRUCTURE AND ENTITY RELATIONSHIP DIAGRAM
This dataset is supplied as part of the Google Advanced Data Analytics Professional Certificate program courses on Coursera. According to Google, this dataset contains synthetic data created in partnership with Waze. It contains 14, 999 entries and 13 attributes listed below.

**Data Card:**
| Variable                    | Description                                                            | Dtype   |
| --------------------------- | ---------------------------------------------------------------------- | ------- |
| **ID**                      | Unique identifier for each user                                        | int64   |
| **label**                   | Binary target variable indicating user status: `retained` or `churned` | object  |
| **sessions**                | Number of times the user opened the app during the month               | int64   |
| **drives**                  | Number of driving sessions (≥1 km) during the month                    | int64   |
| **total_sessions**          | Estimated total number of sessions since user onboarding               | float64 |
| **n_days_after_onboarding** | Number of days since the user signed up for the app                    | int64   |
| **total_navigations_fav1**  | Total navigations to favorite place 1 since onboarding                 | int64   |
| **total_navigations_fav2**  | Total navigations to favorite place 2 since onboarding                 | int64   |
| **driven_km_drives**        | Total kilometers driven during the month                               | float64 |
| **duration_minutes_drives** | Total driving duration (minutes) during the month                      | float64 |
| **activity_days**           | Number of days during the month where user had any session activity    | int64   |
| **driving_days**            | Number of days during the month where user had ≥1 driving session      | int64   |
| **device**                  | Device OS type (categorical)                                           | object  |

**Data Prepocessing Steps:**
| Stage              | Key Actions |
|--------------------|-------------|
| Data Cleaning      | Drop missing values, duplicates, and unnecessary column `ID` |
| Feature Engineering| `km_per_driving_day`, `percent_sessions_in_last_month`, `professional_driver`, `total_sessions_per_day`, `km_per_hour`, `km_per_drive`, `percent_of_sessions_to_favorite` |
| Outlier Handling   | Cap at 95th percentile for Logistic Regression; keep original data for Tree-based models |
| Preprocessing      | OneHotEncoder (categorical), StandardScaler (numeric) |
| Modeling           | Logistic Regression (scaled + encoded); Tree-based Models (encoded only) |

---
### EXPLORATORY DATA ANALYSIS
![features_dist](https://github.com/jenelaineDC/DSML-PROJECTS/blob/main/Waze%20Customer%20Churn/files/feature_dist.png)

##### Feature Engineering
![engfeature_dist](https://github.com/jenelaineDC/DSML-PROJECTS/blob/main/Waze%20Customer%20Churn/files/engfeature_dist.png)
To improve the model’s ability to detect churn, I engineered several new features. Each feature is designed not only to add predictive value but also to provide business-relevant insights into user behavior:

- **`km_per_driving_day`**: Represents the average kilometers driven on each active driving day in the last month, giving a normalized view of driving intensity and helping differentiate light users from heavy or more dependent drivers.  

- **`percent_sessions_in_last_month`**: Measures the share of a user’s total sessions that occurred in their last active month, capturing recency of engagement.  

- **`professional_driver`**: A binary flag identifying users with at least 60 drives and 15 active driving days in the last month, allowing the model to distinguish highly active or professional drivers from casual ones.  

- **`total_sessions_per_day`**: The average number of sessions per day since onboarding, reflecting overall long-term engagement relative to account age.  

- **`km_per_hour`**: The average kilometers driven per hour in the last month.

- **`km_per_drive`**: The average distance per trip in the last month, highlighting driving habits at the trip level and differentiating short, casual usage from longer, more dependent use cases.  

- **`percent_of_sessions_to_favorite`**: The percentage of sessions used to navigate to saved favorite places, serving as a proxy for loyalty and habitual app usage.  

##### Outlier Detection
![features_box](https://github.com/jenelaineDC/DSML-PROJECTS/blob/main/Waze%20Customer%20Churn/files/feature_box.png)
![engfeatures_box](https://github.com/jenelaineDC/DSML-PROJECTS/blob/main/Waze%20Customer%20Churn/files/engfeature_box.png)

As part of the exploratory analysis, I examined the distributions of the numerical variables using histograms and boxplots. Overall, most of the features showed varying degrees of right skewness, with clear outliers that highlight differences in user behavior patterns.

- **`sessions`**: This variable, which captures how often a user opened the app in the last month, shows a right-skewed distribution. Half of the users had 56 or fewer sessions, while a small group of heavy users logged over 700 sessions, marking them as clear outliers.

- **`drives`**: Similar to `sessions`, the number of drives (≥1 km) is also right-skewed and approximately log-normal. The median is 48, but some drivers recorded 400+ drives in a single month, suggesting a subset of highly active or possibly professional users.

- **`total_sessions`**: The total number of sessions since onboarding is also skewed to the right, with a median of ~160 sessions. Compared to the monthly median of ~48 sessions, this indicates that a significant portion of a user’s total activity often occurs in just the most recent month, which is worth deeper analysis.

- **`n_days_after_onboarding`**: This variable, representing user tenure, is uniformly distributed across the range of 0 to ~3,500 days (~9.5 years). Unlike usage features, tenure does not show clustering or heavy skewness.

- **`driven_km_drives`**: The total kilometers driven in the last month shows strong right skew. Half of users drove under ~3,495 km, while the most extreme case exceeded 20,000 km, which is over half the circumference of the Earth. These extreme long-distance drivers clearly stand out as outliers.

- **`duration_minutes_drives`**: Total minutes driven also follows a heavy right-skew. The median is ~1,478 minutes (~25 hours), but some users drove 15,000+ minutes (>250 hours) in one month, again suggesting a small group of outlier users with unusually high activity.

- **`activity_days`**: The number of days a user opened the app in the last month has a median of 16 days and a nearly uniform distribution across the range. Interestingly, ~250 users did not open the app at all, while another ~250 opened it every single day. Unlike `sessions`, which is more skewed, this variable shows a flatter distribution and warrants comparison.

- **`driving_days`**: The number of days a user drove is also fairly uniform but drops off in the higher counts compared to `activity_days`. Notably, almost twice as many users (~1,000) did not drive at all compared to those who didn’t open the app (~550). This discrepancy between app activity and actual driving behavior should be flagged for deeper investigation.

From this outlier analysis, it is clear that several variables (e.g., `sessions`, `drives`, `driven_km_drives`, `duration_minutes_drives`) contain extreme values that could influence model training. The right-skewed distributions suggest that some users are highly active or professional drivers, while others are casual or inactive. These patterns will inform feature transformations, potential log-scaling, or outlier treatment to ensure the churn prediction model is robust and not unduly influenced by extreme user behavior. Additionally, discrepancies between `activity_days` and `driving_days` highlight behavioral segments that may be important predictors of churn.

#### Outlier Handling
From the previous section, the boxplots indicated that many of these numerical variables contain clear outliers. Based on my analysis, these outliers do not appear to be data entry errors—they arise naturally from the right-skewed distributions of the variables.

Depending on how the data will be used, it may be useful to handle these extreme values to reduce their impact on modeling. One approach is to **impute outlying values with more reasonable thresholds**, rather than removing them entirely. A common technique is to set a threshold based on a specific percentile of the distribution.

A function that calculates the **95th percentile** for a given column and then replaces any value exceeding this percentile with the 95th percentile value itself will be used. This ensures that extreme values are capped while preserving the overall distribution structure.

However, for a tree based model, it is not necessary to impute this outliers. So a different dataframe will be used for Logistic Regression model and Tree-based model.
```
def cap_outliers(df_input, columnname, percentile=0.95):
    """
    Caps values above a given percentile for a specified column in a DataFrame.

    Parameters:
    df_input (pd.DataFrame): The DataFrame to modify
    columnname (str): The column to cap
    percentile (float): The percentile threshold (default is 0.95)

    Returns:
    pd.DataFrame: DataFrame with capped column
    """
    p_val = round(df_input[columnname].quantile(percentile), 2)
    df_input[columnname] = df_input[columnname].where(df_input[columnname] < p_val, p_val)
    print(f"{columnname} capped at {int(percentile*100)}th percentile: {p_val}")
    return df_input
```

---
### CUSTOMER CHURN PREDICTION
#### Evaluation Metric Selection
Before moving into the modeling phase, it was important to establish how the model’s performance would be evaluated. This decision depends on both the distribution of the target variable and the business use case.

When selecting an evaluation metric, **accuracy is not ideal in this scenario**. With an **imbalanced dataset**, accuracy can appear high while still failing to identify the users who are most at risk of churn—the group we are most interested in.

From a business perspective, the risk of a false positive prediction (predicting churn when a user does not churn) is low. Such predictions do not cause financial loss or other negative consequences. However, failing to identify true churners could result in missed opportunities to engage and retain valuable customers. For this reason, **recall** was chosen as the key evaluation metric. By focusing on recall, we ensure that the model is optimized to correctly capture as many churned users as possible, aligning directly with our business goal of reducing customer attrition.

#### Model Development

The final modeling dataset contains **14,299 samples**. While this is at the lower end of what is generally recommended for a robust model selection process, it remains sufficient to derive meaningful insights and make data-driven decisions.

To ensure a rigorous modeling approach, I implemented the following workflow:

1. **Data Partitioning (Train/Validation/Test)**  
   I split the dataset into **60/20/20** proportions. When determining the split, I carefully considered both the total number of samples per partition and the representation of the **minority class (churned users)**.  
   - With this split, the **validation and test sets each contain ~2,860 samples**, including approximately **515 churn instances (18%)**, providing a reliable basis for evaluating model performance and minimizing sampling bias.

2. **Model Training and Hyperparameter Optimization**  
   All candidate models were trained on the **training set**, with hyperparameters tuned to maximize predictive performance while preventing overfitting.  

3. **Model Selection Using Validation Set**  
   The **validation set** was used to compare candidate models and identify the **champion model** that best balances performance and generalizability.  

4. **Performance Assessment on Test Set**  
   Finally, the **champion model** was evaluated on the **test set** to confirm its predictive power on unseen data, ensuring the solution is robust for business decision-making.

This structured approach ensures that the churn prediction model is both statistically sound and actionable, providing business stakeholders with confidence in the insights derived from the analysis.

![](https://raw.githubusercontent.com/adacert/tiktok/main/optimal_model_flow_numbered.svg)

#### Model Selection and Evaluation

In the initial validation, all three models showed low recall scores, ranging from 0.12 to 0.17, indicating that the models were struggling to identify churned users effectively. To address this, I retrained the models using SMOTE to balance the training data.

After applying SMOTE, the models’ recall scores on the validation set improved significantly, ranging from 0.33 to 0.41. Based on these results, I selected the Random Forest model as the champion, which achieved a recall score of 0.41 on the validation set.

Finally, I evaluated the champion Random Forest model on the unseen test set, achieving a recall of 0.44, which demonstrates that the model generalizes well and effectively identifies users likely to churn. While precision is 0.30, meaning some retained users are misclassified as churners, the business impact is minimal because engaging these users is low-cost. The F1-score of 0.36 reflects a reasonable balance between recall and precision, and overall accuracy of 0.72 is less meaningful due to class imbalance.

From a business perspective, this model enables Waze to proactively target nearly half of at-risk users, allowing retention campaigns to focus resources effectively. Even capturing a portion of churners early could translate into hundreds of retained customers per month, enhancing overall customer lifetime value. With continued data collection and model iteration, there is potential to further improve recall and precision, maximizing ROI from retention efforts.

---
### RESULTS AND DISCUSION

#### Conclusion

In this project, we successfully developed a predictive model to identify users at risk of churning from Waze. By focusing on recall as the key evaluation metric, we prioritized correctly identifying churned users to support proactive retention strategies.

The champion Random Forest model achieved a recall of 0.44 on the test set, meaning it correctly identifies nearly half of the users likely to churn. Precision (0.30) indicates some false positives, but the cost of misclassifying retained users is minimal, as engagement campaigns can safely target these users. The F1-score of 0.36 and overall accuracy of 0.72 reflect a moderate balance between identifying churners and minimizing misclassification, acknowledging the inherent class imbalance (~18% churn).

Feature importance analysis revealed that activity_days, n_days_after_onboarding, and total_navigations_fav2 are the most influential variables. Importantly, several engineered features—such as km_per_hour, km_per_drive, total_sessions_per_day, and percent_sessions_in_last_month—ranked among the top 10, demonstrating that thoughtful feature engineering significantly enhanced model performance and captured meaningful behavioral patterns.

#### Recommendations

- Target Retention Campaigns: Use the model to engage at-risk users, potentially retaining hundreds per month and boosting loyalty.

- Iterative Model Improvement: Continuously retrain the model with new data to enhance recall and precision, maximizing ROI.

- Feature Engineering: Expand behavioral and usage-based features, including in-app interactions or geolocation signals, to improve predictive power.

