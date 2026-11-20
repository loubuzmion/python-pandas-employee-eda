![Employee Data Manipulation](employee-data-manipulation.jpg)
# Employee Data Exploration & Manipulation with Pandas

Exploring, cleaning, transforming, and aggregating an employee dataset using **Pandas** and **NumPy**, built in a Microsoft Fabric notebook with Python.

## Project Overview

The goal is to perform foundational Exploratory Data Analysis (EDA) and data wrangling on an employee dataset—covering missing value checks, summary statistics, feature creation, missing data imputation and removal, conditional filtering, and department-level salary aggregation.

**Dataset:** 20 employees, 6 columns, no initial missing values.

| Feature | Description |
|---|---|
| `employee_id` | Unique identifier for each employee |
| `name` | Name of the employee |
| `age` | Age of the employee |
| `department` | Department where the employee works (HR, Engineering, Marketing, Finance, Sales) |
| `salary` | Annual salary of the employee (renamed to `annual_salary` during transformation) |
| `work_experience` | Number of years of work experience |

## Tools & Libraries

Python 3.15, Pandas, NumPy, Microsoft Fabric notebooks.

## Approach

### 1. Data Loading & Inspection
- Created the dataset from a Python dictionary and loaded it into a Pandas DataFrame (`df`).
- Displayed the full table to verify structure and data types: 20 rows across 6 columns (`employee_id`, `name`, `age`, `department`, `salary`, `work_experience`).

### 2. Data Exploration (EDA)
- **Missing values check** (`isnull()`): Confirmed that all 20 rows and 6 columns were complete with zero initial missing values.
- **Summary statistics** (`describe()`): Computed count, mean, standard deviation, min, quartiles, and max across the numeric columns (`age`, `salary`, `work_experience`).

### 3. Data Transformation
1. **Feature engineering:** Created `years_to_retirement` by subtracting `age` from a retirement age of 65 (`65 - df['age']`).
2. **Column renaming:** Renamed `salary` to `annual_salary` using `.rename()`.
3. **Sorting:** Sorted employees by `work_experience` in descending order (`df_sorted`), placing the most experienced staff at the top.

### 4. Handling Missing Data
1. **Mean imputation:** Introduced `np.nan` into `annual_salary` for rows at index `1` (Jane) and `4` (Charlie), calculated the mean of the remaining salaries (**$79,000**), and filled the missing values using `.fillna()`.
2. **Row deletion:** Set `annual_salary` to `np.nan` for employees under age 25 (`employee_id` 1: John, age 22; `employee_id` 12: Jack, age 24) and removed those records using `.dropna(subset=['annual_salary'])`, leaving 18 active rows.

### 5. Data Filtering & Selection
- **Conditional filtering:** Filtered `df` for employees older than 30 (`df['age'] > 30`) and sorted ascending by `age` (13 employees, ranging from age 32 to 65).
- **Column subsetting:** Selected only `name`, `age`, and `annual_salary` (`df_selected`) for a focused view of employee compensation by age.

### 6. Data Aggregation
- Grouped the cleaned dataset (18 employees) by `department` and calculated the mean `annual_salary` for each department (`groupby('department')['annual_salary'].mean()`).

## Key Findings

### Summary Statistics (Initial 20 Employees)

| Metric | Age | Salary ($) | Work Experience (Years) |
|---|---|---|---|
| **Mean** | 37.60 | $78,100.00 | 7.05 |
| **Std Dev** | 11.63 | $19,150.10 | 5.41 |
| **Min** | 22.00 | $48,000.00 | 1.00 |
| **Median (50%)** | 36.00 | $77,500.00 | 5.50 |
| **Max** | 65.00 | $120,000.00 | 20.00 |

### Average Annual Salary by Department (Post-Cleaning, n = 18)

| Department | Average Annual Salary |
|---|---|
| **Finance** | **$91,250.00** |
| **Engineering** | $82,000.00 |
| **Sales** | $81,750.00 |
| **Marketing** | $80,000.00 |
| **HR** | $66,666.67 |

### Insights from the Data
- **Experience and age strongly align with compensation:** Grace (Finance, age 65, 20 years experience) is at retirement age (`0` years remaining) and earns the highest salary ($120,000), followed by Frank (Marketing, age 60, 18 years experience, $110,000).
- **Departmental pay gaps:** Finance leads all departments with an average salary of $91,250, while HR has the lowest average at $66,666.67 (even after John's $50,000 entry-level record was dropped).
- **Impact of missing-data strategies:** Imputing missing salaries with the dataset mean ($79,000) preserved sample size but raised Jane's (Engineering) recorded salary from $60,000 to $79,000, which subsequently lifted Engineering's post-cleaning departmental average.

## Limitations
- **Small synthetic dataset:** With only 20 records created in-memory, statistical summaries and department averages are sensitive to individual outliers or single dropped rows.
- **Sequential in-place mutations:** Applying mean imputation prior to dropping rows under age 25 altered Jane's original salary ($60,000 → $79,000) in the downstream aggregation step.
- **No visualisations:** All exploration and summaries are tabular; adding distribution plots or department boxplots would make patterns easier to spot.

## Possible Improvements
- **Isolate data cleaning experiments:** Copy the DataFrame (`df.copy()`) before testing different missing-value strategies (mean imputation vs. dropping rows) so downstream aggregations reflect unmodified figures.
- **Group-wise imputation:** Impute missing salaries using department-level or experience-band medians rather than the overall company mean to avoid distorting junior vs. senior pay.
- **Add visual EDA:** Include Matplotlib/Seaborn bar charts for average salary by department and scatter plots for `work_experience` vs. `annual_salary`.
- **Load from external storage:** Parameterise data ingestion from a CSV file or Azure Blob Storage rather than hard-coding the dictionary inside the notebook.

## Conclusion

This project demonstrates a complete end-to-end Pandas data wrangling workflow—from inspecting raw records and engineering new features to comparing missing-data handling strategies and aggregating departmental salaries[cite: 2]. Among the cleaned employee cohort, **Finance** commands the highest average compensation ($91,250) while **HR** trails ($66,667), illustrating how both tenure and missing-value treatment directly shape summary analytics.
