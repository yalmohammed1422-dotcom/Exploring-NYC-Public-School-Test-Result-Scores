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

Install dependencies:
```bash
pip install pandas matplotlib
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
- Distribution of math scores for qualifying schools (histogram)

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
- Component breakdown for top 3 schools (grouped bar chart)

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
- Standard deviation by borough (bar chart with highlighted max)
- Number of schools by borough (bar chart with counts)
- Comprehensive 4-panel comparison (average, std dev, count, scatter plot)

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

## Usage

1. Load your NYC schools dataset:
```python
import pandas as pd
import matplotlib.pyplot as plt

# Load your data
schools = pd.read_csv('nyc_schools_sat_data.csv')

# Run the analysis script
# [Run the analysis code]
```

2. View the automatically generated visualizations

3. Access key findings:
   - Best math schools list
   - Top 10 overall schools
   - Borough with highest variability

## Key Insights

The analysis reveals:
- **Math Excellence**: Schools meeting the 640+ threshold represent top-tier math programs
- **Overall Performance**: Total SAT scores identify comprehensively strong schools
- **Borough Variability**: Standard deviation highlights inequality within boroughs
- **Resource Distribution**: School counts show concentration of educational institutions

## Code Improvements Implemented

Compared to the original code, this version includes:
- ✅ **Enhanced visualizations**: 8 different charts for comprehensive analysis
- ✅ **Better sorting**: Proper sorting for standard deviation analysis
- ✅ **Clear labeling**: All charts include value labels and legends
- ✅ **Print statements**: Clear console output for key findings
- ✅ **Color coding**: Consistent color scheme for easy interpretation
- ✅ **Grid lines**: Improved readability with subtle gridlines

## Potential Further Analysis

- Compare performance trends over multiple years
- Analyze correlation between school size and performance
- Investigate relationship between borough funding and SAT scores
- Examine subject-specific strengths across boroughs
- Create predictive models for school performance

## Alternative Implementation

For more efficient borough aggregation:
```python
# Direct aggregation instead of transform
borough_summary = schools.groupby('borough').agg({
    'total_SAT': ['mean', 'std', 'count']
}).round(2)
```

## File Structure

```
project/
│
├── sat_analysis_matplotlib.py    # Main analysis script with visualizations
├── README.md                      # This file
└── nyc_schools_sat_data.csv      # Your dataset (not included)
```

## Contributing

Feel free to fork this project and submit pull requests for:
- Additional visualizations
- New statistical analyses
- Performance optimizations
- Enhanced documentation

## License

This project is open source and available under the MIT License.

## Author

NYC Schools SAT Analysis Project

---

*Analysis of NYC public school SAT performance data for educational insights and planning.*

## Sample Output

```
Number of schools with average math score >= 640: XX

Top 10 Schools by Total SAT Score:
                    school_name  total_SAT
0                School Name 1       2400
1                School Name 2       2350
...

Borough with Largest Standard Deviation:
        borough  num_schools  average_SAT  std_SAT
XX   Borough Name          YY      1234.56   123.45
```
