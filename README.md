# 📝 NYC Public High Schools SAT Score Analysis

A data-driven exploration of SAT performance across New York City public high schools. This project focuses on data cleaning and visualization to understand borough- and city-level patterns, enrollment characteristics, attendance hours, and SAT section scores.

---

## 📂 View Notebook

[📄 Open Visualization Notebook](https://github.com/jp-asadon/sat_scores/blob/main/notebook.ipynb)

---

## 📋 Table of Contents

- [About the Project](#about-the-project)
- [Dataset](#dataset)
- [Project Highlights](#project-highlights)
- [Key Visualizations](#key-visualizations)
- [How to Run](#how-to-run)
- [Conclusion & Insights](#conclusion--insights)
- [Future Improvements](#future-improvements)
- [Acknowledgments](#acknowledgments)

---

## 🧠 About the Project

This repository contains a cleaned and visualized analysis of NYC public high school SAT scores using publicly available data from Kaggle. The analysis explores:

- Which boroughs and cities exhibit higher average SAT performance?
- How do reading, writing, and math scores differ across boroughs?
- What does enrollment distribution look like across cities and schools?
- Is there a relationship between the length of the school day and SAT outcomes?

Repository: https://github.com/jp-asadon/sat_scores

---

## 📊 Dataset

**Source:** [Average SAT Scores for NYC Public Schools — Kaggle](https://www.kaggle.com/datasets/nycopendata/high-schools/data)

**Shape:** 374 rows × 22 columns

**Description:**  
The dataset includes one row per accredited NYC high school with administrative and location metadata, bell times (start/end), enrollment totals with race breakdown, and average SAT section scores for the 2014–2015 school year.

### 📄 Data Dictionary (exact columns)

| Column | Type | Description |
|-------|------|-------------|
| `School ID` | object | Department/DOE school identifier |
| `School Name` | object | Official school name |
| `Borough` | object | NYC borough of the school |
| `Building Code` | object | DOE building code |
| `Street Address` | object | Street address |
| `City` | object | City field in the record |
| `State` | object | State (NY) |
| `Zip Code` | int64 | ZIP code |
| `Latitude` | float64 | Latitude |
| `Longitude` | float64 | Longitude |
| `Phone Number` | object | School contact number |
| `Start Time` | object | Start time (string; needs parsing) |
| `End Time` | object | End time (string; needs parsing) |
| `Student Enrollment` | float64 | Total enrolled students (numeric; often treated as int) |
| `Percent White` | object | Percent white (e.g., "12%"; convert to numeric) |
| `Percent Black` | object | Percent Black (e.g., "25%"; convert to numeric) |
| `Percent Hispanic` | object | Percent Hispanic (e.g., "43%"; convert to numeric) |
| `Percent Asian` | object | Percent Asian (e.g., "18%"; convert to numeric) |
| `Average Score (SAT Math)` | float64 | Average SAT Math |
| `Average Score (SAT Reading)` | float64 | Average SAT Reading |
| `Average Score (SAT Writing)` | float64 | Average SAT Writing |
| `Percent Tested` | object | Percent of students tested (e.g., "62%"; convert to numeric) |

Derived in this analysis:
- `Average Score (SAT Total)`: sum of Reading, Writing, and Math averages.
- `School Day Hours`: duration derived from `Start Time` and `End Time` (parsed to hours).
- `School Day Hour Cluster`: binned ranges like `5.0–5.99`, `6.0–6.99`, `7.0–7.99`, etc.

Cleaning notes:
- Convert percent fields (e.g., `Percent White`, `Percent Tested`) from strings like "62%" to numeric proportions or percentages.
- Parse `Start Time` and `End Time` to datetimes, handling formats (e.g., "8:00 AM") and compute duration in hours.
- Cast `Student Enrollment` to integer if appropriate.

---

## 📈 Project Highlights

- ✅ Data Cleaning (types, missing values, time parsing, percent normalization)
- ✅ Borough- and City-level Summaries
- ✅ SAT Section Comparisons (Reading, Writing, Math, and Total)
- ✅ Enrollment Distribution Analysis
- ✅ Attendance Hours vs. SAT Performance Exploration
- ✅ Top-K Ranking Visuals (Enrollment by school/city)

---

## 🖼️ Key Visualizations

### 🏙️ Top Boroughs by Verbal (Reading) Score
- Ranks boroughs by average SAT Reading score.

### 🌈 Racial Distribution per Borough
- Visualizes enrollment composition by race/ethnicity across boroughs.

### 🧭 Average Scores by Borough
- Reading, Writing, Math, and Total SAT score comparisons by borough.

### ⏰ Average SAT Score Distribution by Total Hours Attended
- Distribution of SAT scores relative to estimated school-day hours.

### 🧩 Average SAT Score by Attendance Hour Clusters
- Binned clusters (e.g., `5.0–5.99`, `6.0–6.99`, `7.0–7.99`) to compare average SAT outcomes.

### 🗺️ Number of Schools per City
- City-level count of schools represented in the dataset.

### 👥 Average Student Enrollment by City
- Mean enrollment per city, highlighting concentration and scale.

### 🏫 Top 10 Schools with Highest Enrollment
- Bar chart of the 10 largest schools by enrollment.

### 🧭 Top 10 Cities with Highest Enrollment
- Aggregate enrollment by city, ranked and visualized.

---

## 🚀 How to Run

### 1) Clone the repository
```bash
git clone https://github.com/jp-asadon/sat_scores.git
cd sat_scores
```

### 2) (Recommended) Create and activate a virtual environment

macOS/Linux:
```bash
python3 -m venv .venv
source .venv/bin/activate
```

Windows (PowerShell):
```powershell
python -m venv .venv
.venv\\Scripts\\Activate.ps1
```

### 3) Install dependencies

If a `requirements.txt` is present:
```bash
pip install -r requirements.txt
```

Or install packages directly:
```bash
pip install pandas numpy matplotlib seaborn jupyter
```

### 4) Launch Jupyter and open the notebook
```bash
jupyter notebook
```

Then open `notebook.ipynb` and run cells top-to-bottom.

> Tip: You can also use `jupyter lab` if you prefer.

---

## 📌 Conclusion & Insights

From this exploratory analysis:

- Boroughs differ in average SAT section performance; comparing Reading, Writing, and Math together provides a fuller picture than any single section.
- Estimated school-day hours show possible non-linear relationships with SAT outcomes; interpret cautiously due to schedule/reporting noise.
- Enrollment distributions are skewed; very large and very small schools appear across the performance spectrum, suggesting enrollment alone is not a reliable predictor.
- City-level summaries reveal concentration of schools and students in a handful of locations, which can influence borough averages.
- Demographic composition varies across boroughs; comparisons should consider these context variables.

These are descriptive findings and do not imply causality.

---

## 🔭 Future Improvements

- Add statistical testing (e.g., ANOVA, effect sizes) for borough differences and hour-cluster comparisons.
- Model-based analysis (regularized regression or gradient boosting) to assess feature importance beyond group means.
- Robust handling of bell-time parsing (time zones, format variability) and validation against multiple sources.
- Geospatial analysis (e.g., Folium/Kepler.gl) for mapping schools and scores.
- Interactive dashboard (Streamlit/Plotly Dash) to explore filters by borough, city, enrollment, and hours.
- Automate data refresh and document data lineage/versioning.

---

## 🙌 Acknowledgments

- Dataset: NYC Open Data via Kaggle — Average SAT Scores for NYC Public Schools  
  https://www.kaggle.com/datasets/nycopendata/high-schools/data
- Compiled by the NYC Department of Education; SAT averages and testing rates provided by the College Board.
- Inspiration: Which schools/boroughs score highest? Which sections lead/lag? How do enrollment and hours relate?

---

If you find this helpful, please ⭐ the repo and open an issue for ideas or questions!
```
```

