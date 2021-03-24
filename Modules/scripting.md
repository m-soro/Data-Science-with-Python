---
layout: default
title: Scripting
parent:  Introduction to Python programming
grand_parent: Modules
nav_order: 5
---

# Scripting

## Introduction

<iframe width="100%" height="273" src="https://www.youtube.com/embed/Qxe_gCiXUDg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


**Scripting**

Welcome to this lesson on scripting! You’ll learn about:

* Python Installation and Environment Setup
* Running and Editing Python Scripts
* Interacting with User Input
* Handling Exceptions
* Reading and Writing Files
* Importing Local, Standard, and Third-Party Modules
* Experimenting with an Interpreter

<iframe width="100%" height="273" src="https://www.youtube.com/embed/Fs9uLV2qfgI" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### Scripting With Raw Input

We can get raw input from the user with the built-in function `input`, which takes in an optional string argument that you can use to specify a message to show to the user when asking for input.

```python
name = input("Enter your name: ")
print("Hello there, {}!".format(name.title()))
```

This prompts the user to enter a name and then uses the input in a greeting. The `input` function takes in whatever the user types and stores it as a string. If you want to interpret their input as something other than a string, like an integer, as in the example below, you need to wrap the result with the new type to convert it from a string.

```python
num = int(input("Enter an integer"))
print("hello" * num)
```

We can also interpret user input as a Python expression using the built-in function `eval`. This function evaluates a string as a line of Python.

```python
result = eval(input("Enter an expression: "))
print(result)
```

If the user inputs `2 * 3`, this outputs `6`.

## Errors and Exceptions

<iframe width="100%" height="273" src="https://www.youtube.com/embed/DmthSiy2d0U" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


* **Syntax errors** occur when Python can’t interpret our code, since we didn’t follow the correct syntax for Python. These are errors you’re likely to get when you make a typo, or you’re first starting to learn Python.

* **Exceptions** occur when unexpected things happen during execution of a program, even if the code is syntactically correct. There are different types of built-in exceptions in Python, and you can see which exception is thrown in the error message.

## Handling Errors

<iframe width="100%" height="257" src="https://www.youtube.com/embed/S6hwBZG0KwM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

**Try Statement**

We can use `try` statements to handle exceptions. There are four clauses you can use (one more in addition to those shown in the video).

* `try`: This is the only mandatory clause in a `try` statement. The code in this block is the first thing that Python runs in a `try` statement.
* `except`: If Python runs into an exception while running the `try` block, it will jump to the `except` block that handles that exception.
* `else`: If Python runs into no exceptions while running the try block, it will run the code in this block after running the `try` block.
* `finally`: Before Python leaves this `try` statement, it will run the code in this `finally` block under any conditions, even if it's ending the program. E.g., if Python ran into an error while running code in the `except` or `else` block, this `finally` block will still be executed before stopping the program.

[Why do we need the `finally` clause in Python?](https://stackoverflow.com/questions/11551996/why-do-we-need-the-finally-clause-in-python)

<iframe width="100%" height="433" src="https://www.youtube.com/embed/EHW5I7shdJg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Specifying Exceptions

We can actually specify which error we want to handle in an `except` block like this:

```python
try:
    # some code
except ValueError:
    # some code
```

Now, it catches the ValueError exception, but not other exceptions. If we want this handler to address more than one type of exception, we can include a parenthesized tuple after the `except` with the exceptions.

```python
try:
    # some code
except (ValueError, KeyboardInterrupt):
    # some code
```

Or, if we want to execute different blocks of code depending on the exception, you can have multiple `except` blocks.

```python
try:
    # some code
except ValueError:
    # some code
except KeyboardInterrupt:
    # some code
```

## Accessing Error Messages

When you handle an exception, you can still access its error message like this:

```python
try:
    # some code
except ZeroDivisionError as e:
   # some code
   print("ZeroDivisionError occurred: {}".format(e))
```

This would print something like this:

```python
ZeroDivisionError occurred: integer division or modulo by zero
```

So you can still access error messages, even if you handle them to keep your program from crashing!

If you don't have a specific error you're handling, you can still access the message like this:
```python
try:
    # some code
except Exception as e:
   # some code
   print("Exception occurred: {}".format(e))
```

`Exception` is just the base class for all built-in exceptions. You can learn more about Python's exceptions [here](https://docs.python.org/3/library/exceptions.html#bltin-exceptions).


## Reading and Writing Files

<iframe width="100%" height="433" src="https://www.youtube.com/embed/w-ZG6DMkVi4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Using Files

<iframe width="100%" height="433" src="https://www.youtube.com/embed/1GRv1S6K8gQ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Reading and Writing Files

To follow along with the example above, create a new file in Atom, copy the following text into it, and save it as `some_file.txt`!

```python
Hello!!

You have read the contents of this file!
```

Here's how we read and write files in Python.

## Reading a File

```python
f = open('my_path/my_file.txt', 'r')
file_data = f.read()
f.close()
```

1. First open the file using the built-in function, `open`. This requires a string that shows the path to the file. The open function returns a file object, which is a Python object through which Python interacts with the file itself. Here, we assign this object to the variable `f`.
2. There are optional parameters you can specify in the `open` function. One is the mode in which we open the file. Here, we use `r` or read only. This is actually the default value for the mode argument.
3. Use the `read` method to access the contents from the file object. This read method takes the text contained in a file and puts it into a string. Here, we assign the string returned from this method into the variable `file_data`.
4. When finished with the file, use the `close` method to free up any system resources taken up by the file.

## Writing to a File

```python
f = open('my_path/my_file.txt', 'w')
f.write("Hello there!")
f.close()
```

1. Open the file in writing ('w') mode. If the file does not exist, Python will create it for you. If you open an existing file in writing mode, any content that it had contained previously will be deleted. If you're interested in adding to an existing file, without deleting its content, you should use the append ('a') mode instead of write.
2. Use the write method to add text to the file.
3. Close the file when finished.

### Too Many Open Files

Run the following script in Python to see what happens when you open too many files without closing them!

```python
files = []
for i in range(10000):
    files.append(open('some_file.txt', 'r'))
    print(i)
```

<iframe width="100%" height="433" src="https://www.youtube.com/embed/OQ-Y0mMjm00" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>    

## With

Python provides a special syntax that auto-closes a file for you once you're finished using it.

```python
with open('my_path/my_file.txt', 'r') as f:
    file_data = f.read()
```

This `with` keyword allows you to open a file, do operations on it, and automatically close it after the indented code is executed, in this case, reading from the file. Now, we don’t have to call f.close()! You can only access the file object, f, within this indented block.

## Importing Local Scripts

<iframe width="100%" height="433" src="https://www.youtube.com/embed/qjeSn6zZbR0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

### Importing Local Scripts

We can actually import Python code from other scripts, which is helpful if you are working on a bigger project where you want to organize your code into multiple files and reuse code in those files. If the Python script you want to import is in the same directory as your current script, you just type `import` followed by the name of the file, without the .py extension.

```python
import useful_functions
```

It's the standard convention for `import` statements to be written at the top of a Python script, each one on a separate line. This `import` statement creates a `module` object called `useful_functions`. Modules are just Python files that contain definitions and statements. To access objects from an imported module, you need to use dot notation.

```python
import useful_functions
useful_functions.add_five([1, 2, 3, 4])
```

We can add an alias to an imported module to reference it with a different name.

```python
import useful_functions as uf
uf.add_five([1, 2, 3, 4])
```

## Using a main block

To avoid running executable statements in a script when it's imported as a module in another script, include these lines in an `if __name__ == "__main__"` block. Or alternatively, include them in a function called main() and call this in the `if main` block.

Whenever we run a script like this, Python actually sets a special built-in variable called `__name__` for any module. When we run a script, Python recognizes this module as the main program, and sets the `__name__` variable for this module to the string `"__main__"`. For any modules that are imported in this script, this built-in `__name__` variable is just set to the name of that module. Therefore, the condition `if __name__ == "__main__"`is just checking whether this module is the main program.

###  Try It Out!
Here's the code I used in the video above. Create these scripts in the same directory and run them in your terminal! Experiment with the `if main` block and accessing objects from the imported module!

```python
# demo.py

import useful_functions as uf

scores = [88, 92, 79, 93, 85]

mean = uf.mean(scores)
curved = uf.add_five(scores)

mean_c = uf.mean(curved)

print("Scores:", scores)
print("Original Mean:", mean, " New Mean:", mean_c)

print(__name__)
print(uf.__name__)
```

```python
# useful_functions.py

def mean(num_list):
    return sum(num_list) / len(num_list)

def add_five(num_list):
    return [n + 5 for n in num_list]

def main():
    print("Testing mean function")
    n_list = [34, 44, 23, 46, 12, 24]
    correct_mean = 30.5
    assert(mean(n_list) == correct_mean)

    print("Testing add_five function")
    correct_list = [39, 49, 28, 51, 17, 29]
    assert(add_five(n_list) == correct_list)

    print("All tests passed!")

if __name__ == '__main__':
    main()
```
## The Standard Library

<iframe width="100%" height="527" src="https://www.youtube.com/embed/Fw3vf0tDrJM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

**The Standard Library**
You can discover new modules at the [Python Module of the Week](https://pymotw.com/3/) blog.

**Our favourite modules**

The Python Standard Library has a lot of modules! To help you get familiar with what's available, here are a selection of our favourite Python Standard Library modules and why we use them!

* `csv:` very convenient for reading and writing csv files
* `collections:` useful extensions of the usual data types including `OrderedDict`, `defaultdict` and `namedtuple`
* `random:` generates pseudo-random numbers, shuffles sequences randomly and chooses random items
* `string:` more functions on strings. This module also contains useful collections of letters like `string.digits` (a string containing all characters which are valid digits).
* `re:` pattern-matching in strings via regular expressions
* `math:` some standard mathematical functions
* `os:` interacting with operating systems
* `os.path:` submodule of os for manipulating path names
* `sys:` work directly with the Python interpreter
* `json:` good for reading and writing json files (good for web work)

## Techniques for Importing Modules

<iframe width="100%" height="433" src="https://www.youtube.com/embed/jPGyFgcIvsM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

**Techniques for Importing Modules**

There are other variants of `import` statements that are useful in different situations.

1. To import an individual function or class from a module:
`from module_name import object_name`
2. To import multiple individual objects from a module:
`from module_name import first_object, second_object`
3. To rename a module:
`import module_name as new_name`
4. To import an object from a module and rename it:
`from module_name import object_name as new_name`
5. To import every object individually from a module (DO NOT DO THIS):
`from module_name import *`
6. If you really want to use all of the objects from a module, use the standard import module_name statement instead and access each of the objects with the dot notation.
`import module_name`

<iframe width="100%" height="433" src="https://www.youtube.com/embed/aASigWQ_XU0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Modules, Packages, and Names

In order to manage the code better, modules in the Python Standard Library are split down into sub-modules that are contained within a package. A **package** is simply a module that contains sub-modules. A sub-module is specified with the usual dot notation.

Modules that are submodules are specified by the package name and then the submodule name separated by a dot. You can import the submodule like this.

`import package_name.submodule_name`

## Third-Party Libraries

<iframe width="100%" height="433" src="https://www.youtube.com/embed/epOze9gC6T4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


There are tens of thousands of third-party libraries written by independent developers! You can install them using pip, a package manager that is included with Python 3. pip is the standard package manager for Python, but it isn't the only one. One popular alternative is Anaconda which is designed specifically for data science.

To install a package using pip, just enter "pip install" followed by the name of the package in your command line like this: `pip install package_name`. This downloads and installs the package so that it's available to import in your programs. Once installed, you can import third-party packages using the same syntax used to import from the standard library.

## Using a `requirements.txt` File

Larger Python programs might depend on dozens of third party packages. To make it easier to share these programs, programmers often list a project's dependencies in a file called requirements.txt. This is an example of a requirements.txt file.

```python
beautifulsoup4==4.5.1
bs4==0.0.1
pytz==2016.7
requests==2.11.1
```

Each line of the file includes the name of a package and its version number. The version number is optional, but it usually should be included. Libraries can change subtly, or dramatically, between versions, so it's important to use the same library versions that the program's author used when they wrote the program.

You can use pip to install all of a project's dependencies at once by typing `pip install -r requirements.txt` in your command line.

## Useful Third-Party Packages

Being able to install and import third party libraries is useful, but to be an effective programmer you also need to know what libraries are available for you to use. People typically learn about useful new libraries from online recommendations or from colleagues. If you're a new Python programmer you may not have many colleagues, so to get you started here's a list of packages that are popular with engineers at Udacity.

* [IPython](https://ipython.org/) - A better interactive Python interpreter
* [requests](http://docs.python-requests.org/) - Provides easy to use methods to make web requests. Useful for accessing web APIs.
* [Flask](http://flask.pocoo.org/) - a lightweight framework for making web applications and APIs.
* [Django](https://www.djangoproject.com/) - A more featureful framework for making web applications. Django is particularly good for designing complex, content heavy, web applications.
* [Beautiful Soup](https://www.crummy.com/software/BeautifulSoup/) - Used to parse HTML and extract information from it. Great for web scraping.
* [pytest](http://doc.pytest.org/) - extends Python's builtin assertions and unittest module.
* [PyYAML](http://pyyaml.org/wiki/PyYAML) - For reading and writing [YAML](https://en.wikipedia.org/wiki/YAML) files.
* [NumPy](http://www.numpy.org/) - The fundamental package for scientific computing with Python. It contains among other things a powerful N-dimensional array object and useful linear algebra capabilities.
* [pandas](http://pandas.pydata.org/) - A library containing high-performance, data structures and data analysis tools. In particular, pandas provides dataframes!
* [matplotlib](http://matplotlib.org/) - a 2D plotting library which produces publication quality figures in a variety of hardcopy formats and interactive environments.
* [ggplot](http://ggplot.yhathq.com/) - Another 2D plotting library, based on R's ggplot2 library.
* [Pillow](https://python-pillow.org/) - The Python Imaging Library adds image processing capabilities to your Python interpreter.
* [pyglet](http://www.pyglet.org/) - A cross-platform application framework intended for game development.
* [Pygame](http://www.pygame.org/) - A set of Python modules designed for writing games.
* [pytz](http://pytz.sourceforge.net/) - World Timezone Definitions for Python

## Experimenting with an Interpreter

<iframe width="100%" height="527" src="https://www.youtube.com/embed/hspPtnQwMPg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

**Experimenting With An Interpreter**

Start your Python interactive interpreter by entering the command `python` in your terminal. You can type here to interact with Python directly. This is an awesome place to experiment and try bits of Python code at a time. Just enter Python code, and the output will appear on the next line.
```python
>>> type(5.23)
<class 'float'>
```

In the interpreter, the value of the last line in a prompt will be outputted automatically. If you had multiple lines where you’d want to output values, you’d still have to use print.

If you start to define a function you will see a change in the prompt, to signify that this is a continuation line. You'll have to include your own indentation as you define the function.

```python
>>> def cylinder_volume(height, radius):
...         pi = 3.14159
...         return height * pi * radius ** 2
```

A drawback of the interpreter is that it’s tricky to edit code. If you made a mistake when typing this function, or forgot to indent the body of the function, you can't use the mouse to click your cursor where you want it. You have to navigate with arrow keys to move the cursor forwards and backwards through the line itself for editing. It would be helpful for you to learn useful shortcuts for actions like moving to the beginning or end of the line.

Notice I can reference any objects I defined earlier in the interpreter!

```python
>>> cylinder_volume(10, 3)
282.7431
```
One useful trick is using the up and down arrow to cycle through your recent commands at the interactive prompt. This can be useful to re-run or adapt code you've already tried.

To quit the Python interactive interpreter, use the command `exit()` or hit `ctrl-D` on mac or linux, and `ctrl-Z` then Enter for windows.

**IPython**

There is actually an awesome alternative to the default Python interactive interpreter, IPython, which comes with many additional features.

* tab completion
* `?` for details about an object
* `!` to execute system shell commands
* syntax highlighting!

and a lot more you can find [here](https://ipython.org/ipython-doc/3/interactive/tutorial.html)!

## Getting the information you need to know

It takes an enormous amount of knowledge to be a skilled programmer. There's libraries to know, syntax to remember, and myriad other details. To add to the difficulty, the technology landscape is constantly shifting as new techniques and tools are invented.

To a novice programmer, learning all of these details and keeping abreast of new developments seems like an impossible task. And it is! Expert programmers who have been working for years don't actually carry an encyclopedia's worth of knowledge in their heads. Instead they have mastered the task of finding information quickly.

## How to Search

Here are some techniques for effective web searching:

* Try using "Python" or the name of the library you're using as the first word of your query. This tells the search engine to prioritize results that are explicitly related to the tools you're using.
* Writing a good search query can take multiple attempts. If you don't find helpful results on your first attempt, try again.
* Try using keywords found on the pages you found in your initial search to direct the search engine to better resources in the subsequent search.
* Copy and paste error messages to use as search terms. This will lead you to explanations of the error and potential causes. An error message might include references to specific line numbers of code that you wrote. Only include the part of the error message that comes before this in your search.
* If you can't find an answer to your question, ask it yourself! Communities like StackOverflow have etiquette rules you must learn if you want to participate, but don't let this stop you from using these resources.

## Hierarchy of Online Resources

While there are many online resources about programming, not all of the them are created equal. This list of resources is in approximate order of reliability.

1. [The Python Tutorial](https://docs.python.org/3/tutorial/) - This section of the official documentation surveys Python's syntax and standard library. It uses examples, and is written using less technical language than the main documentation. Make sure you're reading the Python 3 version of the docs!
2. [The Python Language and Library References](https://docs.python.org/3/index.html) - The Language Reference and Library Reference are more technical than the tutorial, but they are the definitive sources of truth. As you become increasingly acquainted with Python you should use these resources more and more.
3. Third-Party Library Documentation - Third-party libraries publish their documentation on their own websites, and often times at https://readthedocs.org/. You can judge the quality of a third-party library by the quality of its documentation. If the developers haven't found time to write good docs, they probably haven't found the time to polish their library either.
4. The websites and blogs of prominent experts - The previous resources are primary sources, meaning that they are documentation from the same people who wrote the code being documented. Primary sources are the most reliable. Secondary sources are also extremely valuable. The difficulty with secondary sources is determining the credibility of the source. The websites of authors like [Doug Hellmann](https://doughellmann.com/blog/) and developers like [Eli Bendersky](http://eli.thegreenplace.net/) are excellent. The blog of an unknown author might be excellent, or it might be rubbish.
5. [StackOverflow](http://stackoverflow.com/) - This question and answer site has a good amount of traffic, so it's likely that someone has asked (and someone has answered) a related question before! However, answers are provided by volunteers and vary in quality. Always understand solutions before putting them into your program. One line answers without any explanation are dubious. This is a good place to find out more about your question or discover alternative search terms.
6. Bug Trackers - Sometimes you'll encounter a problem so rare, or so new, that no one has addressed it on StackOverflow. You might find a reference to your error in a bug report on GitHub for instance. These bug reports can be helpful, but you'll probably have to do some original engineering work to solve the problem.
7. Random Web Forums - Sometimes your search yields references to forums that haven't been active since 2004, or some similarly ancient time. If these are the only resources that address your problem, you should rethink how you're approaching your solution.

## Advanced Topics

## Iterators and Generators

<iframe width="100%" height="527" src="https://www.youtube.com/embed/tYH8X4Zeh-0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

**Iterables** are objects that can return one of their elements at a time, such as a list. Many of the built-in functions we’ve used so far, like 'enumerate,' return an iterator.

An **iterator** is an object that represents a stream of data. This is different from a list, which is also an iterable, but is not an iterator because it is not a stream of data.

**Generators** are a simple way to create iterators using functions. You can also define iterators using **classes**, which you can read more about [here](https://docs.python.org/3/tutorial/classes.html#iterators).

Here is an example of a generator function called `my_range`, which produces an iterator that is a stream of numbers from 0 to (x - 1).

```python
def my_range(x):
    i = 0
    while i < x:
        yield i
        i += 1
```

Notice that instead of using the return keyword, it uses `yield`. This allows the function to return values one at a time, and start where it left off each time it’s called. This `yield` keyword is what differentiates a generator from a typical function.

Remember, since this returns an iterator, we can convert it to a list or iterate through it in a loop to view its contents. For example, this code:
```python
for x in my_range(5):
    print(x)
```

outputs:

```python
0
1
2
3
4
```
## Why Generators?

You may be wondering why we'd use generators over lists. Here’s an excerpt from a [stack overflow page](https://softwareengineering.stackexchange.com/questions/290231/when-should-i-use-a-generator-and-when-a-list-in-python/290235) that addresses this:

> Generators are a lazy way to build iterables. They are useful when the fully realized list would not fit in memory, or when the cost to calculate each list element is high and you want to do it as late as possible. But they can only be iterated over once.

## Generator Expressions

Here's a cool concept that combines generators and list comprehensions! You can actually create a generator in the same way you'd normally write a list comprehension, except with parentheses instead of square brackets.

For example:

```python
sq_list = [x**2 for x in range(10)]  # this produces a list of squares

sq_iterator = (x**2 for x in range(10))  # this produces an iterator of squares
```

This can help you save time and create efficient code!

## Conclusion

<iframe width="100%" height="527" src="https://www.youtube.com/embed/rEMrswkLvh8" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

[:arrow_up:](#)
