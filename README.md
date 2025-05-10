# NYPD Complaint History – Big Data Processing Pipeline

## Project Overview
This project analyzes large-scale public safety data from New York City using Big Data technologies. The core dataset is the **NYPD Complaint Historic Dataset (2006–2025)**, containing millions of crime records across NYC. **The fine named NYPD_Complaints_(Main_File).ipynb contains the main notebook details.**

Instead of simple analysis, we've built a **scalable and reusable data pipeline using Apache Spark** to:
- Clean, enrich, and profile the data
- Integrate additional datasets like arrests, shootings, and emergency responses
- Generate structured outputs for dashboards, machine learning, or research

---

##  Key Features
- Handles **millions of records** efficiently with Apache Spark
- Adds **geographic context** (reverse geocoding lat/lon → borough)
- Merges multiple NYC datasets: Arrests, Shootings, 911 Calls, etc.
- Modular preprocessing functions for reuse
- Scalable for cloud deployment (e.g., AWS, GCP, Databricks)

---

## How to Run

### 1. Environment Setup
- Python 3.7+
- Apache Spark (via PySpark)
- Jupyter Notebook or Google Colab

### 2. Required Libraries

```bash
pip install pyspark geopandas openclean geopy pandas numpy matplotlib seaborn
```

Colab already includes some, or install via:

```python
!pip install pyspark openclean geopandas
```

### 3. Run Notebook Step-by-Step

- Initialize Spark
- Download NYPD datasets
- Clean + enrich using preprocessing modules
- (Optional) Merge with additional datasets
- Visualize and export results

---

## Code Logic Overview

### 1. Spark Setup
- Spark session creation
- Imports: geopandas, openclean, matplotlib, seaborn

### 2. Data Ingestion
- NYPD dataset downloaded from Open Data API
- Loaded into Spark DataFrame

### 3. Preprocessing Modules

Reusable cleaning functions for:
- `valid_date_check()` – Cleans date format (removes out-of-range values)
- `valid_time_check()` – Ensures valid 24-hour format
- `reverse_geo_code_boros()` – Converts lat/lon → borough
- `refine_age_group_race()` – Cleans age/race fields
- `refine_sex_gender_impute()` – Fixes unknown gender/sex
- `refine_precinct_jur()` – Standardizes precinct/jurisdiction info

Other filters include:
- `level_of_offense_check()`
- `KY_CD_Check()`, `hpsa_check()`, `prem_check()`, `pd_cd_check()`

### 4. Integration with Other NYC Datasets
We applied the same pipeline to:
- Arrests
- Shooting Incidents
- 911 Emergency Calls
- Motor Vehicle Collisions
- Rodent Inspection (for testing noise-related geospatial correlation)

### 5. Profiling & Visualization
- Used OpenClean for data profiling
- Plotted borough-wise heatmaps, offense breakdowns, and demographic distributions
- Calculated precision and recall based on valid records

---

## External Datasets Used

| Dataset                  | Source |
|--------------------------|--------|
| [Complaint Data](https://data.cityofnewyork.us/Public-Safety/NYPD-Complaint-Data-Historic/qgea-i56i) |
| [Arrests](https://data.cityofnewyork.us/Public-Safety/NYPD-Arrests-Data-Historic-/8h9b-rp9u) |
| [Vehicle Collisions](https://data.cityofnewyork.us/Public-Safety/Motor-Vehicle-Collisions-Crashes/h9gi-nx95) |
| [Shooting Incidents](https://data.cityofnewyork.us/Public-Safety/NYPD-Shooting-Incident-Data-Historic-/833y-fsy8) |
| [911 Calls](https://data.cityofnewyork.us/Public-Safety/Emergency-Response-Incidents/pasr-j7fb) |
| [Use of Force](https://data.cityofnewyork.us/Public-Safety/NYPD-Use-of-Force-Incidents/f4tj-796d) |
| [Rodent Inspection](https://data.cityofnewyork.us/Health/Rodent-Inspection/p937-wjvj) |

---



> _“Turning massive city data into meaningful safety insights”_

