# Comparative A/B Testing for Facebook and Google AdWords

## Project Description
This project performs an A/B testing analysis to compare advertising campaigns on Facebook and Google AdWords. Through data collection, statistical testing, and time series analysis, this project aims to uncover the most cost-effective advertising strategies and the optimal campaign timings.

## Objectives
- **Data Collection**: Gather and preprocess conversion data from Facebook and Google AdWords.
- **Statistical Analysis**: Use statistical methods to compare conversion rates across platforms.
- **Time Series Analysis**: Analyze time trends to determine the best campaign timings.
- **Cost Efficiency Analysis**: Evaluate the cost-effectiveness of each platform's campaigns.

## Setup and Installation
Ensure you have Python installed, along with the necessary libraries:
- Pandas for data manipulation
- SciPy for statistical analysis
- Matplotlib for data visualization

You can install them using pip:
```bash
pip install pandas scipy matplotlib


## Project Structure

1. Data Collection
python
Copy code
import pandas as pd

# Example of loading data from CSV files
facebook_data = pd.read_csv('facebook_campaign_data.csv')
adwords_data = pd.read_csv('google_adwords_data.csv')

# Combine data into a single DataFrame for analysis
combined_data = pd.concat([facebook_data, adwords_data], ignore_index=True)

# Preprocessing data by removing any missing values
cleaned_data = combined_data.dropna()
2. Statistical Analysis
python
Copy code
from scipy import stats

# Extracting conversion data for statistical comparison
facebook_conversions = cleaned_data[cleaned_data['platform'] == 'Facebook']['conversion_rate']
google_conversions = cleaned_data[cleaned_data['platform'] == 'Google']['conversion_rate']

# Performing a two-sample t-test between the conversion rates of Facebook and Google
t_stat, p_value = stats.ttest_ind(facebook_conversions, google_conversions)

print(f"T-test results -- T-statistic: {t_stat}, P-value: {p_value}")
3. Time Series Analysis
python
Copy code
import matplotlib.pyplot as plt

# Convert the 'date' column to datetime format for time series analysis
cleaned_data['date'] = pd.to_datetime(cleaned_data['date'])

# Grouping data by month and platform for analysis
monthly_data = cleaned_data.groupby([cleaned_data['date'].dt.to_period('M'), 'platform']).sum()

# Plotting monthly conversions
monthly_data.unstack().plot(kind='bar')
plt.title('Monthly Conversions by Platform')
plt.xlabel('Month')
plt.ylabel('Total Conversions')
plt.show()
4. Cost Efficiency Analysis
python
Copy code
# Calculate and plot cost per conversion over time
cleaned_data['cost_per_conversion'] = cleaned_data['total_spend'] / cleaned_data['conversions']

plt.figure(figsize=(10,5))
for platform in ['Facebook', 'Google']:
    platform_data = cleaned_data[cleaned_data['platform'] == platform]
    plt.plot(platform_data['date'], platform_data['cost_per_conversion'], label=f'{platform} Cost per Conversion')

plt.legend()
plt.title('Cost Per Conversion Over Time by Platform')
plt.xlabel('Date')
plt.ylabel('Cost Per Conversion')
plt.show()

