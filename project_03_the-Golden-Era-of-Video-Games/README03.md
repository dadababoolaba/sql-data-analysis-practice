# Practice project: When Was the Golden Era of Video Games?
Practice date: 03-jan-2026

## Project Overview
Video games are big business: the global gaming market is projected to be worth more than $300 billion by 2027 according to Mordor Intelligence. With so much money at stake, the major game publishers are hugely incentivized to create the next big hit. But are games getting better, or has the golden age of video games already passed?

## Dataset
- Source: DataCamp practice project (originally from Kaggle)
- Tables:
  - game_sales
  - reviews
  - users_avg_year_rating
  - critics_avg_year_rating

## Analysis Objectives
- Identify the ten best-selling video games
- Determine the top ten years based on average critic scores
- Identify the years where critics and users broadly agreed that the games released were highly rated

## SQL Used
-  INNER JOIN
-  WHERE
-  GROUP BY
-  HAVING
-  ORDER BY
-  Aggregate functions (COUNT, AVG)

## Core Analysis
### best_selling_games
Find the ten best-selling games. The output should contain all the columns in the `game_sales` table and be sorted by the `games_sold` column in descending order. Save the output as `best_selling_games`.
```sql
-- best_selling_games
SELECT *
FROM game_sales
ORDER BY games_sold DESC
LIMIT 10;
```
### critics_top_ten_years
Find the ten years with the highest average critic score, where at least four games were released (to ensure a good sample size). Return an output with the columns `year`, `num_games` released, and `avg_critic_score`. The `avg_critic_score` should be rounded to 2 decimal places. The table should be ordered by `avg_critic_score` in descending order. Save the output as `critics_top_ten_years`. Do not use the `critics_avg_year_rating` table provided; this has been provided for your third query.
```sql
-- critics_top_ten_years
SELECT g.year, 
	COUNT(DISTINCT name) AS num_games, 
	ROUND(AVG(r.critic_score),2) AS avg_critic_score
FROM game_sales AS g
INNER JOIN reviews AS r
USING(name)
GROUP BY g.year
HAVING COUNT(DISTINCT name)>=4
ORDER BY avg_critic_score DESC
LIMIT 10;
```
### golden_years
Find the years where critics and users broadly agreed that the games released were highly rated. Specifically, return the years where the average critic score was over 9 OR the average user score was over 9. The pre-computed average critic and user scores per year are stored in `users_avg_year_rating` and `critics_avg_year_rating` tables respectively. The query should return the following columns: `year`, `num_games`, `avg_critic_score`, `avg_user_score`, and `diff`. The `diff` column should be the difference between the `avg_critic_score` and `avg_user_score`. The table should be ordered by the year in ascending order, save this as a DataFrame named golden_years.
```sql
-- golden_years
SELECT g.year, 
	COUNT(DISTINCT name) AS num_games, 
	c.avg_critic_score,
	u.avg_user_score,
	((c.avg_critic_score)-(u.avg_user_score)) AS diff
FROM game_sales AS g
INNER JOIN critics_avg_year_rating AS c
USING(year)
INNER JOIN 	users_avg_year_rating AS u
USING(year)
WHERE c.avg_critic_score > 9 OR 
	u.avg_user_score > 9
GROUP BY g.year,
	c.avg_critic_score,
	u.avg_user_score
ORDER BY g.year;
```

### Key Insights
- Years with fewer releases can distort average ratings, so a minimum game threshold is necessary
- High critic scores do not always align perfectly with user scores, highlighting differences in evaluation perspectives

### Learning Notes
- Use `HAVING` instead of `WHERE` when filtering aggregated results
- All non-aggregated columns in the `SELECT` clause must be included in `GROUP BY`

### Next Steps
- practice more to get used to all the function
- start learning python

