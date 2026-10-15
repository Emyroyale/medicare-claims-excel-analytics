# Excel metric definitions

Two versions of every headline metric: the **Excel formulas actually used** in `dashboard/Medicare_Financial_Analysis_2014_2024.xlsx`, and **DAX equivalents** for a Power Pivot model built on the same `Data_State` table.

## Excel formulas (in the workbook)

All formulas read the `Data_State` sheet (rows 5-576: 51 geographies x 11 years + National benchmarks).

| Metric | Excel formula |
|---|---|
| US std $ per beneficiary, 2024 | `=SUMIFS(Data_State!E$5:$576,Data_State!A$5:$576,"National",Data_State!B$5:$576,2024)` |
| Highest state, 2024 | `=MAXIFS(Data_State!E$5:$576,Data_State!A$5:$576,"<>National",Data_State!B$5:$576,2024)` |
| Lowest state, 2024 | `=MINIFS(Data_State!E$5:$576,Data_State!A$5:$576,"<>National",Data_State!B$5:$576,2024)` |
| 10-yr per-beneficiary growth | `=(SUMIFS(...2024...)-SUMIFS(...2014...))/SUMIFS(...2014...)` |
| Inpatient share of spending, 2024 | `=SUMIFS(Data_State!F$5:$576,Data_State!A$5:$576,"National",Data_State!B$5:$576,2024)` |
| Outpatient share of spending, 2024 | `=SUMIFS(Data_State!G$5:$576,Data_State!A$5:$576,"National",Data_State!B$5:$576,2024)` |

## DAX equivalents (Power Pivot)

```dax
-- Base measures on the Data_State table
Total Std Payments (B) =
    SUM ( Data_State[Total std payment ($B)] )

Std $ per Beneficiary =
    DIVIDE (
        SUM ( Data_State[Total std payment ($B)] ) * 1e9,
        SUM ( Data_State[Beneficiaries] )
    )

-- Headline KPIs
US Std $ per Bene 2024 =
    CALCULATE (
        [Std $ per Beneficiary],
        Data_State[State] = "National",
        Data_State[Year] = 2024
    )

Highest State 2024 =
    MAXX (
        FILTER ( VALUES ( Data_State[State] ), Data_State[State] <> "National" ),
        CALCULATE ( [Std $ per Beneficiary], Data_State[Year] = 2024 )
    )

Lowest State 2024 =
    MINX (
        FILTER ( VALUES ( Data_State[State] ), Data_State[State] <> "National" ),
        CALCULATE ( [Std $ per Beneficiary], Data_State[Year] = 2024 )
    )

10-Yr per-Bene Growth =
    VAR v2024 =
        CALCULATE ( [Std $ per Beneficiary], Data_State[State] = "National", Data_State[Year] = 2024 )
    VAR v2014 =
        CALCULATE ( [Std $ per Beneficiary], Data_State[State] = "National", Data_State[Year] = 2014 )
    RETURN DIVIDE ( v2024 - v2014, v2014 )

Inpatient Share 2024 =
    CALCULATE (
        AVERAGE ( Data_State[IP %] ),
        Data_State[State] = "National",
        Data_State[Year] = 2024
    )
```

Note: share columns (IP %, OP %, ...) are precomputed in `Data_State`; the DAX averages the National row directly.
