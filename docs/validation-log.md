# Validation log

Checks run against the source file and the built workbook (2026-10-15).

| # | Check | Result |
|---|---|---|
| 1 | Source file row count | 36,994 rows x 246 columns, as documented |
| 2 | Years present | 2014-2024, all 11 years |
| 3 | State slice | 51 geographies (50 states + DC) x 11 years = 561 rows, no gaps |
| 4 | National benchmark | $348.5B total standardized payments, 2024; per-beneficiary $12,553 |
| 5 | Category shares sum | 17 categories sum to 98.6% (remainder = Part B other services) |
| 6 | Q1 top category | Inpatient hospital 22.9% ($79.8B) |
| 7 | Q2 extremes | FL $14,680 max, HI $8,622 min; ratio 1.70x |
| 8 | Q3 growth | $9,191 (2014) to $12,553 (2024) = +36.6% |
| 9 | Q4 correlation | r = +0.81 (spending vs inpatient stays per 1,000) |
| 10 | Q5 correlation | r = +0.63 (spending vs readmission rate); DC 20.4% max, UT 13.4% min |
| 11 | Workbook integrity | 9 sheets, 572 data rows, 5 charts, 0 em dashes, all titles intact |
| 12 | Dashboard formulas | SUMIFS/MAXIFS/MINIFS reference Data_State rows 5-576; verified against Python values |

All findings in the README trace to these checks.
