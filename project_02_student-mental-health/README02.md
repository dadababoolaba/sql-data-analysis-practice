# Student Mental Health Analysis (SQL)

## Project Overview
This project analyzes the mental health status of international students
using SQL aggregation functions.

## Dataset
- Source: DataCamp practice dataset
- Table used: students

## Analysis Objectives
- Compare average PHQ scores across different stay durations
- Understand sample size distribution

## Key SQL Skills Used
- SELECT, WHERE
- GROUP BY
- ORDER BY
- COUNT, AVG

## Example Query
```sql
SELECT
  stay,
  COUNT(*) AS num_students,
  ROUND(AVG(todep),2) AS avg_phq
FROM students
WHERE inter_dom = 'Inter'
GROUP BY stay
ORDER BY avg_phq DESC;
```
## Key Insight
- Students with longer stay duration show different average PHQ scores
- Sample size varies significantly across groups
