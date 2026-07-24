# MSCS 634 – Project Deliverable 1

## Student Name

Srujana Nevoji

## Project Title

Data Collection, Cleaning, and Exploratory Data Analysis

## Dataset

The Online Retail dataset was selected for this project. The dataset contains transactional information from an online retail business, including invoice numbers, product descriptions, quantities, transaction dates, unit prices, customer identifiers, and countries.

The dataset was selected because it contains a large number of real-world transaction records and provides opportunities for data cleaning, exploratory analysis, visualization, and future data mining applications.

## Data Cleaning

Several data-cleaning steps were performed to improve data quality:

* Examined missing values.
* Removed records missing essential product information.
* Removed duplicate records.
* Removed cancelled transactions.
* Removed records containing nonpositive quantities.
* Removed invalid unit prices.
* Standardized product descriptions.
* Converted transaction dates to datetime format.
* Created additional variables for sales and time-based analysis.

## Exploratory Data Analysis

The cleaned dataset was explored using several visualizations and statistical techniques, including:

* Product-frequency analysis
* Sales analysis by country
* Monthly sales trends
* Quantity distributions
* Box plots for potential outlier detection
* Correlation analysis

## Key Insights

The analysis showed that some products have significantly higher demand than others. Sales activity also varies considerably across geographic markets and over time.

The dataset contains a skewed quantity distribution and several potential outliers. These observations require careful consideration because extreme transactions may represent valid large customer orders rather than data errors.

The EDA also identified product, geographic, transaction, and temporal variables that may be useful in future modeling stages.

## Challenges

One challenge was handling missing and invalid transaction information without unnecessarily removing useful data. Another challenge involved identifying outliers because unusual quantities may represent legitimate customer purchases.

These challenges were addressed by examining the context of the variables before deciding how records should be cleaned.

## Future Work

The cleaned dataset can be used in later project stages for techniques such as customer segmentation, clustering, association-rule mining, predictive modeling, and sales trend analysis.

## Conclusion

This deliverable focused on transforming raw transactional data into a cleaner and more reliable dataset. Exploratory data analysis provided important insights into product demand, geographic sales patterns, transaction distributions, and potential outliers. These findings provide a foundation for future data mining and machine learning stages of the project.
