# Data dictionary

Field definitions for the `Data_State` sheet (from the CMS data dictionary, condensed).

| Field | Definition |
|---|---|
| State | Two-letter state code (50 states + DC). Territories excluded. |
| Year | Calendar year of the Medicare claims, 2014-2024. |
| Beneficiaries | Number of Original Medicare beneficiaries in the state-year. |
| Total std payment ($B) | Total standardized Medicare payments, in billions. Standardized = CMS price adjustment removes wage index and policy add-ons. |
| Std $ per beneficiary | Total standardized payments / beneficiaries. The core efficiency metric. |
| IP % | Share of standardized payments: inpatient hospital. |
| OP % | Share: outpatient hospital. |
| E&M % | Share: physician evaluation & management services. |
| SNF % | Share: skilled nursing facility. |
| DME % | Share: durable medical equipment. |
| HH % | Share: home health. |
| Procedures % | Share: procedures. |
| Hospice % | Share: hospice. |
| IP stays per 1,000 | Covered inpatient stays per 1,000 beneficiaries (utilization). |
| ER visits per 1,000 | Emergency department visits per 1,000 beneficiaries (utilization). |
| Readmission % | Acute hospital 30-day readmission rate (quality: lower is better). |
| Dual % | Share of beneficiaries dually eligible for Medicare and Medicaid. |
| Avg age | Average beneficiary age. |
| National rows | Benchmark rows (State = "National") appended after the state rows; used by Dashboard formulas. |
