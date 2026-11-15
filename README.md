# python-pandas-employee-eda
# Python & Pandas: Employee Exploratory Data Analysis (EDA)

A practical data wrangling and Exploratory Data Analysis (EDA) project built using Python and the Pandas library. This notebook walks through foundational data manipulation techniques on a simulated HR employee dataset.

---

## Core Skills & Techniques Covered
This project demonstrates core data science and data engineering operations in Python:
* **DataFrame Initialization & Inspection:** Creating structured DataFrames from dictionaries and inspecting data summaries using `.describe()` and `.isnull()`[cite: 17].
* **Data Transformation:** Engineering new features (calculating `years_to_retirement` from age), renaming columns (`salary` ➡️ `annual_salary`), and multi-level sorting[cite: 17].
* **Missing Data Management:** Dynamically introducing missing values (`np.nan`), handling imputation via column means, and utilizing conditional row dropping (`dropna`)[cite: 17].
* **Advanced Filtering & Selection:** Applying conditional boolean masks (e.g., filtering employees over age 30) and subsetting specific columns[cite: 17].
* **Group-Based Aggregation:** Using `.groupby()` combined with `.mean()` and `.round()` to calculate and rank average departmental salaries[cite: 17].

---

## Dataset Overview
The dataset models an organization of 20 employees across various departments (HR, Engineering, Marketing, Finance, and Sales)[cite: 17]:
* `employee_id`: Unique identifier (1–20)[cite: 17]
* `name`: Employee first name[cite: 17]
* `age`: Employee age (ranging from 22 to 65)[cite: 17]
* `department`: Organizational department[cite: 17]
* `annual_salary`: Annual compensation[cite: 17]
* `work_experience`: Years of professional experience[cite: 17]

---

## Key Analytical Findings
* **Departmental Salary Rankings:** Grouping and averaging annual salaries revealed that **Finance** leads the organization with the highest average salary ($91,250), followed by Engineering ($82,000), Sales ($81,750), Marketing ($80,000), and HR ($66,667)[cite: 17].
* **Workforce Age & Experience Distribution:** The average employee age across the dataset is 37.6 years with an average tenure/experience of 7.05 years[cite: 17].

---

## How to View / Run
1. Clone the repository or download the `.ipynb` file.
2. Open the notebook in **Jupyter Notebook**, **JupyterLab**, or directly view it natively rendered in your **GitHub** browser interface[cite: 17].
