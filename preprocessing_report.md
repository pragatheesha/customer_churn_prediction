# Preprocessing Report  
## Customer Churn Prediction

## 1. Introduction  

Data preprocessing is a crucial step in the machine learning lifecycle, as raw datasets often contain inconsistencies, missing values, categorical variables, and outliers that can negatively affect model performance. This report documents the complete preprocessing and feature engineering workflow applied to the **customer_churn.csv** dataset to prepare it for churn prediction modeling.

## 2. Dataset Description  

The dataset used in this project, **customer_churn.csv**, contains customer-level information related to subscription-based services. The data includes a combination of numerical and categorical variables that describe customer behavior, billing patterns, and contract details.

**Key variables include:**
- `Tenure`: Duration of customer relationship
- `MonthlyCharges`: Monthly subscription cost
- `TotalCharges`: Total amount charged to the customer
- `Contract`: Type of customer contract
- `PaymentMethod`: Payment method used
- `InternetService`: Type of internet service
- `PaperlessBilling`: Billing preference
- `Churn`: Target variable indicating whether the customer left the service

## 3. Handling Missing Values  

The dataset contained missing and improperly formatted values, particularly in the `TotalCharges` column. To address this:

- `TotalCharges` was converted to a numeric format, coercing invalid values into missing entries.
- Numerical features were imputed using the **median**, which is robust to outliers.
- Categorical features were imputed using the **mode** to preserve the most common category.

This ensured that no missing values remained in the dataset after preprocessing.

## 4. Encoding Categorical Variables  

Machine learning algorithms require numerical input. Multiple encoding techniques were applied to handle different types of categorical variables:

### 4.1 Label Encoding  
- Applied to the target variable `Churn`
- Converted categorical values (`Yes`, `No`) into binary values (1, 0)

### 4.2 Binary Encoding  
- Applied to binary categorical features such as `PaperlessBilling`
- Values mapped as `Yes → 1` and `No → 0`

### 4.3 One-Hot Encoding  
- Applied to nominal categorical variables such as `Contract`, `PaymentMethod`, and `InternetService`
- Created separate binary columns for each category
- The first category was dropped to prevent multicollinearity

## 5. Feature Scaling  

Feature scaling was applied to normalize numerical variables and improve model performance.

- **Min-Max Scaling** was applied to `MonthlyCharges` to scale values between 0 and 1.
- **Standard Scaling** was applied to `Tenure` to standardize values with mean 0 and standard deviation 1.

Using multiple scaling techniques ensures consistency across features with different ranges.

## 6. Outlier Detection and Handling  

Outliers in `MonthlyCharges` were identified using the **Interquartile Range (IQR) method**:

- Q1 (25th percentile) and Q3 (75th percentile) were calculated
- Values outside the range `Q1 − 1.5 × IQR` and `Q3 + 1.5 × IQR` were removed

This reduced the impact of extreme values on future machine learning models.

## 7. Feature Engineering  

To enhance predictive power, new features were engineered from existing data:

1. **Customer_Lifetime_Value**  
   - Calculated as `MonthlyCharges × Tenure`
   - Represents total revenue contribution per customer

2. **High_Value_Customer**  
   - Binary flag indicating customers with above-median lifetime value

3. **Tenure_Group**  
   - Categorized customers into lifecycle stages (New, Medium, Long-term)

4. **Payment_Efficiency**  
   - Ratio of total charges to tenure, reflecting payment behavior

5. **High_Monthly_Charge**  
   - Binary indicator identifying customers with above-average monthly charges

These engineered features capture customer value, behavior, and churn risk more effectively.

## 8. Feature Selection  

After preprocessing, the target variable (`Churn`) was separated from the feature set. All remaining features were retained as they provide meaningful information for churn prediction.

## 9. Preprocessing Pipeline  

A preprocessing pipeline was implemented using scikit-learn to ensure consistency and reproducibility. The pipeline allows the same preprocessing steps to be applied to future or unseen data during model deployment.

## 10. Final Output  

The final processed dataset:
- Contains no missing values
- Includes encoded categorical variables
- Has scaled numerical features
- Incorporates engineered features
- Is suitable for machine learning model training

The cleaned and processed dataset was saved for further modeling.

## 11. Conclusion  

This preprocessing workflow transformed the raw **customer_churn.csv** dataset into a structured, clean, and machine-learning-ready format. By applying systematic data cleaning, encoding, scaling, outlier handling, and feature engineering, the dataset is now well-prepared for accurate and reliable churn prediction modeling.
