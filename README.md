# Covid19-Vaccination-and-Case-Analysis
Python analysis and Power BI Dashboard exploring global COVID-19 vaccination progress and case trends using data from Our World in Data (OWID).
# 🦠 COVID-19 Vaccination & Case Analysis Dashboard (Python + Power BI)

This repository contains a complete data analytics project analyzing global COVID-19 **vaccination** and **case** trends using data from [Our World in Data (OWID)](https://ourworldindata.org/covid-vaccinations).

---

## 🐍 Data Cleaning & Analysis (Python)

Before building the Power BI report, we processed the data using **Python (Pandas + Matplotlib + Seaborn)**.

### ✅ Python Key Steps:
- Loaded vaccination and case data
- Cleaned NaN and inconsistent values
- Merged on `location` and `date`
- Created histograms, line plots, and correlation heatmaps

### 🧠 Sample Python Code:

```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Load data
vacc = pd.read_csv('vaccinations.csv')
cases = pd.read_csv('cases.csv')

# Convert 'date' to datetime
vacc['date'] = pd.to_datetime(vacc['date'])
cases['date'] = pd.to_datetime(cases['date'])

# Clean data: drop rows with missing key values
vacc = vacc.dropna(subset=['total_vaccinations', 'people_vaccinated'])
cases = cases.dropna(subset=['total_cases'])

# Merge data on location and date
df = pd.merge(vacc, cases, on=['location', 'date'], how='inner')

# Histogram of vaccinations
plt.figure(figsize=(10, 5))
plt.hist(df['people_vaccinated_per_hundred'].dropna(), bins=15, color='green', alpha=0.7)
plt.title("People Vaccinated per Hundred - Distribution")
plt.xlabel("People Vaccinated per 100")
plt.ylabel("Number of Countries")
plt.grid(True)
plt.tight_layout()
plt.show()

# Line plot of vaccinations vs total cases
top_countries = df['location'].value_counts().head(5).index
plt.figure(figsize=(12, 6))
for country in top_countries:
    country_data = df[df['location'] == country]
    plt.plot(country_data['date'], country_data['total_cases'], label=f'{country} Cases')
plt.legend()
plt.title("Total COVID-19 Cases Over Time (Top Countries)")
plt.xlabel("Date")
plt.ylabel("Total Cases")
plt.tight_layout()
plt.show()

# Correlation heatmap
selected_cols = ['total_vaccinations', 'people_vaccinated', 'people_fully_vaccinated', 'total_cases']
corr = df[selected_cols].corr()
sns.heatmap(corr, annot=True, cmap='coolwarm')
plt.title("Correlation Matrix")
plt.show()

---

## 📊 Dashboard Features (Power BI)

This Power BI report includes five pages:

1. Dashboard Overview – All visuals in one summary page  
2. Total Cases by Vaccination Status – Bar chart comparing cases vs vaccination  
3. Vaccination Totals by Country – Country-wise vaccination totals  
4. Global Vaccination Map – Filled map with vaccination per 100  
5. Interactive Filters Panel – Slicers for filtering by country/date

---

🧑‍💻 Author
Taranpal Singh
Data Analyst | Power BI & Python Enthusiast
