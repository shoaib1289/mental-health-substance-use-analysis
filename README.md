# Mental Health & Substance Use Analysis in Canada

## Project Objective

This project investigates hospitalization and emergency department (ED) visit trends related to mental health and substance use across Canada and Ontario. The goal is to identify high-risk regions using public datasets and to inform healthcare resource planning and policy intervention strategies.

## Datasets Used

- **CIHI Mental Health Hospitalizations** (2017–2023)
- **CIHI Workforce Availability** (2019–2023)
- **PHO ED Visits by PHU** (2014–2024)
- **Provider Density by PHU** (2025)
- **ON-Marg Deprivation Index** (2021)

## Key Analyses

1. **Crude Rate Trends (2017–2023):**  
   Analyzed mental health hospitalization rates by province.

2. **Workforce Correlation Analysis:**  
   Investigated the relationship between psychologist availability and hospitalization rates using Pearson and Spearman correlation, with and without log transformation.

3. **Opioid ED Visit Trends (2014–2024):**  
   Assessed monthly opioid-related ED visits by PHU.

4. **Socioeconomic Disparities:**  
   Modeled the effect of material deprivation on substance-related ED visits using ON-Marg indices and linear regression.

5. **Substance Use Mortality Trends:**  
   Explored death rates by substance type (opioid, stimulant, benzodiazepine) and regional differences.

6. **Composite Risk Score Mapping:**  
   Combined ED rates, deprivation index, and provider shortage into a single risk index to prioritize PHUs for intervention.

## Methods & Tools

- **Languages:** Python (Pandas, NumPy, Seaborn, Scikit-learn, Statsmodels)
- **Visualization:** Matplotlib, Seaborn, Plotly
- **Data Cleaning & Merging:** Custom scripts with robust error handling
- **Statistical Models:** Correlation, Regression, Z-score normalization, Risk Index formulation

## Insights & Recommendations

- Provinces with lower mental health workforce tend to have higher hospitalization rates.
- Opioid-related ED visits surged post-2018, with high burden in Northern Ontario PHUs.
- PHUs with high deprivation and low provider access require urgent support.
- Created a composite risk index to assist policy-makers in resource targeting.

## Error Checking & Validation

All datasets were cleaned for missing values, suppressed data flags were handled, and results were validated through exploratory analysis and AIC/BIC diagnostics for models.

## How to Run

```bash
# Create a virtual environment
python -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows

# Install dependencies
pip install -r requirements.txt

# Run scripts or notebooks
jupyter notebook
