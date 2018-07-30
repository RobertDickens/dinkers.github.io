---
layout: post
title:  "Decorators"
description: "A special syntax to call a function with another function as an argument."
categories: intermediate
---

Decorators are a special syntax to call a function with another function as an argument.

This is done with an `@` symbol just before the definition of the function to be used as an argument for the function declared with the `@` symbol. A comparison example is as follows:

```python
def add(x, y):
	return x + y
add = timer(add)

@timer
def add(x, y):
	return x + y
```

## Wrapper functions

Wrapper functions are the more complex pattern that decorators are used to implement. Wrapper functions are a way of extending a function and increasing it's complexity without changing it.

This can be useful for code that cannot be changed without a large refactor, for keeping a codebase DRY, and for optionally implementing additional functionality across multiple similar functions.

An example of a wrapper function would be a profiling function that displays how long another function took to complete.

```python
from time import time

def timer(function):

	def wrapper(*args, **kwargs)
		before = time()
		function_output = function(*args, **kwargs)
		after = time()
		print("Time taken: {}".format(after - before))
		return function_output

	return wrapper
```

Without decorators, this would be added to a function by redefining it with the following syntax:

```python
def add(x, y):
	return x + y
add = timer(add)
```

However a decorator can be used to make this redefinition of the function more concise and readable:

```python
@timer
def add(x, y):
	return x + y
```

## Advanced use

Decorators can also be passed arguments, however this requires an additional wrapper function.

```python
def run_multiple_times(times_to_run):

	def inner(function):

		def wrapper(*args, **kwargs):
			for _ in range(times_to_run):
				function_output = function(*args, **kwargs)
			return function_output

		return wrapper

	return inner

@run_multiple_times(4)
def add(x, y):
	return x + y
```

This increases complexity due to multiple nested wrapper functions, which makes code harder to read and maintain.


