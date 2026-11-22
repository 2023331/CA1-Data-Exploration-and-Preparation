# Exploratory Data Analysis and Principal Component Analysis of Household Electricity Consumption Patterns
 
**Author:** Mary Karanja- 2023331
**Language:** R (R Markdown)
**Output:** HTML report
 
## Overview
 
This project analyses minute-level electricity measurements from a single household. It uses exploratory data analysis (EDA) to study how consumption varies over time and how the electrical variables relate to each other. It then applies Principal Component Analysis (PCA) to see whether the seven measurement variables can be summarised with fewer dimensions.
 
**Main research question:** How do household electricity consumption patterns vary over time, and which electrical measurements contribute most to the variation in household energy consumption?
 
## Dataset
 
- **Name:** Individual Household Electric Power Consumption
- **Source:** UCI Machine Learning Repository (Hebrail and Berard, 2012)
- **DOI:** https://doi.org/10.24432/C58K54
- **Coverage:** one house, one reading per minute, December 2006 to November 2010
- **Format:** semicolon-separated text file, with missing numeric values written as `?`
- **Variables:** Date, Time, Global_active_power, Global_reactive_power, Voltage, Global_intensity, Sub_metering_1, Sub_metering_2, Sub_metering_3
The data file is **not included** in this submission because of its size (about 2 million rows). Download it from the link above.
 
## Files
 
| File | Description |
|---|---|
| `Household_electricity.Rmd` | Full analysis: code, commentary and interpretation) |
| `Household_electricity.html` | Knitted report with all outputs and plots |
| `README.md` | This file |
| `household_power_consumption.txt` | Dataset |
| `Household_electricity.pptx`  | Poster | 
 
## How to run
 
1. Download the dataset zip from the UCI repository and unzip it.
2. Place `Household_power_consumption.txt` in the same folder as the `.Rmd` file. Alternatively, edit the `data_path` line in the `read-data` chunk to point to its location.
3. Install the required packages (see below).
4. Open the `.Rmd` in RStudio and click **Knit**, or run:
```r
rmarkdown::render("household_power_analysis.Rmd")
```
 
Knitting reads about 2 million rows and may take a few minutes. Plots that are slow on the full data use a fixed random sample (`set.seed(123)`), so results are reproducible.
 
## Required packages
 
```r
install.packages(c("tidyverse", "lubridate", "corrplot",
                   "factoextra", "knitr", "rmarkdown"))
```
 
## Structure of the analysis
 
| Section | Content |
|---|---|
| 1 to 3 | Problem domain, research questions, dataset description |
| 4 to 8 | Initial exploration, cleaning, missing values, duplicates, data types, outliers |
| 9 to 11 | Distributions, descriptive statistics, hourly, weekday and monthly patterns |
| 12 | Correlation and covariation analysis |
| 13 | Unusual patterns: high-reading hours and unusual days |
| 14 | Categorical variable creation (`Time_Period`) and one-hot encoding |
| 15 | Standardisation of the continuous variables |
| 16 to 18 | PCA, scree plot, cumulative variance, loadings, contributions and scores |
| 19 to 21 | Discussion, conclusion, limitations |
| 22 | Harvard-style references |
 
## Key methodological choices
 
- **Missing values:** rows with missing measurements are removed rather than imputed, so no readings are created that were never recorded and the daily pattern is not flattened.
- **Outliers:** kept in the data, because high readings are likely to be real appliance use. Their effect on PCA is discussed in the limitations.
- **Standardisation:** all variables are scaled to mean 0 and standard deviation 1 before PCA, so that variables with large scales (such as Voltage) do not dominate.
- **Encoding:** `Time_Period` (Morning, Afternoon, Evening, Night) is one-hot encoded because it is a nominal variable. The encoded columns are not used in the PCA, which uses only the seven continuous measurements. The time period is used afterwards to help interpret the component scores.
## Limitations
 
- Data comes from one household, so results describe this home only.
- About four years of data makes long-term trends hard to separate from unusual years.
- Minute-level readings are not independent, so tests assuming independence are not appropriate.
- The sub-meters do not cover all appliances.
- PCA finds only linear patterns and is sensitive to extreme values.
## References
 
Hebrail, G. and Berard, A. (2012) *Individual household electric power consumption*. UCI Machine Learning Repository. Available at: https://doi.org/10.24432/C58K54
 
 
