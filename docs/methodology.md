# Methodology

## Source

CMS Medicare Fee-for-Service Geographic Variation Public Use File, National/State/County edition (data.cms.gov), covering 2014-2024. Public domain (U.S. government work).

## Population

- Original (fee-for-service) Medicare beneficiaries only. Medicare Advantage is excluded by the source file.
- State level, `BENE_AGE_LVL = All`.
- 50 states + District of Columbia. Territories (PR, VI, GU, MP, AS) and aggregate rows ("Territory", "ZZ", "Unknown") are excluded from state rankings because their payment rules differ.

## Standardized payments

All spending comparisons use **standardized payments**: CMS removes geographic price differences (hospital wage index, graduate medical education add-ons, other policy adjustments) so that a dollar in Florida means the same unit of care as a dollar in Hawaii. Remaining gaps reflect utilization and practice patterns, not prices. This is the standard measure for geographic-variation research (Dartmouth Atlas tradition).

## Service categories

Shares are computed on standardized payments. The file reports each category's share of total standardized payments; the 17 categories shown sum to ~98.6% nationally, the remainder being Part B other services not broken out in this file.

H2 note: none. Unlike some CMS files, this PUF keeps a stable schema across all years 2014-2024.

## Correlations

Reported r values are Pearson correlations across the 51 geographies in 2024, computed in Python (pandas). They are descriptive, not causal.

## Reproducibility

`build_workbook.py` (pandas + openpyxl) regenerates the entire workbook from the CMS download. Download link is in the script header.
