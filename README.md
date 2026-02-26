# DEGO Project - Team 11
# # Team Members
- Guillaume Hauben
- Patrick Trepte
- Lavinia Antonino
- Giacomo Castiglioni

## Project Description
Credit scoring bias analysis for DEGO course .

## Structure
- ‘data/‘ - Dataset files
- ‘notebooks/‘ - Jupyter analysis notebooks
- ‘src/‘ - Python source code
- ‘reports/‘ - Final deliverables

### Executive Summary (TO FINISH ONCE PROJECT IS DONE):
The objective of this project is to analyze credit application data in order to understand the key factors that influence credit approval decisions. The project focuses on cleaning, exploring, and preparing the dataset for potential predictive modeling. Through exploratory data analysis (EDA), the goal is to identify patterns, relationships, and trends in applicant characteristics that may affect the likelihood of credit approval.
Financial institutions must evaluate whether a credit applicant represents a low or high risk before granting loans. Poor credit decisions can lead to financial losses, while overly strict decisions may reject reliable customers.
This project addresses the problem of:
•	Understanding which applicant attributes are most associated with credit approval or rejection
•	Identifying patterns that distinguish approved from non-approved applicants
•	Preparing the data for building a machine learning model capable of predicting credit approval outcomes
Ultimately, the project aims to support data-driven decision-making in credit risk assessment.

The dataset represents historical credit applications submitted by individuals seeking financial credit. Each row corresponds to a single applicant, and each column contains information related to their financial, demographic, or credit profile characteristics.
The dataset includes:
•	Applicant financial information (e.g., income, credit history, debt levels)
•	Personal or demographic attributes (if included and anonymized)
•	Credit-related indicators
•	A target variable indicating whether the credit application was approved or rejected
The raw dataset contains the original data, while the cleaned dataset reflects preprocessing steps such as handling missing values, encoding categorical variables, and removing inconsistencies.
Datasets:
•	raw_credit_applications.csv
This file contains the original, unprocessed dataset, including all variables in their initial format, missing values and potential inconsistencies.
•	cleaned_credit_applications.csv
This file contains the processed dataset used for EDA and potential modeling. Data cleaning steps such as handling missing values, encoding categorical variables, and removing duplicates were applied to the raw dataset.

### Data Quality Findings:

## Data Cleaning 
The raw dataset (raw_credit_applications.csv) required several preprocessing steps before it could be used for exploratory analysis and potential predictive modeling. The cleaning process aimed to ensure data quality, consistency, and usability.
Handling Missing Values:
The original dataset contained missing values in several variables.
The following approach was applied:
•	Numerical variables: Missing values were imputed using appropriate statistical measures (e.g., mean or median depending on the distribution).
•	Categorical variables: Missing values were replaced with the mode or categorized as “Unknown” where appropriate.
•	In cases where missing data was excessive and unreliable, affected rows were removed.
This ensured that the dataset remained complete without introducing significant bias.
Removing Duplicates:
The dataset was checked for duplicate records, which were removed to prevent distortion in the analysis and modeling process.
Encoding Categorical Variables:
Since machine learning algorithms require numerical input:
•	Categorical variables were transformed into numerical format.
•	Encoding techniques such as one-hot encoding or label encoding were applied depending on the nature of the variable.
Outlier Treatment:
Financial variables such as income and credit amount were examined for extreme values.
•	Outliers were analyzed carefully.
•	Extreme but realistic values were retained.
•	Clearly erroneous or inconsistent values were treated or removed when necessary.
This ensured that genuine high-income applicants were not incorrectly excluded.
Data Type Corrections:
Variable data types were reviewed and corrected where necessary:
•	Numerical fields were converted to appropriate numeric formats.
•	Date or categorical fields were properly formatted.
The cleaned dataset provides a reliable foundation for exploratory data analysis and predictive modeling.

## Exploratory Data Analysis (EDA)
The exploratory analysis was conducted using the ExploratoryDataAnalysis.ipynb notebook. The objective of the EDA was to understand the structure of the data, identify patterns, detect anomalies, and explore relationships between variables and the target outcome.
The following aspects of the dataset were examined:
•	Distribution of Income: the income variable was analyzed to understand its distribution, detect skewness, and identify potential outliers. Summary statistics and visualizations were used to evaluate income spread across applicants.
•	Credit Score Patterns: credit score distributions were examined to observe differences between approved and rejected applicants. Comparisons helped identify whether higher credit scores are associated with higher approval probability.
•	Approval Rate: The overall proportion of approved versus rejected applications was analyzed. Approval rates were also segmented by key variables such as income level, employment status, and credit history to identify trends.
•	Correlation Matrix: A correlation matrix was computed for numerical variables to evaluate linear relationships between features, to identify which variables are most strongly associated with the target variable and detect potential multicollinearity issues.
The exploratory analysis revealed several important insights:
•	Higher credit scores are strongly associated with increased approval rates.
•	Applicants with stable employment and higher income levels tend to have a greater likelihood of approval.
•	Certain financial variables show moderate correlation with the target variable.
•	The dataset may exhibit some imbalance between approved and rejected applications.
Overall, the EDA provided a clearer understanding of the drivers behind credit approval decisions and laid the foundation for future predictive modeling.
