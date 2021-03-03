
# SQL:  Structured Query Language  Exercise

### Getting Started
1. Go to BigQuery UI https://console.cloud.google.com/bigquery
2. Add in the public data sets. 
	3. Click the Add Data icon
	4. Add any dataset
	5. `bigquery-public-data` should become visible and populate in the BigQuery UI. 
3. Add your queries where it says [YOUR QUERY HERE].
4. Make sure you add your query in between the triple tick marks. 
---

For this section of the exercise we will be using the `bigquery-public-data.austin_311.311_service_requests`  table. 

5. Write a query that tells us how many rows are in the table. 
	```
	SELECT COUNT(*) 
	FROM `bigquery-public-data.austin_311.311_service_requests`; 
	```

7. Write a query that tells us how many _distinct_ values there are in the complaint_description column.
	``` 
	#If we only need the count
	SELECT COUNT(DISTINCT(complaint_description)) 
	FROM `bigquery-public-data.austin_311.311_service_requests`;

	#If we need the list of distinct values
	SELECT DISTINCT(complaint_description)
	FROM `bigquery-public-data.austin_311.311_service_requests`; 
	```
  
8. Write a query that counts how many times each owning_department appears in the table and orders them from highest to lowest. 
	``` 
	SELECT owning_department, COUNT(owning_department) AS owning_count
	FROM `bigquery-public-data.austin_311.311_service_requests`
	GROUP BY owning_department
	ORDER BY COUNT(owning_department) DESC;
	```

9. Write a query that lists the top 5 complaint_description that appear most and the amount of times they appear in this table. (hint... limit)
	```
	SELECT complaint_description, COUNT(complaint_description) AS complaint_count
	FROM `bigquery-public-data.austin_311.311_service_requests`
	GROUP BY complaint_description
	ORDER BY COUNT(complaint_description) DESC
	limit 5;
	  ```
10. Write a query that lists and counts all the complaint_description, just for the where the owning_department is 'Animal Services Office'.
	```
	SELECT complaint_description, COUNT(complaint_description) AS complaint_count
    	FROM `bigquery-public-data.austin_311.311_service_requests`
    	WHERE owning_department = 'Animal Services Office'
    	GROUP BY complaint_description;
		
	### Answer check
	SELECT COUNT(owning_department)
    	FROM `bigquery-public-data.austin_311.311_service_requests`
   	WHERE owning_department = 'Animal Services Office'
	```

11. Write a query to check if there are any duplicate values in the unique_key column (hint.. There are two ways to do this, one is to use a temporary table for the groupby, then filter for values that have more than one count, or, using just one table but including the  `having` function). 
	```
	#Solution 1 using a temp table (with group by) and cheking the count of each group
	
	WITH T AS (
    		SELECT unique_key, COUNT(unique_key) AS key_count
    		FROM `bigquery-public-data.austin_311.311_service_requests`
    		GROUP BY unique_key
	)
	SELECT COUNT(unique_key) AS count_not_unique 
	FROM T 
	WHERE key_count > 1;

	#Solution 1 using group by and having to check the count of each group
	
	SELECT unique_key, COUNT(unique_key) AS key_count
	FROM `bigquery-public-data.austin_311.311_service_requests`
	GROUP BY unique_key
	HAVING key_count > 0;
	```


### For the next question, use the `census_bureau_usa` tables.

1. Write a query that returns each zipcode and their population for 2000 and 2010. 
	```
	WITH Table_2000 AS (
		SELECT zipcode, SUM(population) AS population
		FROM `bigquery-public-data.census_bureau_usa.population_by_zip_2000` 
		GROUP BY zipcode
	)
	, Table_2010 AS (
		SELECT zipcode, SUM(population) AS population
		FROM `bigquery-public-data.census_bureau_usa.population_by_zip_2010`
		GROUP BY zipcode
	)
	, Result AS (
		SELECT A.zipcode AS zip, A.population AS population_2000, B.population AS population_2010
		FROM Table_2000 AS A JOIN Table_2010 AS B ON A.zipcode = B.zipcode
	)
	SELECT * FROM Result;
	```

### For the next section, use the  `bigquery-public-data.google_political_ads.advertiser_weekly_spend` table.
1. Using the `advertiser_weekly_spend` table, write a query that finds the advertiser_name that spent the most in usd. 
	```
	[YOUR QUERY HERE]
	```
2. Who was the 6th highest spender? (No need to insert query here, just type in the answer.)
	```
	[YOUR ANSWER HERE]
	```

3. What week_start_date had the highest spend? (No need to insert query here, just type in the answer.)
	```
	[YOUR ANSWER HERE]
	```

4. Using the `advertiser_weekly_spend` table, write a query that returns the sum of spend by week (using week_start_date) in usd for the month of August only. 
	```
	[YOUR QUERY HERE]
	```
6.  How many ads did the 'TOM STEYER 2020' campaign run? (No need to insert query here, just type in the answer.)
	```
	[YOUR ANSWER HERE]
	```
7. Write a query that has, in the US region only, the total spend in usd for each advertiser_name and how many ads they ran. (Hint, you're going to have to join tables for this one). 
	```
		[YOUR QUERY HERE]
	```
8. For each advertiser_name, find the average spend per ad. 
	```
	[YOUR QUERY HERE]
	```
10. Which advertiser_name had the lowest average spend per ad that was at least above 0. 
	``` 
	[YOUR QUERY HERE]
	```
## For this next section, use the `new_york_citibike` datasets.

1. Who went on more bike trips, Males or Females?
	```
	[YOUR QUERY HERE]
	```
2. What was the average, shortest, and longest bike trip taken in minutes?
	```
	[YOUR QUERY HERE]
	```

3. Write a query that, for every station_name, has the amount of trips that started there and the amount of trips that ended there. (Hint, use two temporary tables, one that counts the amount of starts, the other that counts the number of ends, and then join the two.) 
	```
	[YOUR QUERY HERE]
	```
# The next section is the Google Colab section.  
1. Open up this [this Colab notebook](https://colab.research.google.com/drive/1kHdTtuHTPEaMH32GotVum41YVdeyzQ74?usp=sharing).
2. Save a copy of it in your drive. 
3. Rename your saved version with your initials. 
4. Click the 'Share' button on the top right.  
5. Change the permissions so anyone with link can view. 
6. Copy the link and paste it right below this line. 
	* YOUR LINK:  ________________________________
9. Complete the two questions in the colab notebook file. 
