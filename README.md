# Employee Attrition Risk Analysis

## **Project Overview**

*  This project develops a predictive analytics system to identify employees at high risk of resignation and understand the key factors driving employee attrition.

*  The project integrates Oracle SQL, Python machine learning, and Power BI dashboards to deliver actionable workforce insights.

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

## **Project Architecture**

Oracle Database (Master Data Tables)

↓

Feature Engineering (SQL Views)

↓

Python Data Processing (Data Cleaning & Transformation)

↓

Scikit Learn Machine Learning Model (Logistic Regression Model)

↓

Oracle Database (Attrition Probability & Model Coefficients)

↓

Power BI Dashboard (Data Visualisation, Reporting & Analysis)

## **Data Model**

### *Master Data Tables (ORACLE DB)*

*  Employee master data : PROJECT_EMP_MASTER
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

*  Career progression : PROJECT_PROMOTION_MASTER
    * EMP_ID
    * Promotion Date

*  Training records : PROJECT_TRAINING_MASTER
    * EMP_ID
    * From Date
    * To Date
    * Training Type
    * Training Name

*  Performance ratings : PROJECT_PERF_MASTER
    * EMP_ID
    * From Date
    * End Date
    * Performance Score

*  Absence history : PROJECT_ABSENCE_MASTER
    * EMP_ID
    * From Date
    * End Date

*  Payroll data : PROJECT_SALARY_MASTER
    * EMP_ID
    * From Date
    * End Date
    * Salary Amount

*  Incentive data : PROJECT_INCENTIVE_MASTER
    * EMP_ID
    * Incentive Date
    * Incentive Amount

*  Job Rotation data: PROJECT_POSITION_MASTER
    * EMP_ID
    * From Date
    * End Date
    * Position ID
      
### *Feature Data Tables (ORACLE DB)*

*  PROJECT_SNAP_EMP_MONTH
    *  EMP_ID
    *  Snapshot Month
 
*  PROJECT_FT_ABSENCE
    *  EMP_ID
    *  Snapshot Month
    *  Absence Days (6 Months)
    *  Absence Rate (3 Months)
    *  Absence Rate (30 Days)
    *  Absence Spike

*  PROJECT_FT_COMPA_RATIO
    *  EMP_ID
    *  Snapshot Month
    *  Current Salary
    *  Compa Ratio
    *  Below Peer Flag
  
*  PROJECT_FT_SALARY
    *  EMP_ID
    *  Snapshot Month
    *  Salary Growth

*  PROJECT_FT_RESIG_UNIT_GRADE
    *  EMP_ID
    *  Snapshot Month
    *  Unit
    *  Grade
    *  Resignation Same Unit Grade

*  PROJECT_FT_TRAINING_DAYS
    *  EMP_ID
    *  Snapshot Month
    *  Training Days (6 Months)
      
*  PROJECT_FT_POS_CHNG_COUNT
    *  EMP_ID
    *  Snapshot Month
    *  Position Change Count

*  PROJECT_FT_PERF_SLOPE
    *  EMP_ID
    *  Snapshot Month
    *  Current Score
    *  Score 2 Periods Back
    *  Perf Slope
      
*  PROJECT_FT_PERF_DELTA
    *  EMP_ID
    *  Snapshot Month
    *  Curr Score
    *  Prev Score
    *  Perf Delta

*  PROJECT_FT_MONTHS_SINCE_PROM
    *  EMP_ID
    *  Snapshot Month
    *  Promotion Count
    *  Monce Since Promotion
    *  Stagflation
        
*  PROJECT_FT_INCENTIVE_VOLATILITY
    *  EMP_ID
    *  Snapshot Month
    *  Incentive Volatility
      
*  PROJECT_FT_INCENTIVE_SUM
    *  EMP_ID
    *  Snapshot Month
    *  Incentive (Last 3 Years)
      
*  PROJECT_FT_RESIG_FLAG
    *  EMP_ID
    *  Snapshot Month
    *  Resig Flag
    *  Resig Date
    *  Resig Type
    *  Resig Reason
 
*  PROJECT_MONTHLY_SNAPSHOT
    *  EMP_ID
    *  Snapshot Month
    *  Age (YY)
    *  Function
    *  Cadre Code
    *  Grade Code
    *  Unit Code
    *  Location Code
    *  Tenure (MM)
    *  Training Days (Last 36 Months)
    *  Position Change Count
    *  Perf Slope
    *  Curr Perf Score
    *  Perf Delta
    *  Months Since Promotion
    *  Promotion Count
    *  Stagflation
    *  Incentive Volatility
    *  Incentive Last 3 Years
    *  Resignation Same Unit Grade
    *  Absence Days (6 Months)
    *  Absence Rate (3 Months)
    *  Absence Rate (30 Days)
    *  Absence Spike
    *  Salary Growth
    *  Compa Ratio
    *  Below Peer Flag
    *  Resignation Flag
      
### *Fact Data Tables (Power BI)*

*  FACT_Employee_Master (Source: PROJECT_EMP_MASTER (ORACLE DB))
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
  
*  FACT_Resignation_probab (Generated by Python & saved in Oracle DB) 
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

*  FACT_Attrition_Drivers (Generated by Python & saved in Oracle DB)  
    *  Attrition Driver
    *  Average Value for High Risk Employees
    *  Average Value for Low Risk Employees
    *  Risk Gap
    *  Manpower Impacted
    *  Impact Score

*  FACT_Attrition_Drivers_Coeff (Generated by Python & saved in Oracle DB) 
    *  Attrition Driver
    *  Logistic Regression Model Coefficient
    *  Absolute Value of Coefficient
    *  Impact (Positive/ Negative)

### *Dimension Data Tables (Power BI)*

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

*  Executive Overview :
    * Filters : Date/ Unit/ Location/ Cadre/ Grade/ Gender/ Function
    * KPIs : Headcount (As on Date)/ Attrition % (Last 10 Years) / Resignations (Last 10 Years)/ Predicted High Risk Employee %/ Predicted High Risk Employee Count
    * Visuals : Key Factors impacting Attrition (Clustered Column Chart) / Historical Attrition Trend (Line Chart)/ Attrition Risk Distribution (Pie Chart)/ Historical                         Attrition by Cadre-Grade (Column Chart) / Attrition Risk Heatmap (Matrix)/ Top 50 Employees at Risk (Table)


*  Historical Attrition Trend :
    * Filters : Date/ Unit/ Location/ Cadre/ Grade/ Gender/ Function
    * KPIs : Resignations (Last 10 Years)/ Attrition % (Last 10 Years)/ Average Tenure at Resignation/ Average age at Resignation
    * Visuals : Historical Attrition Trend (Last 10 years) (Line Chart)/ Historical Attrition Rate Heatmap (Matrix)/ Historical Attrition Rate by Unit-Function (Bar Chart)/                    Historical Attrition Rate by Cadre-Grade (Column Chart)/ Historical Attrition Rate by Tenure Band (Column Chart)/ Historical Attrition Rate by Age Band (Column Chart)/ Employee wise Historical Attrition Details (Table)
    * Observations :
        *  Attrition rate has shown fluctuations over the past 10 years, but there is an overall declining trend
        *  Executive Trainees and Supervisor Trainees have experienced the highest attrition
        *  Units 15 and 26 (Anonymised) have consistently recorded higher attrition levels
        *  Function 347 (Anonymised) shows the highest attrition among all functions
        *  Attrition is highest in employees with 0–10 years of tenure and decreases as tenure increases
        *  Employees in the 20–30 age group have the highest attrition, with attrition reducing as age increases

*  Attrition Risk Prediction :
    * Filters : Date/ Unit/ Location/ Cadre/ Grade/ Gender/ Function
    * KPIs :  Predicted High Risk Employee %/ High Risk Employee Count/ Medium Risk Employee Count/ Low Risk Employee Count
    * Visuals : Attrition Risk Probability Distribution (Column Chart)/ Attrition Risk Band Distribution (Pie Chart)/ Attrition Risk Heatmap (Matrix)/ Attrition Risk by                 Tenure Band (Bar Chart)/ Attrition Risk by Age Band (Bar Chart)/ Attrition Risk by Cadre-Grade (Bar Chart)
    * Observations  :
        *  Around 4.74% of employees (1,292 employees) are at high risk of attrition
        *  Majority of employees (~89%) are at low risk, while ~6% fall in the medium risk category
        *  Executive and Supervisor Trainee cadres show the highest concentration of high-risk employees
        *  Employees with 0–10 years of tenure are significantly more prone to attrition risk
        *  The 18–25 age group has the highest attrition risk, which reduces with increasing age
        *  Units 5, 6, 16, 28, 30, and 34 (Anonymised) have a higher proportion of at-risk employees
        *  Functions 342, 347, 361, 354, and 358 (Anonymised) show the highest attrition risk levels

*  Employee Risk Register :
    * Filters : Date/ Unit/ Location/ Cadre/ Grade/ Gender/ Function
    * KPIs :  Headcount (As on Date)/ High Risk Employee Count/ Medium Risk Employee Count/ Predicted High Risk Employee %/ Average Attrition Probability
    * Visuals : Employee Risk Register (Table)

*  Attrition Driver Diagnostics :
    * Visuals : Top Factors impacting Attrition Risk (Bar Chart) / Factor wise Impact Score (Clustered Column Chart)
    * Observations  :
        *  Compa Ratio, Absence Days (last 6 months), and Incentive Volatility are the strongest factors increasing attrition risk
        *  Age, Tenure, Current Performance Score, and Salary Growth (1 year) are associated with lower attrition risk
        *  The largest differences between high-risk and low-risk employees are seen in Current Performance Score, Incentive Volatility, and Age
        *  Tenure, Salary Growth, Current Performance Score, Incentive Volatility, and Age impact a large portion of the workforce
        *  Overall, Current Performance Score, Incentive Volatility, and Age emerge as the most impactful drivers of attrition
 
## **Key Insights**

*  Attrition is primarily an early-career issue, with highest impact in employees aged 18–30 and tenure of 0–10 years
*  Trainee cadres (Executive & Supervisor) are the most vulnerable, indicating gaps in onboarding, role clarity, or career progression
*  Attrition is not uniform and is concentrated in specific units and functions, suggesting localized organizational issues
*  A small segment (~5%) of employees drive most of the attrition risk, enabling focused and targeted interventions
*  Compensation-related factors (Compa Ratio, Incentive Volatility) significantly influence attrition, highlighting the importance of pay stability and fairness
*  Absence patterns act as an early warning signal, indicating disengagement before attrition
*  Performance is a key differentiator, with low-performing employees showing higher attrition risk
*  Employees tend to stabilize as tenure and age increase, indicating retention improves after the early career stage
*  Although overall attrition has declined over time, high-risk pockets still exist within specific employee segments
*  Current Performance Score, Incentive Volatility, and Age are the most impactful drivers influencing attrition across the workforce

## **Disclaimer**

This project was developed using internal organizational HR data.

Due to confidentiality restrictions, the original dataset and Power BI file containing real employee data are not included.

Sample structures and screenshots are provided for demonstration purposes.

## Author

Asad Ali
