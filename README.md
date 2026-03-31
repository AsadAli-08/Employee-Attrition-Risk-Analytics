# Employee Attrition Risk Analysis

## **Project Overview**

This project develops a predictive analytics system to identify employees at high risk of resignation and understand the key factors driving employee attrition.

The project integrates Oracle SQL, Python machine learning, and Power BI dashboards to deliver actionable workforce insights.

## **Problem Objectives**

*  Build a model to forecast workforce size over the next 6 months
  
*  Estimate expected employee exits using attrition predictions
  
*  Understand future hiring needs based on projected workforce changes
  
*  Identify workforce gaps (shortage or surplus) across roles and locations
  
*  Present insights through an interactive Power BI dashboard
  
*  Support HR teams in making informed workforce and hiring decisions

## **Tools & Technologies**

*  Oracle SQL : Data Storage , Data Extraction and Feature Engineering

*  Python : Data Extraction, Data Cleaning, Data Transformation and Machine learning

*  Scikit-learn : Logistic Regression Modeling

*  Pandas : Data Cleaning & Data Transformation

*  Power BI : Data Visualization and Dashboard

## **Data Model**

### *Master Data Tables*

*  Employee master data : PROJECT_EMP_MASTER

*  Career progression : PROJECT_PROMOTION_MASTER

*  Training records : PROJECT_TRAINING_MASTER

*  Performance ratings : PROJECT_PERF_MASTER

*  Absence history : PROJECT_ABSENCE_MASTER

*  Payroll data : PROJECT_SALARY_MASTER

*  Incentive data : PROJECT_INCENTIVE_MASTER

*  Job Rotation data: PROJECT_POSITION_MASTER

### *Fact Data Tables*

*  FACT_Employee_Master
    *  EMP_ID
    *  Name
    *  Gender
    *  DOB
    *  DOJ
    *  Unit Code
    *  Location Code
    *  Function Code
    *  Grade Code
    *  DOR
    *  Cadre Code
  
*  FACT_Resignation_probab
    *  EMP_ID
    *  Attrition Probability%
    *  Risk Band (Low/ Medium/ High)
    *  Snapshot Mmonth
    *  Age
    *  Location Code
    *  Tenure (MM)
    *  Training Days (Last 36 Months)
    *  Job Rotations
    *  Perf Slope
    *  Curr Perf Score
    *  Perf Delta
    *  MOnths since Promotion
    *  Stagflation Flag
    *  Incentive Volatility
    *  Incentive (Last 36 Months)
    *  Resig in Same Unit & Grade
    *  Absence Days (6 Months)
    *  Absence Spike
    *  Salary Growth
    *  Compensation Below peer flag
    *  DOR
    *  DOB
    *  DOJ
    *  Resignation Flag (Next 6 Months)

*  FACT_Attrition_Drivers
    *  Attrition Driver
    *  Average Value for High Risk Employees
    *  Average Value for Low Risk Employees
    *  Risk Gap
    *  Manpower Impacted
    *  Impact Score

*  FACT_Attrition_Drivers_Coeff
    *  Attrition Driver
    *  Logistic Regression Model Coefficient
    *  Absolute Value of Coefficient
    *  Impact (Positive/ Negative)

### *Dimension Data Tables*

*  DIM_Cadre_Master
    *  Cadre Code
    *  Cadre Name

*  DIM_Grade_Master
    *  Grade Code
    *  Grade Name

*  DIM_Location_Master
    *  Location Code
    *  Location Name

*  DIM_Unit_Master
    *  Unit Code
    *  Unit Name

*  DIM_Function_Master
    *  Function Code
    *  Function Name

*  DIM_Gender_Master
    *  Gender Code
    *  Gender Name

*  DIM_Date_Table
    *  Date
    *  Year
    *  Month
    *  Day

## **Feature Engineering**

Several predictive features were created to capture behavioral and compensation patterns.

Key engineered features include:

*  training_days_36m : Training Days in last 3 years

*  pos_chng_count : Position Changes in last 3 years

*  perf_slope : (Current Performance Score – Previous Performance Score)/2

*  curr_score : Latest Score

*  Perf_delta : Current – Previous Score

*  months_since_prom : Months since last promotion

*  prom_count : Total Promotions since Joining

*  stagflation : 1 is no promotion in last 3 years

*  incentive_volatility : Standard deviation of last 4 incentives

*  incentive_sum_last3y : Total Incentive in last 3 years

*  absence_days_6m : Total Absence Days in last 6 months

*  absence_rate_3m : Absence Days in last 3 months/ 90

*  absence_rate_30d : Absence Days in last 30 days / 30

*  absence_spike : absence_rate_30d/ absence_rate_3m

*  sal_growth : Change/ Salary 12m ago

*  compa_ratio : Employee salary/median salary of unit/grade

*  below_peer_flag : Y if comparatio <0.95

*  Unit : Organisational Unit

*  Location : Location of Unit

*  Tenure_mm : Tenure in months

*  Age_yy : Age in years

*  Function : Function (Job Specialisation)

*  Resig_flag : Y if Resigned in coming 6 months

*  resig_same_unit_grade : Resigned same unit/grade in past 12 months

## **Machine Learning Model**

The attrition prediction model uses Logistic Regression.

*  Target Variable : RESIG_FLAG

*  Model Output : Probability of employee resignation

*  Model performance metric : ROC AUC Score

## **Power BI Dashboard**

The Power BI dashboard provides several analytical views:

*  Executive Overview : Summary metrics for attrition trends and workforce risk.

*  Attrition History : Historical attrition patterns across departments and locations.

*  Attrition Risk Prediction : Identification of employees with high predicted attrition probability.

*  Employee Risk Register : Detailed list of employees with high resignation probability.

*  Attrition Driver Diagnostics : Analysis of factors influencing attrition risk.

## **Key Insights**

Analysis of employee attrition drivers indicates that resignation risk is primarily influenced by three factors:

*  Current Performance Score – Employees with low performance scores show significantly higher attrition probability, making this the strongest driver.

*  Incentive Volatility – High variability in incentive payouts is strongly associated with increased resignation risk.

*  Early Career Employees (Age / Tenure) – Younger employees and those with shorter tenure exhibit elevated attrition risk.

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


## **Disclaimer**

This project was developed using internal organizational HR data.

Due to confidentiality restrictions, the original dataset and Power BI file containing real employee data are not included.

Sample structures and screenshots are provided for demonstration purposes.

## Author

Asad Ali
