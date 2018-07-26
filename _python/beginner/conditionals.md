---
layout: post
title:  "Conditionals"
description: "Behaviour based execution (if statements)."
categories: beginner
---

Also known as the `if` statement, a conditional executes different code depending on the state of the program.

## Conditional execution

```python
if money > 0:
	print("You have money")
```

## Alternative execution

```python
if money > 0:
	print("You have money")

else:
	print("You don't have money")
```

## Chained conditionals

```python
if money > 5:
	print("You have a lot of money")

elif money > 0:
	print("You have money")

else:
	print("You don't have money")
```

## Nested conditionals

```python
if money > 0:

	if money > 5:
		print("You have a lot of money")

	else:
		print("You have money")

else:
	print("You don't have money")
```

## `in` operator

The `in` keyword is a boolean operator that takes two strings and returns `True` if the first appears in the second, otherwise it returns `False`.

```python
>>> "a" in "apple"
True

>>> "seed" in "apple"
False
```

## String comparison with relational operators

Strings can be compared with the same operators used to compare numbers. In this case Python uses lexicographical ordering.

Lexicographical ordering uses the Unicode point number to order individual characters (or ASCII for Python2).

This means that later letters in the alphabet have a higher 'value' than earlier letters. Uppercase letters also have a lower value than their lowercase counter parts.

```python
>>> "a" > "b"
False

>>> "a" < "b"
True

>>> "A" < "b"
True

>>> "a" < "A"
False

>>> "A" < "a"
True
```

Strings containing more than one character are assigned a value that is the sum of the values of the individual characters.
