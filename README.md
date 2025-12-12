# Kidney Health Prediction Models

## Project Goal

This project explores machine learning models to predict kidney health outcomes based on the `kidney_dataset.csv` dataset. It is divided into two main analysis notebooks:
1.  **Classification:** To predict the binary status of Chronic Kidney Disease (CKD).
2.  **Regression:** To predict the Glomerular Filtration Rate (GFR), a key continuous measure of kidney function.

---

## Notebooks

### 1. `kidney_function_health_multi_classification_algo.ipynb`

*   **Objective:** This notebook builds and evaluates models to classify whether a patient has Chronic Kidney Disease (`CKD_Status`).
*   **Models Used:** 
    *   Logistic Regression
    *   Decision Tree Classifier
    *   Random Forest Classifier
*   **Conclusion:** The **Random Forest Classifier** is recommended as the best model for this medical context. Despite Logistic Regression having a slightly higher overall accuracy, the Random Forest model achieves a perfect **Recall score of 1.0**. This is critical in a diagnostic setting, as it means the model successfully identifies all actual positive cases, minimizing the risk of dangerous false negatives. Furthermore, its feature importance analysis aligns well with clinical understanding of the disease.

### 2. `kidney_function_health_multi_regression_algo.ipynb`

*   **Objective:** This notebook builds and evaluates models to predict the Glomerular Filtration Rate (`GFR`), a continuous value that indicates the level of kidney function.
*   **Models Used:**
    *   Linear Regression
    *   Decision Tree Regressor
    *   Random Forest Regressor
*   **Conclusion:** The **Decision Tree Regressor** demonstrates the best predictive performance, achieving the highest R-squared value (**0.9942**) and a low Root Mean Squared Error (RMSE) on the test data. The Random Forest Regressor is a strong alternative, offering more robust and interpretable feature importances that align well with the exploratory data analysis, making it a valuable and reliable model.

---

## Common Data Processing Pipeline

Both notebooks follow a similar pipeline for data preparation:
1.  **Data Loading:** The `kidney_dataset.csv` is loaded into a pandas DataFrame.
2.  **Data Cleaning:** Missing values in the `Medication` column are handled by replacing them with the string 'None'.
3.  **Feature Engineering:** A `uACR` (urine albumin-to-creatinine ratio) column is created by dividing `Protein_in_Urine` by `Creatinine`, adding a valuable clinical metric to the dataset.
4.  **Preprocessing:** A `ColumnTransformer` is used to apply `StandardScaler` to all numerical features and `OneHotEncoder` to all categorical features before feeding the data to the models.