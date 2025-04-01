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

-- 1. Check if the table is working
SELECT * FROM NY_HOUSES2 LIMIT 10;
-- Screenshot: ./images/check_if_the_table_works.png

-- 2. Change column type of Last_review from VARCHAR to DATE
ALTER TABLE NY_HOUSES2 MODIFY Last_review DATE;

-- 3. Number of rows
SELECT COUNT(*) FROM NY_HOUSES2;
-- Screenshot: ./images/raw_count.png

-- 4. Number of NULL values in Last_review column
SELECT COUNT(*) FROM NY_HOUSES2 WHERE Last_review IS NULL;

-- 5. Date of the most recent review
SELECT Last_review AS 'The most recent review'
FROM NY_HOUSES2
ORDER BY Last_review DESC 
LIMIT 1;
-- Screenshot: ./images/The_most_recent_review.png

-- 6. Most expensive listing
SELECT Price AS 'The most expensive listing'
FROM NY_HOUSES2 
ORDER BY Price DESC
LIMIT 1;
-- Screenshot: ./images/The_most_expensive_listing.png

-- 7. Cheapest listing (excluding free/invalid ones)
SELECT Price AS 'The cheapest listing'
FROM NY_HOUSES2 
WHERE Price != 0
ORDER BY Price ASC
LIMIT 1;
-- Screenshot: ./images/the_cheapest_lesting.png

-- 8. Disable safe update mode (to allow updates)
SHOW INDEX FROM NY_HOUSES2;
SET SQL_SAFE_UPDATES = 0;

-- 9. Change listing title from 'ENJOY Downtown NYC!' to 'Downtown NYC!'
UPDATE NY_HOUSES2
SET TITLE = 'Downtown NYC!'
WHERE ID = 12192;

-- 10. Confirm the change was successful
SELECT Title FROM NY_HOUSES2 
WHERE ID = 12192;
-- Screenshot: ./images/Title_Downtown_NYC.png

-- 11. Delete listing with ID = 2595
DELETE FROM NY_HOUSES2
WHERE ID = 2595;

-- 12. Listings marked as 'Manhattan' or 'Other'
SELECT TITLE,
    CASE
        WHEN Neighbourhood_group = 'Manhattan' THEN 'Manhattan'
        ELSE 'Other'
    END AS Mark
FROM NY_HOUSES2;
-- Screenshot: ./images/Listings_in_Manhattan_or_other.png

-- 13. Borough-level stats: total listings, average price, and availability
SELECT 
    neighbourhood_group, 
    COUNT(id) AS total_listings, 
    ROUND(AVG(price)) AS avg_price, 
    ROUND(AVG(availability_365)) AS avg_availability
FROM NY_HOUSES2
GROUP BY neighbourhood_group
ORDER BY total_listings DESC;
-- Screenshot: ./images/total_number_of_listings.png

