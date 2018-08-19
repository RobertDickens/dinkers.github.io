---
layout: post
title:  "Dynamically Typed"
description: "Downfall of Python being dynamically typed."
categories: intermediate
---

To type check the factorial function it is necessary to write additional conditionals.

```python
def factorial(number):

	if not isinstance(number, int):
		print("Factorial is only designed for integers")
		return None

	elif number < 0:
		print("Factorial is only designed for positive numbers")
		return None

	elif number == 0:
		return 1

	else:
		recurse = factorial(number - 1)
		result = number * recurse
		return result
```

Without these, a decimal number or a negative integer would result in the terminating conditional never being reached and the recursive function to run indefinitely.
