# Mental Health & Substance Use Hospitalization Analysis (Canada & Ontario)

## Objective

Mental health and substance-use–related emergencies have been rising across Canada, particularly in Ontario. As someone who regularly witnesses these challenges in downtown communities, I wanted to explore:

- What factors contribute to higher hospitalization or ED visit rates?
- Are some regions at disproportionately higher risk?
- Can we quantify and map these risks to guide targeted interventions?

Using a multi-source public dataset approach, this project analyzes provincial and PHU-level disparities, trends in ED visits, mental health workforce availability, socioeconomic deprivation, and mortality patterns related to substance use.

---

## 🗂Datasets Used

| Dataset Name                                | Source                    | Description |
|---------------------------------------------|----------------------------|-------------|
| `cihi_hospitalization_prov_year_2017_2023`  | CIHI                      | Annual MH hospitalizations by province |
| `cihi_workforce_prov_year_2019_2023`        | CIHI                      | Psychologist counts per province |
| `pho_ed_visits_phu_month_2014_2024`         | Public Health Ontario     | Monthly substance-use ED visits per PHU |
| `onmarg_phu_static_2021`                    | Ontario Marginalization Index | Deprivation scores by PHU |
| `provider_density_phu_2025_long`            | Compiled from Public PHU data | Number of facilities per 10,000 residents in each PHU |

All datasets were cleaned and harmonized for matching temporal and geographic resolution.

---

## Methodology

### 1. Crude Hospitalization Rate Trends (Analysis 1)
- Calculated crude rate = `(hospitalizations / population) * 100,000`
- Used line plots to visualize province-level trends (2017–2023)
- Identified provinces with persistently high MH hospitalization burden

### 2. Workforce vs. Hospitalization Rate Correlation (Analysis 2)
- Merged hospitalization and psychologist data by province-year
- Used **Pearson** and **Spearman** correlation, with and without **log transformation**
- Regression modeling was run on 34 province-year data points (a limitation explained in notes)
- Outliers controlled via scatterplot review and log scaling

### 3. ED Visit Trends – Opioid Related (Analysis 3)
- Aggregated monthly ED visits by PHU
- Created rolling averages to smooth spikes
- Highlighted sharp increase in opioid-related ED visits post-2017
- Visualized high-burden PHUs like Sudbury and Thunder Bay

### 4. Socioeconomic Disparity & ED Burden (Analysis 4)
- Merged ON-Marg deprivation index with PHU ED data
- Linear regression tested the relationship between **material deprivation** and average ED burden
- Controlled for multicollinearity and residual skewness
- Emphasized how structural disadvantage predicts ED reliance

### 5. Substance Use Deaths by Substance Type (Analysis 5)
- Examined trends in mortality by opioids, stimulants, benzos, and combinations
- Identified rising deaths due to **polysubstance abuse**, especially **benzo + opioid** (benzo-dope)
- Highlighted regional variation (Northern PHUs hit hardest)

### 6. Composite Risk Index (Analysis 6)
- Normalized three indicators:
  - Avg. opioid-related ED rate (high = high risk)
  - Material deprivation (high = high risk)
  - Facility access per 10K (low = high risk)
- Final Risk Score =  
  `normalized_ED_rate + deprivation_score + (1 - normalized_facility_density)`
- Top 5 PHUs flagged for urgent intervention
- Created bar plots instead of maps to visualize PHU-level risk ranking

---

## Tools & Technologies

- **Languages**: Python (Pandas, NumPy, Matplotlib, Seaborn, Statsmodels)
- **Notebook Environment**: Jupyter
- **Visualizations**: Matplotlib, Seaborn, Plotly
- **Data Transformation**: Merge, Aggregation, Normalization, Rolling Averages
- **Statistical Models**: Linear Regression, Pearson/Spearman correlation, Composite Index
- **File Handling**: CSV, long-format merging, temporal joins

---

## Challenges Encountered & Fixes

| Issue | Resolution |
|-------|------------|
| Inconsistent formats (wide vs. long) | Standardized to long format, reshaped with `pd.melt()` and `groupby()` |
| Suppressed values in PHO data | Dropped or imputed with rolling mean for time series smoothness |
| Different geographic identifiers (e.g., HUID vs PHU name) | Used manual mapping between HUID and PHU |
| Small N in regression (~34 points) | Acknowledged in limitations; used log transformation and visualization to reduce outlier impact |
| Missing facility counts | Manually scraped and validated through official regional sources |

---

## Results Summary

| Key Finding | Insight |
|-------------|---------|
| **High hospitalization rates** | Provinces like Saskatchewan and Manitoba had consistently high MH hospitalization rates (crude rate > 500) |
| **Workforce shortage link** | Provinces with lower psychologist availability tended to show higher hospitalization rates |
| **Opioid ED burden** | Opioid-related ED visits have steadily risen in most PHUs since 2017 |
| **Disparity impact** | Higher deprivation PHUs showed significantly higher substance-use ED burdens |
| **Hotspot PHUs** | Sudbury, Thunder Bay, Timiskaming flagged with highest composite risk index |

---

## Recommendations

- **Invest in workforce**: Scale psychologist coverage, especially in high-burden provinces
- **Expand harm reduction services**: Especially in Northern Ontario
- **Targeted resource allocation**: Use composite risk index to drive policy prioritization
- **Enhance data collection**: Address suppressed or missing data to enable better predictive models

---

##  How to Run This Project

```bash
# Create a virtual environment
python -m venv venv
source venv/Scripts/activate  # or venv/bin/activate (Mac/Linux)

# Install dependencies
pip install -r requirements.txt

# Launch Jupyter
jupyter notebook

