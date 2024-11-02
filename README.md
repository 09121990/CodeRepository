=CALCULATE(
    SUM(SO_Sls[KG]),
    FILTER(
        SO_Sls,
         YEAR(SO_Sls[date]) = 2024 &&
         MONTH(SO_Sls[date]) = 10  
       --  DAY(SO_Sls[date]) <= DAY(TODAY()-1)
    )
)
=CALCULATE(
    SUM(SO_Sls[KG]),
    FILTER(
        SO_Sls,
        MONTH(SO_Sls[date]) = 10 && 
        YEAR(SO_Sls[date]) = 2024 && 
        RELATED(SO[Area Name]) <> ""  // Adjust the condition as needed
    )
)
=SUMX(
    SO,
    IF(
        NOT(ISBLANK(SO[SR/SO Name])),
        IF(
            [IMS_Sept] > 0,
            [IMS_Oct] - [IMS_Sept],
            0
        ),
        BLANK()
    )
)