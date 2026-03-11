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


```python

```


```python

```


```python

```
