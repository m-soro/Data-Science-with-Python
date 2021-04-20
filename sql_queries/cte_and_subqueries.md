Warm up questions:

A. Find the average the number of events that occur each day.
```sql
SELECT channel,
       ROUND(avg(no_of_events),2) avg_events
FROM
    ( 
      SELECT date_trunc('day', occurred_at) date, 
             channel,	
             COUNT(*) no_of_events
      FROM web_events
      GROUP BY 1, 2
    ) x
GROUP BY 1
ORDER BY 2 DESC
```
B. Find only the orders that took place in the same month and year as the first order, and then pull the average for each type of paper qty in this month
```sql
SELECT DATE_TRUNC('month',occurred_at) month_order, 
       AVG(standard_qty) standard,
       AVG(gloss_qty) gloss,
       AVG(poster_qty) poster
FROM orders
WHERE DATE_TRUNC('month',occurred_at) = ( 
                                          SELECT DATE_TRUNC('month', occurred_at)
					  FROM orders
					  ORDER BY 1
					  LIMIT 1
                                        )
GROUP BY 1
```
-- SUBQUERRY QUIZZES

1. Provide the name of the sales_rep in each region with the largest amount of total_amt_usd sales.
```sql
SELECT z.total_usd,
       z.region,
       x.rep
FROM ( 
       SELECT SUM(o.total_amt_usd) total_usd,
              s.name rep
       FROM orders o
       JOIN accounts a ON a.id = o.account_id
       JOIN sales_reps s ON s.id = a.sales_rep_id
       GROUP BY 2
     ) x
JOIN (
       SELECT MAX(total_usd) total_usd,
	      region
       FROM ( 
              SELECT SUM(total_amt_usd) total_usd,
	             r.name region,
		     s.name rep
	      FROM orders o
	      JOIN accounts a ON a.id = o.account_id
              JOIN sales_reps s ON s.id = a.sales_rep_id
	      JOIN region r ON r.id = s.region_id
	      GROUP BY 2,3
            ) y
        GROUP BY 2
     ) z 
ON x.total_usd = z.total_usd
ORDER BY 1 DESC

```

2. For the region with the largest (sum) of sales total_amt_usd, how many total (count) orders were placed?
```sql
SELECT COUNT(*) num_of_orders,
       r.name region
FROM orders o
JOIN accounts a ON a.id = o.account_id
JOIN sales_reps s ON a.sales_rep_id = s.id
JOIN region r ON r.id = s.region_id
WHERE r.name = (
                 SELECT region
           	 FROM (
                        SELECT SUM(total_amt_usd) total_usd,								       
                               r.name region 
                        FROM orders o
		        JOIN accounts a ON a.id = o.account_id
			JOIN sales_reps s ON s.id = a.sales_rep_id
			JOIN region r ON r.id = s.region_id
			GROUP BY 2
			ORDER BY 1 DESC
			LIMIT 1
                      ) x
              )
GROUP BY 2


```
3. How many accounts had more total purchases than the account name which has bought the most standard_qty paper throughout their lifetime as a customer?
```sql
SELECT COUNT(*)
FROM (
       SELECT a.name account_name,
              SUM(o.total) total_purch
       FROM accounts a
       JOIN orders o ON a.id = o.account_id
       GROUP BY 1
       HAVING sum(o.total) > ( 
                               SELECT total_purch
			       FROM ( 
                                      SELECT a.name account_name,
				             SUM(o.standard_qty) standard_qty,
				             SUM(total) total_purch
			              FROM accounts a
				      JOIN orders o ON o.account_id = a.id
				      GROUP BY 1
				      ORDER BY 2 DESC
				      LIMIT 1
                                    ) x
                              )
     ) y


```
4. For the customer that spent the most (in total over their lifetime as a customer) total_amt_usd, how many web_events did they have for each channel?
```sql
SELECT a.name account_name,
       w.channel channel,
       COUNT(*) num_of_times
FROM web_events w
JOIN accounts a ON w.account_id = a.id
WHERE a.name = ( 
                 SELECT account_name
		 FROM ( 
                        SELECT a.name account_name,
			       SUM(o.total_amt_usd) total_usd
		        FROM accounts a
			JOIN orders o ON a.id = o.account_id
			GROUP BY 1
			ORDER BY 2 DESC
			LIMIT 1
                      ) x
              )
GROUP BY 1,2
ORDER BY 3 DESC
```


5. What is the lifetime average amount spent in terms of total_amt_usd for the top 10 total spending accounts?
```sql
SELECT AVG(total_usd) avg_total_usd
FROM (
       SELECT a.name accounts,
              sum(o.total_amt_usd) total_usd
       FROM accounts a
       JOIN orders o ON a.id = o.account_id
       GROUP BY 1
       ORDER BY 2 DESC
       LIMIT 10
     ) x

```

6. What is the lifetime average amount spent in terms of total_amt_usd, including only the companies that spent more per order, on average, than the average of all orders.
```sql
SELECT AVG(avg_total_usd)
FROM (
       SELECT a.name account_name,
	      AVG(total_amt_usd) avg_total_usd
       FROM accounts a
       JOIN orders o ON a.id = o.account_id
       GROUP BY 1
HAVING avg(total_amt_usd) > ( 
                              SELECT AVG(total_amt_usd)
                              FROM orders
                            )
) x
```
-- WITH STATEMENTS

1. Provide the name of the sales_rep in each region with the largest amount of total_amt_usd sales.

```sql
WITH ttl_rep_rgn AS ( 
                      SELECT MAX(total_usd) total_usd,
		             region
		      FROM ( 
                             SELECT r.name region,
			            s.name rep,
				    sum(o.total_amt_usd) total_usd
			     FROM accounts a
			     JOIN orders o ON a.id = o.account_id
			     JOIN sales_reps s ON a.sales_rep_id = s.id
		             JOIN region r ON s.region_id = r.id
			     GROUP BY 1,2
                           ) x
		      GROUP BY 2
                    ),
       rep_total AS (
                      SELECT s.name rep,
		             SUM(o.total_amt_usd) total_usd
		      FROM orders o
		      JOIN accounts a ON a.id = o.account_id
		      JOIN sales_reps s ON s.id = a.sales_rep_id
		      GROUP BY 1
                    )
SELECT trr.region,
       rt.rep,
       trr.total_usd
FROM ttl_rep_rgn trr
JOIN rep_total rt ON rt.total_usd = trr.total_usd
ORDER BY 3 DESC
```

2. For the region with the largest sales total_amt_usd, how many total orders were placed?
```sql
WITH rgn_ttl AS ( 
                  SELECT MAX(total_usd) total_usd,
		         region
	          FROM ( 
                         SELECT r.name region,
				SUM(o.total_amt_usd) total_usd
			 FROM orders o
			 JOIN accounts a ON a.id = o.account_id
			 JOIN sales_reps s ON a.sales_rep_id = s.id
			 JOIN region r ON r.id = s.region_id
			 GROUP BY 1
                       ) x
		  GROUP BY 2
		  ORDER BY 1 DESC
		  LIMIT 1
                ),
     max_rgn AS ( 
                  SELECT region
		  FROM rgn_ttl
                )
SELECT count(*)
FROM orders o
JOIN accounts a ON a.id = o.account_id
JOIN sales_reps s ON a.sales_rep_id = s.id
JOIN region r ON r.id = s.region_id
WHERE r.name = ( 
                 SELECT region
		 FROM max_rgn
               )
```
3. How many accounts had more total purchases than the account name which has bought the most standard_qty paper throughout their lifetime as a customer?
```sql
WITH max_std_qty AS ( 
                      SELECT a.name account,
		             SUM(o.standard_qty) std_qty,
			     SUM(total) total_purch
		      FROM orders o
		      JOIN accounts a ON a.id = o.account_id
		      GROUP BY 1
		      ORDER BY 2 DESC
		      LIMIT 1
                    ),
     acct_total AS ( 
                      SELECT a.name account,
			     SUM(o.total) total
		      FROM orders o
		      JOIN accounts a ON a.id = o.account_id
		      GROUP BY 1
                   )
SELECT count(*)
FROM ( 
       SELECT *
       FROM acct_total
       WHERE total > ( 
                       SELECT total_purch
		       FROM max_std_qty
                     ) 
) x

```
4. For the customer that spent the most (in total over their lifetime as a customer) total_amt_usd, how many web_events did they have for each channel?
```sql
WITH max_acct_spend AS ( 
                         SELECT account
			 FROM ( 
                                SELECT a.name account,
				       SUM(total_amt_usd) total_amt
				FROM orders o
				JOIN accounts a ON a.id = o.account_id
				GROUP BY 1
				ORDER BY 2 DESC
				LIMIT 1
                              ) x
                       )
SELECT a.name account,
       channel,
       COUNT(*) num_of_times
FROM web_events w
JOIN accounts a ON a.id = w.account_id
WHERE a.name = ( 
                 SELECT *
		 FROM max_acct_spend
               )
GROUP BY 1,2
ORDER BY 3 DESC
```

5. What is the lifetime average amount spent in terms of total_amt_usd for the top 10 total spending accounts?
```sql
WITH avg_spent_top10 AS ( 
                          SELECT a.name account,
			         SUM(o.total_amt_usd) total_usd
			  FROM orders o
			  JOIN accounts a ON a.id = o.account_id
			  GROUP BY 1
			  ORDER BY 2 DESC
			  LIMIT 10
                        )
SELECT ROUND(AVG(total_usd),2) avg_top10
FROM avg_spent_top10

```
6. What is the lifetime average amount spent in terms of total_amt_usd, including only the companies that spent more per order, on average, than the average of all orders.

```sql
WITH avg_all AS ( 
                  SELECT a.name account,
		         AVG(total_amt_usd) avg_usd
		  FROM orders o
		  JOIN accounts a ON a.id = o.account_id
	          GROUP BY 1
		  ORDER BY 2 DESC
                )

SELECT AVG(avg_usd)
FROM ( 
       SELECT account,
	      avg_usd
       FROM avg_all
       WHERE avg_usd > ( 
                         SELECT avg(total_amt_usd)
	                 FROM orders 
                       ) 
     ) x
```     
