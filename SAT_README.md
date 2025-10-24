# NYC Schools SAT Performance Analysis

A comprehensive data analysis project exploring SAT performance across New York City schools, focusing on math excellence, top-performing schools, and borough-level comparisons.

## Overview

This project analyzes NYC school SAT data to answer three key questions:
1. Which schools excel in math with scores of 640 or higher?
2. What are the top 10 schools based on total SAT scores?
3. Which NYC borough has the largest variability (standard deviation) in SAT performance?

## Features

- **Math Excellence Analysis**: Identifies and ranks schools with high math performance (≥640)
- **Total SAT Rankings**: Determines top-performing schools across all SAT sections
- **Borough Comparison**: Analyzes performance variability and trends across NYC boroughs
- **Statistical Insights**: Calculates means, standard deviations, and school counts by borough
- **Comprehensive Visualizations**: 8 different charts to explore the data from multiple angles

## Requirements

```python
pandas
matplotlib
```

## Dataset

The analysis expects a DataFrame named `schools` with the following columns:
- `school_name`: Name of the school
- `average_math`: Average math SAT score
- `average_reading`: Average reading SAT score
- `average_writing`: Average writing SAT score
- `borough`: NYC borough location (Manhattan, Brooklyn, Queens, Bronx, Staten Island)

## Analysis Breakdown

### Analysis 1: Best Math Results (≥640)

**Objective**: Identify schools excelling in mathematics

```python
# Filter schools with math scores >= 640
best_math_results = schools[schools["average_math"] >= 640]

# Sort from highest to lowest
best_math_schools = best_math_results.sort_values("average_math", ascending=False)

# Select relevant columns
best_math_schools = best_math_schools[["school_name", "average_math"]]
```

**Visualizations**:
- Top 10 schools by math score (horizontal bar chart)
<img width="2774" height="1579" alt="image" src="https://github.com/user-attachments/assets/83fa8028-96e3-43a7-b513-31a58e00ccf0" />

- Distribution of math scores for qualifying schools (histogram)
<img width="2381" height="1178" alt="image" src="https://github.com/user-attachments/assets/b58f462a-f307-429f-8895-f58d691138c1" />


### Analysis 2: Top 10 Schools by Total SAT Score

**Objective**: Identify overall top-performing schools

```python
# Calculate total SAT score
schools["total_SAT"] = schools["average_math"] + schools["average_reading"] + schools["average_writing"]

# Sort and get top 10
schools_SAT_sorted = schools.sort_values("total_SAT", ascending=False)
top_10_schools = schools_SAT_sorted.head(10)[["school_name", "total_SAT"]]
```

**Visualizations**:
- Top 10 schools by total SAT (horizontal bar chart with scores)
<img width="2774" height="1579" alt="image" src="https://github.com/user-attachments/assets/e468a948-a943-4a9e-ac20-5aba9f0ebdf0" />

- Component breakdown for top 3 schools (grouped bar chart)
<img width="2382" height="1380" alt="image" src="https://github.com/user-attachments/assets/bec0b51d-0332-4132-8803-2f65f451adb3" />

### Analysis 3: Borough with Largest Variability

**Objective**: Identify which borough has the most inconsistent SAT performance

```python
# Calculate borough statistics
schools["average_SAT"] = schools.groupby("borough")["total_SAT"].transform("mean")
schools["std_SAT"] = schools.groupby("borough")["total_SAT"].transform("std")
schools["num_schools"] = schools.groupby("borough")["school_name"].transform("count")

# Find borough with largest standard deviation
borough_stats = schools[["borough", "num_schools", "average_SAT", "std_SAT"]].drop_duplicates()
largest_std_dev = borough_stats.sort_values("std_SAT", ascending=False).head(1)
```

**Visualizations**:
- Average SAT scores by borough (bar chart)
<img width="2382" height="1178" alt="image" src="https://github.com/user-attachments/assets/dfa57863-3aa6-4027-a09a-198d79639ba3" />

- Standard deviation by borough (bar chart with highlighted max)
<img width="2381" height="1179" alt="image" src="https://github.com/user-attachments/assets/9dc11f23-b6ad-454d-8d95-2243a0d099b6" />

- Number of schools by borough (bar chart with counts)
<img width="2382" height="1180" alt="image" src="https://github.com/user-attachments/assets/7934cec2-ab66-4e15-8920-488aa8a5fb56" />

- Comprehensive 4-panel comparison (average, std dev, count, scatter plot)
<img width="2970" height="2359" alt="image" src="https://github.com/user-attachments/assets/2a721ff2-def9-4f79-8bce-b7b4b706cd17" />

## Visualizations Summary

The project includes **8 matplotlib visualizations**:

1. **Top 10 Math Schools** - Horizontal bar chart showing best math performers
2. **Math Score Distribution** - Histogram of schools scoring 640+
3. **Top 10 Total SAT** - Horizontal bar chart with score labels
4. **Top 3 Score Breakdown** - Grouped bars showing Math/Reading/Writing components
5. **Average SAT by Borough** - Bar chart comparing borough averages
6. **Standard Deviation by Borough** - Highlights variability across boroughs
7. **School Count by Borough** - Shows distribution of schools
8. **Comprehensive Borough Dashboard** - 4-panel comparison of all metrics


## Key Insights

The analysis reveals:
- **Math Excellence**: Schools meeting the 640+ threshold represent top-tier math programs
- **Overall Performance**: Total SAT scores identify comprehensively strong schools
- **Borough Variability**: Standard deviation highlights inequality within boroughs
- **Resource Distribution**: School counts show concentration of educational institutions

## Author

Yousef Almohammed - NYC Schools SAT Analysis Project

*Analysis of NYC public school SAT performance data for educational insights and planning.*

