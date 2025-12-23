# Industry Carbon Footprint Analysis (SQL)

## Project Overview
This project analyzes the total product carbon footprint (PCF)
across different industry groups using SQL.

The analysis focuses on the most recent year available in the dataset
and summarizes both the number of unique companies and the total
industry-level carbon footprint.

## Dataset
- Source: DataCamp practice dataset
- Table: product_emissions

## Analysis Objectives
- Identify the most recent year in the dataset
- Count unique companies in each industry group
- Calculate total carbon footprint by industry
- Rank industries by total carbon footprint

## Key SQL Concepts Used
- SELECT, WHERE
- GROUP BY, ORDER BY
- COUNT(DISTINCT)
- SUM, ROUND
- Subquery to dynamically filter the most recent year

## Core Query
```sql
SELECT
  industry_group,
  COUNT(DISTINCT company) AS num_companies,
  ROUND(SUM(carbon_footprint_pcf), 1) AS total_industry_footprint
FROM product_emissions
WHERE year = (SELECT MAX(year) FROM product_emissions)
GROUP BY industry_group
ORDER BY total_industry_footprint DESC;
```
## Key Insight
- Industry groups differ significantly in total carbon footprint
- Using a subquery ensures the analysis always reflects the most recent data
