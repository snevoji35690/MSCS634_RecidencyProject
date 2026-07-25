# MSCS 634 – Data Mining Project

## Student

Srujana Nevoji

## Project Title

Online Retail Data Cleaning, Exploratory Analysis, Feature Engineering, and Regression Modeling

## Project Overview

This project analyzes the Online Retail dataset through two connected project deliverables.

Project Deliverable 1 focuses on data collection, data cleaning, and exploratory data analysis. Project Deliverable 2 extends the same cleaned dataset through feature engineering, regression modeling, model evaluation, and cross-validation.

The overall purpose of the project is to demonstrate a complete data mining workflow, beginning with raw transactional data and progressing toward predictive modeling and model evaluation.

## Dataset

The Online Retail dataset contains transactional data from an online retail business.

Important attributes include:

* Invoice number
* Product description
* Quantity
* Invoice date
* Unit price
* Customer identifier
* Country

The dataset was selected because it contains a large number of real-world transactional records and supports data cleaning, visualization, exploratory analysis, feature engineering, and predictive modeling.

# Project Deliverable 1

## Data Cleaning

Several data-cleaning steps were performed before analysis.

These included:

* Examining missing values
* Removing records missing essential product information
* Removing duplicate records
* Removing cancelled transactions
* Removing transactions with nonpositive quantities
* Removing transactions with invalid unit prices
* Standardising product descriptions
* Converting invoice dates to datetime format

A new variable called `TotalSales` was created by multiplying Quantity by UnitPrice.

Additional time-related features were also extracted from InvoiceDate.

## Exploratory Data Analysis

Several analyses and visualizations were performed, including:

* Top products by quantity sold
* Sales by country
* Monthly sales trends
* Quantity distribution
* Box plots for potential outliers
* Correlation analysis

## Deliverable 1 Key Insights

The exploratory analysis showed that some products are purchased substantially more frequently than others.

Sales were also unevenly distributed across geographic markets, with certain countries generating considerably more revenue.

The monthly sales trend revealed changes in transaction activity over time that may reflect seasonal purchasing behaviour.

The quantity distribution was strongly skewed and contained potential outliers. These observations required careful interpretation because some unusually large transactions could represent valid bulk purchases rather than errors.

These findings helped guide the feature engineering and modeling decisions used in the second project deliverable.

# Project Deliverable 2

## Feature Engineering

The same cleaned Online Retail dataset from Deliverable 1 was used for predictive modeling.

Individual product records were aggregated into invoice-level observations.

The engineered predictors included:

* Total quantity purchased
* Number of unique products
* Average unit price
* Transaction month
* Day of the week
* Transaction hour
* Weekend indicator

The target variable was `TotalSales`, representing the total monetary value of each invoice.

Transactions above the 99th percentile of invoice sales were excluded from the modeling dataset to reduce the influence of extremely large transactions.

## Regression Models

Three regression approaches were developed:

1. Multiple Linear Regression
2. Ridge Regression
3. Lasso Regression

The dataset was divided into 80% training data and 20% testing data.

Features were standardised before regression model training.

## Model Evaluation

The models were evaluated using:

* Mean Absolute Error (MAE)
* Mean Squared Error (MSE)
* Root Mean Squared Error (RMSE)
* R-squared (R²)

The model with the lowest prediction error and highest R² was considered the stronger model based on test-set results.

## Cross-Validation

Five-fold cross-validation was performed to assess the ability of each model to generalize to unseen data.

Cross-validation provided a more reliable assessment of model performance than relying only on one train-test split.

## Key Modeling Insights

Feature engineering transformed the original item-level retail records into meaningful invoice-level observations suitable for regression analysis.

Transaction quantity, product diversity, average product price, and transaction timing provided useful predictors for invoice-level sales.

Regularisation methods such as Ridge and Lasso allowed the project to compare ordinary regression with models that control coefficient magnitude.

Using multiple evaluation measures provided a more complete understanding of predictive performance.

## Challenges

One challenge involved handling missing values, duplicate records, cancellations, and invalid transaction values while preserving useful information.

Another challenge involved identifying potential outliers. Some extremely large transactions may be valid purchases rather than errors.

During the modeling stage, extreme invoice sales could strongly influence regression coefficients. Transactions above the 99th percentile were therefore excluded from the modeling dataset.

Another important consideration was target leakage. Item-level TotalSales is calculated directly from Quantity and UnitPrice. To create a more meaningful prediction problem, transactions were aggregated to the invoice level and additional features were engineered.

Cross-validation pipelines were used so that feature scaling occurred independently within each validation fold, reducing the risk of data leakage.

## Conclusion

This project demonstrated a complete data mining workflow using the Online Retail dataset.

The first phase transformed raw transactional records into a clean and reliable dataset and used exploratory analysis to identify important patterns, trends, and potential data-quality issues.

The second phase extended the same dataset through feature engineering and predictive modeling. Multiple Linear Regression, Ridge Regression, and Lasso Regression were compared using MAE, MSE, RMSE, R², and five-fold cross-validation.

Overall, the project demonstrated the importance of data preparation, exploratory analysis, appropriate feature engineering, model comparison, and validation when building predictive solutions using real-world data.
