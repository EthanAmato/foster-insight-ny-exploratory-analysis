# New York State Foster Care Data Analysis - Dataset Documentation

**Project**: Understanding Environmental Factors Affecting Foster Care Outcomes in New York State  
**Date**: September 9, 2025  
**Data Sources**: Data.ny.gov  
**Analysis Period**: 2009-2024 (optimal overlap period)  

---

## Executive Summary

This documentation covers 7 primary datasets containing information about foster care, crime, social services, economic indicators, and child welfare services across New York State. The datasets have been cleaned, standardized, and prepared for analysis to understand how environmental factors influence foster care outcomes.

**Key Alignment Strategy**: County + Year as primary keys for joining datasets where possible, with district-to-county mapping for social services data.

---

## Dataset Overview

| Dataset | Rows | Columns | Time Range | Geographic Level | Primary Use |
|---------|------|---------|------------|------------------|-------------|
| Foster Care | 1,828 | 17 | 1994-2024 | 59 Counties | Primary outcome variable |
| Child Health Plus | 48,623 | 5 | 2009-2025 | 62 Counties | Health access indicator |
| Crime Data | 23,830 | 15 | 1990-2024 | 62 Counties | Environmental risk factor |
| Child Care Programs | 16,376 | 33 | 2025 (snapshot) | 62 Counties | Family support infrastructure |
| Public Assistance | 13,398 | 14 | 2006-2025 | 59 Districts | Economic distress indicator |
| Social Services Staff | 1,178 | 21 | FY2005-2024 | 58 Districts | Service capacity indicator |
| State Taxes | 1,626 | 5 | FY1995-2024 | Statewide | Economic context |

---

## 1. Foster Care Data
**File**: `Children_in_Foster_Care_Annually___Beginning_1994_20250908.csv`

### Description
Annual foster care statistics by county showing placement types, care duration, admissions, discharges, and child protective services reports. This serves as the primary outcome variable for the analysis.

### Columns and Data Types
| Column | Data Type | Description |
|--------|-----------|-------------|
| County | string | New York State county name |
| Year | int64 | Calendar year |
| Adoptive_Home | int64 | Days of care in adoptive homes |
| Agency_Operated_Boarding_Home | int64 | Days of care in agency boarding homes |
| Approved_Relative_Home | int64 | Days of care with approved relatives |
| Foster_Boarding_Home | int64 | Days of care in foster boarding homes |
| Group_Home | int64 | Days of care in group homes |
| Group_Residence | int64 | Days of care in group residences |
| Institution | int64 | Days of care in institutional settings |
| Supervised_Independent_Living | int64 | Days of care in supervised independent living |
| Other | int64 | Days of care in other placement types |
| Total_Days_In_Care | int64 | Total days of care across all placement types |
| Admissions | int64 | Number of children admitted to foster care |
| Discharges | int64 | Number of children discharged from foster care |
| Children_In_Care | int64 | Number of children in care at year end |
| Number_of_Children_Served | int64 | Total number of children served during the year |
| Indicated_CPS_Reports | int64 | Number of indicated child protective services reports |

### Key Characteristics
- **Geographic Coverage**: 59 counties
- **Temporal Coverage**: 1994-2024 (30 years)
- **Granularity**: Annual data by county
- **Missing Values**: Handled (filled with 0 for counts)
- **Primary Keys**: County + Year

---

## 2. Child Health Plus Enrollment Data
**File**: `Child_Health_Plus_Program_Enrollment_by_County_and_Insurer__Beginning_2009_20250909.csv`

### Description
Monthly enrollment data for New York's Child Health Plus program by county and insurance plan. Indicates access to health insurance for children, which may correlate with family stability and foster care prevention.

### Columns and Data Types
| Column | Data Type | Description |
|--------|-----------|-------------|
| Eligibility_Year | int64 | Year of eligibility |
| Eligibility_Month | int64 | Month of eligibility (1-12) |
| County | string | New York State county name |
| Plan_Name | string | Name of the insurance plan |
| Number_of_Enrollees | int64 | Number of children enrolled |

### Key Characteristics
- **Geographic Coverage**: 62 counties
- **Temporal Coverage**: 2009-2025 (16 years)
- **Granularity**: Monthly data by county and insurer
- **Aggregation Needed**: Monthly to annual for alignment
- **Primary Keys**: County + Eligibility_Year + Eligibility_Month + Plan_Name

---

## 3. Crime Data
**File**: `Index_Crimes_by_County_and_Agency__Beginning_1990_20250909.csv`

### Description
Annual crime statistics by county and law enforcement agency, including violent crimes, property crimes, and specific offense types. Represents environmental risk factors that may correlate with foster care placements.

### Columns and Data Types
| Column | Data Type | Description |
|--------|-----------|-------------|
| County | string | New York State county name |
| Agency | string | Law enforcement agency name |
| Year | int64 | Calendar year |
| Months_Reported | float64 | Number of months agency reported data |
| Index_Total | int64 | Total index crimes |
| Violent_Total | int64 | Total violent crimes |
| Murder | int64 | Number of murders |
| Rape | int64 | Number of rapes |
| Robbery | int64 | Number of robberies |
| Aggravated_Assault | int64 | Number of aggravated assaults |
| Property_Total | int64 | Total property crimes |
| Burglary | int64 | Number of burglaries |
| Larceny | int64 | Number of larcenies |
| Motor_Vehicle_Theft | int64 | Number of motor vehicle thefts |
| Region | string | Geographic region classification |

### Key Characteristics
- **Geographic Coverage**: 62 counties
- **Temporal Coverage**: 1990-2024 (34 years)
- **Granularity**: Annual data by county and agency
- **Aggregation Needed**: Agency to county level
- **Primary Keys**: County + Agency + Year

---

## 4. Child Care Regulated Programs
**File**: `Child_Care_Regulated_Programs_20250908.csv`

### Description
Point-in-time snapshot of licensed child care facilities across New York State. Represents family support infrastructure and child care availability, which may impact foster care prevention.

### Columns and Data Types (Selected Key Columns)
| Column | Data Type | Description |
|--------|-----------|-------------|
| Facility_ID | string | Unique facility identifier |
| Program_Type | string | Type of child care program |
| Region_Code | string | Regional office code |
| County | string | New York State county name |
| Facility_Status | string | Current status of facility |
| Facility_Name | string | Name of the facility |
| Zip_Code | string | ZIP code (preserved with leading zeros) |
| Phone_Number | string | Contact phone number |
| Infant_Capacity | int64 | Licensed capacity for infants |
| Toddler_Capacity | int64 | Licensed capacity for toddlers |
| Preschool_Capacity | int64 | Licensed capacity for preschoolers |
| School_Age_Capacity | int64 | Licensed capacity for school-age children |
| Total_Capacity | int64 | Total licensed capacity |

### Key Characteristics
- **Geographic Coverage**: 62 counties
- **Temporal Coverage**: 2025 snapshot
- **Granularity**: Individual facility level
- **Aggregation Needed**: Facility to county level
- **Primary Keys**: Facility_ID

---

## 5. Public Assistance Cases with Earned Income
**File**: `Public_Assistance_Cases_with_Earned_Income___Beginning_April_2006_20250908.csv`

### Description
Monthly data on public assistance cases where recipients have earned income, by social services district. Indicates economic distress and family financial stability, which may correlate with foster care risk.

### Columns and Data Types
| Column | Data Type | Description |
|--------|-----------|-------------|
| Year | int64 | Calendar year |
| Month | string | Month name |
| Month_Code | int64 | Numeric month code |
| District_Code | int64 | Social services district code |
| District | string | Social services district name |
| TANF_Cases_with_Earned_Income | int64 | TANF cases with earned income |
| TANF_Average_Gross_Earned_Income | int64 | Average gross earned income for TANF cases |
| TANF_Average_Net_Earned_Income | int64 | Average net earned income for TANF cases |
| SNA_MOE_Cases_with_Earned_Income | int64 | SNA MOE cases with earned income |
| SNA_MOE_Average_Gross_Earned_Income | int64 | Average gross earned income for SNA MOE cases |
| SNA_MOE_Average_Net_Earned_Income | int64 | Average net earned income for SNA MOE cases |
| SNA_Non_MOE_Cases_with_Earned_Income | int64 | SNA Non-MOE cases with earned income |
| SNA_Non_MOE_Average_Gross_Earned_Income | int64 | Average gross earned income for SNA Non-MOE cases |
| SNA_Non_MOE_Average_Net_Earned_Income | int64 | Average net earned income for SNA Non-MOE cases |

### Key Characteristics
- **Geographic Coverage**: 59 districts
- **Temporal Coverage**: 2006-2025 (19 years)
- **Granularity**: Monthly data by district
- **Aggregation Needed**: Monthly to annual, district to county mapping
- **Primary Keys**: District + Year + Month

---

## 6. Social Services Staff Data
**File**: `Local_Social_Services_District__SSD__Staff_Counts_by_Function__Beginning_State_Fiscal_Year_2004-2005_20250909.csv`

### Description
Annual staffing counts by function for local social services districts. Represents service capacity and resource availability for child welfare services.

### Columns and Data Types (Selected Key Columns)
| Column | Data Type | Description |
|--------|-----------|-------------|
| State_Fiscal_Year_Ending | int64 | State fiscal year ending |
| District_Code | int64 | Social services district code |
| District | string | Social services district name |
| Total_Staffing | int64 | Total staff count |
| Intake_Case_Maintenance | int64 | Staff for intake and case maintenance |
| Services_Program | int64 | Staff for services programs |
| Services_Administration | int64 | Staff for services administration |
| Employment_Programs | int64 | Staff for employment programs |
| Child_Support | int64 | Staff for child support services |

### Key Characteristics
- **Geographic Coverage**: 58 districts
- **Temporal Coverage**: FY2005-2024 (19 years)
- **Granularity**: Annual data by district
- **Aggregation Needed**: District to county mapping
- **Primary Keys**: District + State_Fiscal_Year_Ending

---

## 7. State Taxes and Fees Data
**File**: `State_Taxes_and_Fees_Collected__Beginning_Fiscal_Year_Ending_March_31__1995_20250909.csv`

### Description
Annual state tax and fee collections by category. Provides statewide economic context and fiscal capacity that may impact social services funding and foster care outcomes.

### Columns and Data Types
| Column | Data Type | Description |
|--------|-----------|-------------|
| Fiscal_Year_Ended | int64 | State fiscal year ended |
| Tax_Category | string | Category of tax or fee |
| Tax_or_Fee | string | Specific tax or fee type |
| Amount_Collected | int64 | Amount collected in dollars |
| Tax_or_Fee_Sort_Order | int64 | Sort order for reporting |

### Key Characteristics
- **Geographic Coverage**: Statewide
- **Temporal Coverage**: FY1995-2024 (29 years)
- **Granularity**: Annual data by tax type
- **Aggregation Needed**: Tax categories for analysis
- **Primary Keys**: Fiscal_Year_Ended + Tax_or_Fee

---

## Data Preparation and Quality

### Data Type Corrections Applied
1. **String Standardization**: County/District names converted to string type and standardized
2. **ZIP Code Preservation**: ZIP codes maintained as strings to preserve leading zeros
3. **Phone Number Preservation**: Phone numbers maintained as strings
4. **Numeric Consistency**: All count fields converted to int64, amounts to appropriate numeric types
5. **Missing Value Handling**: Numeric nulls filled with 0, string nulls filled with appropriate defaults

### Power BI Compatibility
- **Column Names**: Cleaned to remove spaces and special characters (underscores used)
- **Data Types**: Optimized for Power BI import
- **File Format**: Exported as Excel (.xlsx) files for easy import
- **Missing Values**: Properly handled to prevent import errors

### Geographic Alignment Challenges
1. **County vs. District**: Some datasets use social services districts instead of counties
2. **District-County Mapping**: Required for Public Assistance and Social Services Staff data
3. **County Name Standardization**: Ensured consistent county naming across datasets

### Temporal Alignment Strategy
1. **Common Period**: 2009-2024 provides best coverage across all datasets
2. **Fiscal vs. Calendar Years**: Some datasets use state fiscal years (April-March)
3. **Aggregation Requirements**: 
   - Child Health Plus: Monthly to annual
   - Crime Data: Agency to county level
   - Child Care: Facility to county level

---

## Recommended Analysis Framework

### Primary Relationships
- **County + Year**: Primary alignment key for most datasets
- **District + Year**: For social services data requiring county mapping

### Key Analysis Questions
1. **Environmental Factors**: How do crime rates correlate with foster care placements?
2. **Service Capacity**: Does social services staffing impact foster care outcomes?
3. **Economic Indicators**: How do public assistance trends relate to foster care?
4. **Health Access**: Does Child Health Plus enrollment correlate with family stability?
5. **Child Care Availability**: Does child care capacity impact foster care prevention?
6. **Economic Context**: How do state fiscal conditions affect county-level outcomes?

### Data Quality Assessment
- **Completeness**: High across all datasets with minimal missing values
- **Consistency**: Geographic and temporal alignment achieved
- **Accuracy**: Data sourced from authoritative NY state agencies
- **Timeliness**: Most recent data available through 2024-2025

---

## Files and Formats

### CSV Files (Original)
Located in `Data/` subdirectories by dataset

### Cleaned CSV Files
Located in `Data/Cleaned/`:
- `foster_care_cleaned.csv`
- `child_health_plus_cleaned.csv`
- `crime_cleaned.csv`
- `child_care_cleaned.csv`
- `public_assistance_cleaned.csv`
- `ssd_staff_cleaned.csv`
- `state_taxes_cleaned.csv`

### Excel Files (Power BI Ready)
Located in `Data/Excel_for_PowerBI/`:
- `foster_care.xlsx`
- `child_health_plus.xlsx`
- `crime.xlsx`
- `child_care.xlsx`
- `public_assistance.xlsx`
- `ssd_staff.xlsx`
- `state_taxes.xlsx`

---

## Power BI Import Instructions

1. **Data Import**: Use Excel workbook connector for each file
2. **Relationships**: Create relationships on County + Year where available
3. **Date Table**: Create calendar table for years 2009-2024
4. **Aggregations**: 
   - Child Health Plus: Sum enrollees by County + Year
   - Crime Data: Sum crimes by County + Year
   - Child Care: Sum capacity by County
5. **District Mapping**: Create lookup table for District to County relationships

---

*This documentation was generated as part of the New York State Foster Care Environmental Factors Analysis project. For questions or clarifications, refer to the analysis notebooks and data processing code.*
