# Home Mortgage Disclosure Act (HMDA) 2017 Alaska Mortgage Data - Exploratory Data Analysis

**GitHub Repository:** [https://github.com/gour6380/ai-programming-foundations-project](https://github.com/gour6380/ai-programming-foundations-project)

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

## Bias & Data Quality Considerations

### Potential Sources of Bias

Poor data cleaning decisions can introduce or amplify bias in several ways:

1. **Missing Data Deletion**
   - **Issue:** Dropped 526 rows (4.2%) with missing `applicant_income_000s` data
   - **Bias Risk:** If income missingness correlates with loan denial, applicant demographics, or property location, removing these records creates selection bias that underrepresents certain borrower groups
   - **Mitigation Applied:** Analyzed missing data patterns before deletion; documented the count and percentage removed; acknowledged limitation in summary

2. **Geographic Concentration Bias**
   - **Issue:** 46% of records (5,522) come from Anchorage Municipality alone
   - **Bias Risk:** Urban lending patterns in Anchorage may not represent rural Alaska; models trained on this data would be biased toward urban borrower characteristics
   - **Mitigation Applied:** Identified and reported geographic concentration explicitly; performed separate analyses by county and MSA/MD status

3. **"Information Not Provided" Categories**
   - **Issue:** High rates of missing demographic data where applicants chose not to provide race, ethnicity, or sex information
   - **Bias Risk:** If refusal to provide demographic information correlates with loan outcomes or borrower characteristics, analyses excluding these records mask important patterns and create systematic bias
   - **Mitigation Applied:** Retained and tracked "Information not provided" as a distinct category rather than treating as missing; reported counts for these categories

4. **Outlier Impact on Summary Statistics**
   - **Issue:** Extreme values in income and loan amounts (e.g., multimillion-dollar loans, very high incomes)
   - **Bias Risk:** Using mean instead of median inflates typical borrower profile; outliers disproportionately influence correlation calculations and group comparisons
   - **Mitigation Applied:** Reported both mean and median values; used visualizations (histograms) to show full distributions; identified right-skew explicitly

5. **Threshold-Based Column Removal**
   - **Issue:** Automatically dropped all columns with ≥95% missing values (27 columns removed)
   - **Bias Risk:** Sparse but meaningful variables (e.g., rarely-used loan features) may contain information about underserved populations or special loan programs
   - **Mitigation Applied:** Used conservative 95% threshold; manually reviewed list of dropped columns; documented which fields were removed

### Additional Data Quality Limitations

- **Originated Loans Only:** Dataset excludes denied applications, preventing analysis of approval patterns and potential lending discrimination
- **Selection Bias:** Only captures applicants who reached financial institutions, missing those discouraged from applying
- **Temporal Snapshot:** Single year (2017) prevents trend analysis or detection of changing patterns over time
- **MSA/MD Structural Missingness:** Missing values in `msamd_name` represent non-metropolitan areas (meaningful missingness), not data quality issues—treated appropriately by creating "Non-MSA/MD" category

## Dependencies

Key libraries used:
- pandas
- numpy
- matplotlib

Complete list available in `requirements.txt`

## Future Work & ML Integration

### ML Workflow Adaptations

To extend this workflow for machine learning model training, the following modifications would be needed:

1. **Feature Engineering**: Create additional features from existing variables such as debt-to-income ratio, loan-to-value ratio, and geographic indicators
2. **Target Variable**: Define a prediction target (e.g., loan approval, default risk, or loan amount prediction)
3. **Train-Test Split**: Partition the cleaned dataset into training, validation, and test sets using stratified sampling to maintain class distributions
4. **Feature Scaling**: Normalize or standardize numeric features (income, loan amounts) for algorithms sensitive to feature magnitude
5. **Categorical Encoding**: Convert categorical variables (loan type, county) to numeric representations using one-hot encoding or embeddings

### Neural Network Preparation

Additional preprocessing steps for neural network models:

1. **Input Normalization**: Scale all numeric features to [0, 1] or standardize to mean=0, std=1 for faster convergence
2. **Embedding Preparation**: Create embedding layers for high-cardinality categorical features (county names, MSA/MD codes)
3. **Missing Value Strategy**: Replace remaining missing values with learned embeddings or mean/median imputation rather than deletion
4. **Sequence Padding**: If incorporating temporal data (e.g., application dates), ensure consistent sequence lengths
5. **Class Balancing**: Address class imbalance through oversampling, undersampling, or class weights if predicting binary outcomes

### Agentic Automation Potential

This workflow could be enhanced with agentic AI automation in several areas:

1. **Automated Data Profiling**: Deploy AI agents to automatically detect data quality issues, outliers, and distribution shifts across new datasets
2. **Adaptive Cleaning**: Use LLM-based agents to suggest and apply context-appropriate cleaning strategies based on dataset characteristics
3. **Intelligent Feature Engineering**: Leverage agentic systems to propose and test novel feature combinations based on domain knowledge
4. **Automated Visualization Selection**: Deploy agents to select the most informative visualization types based on variable distributions and relationships
5. **Bias Detection**: Implement AI agents to continuously monitor for potential bias in data collection, processing, and model outputs
6. **Report Generation**: Automate the creation of analysis summaries and insights using LLM agents that interpret statistical results and generate human-readable explanations
7. **Pipeline Orchestration**: Use multi-agent systems to coordinate data ingestion, cleaning, analysis, and reporting workflows with minimal human intervention
