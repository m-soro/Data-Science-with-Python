---
layout: default
title: Data Types and Operators
parent:  Introduction to Python programming
grand_parent: Modules
nav_order: 2
---

# Data Types and Operators

You'll learn about:

* Data Types: Integers, Floats, Booleans, Strings
* Operators: Arithmetic, Assignment, Comparison, Logical
* Built-In Functions, Type Conversion
* Whitespace and Style Guidelines

### Arithmetic Operators

* `+` Addition
* `-` Subtraction
* `*` Multiplication
* `/` Division
* `%` Mod (the remainder after dividing)
* `**` Exponentiation (note that `^` does not do this operation, as you might have seen in other languages)
* `//` Divides and rounds down to the nearest integer

The usual order of mathematical operations holds in Python, which you can review in this Math Forum [page](http://mathforum.org/dr.math/faq/faq.order.operations.html) if needed.

**Bitwise operators** are special operators in Python that you can learn more about [here](https://wiki.python.org/moin/BitwiseOperators) if you'd like.

**Quiz: Average Electricity Bill**
It's time to try a calculation in Python!

My electricity bills for the last three months have been $23, $32 and $64. What is the average monthly electricity bill over the three month period? Write an expression to calculate the mean, and use print() to view the result.

**Quiz: Calculate**
In this quiz you're going to do some calculations for a tiler. Two parts of a floor need tiling. One part is 9 tiles wide by 7 tiles long, the other is 5 tiles wide by 7 tiles long. Tiles come in packages of 6.

How many tiles are needed?
You buy 17 packages of tiles containing 6 tiles each. How many tiles will be left over?

Fill this in with an expression that calculates how many tiles are needed.

Fill this in with an expression that calculates how many tiles will be left over.


> Quiz answers are in the python scripts tab

### Variables and Assignment Operators

<iframe width="560" height="315" src="https://www.youtube.com/embed/7pxpUot4x0w" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

**Variables I**

Variables are used all the time in Python! Below is the example you saw in the video where we performed the following:

`mv_population = 74728`

Here `mv_population` is a variable, which holds the value of `74728`. This assigns the item on the right to the name on the left, which is actually a little different than mathematical equality, as 74728 does not hold the value of `mv_population`.

In any case, whatever term is on the left side, is now a name for whatever value is on the right side. Once a value has been assigned to a variable name, you can access the value from the variable name.

**Variables II**

<iframe width="560" height="315" src="https://www.youtube.com/embed/4IJqbP8vi6A" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

In this video you saw that the following two are equivalent in terms of assignment:

```
  x = 3
  y = 4
  z = 5
```
and
`x, y, z = 3, 4, 5`

However, the above isn't a great way to assign variables in most cases, because our variable names should be descriptive of the values they hold.

Besides writing variable names that are descriptive, there are a few things to watch out for when naming variables in Python.

1. Only use ordinary letters, numbers and underscores in your variable names. They can’t have spaces, and need to start with a letter or underscore.

2. You can’t use reserved words or built-in identifiers that have important purposes in Python, which you’ll learn about throughout this course. A list of python reserved words is described here. Creating names that are descriptive of the values often will help you avoid using any of these words. A quick table of these words is also available below.

![image](https://video.udacity-data.com/topher/2018/January/5a71131d_screen-shot-2018-01-30-at-4.39.42-pm/screen-shot-2018-01-30-at-4.39.42-pm.png)

3. The pythonic way to name variables is to use all lowercase letters and underscores to separate words.

YES
```
  my_height = 58
  my_lat = 40
  my_long = 105
```

NO
```
  my height = 58
  MYLONG = 40
  MyLat = 105
```

Though the last two of these would work in python, they are not pythonic ways to name variables. The way we name variables is called snake case, because we tend to connect the words with underscores.

<iframe width="560" height="315" src="https://www.youtube.com/embed/p_qfzL-x3Cs" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Assignment Operators
Below are the assignment operators from the video. You can also use `*=` in a similar way, but this is less common than the operations shown below. You can find some practice with much of what we have already covered [here](https://www.programiz.com/python-programming/operators).

![image](https://video.udacity-data.com/topher/2018/January/5a7118b3_screen-shot-2018-01-30-at-5.14.39-pm/screen-shot-2018-01-30-at-5.14.39-pm.png)

**Quiz: Assign and Modify Variables**

Now it's your turn to work with variables. The comments in this quiz (the lines that begin with #) have instructions for creating and modifying variables. After each comment write a line of code that implements the instruction.

Note that this code uses [scientific notation](https://en.wikipedia.org/wiki/Scientific_notation) to define large numbers. `4.445e8` is equal to `4.445 * 10 ** 8` which is equal to `444500000.0`.

The current volume of a water reservoir (in cubic metres)
reservoir_volume = 4.445e8
The amount of rainfall from a storm (in cubic metres)
rainfall = 5e6

decrease the rainfall variable by 10% to account for runoff

add the rainfall variable to the reservoir_volume variable

increase reservoir_volume by 5% to account for stormwater that flows
into the reservoir in the days following the storm

decrease reservoir_volume by 5% to account for evaporation

subtract 2.5e5 cubic metres from reservoir_volume to account for water
that's piped to arid regions.

print the new value of the reservoir_volume variable

> Quiz answers are in the python scripts tab

## Integers and Floats

<iframe width="560" height="315" src="https://www.youtube.com/embed/MiJ1vfWp-Ts" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Integers and Floats
There are two Python data types that could be used for numeric values:

* **int** - for integer values
* **float** - for decimal or floating point values

You can create a value that follows the data type by using the following syntax:

```
  x = int(4.7)   # x is now an integer 4
  y = float(4)   # y is now a float of 4.0
```
You can check the type by using the `type` function:

```
  >>> print(type(x))
  int
  >>> print(type(y))
  float
```

Because the float, or approximation, for 0.1 is actually slightly more than 0.1, when we add several of them together we can see the difference between the mathematically correct answer and the one that Python creates.

```
  >>> print(.1 + .1 + .1 == .3)
  False
```

You can see more on this [here](https://docs.python.org/3/tutorial/floatingpoint.html).

<iframe width="770" height="433" src="https://www.youtube.com/embed/UxkIwcOczQQ" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

**Python Best Practices**
For all the best practices, see the [PEP8 Guidelines](https://www.python.org/dev/peps/pep-0008/).

You can use the atom package [linter-python-pep8](https://atom.io/packages/linter-python-pep8) to use pep8 within your own programming environment in the Atom text editor, but more on this later. If you aren't familiar with text editors yet, and you are performing all of your programming in the classroom, no need to worry about this right now.

Follow these guidelines to make other programmers and future you happy!

**Divide By Zero?**

```
  Traceback (most recent call last):
    File "/tmp/vmuser_tnryxwdmhw/quiz.py", line 1, in <module>
      print(5/0)

  ZeroDivisionError: division by zero
```

Traceback means "What was the programming doing when it broke"! This part is usually less helpful than the very last line of your error. Though you can dig through the rest of the error, looking at just the final line `ZeroDivisionError`, and the message says we divided by zero. Python is enforcing the rules of arithmetic!

In general, there are two types of errors to look out for

* Exceptions
* Syntax

An **Exception** is a problem that occurs when the code is running, but a 'Syntax Error' is a problem detected when Python checks the code before it runs it. For more information, see the Python tutorial page on [Errors and Exceptions](https://docs.python.org/3/tutorial/errors.html).

## Booleans, Comparison Operators, and Logical Operators

<iframe width="491" height="276" src="https://www.youtube.com/embed/iNNsUJIDtVU" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

The bool data type holds one of the values `True` or `False`, which are often encoded as `1` or `0`, respectively.

There are 6 comparison operators that are common to see in order to obtain a bool value:

**Comparison Operators**

|Symbol Use Case	| Bool | Operation|
|----------------|------|----------
|5 < 3	| False	| Less Than |
|5 > 3	| True	| Greater Than |
|3 <= 3	| True	| Less Than or Equal To |
|3 >= 5	| False	| Greater Than or Equal To |
|3 == 5	| False	| Equal To |
|3 != 5	| True	| Not Equal To |

And there are three logical operators you need to be familiar with:

| Logical Use	| Bool	| Operation |
|-------------|-------|-----------|
| 5 < 3 and 5 == 5	| False | 	`and` - Evaluates if all provided statements are True |
| 5 < 3 or 5 == 5	| True |	`or` - Evaluates if at least one of many statements is True |
| not 5 < 3	| True |	`not` - Flips the Bool Value |

[Here](https://www.irishtimes.com/news/science/how-george-boole-s-zeroes-and-ones-changed-the-world-1.2014673) is more information on how George Boole changed the world!

**Quiz: Which is denser, Rio or San Francisco?**

Try comparison operators in this quiz! This code calculates the population densities of Rio de Janeiro and San Francisco.

Write code to compare these densities. Is the population of San Francisco more dense than that of Rio de Janeiro? Print True if it is and False if not.

sf_population, sf_area = 864816, 231.89
rio_population, rio_area = 6453682, 486.5

san_francisco_pop_density = sf_population/sf_area
rio_de_janeiro_pop_density = rio_population/rio_area

Write code that prints `True` if San Francisco is denser than Rio, and `False` otherwise

> Quiz answers are in the python scripts tab

## Strings

<iframe width="459" height="258" src="https://www.youtube.com/embed/ySZDrs-nNqg" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

In the video above, at the 1:32 mark, the `str` is written as follows `salesman = '"I think you\'re an encyclopedia salesman'"`, but the closing string literals should be double quotes `"` followed by single quotes `'`.

**Strings**

Strings in Python are shown as the variable type `str`. You can define a string with either double quotes `"` or single quotes `'`. If the string you are creating actually has one of these two values in it, then you need to be careful to assure your code doesn't give an error.

```
  >>> my_string = 'this is a string!'
  >>> my_string2 = "this is also a string!!!"
```

You can also include a `\` in your string to be able to include one of these quotes:

```
  >>> this_string = 'Simon\'s skateboard is in the garage.'
  >>> print(this_string)

  Simon's skateboard is in the garage.
```
If we don't use this, notice we get the following error:

```
  >>> this_string = 'Simon's skateboard is in the garage.'
    File "<ipython-input-20-e80562c2a290>", line 1
      this_string = 'Simon's skateboard is in the garage.'
                           ^
  SyntaxError: invalid syntax
```

The color highlighting is also an indication of the error you have in your string in this second case. There are a number of other operations you can use with strings as well. In this video you saw a few:

```
  >>> first_word = 'Hello'
  >>> second_word = 'There'
  >>> print(first_word + second_word)

  HelloThere

  >>> print(first_word + ' ' + second_word)

  Hello There

  >>> print(first_word * 5)

  HelloHelloHelloHelloHello

  >>> print(len(first_word))

  5
```

Unlike the other data types you have seen so far, you can also index into strings, but you will see more on this soon! For now, here is a small example. Notice Python uses 0 indexing - we will discuss this later in this lesson in detail.

```
  >>> first_word[0]

  H

  >>> first_word[1]

  e
```

**The `len()` function**
`len()` is a built-in Python function that returns the length of an object, like a string. The length of a string is the number of characters in the string. This will always be an integer.

There is an example above, but here's another one:
```
  print(len("ababa") / len("ab"))
  2.5
```
You know what the data types are for len("ababa") and len("ab"). Notice the data type of their resulting quotient here.

**Quiz: Fix the Quote**

# TODO: Fix this string!
ford_quote = 'Whether you think you can, or you think you can't--you're right.'

**Quiz: Write a Server Log Message**
In this programming quiz, you’re going to use what you’ve learned about strings to write a logging message for a server.

You’ll be provided with example data for a user, the time of their visit and the site they accessed. You should use the variables provided and the techniques you’ve learned to print a log message like this one (with the username, url, and timestamp replaced with values from the appropriate variables):

`Yogesh accessed the site http://petshop.com/pets/reptiles/pythons at 16:20`.

Use the Test Run button to see your results as you work on coding this piece by piece.

username = "Kinari"
timestamp = "04:50"
url = "http://petshop.com/pets/mammals/cats"

TODO: print a log message using the variables above.
The message should have the same format as this one:
`Yogesh accessed the site http://petshop.com/pets/reptiles/pythons at 16:20.`

**Quiz: len()**
Use string concatenation and the len() function to find the length of a certain movie star's actual full name. Store that length in the name_length variable. Don't forget that there are spaces in between the different parts of a name!

given_name = "William"
middle_names = "Bradley"
family_name = "Pitt"

name_length = #todo: calculate how long this name is

Now we check to make sure that the name fits within the driving license character limit
Nothing you need to do here
driving_license_character_limit = 28
print(name_length <= driving_license_character_limit)

> Quiz answers are in python scripts tab

## Type and Type Conversion

<iframe width="810" height="456" src="https://www.youtube.com/embed/yN6Fam_vZrU" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

**Type And Type Conversion**

You have seen four data types so far:

1. int
2. float
3. bool
4. string

You got a quick look at `type()` from an earlier video, and it can be used to check the data type of any variable you are working with.
```
  >>> print(type(4))
  int
  >>> print(type(3.7))
  float
  >>> print(type('this'))
  str
  >>> print(type(True))
  bool
```
You saw that you can change variable types to perform different operations. For example,

`"0" + "5"`
provides completely different output than

`0 + 5`
What do you think the below would provide?

`"0" + 5`
How about the code here:

`0 + "5"`

Checking your variable types is really important to assure that you are retrieving the results you want when programming.

**Quiz: Total Sales**

In this quiz, you’ll need to change the types of the input and output data in order to get the result you want.

Calculate and print the total sales for the week from the data provided. Print out a string of the form `"This week's total sales: xxx"`, where xxx will be the actual total of all the numbers. You’ll need to change the type of the input data in order to calculate that total.

```
  mon_sales = "121"
  tues_sales = "105"
  wed_sales = "110"
  thurs_sales = "98"
  fri_sales = "95"

  #TODO: Print a string with this format: This week's total sales: xxx
  # You will probably need to write some lines of code before the print statement.
```
> Quiz answers are in python scripts tab

## String Methods

<iframe width="460" height="259" src="https://www.youtube.com/embed/Bv7CAxVOONs" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

In this video you were introduced to methods. **Methods** are like some of the **functions** you have already seen:

1. `len`("this")
2. `type`(12)
3. `print`("Hello world")

These three above are **functions** - notice they use parentheses, and accept one or more **arguments**. Functions will be studied in much more detail in a later lesson!

A **method** in Python behaves similarly to a function. Methods actually are functions that are called using dot notation. For example, lower() is a string method that can be used like this, on a string called "sample string": sample_string.lower().

Methods are specific to the data type for a particular variable. So there are some built-in methods that are available for all strings, different methods that are available for all integers, etc.

Below is an image that shows some methods that are possible with any string.

![image](https://video.udacity-data.com/topher/2018/February/5a72cb8c_screen-shot-2018-02-01-at-12.10.40-am/screen-shot-2018-02-01-at-12.10.40-am.png)

Each of these methods accepts the string itself as the first argument of the method. However, they also could receive additional arguments, that are passed inside the parentheses. Let's look at the output for a few examples.
```
  >>> my_string.islower()
  True
  >>> my_string.count('a')
  2
  >>> my_string.find('a')
  3
```
You can see that the `count` and `find` methods both take another argument. However, the `.islower()` method does not accept another argument.

No professional has all the methods memorized, which is why understanding how to use documentation and find answers is so important. Gaining a strong grasp of the foundations of programming will allow you to use those foundations to use documentation to build so much more than someone who tries to memorize all the built-in methods in Python.

**One important string method:** `format()``
We will be using the `format()` string method a good bit in our future work in Python, and you will find it very valuable in your coding, especially with your `print` statements.

We can best illustrate how to use format() by looking at some examples:

Example 1

`print("Mohammed has {} balloons".format(27))`

Example 1 Output

`Mohammed has 27 balloons`

Example 2
```
  animal = "dog"
  action = "bite"
  print("Does your {} {}?".format(animal, action))
```
Example 2 Output

`Does your dog bite?`

Example 3
```
  maria_string = "Maria loves {} and {}"
  print(maria_string.format("math", "statistics"))
```

Example 3 Output

`Maria loves math and statistics`

Notice how in each example, the number of pairs of curly braces {} you use inside the string is the same as the number of replacements you want to make using the values inside `format()`.

More advanced students can learn more about the formal syntax for using the `format()` string method [here](https://docs.python.org/3.6/library/string.html#format-string-syntax).

You can learn more about strings and string methods by looking at the [string method documentation](https://docs.python.org/3/library/stdtypes.html#string-methods).

You will find that the documentation is one of the most valuable resources for writing code, and not only when it comes to strings or writing code in Python! By reading and searching the documentation you can learn about data types and built-in functions as well as how to use them.

**`format()` Practice**
Use the coding space below to practice using the format() string method. There are no right or wrong answers here, just practice!

Write two lines of code below, each assigning a value to a variable

# Now write a print statement using .format() to print out a sentence and the
#   values of both of the variables
