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

[COALESCE](https://youtu.be/86vgu-ECBCQ?t=28)

Window Functions:

>The easiest way to think about this - leaving the ORDER BY out is equivalent to "ordering" in a way that all rows in the partition are "equal" to each other. Indeed, you can get the same effect by explicitly adding the ORDER BY clause like this: ORDER BY 0 (or "order by" any constant expression), or even, more emphatically, ORDER BY NULL.

**Python**

**zip()**

* returns an iterator! convert it to a list or iterate in a for loop to print result! 
* try to think of it just like a zipper! it just zips all variables together.

```python
  # zip()
  
  list(zip(['a', 'b', 'c'], [1, 2, 3])) # would output: 
  [('a', 1), ('b', 2), ('c', 3)] 
  
  # Example 1:
  
  # given two separate list
  letters = ['a', 'b', 'c']
  nums = [1, 2, 3]
  
  # lets zip letters and numbers together
  for letter, num in zip(letters, nums):
    
    # then un-pack the zipped tuples like this
    print("{}: {}".format(letter, num))
    
    # Example 2:
    
    # How to un-zip a list
    some_list = [('a', 1), ('b', 2), ('c', 3)]
    letters, nums = zip(*some_list)
```
**enumerate()**

* returns an iterator of tuples containing indeces and values of a list!
* often used when you want the indeces along with each element of an iterable in a loop!

```python
  # Example:
  
  letters = ['a', 'b', 'c', 'd', 'e']
  
  for i, letter in enumerate(letters):
    print(i, letter)
    
  # Outputs:
  
  0 a
  1 b
  2 c
  3 d
  4 e
```

### Errors can be classified into two types:
1. Syntax errors - if you are not following the correct syntax! 
2. Exceptions - occur when un expected things happen during execution!

There are several types of exceptions:

* **ValueError** - An object of the correct type but inappropriate value is passed as input to a built in operation or function.
* **NameError** - when using a variable that was not defined. 
* **AssertionError** - An assert statement fails.
* **IndexError** - A sequence subscript is out of range.
* **KeyError** - A key can't be found in a dictionary.
* **TypeError** - An object of an unsupported type is passed as input to an operation or function.
* **UnboundLocalError** - when you are trying to access a local variable before it is defined. Make sure local scope of variable in function is defined or value assigned to it. 
* **ValueError:too many values to unpack(expected 2)** - Assignation error. Inconsistency in how many values being unpacked and how many variables the values should be assigned to. 

## Importing local scripts and if name main block explanation

<iframe width="100%" height="433" src="https://www.youtube.com/embed/qjeSn6zZbR0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Third party libraries and requirements.txt explanation

<iframe width="100%" height="433" src="https://www.youtube.com/embed/epOze9gC6T4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

