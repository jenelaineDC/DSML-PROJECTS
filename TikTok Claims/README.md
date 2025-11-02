---
### BACKGROUND:

In this project, I am tasked with addressing the challenge of mitigating misinformation on the platform. Millions of videos are uploaded and viewed daily, and many are reported by users for potentially violating TikTok’s terms of service. Manually reviewing all reported content is infeasible, creating a critical need for data-driven solutions.

Analysis shows that videos in violation of platform rules are more likely to present a claim rather than an opinion. Accurately distinguishing between these categories allows TikTok to prioritize content that may require immediate moderation, thereby protecting users and ensuring platform integrity.

From an ethical perspective, misclassifying content carries implications for both user experience and safety. A false positive—misclassifying an opinion as a claim—may result in unnecessary human review but preserves platform safety. A false negative—misclassifying a claim as an opinion—poses a higher risk, as harmful content may go unchecked. Therefore, the model must be designed with ethical safeguards to minimize false negatives while maintaining fairness and transparency.

### PROJECT GOALS:

The objective of this project is to build a predictive model that classifies TikTok videos as either claims or opinions. Specifically, I aim to:

1. Develop machine learning models that can accurately estimate the probability that a video presents a claim.
2. Evaluate multiple classification algorithms (e.g., Random Forest, XGBoost) to determine the most effective approach.
3. Prioritize evaluation metrics such as recall to minimize the risk of failing to flag potentially harmful content.
4. Provide actionable insights to inform TikTok’s moderation strategies and support decision-making for content review prioritization

### SCOPE AND LIMITATIONS:
This project will:
- Use the existing TikTok dataset, focusing on the claim_status binary target variable.
- Perform feature engineering, including selection, extraction, and transformation, to improve model performance.
- Compare the performance of different classification models to identify the optimal approach.

This project will not:
- Collect additional data beyond the provided dataset.
- Deploy models into production; findings will guide future iterations and inform business decisions for content moderation.

---
### PROJECT SUMMARY

---
### DATA STRUCTURE

**Data Source:**
This dataset is supplied as part of the Google Advanced Data Analytics Professional Certificate program courses on Coursera. It contains 19, 382 entries and 11 attributes listed below.

**Data Card:**

| Variable                 | Description                                                             | Data Type |
| ------------------------ | ----------------------------------------------------------------------- | --------- |
| #                        | Unique row identifier                                                   | int64     |
| claim_status             | Binary target indicating whether the video is a `claim` or an `opinion` | object    |
| video_id                 | Unique identifier for each video                                        | int64     |
| video_duration_sec       | Duration of the video in seconds                                        | int64     |
| video_transcription_text | Text transcription extracted from the video                             | object    |
| verified_status          | Indicates whether the author’s account is verified                      | object    |
| author_ban_status        | Indicates whether the author has been banned from the platform          | object    |
| video_view_count         | Number of times the video has been viewed                               | float64   |
| video_like_count         | Number of likes the video has received                                  | float64   |
| video_share_count        | Number of times the video has been shared                               | float64   |
| video_download_count     | Number of times the video has been downloaded                           | float64   |
| video_comment_count      | Number of comments on the video                                         | float64   |


**Data Preprocessing Steps:**

| Stage              | Key Actions |
|--------------------|-------------|
| Data Cleaning      | Remove missing values and duplicated entry |
| Feature Engineering| engagement_score, text_length, text_sentiment, likes_per_view, comments_per_view, shares_per_view, downloads_per_view |
| Outlier Handling   | Cap at 95th percentile (Logistic Regression only); keep original df for Tree-based models |
| Preprocessing      | OneHotEncoder (categorical), StandardScaler (numeric), TFIDFVectorizer (text) |
| Modeling           | Logistic Regression (scaled + encoded), Tree-based Models (encoded only) |

---
### EXPLORATORY DATA ANALYSIS

---
 ### CLAIMS PREDICTION
  
  
  
