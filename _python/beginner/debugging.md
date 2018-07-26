---
layout: post
title:  "Debugging"
description: "Tips for debugging a Python programming problem."
categories: beginner
---

## If a function is not working, there are three possibilities to consider:

* There is something wrong with the arguments the function is getting; a pre-condition is violated.
* There is something wrong with the function; a post-condition is violated.
* There is something wrong with the return value or the way it is being used.

## Common solutions to these problems

### Scale down the input

Working with big data sets can present difficulties when debugging simply due to their unwieldy size. Using a sample of the input makes it more manageable and understandable, which will make it easier to deduce how the error is occurring.

Reducing the sample size deliberately and specifically could also be a good way to find where the error is occurring.

### Check summaries and types

Printing a summary of data could make the error more obvious, for example the number of items in a dictionary, or the sum of numbers in a list.

Checking types is also a useful thing to check, especially the different types of arrays.

### Sanity checks

Sanity checks are common sense checks placed in code to made sure things are still within the expected range of results.

An example would be when calculating the average of a list of numbers, writing code to check that the average is not smaller than the smallest number or bigger than the biggest number.

### Format the output

Formatting the output into a more easily read form makes it easier to spot errors. The module `pprint` (pretty print) is a common tool used to do this.

## Catch exceptions

Semantic errors can occur when correct syntax is being used incorrectly.

```python
>>> file_example = open("non_existent_file")
IOError: [Errno 2] No such file or directory: "non_existent_file"

>>> file_example = open("/home")
IsADirectoryError: [Errno 21] Is a directory: "/home"
```

To anticipate errors that may occur and have the application behave differently based on these errors, it is useful to write `try/except` statements.

```python
try:
	file_example = open(file_path)
except IsADirectoryError:
	print("The provided file_path {} is a directory and cannot be opened.".format(file_path))
```

## String introspection

When reading and writing to files, whitespace may create unexpected behaviour. These errors can be hard to debug because of their invisible nature.

```python
>>> example_string = "1 2\t 3\n 4"
>>> print(example_string)
1 2    3
4
```

The built-in function `repr()` can help. It takes any object as an argument and returns a string representation of the object. For a string, it will print the representation of the string, rather than the interpreted string.

```python
>>> print(repr(example_string))
'1 2\t 3\n 4'
```
