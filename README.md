# Home Mortgage Disclosure Act (HMDA) 2017 Alaska Mortgage Data - Exploratory Data Analysis

## Project Description

This project performs exploratory data analysis on the Home Mortgage Disclosure Act (HMDA) 2017 mortgage dataset for Alaska. The analysis examines borrower, loan, and geographic characteristics for first lien, owner-occupied, 1-4 family homes. The goal is to understand how loan amounts vary with applicant income across different loan purposes (home purchase vs refinance) and loan types (Conventional/FHA/VA).

## What Was Built

A complete data workflow using Python that includes:
- Data loading and ingestion from HMDA CSV dataset
- Data cleaning functions to handle missing values and duplicates
- Exploratory data analysis (EDA) functions for summary statistics
- Data visualizations using Matplotlib and Seaborn
- Statistical analysis of relationships between loan amounts, income, and other variables

## Dataset

**Name:** Home Mortgage Disclosure Act (HMDA) 2017 - Alaska (AK)

**Link:** [CFPB Historic HMDA Data](https://www.consumerfinance.gov/data-research/hmda/historic-data/?geo=ak&records=first-lien-owner-occupied-1-4-family-records&field_descriptions=labels)

**Description:** Mortgages for first lien, owner-occupied, 1-4 family homes with plain language labels and HMDA codes

**Size:** 12,579 rows × 78 columns (cleaned to 12,009 rows × 11 columns)

## How to Run the Project

### Install Dependencies

```bash
pip install -r requirements.txt
```

### Open and Run the Notebook

1. Navigate to the project directory
2. Launch Jupyter Notebook:
   ```bash
   jupyter notebook
   ```
3. Open `data_workflow.ipynb`
4. Run all cells in sequence from top to bottom

Alternatively, use Jupyter Lab:
```bash
jupyter lab
```

### Python Version

This project uses **Python 3.13**

## Project Structure

```
.
├── README.md
├── requirements.txt
├── data_workflow.ipynb              # Main analysis notebook
├── hmda_2017_ak_first-lien-owner-occupied-1-4-family-records_labels.csv  # Dataset
├── web.png                          # HMDA download screenshot
├── 1. PROJECT_OVERVIEW.md           # Project overview
├── 1. PROJECT_INSTRUCTIONS.md       # Detailed instructions
├── 1. DATA_WORKFLOW_RUBRIC.md      # Rubric criteria
└── 1. Rubric.md                    # Assessment rubric
```

## Key Findings

- **Dataset Size:** 12,009 mortgage records after cleaning
- **Correlation:** Moderate positive correlation (0.53) between applicant income and loan amount
- **Loan Purpose:** Home purchase has highest average loan amount (~$284k) and largest income gap
- **Loan Type:** VA-guaranteed loans have highest average amounts (~$306k)
- **Geographic Concentration:** Anchorage Municipality accounts for majority of records (5,522)

## Analysis Components

1. **Data Ingestion:** Load and inspect HMDA CSV dataset
2. **Data Cleaning:**
   - Remove columns with ≥95% missing values (78 → 51 columns)
   - Remove duplicate rows (5 duplicates found)
   - Handle missing values in key fields
   - Type conversion for categorical variables

3. **Exploratory Data Analysis:**
   - Summary statistics for numeric and categorical features
   - Correlation analysis
   - Group-wise comparisons by loan purpose, type, and geography
   
4. **Visualizations:**
   - Distribution histograms for applicant income and loan amounts
   - Pie charts for categorical distributions

## Dependencies

Key libraries used:
- pandas
- numpy
- matplotlib

Complete list available in `requirements.txt`
