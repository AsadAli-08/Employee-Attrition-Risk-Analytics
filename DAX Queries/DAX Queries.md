# **DAX Queries**

##	**Historical Attrition Trend**

            *  Resignations Till Date =
                        CALCULATE (
                            DISTINCTCOUNT ( FACT_Employee_Master[Emp ID] ),
                            FILTER (
                                FACT_Employee_Master,
                                FACT_Employee_Master[Reason] = "Resignation"
                                    && FACT_Employee_Master[DOR] >= MIN ( DIM_Date_Table[Date] )
                                    && FACT_Employee_Master[DOR] <= MAX ( DIM_Date_Table[Date] )
                            )
                        )
            
            *  Avg_HeadCount =
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


##	**Attrition Risk Predictive Analysis**



##	**Attrition Risk Register**



##	**Attrition Diagnostic Analysis**
