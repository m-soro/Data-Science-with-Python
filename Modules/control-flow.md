---
layout: default
title: Control Flow
parent:  Introduction to Python programming
grand_parent: Modules
nav_order: 3
---

# Control Flow

## Introduction

<iframe width="100%" height="878" src="https://www.youtube.com/embed/eUrvACMMJ5w" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

**Control Flow**

Welcome to this lesson on Control Flow! Control flow is the sequence in which your code is run. Here, we'll learn about several tools in Python we can use to affect our code's control flow:

* [Conditional Statements](#if-elif-else)
* [Boolean Expressions](#complex-boolean-expressions)
* [For and While Loops](#loops)
* [Break and Continue](#)
* [Zip and Enumerate](#)
* [List Comprehensions](#)

<iframe width="100%" height="433" src="https://www.youtube.com/embed/jWiIUMrwPqA" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## If Statement

An `if` statement is a conditional statement that runs or skips code based on whether a condition is true or false. Here's a simple example.

```python
if phone_balance < 5:
    phone_balance += 10
    bank_balance -= 10
```

Let's break this down.

1. An `if` statement starts with the `if` keyword, followed by the condition to be checked, in this case `phone_balance < 5`, and then a colon. The condition is specified in a boolean expression that evaluates to either True or False.

2. After this line is an indented block of code to be executed if that condition is true. Here, the lines that increment `phone_balance` and decrement `bank_balance` only execute if it is true that `phone_balance` is less than 5. If not, the code in this `if` block is simply skipped.

**Use Comparison Operators in Conditional Statements**

You have learned about Python's comparison operators (e.g. `==` and `!=`) and how they are different from assignment operators (e.g. `=`). In conditional statements, you want to use comparison operators. For example, you'd want to use `if x == 5` rather than `if x = 5`. If your conditional statement is causing a syntax error or doing something unexpected, check whether you have written `==` or `=` !

<iframe width="100%" height="433" src="https://www.youtube.com/embed/KZubH5XT0eU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## If, Elif, Else

In addition to the `if` clause, there are two other optional clauses often used with an `if` statement. For example:

```python
if season == 'spring':
    print('plant the garden!')
elif season == 'summer':
    print('water the garden!')
elif season == 'fall':
    print('harvest the garden!')
elif season == 'winter':
    print('stay indoors!')
else:
    print('unrecognized season')
```    

1. `if`: An `if` statement must always start with an `if` clause, which contains the first condition that is checked. If this evaluates to True, Python runs the code indented in this `if` block and then skips to the rest of the code after the `if` statement.

2. `elif`: `elif` is short for "else if." An `elif` clause is used to check for an additional condition if the conditions in the previous clauses in the `if` statement evaluate to False. As you can see in the example, you can have multiple `elif` blocks to handle different situations.

3. `else`: Last is the `else` clause, which must come at the end of an `if` statement if used. This clause doesn't require a condition. The code in an `else` block is run if all conditions above that in the `if` statement evaluate to False.

<iframe width="100%" height="433" src="https://www.youtube.com/embed/G8qUNOTHtrM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Indentation
Some other languages use braces to show where blocks of code begin and end. In Python we use indentation to enclose blocks of code. For example, `if` statements use indentation to tell Python what code is inside and outside of different clauses.

In Python, indents conventionally come in multiples of four spaces. Be strict about following this convention, because changing the indentation can completely change the meaning of the code. If you are working on a team of Python programmers, it's important that everyone follows the same indentation convention!

**Spaces or Tabs?**

The [Python Style Guide](https://www.python.org/dev/peps/pep-0008/#tabs-or-spaces) recommends using 4 spaces to indent, rather than using a tab. Whichever you use, be aware that "Python 3 disallows mixing the use of tabs and spaces for indentation."

<iframe width="100%" height="289" src="https://www.youtube.com/embed/gWmIKWgzFqI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Complex Boolean Expressions
`If` statements sometimes use more complicated boolean expressions for their conditions. They may contain multiple comparisons operators, logical operators, and even calculations.

Examples:
```python
if 18.5 <= weight / height**2 < 25:
    print("BMI is considered 'normal'")

if is_raining and is_sunny:
    print("Is there a rainbow?")

if (not unsubscribed) and (location == "USA" or location == "CAN"):
    print("send email")
```    
For really complicated conditions you might need to combine some `and`s, `or`s and `not`s together. Use parentheses if you need to make the combinations clear.

However simple or complex, the condition in an `if` statement must be a boolean expression that evaluates to either True or False and it is this value that decides whether the indented block in an `if` statement executes or not.

<iframe width="100%" height="289" src="https://www.youtube.com/embed/95oLh3WtdhY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### Good and Bad Examples

Here are some things to keep in mind while writing boolean expressions for your `if` statements.

**1. Don't use `True or `False` as conditions**

```python
# Bad example
if True:
    print("This indented code will always get run.")
```    

While "True" is a valid boolean expression, it's not useful as a condition since it always evaluates to True, so the indented code will always get run. Similarly, `if False` is not a condition you should use either - the statement following this `if` statement would never be executed.

```python
# Another bad example
if is_cold or not is_cold:
    print("This indented code will always get run.")
```

Similarly, it's useless to use any condition that you know will always evaluate to True, like this example above. A boolean variable can only be True or False, so either `is_cold` or `not is_cold` is always True, and the indented code will always be run.

**2. Be careful writing expressions that use logical operators**

Logical operators `and`, `or` and `not` have specific meanings that aren't quite the same as their meanings in plain English. Make sure your boolean expressions are being evaluated the way you expect them to.

```python
# Bad example
if weather == "snow" or "rain":
    print("Wear boots!")
```

This code is valid in Python, but it is not a boolean expression, although it reads like one. The reason is that the expression to the right of the `or` operator, `"rain"`, is not a boolean expression - it's a string! Later we'll discuss what happens when you use non-boolean-type objects in place of booleans.

**3. Don't compare a boolean variable with `== True` or `== False`**

This comparison isn’t necessary, since the boolean variable itself is a boolean expression.

```python
# Bad example
if is_cold == True:
    print("The weather is cold!")
```

This is a valid condition, but we can make the code more readable by using the variable itself as the condition instead, as below.

```python
# Good example
if is_cold:
    print("The weather is cold!")
```

If you want to check whether a boolean is False, you can use the `not` operator.

<iframe width="100%" height="289" src="https://www.youtube.com/embed/e52uw7ejV8k" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Truth Value Testing
If we use a non-boolean object as a condition in an `if` statement in place of the boolean expression, Python will check for its truth value and use that to decide whether or not to run the indented code. By default, the truth value of an object in Python is considered True unless specified as False in the documentation.

Here are most of the built-in objects that are considered False in Python:

* constants defined to be false: `None` and `False`
* zero of any numeric type: `0`, `0.0`, `0j`, `Decimal(0)`, `Fraction(0, 1)`
* empty sequences and collections: `'""`, `()`, `[]`, `{}`, `set()`, `range(0)`

Example:

```python
errors = 3
if errors:
    print("You have {} errors to fix!".format(errors))
else:
    print("No errors to fix!")
```

In this code, `errors` has the truth value True because it's a non-zero number, so the error message is printed. This is a nice, succinct way of writing an `if` statement.

## Loops

<iframe width="100%" height="330" src="https://www.youtube.com/embed/UtX0PXSUCdY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### For Loops

Python has two kinds of loops - `for` loops and `while` loops. A `for` loop is used to "iterate", or do something repeatedly, over an **iterable**.

An **iterable** is an object that can return one of its elements at a time. This can include sequence types, such as strings, lists, and tuples, as well as non-sequence types, such as dictionaries and files.

**Example**

Let's break down the components of a for `loop`, using this example with the list `cities`:

```python
cities = ['new york city', 'mountain view', 'chicago', 'los angeles']
for city in cities:
    print(city)
print("Done!")
```

### Components of a `for` Loop

1. The first line of the loop starts with the `for` keyword, which signals that this is a `for` loop
2. Following that is `city in cities`, indicating `city` is the iteration variable, and `cities` is the iterable being looped over. In the first iteration of the loop, `city` gets the value of the first element in `cities`, which is “new york city”.
3. The for `loop` heading line always ends with a colon `:`
4. Following the `for` loop heading is an indented block of code, the body of the loop, to be executed in each iteration of this loop. There is only one line in the body of this loop - `print(city)`.
5. After the body of the loop has executed, we don't move on to the next line yet; we go back to the `for` heading line, where the iteration variable takes the value of the next element of the iterable. In the second iteration of the loop above, `city` takes the value of the next element in `cities`, which is "mountain view".
3. This process repeats until the loop has iterated through all the elements of the iterable. Then, we move on to the line that follows the body of the loop - in this case, `print("Done!")`. We can tell what the next line after the body of the loop is because it is unindented. Here is another reason why paying attention to your indentation is very important in Python!
Executing the code in the example above produces this output:

```python
new york city
mountain view
chicago
los angeles
Done!
```

You can name iteration variables however you like. A common pattern is to give the iteration variable and iterable the same names, except the singular and plural versions respectively (e.g., 'city' and 'cities').

## Using the `range()` Function with for Loops
`range()` is a built-in function used to create an iterable sequence of numbers. You will frequently use `range()` with a `for` loop to repeat an action a certain number of times. Any variable can be used to iterate through the numbers, but Python programmers conventionally use `i`, as in this example:

```python
for i in range(3):
    print("Hello!")
```

Output:

```python
Hello!
Hello!
Hello!
```

`range(start=0, stop, step=1)`

The `range()` function takes three integer arguments, the first and third of which are optional:

1. The 'start' argument is the first number of the sequence. If unspecified, 'start' defaults to 0.
2. The 'stop' argument is 1 more than the last number of the sequence. This argument must be specified.
3. The 'step' argument is the difference between each number in the sequence. If unspecified, 'step' defaults to 1.

Notes on using `range()`:

* If you specify one integer inside the parentheses with `range()`, it's used as the value for 'stop,' and the defaults are used for the other two.
**e.g.** - `range(4)` returns `0, 1, 2, 3`
* If you specify two integers inside the parentheses with `range()`, they're used for 'start' and 'stop,' and the default is used for 'step.'
**e.g.** - `range(2, 6)` returns `2, 3, 4, 5`
* Or you can specify all three integers for 'start', 'stop', and 'step.'
**e.g.** - `range(1, 10, 2)` returns `1, 3, 5, 7, 9`

## Creating and Modifying Lists

In addition to extracting information from lists, as we did in the first example above, you can also create and modify lists with `for` loops. You can **create** a list by appending to a new list at each iteration of the `for` loop like this:

```python
# Creating a new list
cities = ['new york city', 'mountain view', 'chicago', 'los angeles']
capitalized_cities = []

for city in cities:
    capitalized_cities.append(city.title())
```

**Modifying** a list is a bit more involved, and requires the use of the `range()` function.

We can use the `range()` function to generate the indices for each value in the `cities` list. This lets us access the elements of the list with `cities[index]` so that we can modify the values in the `cities` list in place.

```python
cities = ['new york city', 'mountain view', 'chicago', 'los angeles']

for index in range(len(cities)):
    cities[index] = cities[index].title()
```

## Building Dictionaries

By now you are familiar with two important concepts: 1) counting with `for` loops and 2) the dictionary `get` method. These two can actually be combined to create a useful counter dictionary, something you will likely come across again. For example, we can create a dictionary, `word_counter`, that keeps track of the total count of each word in a string.

The following are a couple of ways to do it:

### Method 1: Using a for `loop` to create a set of counters
Let's start with a list containing the words in a series of book titles:

```python
book_title =  ['great', 'expectations','the', 'adventures', 'of', 'sherlock','holmes','the','great','gasby','hamlet','adventures','of','huckleberry','fin']
```

**Step 1:** Create an empty dictionary.
```python
word_counter = {}
```
**Step 2.** Iterate through each element in the list. If an element is already included in the dictionary, add 1 to its value. If not, add the element to the dictionary and set its value to 1.
```python
for word in book_title:
    if word not in word_counter:
        word_counter[word] = 1
    else:
        word_counter[word] += 1
```        
**What's happening here?**

* The `for` loop iterates through each element in the list. For the first iteration, `word` takes the value 'great'.
* Next, the if statement checks if `word` is in the `word_counter` dictionary.
* Since it doesn't yet, the statement `word_counter[word] = 1` adds `great` as a key to the dictionary with a value of 1.
* Then, it leaves the if else statement and moves on to the next iteration of the for loop. `word` now takes the value `expectations` and repeats the process.
* When the if condition is not met, it is because that`word` already exists in the `word_counter` dictionary, and the statement `word_counter[word] = word_counter[word] + 1` increases the count of that word by 1.
* Once the for `loop` finishes iterating through the list, the `for` loop is complete.

We can see the output by printing out the dictionary. Printing `word_counter` results in the following output.

```python
{'great': 2, 'expectations': 1, 'the': 2, 'adventures': 2, 'of': 2, 'sherlock': 1, 'holmes': 1, 'gasby': 1, 'hamlet': 1, 'huckleberry': 1, 'fin': 1}
```
Feel free to try this out yourself in the code editor at the bottom of this page.

### Method 2: Using the `get` method

We will use the same list for this example:
```python
book_title =  ['great', 'expectations','the', 'adventures', 'of', 'sherlock','holmes','the','great','gasby','hamlet','adventures','of','huckleberry','fin']
```
**Step 1:** Create an empty dictionary.
```python
word_counter = {}
```
**Step 2.** Iterate through each element, `get()` its value in the dictionary, and add 1.

Recall that the dictionary `get` method is another way to retrieve the value of a key in a dictionary. Except unlike indexing, this will return a default value if the key is not found. If unspecified, this default value is set to None. We can use `get` with a default value of 0 to simplify the code from the first method above.

```python
for word in book_title:
    word_counter[word] = word_counter.get(word, 0) + 1
```
**What's happening here?**

* The for `loop` iterates through the list as we saw earlier. The `for` loop feeds 'great' to the next statement in the body of the `for` loop.
* In this line: `word_counter[word] = word_counter.get(word,0) + 1`, since the key 'great' doesn't yet exist in the dictionary, `get()` will return the value 0 and `word_counter[word]` will be set to 1.
* Once it encounters a word that already exists in `word_counter` (e.g. the second appearance of `'the'`), the value for that key is incremented by 1. On the second appearance of 'the', the key's value would add 1 again, resulting in 2.
* Once the for `loop` finishes iterating through the list, the `for` loop is complete.

Printing `word_counter` shows us we get the same result as we did in method 1.

```python
{'great': 2, 'expectations': 1, 'the': 2, 'adventures': 2, 'of': 2, 'sherlock': 1, 'holmes': 1, 'gasby': 1, 'hamlet': 1, 'huckleberry': 1, 'fin': 1}
```

## Iterating Through Dictionaries with `For` Loops
When you iterate through a dictionary using a `for` loop, doing it the normal way (`for n in some_dict`) will only give you access to the keys in the dictionary - which is what you'd want in some situations. In other cases, you'd want to iterate through both the **keys** and **values** in the dictionary. Let's see how this is done in an example. Consider this dictionary that uses names of actors as keys and their characters as values.

```python
cast = {
           "Jerry Seinfeld": "Jerry Seinfeld",
           "Julia Louis-Dreyfus": "Elaine Benes",
           "Jason Alexander": "George Costanza",
           "Michael Richards": "Cosmo Kramer"
       }
```       
Iterating through it in the usual way with a `for` loop would give you just the keys, as shown below:

```python
for key in cast:
    print(key)
```
This outputs:

```python
Jerry Seinfeld
Julia Louis-Dreyfus
Jason Alexander
Michael Richards
```

If you wish to iterate through both keys and values, you can use the built-in method `items` like this:

```python
for key, value in cast.items():
    print("Actor: {}    Role: {}".format(key, value))
```
This outputs:

```python

Actor: Jerry Seinfeld    Role: Jerry Seinfeld
Actor: Julia Louis-Dreyfus    Role: Elaine Benes
Actor: Jason Alexander    Role: George Costanza
Actor: Michael Richards    Role: Cosmo Kramer
```

`items` is an awesome method that returns tuples of key, value pairs, which you can use to iterate over dictionaries in `for` loops.

## While Loops

<iframe width="100%" height="330" src="https://www.youtube.com/embed/7Sf5tcPlKQw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

**While Loops**

`For` loops are an example of "definite iteration" meaning that the loop's body is run a predefined number of times. This differs from "indefinite iteration" which is when a loop repeats an unknown number of times and ends when some condition is met, which is what happens in a `while` loop.

Here's an example of a `while` loop.
```python
card_deck = [4, 11, 8, 5, 13, 2, 8, 10]
hand = []

# adds the last element of the card_deck list to the hand list
# until the values in hand add up to 17 or more
while sum(hand)  < 17:
    hand.append(card_deck.pop())
```

This example features two new functions. sum returns the `sum` of the elements in a list, and `pop` is a list method that removes the last element from a list and returns it.

**Components of a While Loop**

1. The first line starts with the while keyword, indicating this is a `while` loop.
2. Following that is a condition to be checked. In this example, that's `sum(hand) <= 17`.
3. The `while` loop heading always ends with a colon `:`.
4. Indented after this heading is the body of the `while` loop. If the condition for the `while` loop is true, the code lines in the loop's body will be executed.
5. We then go back to the `while` heading line, and the condition is evaluated again. This process of checking the condition and then executing the loop repeats until the condition becomes false.
6. When the condition becomes false, we move on to the line following the body of the loop, which will be unindented.

The indented body of the loop should modify at least one variable in the test condition. If the value of the test condition never changes, the result is an infinite loop!

## For Loops Vs. While Loops

Now that you are familiar with both `for` and `while` loops, let's consider when it's most helpful to use each of them.

`for` loops are ideal when the **number of iterations is known or finite**.

Examples:

* When you have an iterable collection (list, string, set, tuple, dictionary)
  * `for name in names:`
* When you want to iterate through a loop for a definite number of times, using `range()`
  * `for i in range(5):`

`while` loops are ideal when the **iterations need to continue until a condition is met**.

Examples:

* When you want to use comparison operators
  * `while count <= 100:`
* When you want to loop based on receiving specific user input.
  * `while user_input == 'y':`

## Break, Continue

<iframe width="100%" height="313" src="https://www.youtube.com/embed/F6qJAv9ts9Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

**`Break`, `Continue`**

Sometimes we need more control over when a loop should end, or skip an iteration. In these cases, we use the `break` and `continue` keywords, which can be used in both for and while loops.

* `break` terminates a loop
* `continue` skips one iteration of a loop

## Zip and Enumerate

<iframe width="100%" height="313" src="https://www.youtube.com/embed/bSJPzVArE7M" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

>In the video above, at the 0:55 mark, the instructor says "... you can separate it into an items and weights list, like this," but she should instead say, "... you can separate it into an items tuple and a weights tuple, like this."

### Zip and Enumerate
`zip` and `enumerate` are useful built-in functions that can come in handy when dealing with loops.

**Zip**

`zip` returns an iterator that combines multiple iterables into one sequence of tuples. Each tuple contains the elements in that position from all the iterables. For example, printing

`list(zip(['a', 'b', 'c'], [1, 2, 3]))` would output `[('a', 1), ('b', 2), ('c', 3)]`.

Like we did for `range()` we need to convert it to a list or iterate through it with a loop to see the elements.

You could unpack each tuple in a `for` loop like this.

```python
letters = ['a', 'b', 'c']
nums = [1, 2, 3]

for letter, num in zip(letters, nums):
    print("{}: {}".format(letter, num))
```

In addition to zipping two lists together, you can also unzip a list into tuples using an asterisk.

```python
some_list = [('a', 1), ('b', 2), ('c', 3)]
letters, nums = zip(*some_list)
```

This would create the same `letters` and `nums` tuples we saw earlier.

**Enumerate**

`enumerate` is a built in function that returns an iterator of tuples containing indices and values of a list. You'll often use this when you want the index along with each element of an iterable in a loop.

```python
letters = ['a', 'b', 'c', 'd', 'e']
for i, letter in enumerate(letters):
    print(i, letter)
```
This code would output:

```python
0 a
1 b
2 c
3 d
4 e
```

## List Comprehensions

<iframe width="100%" height="330" src="https://www.youtube.com/embed/6qxo-NV9v_s" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### List Comprehensions
In Python, you can create lists really quickly and concisely with list comprehensions. This example from earlier:

```python
capitalized_cities = []
for city in cities:
    capitalized_cities.append(city.title())
```
can be reduced to:

```python
capitalized_cities = [city.title() for city in cities]
```

List comprehensions allow us to create a list using a `for` loop in one step.

You create a list comprehension with brackets `[]`, including an expression to evaluate for each element in an iterable. This list comprehension above calls `city.title()` for each element `city` in `cities`, to create each element in the new list, `capitalized_cities`.

**Conditionals in List Comprehensions**

You can also add conditionals to list comprehensions (listcomps). After the iterable, you can use the `if` keyword to check a condition in each iteration.

```python
squares = [x**2 for x in range(9) if x % 2 == 0]
```

The code above sets `squares` equal to the list [0, 4, 16, 36, 64], as x to the power of 2 is only evaluated if x is even. If you want to add an `else`, you will get a syntax error doing this.

```python
squares = [x**2 for x in range(9) if x % 2 == 0 else x + 3]
```

If you would like to add `else`, you have to move the conditionals to the beginning of the listcomp, right after the expression, like this.

```python
squares = [x**2 if x % 2 == 0 else x + 3 for x in range(9)]
```

List comprehensions are not found in other languages, but are very common in Python.

**Conclusion**

<iframe width="100%" height="330" src="https://www.youtube.com/embed/vDoqpwCHxs4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
