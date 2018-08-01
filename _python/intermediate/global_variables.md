---
layout: post
title:  "Global Variables"
description: "Variables that can be used independent of function scope."
categories: intermediate
---

Global variables are used to access values with no regard to scope.

```python
soup_of_the_day = "Tomato"

def print_soup():
	global soup_of_the_day
	print(soup_of_the_day)
	
print_soup()  # Tomato
```

This can be useful when variables are important to many different parts of an application, and can save the overhead of passing variables between functions.

```python
functions_run = 0

def function_one(number):
	
	global functions_run
	functions_run += 1
	
	return number * number
	
def function_two(string):

	global functions_run
	functions_run += 1
	
	return string + string
	

result_one = function_one(5)
result_two = function_two("kayra")

print(functions_run)  # This will return 2
```

The overhead of passing variables between functions is clear when global variables are not used:

```python
functions_run = 0

def function_one(number, functions_run):
	
	functions_run += 1
	
	return number * number, functions_run
	
def function_two(string, functions_run):

	functions_run += 1
	
	return string + string, functions_run
	

result_one = function_one(5, functions_run)
result_two = function_two("kayra", functions_run)

print(functions_run)  # This will return 2
```

Be wary of using this feature rashly. Using global variables can make code hard to read, and prone to bugs as it can be unclear where a variable is being changed.