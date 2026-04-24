# 🚗 NYC Collision Insights

An interactive data engineering project that ingests, cleans, integrates, and visualizes **NYC Motor Vehicle Collision** data sourced from [NYC Open Data](https://opendata.cityofnewyork.us/).

---

## 📌 Overview

This project builds a complete data pipeline—from raw CSV downloads straight from the NYC Open Data API to a polished, browser-based dashboard—enabling exploration of nearly **1 million collision records** across all five New York City boroughs.

Key highlights:
- **ETL pipeline** implemented in a reproducible Jupyter notebook
- Merges two large open datasets (Crashes + Persons) on `COLLISION_ID`
- Stores the cleaned output with **Git LFS** to keep the repo lightweight
- Serves an interactive **Plotly Dash** dashboard with light/dark mode

---

## 🗂️ Project Structure

```
NYC-Collision-Insights/
├── DE_Project_data_pre_processing.ipynb  # ETL pipeline (data loading, cleaning & integration)
├── project_de_.py                        # Dash web application
├── cleaned_nyc_crashes.csv               # Processed dataset (tracked via Git LFS)
├── requirements.txt                      # Python dependencies
└── README.md
```

---

## 📊 Data Sources

| Dataset | Source | Records (approx.) |
|---------|--------|-------------------|
| Motor Vehicle Collisions – Crashes | [NYC Open Data](https://data.cityofnewyork.us/Public-Safety/Motor-Vehicle-Collisions-Crashes/h9gi-nx95) | ~988 K |
| Motor Vehicle Collisions – Persons | [NYC Open Data](https://data.cityofnewyork.us/Public-Safety/Motor-Vehicle-Collisions-Person/f55k-p6yu) | ~2 M+ |

---

## ✨ Dashboard Features

- **Interactive collision map** – scatter plot of crash locations sized by injury count
- **Borough filter** – drill down into any of NYC's five boroughs
- **Light / Dark mode toggle** – powered by Bootstrap Minty theme

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| Python 3 | Core language |
| Pandas & NumPy | Data wrangling & memory optimization |
| Plotly Express | Chart rendering |
| Dash + Dash Bootstrap Components | Web dashboard framework |
| Git LFS | Large-file storage for the cleaned CSV |
| Google Colab | ETL notebook execution environment |

---

## 🚀 Getting Started

### Prerequisites

- Python 3.8+
- [Git LFS](https://git-lfs.github.com/) (required to download the cleaned dataset)

### 1 – Clone the repository

```bash
git lfs install
git clone https://github.com/Khaled100233/NYC-Collision-Insights.git
cd NYC-Collision-Insights
```

> Git LFS will automatically pull `cleaned_nyc_crashes.csv` during the clone.

### 2 – Install dependencies

```bash
pip install -r requirements.txt
```

### 3 – Run the dashboard

```bash
python project_de_.py
```

Then open your browser at **http://localhost:8050**.

---

## 🔄 Reproducing the ETL Pipeline (optional)

If you want to regenerate `cleaned_nyc_crashes.csv` from scratch, open `DE_Project_data_pre_processing.ipynb` in [Google Colab](https://colab.research.google.com/) or a local Jupyter environment and run all cells.

The notebook will:
1. Download the **Crashes** dataset from the NYC Open Data API
2. Download the **Persons** dataset in chunks (≈ 200 K rows per chunk)
3. Clean column names, parse dates/times, handle missing values and remove duplicates
4. Left-join crashes with persons on `COLLISION_ID`
5. Downcast numeric dtypes for memory efficiency
6. Save the result as `cleaned_nyc_crashes.csv`

---

## 📁 Dataset Schema (cleaned)

| Column | Description |
|--------|-------------|
| `CRASH_DATE` | Date of the collision |
| `CRASH_TIME` | Time of the collision |
| `BOROUGH` | NYC borough (or *Unknown*) |
| `LATITUDE` / `LONGITUDE` | Geolocation of the crash |
| `NUMBER_OF_PERSONS_INJURED` | Total persons injured |
| `NUMBER_OF_PERSONS_KILLED` | Total fatalities |
| `CONTRIBUTING_FACTOR_VEHICLE_*` | Reported contributing factors |
| `VEHICLE_TYPE_CODE_*` | Vehicle types involved |
| `COLLISION_ID` | Unique crash identifier (join key) |
| `PERSON_TYPE` | Occupant, Pedestrian, Bicyclist, etc. |
| `PERSON_INJURY` | Injury status of the person |
| `PERSON_AGE` | Age of the person involved |
| `PERSON_SEX` | Sex of the person involved |

---

---

## 📄 License

This project is open-source and available under the [MIT License](LICENSE).
