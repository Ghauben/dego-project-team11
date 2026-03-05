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
## Bias Analysis 
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

## Structure
- ‘data/‘ - Dataset files
- ‘notebooks/‘ - Jupyter analysis notebooks
- ‘src/‘ - Python source code
- ‘reports/‘ - Final deliverables
