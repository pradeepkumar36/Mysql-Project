# Movie and TV Show Data Exploration 

### Objective:

To explore and analyze Netflix's movie and TV show catalog using SQL, identifying patterns in content type, countries, release trends, ratings, durations, genres, and more.

### Tools Used:

Database: MySQL

#### Dataset:
Netflix titles (manually created table from provided data)

### Key Analysis & Insights:

use netflix;
select database ();

DROP TABLE IF EXISTS netflix;
CREATE TABLE Netflix
(
    show_id      VARCHAR(5),
    type         VARCHAR(10),
    title        VARCHAR(250),
    director     VARCHAR(550),
    casts        VARCHAR(1050),
    country      VARCHAR(550),
    date_added   VARCHAR(55),
    release_year INT,
    rating       VARCHAR(15),
    duration     VARCHAR(15),
    listed_in    VARCHAR(250),
    description  VARCHAR(550)
);

select * from netflix;

-- # 1. Total Number of Movies and TV Shows

SELECT type,
 COUNT(*) AS total_count
 FROM netflix
 GROUP BY type;

---------------------------------------------------
-- #2. Top 10 Countries with the Most Content

SELECT country, COUNT(*) AS total_content 
FROM netflix
GROUP BY country
ORDER BY total_content DESC LIMIT 10;
 
------------------------------------------------------------------------------ 
 -- # 3. Content Added Over the Years  
 
 SELECT YEAR(STR_TO_DATE(date_added, '%M %d, %Y')) AS year_added, COUNT(*) AS total_added
 FROM netflix
 GROUP BY year_added 
 ORDER BY year_added;

-------------------------------------------------------------
-- # 4. Most Common Ratings

SELECT rating, COUNT(*) AS total 
FROM netflix 
GROUP BY rating 
ORDER BY total DESC;

----------------------------------------------------

-- #  5. Top 10 Directors by Number of Shows

 SELECT director, COUNT(*) AS total_shows 
 FROM netflix 
 WHERE director IS NOT NULL
 GROUP BY director 
 ORDER BY total_shows DESC LIMIT 10;
 
 ------------------------------------------------------------
 
 -- # 6. Show Details for a Specific Country
 
 SELECT * FROM netflix WHERE country = 'India';
 
 --------------------------------------------------------------------
 
 --# 7. Movies with Duration Over 100 Minutes

SELECT title, duration 
FROM netflix 
WHERE type = 'Movie' AND
 CAST(SUBSTRING_INDEX(duration, ' ', 1) AS UNSIGNED) > 100;

-------------------------------------------------------------------------------
-- # 8. Number of TV Shows Per Genre

 SELECT listed_in, COUNT(*) AS show_count 
 FROM netflix 
 WHERE type = 'TV Show' 
 GROUP BY listed_in 
 ORDER BY show_count DESC;
 
 ---------------------------------------------------------------------------------
 -- # 9. Find All Shows Released Before 2000
 
 SELECT title, release_year 
 FROM netflix
 WHERE release_year < 2000
 ORDER BY release_year;
 
 -----------------------------------------------------------------------------------
 -- # 10. Latest Added Shows
 
 SELECT title, date_added 
 FROM netflix 
 ORDER BY STR_TO_DATE(date_added, '%M %d, %Y')
 DESC LIMIT 5;
 
 --------------------------------------------------------------------------
 -- # 11. Find Movies/Shows with "Love" in the Title
 
 SELECT title 
 FROM netflix 
 WHERE title LIKE '%Love%';
 
 -- --------------------------------------------------------------------------------------
 
 -- # 12. Average Duration of Movies
 
 SELECT AVG(CAST(SUBSTRING_INDEX(duration, ' ', 1) AS UNSIGNED)) AS average_movie_duration
 FROM netflix 
 WHERE type = 'Movie';
 
 ------------------------------------------------------------------------------------

 -- # 13. Movies/Shows Without Directors
 
 SELECT title, type 
 FROM netflix
 WHERE director IS NULL;
 
 ---------------------------------------------------------------------------

-- # 14. Longest Duration Movie

 SELECT title, duration 
 FROM netflix 
 WHERE type = 'Movie' 
 ORDER BY CAST(SUBSTRING_INDEX(duration, ' ', 1) AS UNSIGNED) DESC LIMIT 1;

-- ---------------------------------------------------------------------------

-- # 15 Top 5 Countries Producing TV Shows

SELECT country, COUNT(*) AS total_tv_shows 
FROM netflix 
WHERE type = 'TV Show' 
GROUP BY country 
ORDER BY total_tv_shows DESC LIMIT 5;


## Key SQL Techniques Demonstrated:

Use of aggregate functions: COUNT(), AVG()

Date parsing with STR_TO_DATE(), YEAR()

Text manipulation using LIKE, SUBSTRING_INDEX(), CAST()

Filtering with WHERE, handling nulls

Sorting and limiting results using ORDER BY and LIMIT

### Conclusion:

This project showcases a strong foundational ability to explore, clean, and analyze entertainment datasets using SQL. It provides valuable insights into Netflix’s content catalog, viewing trends, and metadata distribution—skills that are essential for any aspiring data analyst.



