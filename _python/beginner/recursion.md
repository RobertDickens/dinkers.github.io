---
layout: post
title:  "Recursion"
description: "A function that calls itself until a condition is met."
categories: beginner
---

A recursive function is a function that calls itself until a condition is met.

```python
def countdown(number):

	if number <= 0:
		print("Blast off!")

	else:
		print(number)
		number = number - 1
		countdown(number)
```

A more complicated but practical recursive function:

```python
def factorial(number):

	if number == 0:
		return 1

	else:
		recurse = factorial(number - 1)
		result = number * recurse
		return result
```

**Be wary of infinate recursion. There must always be a way for the function to reach it's terminating condition.**
