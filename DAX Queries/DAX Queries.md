# **DAX Queries**

*  ##	**Historical Attrition Trend**

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

                         


##	**Attrition Risk Predictive Analysis**



##	**Attrition Risk Register**



##	**Attrition Diagnostic Analysis**
