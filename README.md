# Employee Attrition Risk Analysis

## **Project Overview**

This project develops a predictive analytics system to identify employees at high risk of resignation and understand the key factors driving employee attrition.

The project integrates Oracle SQL, Python machine learning, and Power BI dashboards to deliver actionable workforce insights.

## **Problem Statement**

Organizations often struggle to identify employees who are likely to resign. Traditional HR reporting focuses only on historical attrition.

This project builds a predictive attrition risk model that enables proactive employee retention strategies.

## **Tools & Technologies**

a) Oracle SQL : Data extraction and feature engineering

b) Python : Data preprocessing and machine learning

c) Scikit-learn : Logistic regression modeling

d) Pandas / NumPy : Data manipulation

e) Power BI : Visualization and dashboard

## **Data Description**

The dataset used in this project includes employee-level HR information such as:

a) Employee master data : PROJECT_EMP_MASTER

b) Career progression : PROJECT_PROMOTION_MASTER

c) Training records : PROJECT_TRAINING_MASTER

d) Performance ratings : PROJECT_PERF_MASTER

e) Absence history : PROJECT_ABSENCE_MASTER

f) Payroll data : PROJECT_SALARY_MASTER

g) Incentive data : PROJECT_INCENTIVE_MASTER

h) Job Rotation data: PROJECT_POSITION_MASTER

Note: Due to confidentiality restrictions, the original dataset is not included in this repository.

## **Feature Engineering**

Several predictive features were created to capture behavioral and compensation patterns.

Key engineered features include:

a) training_days_36m : Training Days in last 3 years

b) pos_chng_count : Position Changes in last 3 years

c) perf_slope : (Current Performance Score – Previous Performance Score)/2

d) curr_score : Latest Score

e) Perf_delta : Current – Previous Score

f) months_since_prom : Months since last promotion

g) prom_count : Total Promotions since Joining

h) stagflation : 1 is no promotion in last 3 years

i) incentive_volatility : Standard deviation of last 4 incentives

j) incentive_sum_last3y : Total Incentive in last 3 years

k) absence_days_6m : Total Absence Days in last 6 months

l) absence_rate_3m : Absence Days in last 3 months/ 90

m) absence_rate_30d : Absence Days in last 30 days / 30

n) absence_spike : absence_rate_30d/ absence_rate_3m

o) sal_growth : Change/ Salary 12m ago

p) compa_ratio : Employee salary/median salary of unit/grade

q) below_peer_flag : Y if comparatio <0.95

r) Unit : Organisational Unit

s) Location : Location of Unit

t) Tenure_mm : Tenure in months

u) Age_yy : Age in years

v) Function : Function (Job Specialisation)

w) Resig_flag : Y if Resigned in coming 6 months

x) resig_same_unit_grade : Resigned same unit/grade in past 12 months

## **Machine Learning Model**

The attrition prediction model uses Logistic Regression.

a) Target Variable : RESIG_FLAG

b) Model Output : Probability of employee resignation

c) Model performance metric : ROC AUC Score

## **Power BI Dashboard**

The Power BI dashboard provides several analytical views:

a) Executive Overview : Summary metrics for attrition trends and workforce risk.

b) Attrition History : Historical attrition patterns across departments and locations.

c) Attrition Risk Prediction : Identification of employees with high predicted attrition probability.

d) Employee Risk Register : Detailed list of employees with high resignation probability.

e) Attrition Driver Diagnostics : Analysis of factors influencing attrition risk.

## **Key Insights**

Analysis of employee attrition drivers indicates that resignation risk is primarily influenced by three factors:

a) Current Performance Score – Employees with low performance scores show significantly higher attrition probability, making this the strongest driver.

b) Incentive Volatility – High variability in incentive payouts is strongly associated with increased resignation risk.

c) Early Career Employees (Age / Tenure) – Younger employees and those with shorter tenure exhibit elevated attrition risk.

These findings suggest that performance engagement, incentive stability, and early career retention initiatives should be prioritized to reduce attrition risk.

## **Project Architecture**

Oracle Database

↓

Feature Engineering (SQL Views)

↓

Python Data Processing

↓

Machine Learning Model

↓

Power BI Dashboard

## **GitHub Repository Structure**

Employee-attrition-risk-analysis

├── sql

│ ├── feature_engineering

│ └── snapshot_creation

│ └── data_validation

│

├── python

│ └── attrition_analysis_project.ipynb

│

|── powerbi screenshots

│ ├── executive summary (Screenshot)

│ └── historical attrition analysis

│ └── attrition risk predictive analysis

│ └── attrition risk register

│ └── attrition diagnostic analysis

│

└── readme.md

## **Disclaimer**

This project was developed using internal organizational HR data.

Due to confidentiality restrictions, the original dataset and Power BI file containing real employee data are not included.

Sample structures and screenshots are provided for demonstration purposes.

## Author

Asad Ali
