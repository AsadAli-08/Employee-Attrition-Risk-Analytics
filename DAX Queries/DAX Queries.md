# **DAX Queries**

##	**1) Historical Attrition Trend**

####           Resignations (In specified Period) =
                        CALCULATE (
                            DISTINCTCOUNT ( FACT_Employee_Master[Emp ID] ),
                            FILTER (
                                FACT_Employee_Master,
                                FACT_Employee_Master[Reason] = "Resignation"
                                    && FACT_Employee_Master[DOR] >= MIN ( DIM_Date_Table[Date] )
                                    && FACT_Employee_Master[DOR] <= MAX ( DIM_Date_Table[Date] )
                            )
                        )
            
####           Avg Headcount =
                      VAR max_date =
                          LASTDATE ( DIM_Date_Table[Date] )
                      VAR min_date =
                          FIRSTDATE ( DIM_Date_Table[Date] )
                      RETURN
                          (
                              COUNTX (
                                  FACT_Employee_Master,
                                  IF (
                                      FACT_Employee_Master[DOR] > min_date && FACT_Employee_Master[DOJ] <= min_date,
                                      1,
                                      0
                                  )
                              )
                                  + COUNTX (
                                      FACT_Employee_Master,
                                      IF (
                                          FACT_Employee_Master[DOR] > max_date && FACT_Employee_Master[DOJ] <= max_date,
                                          1,
                                          0
                                      )
                                  )
                          ) / 2


####              Attrition Rate =
                        [Resignations] / [Avg Headcount]              


####              Tenure at Resignation =
                          DATEDIFF ( FACT_Employee_Master[DOJ], FACT_Employee_Master[DOR], YEAR )


####              Average Tenure at Resignation =
                         AVERAGEX (
                              FILTER ( FACT_Employee_Master, FACT_Employee_Master[Reason] = "Resignation" ),
                              FACT_Employee_Master[Tenure at Resig]
                         )

####              Age at Resignation =
                          DATEDIFF ( FACT_Employee_Master[DOB], FACT_Employee_Master[DOR], YEAR )

                         


##	**2) Attrition Risk Predictive Analysis**

####              High Risk Employee =
                            CALCULATE (
                                COUNT ( FACT_Resignation_probab[EMP_ID] ),
                                FACT_Resignation_probab[Risk_Band] = "High"
                                    && FACT_Resignation_probab[DOR] > TODAY ()
                            )

####              Headcount =
                            CALCULATE (
                                COUNT ( FACT_Resignation_probab[EMP_ID] ),
                                FACT_Employee_Master[DOR] > TODAY ()
                            )


####              High Risk Employee % =
                            CALCULATE (
                                COUNT ( FACT_Resignation_probab[EMP_ID] ),
                                FACT_Resignation_probab[Risk_Band] = "High"
                                    && FACT_Resignation_probab[DOR] > TODAY ()
                            ) / [Headcount]





##	**3) Attrition Risk Register**

####              High Risk Employee =
                            CALCULATE (
                                COUNT ( FACT_Resignation_probab[EMP_ID] ),
                                FACT_Resignation_probab[Risk_Band] = "High"
                                    && FACT_Resignation_probab[DOR] > TODAY ()
                            )

####              Headcount =
                            CALCULATE (
                                COUNT ( FACT_Resignation_probab[EMP_ID] ),
                                FACT_Employee_Master[DOR] > TODAY ()
                            )


####              High Risk Employee % =
                            CALCULATE (
                                COUNT ( FACT_Resignation_probab[EMP_ID] ),
                                FACT_Resignation_probab[Risk_Band] = "High"
                                    && FACT_Resignation_probab[DOR] > TODAY ()
                            ) / [Headcount]


##	**4) Attrition Diagnostic Analysis**


####              FACT_Attrition_Drivers =
                            VAR TotalEmployees =
                                CALCULATE (
                                    COUNT ( FACT_Resignation_probab[EMP_ID] ),
                                    FACT_Resignation_probab[Active] = 1
                                )
                            RETURN
                                UNION (
                                    ROW (
                                        "Driver", "Incentive Volatility",
                                        "High Risk Attrition",
                                            CALCULATE (
                                                AVERAGE ( FACT_Resignation_probab[Attrition Probab] ),
                                                FACT_Resignation_probab[IncentiveVolatility_Risk] = "High Risk"
                                            ),
                                        "Low Risk Attrition",
                                            CALCULATE (
                                                AVERAGE ( FACT_Resignation_probab[Attrition Probab] ),
                                                FACT_Resignation_probab[IncentiveVolatility_Risk] = "Low Risk"
                                            ),
                                        "Risk Gap",
                                            CALCULATE (
                                                AVERAGE ( FACT_Resignation_probab[Attrition Probab] ),
                                                FACT_Resignation_probab[IncentiveVolatility_Risk] = "High Risk"
                                            )
                                                - CALCULATE (
                                                    AVERAGE ( FACT_Resignation_probab[Attrition Probab] ),
                                                    FACT_Resignation_probab[IncentiveVolatility_Risk] = "Low Risk"
                                                ),
                                        "Manpower Impacted %",
                                            DIVIDE (
                                                CALCULATE (
                                                    COUNTROWS ( FACT_Resignation_probab ),
                                                    FACT_Resignation_probab[IncentiveVolatility_Risk] = "High Risk"
                                                ),
                                                TotalEmployees
                                            )
                                    ),
                                    ROW (
                                        "Driver", "Absence Days (6 Months)",
                                        "High Risk Attrition",
                                            CALCULATE (
                                                AVERAGE ( FACT_Resignation_probab[Attrition Probab] ),
                                                FACT_Resignation_probab[Absence6M_Risk] = "High Risk"
                                            ),
                                        "Low Risk Attrition",
                                            CALCULATE (
                                                AVERAGE ( FACT_Resignation_probab[Attrition Probab] ),
                                                FACT_Resignation_probab[Absence6M_Risk] = "Low Risk"
                                            ),
                                        "Risk Gap",
                                            CALCULATE (
                                                AVERAGE ( FACT_Resignation_probab[Attrition Probab] ),
                                                FACT_Resignation_probab[Absence6M_Risk] = "High Risk"
                                            )
                                                - CALCULATE (
                                                    AVERAGE ( FACT_Resignation_probab[Attrition Probab] ),
                                                    FACT_Resignation_probab[Absence6M_Risk] = "Low Risk"
                                                ),
                                        "Manpower Impacted %",
                                            DIVIDE (
                                                CALCULATE (
                                                    COUNTROWS ( FACT_Resignation_probab ),
                                                    FACT_Resignation_probab[Absence6M_Risk] = "High Risk"
                                                ),
                                                TotalEmployees
                                            )
                                    ),
                                    ROW (
                                        "Driver", "Age",
                                        "High Risk Attrition",
                                            CALCULATE (
                                                AVERAGE ( FACT_Resignation_probab[Attrition Probab] ),
                                                FACT_Resignation_probab[Age_Risk] = "High Risk"
                                            ),
                                        "Low Risk Attrition",
                                            CALCULATE (
                                                AVERAGE ( FACT_Resignation_probab[Attrition Probab] ),
                                                FACT_Resignation_probab[Age_Risk] = "Low Risk"
                                            ),
                                        "Risk Gap",
                                            CALCULATE (
                                                AVERAGE ( FACT_Resignation_probab[Attrition Probab] ),
                                                FACT_Resignation_probab[Age_Risk] = "High Risk"
                                            )
                                                - CALCULATE (
                                                    AVERAGE ( FACT_Resignation_probab[Attrition Probab] ),
                                                    FACT_Resignation_probab[Age_Risk] = "Low Risk"
                                                ),
                                        "Manpower Impacted %",
                                            DIVIDE (
                                                CALCULATE (
                                                    COUNTROWS ( FACT_Resignation_probab ),
                                                    FACT_Resignation_probab[Age_Risk] = "High Risk"
                                                ),
                                                TotalEmployees
                                            )
                                    ),
                                    ROW (
                                        "Driver", "Tenure",
                                        "High Risk Attrition",
                                            CALCULATE (
                                                AVERAGE ( FACT_Resignation_probab[Attrition Probab] ),
                                                FACT_Resignation_probab[Tenure_Risk] = "High Risk"
                                            ),
                                        "Low Risk Attrition",
                                            CALCULATE (
                                                AVERAGE ( FACT_Resignation_probab[Attrition Probab] ),
                                                FACT_Resignation_probab[Tenure_Risk] = "Low Risk"
                                            ),
                                        "Risk Gap",
                                            CALCULATE (
                                                AVERAGE ( FACT_Resignation_probab[Attrition Probab] ),
                                                FACT_Resignation_probab[Tenure_Risk] = "High Risk"
                                            )
                                                - CALCULATE (
                                                    AVERAGE ( FACT_Resignation_probab[Attrition Probab] ),
                                                    FACT_Resignation_probab[Tenure_Risk] = "Low Risk"
                                                ),
                                        "Manpower Impacted %",
                                            DIVIDE (
                                                CALCULATE (
                                                    COUNTROWS ( FACT_Resignation_probab ),
                                                    FACT_Resignation_probab[Tenure_Risk] = "High Risk"
                                                ),
                                                TotalEmployees
                                            )
                                    ),
                                    ROW (
                                        "Driver", "Curr Performance Score",
                                        "High Risk Attrition",
                                            CALCULATE (
                                                AVERAGE ( FACT_Resignation_probab[Attrition Probab] ),
                                                FACT_Resignation_probab[Performance_Risk] = "High Risk"
                                            ),
                                        "Low Risk Attrition",
                                            CALCULATE (
                                                AVERAGE ( FACT_Resignation_probab[Attrition Probab] ),
                                                FACT_Resignation_probab[Performance_Risk] = "Low Risk"
                                            ),
                                        "Risk Gap",
                                            CALCULATE (
                                                AVERAGE ( FACT_Resignation_probab[Attrition Probab] ),
                                                FACT_Resignation_probab[Performance_Risk] = "High Risk"
                                            )
                                                - CALCULATE (
                                                    AVERAGE ( FACT_Resignation_probab[Attrition Probab] ),
                                                    FACT_Resignation_probab[Performance_Risk] = "Low Risk"
                                                ),
                                        "Manpower Impacted %",
                                            DIVIDE (
                                                CALCULATE (
                                                    COUNTROWS ( FACT_Resignation_probab ),
                                                    FACT_Resignation_probab[Performance_Risk] = "High Risk"
                                                ),
                                                TotalEmployees
                                            )
                                    ),
                                    ROW (
                                        "Driver", "Salary Growth",
                                        "High Risk Attrition",
                                            CALCULATE (
                                                AVERAGE ( FACT_Resignation_probab[Attrition Probab] ),
                                                FACT_Resignation_probab[SalaryGrowth_Risk] = "High Risk"
                                            ),
                                        "Low Risk Attrition",
                                            CALCULATE (
                                                AVERAGE ( FACT_Resignation_probab[Attrition Probab] ),
                                                FACT_Resignation_probab[SalaryGrowth_Risk] = "Low Risk"
                                            ),
                                        "Risk Gap",
                                            CALCULATE (
                                                AVERAGE ( FACT_Resignation_probab[Attrition Probab] ),
                                                FACT_Resignation_probab[SalaryGrowth_Risk] = "High Risk"
                                            )
                                                - CALCULATE (
                                                    AVERAGE ( FACT_Resignation_probab[Attrition Probab] ),
                                                    FACT_Resignation_probab[SalaryGrowth_Risk] = "Low Risk"
                                                ),
                                        "Manpower Impacted %",
                                            DIVIDE (
                                                CALCULATE (
                                                    COUNTROWS ( FACT_Resignation_probab ),
                                                    FACT_Resignation_probab[SalaryGrowth_Risk] = "High Risk"
                                                ),
                                                TotalEmployees
                                            )
                                    )
                                )

####              Impact Score =
                            FACT_Attrition_Drivers[Risk Gap] * FACT_Attrition_Drivers[Manpower Impacted %]
