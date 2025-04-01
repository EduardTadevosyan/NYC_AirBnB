# 🗽 Airbnb NYC 2019 - SQL & Power BI Project

This project is a SQL and Power BI analysis of the Airbnb NYC 2019 dataset. I chose this dataset because I love New York City, and I wanted to practice SQL and Power BI together while uncovering interesting insights about the city’s rental landscape.

---

## 📌 Project Objectives

- Practice SQL querying, data cleaning, and data transformation
- Use Power BI to visualize the results and create an interactive dashboard
- Explore rental pricing, availability, host behavior, and neighborhood trends

---

## 🛠️ Tools Used

- MySQL (local instance)
- Power BI
- CSV Data: [Inside Airbnb - NYC 2019](http://insideairbnb.com/get-the-data.html)
- MySQL Workbench

---

## 🧠 SQL Operations Performed

```sql
-- Check if the table is working
SELECT * FROM NY_HOUSES2 LIMIT 10;

-- Change column type of Last_review from VARCHAR to DATE
ALTER TABLE NY_HOUSES2 MODIFY Last_review DATE;

-- Number of rows
SELECT COUNT(*) FROM NY_HOUSES2;

-- Number of NULL values in Last_review column
SELECT COUNT(*) FROM NY_HOUSES2 WHERE Last_review IS NULL;

-- Date of the most recent review
SELECT * FROM NY_HOUSES2
ORDER BY Last_review DESC 
LIMIT 1;

-- Most expensive listing
SELECT * FROM NY_HOUSES2 
ORDER BY Price DESC
LIMIT 1;

-- Cheapest listing
SELECT * FROM NY_HOUSES2 
WHERE Price != 0
ORDER BY Price ASC;

-- Disable safe update mode (to allow updates)
SHOW INDEX FROM NY_HOUSES2;
SET SQL_SAFE_UPDATES = 0;

-- Change title from 'ENJOY Downtown NYC!' to 'Downtown NYC!'
UPDATE NY_HOUSES2
SET TITLE = 'Downtown NYC!'
WHERE ID = 12192;

-- Check if the change was successful
SELECT * FROM NY_HOUSES2 
WHERE ID = 12192;

-- Delete a row
DELETE FROM NY_HOUSES2
WHERE ID = 2595;

-- Listings in Manhattan
SELECT TITLE,
    CASE
        WHEN Neighbourhood_group = 'Manhattan'
        THEN 'Manhattan'
        WHEN Neighbourhood_group != 'Manhattan'
        THEN 'Other'
    END AS Mark
FROM NY_HOUSES2;

-- Total number of listings + average price and average yearly availability grouped by neighborhood
SELECT 
    neighbourhood_group, 
    COUNT(id) AS total_listings, 
    ROUND(AVG(price)) AS avg_price, 
    ROUND(AVG(availability_365)) AS avg_availability
FROM NY_HOUSES2
GROUP BY neighbourhood_group
ORDER BY total_listings DESC;
