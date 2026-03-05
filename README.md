# Digital Ecosystems and Governance in Organizations - Team 11
## Team Members
- Guillaume Hauben, 72577
- Patrick Trepte, 60713
- Lavinia Antonino, 71907
- Giacomo Castiglioni, 73411

## Executive Summary 
This project evaluates governance risks in NovaCred’s credit application dataset. As a data governance task force, the objective was to assess data quality issues, identify potential algorithmic bias in loan approval decisions, and analyze privacy risks associated with the processing of sensitive personal data.

The dataset contains approximately 500 credit application records including applicant information, financial characteristics, spending behavior, and loan decision outcomes. The analysis identified several data quality issues, including duplicate records and inconsistent categorical values, which were addressed through data cleaning and standardization procedures.

Bias analysis evaluated approval outcomes across demographic groups using the Disparate Impact Ratio (DIR). The results indicate potential disparities in approval rates between male and female applicants, suggesting the need for ongoing fairness monitoring and bias mitigation in automated credit decision systems.

The privacy assessment identified multiple forms of personally identifiable information (PII), including names, email addresses, Social Security Numbers, IP addresses, and dates of birth. A pseudonymization demonstration was implemented to illustrate how sensitive identifiers can be protected while maintaining analytical usability.

Overall, the findings highlight several governance risks related to data quality, fairness, and privacy. The project therefore recommends stronger data governance controls, including systematic data quality monitoring, fairness auditing of automated decision systems, protection of sensitive identifiers, and improved alignment with GDPR principles and emerging AI governance frameworks.

## Introduction
### Project Overview
This project analyzes the governance risks present in NovaCred’s credit application dataset. As a data governance task force, the objective was to assess data quality issues, detect potential algorithmic bias in loan approval decisions, and identify privacy risks related to the handling of sensitive personal data.

The analysis was conducted through three main stages:

•	Data quality assessment

•	Bias and fairness analysis

•	Privacy and governance evaluation

The goal of this project is to identify governance risks in automated credit decision systems and propose recommendations to improve transparency, fairness, and regulatory compliance.

### Dataset Overview
The dataset contains approximately 500 historical credit application records stored in a nested JSON format. Each record represents a single loan application, where rows correspond to individual applicants and columns contain attributes describing their personal information, financial profile, spending behavior, and loan decision outcomes.

Data categories include:

- **Applicant information:** name, email, Social Security Number (SSN), IP address, date of birth, and ZIP code  
- **Financial attributes:** income, credit history, debt-to-income ratio, and savings balance  
- **Spending behavior:** categorized spending patterns across different areas  
- **Loan decision outcomes:** approval status, interest rate, and approved loan amount  

The project uses two versions of the dataset:

**raw_credit_applications.csv**  
This file contains the original dataset converted from the raw JSON source into CSV format. It preserves all variables in their initial structure, including potential inconsistencies and missing values present in the original data.

**cleaned_credit_applications.csv**  
This file contains the processed dataset used for analysis. Data cleaning steps included handling missing values, standardizing categorical variables and removing duplicate or inconsistent records to improve data quality for governance and bias analysis.

## Data Quality Findings
The initial dataset contained 502 records and 36 variables extracted from a nested JSON structure. A systematic data quality assessment was conducted to identify structural inconsistencies, missing data patterns, duplicate records, and schema violations.

Duplicate observations were detected based on key identifiers. Specifically:

•	1 duplicate application entry

•	1 duplicate applicant ID

•	2 duplicate Social Security Numbers

These duplicates were removed to prevent distortion in descriptive statistics and downstream decision analysis. After cleaning, the dataset contained 498 unique records.

A missing value audit revealed substantial sparsity in several variables. For example:

•	decision_notes contained 500 missing values (≈99.6%)

•	Several spending behavior variables exhibited had more than 85% missing values

•	Other attributes such as decision_loan_purpose showed ≈90% missing values

Therefore these variables were removed as their analytical reliability is limited.
Categorical standardization was required for several variables. For example, the gender field contained inconsistent encodings, such as {'Male': 193, 'Female': 193, 'F': 58, 'M': 52, NaN: 2}, which after standardization became {'Female': 251, 'Male': 245, NaN: 2}. This normalization ensured consistent categorical representation across records.

Several schema and validity issues were detected:

•	4 invalid email addresses were removed.

•	2 negative values were detected in financials_credit_history_months (−10 and −3) and were corrected.

•	1 anomalous debt-to-income value was corrected.

•	1 record with annual income equal to 0 was flagged as a potential data quality anomaly.

Additionally, ZIP codes were standardized into zero-padded 5-digit strings, and date of birth values were validated to ensure realistic age ranges.

To reduce privacy risk during analysis, sensitive identifiers were protected:

•	applicant_info_ssn and applicant_info_ip_address were pseudonymized using SHA-256 hashing.

After preprocessing, the cleaned dataset contained 498 observations and 39 variables. Overall, The cleaning process improved schema consistency, reduced duplicate records, corrected invalid values, and enhanced data reliability for subsequent bias and governance analysis.

## Bias Analysis 
The bias assessment evaluated potential disparities in loan approval outcomes across demographic groups, focusing on gender and age. The analysis used commonly applied fairness metrics including approval rate comparisons, the Disparate Impact (DI) ratio, demographic parity metrics, and chi-square statistical testing.

Gender Bias Analysis:

Approval rates differed across genders. Female applicants had an approval rate of 0.5060, while male applicants had an approval rate of 0.6653. The resulting Disparate Impact Ratio (DIR) was 0.7605, which falls below the four-fifths rule threshold of 0.80, indicating potential gender-based disparate impact.

Statistical testing confirmed the significance of this difference (χ² = 12.31, p = 0.0004). Fairness metrics computed using the Fairlearn library produced consistent results, with a demographic parity difference of 0.1593 and a demographic parity ratio of 0.7605, suggesting that male applicants receive approvals at a higher rate.

Age Group Bias Analysis:

Approval outcomes also varied across age groups. Applicants under 30 had the lowest approval rate (0.3784), while applicants aged 40–50 had the highest (0.7200). 

The disparity between the lowest and highest approval groups produced a Disparate Impact Ratio of 0.5255, well below the 0.80 threshold. A chi-square test confirmed significant variation across age groups (χ² = 20.32, p = 0.0001).

Algorithmic Rejection Patterns:

The analysis also examined rejection reasons to understand the role of automated decision-making. Algorithmic risk scoring accounted for 167 rejected applications, compared with 23 due to insufficient credit history, 12 due to high debt-to-income ratios, and 4 due to low income. Overall, automated risk scoring generated approximately 81% of all rejections, indicating a strong reliance on automated decision logic.

Algorithmic rejection rates also differed by gender. Female applicants had a rejection rate of 0.3984, compared with 0.2735 for male applicants. This difference was statistically significant (χ² = 8.12, p = 0.0044). Age patterns were also observed, with applicants under 30 experiencing the highest algorithmic rejection rate (0.4730) and applicants aged 40–50 the lowest (0.2300).

Proxy Variable Assessment

The analysis also evaluated whether ZIP code could act as a proxy variable for protected attributes. ZIP code was strongly associated with gender (χ² = 390.72, p < 0.001), but showed no significant direct relationship with approval outcomes (χ² = 180.03, p = 0.7558). While ZIP code does not directly influence approval decisions, its strong correlation with gender suggests a potential risk of proxy discrimination if used in predictive models.

Overall, the analysis identified statistically significant disparities in approval outcomes across gender and age groups. The Disparate Impact Ratio for gender (0.7605) and the age-group disparity (0.5255) both fall below the four-fifths rule threshold, indicating potential disparate impact. In addition, the strong reliance on automated risk scoring highlights the need for continuous fairness monitoring and governance controls in automated credit decision systems.

## Privacy and Governance Assessment
PII ANALYSIS:
•	full_name: Direct identifier.
•	email: Direct identifier and contact information.
•	ssn: Social Security Number, which is highly sensitive PII and a critical national identifier.
•	ip_address: Online identifier, considered PII under GDPR.
•	date_of_birth: Indirect identifier, explicitly required to be flagged for an "Excellent" grade.
•	zip_code: Location data that, when combined with other data (like gender or date of birth), can be used as identifier . 
•	gender: Protected attribute that requires special handling for bias detection and fairness.
•	spending_behavior array (.category,.amount): This represents sensitive behavioral data collection, which is a major governance gap you need to highlight.

GDPR Requirements Mapping for NovaCred

Lawful Basis (Article 6): The analysis of the dataset reveals a complete lack of a "consent tracking mechanism". NovaCred engages in "sensitive behavioral data collection", such as spending habits and categories. Processing this level of detailed personal data requires a solid legal basis, such as explicit consent, to comply with European regulations.

Data Minimization (Article 5): The system collects information that may not be strictly necessary for evaluating creditworthiness, violating the data minimization principle. Specifically, the "sensitive behavioral data collection"  and the logging of IP addresses should be heavily questioned. We must ask if tracking every single spending category is genuinely indispensable for approving or denying a loan.

Storage Limitation (Article 5): Currently, the company has a major governance gap: there is a "missing data retention policy". Without this control in place, historical application records are stored indefinitely, which directly violates the GDPR storage limitation requirement.

Right to Erasure (Article 17): We identified that "sensitive PII is stored without protection". Keeping this data in plain text makes it incredibly difficult and risky to properly handle legitimate GDPR Article 17 requests (the right to erasure). For this reason, it is crucial to implement pseudonymization or anonymization techniques to secure these fields.

A demonstration of pseudonymization was implemented during the privacy analysis. Sensitive identifiers such as email addresses were transformed using cryptographic hashing techniques to reduce the risk of direct identification while preserving analytical utility. These findings were mapped to key principles of the General Data Protection Regulation (GDPR), including data minimization, storage limitation, and privacy by design.

EU AI ACT CLASSIFICATION
Classification: Under the EU AI Act, AI systems used to evaluate the creditworthiness of natural persons or establish their credit score are classified as High-Risk AI Systems.
NovaCred's Compliance Gaps: Because it uses machine learning to make credit decisions, NovaCred is subject to strict requirements for high-risk systems. Currently, they are failing on two major fronts that you need to highlight:
1.	Transparency: There is "No audit trail for decisions" , making it impossible to explain exactly why a specific model predicted a rejection.
2.	Human Agency: There is a "Lack of human oversight documentation". The AI Act mandates that high-risk systems be designed to allow humans to oversee the system and override automated decisions.

ALGORITHMIC BIAS & FAIRNESS
Gender Disparate Impact: Our analysis calculated a Disparate Impact (DI) ratio of 0.77 for gender.Regulatory Implications: Because this value falls below the 0.8 threshold (the "four-fifths rule"), it clearly indicates potential disparate impact and systemic discrimination in the lending decisions. 
For a High-Risk AI System under the EU AI Act, deploying a model with unmitigated bias exposes NovaCred to severe compliance violations, regulatory scrutiny, and reputational damage.

## Governance Recommendations 
Based on the findings from the data quality, bias, and privacy analyses, several governance measures are recommended to improve the reliability, fairness, and regulatory compliance of NovaCred’s credit decision system.

Data Quality Governance

NovaCred should implement a formal data quality management framework to ensure that the data used in automated credit decisions is reliable and consistent. This includes automated validation checks during data ingestion to detect duplicate identifiers such as Social Security Numbers or applicant IDs. Schema enforcement mechanisms should also be implemented to ensure that all variables follow predefined formats and data types. Additionally, categorical variables should be standardized to avoid inconsistent encodings, and variables with excessive missing values should be regularly monitored and reviewed.

Algorithmic Fairness Governance

The bias analysis revealed disparities in approval outcomes across gender and age groups, with the Disparate Impact Ratio falling below the four-fifths rule threshold. To mitigate fairness risks, NovaCred should introduce regular fairness audits of its credit decision models. These audits should include monitoring fairness metrics such as Disparate Impact and demographic parity.
NovaCred should also evaluate the use of potential proxy variables, such as ZIP codes, that may indirectly encode protected attributes. In addition, automated credit decision models should be documented to improve transparency and explainability.

Privacy and Data Protection Governance

The dataset contains several forms of personally identifiable information (PII) as well as detailed behavioral data. To reduce privacy risks, NovaCred should implement pseudonymization of sensitive identifiers before analytical processing and enforce role-based access controls that limit access to raw personal data.
Sensitive data should also be protected through encryption both at rest and in transit. Finally, the organization should adopt data minimization policies to ensure that only data strictly necessary for credit risk evaluation is collected and processed.

AI Governance and Regulatory Compliance

Credit scoring systems fall under the High-Risk AI System category of the EU AI Act, which requires strict governance controls. NovaCred should therefore implement decision logging and audit trails to ensure that automated credit decisions can be reviewed and explained. The organization should also introduce human oversight mechanisms, allowing human reviewers to intervene in automated decisions for high-risk or borderline cases. Additionally, formal model governance documentation, including model risk assessments and model cards, should be maintained.

Overall Recommendation
Strengthening governance across data quality management, fairness monitoring, privacy protection, and AI oversight will significantly improve the transparency, accountability, and regulatory compliance of NovaCred’s automated credit decision system.