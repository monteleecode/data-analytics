# 🧾 Data Processing & Preparation Steps

## **Step 0 — Understand the Data**

- Loaded the dataset and created a backup copy.
- Reviewed column relationships and formulas (e.g., totals, ratios).
- Goal: understand how variables relate and identify potential data issues.

![Data overview](image/Deliverable%202.png)

---

## **Step 1 — Data Cleaning**

### **1.1 Handle Missing Grade Counts**

- For grade columns (`PK` → `AE`), rows where the sum equals `TOTAL` were identified.    
- Missing grade values in those rows were filled with **0**.
- Reason: ensures internal consistency when totals already match.
![Handle missing grade counts](image/Deliverable%202-1.png)

---

### **1.2 Remove Rows & Columns with Excessive Missing Data**

- Dropped rows with more than **55% missing values**.
- Dropped columns with more than **40% missing values**.
- Reason: reduces noise and unreliable information.
![Remove excessive missing data](image/Deliverable%202-3.png)

---

### **1.3 Replace Placeholder Codes**

- Replaced special codes (`-1, -2, -9, M, N`) with `NaN`.
- Reason: these represent missing or invalid data, not real values.
![Replace placeholder codes 1](image/Deliverable%202-4.png)
![Replace placeholder codes 2](image/Deliverable%202-5.png)

---

### **1.4 Impute and Fix Discrete Fields**

- Fixed ZIP codes by restoring leading zeros.
- Filled missing address/phone info with placeholders ("Unknown").
- Handle "FRELCH", "REDLCH", "TOTFRL" and "TOTAL" by the relationship between "TOTFRL" and "TOTAL".
![Impute discrete fields](image/Deliverable%202-6.png)
- Converted key columns (e.g., `DIRECTCERT`, `FRELCH`) to numeric.
- Reason: ensure correct data types and usability.
![Convert key columns](image/Deliverable%202-7.png)
   
---

### **1.5 Ensure Race & Enrollment Consistency**

- Converted race columns to numeric.
- Drop the ones that missing all the race counts.
- Checked whether race totals match overall totals.
- Imputed missing gender counts using median ratios.
![Race & enrollment consistency 1](image/Deliverable%202-8.png)
- Adding features for indicating the total matches the genders add up ("TOTAL_RACE_CONS")
- Adding features for indicating the total matches the genders add up ("TOTAL_GRADE_CONS").
![Race & enrollment consistency 2](image/Deliverable%202-9.png)
- Reason: maintain logical consistency across demographic data.
![Race & enrollment consistency 3](image/Deliverable%202-10.png)

---

### **1.6 Recalculate / Fill Derived Values**

- Filled missing `STUTERATIO` using `TOTAL / FTE` when possible.
- Reason: preserve a key analytical variable.
![Fill derived values](image/Deliverable%202-11.png)

---

### **1.7 Handle Edge Cases**

- Investigated potential outliers (IQR method) for `STUTERATIO`.
- Reason: detect unrealistic values.
![Handle edge cases](image/Deliverable%202-12.png)

---

## **Step 2 — Feature Processing**

### **2.1 Remove Low-Variance Features**

- Used `VarianceThreshold = 0.3` to drop nearly constant numeric features.
- Reason: these features add little predictive value.
![Remove low-variance features](image/Deliverable%202-13.png)

---

### **2.2 Correlation Analysis**

- Computed Pearson correlation on numeric predictors.
- Excluded target (`STUTERATIO`) from correlation detection.
- Removed highly correlated features to reduce duplicate information.
- Reason: improves model stability and interpretability.
![Correlation analysis](image/Deliverable%202-14.png)

---

### **2.3 Final Data Check**

- Verified dataset shape and remaining missing values.
- Ensured cleaning steps worked as expected.
![Final data check](image/Deliverable%202-15.png)    

---

## **Step 3 — Transformation & Scaling**

- Applied (or planned) **log transformations** for skewed count features.
- Considered standardization for modeling.
  `trans_cols = ["TOTFRL", "REDLCH", "PK", "KG", "G06", "G09", "G13", "UG", "AE", "STUTERATIO", "AMALM", "ASALM", "BLALM", "HPALM", "TRALM", "WHALM"]`
- Reason: improve distribution symmetry and model performance.
![Log transformations 1](image/Deliverable%202-17.png)
![Log transformations 2](image/Deliverable%202-18.png)
![Log transformations 3](image/Deliverable%202-19.png)
![Log transformations 4](image/Deliverable%202-20.png)
![Log transformations 5](image/Deliverable%202-21.png)
![Log transformations 6](image/Deliverable%202-22.png)
![Log transformations 7](image/Deliverable%202-23.png)
![Log transformations 8](image/Deliverable%202-24.png)
![Log transformations 9](image/Deliverable%202-25.png)
![Log transformations 10](image/Deliverable%202-26.png)
![Log transformations 11](image/Pasted%20image%2020260216151140.png)
![Log transformations 12](image/Deliverable%202-27.png)
![Log transformations 13](image/Deliverable%202-28.png)
![Log transformations 14](image/Deliverable%202-29.png)
![Log transformations 15](image/Deliverable%202-30.png)
![Log transformations 16](image/Deliverable%202-31.png)
![Log transformations 17](image/Deliverable%202-32.png)
![Log transformations 18](image/Deliverable%202-33.png)
![Log transformations 19](image/Deliverable%202-34.png)

### After log transformation:
- The ones that need: "TOTFRL", "REDLCH", "PK", "KG", "G06", "G09", "G13", "UG", "AE", "STUTERATIO", "AMALM", "ASALM", "BLALM", "HPALM", "TRALM", "WHALM"
![Log transformation result 1](image/Deliverable%202-35.png)
![Log transformation result 2](image/Deliverable%202-36.png)
![Log transformation result 3](image/Deliverable%202-37.png)
![Log transformation result 4](image/Deliverable%202-38.png)
![Log transformation result 5](image/Deliverable%202-39.png)
![Log transformation result 6](image/Deliverable%202-40.png)
![Log transformation result 7](image/Deliverable%202-41.png)
![Log transformation result 8](image/Deliverable%202-42.png)
![Log transformation result 9](image/Deliverable%202-43.png)
![Log transformation result 10](image/Deliverable%202-44.png)
![Log transformation result 11](image/Deliverable%202-45.png)
![Log transformation result 12](image/Deliverable%202-46.png)
![Log transformation result 13](image/Deliverable%202-47.png)
![Log transformation result 14](image/Deliverable%202-48.png)
![Log transformation result 15](image/Deliverable%202-49.png)
![Log transformation result 16](image/Deliverable%202-50.png)

---

## **Step 4 — Export Clean Dataset**

- Saved the cleaned dataset to CSV.
- Purpose: ready for modeling or analysis.
![Export dataset](image/Deliverable%202-16.png)
