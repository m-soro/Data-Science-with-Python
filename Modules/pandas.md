---
layout: default
title: Pandas
parent:  Introduction to Python programming
grand_parent: Modules
nav_order: 7
---

# Introduction to Pandas

**Pandas** is a package for data manipulation and analysis in Python. The name Pandas is derived from the econometrics term Panel Data. Pandas incorporates two additional data structures into Python, namely **Pandas Series** and **Pandas DataFrame**. These data structures allow us to work with labeled and relational data in an easy and intuitive manner. These lessons are intended as a basic overview of Pandas and introduces some of its most important features.

In the following lessons you will learn:

* How to import Pandas
* How to create Pandas Series and DataFrames using various methods
* How to access and change elements in Series and DataFrames
* How to perform arithmetic operations on Series
* How to load data into a DataFrame
* How to deal with Not a Number (NaN) values

The following lessons assume that you are already familiar with NumPy and have gone over the previous NumPy lessons. Therefore, to avoid being repetitive we will omit a lot of details already given in the NumPy lessons. Consequently, if you haven't seen the NumPy lessons we suggest you go over them first.

### Downloading Pandas

Pandas is included with Anaconda. If you don't already have Anaconda installed on your computer, please refer to the Anaconda section to get clear instructions on how to install Anaconda on your PC or Mac.

### Pandas Versions

As with many Python packages, Pandas is updated from time to time. The following lessons were created using Pandas version 0.22. You can check which version of Pandas you have by typing `!conda list pandas` in your Jupyter notebook or by typing `conda list pandas` in the Anaconda prompt. If you have another version of Pandas installed in your computer, you can update your version by typing `conda install pandas=0.22` in the Anaconda prompt. As newer versions of Pandas are released, some functions may become obsolete or replaced, so make sure you have the correct Pandas version before running the code. This will guarantee your code will run smoothly.

### Pandas Documentation

Pandas is a remarkable data analysis library and it has many functions and features. In these introductory lessons we will only scratch the surface of what Pandas can do. If you want to learn more about Pandas, make sure you check out the [Pandas Documentation](https://pandas.pydata.org/pandas-docs/stable/).

## Why Use Pandas?

The recent success of machine learning algorithms is partly due to the huge amounts of data that we have available to train our algorithms on. However, when it comes to data, quantity is not the only thing that matters, the quality of your data is just as important. It often happens that large datasets don’t come ready to be fed into your learning algorithms. More often than not, large datasets will often have missing values, outliers, incorrect values, etc… Having data with a lot of missing or bad values, for example, is not going to allow your machine learning algorithms to perform well. Therefore, one very important step in machine learning is to look at your data first and make sure it is well suited for your training algorithm by doing some basic data analysis. This is where Pandas come in. Pandas Series and DataFrames are designed for fast data analysis and manipulation, as well as being flexible and easy to use. Below are just a few features that makes Pandas an excellent package for data analysis:

* Allows the use of labels for rows and columns
* Can calculate rolling statistics on time series data
* Easy handling of NaN values
* Is able to load data of different formats into DataFrames
* Can join and merge different datasets together
* It integrates with NumPy and Matplotlib

For these and other reasons, Pandas DataFrames have become one of the most commonly used Pandas object for data analysis in Python.

## Creating Pandas Series

<iframe width="100%" height="379" src="https://www.youtube.com/embed/iXnYN8cnhzs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Pandas Series

A Pandas series is a **one-dimensional** array-like object that can hold **many data types**, such as numbers or strings, and has an option to provide axis labels.

## Difference between NumPy ndarrays and Pandas Series

1. One of the main differences between Pandas Series and NumPy ndarrays is that you can assign an index label to each element in the Pandas Series. In other words, you can name the indices of your Pandas Series anything you want.
2. Another big difference between Pandas Series and NumPy ndarrays is that Pandas Series can hold data of different data types.

Let's start by importing Pandas into Python. It has become a convention to import Pandas as `pd`, therefore, you can import Pandas by typing the following command in your Jupyter notebook:

`import pandas as pd`

Let's begin by creating a Pandas Series. You can create Pandas Series by using the command `pd.Series(data, index)`, where `index` is a list of index labels. Let's use a Pandas Series to store a grocery list. We will use the food items as index labels and the quantity we need to buy of each item as our data.

### Example 1 - Create a Series

```python
# We import Pandas as pd into Python
import pandas as pd

# We create a Pandas Series that stores a grocery list
groceries = pd.Series(data = [30, 6, 'Yes', 'No'], index = ['eggs', 'apples', 'milk', 'bread'])

# We display the Groceries Pandas Series
groceries

# Outputs:
eggs           30
apples         6
milk         Yes
bread       No
dtype: object
```

We see that Pandas Series are displayed with the indices in the first column and the data in the second column. Notice that the data is not indexed 0 to 3 but rather it is indexed with the names of the food we put in, namely eggs, apples, etc... Also, notice that the data in our Pandas Series has both integers and strings.

Just like NumPy ndarrays, Pandas Series have attributes that allow us to get information from the series in an easy way. Let's see some of them:


### Example 2 - Print attributes - shape, ndim,and size
```python
# We print some information about Groceries
print('Groceries has shape:', groceries.shape)
print('Groceries has dimension:', groceries.ndim)
print('Groceries has a total of', groceries.size, 'elements')

#Outputs:
Groceries has shape: (4,)
Groceries has dimension: 1
Groceries has a total of 4 elements
```

We can also print the index labels and the data of the Pandas Series separately. This is useful if you don't happen to know what the index labels of the Pandas Series are.

### Example 3 - Print attributes - values, and index
```python
# We print the index and data of Groceries
print('The data in Groceries is:', groceries.values)
print('The index of Groceries is:', groceries.index)

# Outputs
The data in Groceries is: [30 6 'Yes' 'No']
The index of Groceries is: Index(['eggs', 'apples', 'milk', 'bread'], dtype='object')

```

If you are dealing with a very large Pandas Series and if you are not sure whether an index label exists, you can check by using the in command

### Example 4 - Check if an index is available in the given Series
```python
# We check whether bananas is a food item (an index) in Groceries
x = 'bananas' in groceries

# We check whether bread is a food item (an index) in Groceries
y = 'bread' in groceries

# We print the results
print('Is bananas an index label in Groceries:', x)
print('Is bread an index label in Groceries:', y)

# Outputs
Is bananas an index label in Groceries: False
Is bread an index label in Groceries: True
```
#### Additional Reading - Pandas Series Documentation

Refer to the [Series documentation](https://pandas.pydata.org/pandas-docs/stable/reference/series.html) to have a quick glance at the different attributes of Series, and the optional arguments of the constructor.

## Accessing and Deleting Elements in Pandas Series

<iframe width="100%" height="379" src="https://www.youtube.com/embed/B7MuFIwboKU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Now let's look at how we can access or modify elements in a Pandas Series. One great advantage of Pandas Series is that it allows us to access data in many different ways. Elements can be accessed using index labels or numerical indices inside square brackets, [ ], similar to how we access elements in NumPy ndarrays. Since we can use numerical indices, we can use both positive and negative integers to access data from the beginning or from the end of the Series, respectively. Since we can access elements in various ways, in order to remove any ambiguity to whether we are referring to an index label or numerical index, Pandas Series have two attributes, `.loc` and `.iloc` to explicitly state what we mean. The attribute `.loc` stands for location and it is used to explicitly state that we are using a labeled index. Similarly, the attribute `.iloc` stands for integer location and it is used to explicitly state that we are using a numerical index. Let's see some examples:

### Example 1. Access elements using index labels
```python
# We access elements in Groceries using index labels:

# We use a single index label
print('How many eggs do we need to buy:', groceries['eggs'])
print()

# we can access multiple index labels
print('Do we need milk and bread:\n', groceries[['milk', 'bread']])
print()

# we use loc to access multiple index labels
print('How many eggs and apples do we need to buy:\n', groceries.loc[['eggs', 'apples']])
print()

# We access elements in Groceries using numerical indices:

# we use multiple numerical indices
print('How many eggs and apples do we need to buy:\n',  groceries[[0, 1]])
print()

# We use a negative numerical index
print('Do we need bread:\n', groceries[[-1]])
print()

# We use a single numerical index
print('How many eggs do we need to buy:', groceries[0])
print()
# we use iloc to access multiple numerical indices
print('Do we need milk and bread:\n', groceries.iloc[[2, 3]])

# Ouputs
How many eggs do we need to buy: 30

Do we need milk and bread:
milk       Yes
bread     No
dtype: object

How many eggs and apples do we need to buy:
eggs       30
apples     6
dtype: object

How many eggs and apples do we need to buy:
eggs       30
apples     6
dtype: object

Do we need bread:
bread     No
dtype: object

How many eggs do we need to buy: 30

Do we need milk and bread:
milk       Yes
bread     No
dtype: object
```

Pandas Series are also mutable like NumPy ndarrays, which means we can change the elements of a Pandas Series after it has been created. For example, let's change the number of eggs we need to buy from our grocery list

### Example 2. Mutate elements using index labels
```python

# We display the original grocery list
print('Original Grocery List:\n', groceries)

# We change the number of eggs to 2
groceries['eggs'] = 2

# We display the changed grocery list
print()
print('Modified Grocery List:\n', groceries)

# Outputs
Original Grocery List:
eggs           30
apples         6
milk         Yes
bread       No
dtype: object

Modified Grocery List:
eggs             2
apples         6
milk         Yes
bread       No
dtype: object
```
We can also delete items from a Pandas Series by using the `.drop()` method. `The Series.drop(label)` method removes the given label from the given Series. We should note that the Series.drop(label) method drops elements from the Series out-of-place, meaning that it doesn't change the original Series being modified. Let's see how this works:

### Example 3. Delete elements out-of-place using drop()
```python
# We display the original grocery list
print('Original Grocery List:\n', groceries)

# We remove apples from our grocery list. The drop function removes elements out of place
print()
print('We remove apples (out of place):\n', groceries.drop('apples'))

# When we remove elements out of place the original Series remains intact.

# To see this we display our grocery list again
print()
print('Grocery List after removing apples out of place:\n', groceries)

# Outputs
Original Grocery List:
eggs           30
apples         6
milk         Yes
bread       No
dtype: object

We remove apples (out of place):
eggs           30
milk         Yes
bread       No
dtype: object

Grocery List after removing apples out of place:
eggs           30
apples         6
milk         Yes
bread       No
dtype: object
```

We can delete items from a Pandas Series in place by setting the keyword `inplace` to `True` in the `.drop()` method. Let's see an example:

### Example 4. Delete elements in-place using drop()

```python
# We display the original grocery list
print('Original Grocery List:\n', groceries)

# We remove apples from our grocery list in place by setting the inplace keyword to True
groceries.drop('apples', inplace = True)

# When we remove elements in place the original Series its modified. To see this
# we display our grocery list again
print()
print('Grocery List after removing apples in place:\n', groceries)

# Outputs
Original Grocery List:
eggs           30
apples         6
milk         Yes
bread       No
dtype: object

Grocery List after removing apples in place:
eggs           30
milk         Yes
bread       No
dtype: object
```

### Additional Reading - Pandas Series Documentation
Refer to the list of available functions in the following two sections:

* [Reindexing / selection / label manipulation](https://pandas.pydata.org/pandas-docs/stable/reference/series.html#reindexing-selection-label-manipulation)
* [Indexing, and iteration](https://pandas.pydata.org/pandas-docs/stable/reference/series.html#indexing-iteration)

## Arithmetic Operations on Pandas Series

<iframe width="100%" height="379" src="https://www.youtube.com/embed/yhMT0X6YPFA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Just like with NumPy ndarrays, we can perform element-wise arithmetic operations on Pandas Series. In this lesson we will look at arithmetic operations between Pandas Series and single numbers. Let's create a new Pandas Series that will hold a grocery list of just fruits.

```python
# We create a Pandas Series that stores a grocery list of just fruits
fruits= pd.Series(data = [10, 6, 3,], index = ['apples', 'oranges', 'bananas'])

# We display the fruits Pandas Series
fruits
apples         10
oranges        6
bananas       3
dtype: int64
```

We can now modify the data in fruits by performing basic arithmetic operations. Let's see some examples

### Example 1. Element-wise basic arithmetic operations
```python
# We print fruits for reference
print('Original grocery list of fruits:\n ', fruits)

# We perform basic element-wise operations using arithmetic symbols
print()
print('fruits + 2:\n', fruits + 2) # We add 2 to each item in fruits
print()
print('fruits - 2:\n', fruits - 2) # We subtract 2 to each item in fruits
print()
print('fruits * 2:\n', fruits * 2) # We multiply each item in fruits by 2
print()
print('fruits / 2:\n', fruits / 2) # We divide each item in fruits by 2
print()

# Outputs
Original grocery list of fruits:
apples         10
oranges        6
bananas       3
dtype: int64

fruits + 2:
apples         12
oranges        8
bananas       5
dtype: int64

fruits - 2:
apples           8
oranges        4
bananas       1
dtype: int64

fruits * 2:
apples         20
oranges      12
bananas       6
dtype: int64

fruits / 2:
apples           5.0
oranges        3.0
bananas       1.5
dtype: float64
```

You can also apply mathematical functions from NumPy, such as `sqrt(x)`, to all elements of a Pandas Series.

### Example 2. Use mathematical functions from NumPy to operate on Series
```python
# We import NumPy as np to be able to use the mathematical functions
import numpy as np

# We print fruits for reference
print('Original grocery list of fruits:\n', fruits)

# We apply different mathematical functions to all elements of fruits
print()
print('EXP(X) = \n', np.exp(fruits))
print()
print('SQRT(X) =\n', np.sqrt(fruits))
print()
print('POW(X,2) =\n',np.power(fruits,2)) # We raise all elements of fruits to the power of 2

# Outputs
Original grocery list of fruits:
apples         10
oranges        6
bananas       3
dtype: int64

EXP(X) =
apples        22026.465795
oranges         403.428793
bananas          20.085537
dtype: float64

SQRT(X) =
apples            3.162278
oranges         2.449490
bananas        1.732051
dtype: float64

POW(X,2) =
apples         100
oranges        36
bananas         9
dtype: int64
```
Pandas also allows us to only apply arithmetic operations on selected items in our fruits grocery list. Let's see some examples

### Example 3. Perform arithmetic operations on selected elements
```python
# We print fruits for reference
print('Original grocery list of fruits:\n ', fruits)
print()

# We add 2 only to the bananas
print('Amount of bananas + 2 = ', fruits['bananas'] + 2)
print()

# We subtract 2 from apples
print('Amount of apples - 2 = ', fruits.iloc[0] - 2)
print()

# We multiply apples and oranges by 2
print('We double the amount of apples and oranges:\n', fruits[['apples', 'oranges']] * 2)
print()

# We divide apples and oranges by 2
print('We half the amount of apples and oranges:\n', fruits.loc[['apples', 'oranges']] / 2)

# Outputs:

Original grocery list of fruits:
apples         10
oranges        6
bananas       3
dtype: int64

Amount of bananas + 2 = 5

Amount of apples - 2 = 8

We double the amount of apples and oranges:
apples         20
oranges      12
dtype: int64

We half the amount of apples and oranges:
apples         5.0
oranges      3.0
dtype: float64
```

You can also apply arithmetic operations on Pandas Series of mixed data type provided that the arithmetic operation is defined for *all* data types in the Series, otherwise, you will get an error. Let's see what happens when we multiply our grocery list by 2

### Example 4. Perform multiplication on a Series having integer and string elements
```python
# We multiply our grocery list by 2
groceries * 2

# Outputs
eggs                 60
apples             12
milk         YesYes
bread        NoNo
dtype: object
```
As we can see, in this case, since we multiplied by 2, Pandas doubles the data of each item including the strings. Pandas can do this because the multiplication operation `*` is defined both for numbers and strings. If you were to apply an operation that was valid for numbers but not strings, say for instance, `/` you will get an error. So when you have mixed data types in your Pandas Series make sure the arithmetic operations are valid on all the data types of your elements.

## Creating Pandas DataFrames

<iframe width="100%" height="379" src="https://www.youtube.com/embed/eMHUn9v9dds" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Pandas DataFrames are two-dimensional data structures with labeled rows and columns, that can hold many data types. If you are familiar with Excel, you can think of Pandas DataFrames as being similar to a spreadsheet. We can create Pandas DataFrames manually or by loading data from a file. In this lesson, we will start by learning how to create Pandas DataFrames manually from dictionaries, and later we will see how we can load data into a DataFrame from a data file.

## Create a DataFrame manually

We will start by creating a DataFrame manually from a dictionary of Pandas Series. It is a two-step process:

1. The first step is to create the dictionary of Pandas Series.
2. After the dictionary is created we can then pass the dictionary to the `pd.DataFrame()` function.

We will create a dictionary that contains items purchased by two people, Alice and Bob, on an online store. The Pandas Series will use the price of the items purchased as data, and the purchased items will be used as the index labels to the Pandas Series. Let's see how this done in code:

```python
# We import Pandas as pd into Python
import pandas as pd

# We create a dictionary of Pandas Series
items = {'Bob' : pd.Series(data = [245, 25, 55], index = ['bike', 'pants', 'watch']),
         'Alice' : pd.Series(data = [40, 110, 500, 45], index = ['book', 'glasses', 'bike', 'pants'])}

# We print the type of items to see that it is a dictionary
print(type(items))
# Outputs
class 'dict'
```

Now that we have a dictionary, we are ready to create a DataFrame by passing it to the `pd.DataFrame()` function. We will create a DataFrame that could represent the shopping carts of various users, in this case we have only two users, Alice and Bob.

### Example 1. Create a DataFrame using a dictionary of Series.
```python
# We create a Pandas DataFrame by passing it a dictionary of Pandas Series
shopping_carts = pd.DataFrame(items)

# We display the DataFrame
shopping_carts
```
>Outputs:

![image](assets/images/01.png)

There are several things to notice here, as explained below:

1. We see that DataFrames are displayed in tabular form, much like an Excel spreadsheet, with the labels of rows and columns in bold.
2. Also, notice that the row labels of the DataFrame are built from the union of the index labels of the two Pandas Series we used to construct the dictionary. And the column labels of the DataFrame are taken from the keys of the dictionary.
3. Another thing to notice is that the columns are arranged alphabetically and not in the order given in the dictionary. We will see later that this won't happen when we load data into a DataFrame from a data file.
4. The last thing we want to point out is that we see some `NaN` values appear in the DataFrame. `NaN` stands for *Not a Number*, and is Pandas way of indicating that it doesn't have a value for that particular row and column index. For example, if we look at the column of Alice, we see that it has NaN in the watch index. You can see why this is the case by looking at the dictionary we created at the beginning. We clearly see that the dictionary has no item for Alice labeled watches. So whenever a DataFrame is created, if a particular column doesn't have values for a particular row index, Pandas will put a NaN value there.
5. If we were to feed this data into a machine learning algorithm we will have to remove these NaN values first. In a later lesson, we will learn how to deal with NaN values and clean our data. For now, we will leave these values in our DataFrame.

In the example above, we created a Pandas DataFrame from a dictionary of Pandas Series that had clearly defined indexes. If we don't provide index labels to the Pandas Series, Pandas will use numerical row indexes when it creates the DataFrame. Let's see an example:

### Example 2. DataFrame assigns the numerical row indexes by default.
```python
# We create a dictionary of Pandas Series without indexes
data = {'Bob' : pd.Series([245, 25, 55]),
        'Alice' : pd.Series([40, 110, 500, 45])}

# We create a DataFrame
df = pd.DataFrame(data)

# We display the DataFrame
df
```
>Outputs

![image](assets/images/02.png)

We can see that Pandas indexes the rows of the DataFrame starting from 0, just like NumPy indexes ndarrays.

Now, just like with Pandas Series we can also extract information from DataFrames using attributes. Let's print some information from our `shopping_carts` DataFrame

### Example 3. Demonstrate a few attributes of DataFrame
```python
# We print some information about shopping_carts
print('shopping_carts has shape:', shopping_carts.shape)
print('shopping_carts has dimension:', shopping_carts.ndim)
print('shopping_carts has a total of:', shopping_carts.size, 'elements')
print()
print('The data in shopping_carts is:\n', shopping_carts.values)
print()
print('The row index in shopping_carts is:', shopping_carts.index)
print()
print('The column index in shopping_carts is:', shopping_carts.columns)

# Outputs
shopping_carts has shape: (5, 2)
shopping_carts has dimension: 2
shopping_carts has a total of: 10 elements

The data in shopping_carts is:
[[    500.    245.]
[       40.     nan]
[     110.     nan]
[       45.      25.]
[     nan       55.]]

The row index in shopping_carts is: Index(['bike', 'book', 'glasses', 'pants', 'watch'], dtype='object')

The column index in shopping_carts is: Index(['Alice', 'Bob'], dtype='object')
```

When creating the `shopping_carts` DataFrame we passed the entire dictionary to the `pd.DataFrame()` function. However, there might be cases when you are only interested in a subset of the data. Pandas allows us to select which data we want to put into our DataFrame by means of the keywords columns and index. Let's see some examples:
```python
# We Create a DataFrame that only has Bob's data
bob_shopping_cart = pd.DataFrame(items, columns=['Bob'])

# We display bob_shopping_cart
bob_shopping_cart
```
> Outputs:

![image](assets/images/03.png)

### Example 4. Selecting specific rows of a DataFrame
```python
# We Create a DataFrame that only has selected items for both Alice and Bob
sel_shopping_cart = pd.DataFrame(items, index = ['pants', 'book'])

# We display sel_shopping_cart
sel_shopping_cart
```
> Outputs:

![image](assets/images/04.png)

### Example 5. Selecting specific columns of a DataFrame
```python
# We Create a DataFrame that only has selected items for Alice
alice_sel_shopping_cart = pd.DataFrame(items, index = ['glasses', 'bike'], columns = ['Alice'])

# We display alice_sel_shopping_cart
alice_sel_shopping_cart
```
>Outputs:

![image](assets/images/05.png)

You can also manually create DataFrames from a dictionary of lists (arrays). The procedure is the same as before, we start by creating the dictionary and then passing the dictionary to the `pd.DataFrame()` function. In this case, however, all the lists (arrays) in the dictionary must be of the same length. Let' see an example:

### Example 6. Create a DataFrame using a dictionary of lists
```python
# We create a dictionary of lists (arrays)
data = {'Integers' : [1,2,3],
        'Floats' : [4.5, 8.2, 9.6]}

# We create a DataFrame
df = pd.DataFrame(data)

# We display the DataFrame
df
```

>Outputs:

![image](assets/images/06.png)

The last method for manually creating Pandas DataFrames that we want to look at is by using a list of Python dictionaries. The procedure is the same as before, we start by creating the dictionary and then passing the dictionary to the `pd.DataFrame()` function.

### Example 8. Create a DataFrame using a of list of dictionaries
```python
# We create a list of Python dictionaries
items2 = [{'bikes': 20, 'pants': 30, 'watches': 35},
          {'watches': 10, 'glasses': 50, 'bikes': 15, 'pants':5}]

# We create a DataFrame
store_items = pd.DataFrame(items2)

# We display the DataFrame
store_items
```

>Outputs:

![image](assets/images/07.png)

Again, notice that since the `items2` dictionary we created doesn't have label indices, Pandas automatically uses numerical row indexes when it creates the DataFrame. As before, we can put labels to the row index by using the `index` keyword in the `pd.DataFrame()` function. Let's assume we are going to use this DataFrame to hold the number of items a particular store has in stock. So, we will label the row indices as **store 1** and **store 2**.

### Example 9. Create a DataFrame using a of list of dictionaries, and custom row-indexes (labels)
```python
# We create a list of Python dictionaries
items2 = [{'bikes': 20, 'pants': 30, 'watches': 35},
          {'watches': 10, 'glasses': 50, 'bikes': 15, 'pants':5}]

# We create a DataFrame  and provide the row index
store_items = pd.DataFrame(items2, index = ['store 1', 'store 2'])

# We display the DataFrame
store_items
```

>Outputs:

![image](assets/images/08.png)

### Additional Reading - Pandas Documentation
1. Refer to the [Intro to data structures](https://pandas.pydata.org/pandas-docs/stable/user_guide/dsintro.html#intro-to-data-structures) for an overview of both the data structures - Series and DataFrame.
2. Refer to the **Attributes and underlying data** section in the [DataFrame documentation](https://pandas.pydata.org/pandas-docs/stable/reference/frame.html#dataframe).

## Accessing Elements in Pandas DataFrames

<iframe width="100%" height="379" src="https://www.youtube.com/embed/lClsJnZn_7w" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

We can access elements in Pandas DataFrames in many different ways. In general, we can access rows, columns, or individual elements of the DataFrame by using the row and column labels. We will use the same `store_items` DataFrame created in the previous lesson. Let's see some examples:

### Example 1. Access elements using labels
```python
# We print the store_items DataFrame
print(store_items)

# We access rows, columns and elements using labels
print()
print('How many bikes are in each store:\n', store_items[['bikes']])
print()
print('How many bikes and pants are in each store:\n', store_items[['bikes', 'pants']])
print()
print('What items are in Store 1:\n', store_items.loc[['store 1']])
print()
print('How many bikes are in Store 2:', store_items['bikes']['store 2'])
```
>Outputs:

![image](assets/images/09.png)

![image](assets/images/010.png)

It is important to know that when accessing individual elements in a DataFrame, as we did in the last example above, the labels should always be provided with the column label first, i.e. in the form `dataframe[column][row]`. For example, when retrieving the number bikes in store 2, we first used the column label bikes and then the row label store 2. If you provide the row label first you will get an error.

We can also modify our DataFrames by adding rows or columns. Let's start by learning how to add new columns to our DataFrames. Let's suppose we decided to add shirts to the items we have in stock at each store. To do this, we will need to add a new column to our store_items DataFrame indicating how many shirts are in each store. Let's do that:

### Example 2. Add a column to an existing DataFrame

```python
# We add a new column named shirts to our store_items DataFrame indicating the number of
# shirts in stock at each store. We will put 15 shirts in store 1 and 2 shirts in store 2
store_items['shirts'] = [15,2]

# We display the modified DataFrame
store_items
```
>Outputs:

![image](assets/images/011.png)

We can see that when we add a new column, the new column is added at the end of our DataFrame.

We can also add new columns to our DataFrame by using arithmetic operations between other columns in our DataFrame. Let's see an example:

### Example 3. Add a new column based on the arithmetic operation between existing columns of a DataFrame

```python
# We make a new column called suits by adding the number of shirts and pants
store_items['suits'] = store_items['pants'] + store_items['shirts']

# We display the modified DataFrame
store_items
```

>Outputs:

![image](assets/images/012.png)

Suppose now, that you opened a new store and you need to add the number of items in the stock of that new store into your DataFrame. We can do this by adding a new row to the `store_items` Dataframe. To add rows to our DataFrame we first have to create a new Dataframe and then append it to the original DataFrame. Let's see how this works

### Example 4 a. Create a row to be added to the DataFrame
```python
# We create a dictionary from a list of Python dictionaries that will contain the number of different items at the new store
new_items = [{'bikes': 20, 'pants': 30, 'watches': 35, 'glasses': 4}]

# We create new DataFrame with the new_items and provide and index labeled store 3
new_store = pd.DataFrame(new_items, index = ['store 3'])

# We display the items at the new store
new_store
```

>Outputs:

![image](assets/images/013.png)

We now add this row to our `store_items` DataFrame by using the `.append()` method.

### Example 4 b. Append the row to the DataFrame
```python
# We append store 3 to our store_items DataFrame
store_items = store_items.append(new_store)

# We display the modified DataFrame
store_items
```

>Outputs:

![image](assets/images/014.png)

It is also possible, to insert new columns into the DataFrames anywhere we want. The `dataframe.insert(loc,label,data)` method allows us to insert a new column in the `dataframe` at location `loc`, with the given column `label`, and given `data`. Let's add new column named **shoes** right before the **suits** column. Since **suits** has numerical index value 4 then we will use this value as loc. Let's see how this works:

### Example 6. Add new column at a specific location
```python
# We insert a new column with label shoes right before the column with numerical index 4
store_items.insert(4, 'shoes', [8,5,0])

# we display the modified DataFrame
store_items
```
>Outputs:

![image](assets/images/015.png)

### Example 8. Delete multiple columns from a DataFrame
```python
# We remove the watches and shoes columns
store_items = store_items.drop(['watches', 'shoes'], axis = 1)

# we display the modified DataFrame
store_items
```

>Outputs:

![image](assets/images/016.png)

### Example 9. Delete rows from a DataFrame
```python
# We remove the store 2 and store 1 rows
store_items = store_items.drop(['store 2', 'store 1'], axis = 0)

# we display the modified DataFrame
store_items
```

>Outputs:

![image](assets/images/017.png)

Sometimes we might need to change the row and column labels. Let's change the **bikes** column label to **hats** using the `.rename()` method

###Example 10. Modify the column label
```python
# We change the column label bikes to hats
store_items = store_items.rename(columns = {'bikes': 'hats'})

# we display the modified DataFrame
store_items
```

>Outputs:

![image](assets/images/018.png)

Now let's change the row label using the `.rename()` method again.

### Example 11. Modify the row label
```python
# We change the row label from store 3 to last store
store_items = store_items.rename(index = {'store 3': 'last store'})

# we display the modified DataFrame
store_items
```
>Outputs:

![image](assets/images/019.png)

You can also change the index to be one of the columns in the DataFrame.

### Example 12. Use existing column values as row-index
```python
# We change the row index to be the data in the pants column
store_items = store_items.set_index('pants')

# we display the modified DataFrame
store_items
```
>Outputs:

![image](assets/images/020.png)

## Dealing with NaN

<iframe width="100%" height="384" src="https://www.youtube.com/embed/GS1kj04XQcM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

As mentioned earlier, before we can begin training our learning algorithms with large datasets, we usually need to clean the data first. This means we need to have a method for detecting and correcting errors in our data. While any given dataset can have many types of bad data, such as outliers or incorrect values, the type of bad data we encounter almost always is missing values. As we saw earlier, Pandas assigns `NaN` values to missing data. In this lesson we will learn how to detect and deal with NaN values.

We will begin by creating a DataFrame with some NaN values in it.

### Example 1. Create a DataFrame
```python
# We create a list of Python dictionaries
items2 = [{'bikes': 20, 'pants': 30, 'watches': 35, 'shirts': 15, 'shoes':8, 'suits':45},
{'watches': 10, 'glasses': 50, 'bikes': 15, 'pants':5, 'shirts': 2, 'shoes':5, 'suits':7},
{'bikes': 20, 'pants': 30, 'watches': 35, 'glasses': 4, 'shoes':10}]

# We create a DataFrame  and provide the row index
store_items = pd.DataFrame(items2, index = ['store 1', 'store 2', 'store 3'])

# We display the DataFrame
store_items
```

>Outputs:

![image](assets/images/021.png)

We can clearly see that the DataFrame we created has 3 `NaN` values: one in store 1 and two in store 3. However, in cases where we load very large datasets into a DataFrame, possibly with millions of items, the number of NaN values is not easily visualized. For these cases, we can use a combination of methods to count the number of `NaN` values in our data. The following example combines the `.isnull()` and the `sum()` methods to count the number of `NaN` values in our DataFrame

### Example 2 a. Count the total NaN values
```python
# We count the number of NaN values in store_items
x =  store_items.isnull().sum().sum()

# We print x
print('Number of NaN values in our DataFrame:', x)

#Outputs:

Number of NaN values in our DataFrame: 3
```

In the above example, the `.isnull()` method returns a *Boolean* DataFrame of the same size as `store_items` and indicates with `True` the elements that have `NaN` values and with `False` the elements that are not. Let's see an example:

### Example 2 b. Return boolean True/False for each element if it is a NaN
`store_items.isnull()`

**bikes**|**glasses**|**pants**|**shirts**|**shoes**|**suits**|**watches**
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
store 1|False|True|False|False|False|False
store 2|False|False|False|False|False|False
store 3|False|False|False|True|False|True

In Pandas, logical `True` values have numerical value **1** and logical `False` values have numerical value **0**. Therefore, we can count the number of NaN values by counting the number of logical `True` values. In order to count the total number of logical True values we use the `.sum()` method twice. We have to **use it twice** because the **first sum** returns a Pandas Series with the sums of **logical True values along columns**, as we see below:

### Example 2 c. Count NaN down the column.

`store_items.isnull().sum()`

>Outputs:

bikes          0
glasses        1
pants          0
shirts         1
shoes          0
suits          1
watches        0
dtype: int64

The **second sum** will then **add up the 1s** in the above Pandas Series.

Instead of counting the number of `NaN` values we can also do the opposite, we can count the number of **non-NaN values**. We can do this by using the `.count()` method as shown below:

### Example 3. Count the total non-NaN values
```python
# We print the number of non-NaN values in our DataFrame
print()
print('Number of non-NaN values in the columns of our DataFrame:\n', store_items.count())
```
>Outputs:

Number of non-NaN values in the columns of our DataFrame:
bikes          3
glasses        2
pants          3
shirts         2
shoes          3
suits          2
watches        3
dtype: int64

## Eliminating NaN Values

Now that we learned how to know if our dataset has any `NaN` values in it, the next step is to decide what to do with them. In general, we have two options, we can either delete or replace the NaN values. In the following examples, we will show you how to do both.

We will start by learning how to eliminate rows or columns from our DataFrame that contain any NaN values. The `.dropna(axis)` method eliminates any **rows** with NaN values when **axis = 0** is used and will eliminate any **columns** with NaN values when **axis = 1** is used.

>**Tip**: Remember, you learned that you can read **axis = 0** as "**down**" and **axis = 1** as "**across**" the given Numpy ndarray or Pandas dataframe object.

Let's see some examples.

### Example 4. Drop rows having NaN values
```python
# We drop any rows with NaN values
store_items.dropna(axis = 0)
```
![image](assets/images/022.png)

### Example 5. Drop columns having NaN values
```python
# We drop any columns with NaN values
store_items.dropna(axis = 1)
```

**bikes**|**pants**|**shoes**|**watches**
:-----:|:-----:|:-----:|:-----:
store 1|20|30|8
store 2|15|5|5
store 3|20|30|10

Notice that the `.dropna()` method eliminates (drops) the rows or columns with NaN values **out of place**. This means that the original DataFrame is **not modified**. You can always remove the desired rows or columns in place by setting the keyword **inplace = True** inside the `dropna()` function.

### Substituting NaN Values

Now, instead of eliminating NaN values, we can replace them with suitable values. We could choose for example to replace all NaN values with the value 0. We can do this by using the `.fillna()` method as shown below.

### Example 6. Replace NaN with 0
```python
# We replace all NaN values with 0
store_items.fillna(0)
```

**bikes**|**glasses**|**pants**|**shirts**|**shoes**|**suits**|**watches**
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
store 1|20|0.0|30|15.0|8|45.0
store 2|15|50.0|5|2.0|5|7.0
store 3|20|4.0|30|0.0|10|0.0

We can also use the `.fillna()` method to replace `NaN` values with previous values in the DataFrame, this is known as *forward filling*. When replacing NaN values with forward filling, we can use previous values taken from columns or rows. The `.fillna(method = 'ffill', axis)` will use the forward filling (`ffill`) method to replace `NaN` values using the previous known value along the given axis. Let's see some examples:

### Example 7. Forward fill NaN values down (axis = 0) the dataframe
```python
# We replace NaN values with the previous value in the column
store_items.fillna(method = 'ffill', axis = 0)
```
**bikes**|**glasses**|**pants**|**shirts**|**shoes**|**suits**|**watches**
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
store 1|20|NaN|30|15.0|8|45.0
store 2|15|50.0|5|2.0|5|7.0
store 3|20|4.0|30|2.0|10|7.0

Notice that the two `NaN` values in **store 3** have been replaced with previous values in their columns. However, notice that the `NaN` value in **store 1** didn't get replaced. That's because there are no previous values in this column, since the NaN value is the first value in that column. However, if we do forward fill using the previous row values, this won't happen. Let's take a look:

### Example 8. Forward fill NaN values across (axis = 1) the dataframe
```python
# We replace NaN values with the previous value in the row
store_items.fillna(method = 'ffill', axis = 1)
```

**bikes**|**glasses**|**pants**|**shirts**|**shoes**|**suits**|**watches**
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
store 1|20.0|20.0|30.0|15.0|8.0|45.0
store 2|15.0|50.0|5.0|2.0|5.0|7.0
store 3|20.0|4.0|30.0|30.0|10.0|10.0

We see that in this case all the NaN values have been replaced with the **previous row values**.

Similarly, you can choose to replace the NaN values with the values that go after them in the DataFrame, this is known as *backward filling*. The `.fillna(method = 'backfill', axis)` will use the backward filling (backfill) method to replace `NaN` values using the **next known value** along the given axis. Just like with forward filling we can choose to use row or column values. Let's see some examples:

### Example 9. Backward fill NaN values down (axis = 0) the dataframe

```python
# We replace NaN values with the next value in the column
store_items.fillna(method = 'backfill', axis = 0)
```

**bikes**|**glasses**|**pants**|**shirts**|**shoes**|**suits**|**watches**
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
store 1|20|50.0|30|15.0|8|45.0
store 2|15|50.0|5|2.0|5|7.0
store 3|20|4.0|30|NaN|10|NaN

Notice that the `NaN` value in **store 1** has been replaced with the next value in its column. However, notice that the two `NaN` values in **store 3** didn't get replaced. That's because there are no next values in these columns, since these NaN values are the last values in those columns. However, if we do backward fill using the next row values, this won't happen. Let's take a look:

### Example 10. Backward fill NaN values across (axis = 1) the dataframe
```python
# We replace NaN values with the next value in the row
store_items.fillna(method = 'backfill', axis = 1)
```

**bikes**|**glasses**|**pants**|**shirts**|**shoes**|**suits**|**watches**
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
store 1|20.0|30.0|30.0|15.0|8.0|45.0
store 2|15.0|50.0|5.0|2.0|5.0|7.0
store 3|20.0|4.0|30.0|10.0|10.0|35.0

Notice that the `.fillna()` method replaces (fills) the `NaN` values out of place. This means that the **original DataFrame is not modified**. You can always replace the NaN values in place by setting the keyword `inplace = True` inside the `fillna()` function.

We can also choose to replace `NaN` values by using different interpolation methods. For example, the `.interpolate(method = 'linear', axis)` method will use `linear` interpolation to replace NaN values using the values along the given axis. Let's see some examples:

### Example 11. Interpolate (estimate) NaN values down (axis = 0) the dataframe
```python
# We replace NaN values by using linear interpolation using column values
store_items.interpolate(method = 'linear', axis = 0)
```

**bikes**|**glasses**|**pants**|**shirts**|**shoes**|**suits**|**watches**
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
store 1|20|NaN|30|15.0|8|45.0
store 2|15|50.0|5|2.0|5|7.0
store 3|20|4.0|30|2.0|10|7.0

Notice that the two `NaN` values in **store 3** have been replaced with linear interpolated values. However, notice that the `NaN` value in **store 1** didn't get replaced. That's because the NaN value is the first value in that column, and since there is no data before it, the interpolation function can't calculate a value. Now, let's interpolate using row values instead:

### Example 12. Interpolate (estimate) NaN values across (axis = 1) the dataframe
```python
# We replace NaN values by using linear interpolation using row values
store_items.interpolate(method = 'linear', axis = 1)
```

**bikes**|**glasses**|**pants**|**shirts**|**shoes**|**suits**|**watches**
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
store 1|20.0|25.0|30.0|15.0|8.0|45.0
store 2|15.0|50.0|5.0|2.0|5.0|7.0
store 3|20.0|4.0|30.0|20.0|10.0|22.5

Just as with the other methods we saw, the `.interpolate()` method replaces `NaN` values out of place.

## Loading Data into a pandas DataFrame

<iframe width="100%" height="412" src="https://www.youtube.com/embed/ruTYp-twXO0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

In machine learning you will most likely use databases from many sources to train your learning algorithms. Pandas allows us to load databases of different formats into DataFrames. One of the most popular data formats used to store databases is csv. CSV stands for Comma Separated Values and offers a simple format to store data. We can load CSV files into Pandas DataFrames using the `pd.read_csv()` function. Let's load Google stock data into a Pandas DataFrame. The GOOG.csv file contains Google stock data from 8/19/2004 till 10/13/2017 taken from Yahoo Finance.

### Example 1. Load the data from a .csv file.
```python
# We load Google stock data in a DataFrame
Google_stock = pd.read_csv('./GOOG.csv')

# We print some information about Google_stock
print('Google_stock is of type:', type(Google_stock))
print('Google_stock has shape:', Google_stock.shape)

# Outputs:

Google_stock is of type: class 'pandas.core.frame.DataFrame'
Google_stock has shape: (3313, 7)
```
We see that we have loaded the GOOG.csv file into a Pandas DataFrame and it consists of 3,313 rows and 7 columns. Now let's look at the stock data

### Example 2. Look at the first few rows of the DataFrame
`Google_stock`

**Date**|**Open**|**High**|**Low**|**Close**|**Adj Close**|**Volume**
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
0|2004-08-19|49.676899|51.693783|47.669952|49.845802|49.845802
1|2004-08-20|50.178635|54.187561|49.925285|53.805050|53.805050
2|2004-08-23|55.017166|56.373344|54.172661|54.346527|54.346527
3311|2017-10-12|987.450012|994.119995|985.000000|987.830017|987.830017
3312|2017-10-13|992.000000|997.210022|989.000000|989.679993|989.679993

>3313 rows × 7 columns

We see that it is quite a large dataset and that Pandas has automatically assigned numerical row indices to the DataFrame. Pandas also used the labels that appear in the data in the CSV file to assign the column labels.

When dealing with large datasets like this one, it is often useful just to take a look at the first few rows of data instead of the whole dataset. We can take a look at the first 5 rows of data using the .head() method, as shown below

### Example 3. Look at the first 5 rows of the DataFrame

`Google_stock.head()`

**Date**|**Open**|**High**|**Low**|**Close**|**Adj Close**|**Volume**
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
0|2004-08-19|49.676899|51.693783|47.669952|49.845802|49.845802
1|2004-08-20|50.178635|54.187561|49.925285|53.805050|53.805050
2|2004-08-23|55.017166|56.373344|54.172661|54.346527|54.346527
3|2004-08-24|55.260582|55.439419|51.450363|52.096165|52.096165
4|2004-08-25|52.140873|53.651051|51.604362|52.657513|52.657513

We can also take a look at the last 5 rows of data by using the .tail() method:

### Example 4. Look at the last 5 rows of the DataFrame
`Google_stock.tail()`

**Date**|**Open**|**High**|**Low**|**Close**|**Adj Close**|**Volume**
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
3308|2017-10-09|980.000000|985.424988|976.109985|977.000000|977.000000
3309|2017-10-10|980.000000|981.570007|966.080017|972.599976|972.599976
3310|2017-10-11|973.719971|990.710022|972.250000|989.250000|989.250000
3311|2017-10-12|987.450012|994.119995|985.000000|987.830017|987.830017
3312|2017-10-13|992.000000|997.210022|989.000000|989.679993|989.679993

We can also optionally use `.head(N)` or `.tail(N)` to display the first and last N rows of data, respectively.

Let's do a quick check to see whether we have any `NaN` values in our dataset. To do this, we will use the `.isnull()` method followed by the `.any()` method to check whether any of the columns contain NaN values.

### Example 5. Check if any column contains a NaN. Returns a boolean for each column label.
`Google_stock.isnull().any()`

Date                False
Open                False
High                False
Low                 False
Close               False
Adj Close           False
Volume              False
dtype: bool

We see that we have no NaN values.

When dealing with large datasets, it is often useful to get statistical information from them. Pandas provides the `.describe()` method to get descriptive statistics on each column of the DataFrame. Let's see how this works:

### Example 6. See the descriptive statistics of the DataFrame
```python
# We get descriptive statistics on our stock data
Google_stock.describe()
```

**Open**|**High**|**Low**|**Close**|**Adj Close**|**Volume**
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
count|3313.000000|3313.000000|3313.000000|3313.000000|3313.000000
mean|380.186092|383.493740|376.519309|380.072458|380.072458
std|223.818650|224.974534|222.473232|223.853780|223.853780
min|49.274517|50.541279|47.669952|49.681866|49.681866
25%|226.556473|228.394516|224.003082|226.407440|226.407440
50%|293.312286|295.433502|289.929291|293.029114|293.029114
75%|536.650024|540.000000|532.409973|536.690002|536.690002
max|992.000000|997.210022|989.000000|989.679993|989.679993

If desired, we can apply the `.describe()` method on a single column as shown below:

### Example 7. See the descriptive statistics of one of the columns of the DataFrame
```python
# We get descriptive statistics on a single column of our DataFrame
Google_stock['Adj Close'].describe()
```
count         3313.000000
mean          380.072458
std           223.853780
min           49.681866
25%           226.407440
50%           293.029114
75%           536.690002
max           989.679993
Name: Adj Close, dtype: float64

Similarly, you can also look at one statistic by using one of the many statistical functions Pandas provides. Let's look at some examples:

### Example 8. Statistical operations - Min, Max, and Mean
```python
# We print information about our DataFrame  
print()
print('Maximum values of each column:\n', Google_stock.max())
print()
print('Minimum Close value:', Google_stock['Close'].min())
print()
print('Average value of each column:\n', Google_stock.mean())

#Outputs:

Maximum values of each column:
Date            2017-10-13
Open            992
High            997.21
Low             989
Close           989.68
Adj Close       989.68
Volume          82768100
dtype: object

Minimum Close value: 49.681866

Average value of each column:
Open            3.801861e+02
High            3.834937e+02
Low             3.765193e+02
Close           3.800725e+02
Adj Close       3.800725e+02
Volume          8.038476e+06
dtype: float64

```
Another important statistical measure is **data correlation**. Data correlation can tell us, for example, if the data in different columns are correlated. We can use the `.corr()` method to get the correlation between different columns, as shown below:

### Example 9. Statistical operation - Correlation
```python
# We display the correlation between columns
Google_stock.corr()
```

**Open**|**High**|**Low**|**Close**|**Adj Close**|**Volume**
:-----:|:-----:|:-----:|:-----:|:-----:|:-----:
Open|1.000000|0.999904|0.999845|0.999745|0.999745
High|0.999904|1.000000|0.999834|0.999868|0.999868
Low|0.999845|0.999834|1.000000|0.999899|0.999899
Close|0.999745|0.999868|0.999899|1.000000|1.000000
Adj Close|0.999745|0.999868|0.999899|1.000000|1.000000
Volume|-0.564258|-0.562749|-0.567007|-0.564967|-0.564967

A correlation value of 1 tells us there is a high correlation and a correlation of 0 tells us that the data is not correlated at all.

### `groupby()` method

We will end this Introduction to Pandas by taking a look at the `.groupby()` method. The `.groupby()` method allows us to group data in different ways. Let's see how we can group data to get different types of information. For the next examples, we are going to load fake data about a fictitious company.
```python
# We load fake Company data in a DataFrame
data = pd.read_csv('./fake_company.csv')

data
```

**Year**|**Name**|**Department**|**Age**|**Salary**
:-----:|:-----:|:-----:|:-----:|:-----:
0|1990|Alice|HR|25
1|1990|Bob|RD|30
2|1990|Charlie|Admin|45
3|1991|Dakota|HR|26
4|1991|Elsa|RD|31
5|1991|Frank|Admin|46
6|1992|Grace|Admin|27
7|1992|Hoffman|RD|32
8|1992|Inaar|Admin|28

We see that the data contains information for the year 1990 through 1992. For each year we see name of the employees, the department they work for, their age, and their annual salary. Now, let's use the `.groupby()` method to get information.

### Example 10. Demonstrate groupby() and sum() method

Let's calculate how much money the company spent on salaries each year. To do this, we will group the data by Year using the `.groupby()` method and then we will add up the salaries of all the employees by using the `.sum()` method.
```python
# We display the total amount of money spent in salaries each year
data.groupby(['Year'])['Salary'].sum()
```
Year
1990     153000
1991     162000
1992     174000
Name: Salary, dtype: int64

We see that the average salary in 1990 was 51,000 dollars, 54,000 in 1991, and 58,000 in 1992.

### Example 12. Demonstrate groupby() on single column

Now let's see how much did each employee gets paid in those three years. In this case, we will group the data by Name using the `.groupby()` method and then we will add up the salaries for each year. Let's see the result
```python
# We display the total salary each employee received in all the years they worked for the company
data.groupby(['Name'])['Salary'].sum()
```
Name
Alice         162000
Bob          150000
Charlie     177000
Name: Salary, dtype: int64

We see that Alice received a total of 162,000 dollars in the three years she worked for the company, Bob received 150,000, and Charlie received 177,000.

### Example 13. Demonstrate groupby() on two columns

Now let's see what was the salary distribution per department per year. In this case, we will group the data by Year and by Department using the `.groupby()` method and then we will add up the salaries for each department. Let's see the result
```python
# We display the salary distribution per department per year.
data.groupby(['Year', 'Department'])['Salary'].sum()
```
Year     Department
1990    Admin              55000
             HR                    50000
             RD                    48000
1991    Admin              60000
             HR                    52000
             RD                    50000
1992    Admin            122000
             RD                    52000
Name: Salary, dtype: int64

We see that in 1990 the Admin department paid 55,000 dollars in salaries,the HR department paid 50,000, and the RD department 48,0000. While in 1992 the Admin department paid 122,000 dollars in salaries and the RD department paid 52,000.

### Recommended Practice
We recommend you practice the examples available at the [10 minutes to pandas](https://pandas.pydata.org/pandas-docs/stable/user_guide/10min.html) as a conclusive tutorial.
