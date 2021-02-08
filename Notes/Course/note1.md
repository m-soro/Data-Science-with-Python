---
layout: default
title: First Note
parent:  Course
grand_parent: Notes
nav_order: 1
---

# Helpful tips:

In `joins_sql_queries.txt` 
* Quiz 6: Pre-filter on the `ON` clause using `AND`
* Quiz 13: Notice that the endpoint is '2016-01-01' the later part of the `BETWEEN` clause is ommitted. 

* `NULL` is not a value but a property of the data, therefore `NULL = 0` does not work! When working with `NULL`s you write `IS NULL` or `IS NOT NULL`.
* In `sql_aggregations_queries.txt` Quiz 11 Find the median. Helpful [link](https://www.compose.com/articles/metrics-maven-meet-in-the-middle-median-in-postgresql/).

In `sql_aggregations_queries.txt`

* Quiz 32: You can also pre-filter with `AND` in `HAVING` clause.

* Working with dates -->`DATE_TRUNC` and `DATE_PART`
<iframe width="560" height="315" src="https://www.youtube.com/embed/UPWkDhW4cLI" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

* Quiz 36 Notice this line
`WHERE occurred_at BETWEEN '2014-01-01' AND '2017-01-01'`

* Quiz 37 
`WHERE DATE_TRUNC('year', OCCURRED_AT) BETWEEN '2014-01-01 00:00:00' AND '2016-01-01 00:00:00'`
Un-neccessary but both lines work

In Data Cleaning SQL:
CAST(to_cast as DATEorSomethingElse) or ::DATEOrSomethingElse.
