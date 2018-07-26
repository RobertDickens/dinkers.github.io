---
layout: post
title:  "Variables"
description: "A storage location for a mutable value."
categories: beginner
---

## Reassignment

A new assignment makes an existing variable refer to a new value.

```python
>>> number = 5
>>> print(number)
5
>>> number = 7
>>> print(number)
7
```

An assignment can make two variables equal, but they don't have to stay that way.

```python
>>> first_number = 5
>>> second_number = first_number
>>> first_number = 3
>>> print(second_number)
5
```

It is possible to update a variable, but only if it already exists. Python evaluates the right side of the assignment before assigning the resulting value to the variable name.

```python
X undefined_number = undefined_number + 1

  defined_number = 0
√ defined_number = defined_number + 1
```

## Global variables

Variables belonging to the `__main__` frame are called **global** as they are not local to any function.

```python
verbose = True

def example_function():

	if verbose:
		print("Running example function")
```

Reading a global variable from inside a function (or a more nested scope) does not require any special syntax. However assigning to a global variable from anywhere other than the `__main__` frame requires the global variable to assigned specifically before it can be used.

```python
has_been_run = True

def example_function_two():

	global has_been_run
	has_been_run = False
```

Trying to assign one without this definition will result in an unbound local error.

```python
UnboundLocalError: local variable 'has_been_run' referenced before assignment
```

**This rule does not apply to mutable variables. They can be modified without declaring the variable as global.**

## Memos

A previously computed value that is stored for later use is called a **memo**. The computation is memorised and stored for efficiency.

For example, memos can be used in a Fibonacci calculating function to save processing power when calculating large numbers, as the Fibonacci function will be run repeatedly for the smaller numbered functions.

```python
known = {0:0, 1:1}

def fibonacci(number):

	if number in known:
		return known[number]

	result = fibonacci(number - 1) + fibonacci(number -2)
	known[number] = result

	return result
```
