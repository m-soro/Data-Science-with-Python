---
layout: default
title: Functions
parent:  Introduction to Python programming
grand_parent: Modules
nav_order: 4
---

# Functions

<iframe width="100%" height="433" src="https://www.youtube.com/embed/IP_tJYhynbc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Defining Functions

**Example of a function definition:**

```python
def cylinder_volume(height, radius):
    pi = 3.14159
    return height * pi * radius ** 2
```
After defining the `cylinder_volume` function, we can call the function like this.

`cylinder_volume(10, 3)`

This is called a **function call** statement.

A function definition includes several important parts.

**Function Header**

Let's start with the function header, which is the first line of a function definition.

1. The function header always starts with the `def` keyword, which indicates that this is a **function definition**.
2. Then comes the **function name** (here, cylinder_volume), which follows the same naming conventions as variables. You can revisit the naming conventions below.
3. Immediately after the name are parentheses that may include arguments separated by commas (here, height and radius). **Arguments**, or **parameters**, are values that are passed in as inputs when the function is called, and are used in the function body. If a function doesn't take arguments, these parentheses are left empty.
4. The header always end with a colon `:`.

**Function Body**

The rest of the function is contained in the body, which is where the function does its work.

1. The **body** of a function is the code indented after the header line. Here, it's the two lines that define `pi` and `return` the volume.
2. Within this body, we can refer to the **argument variables** and define new variables, which can only be used within these indented lines.
3. The body will often include a `return` statement, which is used to send back an output value from the function to the statement that called the function. A `return` statement consists of the `return` keyword followed by an expression that is evaluated to get the output value for the function. If there is no return statement, the function simply returns `None`.


**Naming Conventions for Functions**

Function names follow the same naming conventions as variables.

1. Only use ordinary letters, numbers and underscores in your function names. They can’t have spaces, and need to start with a letter or underscore.
2. You can’t use reserved words or built-in identifiers that have important purposes in Python, which you’ll learn about throughout this course. A list of Python reserved words is described [here](https://pentangle.net/python/handbook/node52.html).
3. Try to use descriptive names that can help readers understand what the function does.

## Default Arguments

<iframe width="100%" height="433" src="https://www.youtube.com/embed/cG6UfBZX2KI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

We can add default arguments in a function to have default values for parameters that are unspecified in a function call.

```python
def cylinder_volume(height, radius=5):
    pi = 3.14159
    return height * pi * radius ** 2
```

In the example above, `radius` is set to 5 if that parameter is omitted in a function call. If we call `cylinder_volume(10)`, the function will use 10 as the height and 5 as the radius. However, if we call `cylinder_volume(10, 7)` the 7 will simply overwrite the default value of 5.

Also notice here we are passing values to our arguments by position. It is possible to pass values in two ways - by **position** and by **name**. Each of these function calls are evaluated the same way.

```python
cylinder_volume(10, 7)  # pass in arguments by position
cylinder_volume(height=10, radius=7)  # pass in arguments by name
```

## Variable Scope

<iframe width="100%" height="433" src="https://www.youtube.com/embed/rYubQlAM-gw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

**Variable Scope**

Variable scope refers to which parts of a program a variable can be referenced, or used, from.

It's important to consider scope when using variables in functions. If a variable is created inside a function, it can only be used within that function. Accessing it outside that function is not possible.

```python
# This will result in an error
def some_function():
    word = "hello"

print(word)
```

In the example above and the example below, word is said to have scope that is only **local** to each function. This means you can use the same name for different variables that are used in different functions.

```python
# This works fine
def some_function():
    word = "hello"

def another_function():
    word = "goodbye"
```    

Variables defined outside functions, as in the example below, can still be accessed within a function. Here, word is said to have a **global scope**.

```python
# This works fine
word = "hello"

def some_function():
    print(word)

some_function()
```

Notice that we can still access the value of the global variable word within this function. However, **the value of a global variable can not be modified inside the function**. If you want to modify that variable's value inside this function, it should be passed in as an argument.

Scope is essential to understanding how information is passed throughout programs in Python and really any programming language.

**More on Variable Scope**
When you program, you'll often find that similar ideas come up again and again. You'll use variables for things like counting, iterating and accumulating values to return. In order to write readable code, you'll find yourself wanting to use similar names for similar ideas. As soon as you put multiple piece of code together (for instance, multiple functions or function calls in a single script) you might find that you want to use the same name for two separate concepts.

Fortunately, you don't need to come up with new names endlessly. Reusing names for objects is OK as long as you keep them in separate scope.

**Good practice:** It is best to define variables in the smallest scope they will be needed in. While functions can refer to variables defined in a larger scope, this is very rarely a good idea since you may not know what variables you have defined if your program has a lot of variables.

```python
egg_count = 0

def buy_eggs():
    egg_count += 12 # purchase a dozen eggs

buy_eggs()
```

This code causes an `UnboundLocalError`, because the variable `egg_count` in the first line has global scope. Note that it is not passed as an argument into the function, so the function assumes the egg_count being referred to is the global variable.

In the last video, you saw that within a function, we can print a global variable's value successfully without an error. This worked because we were simply accessing the value of the variable. If we try to **change** or **reassign** this global variable, however, as we do in this code, we get an error. Python doesn't allow functions to modify variables that aren't in the function's scope.

A better way to write this would be:

```python
egg_count = 0

def buy_eggs(count):
    return count + 12  # purchase a dozen eggs

egg_count = buy_eggs(egg_count)
```

## Documentation

<iframe width="100%" height="527" src="https://www.youtube.com/embed/_Vl9NJkA6JQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

**Documentation**

Documentation is used to make your code easier to understand and use. Functions are especially readable because they often use documentation strings, or `docstrings`. Docstrings are a type of comment used to explain the purpose of a function, and how it should be used. Here's a function for population density with a docstring.

```python
def population_density(population, land_area):
    """Calculate the population density of an area. """
    return population / land_area
```

Docstrings are surrounded by triple quotes. The first line of the docstring is a brief explanation of the function's purpose. If you feel that this is sufficient documentation you can end the docstring at this point; single line docstrings are perfectly acceptable, as in the example above.

```python
def population_density(population, land_area):
    """Calculate the population density of an area.

    INPUT:
    population: int. The population of that area
    land_area: int or float. This function is unit-agnostic, if you pass in values in terms
    of square km or square miles the function will return a density in those units.

    OUTPUT:
    population_density: population / land_area. The population density of a particular area.
    """
    return population / land_area
```

If you think that a longer description would be appropriate for the function, you can add more information after the one-line summary. In the example above, you can see that we wrote an explanation of the function's arguments, stating the purpose and types of each one. It's also common to provide some description of the function's output.

Every piece of the docstring is optional, however, docstrings are a part of good coding practice. You can read more about docstring conventions [here](https://www.python.org/dev/peps/pep-0257).

## Lambda Expressions

<iframe width="100%" height="527" src="https://www.youtube.com/embed/wkEmPz1peJM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

**Lambda Expressions**

You can use lambda expressions to create **anonymous functions**. That is, functions that don’t have a name. They are helpful for creating quick functions that aren’t needed later in your code. This can be especially useful for higher order functions, or functions that take in other functions as arguments.

With a lambda expression, this function:

```python
def multiply(x, y):
    return x * y
```

can be reduced to:

```python
multiply = lambda x, y: x * y
```

Both of these functions are used in the same way. In either case, we can call multiply like this:

```python
multiply(4, 7)
```

This returns 28.

**Components of a Lambda Function**

1. The `lambda` keyword is used to indicate that this is a lambda expression.
2. Following `lambda` are one or more arguments for the anonymous function separated by commas, followed by a colon `:`. Similar to functions, the way the arguments are named in a lambda expression is arbitrary.
3. Last is an expression that is evaluated and returned in this function. This is a lot like an expression you might see as a return statement in a function.

With this structure, lambda expressions aren’t ideal for complex functions, but can be very useful for short, simple functions.

### Quiz: Lambda with `Map`

`map()` is a higher-order built-in function that takes a function and iterable as inputs, and returns an iterator that applies the function to each element of the iterable. The code below uses `map()` to find the mean of each list in `numbers` to create the list `averages`. Give it a test run to see what happens.

Rewrite this code to be more concise by replacing the `mean` function with a lambda expression defined within the call to `map()`.

```python

numbers = [
              [34, 63, 88, 71, 29],
              [90, 78, 51, 27, 45],
              [63, 37, 85, 46, 22],
              [51, 22, 34, 11, 18]
           ]

# def mean(num_list):
    # return sum(num_list) / len(num_list)

mean = lambda num_list: sum(num_list) / len(num_list)


averages = list(map(mean, numbers))
print(averages)

```

### Quiz: Lambda with `Filter`

`filter()` is a higher-order built-in function that takes a function and iterable as inputs and returns an iterator with the elements from the iterable for which the function returns True. The code below uses `filter()` to get the names in `cities` that are fewer than 10 characters long to create the list `short_cities`. Give it a test run to see what happens.

Rewrite this code to be more concise by replacing the `is_short` function with a lambda expression defined within the call to `filter()`.

```python

cities = ["New York City", "Los Angeles", "Chicago", "Mountain View", "Denver", "Boston"]

# def is_short(name):
    # return len(name) < 10

is_short = lambda name: len(name) < 10

short_cities = list(filter(is_short, cities))
print(short_cities)

```

<iframe width="100%" height="273" src="https://www.youtube.com/embed/QRnLr7pwHyk" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

**Additional Resources**

* If you want to learn more about writing functions, check out [this talk from PyCon](https://youtu.be/rrBJVMyD-Gs) by Jack Diederich. Diederich covers best practices for writing functions in Python that also apply to all code in Python.

* [Here's a great blog post](https://jeffknupp.com/blog/2013/04/07/improve-your-python-yield-and-generators-explained/) about `yield` and generators from Jeff Knupp.

[:arrow_up:](#)
