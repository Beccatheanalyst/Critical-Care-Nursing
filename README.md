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
- Tableau - Creating reports

### Data Cleaning/Preparation

  In the initial data preparation phase, The following tasks were performed;
  1. Data loading and inspection.
  2. Handling missing values.
  3. Data cleaning and Formating.

 ### Exploratory data analysis

EDA involved exploring Dataset to answer key questions such as; 
1. What is the total number of RN per state?
2. What is the number of nursing schools by state?
3. What is the percentage of CCRN by state?
4. What is the percentage of total RNs with each type of critical care certification by state?
5. What is the ratio of hospitals to Nursing schools?
6. What is the ratio of Nursing schools in relation to RNs?
7. What is the ratio of Nursing schools relative to Hospitals?
8. What is the ratio of Hospitals to RNs?  

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

------------ The ratio of total hospitals to nursing school
SELECT State, (Total_Hospitals/Nursing_schools) AS Ratio_hospital_to_nursing
FROM criticalnursingeda
ORDER BY 1,2

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

1. The "Old" category experiences higher quality of sleep.
2. The "Overweight" category exhibits the highest physical activity level.
3. The "Adult" category demonstrates the highest stress level.
4. Engineers show the lowest stress level.
5. Nurses record the highest number of daily steps.

### Recommendations 

Based on the analysis, The following actions can be recommended:
1. Individuals with sleep disorders should consider consulting neurologists, pulmonologists, or psychiatrists for specialized care.
2. Efforts to improve quality of s
