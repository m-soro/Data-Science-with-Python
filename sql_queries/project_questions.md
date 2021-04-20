1. Create a table that provides the following details: actor's first and last name combined as full_name, film title, film description and length of the movie.
```sql
SELECT a.first_name||' '||a.last_name AS actor, 
       f.title, 
       f.description, 
       f.length 
FROM   film_actor fa
JOIN   actor a ON fa.actor_id = a.actor_id
JOIN   film f ON  f.film_id = fa.film_id
```

2. Write a query that creates a list of actors and movies where the movie length was more than 60 minutes.
```sql
SELECT a.first_name||' '||a.last_name AS actor, 
       f.title, 
       f.description, 
       f.length 
FROM   film_actor fa
JOIN   actor a ON fa.actor_id = a.actor_id
JOIN   film f ON  f.film_id = fa.film_id
WHERE f.length > 60
```
3. Write a query that captures the actor id, full name of the actor, and counts the number of movies each actor has made. (HINT: Think about whether you should group by actor id or the full name of the actor.) Identify the actor who has made the maximum number movies.
```sql
SELECT a.actor_id,
       a.first_name||' '||a.last_name AS actor,
       count(*) movie_count
FROM   film_actor fa
JOIN   actor a ON fa.actor_id = a.actor_id
JOIN   film f ON  f.film_id = fa.film_id
GROUP BY 1,2
ORDER BY 3 DESC
```
4. Write a query that displays a table with 4 columns: actor's full name, film title, length of movie, and a column name "filmlen_groups" that classifies movies based on their length. Filmlen_groups should include 4 categories: 1 hour or less, Between 1-2 hours, Between 2-3 hours, More than 3 hours.
```sql
SELECT a.first_name||' '||a.last_name AS actor,
       f.title AS film_title,
       f.length AS film_length,
       CASE WHEN f.length < 60 THEN '1 hr or less'
	    WHEN f.length >= 60 AND f.length <= 120 THEN 'Between 1-2 hrs'
            WHEN f.length >= 120 AND f.length <= 180 THEN 'Between 2-3 hrs'
	    ELSE 'More than 3 hrs' 
       END AS filmlen_groups			
FROM   film_actor fa
JOIN   actor a ON fa.actor_id = a.actor_id
JOIN   film f ON f.film_id = fa.film_id
GROUP BY 1,2,3
```
5. Now, we bring in the advanced SQL query concepts! Revise the query you wrote above to create a count of movies in each of the 4 filmlen_groups: 1 hour or less, Between 1-2 hours, Between 2-3 hours, More than 3 hours.

-- USING CTE
```sql
WITH t1 as ( 
	     SELECT title,
	   	    length,
	     CASE WHEN length <= 60 THEN '1 hr or less'
	          WHEN length > 60 AND length <= 120 THEN 'Between 1-2 hrs'
		  WHEN length > 120 AND length <= 180 THEN 'Between 2-3 hrs'
	          ELSE 'More than 3 hrs' END AS filmlen_groups
             FROM film
             GROUP BY 1,2
           )

SELECT filmlen_groups, 
       COUNT(*)
FROM t1
GROUP BY 1
```

-- USING WINDOW FUNCTION
```sql
SELECT DISTINCT(filmlen_groups),
       COUNT(*) OVER(PARTITION BY filmlen_groups)

FROM ( 
       SELECT title,
              length,
       CASE WHEN length <= 60 THEN '1 hr or less'
	    WHEN length > 60 AND length <= 120 THEN 'Between 1-2 hrs'
            WHEN length > 120 AND length <= 180 THEN 'Between 2-3 hrs'
	    ELSE 'More than 3 hrs' END AS filmlen_groups
       FROM film
       GROUP BY 1,2
     ) x
```
-- Question Set 1

6. We want to understand more about the movies that families are watching. The following categories are considered family movies: Animation, Children, Classics, Comedy, Family and Music.

Create a query that lists each movie, the film category it is classified in, and the number of times it has been rented out.
		   
```sql	
WITH main AS ( 
               SELECT f.title AS film_title, 
                      c.name AS category_name, 
                      r.rental_date
               FROM film f
               JOIN film_category fc ON f.film_id = fc.film_id
               JOIN category c ON c.category_id = fc.category_id
               AND c.name IN ('Animation','Children','Classics','Comedy','Family','Music')
               JOIN inventory i ON i.film_id = f.film_id
               JOIN rental r ON i.inventory_id = r.inventory_id 
             )

SELECT DISTINCT(film_title), 
       category_name,
       COUNT(rental_date) OVER(PARTITION BY film_title) AS rental_count
FROM main_table
ORDER BY 2
```

7. Now we need to know how the length of rental duration of these family-friendly movies compares to the duration that all movies are rented for. Can you provide a table with the movie titles and divide them into 4 levels (first_quarter, second_quarter, third_quarter, and final_quarter) based on the quartiles (25%, 50%, 75%) of the rental duration for movies across all categories? Make sure to also indicate the category that these family-friendly movies fall into.
```sql
SELECT f.title AS film_title, 
       c.name AS category_name,
       f.rental_duration,
       NTILE(4) OVER(ORDER BY rental_duration) standard_quartile
FROM film f
JOIN film_category fc ON f.film_id = fc.film_id
JOIN category c ON c.category_id = fc.category_id
AND c.name IN ('Animation','Children','Classics','Comedy','Family','Music')
```

8. Finally, provide a table with the family-friendly film category, each of the quartiles, and the corresponding count of movies within each combination of film category for each corresponding rental duration category. The resulting table should have three columns:

1. Category
2. Rental length category
3. Count

Solution:
```sql
WITH main AS ( 
	       SELECT f.title AS film_title, 
                      c.name AS category_name,
	              f.rental_duration,
	              NTILE(4) OVER(ORDER BY rental_duration) AS standard_quartile
               FROM film f
               JOIN film_category fc ON f.film_id = fc.film_id
               JOIN category c ON c.category_id = fc.category_id
               AND c.name IN ('Animation','Children','Classics','Comedy','Family','Music') 
             )

SELECT category_name,
       standard_quartile,
       COUNT(film_title)
FROM main
GROUP BY 1,2
ORDER BY 1,2
```
-- Question Set 2

9. We want to find out how the two stores compare in their count of rental orders during every month for all the years we have data for. Write a query that returns the store ID for the store, the year and month and the number of rental orders each store has fulfilled for that month. Your table should include a column for each of the following: year, month, store ID and count of rental orders fulfilled during that month.

```sql
SELECT DATE_PART('month',r.rental_date) rental_month, 
       DATE_PART('year',r.rental_date) rental_year, 
       s.store_id,
       COUNT(r.rental_id) rental_count
FROM rental AS r
JOIN staff AS st ON r.staff_id = st.staff_id
JOIN store AS s ON s.store_id = st.store_id
GROUP BY 1,2,3
ORDER BY 4 DESC

```

10. We would like to know who were our top 10 paying customers, how many payments they made on a monthly basis during 2007, and what was the amount of the monthly payments. Can you write a query to capture the customer name, month and year of payment, and total payment amount for each month by these top 10 paying customers?
```sql
WITH t1 AS ( 
             SELECT c.first_name || ' ' || c.last_name AS customer,
		    c.customer_id,
		    SUM(p.amount) AS total
	     FROM customer c
	     JOIN payment p ON c.customer_id = p.customer_id
	     GROUP BY 1,2
	     ORDER BY 3 DESC
             LIMIT 10
           )

SELECT date_trunc('month',payment_date),
       customer,
       count(p.*) pay_ct_per_month,
       sum(p.amount) pay_amount
FROM t1
JOIN payment p ON p.customer_id = t1.customer_id
GROUP BY 1,2
ORDER BY 2
```

11. Finally, for each of these top 10 paying customers, I would like to find out the difference across their monthly payments during 2007. Please go ahead and write a query to compare the payment amounts in each successive month. Repeat this for each of these 10 paying customers. Also, it will be tremendously helpful if you can identify the customer name who paid the most difference in terms of payments.

```sql
WITH t1 AS ( 
             SELECT c.first_name || ' ' || c.last_name AS customer,
		    c.customer_id,
		    SUM(p.amount) AS total
	     FROM customer c
	     JOIN payment p ON c.customer_id = p.customer_id
	     GROUP BY 1,2
	     ORDER BY 2 DESC
             LIMIT 10
           ),
     t2 AS (
             SELECT date_trunc('month',payment_date) AS pay_month,
                    customer,
                    COUNT(p.*) pay_ct_per_month,
                    SUM(p.amount) pay_amount
	   
             FROM t1
             JOIN payment p ON p.customer_id = t1.customer_id
             GROUP BY 1,2
             ORDER BY 2 
	   )
SELECT *, 
       COALESCE(LEAD(pay_amount) OVER (PARTITION BY customer ORDER BY pay_month) - pay_amount,0) AS difference
FROM t2
```


   

