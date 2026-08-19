# Healthcare Data Cleaning & Preprocessing

## 📌 Project Overview

This project demonstrates a data cleaning and preprocessing workflow for a **messy healthcare dataset** using Python.

The raw dataset contains common real-world data quality issues, including missing values, duplicate records, inconsistent categorical labels, mixed date formats, invalid numerical values, inconsistent medication dosages, and unstructured clinical measurements.

The goal of this project was to transform these data into a cleaner and more structured dataset that can be used for further statistical analysis or visualization.

---

## 🛠️ Tools & Libraries

* **Python**
* **Pandas** — data manipulation and preprocessing
* **NumPy** — numerical operations and missing-value handling
* **Matplotlib** — data visualization
* **Seaborn** — distribution visualization
* **Regular Expressions (re)** — parsing inconsistent text values
* **Datetime** — date parsing and standardization
* **Google Colab** — development environment

---

## 🔍 Data Quality Assessment

Before cleaning the dataset, I performed an initial assessment to identify potential data quality problems.

This included:

* Inspecting dataset structure and data types
* Identifying missing values by column
* Generating descriptive statistics for numerical variables
* Examining unique values in categorical and clinical variables
* Detecting duplicate records
* Identifying inconsistent formats and implausible values

---

## 🧹 Data Cleaning Workflow

### 1. Missing Values

Missing categorical values were standardized as `Unknown` to distinguish unavailable information from valid observations.

The dataset was then rechecked to identify remaining missing values requiring variable-specific handling.

---

### 2. Duplicate Records

Exact duplicate rows were identified and removed from the dataset.

---

### 3. Date Standardization

Several date variables contained different formats.

The following variables were standardized:

* Date of Birth
* Admission Date
* Discharge Date
* Treatment Date

The cleaning function recognizes formats including:

```text
YYYY-MM-DD
MM/DD/YYYY
DD.MM.YYYY
MM.DD.YYYY
```

Valid dates were converted to:

```text
YYYY-MM-DD
```

Invalid or unrecognized dates were classified as `Unknown`.

---

### 4. Gender Standardization

Different representations of gender were mapped into standardized categories.

Examples include:

```text
M, male, boy, mle → Male
F, female, girl, fem → Female
```

The final categories were:

* Male
* Female
* Other
* Unknown

---

### 5. Medication Name Standardization

Misspelled and alternative medication names were standardized.

Examples:

```text
Asprin → Aspirin
Advil → Ibuprofen
```

A new standardized medication variable was created while retaining the original information.

---

### 6. Medication Dosage Parsing

Medication dosage information was converted from semi-structured text into separate analytical variables.

The cleaning function extracts:

* `Dose_Value`
* `Dose_Unit`
* `Frequency`

It also standardizes different measurement units.

For example:

```text
0.5 g → 500 mg
500 mg → 500 mg
```

Insulin doses are handled separately using **units** rather than milligrams.

Medication frequencies such as the following are also extracted when available:

```text
daily
weekly
BID
TID
QID
QOD
PRN
```

---

### 7. Hospital Name Standardization

Different spellings and abbreviations referring to the same hospital were consolidated.

For example:

```text
Cty Hospital → City Hospital
City Hosp → City Hospital
```

---

### 8. Diagnosis Classification

Diagnosis codes were used to generate standardized primary diagnosis categories based on **ICD-10 D-code blocks**.

The resulting categories include:

* In situ neoplasms
* Benign neoplasms
* Neoplasms of uncertain or unspecified behaviour
* Nutritional anemias
* Hemolytic anemias
* Aplastic and other anemias
* Coagulation defects and purpura
* Other diseases of blood and blood-forming organs
* Immune mechanism disorders

Codes outside the ICD-10 D chapter were separately classified.

---

### 9. Insurance Type Standardization

Inconsistent insurance labels and spelling errors were standardized.

For example:

```text
Self-pay → Private
Privte → Private
```

---

### 10. Age Cleaning

Age values were converted to numeric values and checked for implausible observations.

The cleaning process:

* Identifies impossible ages below 0 or above 120
* Corrects selected apparent missing-decimal values
* Converts unresolved invalid values to `Unknown`

The cleaned age distribution was then visualized using a histogram and kernel density estimate.

---

### 11. Blood Pressure Parsing

Blood pressure was transformed from an unstructured text field into separate variables:

```text
Systolic_BP
Diastolic_BP
BP_High_Flag
```

Values expressed as:

```text
120/80
```

were separated into systolic and diastolic measurements.

The cleaning algorithm also:

* Detects and corrects reversed systolic/diastolic values
* Removes physiologically implausible measurements
* Recognizes text labels such as `high` and `hypertensive`
* Flags blood pressure as high when systolic BP ≥ 140 mmHg or diastolic BP ≥ 90 mmHg

---

### 12. Billing Amount Cleaning

Billing values were converted from formatted text into numerical values.

The preprocessing handles:

* Currency symbols
* Thousands separators
* Missing-value labels
* Parentheses used to represent negative values

A cleaned variable, `BillingAmount_clean`, was created.

The resulting distribution was visualized after parsing.

---

### 13. Length of Stay

Length of stay was standardized into a new variable:

```text
LOS_days
```

Whenever valid admission and discharge dates were available, length of stay was calculated directly:

```text
Discharge Date - Admission Date
```

If valid dates were unavailable, the original length-of-stay text was parsed as a fallback.

Negative or invalid lengths of stay were treated as unknown.

---

## 📊 Output

After completing the cleaning workflow, the final dataset was exported as an Excel file containing the cleaned and derived variables.

Examples of newly created variables include:

```text
Gender_clean
Medication_clean
Dose_Value
Dose_Unit
Frequency
Hospital_clean
Insurance_clean
Systolic_BP
Diastolic_BP
BP_High_Flag
BillingAmount_clean
LOS_days
```

The cleaned dataset can then be used for further:

* Exploratory data analysis
* Statistical analysis
* Epidemiological analysis
* Data visualization
* Predictive modeling

---

## 📁 Repository Structure

```text
Data_Cleaning/
│
├── Cleaning_Project.ipynb
├── README.md
└── data/
    └── README.md
```

> **Note:** The dataset used for this project should only be included in the repository if its license and privacy conditions permit public redistribution.

---

## 💡 Skills Demonstrated

This project demonstrates practical experience with:

* Healthcare data preprocessing
* Data quality assessment
* Missing data handling
* Duplicate detection
* Categorical variable standardization
* Regular expressions
* Date parsing
* Clinical data transformation
* ICD-10-based classification
* Medication dosage parsing
* Outlier and plausibility checking
* Feature engineering
* Data visualization
* Reproducible data cleaning workflows

---

## 🚀 Future Improvements

Potential extensions to this project include:

* Adding automated data-quality validation
* Creating a before-and-after data quality report
* Separating reusable cleaning functions into Python modules
* Adding unit tests for cleaning functions
* Expanding exploratory data analysis after cleaning
* Creating a reproducible cleaning pipeline for new datasets

---

## 👤 Author

**Wahyunilamma**

Medical and biomedical researcher interested in epidemiology, biostatistics, healthcare data analysis, and reproducible research.
