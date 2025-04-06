# Covid-19-Vaccinations-Trend-Dashboard

## Project Overview
This dashboard visualizes global COVID-19 vaccination trends using data from Our World in Data. The interactive visualization allows users to explore vaccination progress across countries, compare vaccination rates, and analyze temporal patterns in vaccine distribution and administration.

## Live Dashboard
https://public.tableau.com/views/Book1_17439827465750/Dashboard1?:language=en-US&publish=yes&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link

## Data Source
- **Primary Dataset**: [Our World in Data COVID-19 Vaccination Dataset](https://ourworldindata.org/covid-vaccinations)
- **Last Updated**: April 2025
- **Data Range**: December 2020 - March 2025
- **Key Metrics**: Total vaccinations, people fully vaccinated, vaccination rates per 100 people

### Visualizations
1. **Global Vaccination Progress** - Time series showing the cumulative number of vaccinations worldwide
2. **Country Comparison** - Bar chart ranking countries by vaccination rates
3. **Vaccination Rate Map** - Choropleth map displaying global vaccination coverage

## Key Insights
- Global vaccination rates reached X% by March 2025
- Highest vaccination rates were achieved in [Countries]
- Significant disparities exist between [Regions]
- Vaccination campaigns accelerated most rapidly during [Time Period]
- Correlation between [Factors] and vaccination success

## Technical Implementation
- **Visualization Tool**: Tableau Public
- **Data Preprocessing**: Python (pandas) for data cleaning and feature engineering
- **Data Transformation**:
  - Calculated days since first vaccination
  - Normalized rates for population comparison
  - Created regional aggregations
  - Removed incomplete data points

## Data Preprocessing
The raw data was preprocessed using a Python script to:
1. Clean missing values
2. Convert date formats
3. Calculate derived metrics
4. Normalize country names
5. Create temporal features

```python
# Sample of preprocessing code
import pandas as pd

# Load and clean the data
df = pd.read_csv('covid-vaccination-data.csv')
df['date'] = pd.to_datetime(df['date'])
df = df.dropna(subset=['total_vaccinations'])

# Create derived features
location_col = 'country'
first_dates = df.groupby(location_col)['date'].min().reset_index()
first_dates.columns = [location_col, 'first_date']
df = pd.merge(df, first_dates, on=location_col)
df['days_since_first_vax'] = (df['date'] - df['first_date']).dt.days

# Save processed data
df.to_csv('processed_covid_data.csv', index=False)
```
