---
layout: post
title:  "Functions"
description: "A named sequence of statements that perform a computation."
categories: beginner
---

Functions are a named sequence of statements that perform a computation.

## Why use functions

* Naming a group of statements makes a program easier to read and debug
* Allows you to reuse the same code and keep your program DRY (Don't Repeat Yourself)
* Only have to make a change in one place when making adjustments
* Dividing a long program into smaller functions allows the debugging and maintenance of parts one at a time

## Different kinds of functions

**Fruitful functions** - Return a value

**Void functions** - Perform an action (return `None`)

**Generators** - Iterate over an array to return one element at a time

## Incremental development

1. Start with a working program and make small incremental changes. At any point, if there is an error, it should be obvious where it is.
2. Use variables to hold intermediate values to display and check them.
3. Once the program is working, remove some of the scaffolding or consolidate multiple statements into compound expressions, but only if it does not make the program difficult to read.

## Variable length arguments

### Gather

Functions can take a dynamically variable number of arguments. A parameter name beginning with `*` is a **gather** variable, and gathers arguments into a tuple.

```python
>>> def print_all(*args):
... 	print(args)

>>> print_all(1, 2.5, "3")
(1, 2.5, "3")

>>> print_all(1, 2, 3, 4, 5)
(1, 2, 3, 4, 5)
```

### Scatter

A sequence can be passed to a function as multiple arguments. An argument name beginning with a `*` is a **scatter** variable, and scatters a sequence into multiple arguments.

The function `divmod()` takes exactly two arguments, and won't work with a sequence.

```python
>>> arguments = (3, 4)
>>> divmod(arguments)
TypeError: divmod expected 2 arguments, got 1
```

Scattering the arguments inside the tuple will allow this to work.

```python
>>> arguments = (3, 4)
>>> divmod(*arguments)
(0, 3)
```
