# 📌 Hospital Patient Records Metadata Documentation

## 📖 Project Overview  
This project focuses on documenting hospital patient records by creating a **data dictionary** with metadata. The goal is to ensure structured, standardized, and well-documented data, which is essential for data governance and analytics.

## 📊 Dataset Information  
The dataset consists of hospital patient records, including attributes like patient demographics, medical conditions, procedures, billing details, and outcomes.

## 🛠 Tools & Technologies Used  
- **SQL Server Management Studio (SSMS)** – To manage and query the database  
- **SQL** – To store, retrieve, and manage data dictionary metadata  
- **DBeaver** – (Optional) For database visualization  
- **Excel/Google Sheets** – For metadata documentation  
- **GitHub** – To showcase the project  

## 📂 Data Dictionary Table Structure  
The data dictionary table stores metadata about each variable in the hospital records dataset.

### 🏛 Table Name: `data_dictionary`  
| Column Name        | Data Type   | Description                                     |
|--------------------|------------|-------------------------------------------------|
| `variable_name`    | VARCHAR(100) | Name of the column in the dataset              |
| `data_type`        | VARCHAR(50)  | Data type (INT, FLOAT, VARCHAR, etc.)          |
| `sample_value`     | VARCHAR(100) | Example value from the dataset                 |
| `source`          | VARCHAR(100) | Source of the data (e.g., Billing System)      |
| `allowed_values`   | VARCHAR(255) | Defined range or categories of values          |
| `transformation_rules` | TEXT  | Data processing rules and standardizations     |

## 🔍 SQL Queries  

### 🎯 Creating the Data Dictionary Table  
```sql
CREATE TABLE data_dictionary (
    variable_name VARCHAR(100) PRIMARY KEY,
    data_type VARCHAR(50),
    sample_value VARCHAR(100),
    source VARCHAR(100),
    allowed_values VARCHAR(255),
    transformation_rules TEXT
);

```

### 📥 Populating the Data Dictionary Table
```sql
INSERT INTO data_dictionary (variable_name, data_type, sample_value, source, allowed_values, transformation_rules) 
VALUES 
('Patient_ID', 'INT', '1', 'Hospital Database', 'Unique ID', 'No transformation'),
('Age', 'INT', '45', 'Hospital Database', '0-120', 'No transformation'),
('Gender', 'VARCHAR(10)', 'Female', 'Patient Records', 'Male, Female', 'Standardized categories'),
('Condition', 'VARCHAR(100)', 'Heart Disease', 'Doctor Records', 'Various conditions', 'No transformation'),
('Procedure', 'VARCHAR(100)', 'Angioplasty', 'Surgical Records', 'Various procedures', 'No transformation'),
('Cost', 'FLOAT', '15000', 'Billing System', '>0', 'Convert currency if needed'),
('Length_of_Stay', 'INT', '5', 'Hospital Database', '1-30 days', 'Ensure within 1-30 days'),
('Readmission', 'VARCHAR(10)', 'No', 'Patient Records', 'Yes, No', 'Encode Yes=1, No=0'),
('Outcome', 'VARCHAR(50)', 'Recovered', 'Hospital Database', 'Recovered, Not Recovered', 'Ensure consistency'),
('Satisfaction', 'INT', '4', 'Survey System', '1-5 (Rating)', 'Ensure integer rating');
```
### Data Validation & Confirmation
#### Check Metadata info
```sql
SELECT * FROM data_dictionary 
```
![image](https://github.com/user-attachments/assets/84ac5650-41be-4320-b0e3-71a6861edee9)

### Check for Missing Metadata
```sql
SELECT * FROM data_dictionary 
WHERE data_type IS NULL OR source IS NULL;
```

### Validate Data Types
```sql
SELECT Variable_Name, Data_Type 
FROM data_dictionary 
```
![image](https://github.com/user-attachments/assets/5cdbce68-6cf8-421e-a508-6f7e9562b307)

### Check for Duplicate Entries
```sql
SELECT variable_name, COUNT(*) 
FROM data_dictionary 
GROUP BY variable_name 
HAVING COUNT(*) > 1;
```




