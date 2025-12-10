# Karatina University - AI & Expert Systems (Python Track) - CAT 1 Submission

This repository contains the solution and  output files for CAT 1, covering Data Preprocessing, Regression, and Natural Language Processing.

## Repository Contents

| File Name | Description | Related Question |
| :--- | :--- | :--- |
| `AI Impact.csv` | **Input Data:** Used for Questions 1 & 2 (AI Impact on Jobs). | Q1, Q2 |
| `final_data.csv` | **Input Data:** Used for Question 3 (NBA Game Statistics, converted to text). | Q3 |
| `engineered_ai_impact.csv` | **Output:** The dataset after preprocessing, scaling, encoding, and feature engineering. | Q1 |
| `regression_plot.png` | **Output:** Visualization of Actual vs. Predicted Salary for the better-performing regression model. | Q2 |
| `confusion_matrix_nlp.png` | **Output:** Visualization of the classification results for the NLP model. | Q3 |
| `CAT 1 P101 GROUP.ipynb` | **Source Code:** The full Python notebook containing all working solutions (Recommended to rename your Colab file to this). | Q1, Q2, Q3 |

## Question 1: Data Preprocessing & Feature Engineering

**Dataset Used:** `AI Impact.csv`

### Feature Engineering Techniques
1.  **Encoding Categorical Variables:** `Job_Title`, `Education_Level`, and `Risk_Category` were converted to numerical representations using **Label Encoding**.
2.  **Feature Binning:** `Years_Experience` was binned into three ordinal categories: **'Junior'** (0-5 years), **'Mid'** (6-15 years), and **'Senior'** (16+ years).
3.  **Feature Scaling:** **StandardScaler** was applied to normalize all numerical features, ensuring consistent contribution to the downstream models.

### Feature Selection
Two methods were used to identify the most relevant features for predicting the target variable (`Average_Salary`).

| Method | Top 5 Features Identified |
| :--- | :--- |
| **Correlation Analysis** | `Skill_10`, `Risk_Category_Encoded`, `Skill_3`, `Years_Experience`, `Tech_Growth_Factor` |
| **Mutual Information** | `Skill_2`, `Skill_5`, `Skill_6`, `Job_Title_Encoded`, `Education_Level_Encoded` |

**Discussion:** The **Mutual Information** results are considered more reliable here, as they captured specific skills and job/education encodings which hold complex, non-linear dependencies with the target salary.

---

## Question 2: Regression Model Development (35 Marks)

**Target Variable:** `Average_Salary` (from `engineered_ai_impact.csv`)

### Model Performance Summary
| Model | MAE | MSE | RMSE | R² Score |
| :--- | :--- | :--- | :--- | :--- |
| **Linear Regression** | 30253.70 | $1.216 \times 10^9$ | 34875.26 | **0.0020** |
| **Random Forest Regressor** | 30502.40 | $1.240 \times 10^9$ | 35221.55 | -0.0179 |

### Justification
**Linear Regression** is the superior model. Although the $R^2$ scores for both models are extremely low (close to 0), indicating that the current set of features only weakly predicts the salary, the Linear Regression model performed marginally better with a slightly **higher $R^2$ (0.0020)** and **lower RMSE** compared to the Random Forest model (which showed a negative $R^2$, suggesting it performed worse than simply predicting the mean).



---

## 💬 Question 3: NLP Text Classification (35 Marks)

**Dataset Used:** `final_data.csv` (NBA Stats)

* **Approach:** Since the input data was tabular, a narrative description was synthesized for each game row (e.g., "The Washington Wizards scored 84 points...") to enable text classification.
* **Target:** `RESULT` (1 = Win, 0 = Loss).

### NLP Pipeline Steps (Q3.a)
1.  **Tokenization:** Sentences were split into individual words/tokens.
2.  **Stop-word Removal:** Common English words were removed (e.g., 'the', 'and', 'with').
3.  **Lemmatization/Stemming:** A simplified stemming approach was applied (e.g., removing 's' from plurals).
4.  **Vectorization:** **TF-IDF (Term Frequency-Inverse Document Frequency)** was used to weigh word importance.

### Model Evaluation (Q3.c)
| Metric | Score |
| :--- | :--- |
| **Accuracy** | 0.5531 |
| **Macro F1-Score** | 0.55 |



### Top 10 Informative Features (Q3.d)
The features most strongly associated with a **'Win'** prediction (Class 1) were:
`['raptor', 'buck', 'nugget', 'maverick', 'celtic', 'scored', 'rebound', 'assist', 'steal', 'point']`

**Interpretation:** The model heavily relies on team names (e.g., 'buck', 'nugget') and general positive action words (e.g., 'point', 'assist') to classify a result, demonstrating that the generated text successfully captured the underlying win/loss pattern.

### Custom Input Predictions (Q3.e)
| Custom Sentence | Model Prediction |
| :--- | :--- |
| "The Lakers scored 130 points with high assists against the Celtics." | **Win**|
| "The team scored only 80 points and had many turnovers." | **Loss** |
| "Golden State Warriors scored 120 points with 30 assists." | **Win** |
| "The Bulls played poorly scoring 70 points." | **Loss** |
| "The Heat defended well and scored 110 points." | **Win** |
