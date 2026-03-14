## Project Overview
This project analyzes a healthcare dataset containing hospital admissions, patient demographics, medical conditions, test results, and billing information. 
The objective of the analysis is to uncover patterns in hospital admissions, identify factors influencing patient length of stay, and explore cost drivers in healthcare services.

The analysis was performed using Python for data cleaning and exploratory analysis and MySQL for data analysis.

## Tools and Technologies
- **Python** (Jupyter Notebook)
- **Pandas**
- **Matplotlib**
- **SQL**

## Project Structure
- **Datasets/**: Contains the datasets
  - clean_healthcare_data.csv
  - raw_healthcare_dataset.csv
- **Notebooks/**: Contains the jupyter notebooks
  - notebook_1_data_cleaning.ipynb
  - notebook_2_eda.ipynb
  - notebook_3_insights.ipynb
- **Charts/**: Contains the charts of the analysis
  - Admission Type Count.png
  - Average Billing Amount by Admission Type.png
  - Average Billing Amount by Insurance Provider.png
  - Average Billing Amount by Medical Condition.png
  - Average Length of Stay by Admission Type.png
  - Average Length of Stay by Test Result.png
  - Blood Type Distribution of Patients.png
  - Distribution of Age.png
  - Distribution of Test Results.png
  - Gender Distribution of Patients.png
  - Hospital Admissions Over Time.png
  - Top 10 Conditions with Longest Hospital Stay.png
  - Top 10 Medical Conditions.png
- **sql/**: Contains the sql file
  - healthcare_queries.sql

## Data Cleaning (Notebook 1)

### Import Required Libraries
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

### Load file (File location omitted for security resaons)
```python
df = pd.read_csv("C:/___/____/____/Hospital DA/Datasets/raw_healthcare_dataset.csv")
```

### Describing the basic stats of the data
```python
df.describe()
```

### Total number of rows and columns
```python
df.shape
```

### Check for missing values 
```python
df.isna().sum()
```

### To know the data types in the dataset
```python
df.dtypes
```

### Change the data types of dates into datetime
```python
df["Discharge Date"] = pd.to_datetime(df["Discharge Date"])
df["Date of Admission"] = pd.to_datetime(df["Date of Admission"])
```

### Standardized column names to snake_case
```python
df.columns = df.columns = (
    df.columns
        .str.strip()
        .str.lower()
        .str.replace(" ", "_")
        .str.replace("/", "_")
        .str.replace("-", "_")
)
```

### Save the cleaned data 
```python
df.to_csv('../Datasets/clean_healthcare_data.csv', index=False)
```

## EDA (Notebook 2)

### Import Librariess
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

### Load File
```python
df = pd.read_csv("../Datasets/clean_healthcare_data.csv")
```

### Distribution of Age
```python
plt.hist(df["age"])
plt.xlabel("Age")
plt.ylabel("Frequency")
plt.title("Ditribution of Age")
plt.show()
```

### Gender Distribution of Patients
```python
gender_counts = df['gender'].value_counts()

gender_counts.plot(kind='bar')

plt.xlabel("Gender")
plt.ylabel("Frequency")
plt.title("Gender Ditribution of Patients")
plt.show()
```

### Blood Type Distribution of Patients
```python
blood_type_counts = df['blood_type'].value_counts()

blood_type_counts.plot(kind='bar')

plt.xlabel("Blood Type")
plt.ylabel("Frequency")
plt.title("Blood Type Ditribution of Patients")
plt.show()
```

### Top 10 Medical Conditions
```python
condition_counts = df['medical_condition'].value_counts()

top_conditions = condition_counts.head(10)

top_conditions.plot(kind='bar')

plt.title("Top 10 Medical Conditions")
plt.xlabel("Medical Condition")
plt.ylabel("Number of Patients")
plt.xticks(rotation=45)

plt.show()
```

### Admission Type Count
```python
admission_type_counts = df['admission_type'].value_counts()

admission_type_counts.plot(kind='bar')

plt.title("Admission Type Count")
plt.xlabel("Admission Type")
plt.ylabel("Number of Patients")

plt.show()
```

### Hospital Admissions over Time
```python
df['date_of_admission'] = pd.to_datetime(df['date_of_admission'])

df['admission_month'] = df['date_of_admission'].dt.to_period('M')

monthly_admissions = df.groupby('admission_month').size()
monthly_admissions.index = monthly_admissions.index.to_timestamp()

plt.figure(figsize=(10,5))

plt.plot(monthly_admissions)

plt.title("Hospital Admissions Over Time")
plt.xlabel("Time of Admission")
plt.ylabel("Number of Admissions")

plt.xticks(rotation=45)

plt.tight_layout()
plt.show()
```

### Top 10 Conditions with the Longest Hospital Stay  
```python
top_conditions = df.groupby('medical_condition')['length_of_stay'].mean().sort_values(ascending=False).head(10)

top_conditions.sort_values().plot(kind='barh', figsize=(10,6))

plt.title("Top 10 Conditions with Longest Hospital Stay")
plt.xlabel("Average Length of Stay (Days)")
plt.ylabel("Medical Condition")

plt.tight_layout()
plt.show()
```

### Average Length of Stay by Admission Type
```python
stay_by_admission = df.groupby('admission_type')['length_of_stay'].mean()

stay_by_admission.plot(kind='bar', figsize=(8,5))

plt.title("Average Length of Stay by Admission Type")
plt.xlabel("Admission Type")
plt.ylabel("Average Length of Stay (Days)")

plt.xticks(rotation=0)

plt.tight_layout()
plt.show()
```

### Average Billing Amount by Medical Condition
```python
avg_billing_mc = df.groupby('medical_condition')['billing_amount'].mean().sort_values(ascending=False)

avg_billing_mc.sort_values().plot(kind='barh', figsize=(10,6))

plt.title("Average Billing Amount by Medical Condition")
plt.xlabel("Average Billing Amount")
plt.ylabel("Medical Condition")

plt.tight_layout()
plt.show()
```

### Average Billing Amount by Admission Type
```python
avg_billing_at = df.groupby('admission_type')['billing_amount'].mean().sort_values(ascending=False)

avg_billing_at.sort_values().plot(kind='barh', figsize=(10,6))

plt.title("Average Billing Amount by Admission Type")
plt.xlabel("Average Billing Amount")
plt.ylabel("Admission Type")

plt.tight_layout()
plt.show()
```

### Average Billing Amount by Insurance Provider
```python
avg_billing_ip = df.groupby('insurance_provider')['billing_amount'].mean().sort_values(ascending=False)

avg_billing_ip.sort_values().plot(kind='barh', figsize=(10,6))

plt.title("Average Billing Amount by Insurance Provider")
plt.xlabel("Average Billing Amount")
plt.ylabel("Insurance Provider")

plt.tight_layout()
plt.show()
```

### Distribution of Test Results
```python
test_counts = df['test_results'].value_counts()

test_counts.plot(kind='bar', figsize=(8,5))

plt.title("Distribution of Test Results")
plt.xlabel("Test Result")
plt.ylabel("Number of Patients")

plt.xticks(rotation=0)

plt.tight_layout()
plt.show()
```

### Average Length of Stay by Test Result
```python
avg_stay = df.groupby('test_results')['length_of_stay'].mean()

avg_stay.plot(kind='bar', figsize=(8,5))

plt.title("Average Length of Stay by Test Result")
plt.xlabel("Test Result")
plt.ylabel("Average Length of Stay (Days)")

plt.xticks(rotation=0)

plt.show()
```

## Sql Data Analysis

### Create Table and import data
```sql
DROP TABLE IF EXISTS healthcare_data;
CREATE TABLE healthcare_data (
    name VARCHAR(100),
    age INT,
    gender VARCHAR(10),
    blood_type VARCHAR(5),
    medical_condition VARCHAR(100),
    date_of_admission DATE,
    doctor VARCHAR(100),
    hospital VARCHAR(150),
    insurance_provider VARCHAR(100),
    billing_amount DECIMAL(10,2),
    room_number INT,
    admission_type VARCHAR(20),
    discharge_date DATE,
    medication VARCHAR(100),
    test_results VARCHAR(50),
    length_of_stay INT
);


LOAD DATA LOCAL INFILE 'Hospital DA/Datasets/clean_healthcare_data.csv'
INTO TABLE healthcare_data
FIELDS TERMINATED BY ','
ENCLOSED BY '"'
LINES TERMINATED BY '\n'
IGNORE 1 ROWS;
```

### Admissions per year
```sql
SELECT
	YEAR(date_of_admission) AS admission_year,
    COUNT(*) AS total_admissions
FROM healthcare_data
GROUP BY admission_year
ORDER BY admission_year;
```

### Top 5 costly conditions
```sql
SELECT
	medical_condition,
    AVG(billing_amount) AS avg_billing_amount
FROM healthcare_data
GROUP BY medical_condition
ORDER BY 2 DESC;
```

### Avg billing by insurance provider
```sql
SELECT
	insurance_provider,
    AVG(billing_amount) AS avg_billing_amount
FROM healthcare_data
GROUP BY insurance_provider
ORDER BY 2 DESC; 
```

### Length of stay by admission type
```sql
SELECT
	admission_type,
    AVG(length_of_stay) AS avg_length_of_stay
FROM healthcare_data
GROUP BY admission_type
ORDER BY 2 DESC;
```

### Average Billing Amount for different Age Groups
```sql
SELECT 
    CASE 
        WHEN age < 18 THEN 'Pediatric'
        WHEN age >= 18 AND age < 60 THEN 'Adult'
        WHEN age >= 60 THEN 'Elderly'
        ELSE 'Unknown'
    END AS age_group,
    AVG(billing_amount) AS avg_cost
FROM 
    healthcare_data
GROUP BY 
    CASE 
        WHEN age < 18 THEN 'Pediatric'
        WHEN age >= 18 AND age < 60 THEN 'Adult'
        WHEN age >= 60 THEN 'Elderly'
        ELSE 'Unknown'
    END;
```

