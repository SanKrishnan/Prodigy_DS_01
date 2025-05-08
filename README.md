✅ Task 1: Visualize Total Population Distribution (2023)
📌 Task Description
Create a bar chart or histogram to visualize the distribution of a categorical or continuous variable, such as total population across countries.

🔗 Dataset Used
World Bank Indicator: SP.POP.TOTL

🐍 Sample Code
python
Copy
Edit
import pandas as pd
import requests
import matplotlib.pyplot as plt

def fetch_total_population(year=2023):
    url = f"http://api.worldbank.org/v2/country/all/indicator/SP.POP.TOTL?format=json&date={year}&per_page=300"
    response = requests.get(url)
    data = response.json()
    entries = data[1]
    result = []
    for entry in entries:
        country = entry['country']['value']
        value = entry['value']
        if value is not None and country != 'World':
            result.append((country, value))
    df = pd.DataFrame(result, columns=['Country', 'Population'])
    return df

def plot_population_distribution(df, top_n=10):
    df_sorted = df.sort_values(by="Population", ascending=False).head(top_n)
    plt.figure(figsize=(12, 6))
    plt.bar(df_sorted["Country"], df_sorted["Population"], color="mediumseagreen")
    plt.title(f"Top {top_n} Countries by Total Population (2023)")
    plt.ylabel("Population")
    plt.xlabel("Country")
    plt.xticks(rotation=45)
    plt.tight_layout()
    plt.grid(axis='y', linestyle='--', alpha=0.5)
    plt.show()
🌍 World Population Age Group Analysis
This Python project visualizes population data across different age groups and total population statistics using the World Bank API. It includes top/bottom comparisons and year-on-year demographic insights.

📊 Features
Fetches and analyzes population data by age group:

0-14 years

15-64 years

65+ years

For each age group:

Visualizes Top 5 countries by percentage (2023)

Visualizes Bottom 5 countries by count (2023)

Compares 2022 vs 2023 for Top 5 countries (percentage)

Includes Task 1: Total population distribution chart

📦 Requirements
Python 3.x

pandas

requests

matplotlib

✅ Install Dependencies
bash
Copy
Edit
pip install pandas requests matplotlib
