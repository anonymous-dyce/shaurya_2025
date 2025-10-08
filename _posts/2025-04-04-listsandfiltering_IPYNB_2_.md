---
layout: page
title: Lists and Filtering HW
toc: True
permalink: /binary_history/listsandfilteringhw
categories: ['CSP Classwork']
---

### POPCORN HACK #1

``` python
def find_students_in_range(df, min_score, max_score):
    return df[(df['Score'] >= min_score) & (df['Score'] <= max_score)]
```

### POPCORN HACK #2

```python
def add_letter_grades(df):
    def get_letter(score):
        if score >= 90:
            return 'A'
        elif score >= 80:
            return 'B'
        elif score >= 70:
            return 'C'
        elif score >= 60:
            return 'D'
        else:
            return 'F'

    df['Letter'] = df['Score'].apply(get_letter)
    return df
```

### POPCORN HACK #3

```python
def find_mode(series):
    return series.mode().iloc[0] if not series.mode().empty else None
```

### HOMEWORK HACK

The questions for the hack were related to your project, and there was little to no way to implement those questions on my dataset for biotech trivia.

``` python

# Load Data

datas = pd.read_csv('firepredictions.csv')

# Find fire incidents with the highest and lowest overall average temperature

highest = datas.loc[datas['Temperature'].idxmax()]
lowest = datas.loc[datas['Temperature'].idxmin()]

# Calculate the temperature range (max - min) per incident

datas['Temp_Diff'] = datas['Max_Temp'] - datas['Min_Temp']

# Incidents where temperature exceeded the average

temp_avg = datas['Temperature'].mean()
above_avg = datas[datas['Temperature'] > temp_avg]

# Group by vegetation type and weather, calculate mean temp and wind

grouped = datas.groupby(['Vegetation_Type', 'Weather_Condition'])[['Temperature', 'Wind_Speed']].mean().reset_index()

# Convert vegetation type to numeric codes for correlation

encoded = datas.copy()
encoded['Vegetation_Type_Code'] = encoded['Vegetation_Type'].astype('category').cat.codes
correlation = encoded[['Vegetation_Type_Code', 'Fire_Intensity']].corr().iloc[0,1]

sns.barplot(x='Vegetation_Type', y='Fire_Intensity', data=datas)
plt.xticks(rotation=45)
plt.title('Fire Intensity by Vegetation Type')
plt.tight_layout()
plt.show()

# Weather condition with highest fire intensity

weather_intensity = datas.groupby('Weather_Condition')['Fire_Intensity'].mean()
highest_intensity = weather_intensity.idxmax()

# % of incidents with temp > 100F

above_100 = datas[datas['Temperature'] > 100]
percent_above = (len(above_100) / len(datas)) * 100

# Create SQLite Database

conn = sqlite3.connect("fire_data.db")
datas.to_sql("fire_incidents", conn, if_exists='replace', index=False)

# SQL Queries

query1 = """
SELECT Vegetation_Type, AVG(Temperature) as Avg_Temp, AVG(Wind_Speed) as Avg_Wind
FROM fire_incidents
GROUP BY Vegetation_Type
"""

query2 = """
SELECT * FROM fire_incidents
WHERE Temperature > 120 AND Wind_Speed > 15
"""

query3 = """
SELECT Weather_Condition, AVG(Fire_Intensity) as Avg_Intensity
FROM fire_incidents
GROUP BY Weather_Condition
"""

# Execute SQL queries
avg_temp_wind_by_veg = pd.read_sql(query1, conn)
high_temp_wind_incidents = pd.read_sql(query2, conn)
intensity_by_weather_sql = pd.read_sql(query3, conn)

conn.close()
```

SQL is ideal for handling large, structured datasets stored in databases, offering efficient performance for querying, aggregating, and joining tables, and scenarios with data persistence, such as in enterprise applications or when working with relational databases. On the other hand, Pandas is better in flexibility, ease of use, and for exploratory data analysis, quick iterations, and complex data transformations, especially in research or development environments.
