---
layout: post
title:  "Membership Testing"
description: "Membership operators test for membership in a sequence."
categories: intermediate
---

Python’s membership operators test for membership in a sequence.

## in

The `in` operator evaluates to `True` if it finds a given variable in the sequence.

```python
>>> a = 1
>>> b = 20
>>> list = [1, 2, 3, 4, 5]

>>> if (a in list):
... 	print("a is available in the given list")
... else:
... 	print("a is not available in the given list")

'a is available in the given list'
```

## not in

The `not in` operator evaluates to `True` if it does not find a given variable in the sequence.

```python
>>> a = 1
>>> b = 20
>>> list = [1, 2, 3, 4, 5]

>>> if (b not in list):
... 	print("b is not available in the given list")
... else:
... 	print("b is available in the given list")

'b is not available in the given list'
```
