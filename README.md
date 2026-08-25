# COVID-19-Canadian-Census-Tableau-Analysis

# Overview
This project successfully integrated two independent public datasets — the Rami Krispin COVID-19 tidy dataset and the Statistics Canada Census Profile — to explore the relationship between COVID-19 mortality and household demographic patterns across Canadian provinces and territories. Using R exclusively for data extraction and Tableau Desktop for all cleaning, transformation, joining, and visualization, three distinct and purposeful dashboards were built to answer analytical questions that spanned both datasets.

# Datasets
Dataset 1 — COVID-19 (Rami Krispin, GitHub)
The coronavirus tidy dataset provides daily case counts for countries and provinces worldwide. Fields used: cases, country, date, province, type...

Extraction method: R was used exclusively to retrieve and filter the dataset to Canada, then export it as a CSV using write.csv().

# R extraction script
library(tidyverse)

covid_raw <- read.csv("https://raw.githubusercontent.com/RamiKrispin/coronavirus/master/csv/coronavirus.csv")

canada_covid <- covid_raw %>%
  filter(country == "Canada")

write.csv(canada_covid, "canada_covid19.csv", row.names = FALSE)

Dataset 2 — Statistics Canada Census Profile (2016/2021)
Census Profile data at the province and territory level, downloaded from Statistics Canada. The raw English CSV is not in tidy format — parameters were unpivoted and transformed into usable columns within Tableau before analysis.

# Methodology
Step 1 — Data Extraction (R)
R Studio was used solely to retrieve the COVID-19 dataset from GitHub and export a Canada-filtered CSV. No transformations or analysis were performed in R.

Step 2 — Data Cleaning & Transformation (Tableau)
Three separate data connections were created in Tableau Desktop to minimize errors:

Connection 1: Cleaned COVID-19 dataset → used for Viz 1
Connection 2: Cleaned Census dataset → used for Viz 2
Connection 3: Joined COVID + Census dataset → used for Viz 3
Cleaning steps applied in Tableau:

Removed outliers from the COVID dataset
Filtered to Canadian provinces and territories only
Unpivoted household size columns in the Census dataset (1 Person, 2 Persons, 3 Persons, 4 Persons, 5+ Persons) to create a usable structure
Created calculated fields for aggregations and cross-dataset metrics

Step 3 — Joining Datasets (Tableau)
The COVID and Census datasets were joined using Province as the shared key. A new calculated field — Death per 1-Person Household — was created to enable the cross-dataset analysis in Viz 3.

# Visualizations
Viz 1 — Number of COVID Deaths in Canadian Provinces
Chart type: Treemap
Dataset: COVID-19 (deaths only)
Question: Which Canadian provinces recorded the highest number of COVID-19 deaths?

Variables used:

Province
Sum of Deaths (aggregated)
Key insight: Ontario recorded the highest total COVID-19 deaths (5,664), followed by Quebec (3,368) and Alberta (2,264). Smaller territories such as Nunavut, Yukon, and the Northwest Territories reported significantly fewer deaths, reflecting both smaller populations and geographic isolation.

<img width="1434" height="840" alt="viz1_covid_deaths_treemap" src="https://github.com/user-attachments/assets/49a7e21e-ef24-417f-9eb2-3300baa47eae" />




Viz 2 — Number of Families in Private Households Across Canadian Provinces
Chart type: Grouped Bar Chart
Dataset: Statistics Canada Census Profile
Question: How are families distributed by household size across Canadian provinces and territories?

Variables used:

Province
Household size categories: 1 Person, 2 Persons, 3 Persons, 4 Persons, 5+ Persons
Key insight: Ontario and Quebec lead in total private household counts across all household sizes. Larger multi-person households (5+ persons) are more prevalent in Ontario and British Columbia, while smaller provinces show proportionally more 1- and 2-person households, reflecting both population size and demographic composition.


<img width="1508" height="841" alt="viz2_household_families_bar" src="https://github.com/user-attachments/assets/eae39470-cc7f-4004-9789-7de8f09feeb7" />




Viz 3 — COVID-19 Death Rate as a Percentage of 1-Person Households Across Canadian Provinces
Chart type: Bubble / Scatter Chart
Dataset: Joined COVID-19 + Statistics Canada Census
Question: Is there a relationship between COVID-19 death totals and the proportion of 1-person households across Canadian provinces?

Variables used:

Province (color)
Sum of Deaths (x-axis)
Death per 1-Person Household % (y-axis) — new calculated field
Bubble size scaled to Death per 1-Person Household %
Calculated field:

Death per 1-Person % = SUM([Death]) / SUM([1 Person]) * 100
Key insight: Provinces with high absolute death counts, such as Ontario, do not necessarily have the highest death-per-1-person-household ratio, suggesting that household density and living arrangements interact with COVID outcomes in complex ways. Smaller provinces with fewer single-person households show disproportionately high ratios.


<img width="1004" height="895" alt="viz3_death_rate_bubble" src="https://github.com/user-attachments/assets/23e58629-7698-4e9f-bed8-d6f143f1e3bb" />



# About
This project was completed as part of a post-graduate Data Analytics Certificate program. It demonstrates end-to-end data analytics skills including data extraction (R), ETL and data wrangling (Tableau), multi-dataset joining, calculated field creation, and storytelling through visualization.

Skills showcased: R · Tableau · Data Cleaning · ETL · Data Joining · Calculated Fields · Statistical Aggregation · Data Visualization

# Conclusion
This project demonstrated core competencies in end-to-end data analytics: extracting raw data programmatically, cleaning and transforming messy real-world datasets, joining data from disparate sources, creating meaningful calculated metrics, and communicating findings through clear and varied visualizations. The three-visualization structure — moving from single-dataset exploration to a cross-dataset integrated analysis — reflects a deliberate analytical progression that mirrors professional data analysis workflows.

The findings reinforce that effective data storytelling requires both technical execution and interpretive judgment. Numbers alone do not tell a story; the analyst's job is to ask the right questions, build the right metrics, and present findings in a way that is honest, clear, and actionable.
