# HR Analytics Dashboard | Power BI

Interactive HR analytics report for workforce composition, attrition, job satisfaction, compensation and tenure.
# Dashboard
<img width="1204" height="675" alt="Dashboard" src="https://github.com/user-attachments/assets/aa820932-94ac-4fcb-981d-f363bda9c3c9" />


## Business problem
HR stakeholders need a consistent view of headcount and recorded attrition across departments, job roles and employee groups. This project uses Power BI to explore patterns in a cross-sectional HR dataset; it does not determine why employees leave.

## Dataset and validation
- Source: `HR_Analytics-DataSet.csv`, 1,480 rows and 38 columns.
- 1,470 unique `EmpID` values; ten IDs repeat and seven complete rows are duplicates.
- 57 missing values in `YearsWithCurrManager`.
- Inconsistent `BusinessTravel` values: `Travel_Rarely` and `TravelRarely`.
- Dashboard baseline uses one row per employee ID; inspect conflicting duplicates before selecting a record.

## Verified baseline KPIs (deduplicated)
| Measure | Value |
|---|---:|
| Distinct employees | 1,470 |
| Employees with Attrition = Yes | 237 |
| Attrition rate | 16.12% |
| Average age | 36.92 years |
| Average monthly income | 6,502.93 (currency unspecified) |
| Average years at company | 7.01 |

## Power BI report
The PBIX includes six KPI cards, a department slicer, an education donut chart, an age-group column chart, a job-satisfaction matrix, salary-band and job-role bar charts, a tenure area chart and a gender treemap. The original model's DAX expressions could not be independently extracted; the rebuilding guide provides equivalent documented examples.

## Rebuild
1. Install Power BI Desktop.
2. Import the CSV through Power Query and validate data types.
3. Preserve the raw query, create a cleaned reference query and resolve duplicate IDs.
4. Add DAX measures for headcount, attrition and averages.
5. Rebuild visuals and configure department slicer interactions.
6. Validate totals, refresh behavior, sorting and labels.
7. Export a report screenshot and publish only privacy-safe files.

See `HR_Analytics_Rebuild_Guide.pdf` for detailed instructions, DAX, slicer configuration and optional Excel VBA examples.

## Example DAX
```dax
Headcount = DISTINCTCOUNT(HR_Analytics[EmpID])
Attrition Count = CALCULATE(DISTINCTCOUNT(HR_Analytics[EmpID]), HR_Analytics[Attrition] = "Yes")
Attrition Rate = DIVIDE([Attrition Count], [Headcount], 0)
Avg Age = AVERAGE(HR_Analytics[Age])
Avg Monthly Income = AVERAGE(HR_Analytics[MonthlyIncome])
Avg Tenure = AVERAGE(HR_Analytics[YearsAtCompany])
```

## Data dictionary
- **EmpID**: Employee identifier; use distinct count and verify duplicate records.
- **Age**: Employee age in years.
- **AgeGroup**: Age band, such as 18–25 or 26–35.
- **Attrition**: Yes/No indicator that an employee left.
- **BusinessTravel**: Business travel frequency; contains inconsistent TravelRarely spelling.
- **DailyRate**: Recorded daily pay rate; currency not documented.
- **Department**: Employee department.
- **DistanceFromHome**: Reported distance from home; units unspecified.
- **Education**: Numeric education-level code; mapping requires confirmation.
- **EducationField**: Field of education.
- **EmployeeCount**: Row-level count indicator, usually 1; sums include duplicates.
- **EmployeeNumber**: Additional numeric employee identifier.
- **EnvironmentSatisfaction**: Ordinal environment satisfaction score.
- **Gender**: Recorded gender category.
- **HourlyRate**: Recorded hourly pay rate; currency unspecified.
- **JobInvolvement**: Ordinal job involvement score.
- **JobLevel**: Numeric job-level code.
- **JobRole**: Employee job role.
- **JobSatisfaction**: Ordinal job satisfaction score.
- **MaritalStatus**: Reported marital status.
- **MonthlyIncome**: Recorded monthly income; currency unspecified.
- **SalarySlab**: Monthly income band.
- **MonthlyRate**: Separate rate field; definition and units not documented.
- **NumCompaniesWorked**: Number of companies worked for.
- **Over18**: Over-18 flag; all records are Y.
- **OverTime**: Yes/No overtime indicator.
- **PercentSalaryHike**: Reported percentage salary increase.
- **PerformanceRating**: Ordinal performance rating.
- **RelationshipSatisfaction**: Ordinal relationship satisfaction score.
- **StandardHours**: Standard hours value; constant in source.
- **StockOptionLevel**: Stock option level code.
- **TotalWorkingYears**: Total years of work experience.
- **TrainingTimesLastYear**: Training sessions in the previous year.
- **WorkLifeBalance**: Ordinal work-life balance score.
- **YearsAtCompany**: Employee tenure in years.
- **YearsInCurrentRole**: Years in present job role.
- **YearsSinceLastPromotion**: Years since most recent promotion.
- **YearsWithCurrManager**: Years with current manager; 57 missing values.

## Limitations and ethics
The dataset has no reporting date, exit dates or time-series snapshots, so attrition is a cross-sectional proportion, not an annualized turnover rate. The currency and several ordinal code mappings are undocumented. Avoid causal conclusions and do not make individual employment decisions from these visualizations. Publish only a permitted, anonymized or synthetic source dataset.

## Tools
Power BI Desktop, Power Query, DAX, CSV/Excel, interactive visuals and slicers. VBA examples in the guide apply to an optional Excel companion only.
