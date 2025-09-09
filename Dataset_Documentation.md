# New York State Foster Care Analysis Datasets Documentation

This document provides comprehensive documentation for all datasets used in the New York State Foster Care Analysis project. The datasets are sourced from data.ny.gov and cover various social, economic, and administrative factors that may influence foster care outcomes in New York State.

## Project Overview

**Goal**: To understand the effects of environmental factors such as crime, taxation/fees, earned income, and social services staffing on the number of foster care children and related outcomes to inform policy decisions.

**Primary Alignment Strategy**: All datasets will be aligned by **County** and **Year** for comprehensive analysis.

---

## 1. Children in Foster Care Annually Dataset

### Description
Annual data on children in foster care by county in New York State, showing placement types, care statistics, and child protective services reports from 1994 to 2024.

### Source File
`Data/ChildrenFosterCareAnnually/Children_in_Foster_Care_Annually___Beginning_1994_20250908.csv`

### Dataset Characteristics
- **Time Range**: 1994-2024 (30 years)
- **Geographic Coverage**: 62 counties in New York State
- **Data Granularity**: Annual data by county
- **Total Records**: 1,830 rows

### Columns and Data Types
| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| County | string | County name in New York State |
| Year | int64 | Calendar year |
| Adoptive Home | int64 | Days in adoptive home care |
| Agency Operated Boarding Home | int64 | Days in agency operated boarding homes |
| Approved Relative Home | int64 | Days in approved relative homes |
| Foster Boarding Home | int64 | Days in foster boarding homes |
| Group Home | int64 | Days in group home care |
| Group Residence | int64 | Days in group residence care |
| Institution | int64 | Days in institutional care |
| Supervised Independent Living | int64 | Days in supervised independent living |
| Other | int64 | Days in other care arrangements |
| Total Days In Care | int64 | Total days all children spent in care |
| Admissions | int64 | Number of children admitted to foster care |
| Discharges | int64 | Number of children discharged from foster care |
| Children In Care | int64 | Number of children in care at year end |
| Number of Children Served | int64 | Total number of children served during year |
| Indicated CPS Reports | int64 | Number of indicated child protective services reports |

### Key Variables for Analysis
- **Dependent Variables**: Children In Care, Admissions, Discharges, Number of Children Served
- **Care Quality Indicators**: Distribution across placement types, Total Days In Care
- **Risk Indicators**: Indicated CPS Reports

---

## 2. Child Health Plus Program Enrollment Dataset

### Description
Monthly enrollment data for the Child Health Plus program by county and health insurance plan, covering children's health insurance enrollment from 2009 to 2025.

### Source File
`Data/ChildHealthPlusenrollmentByCountyInsurer/Child_Health_Plus_Program_Enrollment_by_County_and_Insurer__Beginning_2009_20250909.csv`

### Dataset Characteristics
- **Time Range**: 2009-2025 (16 years)
- **Geographic Coverage**: 62 counties in New York State
- **Data Granularity**: Monthly data by county and insurance plan
- **Total Records**: 48,623 rows

### Columns and Data Types
| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| Eligibility Year | int64 | Year of eligibility |
| Eligibility Month | int64 | Month of eligibility (1-12) |
| County | string | County name in New York State |
| Plan Name | object | Name of health insurance plan |
| Number of Enrollees | int64 | Number of children enrolled in the plan |

### Data Aggregation Requirements
- **For Annual Analysis**: Aggregate monthly data by county and year
- **Health Access Indicator**: Total enrollees per county per year as proxy for children's health service access

---

## 3. Index Crimes by County and Agency Dataset

### Description
Annual crime statistics by county and law enforcement agency, including violent and property crimes from 1990 to 2024.

### Source File
`Data/CrimeData/Index_Crimes_by_County_and_Agency__Beginning_1990_20250909.csv`

### Dataset Characteristics
- **Time Range**: 1990-2024 (34 years)
- **Geographic Coverage**: 62 counties in New York State
- **Data Granularity**: Annual data by county and agency
- **Total Records**: 23,830 rows

### Columns and Data Types
| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| County | string | County name in New York State |
| Agency | object | Law enforcement agency name |
| Year | int64 | Calendar year |
| Months Reported | float64 | Number of months agency reported data |
| Index Total | int64 | Total index crimes |
| Violent Total | int64 | Total violent crimes |
| Murder | int64 | Number of murders |
| Rape | int64 | Number of rapes |
| Robbery | int64 | Number of robberies |
| Aggravated Assault | int64 | Number of aggravated assaults |
| Property Total | int64 | Total property crimes |
| Burglary | int64 | Number of burglaries |
| Larceny | int64 | Number of larcenies |
| Motor Vehicle Theft | int64 | Number of motor vehicle thefts |
| Region | object | Geographic region classification |

### Data Aggregation Requirements
- **For County Analysis**: Sum all crime statistics by county and year across all agencies
- **Crime Rate Calculation**: Consider population data for per-capita crime rates

---

## 4. Child Care Regulated Programs Dataset

### Description
Point-in-time snapshot of all regulated child care programs in New York State, including facility details, capacity, and location information.

### Source File
`Data/NY_Child_Care_Regulated_Programs/Child_Care_Regulated_Programs_20250908.csv`

### Dataset Characteristics
- **Time Range**: Point-in-time snapshot (September 2025)
- **Geographic Coverage**: All counties in New York State
- **Data Granularity**: Individual facility level
- **Total Records**: 16,378 facilities

### Columns and Data Types
| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| Facility ID | string | Unique facility identifier |
| Program Type | object | Type of child care program |
| Region Code | object | Regional office code |
| County | string | County name in New York State |
| Facility Status | object | Current status of facility |
| Facility Name | object | Name of the facility |
| Facility Opened Date | object | Date facility opened |
| License Issue Date | object | Date license was issued |
| License Expiration Date | object | Date license expires |
| Address Omitted | object | Whether address is omitted for privacy |
| Street Number | object | Street number |
| Street Name | object | Street name |
| Additional Address | object | Additional address information |
| Floor | object | Floor number |
| Apartment | object | Apartment number |
| City | object | City name |
| State | object | State (NY) |
| Zip Code | string | ZIP code (preserved as string) |
| Phone Number Omitted | object | Whether phone number is omitted |
| Phone Number | string | Phone number (preserved as string) |
| Phone Extension | object | Phone extension |
| Provider Name | object | Name of care provider |
| School District Name | object | School district name |
| Capacity Description | object | Text description of capacity |
| Infant Capacity | int64 | Number of infants facility can serve |
| Toddler Capacity | int64 | Number of toddlers facility can serve |
| Preschool Capacity | int64 | Number of preschoolers facility can serve |
| School Age Capacity | int64 | Number of school-age children facility can serve |
| Total Capacity | int64 | Total capacity of facility |
| Program Profile | object | URL to program profile |
| Latitude | float64 | Geographic latitude |
| Longitude | float64 | Geographic longitude |
| Georeference | object | Geographic reference point |

### Data Aggregation Requirements
- **For County Analysis**: Aggregate facilities, total capacity, and program types by county
- **Capacity Analysis**: Sum capacity by age group and program type per county

---

## 5. Public Assistance Cases with Earned Income Dataset

### Description
Monthly data on public assistance cases with earned income by district, including TANF and SNA programs from April 2006 to present.

### Source File
`Data/PublicAssistanceCasesEarnedIncome/Public_Assistance_Cases_with_Earned_Income___Beginning_April_2006_20250908.csv`

### Dataset Characteristics
- **Time Range**: 2006-2024 (18+ years)
- **Geographic Coverage**: 58 social services districts in New York State
- **Data Granularity**: Monthly data by district
- **Total Records**: 13,400 rows

### Columns and Data Types
| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| Year | int64 | Calendar year |
| Month | object | Month name |
| Month Code | int64 | Numeric month code (1-12) |
| District Code | int64 | Numeric district identifier |
| District | string | District name |
| TANF Cases with Earned Income | int64 | Number of TANF cases with earned income |
| TANF Average Gross Earned Income | int64 | Average gross earned income for TANF cases |
| TANF Average Net Earned Income | int64 | Average net earned income for TANF cases |
| SNA MOE Cases with Earned Income | int64 | Number of SNA MOE cases with earned income |
| SNA MOE Average Gross Earned Income | int64 | Average gross earned income for SNA MOE cases |
| SNA MOE Average Net Earned Income | int64 | Average net earned income for SNA MOE cases |
| SNA Non-MOE Cases with Earned Income | int64 | Number of SNA Non-MOE cases with earned income |
| SNA Non-MOE Average Gross Earned Income | int64 | Average gross earned income for SNA Non-MOE cases |
| SNA Non-MOE Average Net Earned Income | int64 | Average net earned income for SNA Non-MOE cases |

### Data Aggregation Requirements
- **For Annual Analysis**: Aggregate monthly data to annual averages by district
- **District-County Mapping**: Map social services districts to counties for alignment

---

## 6. Local Social Services District Staff Counts Dataset

### Description
Annual staffing data for Local Social Services Districts by function, from State Fiscal Year 2004-2005 to present.

### Source File
`Data/SocialServiceStaffByYear/Local_Social_Services_District__SSD__Staff_Counts_by_Function__Beginning_State_Fiscal_Year_2004-2005_20250909.csv`

### Dataset Characteristics
- **Time Range**: Fiscal Years 2005-2024 (19 years)
- **Geographic Coverage**: 58 social services districts in New York State
- **Data Granularity**: Annual data by district and function
- **Total Records**: 1,180 rows

### Columns and Data Types
| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| State Fiscal Year Ending | int64 | Fiscal year ending date |
| District Code | int64 | Numeric district identifier |
| District | string | District name |
| Total Staffing | int64 | Total number of staff |
| Intake/Case Maintenance | int64 | Staff in intake/case maintenance |
| Services Program | int64 | Staff in services programs |
| Services Administration | int64 | Staff in services administration |
| Employment Programs | int64 | Staff in employment programs |
| Medicaid Eligibility Determination and Payment Authorization | int64 | Staff in Medicaid eligibility |
| Medicaid Policy Planning and Administration | int64 | Staff in Medicaid policy/admin |
| Training | int64 | Staff in training |
| Supplemental Nutrition Assistance Program | int64 | Staff in SNAP |
| Child Support | int64 | Staff in child support |
| Fraud and Abuse | int64 | Staff in fraud and abuse |
| Home Energy Assistance Program | int64 | Staff in HEAP |
| Welfare Management System | int64 | Staff in welfare management systems |
| Other Reimbursable Programs | int64 | Staff in other reimbursable programs |
| TANF Funded Services | int64 | Staff in TANF funded services |
| Administrative Overhead | int64 | Administrative overhead staff |
| Non-Administrative Local Program | int64 | Non-administrative local program staff |
| Overall Overhead | int64 | Overall overhead staff |

### Key Variables for Analysis
- **Child Services Staffing**: Services Program, Intake/Case Maintenance, Child Support
- **Total Capacity**: Total Staffing
- **Efficiency Indicators**: Ratios of service staff to administrative staff

---

## 7. State Taxes and Fees Collected Dataset

### Description
Annual collection data for various state taxes and fees by category from Fiscal Year 1995 to 2024.

### Source File
`Data/StateTaxesFeesSince1995/State_Taxes_and_Fees_Collected__Beginning_Fiscal_Year_Ending_March_31__1995_20250909.csv`

### Dataset Characteristics
- **Time Range**: Fiscal Years 1995-2024 (29 years)
- **Geographic Coverage**: Statewide (not county-specific)
- **Data Granularity**: Annual data by tax/fee type
- **Total Records**: 1,626 rows

### Columns and Data Types
| Column Name | Data Type | Description |
|-------------|-----------|-------------|
| Fiscal Year Ended | int64 | Fiscal year ending |
| Tax Category | object | Category of tax or fee |
| Tax or Fee | object | Specific tax or fee name |
| Amount Collected | int64 | Amount collected in dollars |
| Tax or Fee Sort Order | int64 | Sort order for reporting |

### Tax Categories
- Personal Income
- Corporation and Business
- Sales and Use
- Motor Fuel
- Motor Vehicle
- Other

### Usage in Analysis
- **Economic Context**: Statewide economic indicators
- **Revenue Trends**: State fiscal capacity over time
- **Per-County Estimation**: May be allocated to counties using population or economic activity weights

---

## Data Alignment Strategy

### Primary Alignment Dimensions
1. **Geographic**: County (with district-to-county mapping where needed)
2. **Temporal**: Calendar/Fiscal Year

### Common Time Period
**Recommended Analysis Period: 2009-2024**
- Best overlap across all datasets
- 15 years of data for trend analysis
- Covers both pre and post-economic recovery periods

### Required Data Transformations

#### 1. Geographic Standardization
- Map Social Services Districts to Counties
- Aggregate facility-level data to county level
- Standardize county name formatting

#### 2. Temporal Standardization
- Convert fiscal years to calendar years where appropriate
- Aggregate monthly data to annual data
- Handle partial year reporting

#### 3. Data Aggregation
- **Crime Data**: Sum by county and year across all agencies
- **Child Health Plus**: Sum enrollees by county and year
- **Child Care**: Sum facilities and capacity by county
- **Public Assistance**: Average monthly values to annual by district/county
- **State Taxes**: Use as statewide context variable

### Missing Data Considerations
- Some counties may have missing data in certain years
- Facility-level data represents point-in-time snapshot
- Crime reporting completeness varies by agency and year

### Data Quality Checks Required
1. County name standardization across datasets
2. Year range validation and alignment
3. Missing value analysis by county and year
4. Outlier detection for key variables
5. Consistency checks for calculated fields

---

## Analysis Framework

### Primary Research Questions
1. How do crime rates correlate with foster care placement rates?
2. What is the relationship between social services staffing levels and foster care outcomes?
3. How do economic factors (public assistance, health insurance coverage) relate to child welfare outcomes?
4. What role does child care availability play in family stability and foster care prevention?
5. How do statewide economic conditions (tax revenue) correlate with county-level child welfare outcomes?

### Key Performance Indicators
- Foster care entry and exit rates
- Length of stay in foster care
- Placement stability (multiple placements)
- Child protective services report rates
- Social services staffing ratios
- Child care capacity per child population
- Crime rates per capita
- Economic distress indicators

This documentation provides the foundation for comprehensive analysis of factors affecting foster care outcomes in New York State, enabling evidence-based policy recommendations.
