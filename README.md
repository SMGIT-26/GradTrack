# GradTrack
Analyzing graduation rates and cohort trends for Institutional Effectiveness using Excel and Power BI
# Institutional Effectiveness Data Project – Graduation Rate Analysis

This project was developed as part of the selection process for the Institutional Effectiveness Internship at Midwestern State University. The objective was to calculate and analyze graduation rates for the **Fall 2012 cohort** (including **preceding Summer I and Summer II students**) and derive equity-focused insights using Excel and Power BI.

---

## 🎯 Project Goal

To calculate the percentage of students from the **Fall 2012 cohort** who graduated within:
- **4 years**
- **6 years**
- **8 years**

…and to analyze these metrics across different student demographics (especially **ethnicity**), delivering actionable insights for institutional planning.

---

## 📁 Files in this Repository

| File Name                     | Description |
|------------------------------|-------------|
| `EnrollmentData_Cleaned.xlsx` | Final Excel with cohort filtering, grad year flags, and pivot tables |
| `DegreesAwarded.csv`         | Original degree data used for matching graduation |
| `Dashboard.pbix`             | Power BI file showing visual insights |
| `Dashboard_PDF.pdf`          | Snapshot of the Power BI dashboard |
| `Documentation.pdf`          | Step-by-step explanation of the entire process |
| `Presentation_Slides.pdf`    | Final summary slides for 5-minute presentation |
| `DAX_Notes.txt`              | All key DAX formulas used in the dashboard |

---

## 🧹 Step-by-Step Data Preparation

1. **Import Raw Data:**
   - `EnrollmentData_Fall2012.csv` (included students with term codes `201280`, `201290`, and `201310` per cohort definition)
   - `DegreesAwarded.csv` (used to find graduation status)

2. **Cohort Filtering (Fall 2012):**
   - **Term Codes Used**:
     - Summer I: `201280`
     - Summer II: `201290`
     - Fall: `201310`
   - Filtered only **first-time full-time students**.

3. **Graduation Flags (in Excel):**
   - Merged degree data using **VLOOKUP**:
     ```excel
     =VLOOKUP([@StudentID], DegreesAwarded!$A:$Z, Col#, FALSE)
     ```
   - Added flags:
     - **Grad_4yr**: 1 if graduated by **201630**
     - **Grad_6yr**: 1 if graduated by **201830**
     - **Grad_8yr**: 1 if graduated by **202030**
   - Used IF logic:
     ```excel
     =IF([@GraduationTerm] <= "201630", 1, 0)
     ```

4. **Data Cleaned:**
   - Removed null and duplicate values
   - Standardized columns for ethnic group analysis
   - Re-coded graduation flags: `1 → Graduated`, `0 → Not Graduated`

---

## 📊 Analysis & Visuals (Power BI)

### Dashboard Pages:
- **Overall Graduation Rates**
- **Comparison by Ethnicity**
- **Graduation Trends over Time**
- **Insights & Recommendations**

### Sample DAX Formulas:
```DAX
Graduated_4yr = IF([Graduation Term] <= "201630", "Graduated", "Not Graduated")
Graduated_6yr = IF([Graduation Term] <= "201830", "Graduated", "Not Graduated")
Graduated_8yr = IF([Graduation Term] <= "202030", "Graduated", "Not Graduated")
