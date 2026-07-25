# MSCS 634 – Final Data Mining Project

## Online Retail Data Mining Analysis

**Student:** Srujana Nevoji  
**Course:** MSCS 634 – Data Mining  
**University:** University of the Cumberlands

---

## Project Overview

This project applies data mining and machine learning techniques to a real-world
Online Retail dataset. The project was completed in multiple phases covering data
collection and cleaning, exploratory data analysis, feature engineering, regression,
classification, clustering, hyperparameter tuning, and association rule mining.

The overall goal of the project was to transform raw retail transaction data into
meaningful insights that could support business decisions such as sales prediction,
identification of high-value transactions, transaction segmentation, product
recommendations, cross-selling, and inventory planning.

---

## Dataset

The Online Retail dataset from the UCI Machine Learning Repository was used for
this project. It contains transactional data from a UK-based online retailer and
includes purchases from customers in multiple countries.

Dataset source:

https://archive.ics.uci.edu/dataset/352/online-retail

Important attributes include:

- InvoiceNo – Unique invoice/transaction identifier
- StockCode – Product identifier
- Description – Product description
- Quantity – Number of units purchased
- InvoiceDate – Date and time of transaction
- UnitPrice – Price per unit
- CustomerID – Customer identifier
- Country – Country associated with the transaction

The dataset was selected because it provides real-world transactional information
that can be used for several different data mining tasks.

---

## Project Workflow

The project consisted of four major phases:

1. Data Collection, Cleaning, and Exploration
2. Feature Engineering and Regression
3. Classification, Clustering, and Pattern Mining
4. Final Analysis, Recommendations, and Ethical Considerations

---

## 1. Data Preparation and Cleaning

The original dataset required preprocessing before machine learning and statistical
analysis could be performed.

The main preprocessing steps included:

- Examining missing values
- Removing records with missing information when required
- Removing duplicate records
- Removing cancelled transactions
- Removing records with invalid quantities
- Removing records with invalid unit prices
- Converting InvoiceDate to datetime format
- Standardizing product descriptions
- Creating a TotalSales variable

TotalSales was calculated as:

TotalSales = Quantity × UnitPrice

After cleaning, the resulting dataset contained valid completed transactions that
could be used for further analysis.

---

## 2. Exploratory Data Analysis

Exploratory Data Analysis (EDA) was performed to understand the characteristics
and patterns of the retail dataset.

The analysis included:

- Sales distribution
- Product purchase frequency
- Sales and transaction activity by country
- Monthly sales patterns
- Quantity and price distributions
- Detection of extreme values and outliers

The EDA showed that the sales distribution was right-skewed, with most transactions
having relatively smaller values and a smaller number of transactions having very
large values.

The geographic analysis also showed that sales were strongly concentrated in the
United Kingdom. Product analysis revealed that several relatively small household
and decorative products were purchased in high quantities.

Monthly analysis indicated changes in purchasing activity over time, including
increased sales activity toward the later months of the year.

These findings helped guide the feature engineering and modeling stages.

---

## 3. Feature Engineering

The original dataset contains individual product-level records. For predictive
modeling, the data was aggregated to the invoice level.

The following features were created:

- TotalQuantity
- UniqueProducts
- AvgUnitPrice
- TotalSales
- Month
- DayOfWeek
- Hour
- Weekend

These engineered features provide information about transaction size, product
diversity, product prices, transaction timing, and overall transaction value.

Feature engineering allowed the raw transactional data to be transformed into a
format suitable for regression, classification, and clustering.

---

## 4. Regression Analysis

Regression models were developed to predict invoice-level TotalSales.

The following models were evaluated:

- Multiple Linear Regression
- Ridge Regression
- Lasso Regression

The models were evaluated using:

- Mean Absolute Error (MAE)
- Mean Squared Error (MSE)
- Root Mean Squared Error (RMSE)
- R-squared (R²)
- 5-fold cross-validation

### Regression Results

| Model | MAE | MSE | RMSE | R² |
|------|------:|------:|------:|------:|
| Multiple Linear Regression | 141.167949 | 58677.91371| 242.235245 | 0.634831 |
| Ridge Regression | 141.168060 | 58677.9208030 | 242.235252 | 0.634831 |
| Lasso Regression | 141.508559 | 58678.4692029 | 242.292268 | 0.634659 |

The three models produced very similar results. Multiple Linear Regression achieved
The lowest prediction error by a very small margin and was selected as the strongest
Overall regression model.

The mean cross-validation R² was approximately **0.614323** for all three models,
indicating reasonably consistent performance across different subsets of the data.

---

## 5. Classification Analysis

Classification models were developed to identify high-value and lower-value
transactions.

Because the original dataset did not contain a predefined classification target,
a new binary variable called `HighValue` was created.

- 1 = High-value transaction
- 0 = Lower-value transaction

The median TotalSales value was used as the threshold.

Two classification models were evaluated:

- Decision Tree
- k-Nearest Neighbors (k-NN)

### Classification Results

| Model | Accuracy | F1 Score | ROC-AUC |
|------|------:|------:|------:|
| Decision Tree | 0.845697 | 0.844396 | 0.845695 |
| k-NN | 0.755867 | 0.748121 | 0.807626 |

The Decision Tree performed better than k-NN across Accuracy, F1 Score, and ROC-AUC.

Confusion matrices and ROC curves were also used to evaluate classification
performance.

---

## 6. Hyperparameter Tuning

GridSearchCV was used to optimize the Decision Tree classifier.

The parameters evaluated included:

- max_depth
- min_samples_split
- min_samples_leaf
- criterion

The best parameters were:

- max_depth = 7
- min_samples_split = 2
- min_samples_leaf = 2
- criterion = entropy

The best cross-validation F1 score was approximately:

**0.884965**

### Original vs. Tuned Decision Tree

| Model | Accuracy | F1 Score | ROC-AUC |
|------|------:|------:|------:|
| Original Decision Tree | 0.845697 | 0.844396 | 0.845695 |
| Tuned Decision Tree | 0.877529 | 0.880147 | 0.953112 |

Hyperparameter tuning improved the Decision Tree's performance. The tuned model
produced higher Accuracy, F1 Score, and ROC-AUC than the original model.

The improvement in ROC-AUC was particularly noticeable, indicating better
separation between high-value and lower-value transactions.

---

## 7. K-Means Clustering

K-Means clustering was used to identify naturally occurring transaction groups.

The clustering model used:

- TotalQuantity
- UniqueProducts
- AvgUnitPrice
- TotalSales

The variables were standardized before applying K-Means because the algorithm is
based on distance calculations.

The Elbow Method and Silhouette Score were used to determine an appropriate number
of clusters.

The highest silhouette score was obtained with:

**k = 2**

Silhouette Score:

**0.42603372**

The final model therefore used two clusters.

### Cluster Interpretation

**Cluster 0 – Smaller / Lower-Value Transactions**

This cluster contained transactions with approximately:

- Average TotalQuantity: 133 units
- Average UniqueProducts: 14
- Average UnitPrice: 3.39
- Average TotalSales: 245.82

**Cluster 1 – Larger / Higher-Value Transactions**

This cluster contained transactions with approximately:

- Average TotalQuantity: 501 units
- Average UniqueProducts: 39
- Average UnitPrice: 2.64
- Average TotalSales: 774.73

The results suggest that the larger transaction group generated higher sales mainly
through greater product quantities and greater product diversity rather than through
higher individual product prices.

---

## 8. Association Rule Mining

Association rule mining was performed using the Apriori algorithm to identify
products that were frequently purchased together.

A subset of transactions from France was used to make market-basket analysis more
computationally manageable.

The analysis used:

- Minimum support: 0.05
- Minimum confidence: 0.50

The Apriori algorithm identified approximately **194 frequent itemsets** that met
the selected support threshold.

Several ALARM CLOCK BAKELIKE products appeared among the most frequent items,
including pink, green, and red variations.

Strong association rules were also found between related products, including
SKULL-themed paper napkins and matching paper plates.

Several of these rules produced very high confidence and lift values, indicating
that the products occurred together substantially more frequently than would be
expected if their purchases were independent.

These relationships could support product recommendations, cross-selling,
promotional bundles, and inventory planning.

---

## 9. Key Findings

The major findings from the project include:

- Data cleaning was necessary because the original dataset contained missing values,
  duplicate records, cancelled invoices, and invalid transaction values.

- Retail sales were highly right-skewed, with most transactions having relatively
  small values and a smaller number of transactions having much larger values.

- Multiple Linear Regression provided the strongest regression results, although
  Ridge and Lasso produced nearly identical performance.

- The Decision Tree performed better than k-NN for identifying high-value
  transactions.

- Hyperparameter tuning improved the Decision Tree, producing an accuracy of
  approximately 87.75%, an F1 score of approximately 0.880, and ROC-AUC of
  approximately 0.953.

- K-Means identified two major transaction groups representing smaller/lower-value
  and larger/higher-value purchasing patterns.

- Association rule mining identified meaningful relationships among products that
  were frequently purchased together.

Overall, the project demonstrated that different data mining methods provide
different but complementary insights into retail transaction data.

---

## 10. Practical Business Applications

The results of this project could support several practical retail applications.

### Product Recommendations

Association rules can be used to recommend related products when customers add
certain products to their shopping carts.

### Cross-Selling and Bundling

Products with strong confidence and lift values can potentially be bundled or
promoted together.

### Transaction Segmentation

K-Means clusters can help distinguish different transaction patterns and support
more targeted marketing strategies.

### High-Value Transaction Identification

Classification models can help identify transaction characteristics associated
with higher-value purchases.

### Inventory Management

Frequently purchased products and strongly associated product combinations can
help retailers make more informed inventory decisions.

### Sales Analysis

Regression models can help businesses understand relationships between transaction
characteristics and overall transaction value.

---

## 11. Ethical Considerations

Several ethical considerations should be addressed when applying machine learning
to retail transaction data.

### Data Privacy

Retail transaction data may contain customer identifiers and purchasing histories.
Organizations should protect customer information through appropriate access
controls, anonymization, and responsible data management.

CustomerID was not used as a direct predictive feature in the final models.

### Fairness

Machine learning predictions should not be used to unfairly exclude customers from
offers, services, or opportunities.

### Bias

The dataset represents transactions from a specific retailer and historical period.
The purchasing patterns may therefore not represent every customer population,
geographic region, or retail organization.

### Responsible Model Use

Classification and clustering results should support business decision-making
rather than automatically replace human judgment.

Association rules represent statistical relationships and should not be interpreted
as proof that purchasing one product causes the purchase of another.

---

## 12. Challenges

Several challenges were encountered during the project:

- Handling missing values
- Removing cancelled and invalid transactions
- Managing duplicate records
- Handling extreme transaction values
- Aggregating product-level records into invoice-level data
- Creating meaningful predictive features
- Creating a classification target
- Selecting the appropriate number of clusters
- Choosing appropriate Apriori support and confidence thresholds
- Managing the computational requirements of association rule mining
- Installing and configuring Python packages in Jupyter Notebook

These challenges were addressed through data preprocessing, feature engineering,
model evaluation, parameter experimentation, and incremental testing of the code.

---

## 13. Future Improvements

Future work could extend this project by:

- Testing Random Forest and Gradient Boosting models
- Evaluating Support Vector Machines
- Performing more extensive hyperparameter tuning
- Comparing K-Means with DBSCAN and Hierarchical Clustering
- Performing customer-level RFM analysis
- Developing a product recommendation system
- Applying FP-Growth to larger transaction datasets
- Examining seasonal purchasing patterns in greater detail
- Validating models using newer transaction data

These improvements could provide additional insights and improve model
generalization.

---

## 14. Technologies and Libraries

The project was completed using Python in Jupyter Notebook.

Major libraries included:

- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- mlxtend

Machine learning and data mining techniques included:

- Multiple Linear Regression
- Ridge Regression
- Lasso Regression
- Decision Tree
- k-Nearest Neighbors
- GridSearchCV
- K-Means Clustering
- PCA
- Apriori
- Association Rules

---

## Repository Contents

This repository contains:

- `MSCS_634_Final_Project.ipynb` – Complete Jupyter Notebook containing the analysis
- `README.md` – Summary of the project, methodology, and findings
- Final project report – Detailed written analysis of the project
- Presentation – Slides summarizing the project and key findings
- Dataset or dataset information, where applicable

---

## Conclusion

This project provided practical experience with the complete data mining workflow,
beginning with raw transactional data and progressing through cleaning, exploratory
analysis, feature engineering, predictive modeling, clustering, and pattern mining.

Regression, classification, clustering, and association rule mining each provided
different perspectives on the Online Retail dataset. Multiple Linear Regression
provided useful sales predictions, the tuned Decision Tree successfully classified
high-value transactions, K-Means identified distinct transaction groups, and Apriori
identified meaningful relationships between products.

The project demonstrates how data mining can transform raw retail transactions into
actionable information that can potentially support marketing, recommendations,
cross-selling, customer segmentation, and inventory management.

---

## References

Chen, D. (2015). Online retail [Data set]. UCI Machine Learning Repository.
https://doi.org/10.24432/C5BW33

Chen, D., Sain, S. L., & Guo, K. (2012). Data mining for the online retail
industry: A case study of RFM model-based customer segmentation using data mining.
Journal of Database Marketing & Customer Strategy Management, 19, 197–208.

Han, J., Pei, J., & Tong, H. (2022). Data mining: Concepts and techniques
(4th ed.). Morgan Kaufmann.

