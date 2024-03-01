# Critical-Care-Nursing
This dataset is a breakdown of the nursing profession and the advanced critical care certifications nurses can get by state.
Also included are total RNs, Hospitals, and staffed ICU beds.

## Project Overview
This project explores the nursing profession and advanced critical care certifications across states in the United States. The dataset includes certifications like CCRN, CMC, CSC, CCRNs (pediatric and neonatal), and PCCN. Alongside, it provides metrics on total RNs, hospitals, and staffed ICU beds by state. Through this analysis, we aim to uncover patterns and trends in critical care certifications and healthcare infrastructure, informing strategic decisions on resource allocation and training programs for nurses.

### Data Sources 

Critical Care Nursing : Kaggle 

### Tools

- Excel - Data Cleaning and Analysis
- SQL server - Data analysis

### Data Cleaning/Preparation

  In the initial data preparation phase, The following tasks were performed;
  1. Data loading and inspection.
  2. Handling missing values.
  3. Data cleaning and Formating.

 ### Exploratory data analysis

EDA involved exploring Dataset to answer key questions such as; 
1. What is the total number of RN per state?
2. What is the number of nursing schools by state?
3. What is the percentage of total RNs with each type of critical care certification by state?
4. What is the ratio of Nursing schools in relation to RNs?
5. What is the ratio of Nursing schools relative to Hospitals?


### Data Analysis 
```sql
SELECT *
FROM criticalnursingeda

-------------Calculate Total RN per state
SELECT State, Total_rn
FROM criticalnursingeda
ORDER BY State DESC

-------calculate highest numb of nursing school 
SELECT State, MAX(Nursing_schools) 
FROM criticalnursingeda
GROUP BY State

-----Percentage numb of CCRN per State 
SELECT State, Total_rn, CCRN, (CCRN/Total_rn)*100 AS percentCCRN
FROM criticalnursingeda
ORDER BY 1,2

ALTER TABLE criticalnursingeda
ADD COLUMN PercentCCRN VARCHAR(255)

UPDATE criticalnursingeda
SET PercentCCRN = CONCAT(ROUND((CCRN/Total_rn)*100,2), '%')
WHERE Total_rn;

---------- Calculate the total number of RNs by state
SELECT State, SUM(Total_rn) AS Total_RNs
FROM criticalnursingeda
GROUP BY State;

--------- Calculate the percentage of total RNs with each type of critical care certification by state
SELECT State,
(CCRN/Total_rn) *100 AS Percentageccrn,
(CMC/Total_rn) *100 AS Percentagecmc,
(CSC/Total_rn) *100 AS Percentagecsc,
(CCRN_peds/Total_rn) *100 AS Percentageccrnpeds,
(CCRN_neo/Total_rn) *100 AS Percentageccrnneo,
(PCCN/Total_rn) *100 AS Percentagepccn
FROM criticalnursingeda

------- Nursing schools relative to total RNs
SELECT State, (Nursing_schools / Total_rn) AS School_Ratio
FROM criticalnursingeda
ORDER BY School_Ratio DESC;

------ Nursing schools relative to hospitals
SELECT State, (Nursing_schools / Total_Hospitals) AS School_Ratio
FROM criticalnursingeda
ORDER BY School_Ratio DESC;

---------- hospital to RN ratio 
SELECT State, (Total_Hospitals / Total_rn) AS Hospital_RN_ratio
FROM criticalnursingeda
ORDER BY Hospital_RN_ratio DESC;
```

### Results/Finding

1. California boasts the highest count of registered nurses.
2. New Jersey exhibits the highest proportion of CCRN certifications.
3. North Dakota displays the most favorable ratio of nursing schools to hospitals.
4. Oklahoma demonstrates the highest hospital-to-RN ratio among states.

### Recommendations 

Based on the analysis, The following actions can be recommended:
1. Encourage other states to emulate California's approach to nursing staffing.
2. Investigate the factors contributing to New Jersey's high CCRN certification rate for potential replication in other regions.
3. Assess the effectiveness of nursing school distribution and consider adjustments to achieve a balanced ratio similar to North Dakota's.
4. Evaluate the reasons behind Oklahoma's high hospital-to-RN ratio and explore strategies to optimize staffing levels for better patient care.
