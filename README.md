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

### Key Insights from Patient Records (SQL Analysis)
#### Most Common Medical Conditions
```sql
SELECT Condition, COUNT(*) AS Condition_Count 
FROM patient_records
GROUP BY Condition
ORDER BY Condition_Count DESC;
```
![image](https://github.com/user-attachments/assets/60e9e85d-ad5f-4b04-a186-1e5003fbf999)

#### Average Cost per Procedure
```sql
SELECT [Procedure], AVG(Cost) AS Avg_Cost 
FROM patient_records
GROUP BY [Procedure]
ORDER BY Avg_Cost DESC;
```
![image](https://github.com/user-attachments/assets/3e60ad13-f5fb-4000-ae5e-debfab599d4e)

#### Readmission Rates per Condition
```sql
SELECT Condition, 
       COUNT(CASE WHEN Readmission = 1 THEN 1 END) * 100.0 / COUNT(*) AS Readmission_Rate
FROM patient_records
GROUP BY Condition
ORDER BY Readmission_Rate DESC;
```
![image](https://github.com/user-attachments/assets/bdee5374-7d61-4a9f-92b8-9cf14fb4a2be)

#### Average Length of Stay per Condition
```sql
SELECT Condition, AVG(Length_of_Stay) AS Avg_Stay_Days 
FROM patient_records
GROUP BY Condition
ORDER BY Avg_Stay_Days DESC;
```
![image](https://github.com/user-attachments/assets/1bf15a4a-e3fd-46f1-bc98-89dc03a61967)

#### Patient Satisfaction Distribution
```sql
SELECT Satisfaction, COUNT(*) AS Patient_Count 
FROM patient_records
GROUP BY Satisfaction
ORDER BY Satisfaction DESC;
```
![image](https://github.com/user-attachments/assets/760604e1-5290-4503-a020-a6cf7a71c379)

#### Readmission Rate vs. Cost
Do expensive treatments result in lower readmission rates?
```sql
SELECT 
    CASE 
        WHEN Cost < 5000 THEN 'Low Cost'
        WHEN Cost BETWEEN 5000 AND 15000 THEN 'Medium Cost'
        ELSE 'High Cost'
    END AS Cost_Category,
    COUNT(CASE WHEN Readmission = 1 THEN 1 END) * 100.0 / COUNT(*) AS Readmission_Rate
FROM patient_records
GROUP BY 
    CASE 
        WHEN Cost < 5000 THEN 'Low Cost'
        WHEN Cost BETWEEN 5000 AND 15000 THEN 'Medium Cost'
        ELSE 'High Cost'
    END
ORDER BY Readmission_Rate DESC;
```
![image](https://github.com/user-attachments/assets/78ec5511-750d-4d84-a2d4-46eacd217a6f)







