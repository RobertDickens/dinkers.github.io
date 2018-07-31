---
layout: post
title:  "Lambda"
description: "A way to define a fruitful anonymous function."
categories: intermediate
---

Lambda is a way to define a fruitful anonymous function. This means a function with no name, that **must** return a value.

A lambda function is defined by it's keyword followed by the function's arguments, then the body of the function.

The following example compares a simple function both in lambda form and traditionally defined.

```python
def square(x):
	return x * x

square = lambda x: x * x
```
There is no need for a return keyword as lambdas always return a value.

## Reason for use

The best reason to use lambda is when a method expects a function as an argument.

```python
def key_definition(x):
    return x[1]

a = [(1, 2), (3, 1), (5, 10), (11, -3)]
a.sort(key=key_definition)
```

If the key definition is only being used once, it can be defined as it is being passed as an argument to the sort method.

```python
a = [(1, 2), (3, 1), (5, 10), (11, -3)]
a.sort(key=lambda x: x[1])
```
